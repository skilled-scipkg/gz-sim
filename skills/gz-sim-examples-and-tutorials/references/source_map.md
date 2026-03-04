# gz-sim source map: Examples and Tutorials

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "EntitySystemAddService|LoadPlugin|ActivatePendingSystems" src/SystemManager.cc`
- `rg -n "OnWorldControl|CreateEntities|SetCreateEntities" src/SimulationRunner.cc`
- `rg -n "WebsocketServer::|JointController::|JointPositionController::|LogVideoRecorder::" src/systems`

## Source entry points by behavior
- `src/SystemManager.cc` | dynamic system insertion path used by tutorial service calls (`EntitySystemAddService`)
- `src/SimulationRunner.cc` | world control and entity lifecycle for runnable examples (`OnWorldControl`, `CreateEntities`)
- `src/systems/websocket_server/WebsocketServer.cc` | websocket runtime behavior (`Configure`, `Run`, `OnRequest`, `OnMessage`)
- `src/systems/joint_controller/JointController.cc` | velocity/force command handling (`Configure`, `PreUpdate`)
- `src/systems/joint_position_controller/JointPositionController.cc` | position command + PID flow (`Configure`, `ConfigureParameters`, `PreUpdate`)
- `src/systems/log_video_recorder/LogVideoRecorder.cc` | automated log-playback recording (`Configure`, `PostUpdate`)
- `src/gui/plugins/video_recorder/VideoRecorder.cc` | GUI recording flow (`OnStart`, `OnStop`, `OnSave`)
- `src/gui/plugins/mouse_drag/MouseDrag.cc` | interactive drag/wrench behavior (`Update`, `CalculateWrench`, mode handling)
- `src/LevelManager.cc` | levels activation behavior used by distributed-level demos
- `include/gz/sim/components/JointForceCmd.hh` | component contract for joint-force example checks
