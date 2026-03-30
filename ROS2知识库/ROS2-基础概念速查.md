# ROS 2 基础概念速查

---

## 节点 (Node)

### 定义
- 执行计算的基本单元
- 一个进程可包含多个节点
- 通过话题、服务、动作通信

### 创建节点
```cpp
auto node = rclcpp::Node::make_shared("node_name");
// 或继承方式
class MyNode : public rclcpp::Node {
    MyNode() : Node("node_name") {}
};
```

---

## 话题 (Topic)

### 特点
- 发布/订阅模式
- 多对多通信
- 单向数据流

### 常用命令
```bash
ros2 topic list          # 列出所有话题
ros2 topic echo /topic   # 查看话题内容
ros2 topic hz /topic     # 查看发布频率
ros2 topic bw /topic     # 查看带宽
```

---

## 服务 (Service)

### 特点
- 请求/响应模式
- 一对一通信
- 同步调用

### 常用命令
```bash
ros2 service list              # 列出所有服务
ros2 service call /service type {data}  # 调用服务
ros2 service type /service     # 查看服务类型
```

---

## 动作 (Action)

### 特点
- 目标/反馈/结果模式
- 长时间运行任务
- 支持取消

### 文件结构
```
.action 文件格式:
---
# Goal
int32 order
---
# Result
int32[] sequence
---
# Feedback
int32[] partial_sequence
```

---

## 参数 (Parameter)

### 特点
- 节点配置
- 运行时修改
- 支持类型: bool, int, double, string, byte[], bool[], int[], double[], string[]

### 常用命令
```bash
ros2 param list                    # 列出所有参数
ros2 param get /node param_name    # 获取参数值
ros2 param set /node param_name value  # 设置参数
ros2 param dump /node              # 导出参数
```

---

## Launch 文件

### Python Launch 示例
```python
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='package_name',
            executable='executable_name',
            name='node_name',
            parameters=[{'param_name': 'value'}],
            remappings=[('/old_topic', '/new_topic')]
        )
    ])
```

---

## 常用工具

| 工具 | 用途 |
|------|------|
| `ros2 node` | 节点管理 |
| `ros2 topic` | 话题管理 |
| `ros2 service` | 服务管理 |
| `ros2 param` | 参数管理 |
| `ros2 action` | 动作管理 |
| `ros2 bag` | 数据记录/回放 |
| `ros2 doctor` | 诊断问题 |
| `rqt` | GUI工具 |
| `rviz2` | 可视化 |

---

## 工作空间结构

```
ros2_ws/
├── build/          # 编译输出
├── install/        # 安装文件
├── log/            # 日志
└── src/            # 源码
    └── package_name/
        ├── include/
        ├── src/
        ├── CMakeLists.txt
        └── package.xml
```

---

## 常用 CMake 模板

```cmake
cmake_minimum_required(VERSION 3.8)
project(package_name)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(node_name src/node.cpp)
ament_target_dependencies(node_name rclcpp std_msgs)

install(TARGETS node_name
    DESTINATION lib/${PROJECT_NAME})

ament_package()
```

---

## 常用 package.xml 模板

```xml
<?xml version="1.0"?>
<package format="3">
  <name>package_name</name>
  <version>0.0.1</version>
  <description>Package description</description>
  <maintainer email="email@example.com">Name</maintainer>
  <license>Apache-2.0</license>

  <buildtool_depend>ament_cmake</buildtool_depend>
  <depend>rclcpp</depend>
  <depend>std_msgs</depend>

  <test_depend>ament_lint_auto</test_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```
