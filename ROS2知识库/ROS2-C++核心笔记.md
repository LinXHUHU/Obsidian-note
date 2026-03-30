# ROS 2 Jazzy C++ 核心笔记

> 来源: https://docs.ros.org/en/jazzy/Tutorials.html
> 整理日期: 2026-03-31

---

## 1. 发布者与订阅者 (Publisher/Subscriber)

### 核心概念
- **节点**是可执行进程，通过ROS图通信
- **话题**是节点间传递消息的通道
- 发布者(Publisher)发送数据，订阅者(Subscriber)接收数据

### 关键代码结构

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

class MinimalPublisher : public rclcpp::Node
{
public:
    MinimalPublisher() : Node("minimal_publisher"), count_(0)
    {
        // 创建发布者: 话题名"topic", 队列大小10
        publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
        
        // 创建定时器: 500ms周期
        timer_ = this->create_wall_timer(500ms, timer_callback);
    }

private:
    rclcpp::TimerBase::SharedPtr timer_;
    rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
    size_t count_;
};

// main函数标准模板
int main(int argc, char * argv[])
{
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<MinimalPublisher>());
    rclcpp::shutdown();
    return 0;
}
```

### 关键API
| API | 作用 |
|-----|------|
| `create_publisher<T>()` | 创建发布者 |
| `create_subscription<T>()` | 创建订阅者 |
| `create_wall_timer()` | 创建定时器 |
| `rclcpp::spin()` | 启动节点事件循环 |
| `RCLCPP_INFO()` | 日志输出 |

---

## 2. 服务与客户端 (Service/Client)

### 核心概念
- **服务**是同步通信，请求-响应模式
- 客户端(Client)发送请求，服务端(Server)返回响应
- 使用`.srv`文件定义请求/响应结构

### 服务端代码

```cpp
#include "example_interfaces/srv/add_two_ints.hpp"

// 服务回调函数
void add(const std::shared_ptr<example_interfaces::srv::AddTwoInts::Request> request,
         std::shared_ptr<example_interfaces::srv::AddTwoInts::Response> response)
{
    response->sum = request->a + request->b;
}

int main(int argc, char **argv)
{
    rclcpp::init(argc, argv);
    auto node = rclcpp::Node::make_shared("add_two_ints_server");
    
    // 创建服务
    auto service = node->create_service<example_interfaces::srv::AddTwoInts>(
        "add_two_ints", &add);
    
    rclcpp::spin(node);
    rclcpp::shutdown();
}
```

### 客户端代码要点
```cpp
// 创建客户端
auto client = node->create_client<example_interfaces::srv::AddTwoInts>("add_two_ints");

// 等待服务可用
while (!client->wait_for_service(1s)) {
    if (!rclcpp::ok()) return;
}

// 发送异步请求
auto result = client->async_send_request(request);
```

---

## 3. 参数 (Parameters)

### 核心概念
- 参数可在运行时从launch文件或命令行设置
- 支持类型推断（从默认值推断类型）

### 代码示例

```cpp
class MinimalParam : public rclcpp::Node
{
public:
    MinimalParam() : Node("minimal_param_node")
    {
        // 声明参数: 名称 + 默认值
        this->declare_parameter("my_parameter", "world");
        
        // 获取参数值
        std::string my_param = this->get_parameter("my_parameter").as_string();
        
        // 设置参数值
        std::vector<rclcpp::Parameter> all_new_parameters{
            rclcpp::Parameter("my_parameter", "new_value")
        };
        this->set_parameters(all_new_parameters);
    }
};
```

### 参数描述符（可选）
```cpp
auto param_desc = rcl_interfaces::msg::ParameterDescriptor{};
param_desc.description = "This parameter is mine!";
this->declare_parameter("my_parameter", "world", param_desc);
```

---

## 4. 插件 (Pluginlib)

### 核心概念
- 动态加载类，无需显式链接库
- 基类定义接口，插件类实现具体功能

### 实现步骤

**1. 定义基类（抽象类）**
```cpp
namespace polygon_base
{
    class RegularPolygon
    {
    public:
        virtual void initialize(double side_length) = 0;
        virtual double area() = 0;
        virtual ~RegularPolygon(){}
    };
}
```

**2. 实现插件类**
```cpp
#include <pluginlib/class_list_macros.hpp>

namespace polygon_plugins
{
    class Square : public polygon_base::RegularPolygon
    {
    public:
        void initialize(double side_length) override { ... }
        double area() override { ... }
    };
}

// 注册插件
PLUGINLIB_EXPORT_CLASS(polygon_plugins::Square, polygon_base::RegularPolygon)
```

**3. 插件声明文件 (plugins.xml)**
```xml
<library path="polygon_plugins">
    <class type="polygon_plugins::Square" base_class_type="polygon_base::RegularPolygon">
        <description>Square plugin</description>
    </class>
</library>
```

---

## 5. Action 服务器与客户端

### 核心概念
- **Action**是异步通信，支持目标、反馈、结果
- 适合长时间运行的任务（如导航、机械臂运动）
- 可取消正在执行的目标

### Action 服务端要点

```cpp
#include "rclcpp_action/rclcpp_action.hpp"

