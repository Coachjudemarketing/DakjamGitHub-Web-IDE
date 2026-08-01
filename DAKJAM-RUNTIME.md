# DakJam Runtime Contract

## Why this exists

DakJam projects should have one canonical runtime contract instead of scattered setup instructions. A project is not considered "done" until the app can be located, installed, started, health-checked, and connected from a supported device.

## Source of truth

GitHub is the source of truth for application code and deployment configuration.

Supported workstation targets:

- Android / Termux
- Windows
- macOS
- Linux

## Required lifecycle

```text
Repository
  -> dependency install
  -> configuration validation
  -> build
  -> tests
  -> local run
  -> health check
  -> deployment
  -> remote health check
  -> device/browser verification
```

A green GitHub commit alone does not prove the app is running.

## Runtime states

| State | Meaning |
|---|---|
| `SOURCE_OK` | Code is present in the repository |
| `INSTALL_OK` | Dependencies installed successfully |
| `CONFIG_OK` | Required non-secret configuration exists |
| `BUILD_OK` | Application builds |
| `TEST_OK` | Automated tests pass |
| `RUNNING` | Process/server is actually running |
| `HEALTHY` | Health endpoint responds |
| `CONNECTED` | Required external services authenticate/connect |
| `DEVICE_READY` | User can open/use the application on the target device |
| `PRODUCTION_READY` | Deployment and smoke tests pass |

## Definition of done

A feature/app is not marked complete until all applicable states are green. This prevents "files exist" from being confused with "application works."

## Canonical health contract

Every DakJam service should expose a simple health check such as `/health` returning structured status. Example:

```json
{
  "status": "ok",
  "service": "dakjam",
  "version": "...",
  "environment": "development|staging|production",
  "dependencies": {
    "database": "ok",
    "queue": "ok",
    "model_provider": "ok"
  }
}
```

Do not include secrets, tokens, passwords, or private credentials in health responses.

## Configuration contract

Keep configuration in one documented location. Secrets belong in the deployment platform's secret store, not in Git.

Minimum categories:

- application URL
- environment name
- database connection
- authentication provider
- model provider credentials
- external integration credentials
- webhook secrets
- feature flags

## Device principle

Do not make the phone, Mac, Windows PC, or Linux workstation the source of truth. Devices are clients/workstations. A missing local copy should never mean the project disappeared; it should be recoverable from GitHub and the deployment target.

## Debug order

When an app appears and disappears or cannot be found, check in this order:

1. Is the repository/branch present?
2. Does the expected entry point exist?
3. Are dependencies installed?
4. Is configuration valid?
5. Does the build pass?
6. Does the process actually start?
7. What port/URL is it listening on?
8. Does `/health` respond?
9. Can the device reach that URL?
10. Are external integrations authenticated?
11. Are background workers/queues running?
12. Is the deployed revision the revision being tested?

## Anti-fragmentation rule

Do not create another disconnected app directory when an existing DakJam project already owns the capability. Add the capability to the canonical repository or explicitly declare a separate repository and its relationship in the manifest.

## Security note

Unexpected background processes, files changing without a known workflow, or unexplained device behavior should be investigated through logs, process lists, repository history, deployment history, and account audit logs. Do not assume a hidden attacker or daemon without evidence. The runtime contract is designed to make those facts observable.
