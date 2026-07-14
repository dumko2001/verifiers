# OpenEnv

The built-in `openenv` taskset runs any OpenEnv environment through its native client:

```bash
uv run --with openenv --with-editable . eval openenv \
  --taskset.env openenv/wordle \
  --taskset.provider-kwargs '{"app":"textarena_env.server.app:app"}' \
  --harness.id null -n 1 --push false
```

Environment ids use OpenEnv's UV provider by default. Set `use_docker=true` to let OpenEnv
resolve and run the environment's published image, or set `base_url` to connect to an existing
server. Pass exactly one of `env` and `base_url`. Prime uses a VM by default when OpenEnv Docker
is selected. `provider_kwargs` passes options such as `app`, `env_vars`, `tag`, and
`project_path` directly to OpenEnv.

V1's `-n` bounds the generated seeds; `seed` selects the first one and `reset` supplies other
reset arguments. The user simulator exposes each observation and action schema to the model,
then maps OpenEnv's reward and termination signal back to the trace.
