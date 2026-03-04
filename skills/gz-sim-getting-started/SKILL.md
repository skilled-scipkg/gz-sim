---
name: gz-sim-getting-started
description: Docs-first onboarding path for first successful gz-sim runs, core terminology, and resource resolution before deeper workflow or API work.
---

# gz-sim: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill for first-run setup, terminology, and initial world launch issues.
- Route to `gz-sim-build-and-install` for dependency or compilation blockers.
- Route to `gz-sim-simulation-workflows` for pause/reset/log/distributed workflows.
- Route to `gz-sim-inputs-and-modeling` for model/world authoring and physics tuning.
- Route to `gz-sim-api-and-scripting` for Python or plugin development.

### Triage questions
- Was gz-sim installed from binaries or built from source? (`tutorials/install.md`)
- Does `gz sim -h` work in this shell? (`README.md`)
- Which world file is being launched, and what world name does it define?
- Are custom model/plugin paths required? (`tutorials/resources.md`)
- Is the goal just launch, or launch + runtime entity creation? (`tutorials/entity_creation.md`)

### Canonical workflow
1. Validate install and CLI entrypoint.
2. Align vocabulary (world/entity/component/system/ECM).
3. Start one known-good world from repo paths.
4. Verify `/world/<name>/create` and `/world/<name>/control` services.
5. Run one minimal create-service example.
6. Only then move to custom worlds/plugins.

### Minimal working example
```bash
# terminal 1, from repo root
gz sim examples/worlds/empty.sdf
```

```bash
# terminal 2, from repo root
cd examples/standalone/entity_creation
cmake -S . -B build
cmake --build build
./build/entity_creation
gz service --list | rg "/world/empty/create|/world/empty/control"
```

### Pitfalls and fixes
- `entity_creation` appears idle: it expects a running world named `empty` (`examples/standalone/entity_creation/README.md`).
- `/world/<name>/create` missing: ensure `UserCommands` system is loaded (`tutorials/entity_creation.md`).
- Resource URI lookup fails: set `GZ_SIM_RESOURCE_PATH` (`tutorials/resources.md`).
- Plugin load failures: verify `GZ_SIM_SYSTEM_PLUGIN_PATH` and `GZ_GUI_PLUGIN_PATH` (`tutorials/resources.md`).
- Mixed install command mismatch: set `GZ_CONFIG_PATH` (`README.md`).
- On Windows, run server and GUI in separate terminals (`README.md`).

### Convergence and validation checks
- `gz sim -h` succeeds.
- `gz sim examples/worlds/empty.sdf` starts and publishes `/stats`.
- `/world/empty/create` and `/world/empty/control` appear in service list.
- `./build/entity_creation` inserts entities into the running world.
- Startup logs show no unresolved resource or plugin path warnings.

## Scope
- First runnable simulation path and foundational resource/path behavior.

## Primary documentation references
- `tutorials/install.md`
- `README.md`
- `tutorials/terminology.md`
- `tutorials/resources.md`
- `tutorials/entity_creation.md`
- `examples/standalone/entity_creation/README.md`

## Workflow
- Solve startup path issues first.
- Confirm terminology and path resolution before deeper runtime debugging.
- Escalate to runtime/API skills only after baseline launch is stable.

## Source entry points for unresolved issues
- `include/gz/sim/Server.hh`
- `src/Server.cc`
- `include/gz/sim/ServerConfig.hh`
- `src/ServerConfig.cc`
- `src/SimulationRunner.cc`
- `include/gz/sim/SdfEntityCreator.hh`
- `src/SdfEntityCreator.cc`
- `include/gz/sim/components/World.hh`
- `include/gz/sim/components/Name.hh`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" include/gz/sim src`.
