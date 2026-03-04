---
name: gz-sim-build-and-install
description: Docs-first playbook for installing and building gz-sim, then diagnosing dependency, configuration, and test failures with concrete source entry points.
---

# gz-sim: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for install, dependency, configure, compile, and test failures.
- Route to `gz-sim-getting-started` after build succeeds and first launch works.
- Route to `gz-sim-api-and-scripting` when the blocker is Python bindings or plugin development.
- Route to `gz-sim-simulation-workflows` for runtime control, logging, distributed, or levels behavior.

### Triage questions
- Which install route is intended (apt / brew / conda / source)? (`tutorials/install.md`)
- Are you building this repo or only a local example/plugin target?
- Is Python support required (`SKIP_PYBIND11`, `pybind11`)? (`CMakeLists.txt`, `python/CMakeLists.txt`)
- Are websocket or rendering-dependent features required? (`CMakeLists.txt`)
- Is the environment headless/CI (display-dependent tests may be skipped)? (`src/CMakeLists.txt`, `test/integration/CMakeLists.txt`)

### Canonical workflow
1. Prefer binary install for fastest unblock (`tutorials/install.md`).
2. For source builds, configure from repo root into `build/`.
3. Build library + tools.
4. Run tests with `ctest` and inspect skipped/failing groups.
5. Smoke-test CLI and at least one world launch.
6. For example plugins, build in example dir and export plugin path before running.

### Minimal working example
```bash
# from repo root
cmake -S . -B build -DCMAKE_BUILD_TYPE=RelWithDebInfo
cmake --build build -j"$(nproc)"
ctest --test-dir build --output-on-failure
gz sim -h
```

```bash
# plugin smoke test: examples/plugin/hello_world/README.md
cd examples/plugin/hello_world
cmake -S . -B build
cmake --build build
export GZ_SIM_SYSTEM_PLUGIN_PATH="$(pwd)/build"
gz sim -v 3 hello_world_plugin.sdf
```

### Pitfalls and fixes
- `gz` CLI-dependent tests skipped: ensure `gz-tools` is installed (`CMakeLists.txt`, `test/integration/CMakeLists.txt`).
- Python bindings missing: verify `SKIP_PYBIND11=OFF`, Python3, and pybind11 detection (`CMakeLists.txt`, `python/CMakeLists.txt`).
- Websocket system missing: `libwebsockets` was not found at configure time (`CMakeLists.txt`).
- Plugin load failures: export `GZ_SIM_SYSTEM_PLUGIN_PATH` and / or `GZ_GUI_PLUGIN_PATH` (`tutorials/resources.md`).
- Mixed binary + source toolchain mismatch: set `GZ_CONFIG_PATH` (`README.md`).

### Convergence and validation checks
- `gz sim -h` works without missing-library errors.
- `ctest --test-dir build --output-on-failure` completes with no new regressions.
- `gz sim examples/worlds/empty.sdf -r -s` starts and `/world/empty/control` exists in `gz service --list`.
- If Python bindings are expected: `python3 -c "import gz.sim"` succeeds.
- At least one example/plugin run path works end-to-end.

## Scope
- Build/install/dependency workflows and test pipeline stability.

## Primary documentation references
- `tutorials/install.md`
- `README.md`
- `tutorials/resources.md`
- `examples/plugin/hello_world/README.md`
- `examples/plugin/custom_sensor_system/README.md`
- `examples/plugin/rendering_plugins/README.md`
- `examples/plugin/reset_plugin/README.md`
- `examples/standalone/gtest_setup/README.md`

## Workflow
- Start docs-first with install/build instructions.
- Reproduce with minimal commands before source inspection.
- Use `references/source_map.md` for behavior checks when docs are insufficient.

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `src/CMakeLists.txt`
- `python/CMakeLists.txt`
- `test/CMakeLists.txt`
- `test/integration/CMakeLists.txt`
- `src/InstallationDirectories.cc`
- `include/gz/sim/InstallationDirectories.hh`
- `src/SystemLoader.cc`
- `include/gz/sim/SystemLoader.hh`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" CMakeLists.txt src python test include`.
