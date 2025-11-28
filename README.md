# devportal-wrappers

VeeCode DevPortal wrappers for public plugins (workarounds for legacy customers)

## Motivation

Sometimes we just need to repackage an existing login as a dynamic plugin. This helps avoiding forking the original plugin and meks keeping track of many plugins in a distro a little easier.

## Wrapped Plugins

| Original Plugin | Wrapped Plugin |
|----------------|----------------|
| @backstage-community/plugin-scaffolder-backend-module-azure-devops | @veecode/plugin-scaffolder-backend-module-azure-devops |

## Steps for each plugin

Creating a wrapped version of a plugin is done by the sequence of steps below. We are still experimenting around this, but pay attention to `package.json` details and plugin role requirements.

- Create a base "package.json" for a plugin
- Define "backstage role"
- Include original package as dependency
- Build tasks "build", "tsc", "clean", "export-dynamic" and "export-dynamic-clean"
- Attention to "main", "types", "publishConfig" and "files"
- Task "export-dynamic" should --embed-package the wrapped package
- The "rhdh-cli" should exclude the "@backstage" packages, but still we must declare then as "peerDependencies" AND "devDependencies" (both), or exporting will fail or produce a too big package.
- Write a Makefile for each wrapper (will make life easier)

TODO: find a good way to list dependencies that should move to "peerDependencies" AND "devDependencies".

### Docker Compose testing

Build and export:

```sh
make build-plugin-dynamic
```

Start DevPortal mounting the wrapped plugin's `dist-dynamic` folder:

```sh
docker compose up --no-log-prefix
```
