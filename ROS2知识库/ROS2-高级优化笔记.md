# ROS 2 高级优化笔记

---

## 1. 内存分配器 (Memory Allocator)

### 为什么需要自定义分配器
- 减少内存碎片
- 避免动态分配开销
- 实时系统要求确定性

### 使用示例
```cpp
#include "rclcpp/strategies/allocator_memory_strategy.hpp"
#include "rcutils/allocator.h"

template<typename T = void>
struct MyAllocator {
    // 自定义分配逻辑
    T* allocate(size_t size) {
        return static_cast<T*>(malloc(size * sizeof(T)));
    }
    
    void deallocate(T* ptr, size_t size) {
        free(ptr);
    }
};

// 在节点中使用
using Alloc = MyAllocator<void>;
using MessageAllocTraits = rclcpp::allocator::AllocRebind<std_msgs::msg::UInt8, Alloc>;
using MessageAlloc = MessageAllocTraits::allocator_type;

auto alloc = std::make_shared<Alloc>();
rclcpp::PublisherOptionsWithAllocator<Alloc> publisher_options;
publisher_options.allocator = alloc;

auto publisher = node->create_publisher<std_msgs::msg::UInt8>(
    "topic", 10, publisher_options);
```

---

## 2. 实时编程 (Real-time)

### 实时性要求
- 确定性延迟
- 无内存分配
- 优先级调度

### 关键配置
```cpp
// 设置实时优先级
struct sched_param param;
param.sched_priority = 80;  // 实时优先级
sched_setscheduler(0, SCHED_FIFO, &param);

// 锁定内存
mlockall(MCL_CURRENT | MCL_FUTURE);
```

### 实时安全编程原则
1. 初始化阶段完成所有分配
2. 运行时避免 malloc/free
3. 使用预分配的消息池
4. 避免动态数据结构

---

## 3. 数据记录 (Rosbag2)

### 从节点录制
```cpp
#include "rosbag2_cpp/writer.hpp"

class BagRecorder : public rclcpp::Node
{
    std::unique_ptr<rosbag2_cpp::Writer> writer_;
    rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;

public:
    BagRecorder() : Node("bag_recorder")
    {
        writer_ = std::make_unique<rosbag2_cpp::Writer>();
        writer_->open("my_bag");
        
        subscription_ = create_subscription<std_msgs::msg::String>(
            "topic", 10,
            [this](std::shared_ptr<rclcpp::SerializedMessage> msg) {
                writer_->write(msg, "topic", "std_msgs/msg/String", this->now());
            });
    }
};
```

### 从 Bag 读取
```cpp
#include "rosbag2_cpp/reader.hpp"

rosbag2_cpp::Reader reader;
reader.open("my_bag");

while (reader.has_next()) {
    auto msg = reader.read_next();
    // 处理消息
}
```

---

## 4. DDS 配置

### Fast DDS 发现服务器
```bash
# 启动发现服务器
fastdds discovery -i 0 -l 127.0.0.1 -p 11811
```

### 环境变量配置
```bash
export ROS_DISCOVERY_SERVER="127.0.0.1:11811"
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
```

### XML 配置
```xml
<!-- DEFAULT_FASTRTPS_PROFILES.xml -->
<profiles>
    <participant profile_name="participant_profile">
        <rtps>
            <builtin>
                <discovery_config>
                    <discoveryProtocol>SERVER</discoveryProtocol>
                    <discoveryServersList>
                        <RemoteServer prefix="44.53.00.5f.45.50.52.4f.53.49.4d.41">
                            <metatrafficUnicastLocatorList>
                                <locator>
                                    <udpv4>
                                        <address>127.0.0.1</address>
                                        <port>11811</port>
                                    </udpv4>
                                </locator>
                            </metatrafficUnicastLocatorList>
                        </RemoteServer>
                    </discoveryServersList>
                </discovery_config>
            </builtin>
        </rtps>
    </participant>
</profiles>
```

---

## 5. 性能优化技巧

