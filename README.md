# research-tool

CLI tool to scaffold new Lean 4 + Mathlib research projects.

Inspired by [tobiasosborne/ProjSeminorm](https://github.com/tobiasosborne/ProjSeminorm).

## Usage

```
research new                  scaffold a new project (interactive)
research list                 list all managed projects (with full paths)
research delete NAME          delete a project (local directory + GitHub repo)
research completion           print shell completion script
research completion install   add completion to ~/.zshrc
```

`research new` prompts for:
- Project name (required, must be unique)
- Parent directory (default: `~/Research`, created if absent)
- Research question (default: placeholder)
- GitHub visibility: private / public / local (default: private)

Then creates the full project skeleton, makes an initial git commit, and
pushes a new GitHub repo (unless visibility is `local`).

## Setup (one-time)

```bash
# Clone the repo (choose any location you like)
git clone https://github.com/MarkAureli/research-tool

# Make the script executable
chmod +x research-tool/research

# Add to PATH via symlink
ln -s "$(pwd)/research-tool/research" ~/.local/bin/research
```

Make sure `~/.local/bin` is on your `PATH` (add to `~/.zshrc` if needed):

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Then enable shell completion (zsh):

```bash
research completion install
source ~/.zshrc
```

## Updating

```bash
cd /path/to/research-tool && git pull
```

## Project skeleton

Each new project contains:

| File | Purpose |
|------|---------|
| `LICENSE` | Apache License 2.0 |
| `lean-toolchain` | Lean version pin |
| `lakefile.toml` | Lake config with mathlib v4.27.0 |
| `lake-manifest.json` | Lockfile |
| `.gitignore` | Ignores `.lake/` and `references/` |
| `<Name>.lean` | Root import |
| `<Name>/Basic.lean` | Initial stub |
| `CLAUDE.md` | Build command + project notes |
| `AGENTS.md` | Agent instructions |
| `.mcp.json` | Lean 4 LSP MCP server (`lean-lsp-mcp` via `uvx`) |

`af` (vibefeld) is available for adversarial proof trees but not initialised at scaffold time — it requires a specific conjecture. See `AGENTS.md` for usage.

## Acknowledgements

Project structure inspired by
[tobiasosborne/ProjSeminorm](https://github.com/tobiasosborne/ProjSeminorm).
