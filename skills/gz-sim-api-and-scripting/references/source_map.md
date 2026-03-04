# gz-sim source map: API and Scripting

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "ISystemConfigure|ISystemPreUpdate|ISystemUpdate|ISystemPostUpdate|ISystemReset" include/gz/sim/System.hh`
- `rg -n "LoadPlugin|AddSystemPluginPath|InstantiateSystemPlugin|FixDeprecatedPluginName" src/SystemLoader.cc src/SystemManager.cc`
- `rg -n "PYBIND11_MODULE|TestFixture::|Server::Run|World::SetSphericalCoordinates" python/src/gz/sim/*.cc`

## Source entry points by behavior
- `include/gz/sim/System.hh` | system interface contracts (`ISystemConfigure`, `ISystemPreUpdate`, `ISystemUpdate`, `ISystemPostUpdate`, `ISystemReset`)
- `include/gz/sim/SystemPluginPtr.hh` | plugin pointer type composition for supported interfaces
- `include/gz/sim/SystemLoader.hh` | plugin loader API
- `src/SystemLoader.cc` | loader behavior (`AddSystemPluginPath`, `PluginPaths`, `LoadPlugin`, `InstantiateSystemPlugin`)
- `src/SystemManager.cc` | runtime activation and dynamic insertion (`LoadPlugin`, `ActivatePendingSystems`, `EntitySystemAddService`)
- `python/src/gz/sim/_gz_sim_pybind11.cc` | Python module registration (`PYBIND11_MODULE`)
- `python/src/gz/sim/TestFixture.cc` | Python fixture callbacks and finalize wiring (`Finalize`, `on_pre_update`, `on_post_update`)
- `python/src/gz/sim/Server.cc` | Python server bindings (`run`, `reset`, `reset_all`, `running`)
- `python/src/gz/sim/World.cc` | world-query bindings (`name`, `model_by_name`, `set_spherical_coordinates`)
- `python/src/gz/sim/EntityComponentManager.cc` | Python ECS access patterns for behavior checks
