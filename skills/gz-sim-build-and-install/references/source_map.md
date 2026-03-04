# gz-sim source map: Build and Install

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "SKIP_PYBIND11|pybind11|libwebsockets|BUILD_TESTING" CMakeLists.txt src/CMakeLists.txt python/CMakeLists.txt`
- `rg -n "getPluginInstallDir|getGUIPluginInstallDir" src/InstallationDirectories.cc include/gz/sim/InstallationDirectories.hh`
- `rg -n "AddSystemPluginPath|PluginPaths|LoadPlugin" src/SystemLoader.cc include/gz/sim/SystemLoader.hh`

## Source entry points by behavior
- `CMakeLists.txt` | top-level feature gates and optional dependencies (`SKIP_PYBIND11`, `libwebsockets`)
- `src/CMakeLists.txt` | core library/system targets and feature-conditioned builds
- `python/CMakeLists.txt` | Python module build definitions (`pybind11_add_module`)
- `test/CMakeLists.txt` | global test enablement and grouping
- `test/integration/CMakeLists.txt` | integration-test gating for CLI/display/Python features
- `src/InstallationDirectories.cc` | runtime install path resolution (`getPluginInstallDir`, `getGUIPluginInstallDir`)
- `include/gz/sim/InstallationDirectories.hh` | public install-directory API contract
- `src/SystemLoader.cc` | runtime plugin search path and load path (`AddSystemPluginPath`, `PluginPaths`, `LoadPlugin`)
- `include/gz/sim/SystemLoader.hh` | plugin loader interface used by runtime systems
- `src/SystemManager.cc` | plugin activation path and dynamic load integration (`LoadPlugin`, `ActivatePendingSystems`)
