# tagviu

`tagviu` is distributed as a **precompiled native executable**. The source repository is private, but the release binaries and installation scripts are publicly available from this `orashus/tagviu` distribution repository.

This repository does **not** contain the Go source code. It hosts installation scripts and GitHub Releases only.

## Install (macOS / Linux)

```bash
curl -fsSL https://raw.githubusercontent.com/orashus/tagviu/main/install.sh | sh
```

Pinned version:

```bash
curl -fsSL https://raw.githubusercontent.com/orashus/tagviu/main/install.sh | TAGVIU_VERSION=v0.1.0 sh
```

Custom install directory:

```bash
curl -fsSL https://raw.githubusercontent.com/orashus/tagviu/main/install.sh | TAGVIU_INSTALL_DIR="$HOME/.local/bin" sh
```

### Inspect before running

Piping a remote script to `sh` requires trusting this repository's installer. Prefer reviewing it first:

```bash
curl -fsSL https://raw.githubusercontent.com/orashus/tagviu/main/install.sh -o install.sh
less install.sh
sh install.sh
```

The installer downloads the matching release archive, verifies `checksums.txt`, then installs `tagviu` to `~/.local/bin` by default.

## Install (Windows)

```powershell
irm https://raw.githubusercontent.com/orashus/tagviu/main/install.ps1 | iex
```

Pinned version / custom directory:

```powershell
$env:TAGVIU_VERSION = "v0.1.0"
$env:TAGVIU_INSTALL_DIR = "$env:LOCALAPPDATA\tagviu\bin"
irm https://raw.githubusercontent.com/orashus/tagviu/main/install.ps1 | iex
```

Inspect before running:

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/orashus/tagviu/main/install.ps1 -OutFile install.ps1
notepad install.ps1
.\install.ps1
```

## Manual download

Browse releases:

https://github.com/orashus/tagviu/releases

Archives look like:

```text
tagviu_v0.1.0_darwin_arm64.tar.gz
tagviu_v0.1.0_darwin_amd64.tar.gz
tagviu_v0.1.0_linux_arm64.tar.gz
tagviu_v0.1.0_linux_amd64.tar.gz
tagviu_v0.1.0_windows_amd64.zip
checksums.txt
```

Verify the SHA-256 of your archive against `checksums.txt` before running the binary.

## Usage

```bash
# Copy the secret from Tagviu Dashboard → Developer → View
tagviu login <secret>
tagviu whoami
tagviu http://localhost:3000
tagviu http://localhost:3000 --json
tagviu https://orashus.com
tagviu https://orashus.com --json
tagviu https://orashus.com --save
tagviu mcp
tagviu logout
```

Optional API override:

```bash
export TAGVIU_API_URL=http://localhost:3000
# Optional: environment secret (overrides credentials.json)
export TAGVIU_API_KEY=api_…
```

Default API: `https://tagviu.orashus.com`

## Supported platforms

| OS | Arch |
| --- | --- |
| macOS | amd64, arm64 |
| Linux | amd64, arm64 |
| Windows | amd64 |

## What this CLI does

Fetches localhost HTML on your machine and submits it to Tagviu, or inspects a public URL with `POST /api/inspect` (`--save` creates a LocalPreview). Production Tagviu never fetches your localhost URL.

Local MCP (stdio): `tagviu mcp` (`TAGVIU_API_KEY` or `credentials.json`; `inspect_local_url` + `inspect_remote_url`) introduced in `v1.1.0`.