### 消息序列化优化
- 使用 `rclcpp::SerializedMessage` 避免重复序列化
- 进程内通信使用 `unique_ptr` 实现零拷贝

### 执行器优化
```cpp
// 单线程执行器 (默认)
rclcpp::spin(node);

// 多线程执行器
rclcpp::executors::MultiThreadedExecutor executor;
executor.add_node(node);
executor.spin();

// 静态单线程执行器 (最高效)
rclcpp::executors::StaticSingleThreadedExecutor executor;
executor.add_node(node);
executor.spin();
```

### 订阅者优化
```cpp
// 使用消息池
rclcpp::SubscriptionOptions options;
options.use_intra_process_comm = rclcpp::IntraProcessSetting::Enable;

// 批量处理
callback_group_ = node->create_callback_group(
    rclcpp::CallbackGroupType::MutuallyExclusive);
```

---

## 6. 调试与追踪

### ros2_tracing
```bash
# 安装
sudo apt install ros-jazzy-ros2trace

# 追踪会话
ros2 trace start my_session
# 运行节点
ros2 trace stop

# 分析
tracetools_analysis process my_session
```

### 性能分析
```bash
# 查看节点统计
ros2 node info /node_name

# 查看话题统计
ros2 topic info -v /topic_name

# 查看系统拓扑
ros2 doctor --report
```

---

## 7. 安全 (Security)

### 启用安全
```bash
# 生成安全文件
ros2 security create_keystore keystore
ros2 security create_key keystore /node_name

# 启动安全节点
export ROS_SECURITY_ENABLE=true
export ROS_SECURITY_STRATEGY=Enforce
ros2 run package node
```

### 访问控制
```xml
<!-- policy.xml -->
<policy version="0.2.0">
    <enclaves>
        <enclave path="/node_name">
            <profiles>
                <profile ns="/" node="node_name">
                    <topics publish="ALLOW" subscribe="DENY">
                        <topic>topic_name</topic>
                    </topics>
                </profile>
            </profiles>
        </enclave>
    </enclaves>
</policy>
```

---

## 8. 多机部署

### 网络配置
```bash
# 设置域ID (隔离不同网络)
export ROS_DOMAIN_ID=42

# 设置网络接口
export ROS_LOCALHOST_ONLY=0
```

### 发现配置
```bash
# 使用广播
export ROS_AUTOMATIC_DISCOVERY_RANGE=SUBNET

# 使用本地回环
export ROS_AUTOMATIC_DISCOVERY_RANGE=LOCALHOST

# 禁用发现
export ROS_AUTOMATIC_DISCOVERY_RANGE=OFF
```

---

## 9. 容器化部署

### Dockerfile 示例
```dockerfile
FROM ros:jazzy-ros-base

WORKDIR /ros2_ws
COPY src/ src/

RUN rosdep install --from-paths src --ignore-src -y && \
    colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release

CMD ["ros2", "launch", "package", "launch.py"]
```

### Docker Compose
```yaml
version: '3'
services:
  ros2_app:
    build: .
    network_mode: host
    environment:
      - ROS_DOMAIN_ID=42
    volumes:
      - /dev/shm:/dev/shm
```

---

## 10. 性能基准

### 延迟测试
```cpp
// 发布-订阅延迟测量
auto start = std::chrono::high_resolution_clock::now();
publisher->publish(msg);
// 在回调中
auto end = std::chrono::high_resolution_clock::now();
auto latency = std::chrono::duration_cast<std::chrono::microseconds>(end - start);
```

### 吞吐量测试
```bash
# 使用 ros2 topic bw
ros2 topic bw /topic

# 使用 ros2 topic hz
ros2 topic hz /topic
```

### 典型性能指标
| 配置 | 延迟 | 吞吐量 |
|------|------|--------|
| 进程内 | ~1μs | >1M msg/s |
| 共享内存 | ~10μs | >100K msg/s |
| 网络 | ~100μs | >10K msg/s |
