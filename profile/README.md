<div align="center">

# Open Multiverse

**Bringing 3D worlds to the browser with Rust**

[![Rust](https://img.shields.io/badge/Rust-2021-orange?logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![WebAssembly](https://img.shields.io/badge/WebAssembly-wasm32--unknown--unknown-654FF0?logo=webassembly&logoColor=white)](https://webassembly.org/)
[![WebGPU](https://img.shields.io/badge/WebGPU-ready-4ade80)](https://www.w3.org/TR/webgpu/)
[![Bevy](https://img.shields.io/badge/Bevy-0.15-8a2be2)](https://bevyengine.org/)
[![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)](https://github.com/Open-Multiverse/NovaEngine)

[English](https://github.com/Open-Multiverse/.github/blob/master/profile/README.md) · [中文](https://github.com/Open-Multiverse/.github/blob/master/profile/README_CN.md)

</div>

---

## About us

Open Multiverse is an open-source organization focused on **web-native 3D game engines**.

We believe the browser is the natural distribution channel for the next generation of games and interactive content: nothing to install, a shareable link, and consistent behavior across platforms. We use **Rust + WebAssembly + WebGPU** to break that capability into composable, reusable engine modules so creators can focus on the game itself.

## Flagship project: Nova Engine

> A plugin-based web 3D game engine built on the Bevy 0.15 ECS, working toward a **fully playable RTS game running in the browser**.

[**Explore the repository →**](https://github.com/Open-Multiverse/NovaEngine) · [Chinese docs](https://github.com/Open-Multiverse/NovaEngine/blob/master/docs/README_CN.md)

**Highlights**

- **WebGPU rendering** — a modern graphics API for high-performance 3D
- **Physics** — rigid bodies, colliders and collision events powered by Rapier 3D
- **Immediate-mode UI** — egui integration with built-in CJK font support
- **Animation** — keyframes, tweens and an animation state machine
- **RTS map system** — tile maps, procedural terrain, A\* pathfinding, fog of war and an RTS camera
- **Characters & AI** — attributes/state modeling, perception, behavior trees, emotion and tactics
- **Formations** — slot assignment and formation-following movement
- **Tooling** — the `nova_test` harness, the `nova_inspector` ECS debugger, and Trunk-based WASM builds

## Modular architecture

The engine is split into 13 crates, composed through a single `nova_engine` prelude (plus a debugger under `tools/`):

| Crate | Responsibility |
|-------|----------------|
| `nova_core` | App lifecycle, ECS infrastructure, input, scene serialization, scheduling |
| `nova_render` | Cameras, lights, meshes, materials, plus frustum culling / LOD / instancing / spatial grid |
| `nova_physics` | Rapier 3D rigid bodies, colliders and collision events |
| `nova_ui` | Immediate-mode UI with egui |
| `nova_animation` | Keyframes, tweens and animation state machines |
| `nova_audio` | Music, sound effects and spatial audio |
| `nova_assets` | Asset registry, preloading and load-state tracking |
| `nova_map` | Tile maps, procedural generation, A\* pathfinding, fog of war, RTS camera |
| `nova_character` | Character attributes, state and visual feedback |
| `nova_ai` | Perception, behavior trees, emotion, personality and tactics |
| `nova_formation` | Formation management and slot assignment |
| `nova_test` | `TestApp`, assertion helpers and WASM test support |
| `nova_engine` | Unified entry point aggregating every subsystem prelude |
| `nova_inspector` | Native ECS debug inspector (tools) |

## Quick start

```bash
# Get the code
git clone https://github.com/Open-Multiverse/NovaEngine.git
cd NovaEngine

# Prerequisites
rustup target add wasm32-unknown-unknown
cargo install trunk

# Run a demo (open http://127.0.0.1:8080 in your browser)
trunk serve examples/basic_demo
```

```rust
use nova_engine::prelude::*;

fn main() {
    NovaApp::new()
        .with_title("My Game")
        .add_plugin(NovaRenderPlugin)
        .add_plugin(OrbitCameraPlugin)
        .add_startup_system(setup)
        .run();
}

fn setup(mut commands: Commands) {
    commands.spawn(Camera3d::default());
}
```

## Examples

| Example | What it shows |
|---------|---------------|
| `basic_demo` | Basic 3D scene, physics and orbit camera |
| `physics_demo` | Physics simulation |
| `animation_demo` | Animation system |
| `ui_demo` | egui UI |
| `breakout_3d` | A 3D breakout game |
| `rts_demo` | RTS prototype: selection, pathfinding movement, combat, AI, formations |

## Roadmap

Nova Engine is developed in 8 phases and is currently at an early stage:

| Phase | Goal | Status |
|-------|------|--------|
| 1 | Test infrastructure fixes | ✅ Done |
| 2 | Character movement system | 🚧 In progress |
| 3 | Combat damage system | Planned |
| 4 | AI behavior tree completion | Planned |
| 5 | Real audio playback | Planned |
| 6 | Truthful rendering stats & screenshot tests | Planned |
| 7 | Critical-path performance work | Planned |
| 8 | End-to-end RTS demo integration | Planned |

## Contributing

- Report issues and share ideas via [Issues](https://github.com/Open-Multiverse/NovaEngine/issues)
- Before opening a PR, run `cargo fmt --all`, `cargo clippy --all-targets` and `cargo test --all`
- Documentation and commit messages are primarily in Chinese; code follows Rust community conventions

## License

Nova Engine is dual-licensed under **MIT OR Apache-2.0**; you may use it under either license.

---

<div align="center">

**Open Multiverse** · [GitHub](https://github.com/Open-Multiverse) · [Nova Engine](https://github.com/Open-Multiverse/NovaEngine)

</div>
