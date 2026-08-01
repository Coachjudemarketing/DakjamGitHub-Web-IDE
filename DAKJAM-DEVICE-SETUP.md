# DakJam Cross-Device Setup

## Goal

One project, one source of truth, four supported device environments.

### Android

Use Termux for command-line development. Install Git and Node.js, clone the canonical repository, and run the project's documented install/start commands.

### Windows

Use PowerShell or Windows Terminal. Install Git and Node.js, clone the canonical repository, then use the project's documented install/start commands.

### macOS

Use Terminal. Install Git and Node.js, clone the canonical repository, then use the project's documented install/start commands.

### Linux

Use the system terminal. Install Git and Node.js, clone the canonical repository, then use the project's documented install/start commands.

## Important

This document intentionally does not guess the project's package manager or framework. The repository's actual manifest must determine whether the app uses npm, pnpm, yarn, bun, Python, Rust, Docker, or another runtime.

## First diagnostic commands

```bash
git status
git branch --show-current
git log -1 --oneline
node --version
npm --version
git --version
```

Then identify the runtime manifest before installing anything:

```bash
ls -la
```

Look for one or more of:

- `package.json`
- `pnpm-lock.yaml`
- `yarn.lock`
- `bun.lockb` / `bun.lock`
- `requirements.txt`
- `pyproject.toml`
- `Cargo.toml`
- `Dockerfile`
- `docker-compose.yml`

Do not blindly run commands from another project. The runtime manifest is the authority.

## Clone the canonical project

```bash
git clone https://github.com/Coachjudemarketing/DakjamGitHub-Web-IDE.git
dakjam-project
cd dakjam-project
```

Use the branch intended for development when required:

```bash
git checkout codex/setup
```

## Verify before changing anything

```bash
git status
git log -1 --oneline
```

## Connection model

```text
Device -> GitHub source -> build -> deploy -> live URL
                         |
                         +-> external services
```

A device-local copy is not the deployment. A GitHub commit is not the deployment. A successful build is not proof of a running service. The health check and device verification are required.

## Recovery

If a local project seems to disappear:

1. Check GitHub first.
2. Check the current branch.
3. Check `git status` and `git log`.
4. Re-clone if necessary.
5. Compare the deployed commit with the local commit.
6. Only then investigate local filesystem/process issues.

Never delete or reset a repository while troubleshooting unless the current work has been backed up or committed.
