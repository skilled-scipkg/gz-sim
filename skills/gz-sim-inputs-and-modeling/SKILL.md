---
name: gz-sim-inputs-and-modeling
description: Docs-first playbook for SDF/world/model authoring, ECS component use, and physics/environment parameterization in gz-sim.
---

# gz-sim: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use this skill for SDF/model/world authoring, component semantics, and physics/environment parameterization.
- Route to `gz-sim-getting-started` for basic setup and terminology.
- Route to `gz-sim-simulation-workflows` for run/pause/reset/log/distributed control issues.
- Route to `gz-sim-api-and-scripting` when behavior depends on plugin interface implementation details.

### Triage questions
- Is the issue in SDF authoring, runtime entity creation, or component reads/writes?
- Which physics engine and world-level physics parameters are intended? (`tutorials/physics.md`)
- Are spherical coordinates / georeferenced operations required? (`tutorials/spherical_coordinates.md`)
- Is buoyancy expected, and if so uniform or graded mode? (`tutorials/theory_buoyancy.md`)
- Are missing resources/plugins caused by path resolution? (`tutorials/resources.md`)

### Canonical workflow
1. Validate resource and plugin resolution paths.
2. Start from known worlds before custom SDF edits.
3. Confirm physics plugin and engine selection in logs.
4. Apply and verify component changes through services or ECS checks.
5. Tune buoyancy / environment parameters and re-check behavior.

### Minimal working example
```bash
# from repo root
gz sim examples/worlds/spherical_coordinates.sdf
gz service -s /world/spherical_coordinates/set_spherical_coordinates --reqtype gz.msgs.SphericalCoordinates --reptype gz.msgs.Boolean --timeout 2000 --req 'surface_model: EARTH_WGS84, latitude_deg: 35.6, longitude_deg: 140.1, elevation: 10.0'
```

```bash
# from repo root
gz sim examples/worlds/buoyancy.sdf
```

### Pitfalls and fixes
- Model/mesh URI not found: set `GZ_SIM_RESOURCE_PATH` (`tutorials/resources.md`).
- Custom physics engine not found: set `GZ_SIM_PHYSICS_ENGINE_PATH` (`tutorials/physics.md`).
- Spherical origin update appears ineffective: changing origin does not move existing entities (`tutorials/spherical_coordinates.md`).
- Graded buoyancy unexpected: only `<box>` and `<sphere>` collisions are supported in graded mode (`tutorials/theory_buoyancy.md`).
- `Configure()` component reads incomplete: entities outside plugin parent may not be loaded yet (`tutorials/using_components.md`).

### Convergence and validation checks
- Required entities/components exist and are visible in GUI inspector or ECS query.
- Physics engine selection in logs matches expected plugin.
- Spherical coordinate service responds `data: true`.
- Buoyancy behavior (sink/neutral/float) matches configured density and collision volume.
- No unresolved resource/plugin-path warnings during world startup.

## Scope
- Simulation input correctness and modeling semantics that directly affect physical behavior.

## Primary documentation references
- `tutorials/using_components.md`
- `tutorials/resources.md`
- `tutorials/physics.md`
- `tutorials/spherical_coordinates.md`
- `tutorials/theory_buoyancy.md`
- `tutorials/entity_creation.md`
- `tutorials/component_pose.md`
- `tutorials/component_jointforcecmd.md`

## Workflow
- Resolve path/plugin discovery first.
- Validate with smallest runnable world before introducing custom complexity.
- Escalate to source for function-level behavior ambiguity.

## Source entry points for unresolved issues
- `include/gz/sim/SdfEntityCreator.hh`
- `src/SdfEntityCreator.cc`
- `src/systems/physics/Physics.cc`
- `src/systems/buoyancy/Buoyancy.cc`
- `src/systems/buoyancy/Buoyancy.hh`
- `include/gz/sim/components/Physics.hh`
- `include/gz/sim/components/SphericalCoordinates.hh`
- `include/gz/sim/components/Pose.hh`
- `include/gz/sim/components/World.hh`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" include/gz/sim/components src/systems src`.
