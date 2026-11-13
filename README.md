# rpm-packages

RPM repository for [vmvarela](https://github.com/vmvarela) tools, served via GitHub Pages.

## Installation

```bash
sudo curl -fsSL https://vmvarela.github.io/rpm-packages/vmvarela.repo \
  -o /etc/yum.repos.d/vmvarela.repo
sudo dnf install sql-pipe
```

## Packages

| Package | Description |
|---------|-------------|
| [sql-pipe](https://github.com/vmvarela/sql-pipe) | Read CSV from stdin, query with SQL, write CSV to stdout |
| [damas](https://github.com/vmvarela/damas) | Terminal board game suite |

## How it is built

`update.yml` checks out `vmvarela/package-distribution` at the pinned
`PACKAGE_DISTRIBUTION_SHA` and runs its RPM publisher, which owns the catalog,
the verification of every release asset and the layout of the site. This
repository contributes the trigger, the signing key, the deployment and the
durable state.

The state (`state/<package>/state.json` plus `pool/`) is committed by the
workflow after a successful deploy. It is what keeps the current and previous
version of every package, so the next run only needs the new release.

`gpgcheck=1` and `repo_gpgcheck=1` are always on: the publisher signs every
package and every architecture's metadata, and a run without the key fails
instead of deploying an unsigned repository.

## Required Secrets

| Secret | Description |
|--------|-------------|
| `GPG_SIGNING_KEY` | GPG private key (armored) used to sign packages and metadata |
| `GPG_KEY_ID` | Key ID or fingerprint matching `GPG_SIGNING_KEY` |

Both are mandatory. The published key is `RPM-GPG-KEY-vmvarela`, served from
the repository root and referenced by the generated `.repo`.
