# shpyrd catalog

Applications a [shpyrd](https://github.com/shpyrd-io/shpyrd) project can be
made from: agents, CRMs, open-source projects that run on the platform. An
entry is a folder under `entries/`, named as the project's slug will be,
holding a `shpyrd.yaml`: the keys of a project's own `shpyrd.yaml`
(`processes`, `build`, `env`) under a `catalog` block that says what the
entry is, where its code lives, and what it asks at install.

```yaml
catalog:
  name: Fluxyr
  description: A Python framework for agents, with its own web UI.
  category: agents
  icon: message-square
  color: teal
  source:
    git: https://github.com/shpyrd-io/fluxyr
    revision: main          # a branch is followed; a tag is pinned
  inputs:
    - name: OPENROUTER_API_KEY
      label: OpenRouter API key
      secret: true
      required: true
    - name: VAULT_ENCRYPTION_KEY
      generate: 32          # made at install, never asked
  volumes:
    - name: data
      size: 5Gi
processes:
  web:
    port: 5050
    volumes: [{name: data, path: /var/lib/fluxyr}]
build:
  strategy: dockerfile
```

Beside the `shpyrd.yaml`: a `README.md`, shown on the entry's page; an
`icon.svg` (or `.png`, `.webp`) for its card; and any other file is the
**overlay**, laid over the upstream checkout before the build. That is how
an entry gives a Dockerfile to a project that has none, or a better one.
An overlay goes with `build.strategy: dockerfile`: the buildpacks builder
reads one source. Buildpacks are the default build; a Dockerfile is for
what they cannot build, and an entry that ships one says why in its readme.

## How it is published

The platform reads an index over HTTPS, not this repository. On every push
to `main`, [`publish.yml`](.github/workflows/publish.yml) validates the
entries and writes the index with the shpyrd CLI:

```sh
shpyrd catalog validate entries
shpyrd catalog publish entries --out public
```

and publishes `public/` to GitHub Pages, at
`https://shpyrd-io.github.io/catalog/index.json`, which a server reads
unless `SHPYRD_CATALOG_URL` names another (a fork of this repository, a
private catalog) or `off`. Pull requests run the validation.

## Adding an entry

1. A folder under `entries/`, with its `shpyrd.yaml` and `README.md`.
2. `shpyrd catalog validate entries` says what is missing.
3. A pull request. The review reads the entry as a person installing it
   would: what it asks for, what it runs, where the code comes from.

An installed project is a copy made at install time, marked with the
entry's name and digest. A change to an entry reaches new installs; the
projects already made keep following their upstream branch.
