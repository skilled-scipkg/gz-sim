---
name: gz-sim-test
description: Focused test skill for fixture-driven simulation checks, rolling log media playback, and source-level validation entry points.
---

# gz-sim: Test

## Scope
- Focused guidance for `test/media/rolling_shapes_log/README.md` fixtures and `TestFixture`-driven regression checks.

## Primary documentation references
- `test/media/rolling_shapes_log/README.md`
- `tutorials/test_fixture.md`
- `tutorials/log.md`
- `examples/standalone/gtest_setup/README.md`
- `examples/scripts/python_api/README.md`

## Workflow
1. Reproduce log playback and state transitions with the rolling-shapes fixture.
2. Validate scripted simulation checks via C++ `TestFixture` and Python `TestFixture`.
3. If runtime control behavior is suspect, pivot to `gz-sim-simulation-workflows`.
4. If test/build pipeline is failing, pivot to `gz-sim-build-and-install`.

## Minimal working example
```bash
# replay existing fixture log from repo root
gz sim -r --playback test/media/rolling_shapes_log
```

```bash
# generate or refresh fixture data (overwrites existing log)
gz sim -r -s -i 5000 --log-overwrite --physics-engine gz-physics-bullet-plugin rolling_shapes.sdf --record-path test/media/rolling_shapes_log/
```

```bash
# C++ fixture tests
cd examples/standalone/gtest_setup
cmake -S . -B build
cmake --build build
./build/gravity_TEST
./build/command_TEST
```

## Convergence and validation checks
- Playback starts from `test/media/rolling_shapes_log` and simulation advances deterministically.
- `gravity_TEST` and `command_TEST` complete without regression.
- `TestFixture` callbacks execute with expected iteration counts.
- Log record/playback behavior is stable across repeated runs.

## Source entry points for unresolved issues
- `src/TestFixture.cc`
- `src/TestFixture_TEST.cc`
- `python/src/gz/sim/TestFixture.cc`
- `src/systems/log/LogRecord.cc`
- `src/systems/log/LogPlayback.cc`
- `src/systems/log_video_recorder/LogVideoRecorder.cc`
- `include/gz/sim/components/LogPlaybackStatistics.hh`
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" src python/src test`.
