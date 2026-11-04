# Fluxyr

Flask-compatible Python framework for agents, skills and durable execution.
You write Flask-style apps; the agent builds, tests and saves Python skills
through chat, with tools, memory, conversations, streaming, background runs
and scheduled routines. It ships its own web UI.

## What the install makes

- A `web` process on port 5050, built from the repository's own Dockerfile.
- A 5Gi disk at `/var/lib/fluxyr`, where the agent keeps its state, its
  SQLite database and its skills.
- The config vars: your OpenRouter key (a secret), the model, the agent's
  name, and a vault key generated at install.

## After the install

The agent answers at the project's address once the first build is done.
It follows `main` of the upstream repository: a new commit is built and
released, as any git project of the platform is.

To use another provider, set `FLUXYR_PROVIDER` (`openai`, `anthropic`,
`custom`) and its key (`OPENAI_API_KEY`, `ANTHROPIC_API_KEY`,
`CUSTOM_API_KEY`) in the project's config vars. For PostgreSQL instead of
SQLite, attach a database and set `DATABASE_URL` in the
`postgresql+psycopg2://` form Fluxyr reads.
