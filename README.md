# research-tool

CLI tool to scaffold new Lean 4 + Mathlib research projects.

## Usage

```bash
research
```

Prompts for:
- Project name (required)
- Parent directory (default: `~/Code`)
- Research question (default: placeholder)
- GitHub visibility: private / public (default: private)

Then creates the full project skeleton, makes an initial git commit, and
pushes a new GitHub repo.

After the project is created, fetch the Mathlib cache:

```bash
cd ~/Code/<project-name> && lake exe cache get
```

## Setup (one-time)

```bash
# Clone the repo
git clone https://github.com/lennartbinkowski/research-tool ~/Code/research-tool

# Make the script executable
chmod +x ~/Code/research-tool/research

# Add to PATH via symlink
ln -s ~/Code/research-tool/research ~/.local/bin/research
```

Make sure `~/.local/bin` is on your `PATH` (add to `~/.zshrc` if needed):

```bash
export PATH="$HOME/.local/bin:$PATH"
```

## Updating

```bash
cd ~/Code/research-tool && git pull
```

## Project skeleton

Each new project contains:

| File | Purpose |
|------|---------|
| `lean-toolchain` | Lean version pin |
| `lakefile.toml` | Lake config with mathlib v4.27.0 |
| `lake-manifest.json` | Lockfile |
| `.gitignore` | Ignores `.lake/` and `references/` |
| `<Name>.lean` | Root import |
| `<Name>/Basic.lean` | Stub with `import Mathlib` |
| `CLAUDE.md` | Build command + project notes |
| `HANDOFF.md` | Mathematical context + session log |
| `AGENTS.md` | Agent instructions |
