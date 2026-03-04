# gz-sim source map: Getting Started

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "Server::Run|Server::SetPaused|Server::Reset" src/Server.cc include/gz/sim/Server.hh`
- `rg -n "CreateEntities|OnWorldControl|PublishStats" src/SimulationRunner.cc`
- `rg -n "SetSdfFile|SetSdfString|SetUpdateRate" src/ServerConfig.cc include/gz/sim/ServerConfig.hh`

## Source entry points by behavior
- `include/gz/sim/Server.hh` | server lifecycle API (`Run`, `RunOnce`, `Running`, `SetPaused`, `ResetAll`, `Reset`)
- `src/Server.cc` | concrete run loop control and server status transitions
- `include/gz/sim/ServerConfig.hh` | startup/runtime configuration API contract
- `src/ServerConfig.cc` | config parsing and runtime option setters (`SetSdfFile`, `SetSdfString`, `SetUpdateRate`)
- `src/SimulationRunner.cc` | world initialization and control service handlers (`CreateEntities`, `OnWorldControl`, `ProcessWorldControl`)
- `include/gz/sim/SdfEntityCreator.hh` | SDF-to-entity creation API (`CreateEntities`, `RequestRemoveEntity`)
- `src/SdfEntityCreator.cc` | actual entity graph construction and parent wiring (`CreateEntities`, `SetParent`)
- `include/gz/sim/components/World.hh` | world component contract used for world entity detection
- `include/gz/sim/components/Name.hh` | name component used for lookup and service-level targeting
- `src/SystemManager.cc` | runtime system insertion endpoint (`EntitySystemAddService`)
