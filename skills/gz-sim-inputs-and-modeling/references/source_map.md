# gz-sim source map: Inputs and Modeling

Use this map after reviewing `doc_map.md`.

## Fast source navigation
- `rg -n "SdfEntityCreator::CreateEntities|RequestRemoveEntity|SetParent" src/SdfEntityCreator.cc include/gz/sim/SdfEntityCreator.hh`
- `rg -n "Physics::Configure|Physics::Update|Physics::Reset|UpdatePhysics|UpdateSim" src/systems/physics/Physics.cc`
- `rg -n "Buoyancy::Configure|Buoyancy::PreUpdate|Buoyancy::PostUpdate|graded_buoyancy" src/systems/buoyancy/Buoyancy.cc src/systems/buoyancy/Buoyancy.hh`

## Source entry points by behavior
- `include/gz/sim/SdfEntityCreator.hh` | SDF-to-entity API (`CreateEntities`, `RequestRemoveEntity`, `SetParent`)
- `src/SdfEntityCreator.cc` | hierarchy/component creation across world/model/link/joint/sensor entities
- `src/systems/physics/Physics.cc` | physics plugin load and simulation sync (`Configure`, `Update`, `Reset`, `UpdatePhysics`, `UpdateSim`)
- `src/systems/buoyancy/Buoyancy.cc` | buoyancy force computation and lifecycle (`Configure`, `PreUpdate`, `PostUpdate`, `IsEnabled`)
- `src/systems/buoyancy/Buoyancy.hh` | buoyancy SDF schema and option semantics (`uniform_fluid_density`, `graded_buoyancy`)
- `include/gz/sim/components/Physics.hh` | physics component contracts used by physics system
- `include/gz/sim/components/SphericalCoordinates.hh` | spherical coordinate component serialization/contract
- `include/gz/sim/components/Pose.hh` | pose component contract for spatial state checks
- `include/gz/sim/components/World.hh` | world tagging used for world-level queries
- `include/gz/sim/World.hh` | world API hooks including spherical-coordinate operations
