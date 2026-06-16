# OrchStep Starter

A ready-to-run [OrchStep](https://orchstep.dev) project. Click **Use this
template** at the top of the repo to scaffold your own, then replace the
placeholder commands with your real build, test, and deploy steps.

It works the moment you clone it - no dependencies, runs the same locally and in CI.

## Use this template

1. Click **Use this template -> Create a new repository**.
2. Install the OrchStep CLI:
   ```bash
   curl -fsSL https://orchstep.dev/install.sh | sh
   # or: brew install orchstep/tap/orchstep | npm i -g orchstep | pip install orchstep
   ```
3. Run the pipeline:
   ```bash
   orchstep run
   ```
4. Push to GitHub - the included CI runs lint + build + test automatically.

## Run it locally

```bash
orchstep run            # the build + test pipeline (the "main" task)
orchstep run build      # a single task
orchstep list-tasks     # everything you can run
orchstep run --dry-run  # preview the whole plan without executing
orchstep menu           # interactive task picker
```

```text
$ orchstep run
Discovered 3 task file(s) from tasks/ directory
Task: main
Task: build
  $ echo "building my-app v0.1.0"
building my-app v0.1.0
  $ echo "artifact my-app-0.1.0 is ready"
artifact my-app-0.1.0 is ready
Task: test
  $ echo "running tests for my-app"
running tests for my-app
Result: success
```

Deploy is parameterized - override variables at the call site:

```bash
orchstep run deploy --var environment=production --var version=1.2.3
```

## What's inside

```text
.
├── orchstep.yml              # root: defaults + the top-level "main" pipeline
├── tasks/                    # one file per task, auto-discovered
│   ├── build.yml             #   -> orchstep run build
│   ├── test.yml              #   -> orchstep run test
│   └── deploy.yml            #   -> orchstep run deploy
└── .github/workflows/ci.yml  # CI via orchstep/run-orchstep@v1
```

- **`orchstep.yml`** declares `defaults:` (variables) and top-level `steps:` that
  call the discovered tasks - this is the `main` pipeline `orchstep run` executes.
- **`tasks/`** holds one task per file; the file name is the task name
  (`tasks/build.yml` -> `build`). Add a task by dropping in a new file.
- **`.github/workflows/ci.yml`** lints and runs the pipeline on every push, and
  has a manual **Deploy** job (Actions tab -> Run workflow).

## Customize

- **Real commands:** replace the `echo ...` lines in `tasks/*.yml` with your build,
  test, and deploy commands. The comments show common examples per stack.
- **New task:** add `tasks/<name>.yml` with a `steps:` list - it is callable
  immediately as `orchstep run <name>`.
- **Variables:** `defaults:` sets values; override with `--var key=value`. Note
  `env` is reserved (it is the environment-variable namespace) - this template
  uses `environment`.
- **Environments & modules:** grow into per-environment configs and shared,
  versioned modules when you need them (links below).

## Learn more

- [Quick Start](https://orchstep.dev/getting-started/quick-start)
- [CLI Reference](https://orchstep.dev/getting-started/cli)
- [Task Files](https://orchstep.dev/learn/task-files)
- [OrchStep in CI](https://orchstep.dev/getting-started/ci)
- [Migrating from Make / Just / Task / npm / shell](https://orchstep.dev/migrating/overview)