class FibonacciActionServer : public rclcpp::Node
{
    using Fibonacci = custom_action_interfaces::action::Fibonacci;
    using GoalHandleFibonacci = rclcpp_action::ServerGoalHandle<Fibonacci>;

public:
    FibonacciActionServer() : Node("fibonacci_action_server")
    {
        // 创建Action服务器
        this->action_server_ = rclcpp_action::create_server<Fibonacci>(
            this,
            "fibonacci",
            std::bind(&FibonacciActionServer::handle_goal, this, _1, _2),
            std::bind(&FibonacciActionServer::handle_cancel, this, _1),
            std::bind(&FibonacciActionServer::handle_accepted, this, _1));
    }

private:
    // 处理目标请求
    rclcpp_action::GoalResponse handle_goal(...)
    {
        return rclcpp_action::GoalResponse::ACCEPT_AND_EXECUTE;
    }
    
    // 处理取消请求
    rclcpp_action::CancelResponse handle_cancel(...)
    {
        return rclcpp_action::CancelResponse::ACCEPT;
    }
    
    // 执行目标（在新线程中）
    void execute(const std::shared_ptr<GoalHandleFibonacci> goal_handle)
    {
        // 发布反馈
        goal_handle->publish_feedback(feedback);
        
        // 检查取消
        if (goal_handle->is_canceling()) {
            goal_handle->canceled(result);
            return;
        }
        
        // 成功完成
        goal_handle->succeed(result);
    }
};
```

### 关键回调

| 回调 | 作用 |
|------|------|
| `handle_goal` | 接收目标请求，决定是否接受 |
| `handle_cancel` | 接收取消请求 |
| `handle_accepted` | 目标被接受后开始执行 |

---

## 6. 可组合节点 (Composable Node)

### 核心概念
- 多个节点运行在同一进程，实现**零拷贝通信**
- 使用 `rclcpp_components` 实现组件化
- 通过容器动态加载/组合节点

### 改造步骤

**1. 修改构造函数**
```cpp
// 原: VincentDriver() : Node("vincent_driver")
// 改为:
VincentDriver(const rclcpp::NodeOptions & options) 
    : Node("vincent_driver", options)
{
    // ...
}
```

**2. 移除 main 函数，添加注册宏**
```cpp
#include <rclcpp_components/register_node_macro.hpp>
RCLCPP_COMPONENTS_REGISTER_NODE(palomino::VincentDriver)
```

**3. CMakeLists.txt 修改**
```cmake
find_package(rclcpp_components REQUIRED)

# 改为库而不是可执行文件
add_library(vincent_driver_component SHARED src/vincent_driver.cpp)
ament_target_dependencies(vincent_driver_component "rclcpp_components" ...)

# 注册节点
rclcpp_components_register_node(
    vincent_driver_component
    PLUGIN "palomino::VincentDriver"
    EXECUTABLE vincent_driver
)
```

**4. Launch 文件使用**
```python
from launch_ros.actions import ComposableNodeContainer
from launch_ros.descriptions import ComposableNode

ComposableNodeContainer(
    name='container',
    package='rclcpp_components',
    executable='component_container',  # 或 component_container_mt (多线程)
    composable_node_descriptions=[
        ComposableNode(
            package='palomino',
            plugin='palomino::VincentDriver',
            name='vincent_driver',
            extra_arguments=[{'use_intra_process_comms': True}],  # 启用进程内通信
        ),
    ]
)
```

---

## 7. 话题统计 (Topic Statistics)

### 核心概念
- 测量订阅接收消息的统计信息
- 用于系统性能分析和问题诊断

### 启用统计

```cpp
#include "rclcpp/subscription_options.hpp"

class MinimalSubscriberWithTopicStatistics : public rclcpp::Node
{
public:
    MinimalSubscriberWithTopicStatistics() : Node("minimal_subscriber_with_topic_statistics")
    {
        auto options = rclcpp::SubscriptionOptions();
        
        // 启用话题统计
        options.topic_stats_options.state = rclcpp::TopicStatisticsState::Enable;
        
        // 配置发布周期 (默认1s)
        options.topic_stats_options.publish_period = std::chrono::seconds(10);
        
        // 配置统计话题名 (默认"/statistics")
        // options.topic_stats_options.publish_topic = "/my_statistics";
        
        subscription_ = this->create_subscription<std_msgs::msg::String>(
            "topic", 10, callback, options);
    }
};
```

### 配置选项
| 选项 | 说明 | 默认值 |
|------|------|--------|
| `state` | 启用/禁用统计 | Disable |
| `publish_period` | 统计发布周期 | 1s |
| `publish_topic` | 统计话题名 | /statistics |

---

## 8. 常用依赖包

```xml
<!-- package.xml -->
<depend>rclcpp</depend>
<depend>rclcpp_action</depend>
<depend>rclcpp_components</depend>
<depend>std_msgs</depend>
<depend>example_interfaces</depend>
<depend>pluginlib</depend>
```

```cmake
# CMakeLists.txt
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(std_msgs REQUIRED)

ament_target_dependencies(your_target
    rclcpp
    std_msgs
)
```

---

## 9. 学习路径

```
第一阶段: 基础
├── Publisher/Subscriber
├── Service/Client
└── Parameters

第二阶段: 进阶
├── Pluginlib
├── Action Server/Client
└── Composable Nodes

第三阶段: 优化
├── Topic Statistics
├── Memory Allocator
└── Real-time Programming
```
