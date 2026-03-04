---
name: gz-sim-simulation-workflows
description: Docs-first runbook for launching, pausing, resetting, logging, and distributed/headless gz-sim execution with source entry points for runtime behavior.
---

# gz-sim: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for launch/run/pause/reset/log/playback and distributed/levels workflows.
- Route to `gz-sim-build-and-install` for build/dependency errors.
- Route to `gz-sim-api-and-scripting` for plugin/system implementation details.
- Route to `gz-sim-inputs-and-modeling` when failures come from SDF/model/physics configuration.

### Triage questions
- What world name is running? (service paths are world-scoped)
- GUI + server together, server-only (`-s`), or headless rendering?
- Is control needed via GUI, transport service, or C++ API?
- Are logs needed (record path, playback, compression)?
- Is this distributed simulation, and how many secondaries are expected?

### Canonical workflow
1. Launch a known world with explicit repo path.
2. Control run/pause/reset through `/world/<name>/control`.
3. Validate state with `/stats`.
4. Record a short log, then playback to confirm reproducibility.
5. For distributed mode, start secondaries first, then primary.
6. For levels mode, run with `--levels` and verify load/unload transitions.

### Minimal working example
```bash
# from repo root
gz sim examples/worlds/default.sdf
gz service -s /world/default/control --reqtype gz.msgs.WorldControl --reptype gz.msgs.Boolean --timeout 3000 --req 'pause: true'
gz service -s /world/default/control --reqtype gz.msgs.WorldControl --reptype gz.msgs.Boolean --timeout 3000 --req 'pause: false'
gz service -s /world/default/control --reqtype gz.msgs.WorldControl --reptype gz.msgs.Boolean --timeout 3000 --req 'reset: {all: true}'
gz topic --echo --topic /stats -n 1
```

```bash
# distributed demo, from repo root
cd examples/scripts/distributed
./secondary.sh   # run in N terminals
./primary.sh
```

### Pitfalls and fixes
- Service calls fail: wrong world name in service path.
- Expected plugins not loaded: verify server-config precedence and env paths (`tutorials/server_config.md`).
- Record and playback requested together: unsupported (`tutorials/log.md`).
- Distributed run stalls: primary started too early or peer heartbeat failed (`tutorials/distributed_simulation.md`).
- `--levels` behavior absent: performers/levels tags not configured or missing `--levels` launch (`tutorials/levels.md`).

### Convergence and validation checks
- `/stats` shows pause toggles and increasing iterations while running.
- Reset request returns true and simulation time restarts near zero.
- Record path contains `state.tlog`; playback starts from that directory.
- Distributed primary reports expected secondaries and continues stepping.
- In levels demo, entities load/unload as performers move.

## Scope
- Operational simulation control, server config behavior, logging, levels, and distributed execution.

## Primary documentation references
- `tutorials/pause_run_simulation.md`
- `tutorials/reset_simulation.md`
- `tutorials/log.md`
- `tutorials/distributed_simulation.md`
- `tutorials/levels.md`
- `tutorials/server_config.md`
- `examples/scripts/distributed/README.md`
- `examples/scripts/distributed_levels/README.md`
- `examples/scripts/log_video_recorder/README.md`

## Workflow
- Reproduce with docs + scripts first.
- Validate with transport services and `/stats` checkpoints.
- Escalate to source only when runtime control flow remains unclear.

## Source entry points for unresolved issues
- `src/Server.cc`
- `src/SimulationRunner.cc`
- `src/ServerConfig.cc`
- `src/LevelManager.cc`
- `src/network/NetworkManagerPrimary.cc`
- `src/network/NetworkManagerSecondary.cc`
- `src/systems/log/LogRecord.cc`
- `src/systems/log/LogPlayback.cc`
- `src/systems/log_video_recorder/LogVideoRecorder.cc`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src include/gz/sim`.
