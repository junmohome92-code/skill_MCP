# Setup

## 1. WSL — recommended main Codex environment

Prerequisites:

```bash
node --version
npm --version
docker --version
docker compose version
codex --version
```

Playwright MCP requires Node.js. The current Playwright MCP documentation recommends Node.js 20 or newer.

Copy the relevant MCP blocks from:

```text
configs/wsl.config.example.toml
```

into:

```text
~/.codex/config.toml
```

Then restart Codex.

## 2. Context7

This workspace uses the hosted HTTP MCP endpoint:

```toml
[mcp_servers.context7]
url = "https://mcp.context7.com/mcp"
```

Context7 can work without putting a secret in this repository. If you later use an API key, store it only in an environment variable/local secret store and configure Codex to read the environment variable.

## 3. Playwright

Codex-compatible configuration:

```toml
[mcp_servers.playwright]
command = "npx"
args = ["-y", "@playwright/mcp@latest"]
```

On a headless server:

```toml
args = ["-y", "@playwright/mcp@latest", "--headless"]
```

## 4. Docker Desktop MCP Toolkit

Docker Desktop 4.62+ provides MCP Toolkit.

Recommended setup:

1. Docker Desktop → Settings → Beta features → enable **Docker MCP Toolkit**.
2. MCP Toolkit → Profiles → create profile **codex-dev**.
3. Catalog → add the MCP servers you want, for example **GitHub Official**.
4. WSL Codex connects to that profile with:

```toml
[mcp_servers.docker_toolkit]
command = "docker"
args = ["mcp", "gateway", "run", "--profile", "codex-dev"]
```

This keeps multiple Docker-hosted MCP servers behind one gateway instead of adding every server separately to Codex.

## 5. GitHub

Preferred on the Windows/WSL development PC:

- Add **GitHub Official** to the Docker MCP Toolkit `codex-dev` profile.
- Complete authentication in Docker Desktop.
- Do not commit a GitHub PAT to this repository.

If you later decide to run GitHub MCP directly instead of through Docker Toolkit, keep the token in an environment variable.

## 6. Filesystem and Git

Do **not** add these by default.

Codex already operates on the local project filesystem and can execute:

```bash
git status
git diff
git log
git commit
```

Adding separate Filesystem/Git MCP servers usually duplicates existing capabilities. Add them only if a specific workflow requires an isolated/root-limited MCP interface.

## 7. Suggested split

### WSL
- Context7: ON
- Playwright: ON when doing web work
- Docker Toolkit: ON
- GitHub: via Docker Toolkit
- Filesystem/Git MCP: OFF

### Windows
- Same as WSL only when using Windows Codex directly.
- Otherwise keep Windows Codex minimal.

### Home server
- Context7: ON
- Playwright: OFF by default
- Docker MCP Toolkit: not needed
- Docker/Git/files: use native CLI

## 8. Never commit

Never commit:

- GitHub PAT
- Context7 API key
- OpenAI API key
- `.env`
- OAuth credential/cache files
- your real `~/.codex/config.toml` if it contains secrets

Use the example files in this repo as the source of truth and merge them manually into each machine's local Codex config.
