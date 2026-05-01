# rpm-packages

RPM repository for [vmvarela](https://github.com/vmvarela) tools, served via GitHub Pages.

## Installation

```bash
sudo dnf config-manager --add-repo https://vmvarela.github.io/rpm-packages/vmvarela.repo
sudo dnf install sql-pipe
```

## Packages

| Package | Description |
|---------|-------------|
| [sql-pipe](https://github.com/vmvarela/sql-pipe) | Read CSV from stdin, query with SQL, write CSV to stdout |

## Required Secrets

| Secret | Description |
|--------|-------------|
| `GPG_SIGNING_KEY` | GPG private key (armored) for signing the repository |
| `GPG_KEY_ID` | Key ID or fingerprint matching `GPG_SIGNING_KEY` |

If secrets are not set the repository is built but left unsigned.
