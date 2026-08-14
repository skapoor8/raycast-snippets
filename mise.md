---
tags: [snippets, mise]
---

# mise

<!-- generated from mise.json by snippets2md.py — edit the JSON, not this file -->

30 snippets. Import via Raycast → Settings → Snippets → Import → `mise.json`.

| keyword | snippet |
| --- | --- |
| `;misetask` | [[#toml task (template)]] |
| `;misemin` | [[#toml task (minimal)]] |
| `;miserunblock` | [[#toml task (multiline run)]] |
| `;miseusage` | [[#usage spec reference]] |
| `;misecache` | [[#task caching (sources/outputs)]] |
| `;misedepends` | [[#task depends]] |
| `;miseconfirm` | [[#task confirm guard]] |
| `;misefile` | [[#file task (template, mise-tasks/<name>)]] |
| `;misefilemin` | [[#file task (minimal, mise-tasks/<name>)]] |
| `;misehide` | [[#file task (hidden helper)]] |
| `;misetaskdir` | [[#enable mise-tasks dir]] |
| `;miseconf` | [[#config skeleton]] |
| `;misetools` | [[#tools]] |
| `;miseenv` | [[#env]] |
| `;misestd` | [[#standard task set]] |
| `;misegroup` | [[#namespaced task group]] |
| `;misedocker` | [[#docker tasks]] |
| `;misepublish` | [[#gcp publish task]] |
| `;misemono` | [[#monorepo filter tasks]] |
| `;miserun` | [[#run task]] |
| `;miserunargs` | [[#run task with args and flags]] |
| `;misels` | [[#list tasks]] |
| `;miseinfo` | [[#task info]] |
| `;misedeps` | [[#task dependency tree]] |
| `;misevalidate` | [[#validate tasks]] |
| `;misewatch` | [[#watch and rerun]] |
| `;miseinstall` | [[#install tools]] |
| `;miseuse` | [[#pin a tool]] |
| `;miseexec` | [[#run with a tool version]] |
| `;misetrust` | [[#trust config]] |

## toml task (template)

`;misetask`

```toml
[tasks."db:migrate"]
description = "Run database migrations"
alias       = "dbm"
depends     = ["build"]
dir         = "{{ config_root }}"
env         = { LOG_LEVEL = "info" }
usage       = '''
arg "<env>" help="Environment to migrate" default="dev"
flag "-n --dry-run" help="Print the plan without applying"
flag "-s --steps <steps>" help="How many migrations to apply" default="all"
'''
run = '''
set -euo pipefail

env="${usage_env:-dev}"
steps="${usage_steps:-all}"

if [ "${usage_dry_run:-false}" = "true" ]; then
  echo "would migrate $env ($steps)"
  exit 0
fi

{cursor}
echo "migrated $env ($steps)"
'''
```

## toml task (minimal)

`;misemin`

```toml
[tasks.build]
description = "Build the project"
run         = "{cursor}"
```

## toml task (multiline run)

`;miserunblock`

```toml
[tasks.release]
description = "Cut a release"
depends     = ["test", "build-prod"]
run         = '''
set -euo pipefail

version="$(cat version.txt)"
echo "releasing ${version}"
{cursor}
'''
```

## usage spec reference

`;miseusage`

```toml
[tasks."{cursor}"]
description = "Task with fully parsed args and flags"
usage       = '''
arg "<env>" help="Required positional"
arg "[tag]" help="Optional positional" default="latest"
arg "<files>" help="Repeatable positional, space-joined in $usage_files" var=#true
flag "-v --verbose" help="Boolean switch -> usage_verbose is true/false"
flag "-o --out <path>" help="Flag that takes a value -> usage_out"
flag "-p --profile <profile>" help="Constrained value" default="debug" {
  choices "debug" "release"
}
'''
run = '''
echo "env=${usage_env} tag=${usage_tag} files=${usage_files}"
echo "verbose=${usage_verbose:-false} out=${usage_out:-} profile=${usage_profile}"
'''
```

## task caching (sources/outputs)

`;misecache`

```toml
[tasks.build]
description = "Build the project"
sources     = ["src/**/*.rs", "Cargo.toml"]
outputs     = ["target/debug/{cursor}"]
run         = "cargo build"
```

## task depends

`;misedepends`

```toml
[tasks.test]
description = "Run tests"
depends     = ["build"]
run         = "{cursor}"
```

## task confirm guard

`;miseconfirm`

```toml
[tasks."db:reset"]
description = "Drop and recreate the database"
confirm     = "This destroys all local data. Continue?"
run         = "{cursor}"
```

## file task (template, mise-tasks/<name>)

`;misefile`

```bash
#!/usr/bin/env bash
#MISE description="Deploy a service to an environment"
#MISE alias="dp"
#MISE depends=["build"]
#MISE dir="{{ config_root }}"
#MISE sources=["src/**/*"]
#MISE env={LOG_LEVEL = "info"}
#USAGE arg "<env>" help="Environment to deploy to"
#USAGE flag "-f --force" help="Skip the safety checks"
#USAGE flag "-r --replicas <replicas>" help="Replica count" default="2"

set -euo pipefail

env="${usage_env?}"
replicas="${usage_replicas:-2}"

if [ "${usage_force:-false}" != "true" ]; then
  echo "pre-flight checks for ${env}"
fi

{cursor}
echo "deployed ${env} with ${replicas} replicas"
```

## file task (minimal, mise-tasks/<name>)

`;misefilemin`

```bash
#!/usr/bin/env bash
#MISE description="{cursor}"

set -euo pipefail
```

## file task (hidden helper)

`;misehide`

```bash
#!/usr/bin/env bash
#MISE description="Internal helper"
#MISE hide=true

set -euo pipefail

{cursor}
```

## enable mise-tasks dir

`;misetaskdir`

```toml
[task_config]
includes = ["mise-tasks"]

[settings]
experimental = true
```

## config skeleton

`;miseconf`

```toml
[env]
PROJECT = "{cursor}"
VERSION = "{{ exec(command='cat version.txt 2>/dev/null | tr -d [:space:] || echo 0.1.0') }}"
_.path  = ["{{ config_root }}/node_modules/.bin"]

[tools]
node = "lts"

[tasks.build]
description = "Build the project"
run         = "echo build"

[task_config]
includes = ["mise-tasks"]

[settings]
experimental = true
```

## tools

`;misetools`

```toml
[tools]
node       = "lts"
pnpm       = "latest"
terraform  = "1"
shellcheck = "latest"
shfmt      = "latest"
{cursor}
```

## env

`;miseenv`

```toml
[env]
PROJECT = "{cursor}"
VERSION = "{{ exec(command='cat version.txt 2>/dev/null | tr -d [:space:] || echo 0.1.0') }}"
_.path  = ["{{ config_root }}/node_modules/.bin"]
```

## standard task set

`;misestd`

```toml
[tasks.install]
description = "Install dependencies"
run         = "{cursor}"

[tasks.build]
description = "Build the project"
depends     = ["install"]
run         = "echo build"

[tasks.test]
description = "Run tests"
depends     = ["build"]
run         = "echo test"

[tasks.lint]
description = "Run the linter"
run         = "echo lint"

[tasks."lint-fix"]
description = "Auto-fix linting issues"
run         = "echo lint-fix"

[tasks.format]
description = "Format source files"
run         = "echo format"

[tasks."format-check"]
description = "Check formatting without writing"
run         = "echo format-check"

[tasks.clean]
description = "Remove build artifacts"
run         = "echo clean"

[tasks.version]
description = "Print the current version"
run         = "cat version.txt"
```

## namespaced task group

`;misegroup`

```toml
[tasks."{cursor}:plan"]
description = "Plan the change"
run         = "echo plan"

[tasks."{cursor}:apply"]
description = "Apply the change"
depends     = ["{cursor}:plan"]
run         = "echo apply"
```

## docker tasks

`;misedocker`

```toml
[tasks."docker-build"]
description = "Build the Docker image"
run         = "COMPOSE_BAKE=true docker compose build"

[tasks."docker-run"]
description = "Run the app in Docker"
depends     = ["docker-build"]
run         = "docker compose up"

[tasks."docker-test"]
description = "Run the test suite in Docker"
depends     = ["docker-build"]
run         = "docker compose run --rm app mise run test"
```

## gcp publish task

`;misepublish`

```toml
[tasks.publish]
description = "Publish to GCP Artifact Registry"
depends     = ["test", "build-prod"]
run         = '''
set -euo pipefail

IMAGE="${GCP_REGISTRY_REGION}-docker.pkg.dev/${GCP_REGISTRY_PROJECT_ID}/${GCP_REGISTRY_NAME}/${PROJECT}:${VERSION}"
docker build -t "$IMAGE" .
docker push "$IMAGE"
echo "Published: $IMAGE"
'''
```

## monorepo filter tasks

`;misemono`

```toml
[tasks."build:web"]
description = "Build the web app"
run         = "pnpm --filter @{cursor}/web run build"

[tasks."build:api"]
description = "Build the API"
run         = "pnpm --filter @{cursor}/api run build"
```

## run task

`;miserun`

```bash
mise run {cursor}
```

## run task with args and flags

`;miserunargs`

```bash
mise run db:migrate {cursor} --steps 3 --dry-run
```

## list tasks

`;misels`

```bash
mise tasks ls
```

## task info

`;miseinfo`

```bash
mise tasks info {cursor}
```

## task dependency tree

`;misedeps`

```bash
mise tasks deps {cursor}
```

## validate tasks

`;misevalidate`

```bash
mise tasks validate
```

## watch and rerun

`;misewatch`

```bash
mise watch -t {cursor}
```

## install tools

`;miseinstall`

```bash
mise install
```

## pin a tool

`;miseuse`

```bash
mise use {cursor}@latest
```

## run with a tool version

`;miseexec`

```bash
mise exec {cursor}@latest -- node --version
```

## trust config

`;misetrust`

```bash
mise trust
```
