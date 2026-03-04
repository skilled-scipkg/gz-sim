---
name: gz-sim-examples-and-tutorials
description: Docs-first recipe router that maps gz-sim tutorials to runnable examples, scripts, and minimal reproductions.
---

# gz-sim: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill when the request asks for runnable recipes, tutorial reproduction, or quick behavior demos.
- Route to `gz-sim-build-and-install` if examples fail to build or load dependencies.
- Route to `gz-sim-simulation-workflows` for deep runtime control, logging, or distributed diagnostics.
- Route to `gz-sim-api-and-scripting` for custom code extensions beyond tutorial usage.

### Triage questions
- Which behavior should be demonstrated (entity creation, distributed, websocket, recording, joint control, Python API)?
- Is the target GUI-based, headless, or multi-terminal?
- Are local plugins/scripts already built and path-exported?
- Is a one-command demo enough, or is a reproducible multi-step script needed?

### Canonical workflow
1. Pick the nearest tutorial.
2. Map it to a concrete example directory or world file.
3. Run the minimal documented path exactly.
4. Validate expected service/topic/UI behavior.
5. Then adapt parameters only if required.

### Tutorial-to-example map
- `tutorials/entity_creation.md` -> `examples/standalone/entity_creation`
- `tutorials/python_interfaces.md` -> `examples/scripts/python_api`
- `tutorials/distributed_simulation.md` -> `examples/scripts/distributed`
- `tutorials/levels.md` -> `examples/scripts/distributed_levels`
- `tutorials/websocket_server.md` -> `examples/scripts/websocket_server`
- `tutorials/video_recorder.md` -> `examples/scripts/log_video_recorder` and `examples/worlds/video_record_dbl_pendulum.sdf`
- `tutorials/server_config.md` -> `examples/plugin/priority_printer_plugin`
- `tutorials/joint_controller.md` -> `examples/worlds/joint_controller.sdf`

### Minimal working example
```bash
# distributed demo, from repo root
cd examples/scripts/distributed
./secondary.sh   # in separate terminals
./primary.sh
```

```bash
# websocket system added at runtime, from repo root
gz sim -v 4 examples/worlds/shapes.sdf -s
gz service -s /world/shapes/entity/system/add --reqtype gz.msgs.EntityPlugin_V --reptype gz.msgs.Boolean --timeout 2000 --req 'plugins: {name: "gz::sim::systems::WebsocketServer", filename: "gz-sim-websocket-server-system", innerxml: "<port>9002</port><publication_hz>30</publication_hz><max_connections>-1</max_connections>"}'
```

### Pitfalls and fixes
- Example plugin not found: export `GZ_SIM_SYSTEM_PLUGIN_PATH` and / or `GZ_GUI_PLUGIN_PATH` from build dir.
- Wrong world name in service path: use actual world name from SDF.
- Video codec mismatch: choose a supported format (OGV can fail on some setups).
- Distributed demo stalls: primary started before secondaries.
- Playback recorder misses assets: ensure required Fuel models exist in cache (`examples/scripts/log_video_recorder/README.md`).

### Convergence and validation checks
- Demo world launches with intended systems/plugins.
- Required endpoints appear in `gz service --list` / `gz topic --list`.
- Behavior matches tutorial intent (movement, recording, websocket, distributed sync).
- Command sequence is repeatable in a clean shell.

## Scope
- Fast, reproducible tutorial execution paths and their example mappings.

## Primary documentation references
- `tutorials/entity_creation.md`
- `tutorials/distributed_simulation.md`
- `tutorials/levels.md`
- `tutorials/websocket_server.md`
- `tutorials/video_recorder.md`
- `tutorials/joint_controller.md`
- `tutorials/python_interfaces.md`
- `examples/scripts/websocket_server/README.md`
- `examples/scripts/distributed/README.md`
- `examples/scripts/distributed_levels/README.md`
- `examples/scripts/log_video_recorder/README.md`

## Workflow
- Prefer exact tutorial-to-example mapping over ad-hoc command invention.
- Use smallest runnable artifact first.
- Escalate to source only when documented behavior does not match runtime.

## Source entry points for unresolved issues
- `src/SystemManager.cc`
- `src/SimulationRunner.cc`
- `src/systems/websocket_server/WebsocketServer.cc`
- `src/systems/log_video_recorder/LogVideoRecorder.cc`
- `src/gui/plugins/video_recorder/VideoRecorder.cc`
- `src/gui/plugins/mouse_drag/MouseDrag.cc`
- `src/systems/joint_controller/JointController.cc`
- `src/systems/joint_position_controller/JointPositionController.cc`
- `src/LevelManager.cc`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src include/gz/sim examples`.
