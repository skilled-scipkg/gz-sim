---
name: gz-sim-index
description: Top-level router for gz-sim skills with docs-first escalation across build, startup, runtime workflows, APIs, modeling, examples, and test validation.
---

# gz-sim Skills Index

## Request triage
- Build/install/dependency/test setup -> `gz-sim-build-and-install`
- First run, terminology, and resource paths -> `gz-sim-getting-started`
- Launch/pause/reset/log/distributed/headless -> `gz-sim-simulation-workflows`
- Python bindings and system/plugin extension -> `gz-sim-api-and-scripting`
- SDF/model/world authoring and physics parameters -> `gz-sim-inputs-and-modeling`
- Runnable recipe mapping from tutorials to examples -> `gz-sim-examples-and-tutorials`
- Fixture and regression checks around logs and TestFixture -> `gz-sim-test`

## Fast simulation bootstrap
1. Validate CLI: `gz sim -h`
2. Start a known world: `gz sim examples/worlds/empty.sdf`
3. Verify control channel: `gz service --list | rg "/world/.*/control|/world/.*/create"`
4. If anything fails, route immediately to `gz-sim-build-and-install`

## Escalation order (mandatory)
1. Use the selected skill `SKILL.md` and its primary docs.
2. Reproduce with that skill's listed tutorial/example commands.
3. Check behavior/regression artifacts (`test`, `python/test`, `tutorials/test_fixture.md`).
4. Inspect source via the selected skill's source map and entry points.

## Router notes
- Keep responses docs-first and command-driven.
- Use concrete repo paths whenever possible (for example `examples/worlds/default.sdf`).
- Switch skills when request scope changes (build vs runtime vs API vs modeling).
- Prefer smallest runnable reproduction before broadening scope.
