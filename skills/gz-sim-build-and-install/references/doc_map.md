# gz-sim documentation map: Build and Install

Use these docs first for installation, dependency resolution, and build/test workflows.

## Core install and environment docs
- `tutorials/install.md` | binary and source install flows (Ubuntu, macOS, Windows)
- `README.md` | CLI usage and mixed-install `GZ_CONFIG_PATH` workaround
- `tutorials/resources.md` | plugin/resource path variables used at runtime

## Build and plugin example docs
- `examples/plugin/hello_world/README.md` | minimal system plugin build/run flow
- `examples/plugin/custom_sensor_system/README.md` | plugin build with external sensor dependency
- `examples/plugin/rendering_plugins/README.md` | combined GUI/server plugin path configuration
- `examples/plugin/reset_plugin/README.md` | reset-oriented plugin load and runtime check
- `examples/standalone/entity_creation/README.md` | standalone build and create-service validation

## Test-oriented docs
- `examples/standalone/gtest_setup/README.md` | simulation-based GTest setup and execution
- `tutorials/test_fixture.md` | fixture-based simulation testing strategy
- `tutorials/headless_rendering.md` | headless rendering runtime prerequisites
