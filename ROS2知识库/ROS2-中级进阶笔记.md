# ROS 2 中级进阶笔记

---

## 1. 自定义消息/服务/动作

### 创建接口包

```bash
ros2 pkg create --build-type ament_cmake --license Apache-2.0 custom_interfaces
```

### msg 文件
```
# MyMessage.msg
int64 x
int64 y
string name
float64 confidence
```

### srv 文件
```
# MyService.srv
int64 a
int64 b
---
int64 sum
```

### action 文件
```
# MyAction.action
int32 target
---
int32 result
---
int32 progress
```

### CMakeLists.txt 配置
```cmake
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
    "msg/MyMessage.msg"
    "srv/MyService.srv"
    "action/MyAction.action"
)

ament_export_dependencies(rosidl_default_runtime)
```

---

## 2. 参数回调与监控

### 参数变化回调

```cpp
class ParameterNode : public rclcpp::Node
{
public:
    ParameterNode() : Node("parameter_node")
    {
        // 声明参数
        this->declare_parameter("my_param", 1.0);
        
        // 设置参数回调
        param_callback_handle_ = this->add_on_set_parameters_callback(
            std::bind(&ParameterNode::parameters_callback, this, _1));
    }

private:
    rclcpp::node_interfaces::OnSetParametersCallbackHandle::SharedPtr param_callback_handle_;
    
    rcl_interfaces::msg::SetParametersResult parameters_callback(
        const std::vector<rclcpp::Parameter> &parameters)
    {
        rcl_interfaces::msg::SetParametersResult result;
        result.successful = true;
        
        for (const auto &param : parameters) {
            RCLCPP_INFO(this->get_logger(), "Parameter %s changed", param.get_name().c_str());
        }
        
        return result;
    }
};
```

---

## 3. 节点生命周期 (Managed Nodes)

### 状态机
```
Unconfigured → Configuring → Inactive → Activating → Active
                    ↑__________|___________|_________|
                    |          |           |
                  Cleaning   Cleaning    Deactivating
```

### 生命周期节点要点
- 使用 `rclcpp_lifecycle` 包
- 需要显式配置和激活
- 支持状态转换回调

---

## 4. TF2 坐标变换

### 发布 TF
```cpp
#include "tf2_ros/transform_broadcaster.h"

class TFPublisher : public rclcpp::Node
{
    tf2_ros::TransformBroadcaster tf_broadcaster_;
    
    void publish_tf() {
        geometry_msgs::msg::TransformStamped t;
        t.header.stamp = this->get_clock()->now();
        t.header.frame_id = "parent_frame";
        t.child_frame_id = "child_frame";
        t.transform.translation.x = 1.0;
        t.transform.rotation.w = 1.0;
        tf_broadcaster_.sendTransform(t);
    }
};
```

### 监听 TF
```cpp
#include "tf2_ros/buffer.h"
#include "tf2_ros/transform_listener.h"

tf2_ros::Buffer tf_buffer(this->get_clock());
tf2_ros::TransformListener tf_listener(tf_buffer);

// 查询变换
try {
    auto transform = tf_buffer.lookupTransform(
        "target_frame", "source_frame", tf2::TimePointZero);
} catch (tf2::TransformException &ex) {
    RCLCPP_WARN(this->get_logger(), "Transform error: %s", ex.what());
}
```

---

## 5. QoS (服务质量)

### QoS 配置
```cpp
// 可靠通信 (默认)
auto qos = rclcpp::QoS(10).reliable();

// 尽力而为 (适合传感器数据)
auto qos = rclcpp::QoS(10).best_effort();

// 持久化 (适合地图等)
auto qos = rclcpp::QoS(1).transient_local();

// 自定义
auto qos = rclcpp::QoS(10)
    .reliable()
    .durability_volatile()
    .deadline(std::chrono::milliseconds(100));
```

### QoS 策略
| 策略 | 选项 | 用途 |
|------|------|------|
| Reliability | Reliable / Best Effort | 可靠性 vs 性能 |
| Durability | Volatile / Transient Local | 历史数据保留 |
| History | Keep Last / Keep All | 缓存策略 |
| Deadline | 时间值 | 数据时效性 |
| Lifespan | 时间值 | 数据有效期 |

---

## 6. 进程内通信 (Intra-process)

### 启用条件
- 使用 ComposableNodeContainer
- 设置 `use_intra_process_comms: True`
- 使用 `unique_ptr` 发布消息

### 代码示例
```cpp
// 发布者使用 unique_ptr
auto msg = std::make_unique<std_msgs::msg::String>();
msg->data = "Hello";
publisher_->publish(std::move(msg));

// 订阅者接收 const shared_ptr
void callback(const std_msgs::msg::String::SharedPtr msg) {
    // 零拷贝接收
}
```

---

## 7. 日志系统

### 日志级别
```cpp
RCLCPP_DEBUG(this->get_logger(), "Debug message");
RCLCPP_INFO(this->get_logger(), "Info message");
RCLCPP_WARN(this->get_logger(), "Warn message");
RCLCPP_ERROR(this->get_logger(), "Error message");
RCLCPP_FATAL(this->get_logger(), "Fatal message");
```

### 设置日志级别
```bash
ros2 run package node --ros-args --log-level DEBUG
ros2 run package node --ros-args --log-level node_name:=DEBUG
```

---

## 8. 测试

### 单元测试
```cpp
#include <gtest/gtest.h>
#include "rclcpp/rclcpp.hpp"

TEST(MyTestSuite, test_name) {
    rclcpp::init(0, nullptr);
    auto node = std::make_shared<rclcpp::Node>("test_node");
    
    // 测试代码
    
    rclcpp::shutdown();
}

int main(int argc, char **argv) {
    testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

### CMake 配置
```cmake
find_package(ament_cmake_gtest REQUIRED)
ament_add_gtest(test_name test/test_file.cpp)
```

---

## 9. 常用设计模式

### 组件化设计
```
系统 = 容器 + 组件1 + 组件2 + ...
```

### 节点组合
- 独立进程: 容错性好，适合分布式
- 同一进程: 性能高，适合通信密集型

### 推荐架构
```
┌─────────────────────────────────────┐
│         ComposableNodeContainer      │
│  ┌─────────┐  ┌─────────┐           │
│  │ Sensor  │  │ Planner │           │
│  │ Driver  │  │ Node    │           │
│  └────┬────┘  └────┬────┘           │
│       │            │                 │
│       └────────────┘                 │
│              │                       │
│       ┌──────┴──────┐                │
│       │  Controller │                │
│       │    Node     │                │
│       └─────────────┘                │
└─────────────────────────────────────┘
```
