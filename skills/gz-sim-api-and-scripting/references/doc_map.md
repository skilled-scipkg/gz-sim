# gz-sim documentation map: API and Scripting

Use these docs before inspecting source for Python bindings and system-plugin APIs.

## Python API and fixture docs
- `tutorials/python_interfaces.md` | Python `TestFixture`, callback lifecycle, and Python-system loading
- `examples/scripts/python_api/README.md` | Python API example entrypoint
- `examples/scripts/python_api/testFixture.py` | executable Python fixture example
- `tutorials/test_fixture.md` | fixture-driven automated simulation tests

## Plugin and system interface docs
- `tutorials/create_system_plugins.md` | `ISystem*` implementation and plugin registration flow
- `tutorials/resources.md` | plugin discovery paths (`GZ_SIM_SYSTEM_PLUGIN_PATH`, `PYTHONPATH`)
- `tutorials/migration_world_api.md` | world API migration surface
- `tutorials/migration_link_api.md` | link API migration surface
- `tutorials/migration_joint_api.md` | joint API migration surface
- `tutorials/migration_sensor_api.md` | sensor API migration surface
