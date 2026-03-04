# gz-sim documentation map: Getting Started

Use these docs for first launch, core terminology, and resource/service basics.

## First-run essentials
- `tutorials/install.md` | installation paths and prerequisites
- `README.md` | `gz sim` invocation and known CLI/tooling caveats
- `tutorials/terminology.md` | world/entity/component/system vocabulary

## Runtime basics
- `tutorials/resources.md` | `GZ_SIM_RESOURCE_PATH`, plugin paths, and URI resolution
- `tutorials/entity_creation.md` | `/world/<name>/create` service and `UserCommands` requirement
- `tutorials/pause_run_simulation.md` | transport control basics (`/world/<name>/control`)
- `tutorials/reset_simulation.md` | reset request semantics

## Minimal reproducible examples
- `examples/standalone/entity_creation/README.md` | build/run flow against `empty` world
- `examples/worlds/empty.sdf` | known-good startup world
- `examples/worlds/default.sdf` | known-good control/reset world
