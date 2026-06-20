# REACHABLE GitHub And GitLab Demo Repositories

This file explains the public CI/CD demo repository layout. The GitHub and
GitLab sets are intentionally symmetrical: each ecosystem has a reusable
toolkit, a distribution/discovery surface, a basic scan demo, and a Go
remediation/public-clone proof demo.

## GitHub Repositories

| Repository | Primary role | Use this when |
|---|---|---|
| [`reach-testbed-github-marketplace`](https://github.com/sthenos-security/reach-testbed-github-marketplace) | GitHub Marketplace distribution surface plus the configurable root action. | You need the public GitHub Marketplace listing or the root action that mirrors the GitLab catalog surface. |
| [`reach-ci-github`](https://github.com/sthenos-security/reach-ci-github) | Reusable GitHub Actions toolkit for production auto-remediation. | You want the recommended customer workflow with branch creation, proof scan, optional PR, artifacts, and Pages proof. |
| [`reach-testbed-github-go`](https://github.com/sthenos-security/reach-testbed-github-go) | Go public-clone/remediation proof demo. | You want the runnable Codex and Claude demos, public source cloning, MCP GitHub cloning, git clone fallback, and post-remediation proof. |
| [`reach-testbed-github`](https://github.com/sthenos-security/reach-testbed-github) | Basic GitHub scan demo and simple scanner reference. | You want a minimal scan-only example and simple CI code reference. |

## GitLab Repositories

| Repository | Primary role | GitHub equivalent |
|---|---|---|
| [`reach-testbed-gitlab-catalog`](https://gitlab.com/sthenos-security-public/reach-testbed-gitlab-catalog) | GitLab CI/CD Catalog component plus full remediation demo. GitLab Catalog is the GitLab distribution surface; commercial partner routing is separate. | `reach-testbed-github-marketplace` |
| [`reach-ci-gitlab`](https://gitlab.com/sthenos-security-public/reach-ci-gitlab) | Reusable GitLab remediation toolkit. | `reach-ci-github` |
| [`reach-testbed-gitlab-go`](https://gitlab.com/sthenos-security-public/reach-testbed-gitlab-go) | Go public-clone/remediation proof demo. | `reach-testbed-github-go` |
| [`reach-testbed-gitlab`](https://gitlab.com/sthenos-security-public/reach-testbed-gitlab) | Basic GitLab scan demo and simple CI code reference. | `reach-testbed-github` |

## Architecture

```text
Distribution surface
  GitHub Marketplace action / GitLab Catalog component
        |
        v
Reusable toolkit
  reach-ci-github / reach-ci-gitlab
        |
        v
Demo application
  basic scan demo or Go remediation proof demo
        |
        v
REACHABLE
  install latest beta, scan, build remediation bundle, run selected coding
  agent, rescan, publish sanitized proof
```

The Marketplace/Catalog repositories are the discovery and onboarding
surfaces. The toolkit repositories contain the reusable CI implementation. The
testbed repositories are examples and validation targets.

## Token Model

Both ecosystems use one AI provider key plus platform-specific source/control
tokens:

| Purpose | GitHub | GitLab |
|---|---|---|
| OpenAI/Codex lane | `OPENAI_API_KEY` | `OPENAI_API_KEY` |
| Claude lane | `ANTHROPIC_API_KEY` | `ANTHROPIC_API_KEY` |
| Read-only source/package context | `MCP_GITHUB_TOKEN` with Contents read-only | GitLab token only where private source access requires it |
| CI branch/PR/MR control | Built-in `GITHUB_TOKEN` | Prefer `CI_JOB_TOKEN` branch push; use `REACHABLE_GITLAB_TOKEN` only for automatic MR creation |

`MCP_GITHUB_TOKEN` is read-only source context. It is not the token that pushes
remediation branches or opens pull requests.

## Recommended Customer Path

Use the distribution surface first:

- GitHub: Marketplace action for discovery and install, `reach-ci-github` for
  direct toolkit use, and `reach-testbed-github-go` for the runnable demos.
- GitLab: Catalog component for the full pipeline.

Keep the basic scan demos available as copy-paste references. They are examples,
not the preferred full remediation integration.
