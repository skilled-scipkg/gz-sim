# gz-sim source map: Simulation Workflows

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "Server::Run|Server::SetPaused|Server::Reset|Server::Stop" src/Server.cc`
- `rg -n "OnWorldControl|ProcessWorldControl|Step|CreateEntities|LoadLoggingPlugins" src/SimulationRunner.cc`
- `rg -n "SetUseLogRecord|SetLogRecordPath|SetLogPlaybackPath|SetNetworkRole|SetUseLevels" src/ServerConfig.cc`

## Source entry points by behavior
- `src/Server.cc` | top-level server lifecycle and world-facing control (`Run`, `SetPaused`, `Reset`, `Stop`)
- `src/SimulationRunner.cc` | world control, stepping, and service handling (`OnWorldControl`, `ProcessWorldControl`, `Step`, `CreateEntities`)
- `src/ServerConfig.cc` | runtime config semantics for distributed/levels/logging/headless options
- `src/LevelManager.cc` | levels state transitions (`ReadLevels`, `UpdateLevelsState`, `LoadActiveEntities`, `UnloadInactiveEntities`)
- `src/network/NetworkManagerPrimary.cc` | distributed primary orchestration (`Handshake`, `Step`, `OnStepAck`)
- `src/network/NetworkManagerSecondary.cc` | distributed secondary flow (`OnControl`, `OnStep`)
- `src/systems/log/LogRecord.cc` | recording pipeline (`Configure`, `PreUpdate`, `PostUpdate`, resource capture)
- `src/systems/log/LogPlayback.cc` | playback pipeline (`Configure`, `Update`, `ExtractStateAndResources`)
- `src/systems/log_video_recorder/LogVideoRecorder.cc` | playback video generation (`Configure`, `PostUpdate`)
- `include/gz/sim/ServerConfig.hh` | public API contract for runtime control options
