# gz-sim source map: Test

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "TestFixture::Finalize|OnPreUpdate|OnPostUpdate|Server\(" src/TestFixture.cc python/src/gz/sim/TestFixture.cc`
- `rg -n "LogRecord::|LogPlayback::|Configure|PreUpdate|PostUpdate|Update" src/systems/log/LogRecord.cc src/systems/log/LogPlayback.cc`
- `rg -n "LogVideoRecorder::Configure|LogVideoRecorder::PostUpdate" src/systems/log_video_recorder/LogVideoRecorder.cc`

## Source entry points by behavior
- `src/TestFixture.cc` | C++ fixture lifecycle and callback registration (`Finalize`, `OnConfigure`, `OnPreUpdate`, `OnPostUpdate`)
- `src/TestFixture_TEST.cc` | fixture behavior assertions and regression examples
- `python/src/gz/sim/TestFixture.cc` | Python fixture binding methods (`finalize`, callback hooks)
- `src/systems/log/LogRecord.cc` | recording pipeline behavior (`Configure`, `PreUpdate`, `PostUpdate`, resource capture)
- `src/systems/log/LogPlayback.cc` | playback state application (`Configure`, `Update`, `ExtractStateAndResources`)
- `src/systems/log_video_recorder/LogVideoRecorder.cc` | log-playback video capture flow (`Configure`, `PostUpdate`)
- `include/gz/sim/components/LogPlaybackStatistics.hh` | playback statistics component contract for assertions
- `src/SimulationRunner.cc` | world stepping/control behavior when fixture checks depend on control flow
