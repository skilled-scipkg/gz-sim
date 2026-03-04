---
name: gz-sim-api-and-scripting
description: Docs-first guide for Python bindings and system plugin extension points in gz-sim, with concrete source entry files for loader and interface behavior.
---

# gz-sim: API and Scripting

## High-Signal Playbook
### Route conditions
- Use this skill for Python API usage, Python systems, and C++ system/plugin extension points.
- Route to `gz-sim-build-and-install` for pybind11/Python/build blockers.
- Route to `gz-sim-simulation-workflows` for runtime controls/logging/distributed behavior.
- Route to `gz-sim-inputs-and-modeling` when request is mainly SDF/component modeling.

### Triage questions
- Are you writing Python scripts, Python systems, or C++ systems?
- Does `python3 -c "import gz.sim"` succeed?
- Are `PYTHONPATH` and `GZ_SIM_SYSTEM_PLUGIN_PATH` configured? (`tutorials/python_interfaces.md`, `tutorials/resources.md`)
- Which interfaces are needed (`Configure`, `PreUpdate`, `Update`, `PostUpdate`, `Reset`)? (`include/gz/sim/System.hh`)
- Is plugin loading failing by name, filename, or search path? (`src/SystemLoader.cc`)

### Canonical workflow
1. Verify Python bindings availability.
2. Reproduce with `TestFixture` first.
3. For Python systems, implement `get_system()` and load with `PythonSystemLoader`.
4. For C++ systems, implement `ISystem*` interfaces and register plugin correctly.
5. Validate plugin path discovery and loader output.
6. If load fails, inspect loader + manager source paths.

### Minimal working example
```bash
# from repo root
python3 -c "import gz.sim"
cd examples/scripts/python_api
python3 testFixture.py
```

```xml
<!-- load a Python system from SDF -->
<plugin filename="gz-sim-python-system-loader-system"
        name="gz::sim::systems::PythonSystemLoader">
  <module_name>test_system</module_name>
  <force>100</force>
</plugin>
```

### Pitfalls and fixes
- Python callback never runs: `fixture.finalize()` omitted before `server.run(...)` (`tutorials/python_interfaces.md`).
- `import gz.sim` fails: bindings not installed or `PYTHONPATH` missing.
- Python system not discovered: module path missing from `GZ_SIM_SYSTEM_PLUGIN_PATH` or `PYTHONPATH`.
- Plugin load fails with "library not found": filename/path mismatch in loader search.
- Plugin loads but system never updates: plugin does not implement required `System` interfaces.

### Convergence and validation checks
- `python3 -c "import gz.sim"` succeeds.
- `python3 examples/scripts/python_api/testFixture.py` runs and reports iterations.
- Verbose server logs show plugin/system load without loader errors.
- Expected callbacks (`PreUpdate`/`Update`/`PostUpdate`) fire in intended phases.

## Scope
- Programmatic simulation control and extension via Python and C++ APIs.

## Primary documentation references
- `tutorials/python_interfaces.md`
- `tutorials/create_system_plugins.md`
- `tutorials/resources.md`
- `examples/scripts/python_api/README.md`
- `examples/scripts/python_api/testFixture.py`
- `tutorials/migration_world_api.md`
- `tutorials/migration_link_api.md`
- `tutorials/migration_joint_api.md`
- `tutorials/migration_sensor_api.md`

## Workflow
- Start from Python/TestFixture or system-interface docs.
- Reproduce with minimal runnable code before deep source inspection.
- Escalate to loader/manager internals only when behavior is still ambiguous.

## Source entry points for unresolved issues
- `include/gz/sim/System.hh`
- `include/gz/sim/SystemLoader.hh`
- `include/gz/sim/SystemPluginPtr.hh`
- `src/SystemLoader.cc`
- `src/SystemManager.cc`
- `python/src/gz/sim/_gz_sim_pybind11.cc`
- `python/src/gz/sim/TestFixture.cc`
- `python/src/gz/sim/Server.cc`
- `python/src/gz/sim/World.cc`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" include/gz/sim src python/src/gz/sim`.
