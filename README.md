# Neuro-Nav: Hybrid Embodied Intelligence Framework

[![ROS 2](https://img.shields.io/badge/ROS_2-Humble%2FJazzy-22314E?logo=ros)](https://docs.ros.org/)
[![Simulation](https://img.shields.io/badge/Simulation-Isaac_Sim_4.0+-76B900?logo=nvidia)](https://developer.nvidia.com/isaac-sim)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

> **Where Geometric Precision meets Semantic Understanding.**
>
> 传统的 SLAM 赋予机器人“小脑”，保证其在物理世界中的定位与避障；大模型赋予机器人“大脑”，使其理解环境语义与物理属性。Neuro-Nav 是一个基于 ROS 2 和 NVIDIA Isaac Sim 的混合架构框架，旨在探索 **Geometric SLAM** 与 **Vision-Language Models (VLM)** 的最佳工程化互补实践。

## 🏗 System Architecture (v1.0 Skeleton)

v1.0 版本的核心目标是**搭建稳健的仿真基座**，打通 Isaac Sim 到 ROS 2 的数据闭环，并为后续的 VLM (Vision-Language Model) 和 RL (Reinforcement Learning) 模块预留标准接口。
# Neuro-Nav: Hybrid Embodied Intelligence Framework

[![ROS 2](https://img.shields.io/badge/ROS_2-Humble%2FJazzy-22314E?logo=ros)](https://docs.ros.org/)
[![Simulation](https://img.shields.io/badge/Simulation-Isaac_Sim_4.0+-76B900?logo=nvidia)](https://developer.nvidia.com/isaac-sim)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

> **Where Geometric Precision meets Semantic Understanding.**
>
> 传统的 SLAM 赋予机器人“小脑”，保证其在物理世界中的定位与避障；大模型赋予机器人“大脑”，使其理解环境语义与物理属性。Neuro-Nav 是一个基于 ROS 2 和 NVIDIA Isaac Sim 的混合架构框架，旨在探索 **Geometric SLAM** 与 **Vision-Language Models (VLM)** 的最佳工程化互补实践。

## 🏗 System Architecture (v1.0 Skeleton)

v1.0 版本的核心目标是**搭建稳健的仿真基座**，打通 Isaac Sim 到 ROS 2 的数据闭环，并为后续的 VLM (Vision-Language Model) 和 RL (Reinforcement Learning) 模块预留标准接口。

graph TD
    subgraph Physical_World ["Isaac Sim (Physical World)"]
        SimRobot["Robot: Carter V2"]
        SimSensors["Lidar + RGB-D + IMU"]
        SimScene["Home/Office Environment"]
    end

    subgraph ROS2_Bridge ["ROS 2 Middleware (Bridge)"]
        ActionGraph["Isaac ROS Bridge"]
    end

    subgraph Geometric_Layer ["The Cerebellum (Geometric Layer)"]
        SLAM["SLAM Toolbox"]
        Nav2["Nav2 Stack (Planner/Controller)"]
        Odom["Odometry"]
    end

    subgraph Semantic_Layer ["The Brain (Semantic Layer - Interfaces Ready)"]
        style Semantic_Layer stroke-dasharray: 5 5
        VLM_Node["VLM Perception Node (Placeholder)"]
        Sem_Map["Semantic Map Interface"]
    end

    %% Data Flow
    SimSensors --> ActionGraph
    ActionGraph -->|/scan, /rgb, /depth| SLAM
    ActionGraph -->|/odom| Nav2
    
    SLAM -->|/map| Nav2
    Nav2 -->|/cmd_vel| ActionGraph
    ActionGraph --> SimRobot

    %% Future Interfaces
    ActionGraph -.->|/rgb_image| VLM_Node
    VLM_Node -.->|Semantic Constraints| Nav2

🚀 Features (v1.0)
High-Fidelity Simulation: 基于 NVIDIA Isaac Sim 的光追仿真环境，为后续 VLM 视觉感知提供“保真”数据（避免 Sim-to-Real Gap）。

Robust Navigation Stack: 集成 ROS 2 Nav2 和 SLAM Toolbox，实现高精度的几何建图与导航。

Modular Design: 采用分层架构设计，将“感知”、“决策”、“控制”解耦。

Future-Proof Interfaces: 在 neuro_nav_interfaces 中预定义了语义导航所需的自定义消息类型，为接入 Florence-2 或 Llama-3 做好准备。

🛠️ Prerequisites
OS: Ubuntu 22.04 LTS

ROS 2: Humble Hawksbill (or Jazzy Jalisco)

Simulation: NVIDIA Isaac Sim 4.0+ (Requires RTX GPU)

Hardware: NVIDIA GPU (RTX 3080/4070 or higher recommended)

📂 Project Structure
Plaintext

neuro-nav/
├── neuro_nav_sim/           # Isaac Sim 场景加载脚本与 USD 资产配置
├── neuro_nav_bringup/       # 系统级 Launch 文件 (一键启动)
├── neuro_nav_interfaces/    # 自定义 ROS 消息 (SemanticMap, GoalDescription)
├── neuro_nav_brain/         # (WIP) VLM 与 LLM 节点的存放处
└── README.md
🗺️ Roadmap
Phase 1: The Foundation (Current v1.0)
[x] 初始化项目仓库与依赖管理。

[ ] 搭建 Isaac Sim 室内仿真场景（Office/Home）。

[ ] 配置 Isaac Sim <-> ROS 2 Bridge (Lidar, RGB-D, TF, Odom)。

[ ] 跑通 SLAM Toolbox 建图与 Nav2 点到点导航。

Phase 2: The Eyes (Semantic Perception)
[ ] 集成 Florence-2 / YOLO-World 进行开放词汇目标检测。

[ ] 实现 2D 像素坐标到 3D 地图坐标的投影 (Pixel2Map Node)。

Phase 3: The Brain (Hybrid Navigation)
[ ] 开发 Nav2 Semantic Costmap Layer 插件。

[ ] 实现“自然语言 -> 导航目标”的指令解析。

🤝 Acknowledgements
This project is inspired by recent advancements in Embodied AI, including OrionNav and VLN-Zero.