<div align="center">

# Open Multiverse

**用 Rust 把 3D 世界带进浏览器**

[![Rust](https://img.shields.io/badge/Rust-2021-orange?logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![WebAssembly](https://img.shields.io/badge/WebAssembly-wasm32--unknown--unknown-654FF0?logo=webassembly&logoColor=white)](https://webassembly.org/)
[![WebGPU](https://img.shields.io/badge/WebGPU-ready-4ade80)](https://www.w3.org/TR/webgpu/)
[![Bevy](https://img.shields.io/badge/Bevy-0.15-8a2be2)](https://bevyengine.org/)
[![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)](https://github.com/Open-Multiverse/NovaEngine)

[English](https://github.com/Open-Multiverse/.github/blob/master/profile/README.md) · [中文](https://github.com/Open-Multiverse/.github/blob/master/profile/README_CN.md)

</div>

---

## 关于我们

Open Multiverse 是一个开源组织，专注于 **Web 原生的 3D 游戏引擎**。

我们相信浏览器是下一代游戏与交互内容的天然发布渠道：无需安装、一个链接即可分享、跨平台表现一致。我们用 **Rust + WebAssembly + WebGPU** 把这些能力拆解成可组合、可复用的引擎模块，让创作者把精力放在玩法本身。

## 核心项目：Nova Engine

> 基于 Bevy 0.15 ECS 的插件化 Web 3D 游戏引擎，目标是让一款**功能完整的 RTS 游戏在浏览器中真正可玩**。

[**进入仓库 →**](https://github.com/Open-Multiverse/NovaEngine) · [中文文档](https://github.com/Open-Multiverse/NovaEngine/blob/master/docs/README_CN.md)

**核心特性**

- **WebGPU 渲染** —— 现代图形 API，高性能 3D 管线
- **物理模拟** —— 基于 Rapier 3D 的刚体、碰撞体与碰撞事件
- **即时模式 UI** —— egui 集成，原生支持中文字体
- **动画系统** —— 关键帧、补间（Tween）与动画状态机
- **RTS 地图系统** —— 瓦片地图、程序化地形、A\* 寻路、战争迷雾、RTS 相机
- **角色与 AI** —— 属性/状态建模、感知、行为树、情绪与战术
- **编队系统** —— 编队槽位分配与跟随移动
- **工程化工具** —— `nova_test` 测试框架、`nova_inspector` ECS 调试器、Trunk WASM 构建

## 模块化架构

引擎按职责拆分为 13 个 crate，全部通过统一的 `nova_engine` prelude 组合使用（另有 `tools/` 下的调试器）：

| Crate | 职责 |
|-------|------|
| `nova_core` | App 生命周期、ECS 基础设施、输入、场景序列化、调度 |
| `nova_render` | 相机、光照、网格、材质，以及视锥剔除 / LOD / 实例化 / 空间网格 |
| `nova_physics` | Rapier 3D 刚体、碰撞体与碰撞事件 |
| `nova_ui` | 基于 egui 的即时模式 UI |
| `nova_animation` | 关键帧、Tween、动画状态机 |
| `nova_audio` | 背景音乐、音效与空间音频 |
| `nova_assets` | 资源注册、预加载与加载状态追踪 |
| `nova_map` | 瓦片地图、程序化生成、A\* 寻路、战争迷雾、RTS 相机 |
| `nova_character` | 角色属性、状态与视觉反馈 |
| `nova_ai` | 感知、行为树、情绪、人格与战术 |
| `nova_formation` | 编队管理与槽位分配 |
| `nova_test` | `TestApp`、断言工具与 WASM 测试支持 |
| `nova_engine` | 统一入口，聚合各子系统 prelude |
| `nova_inspector` | 原生 ECS 调试检查器（tools） |

## 快速开始

```bash
# 获取代码
git clone https://github.com/Open-Multiverse/NovaEngine.git
cd NovaEngine

# 环境准备
rustup target add wasm32-unknown-unknown
cargo install trunk

# 运行示例（浏览器打开 http://127.0.0.1:8080）
trunk serve examples/basic_demo
```

```rust
use nova_engine::prelude::*;

fn main() {
    NovaApp::new()
        .with_title("我的游戏")
        .add_plugin(NovaRenderPlugin)
        .add_plugin(OrbitCameraPlugin)
        .add_startup_system(setup)
        .run();
}

fn setup(mut commands: Commands) {
    commands.spawn(Camera3d::default());
}
```

## 示例

| 示例 | 内容 |
|------|------|
| `basic_demo` | 基础 3D 场景、物理与轨道相机 |
| `physics_demo` | 物理模拟演示 |
| `animation_demo` | 动画系统演示 |
| `ui_demo` | egui UI 演示 |
| `breakout_3d` | 3D 打砖块小游戏 |
| `rts_demo` | RTS 原型：选中、寻路移动、战斗、AI、编队 |

## 路线图

Nova Engine 按 8 个阶段推进，当前处于早期开发阶段：

| 阶段 | 目标 | 状态 |
|------|------|------|
| 1 | 测试基础设施修复 | ✅ 已完成 |
| 2 | 角色移动系统 | 🚧 进行中 |
| 3 | 战斗伤害系统 | 计划中 |
| 4 | AI 行为树完善 | 计划中 |
| 5 | 音频真实实现 | 计划中 |
| 6 | 渲染统计修正与截图测试 | 计划中 |
| 7 | 性能关键路径优化 | 计划中 |
| 8 | RTS Demo 端到端集成 | 计划中 |

## 参与贡献

- 欢迎通过 [Issues](https://github.com/Open-Multiverse/NovaEngine/issues) 反馈问题、提出想法
- 提交 PR 前请先运行 `cargo fmt --all`、`cargo clippy --all-targets` 与 `cargo test --all`
- 项目文档与提交信息以中文为主，代码遵循 Rust 社区惯例

## 许可证

Nova Engine 采用 **MIT OR Apache-2.0** 双许可，可任选其一使用。

---

<div align="center">

**Open Multiverse** · [GitHub](https://github.com/Open-Multiverse) · [Nova Engine](https://github.com/Open-Multiverse/NovaEngine)

</div>
