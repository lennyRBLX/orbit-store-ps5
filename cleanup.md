# Cleanup: erasing the Orbit work from this Mac

A checklist for removing this project, its sibling projects and the build tooling. Items
marked **(pre-existing)** were already on this Mac before this work started. Remove them only
if nothing else uses them.

> This file lives inside `orbit-store-ps5/`, so step 1 deletes it too. Read it through first,
> or copy it somewhere else.

> The native macOS build added `llvm@19` and `lld@19` (Homebrew) plus the in-tree items listed
> below. Nothing else was installed system-wide (no Docker, no sudo).

## 1. Project folders (~2.6 GB)

All under `/Users/jweaver/Desktop/Work/reversing/`:

- [ ] `orbit-store-ps5/` (~1.2 GB): the Orbit docs/feeds clone (remotes: your fork + upstream). Includes `.serena/`.
- [ ] `orbit-src-1.9.6/` (~2 GB after the build): the downloaded 1.9.6 source bundle zip, its
      extracted dependency archives (`src/`), `toolchain/` (83 MB: PS5 payload SDK v0.43 zip + unpacked SDK
      with the built PS5 libraries, and the `llvm19/` wrapper), and the edited working tree
      (`orbit/orbit-store-1.9.6/`, a local git repo with `build/` 131 MB, `.deps/` 448 MB, `node_modules/` 80 MB,
      `.venv/` 13 MB, `dist/`). It holds the modified source, `PEGASUS_DL_PORT.md`, `tools/build-macos.sh` and the
      built `build/orbit_store.elf`, so back up anything you want to keep first.
- [ ] Build temp dir used by `tools/build-deps.sh`: `/tmp/orbit-deps` (if present; cleared on reboot)
- [ ] `pegasus-dl/` (~296 MB)
- [ ] `kraken-mount-main/` (~2.4 MB)

```bash
rm -rf ~/Desktop/Work/reversing/orbit-store-ps5 ~/Desktop/Work/reversing/orbit-src-1.9.6 ~/Desktop/Work/reversing/pegasus-dl ~/Desktop/Work/reversing/kraken-mount-main
```

Not part of this work, but in the same folder. Review separately: `discovery/`, `RobloxStudio.7z`,
`decrypt_allocation_3.zip`, `decrypted_12.03.zip`, `the_finals_destruction.md`, `.DS_Store`.

## 2. Claude Code / tooling state for this project

- [ ] Claude Code project data (transcripts, memory) for this folder:
      `~/.claude/projects/-Users-jweaver-Desktop-Work-reversing-orbit-store-ps5/`
- [ ] Session scratchpad (temporary, cleared on reboot):
      `/private/tmp/claude-501/` entries for this session
- [ ] Serena global state, if you don't use Serena elsewhere: `~/.serena/` (the per-project `.serena/` goes with step 1)
- [ ] Serena/Ghidra MCP server entries in your Claude Code settings, if you added them only for this

```bash
rm -rf ~/.claude/projects/-Users-jweaver-Desktop-Work-reversing-orbit-store-ps5
```

## 3. Build tools

Native macOS build (Docker was not used, so no Docker/Colima/VM images to remove).

- [ ] Homebrew formulae installed for the build: `llvm@19` (19.1.7, keg-only, ~1.7 GB) and `lld@19` (19.1.7, keg-only, ~5 MB)
- [ ] PS5 payload SDK v0.43: inside `orbit-src-1.9.6/toolchain/`, so step 1 covers it
- [ ] `llvm` **(pre-existing)**
- [ ] `openssl@3`, `openssl@4` **(pre-existing)**
- [ ] `node` **(pre-existing)**
- [ ] `python@3.14` (Homebrew) and the python.org Python 3.14 framework **(pre-existing)**
- [ ] Command Line Tools for Xcode **(pre-existing)**. Remove with `sudo rm -rf /Library/Developer/CommandLineTools` only if nothing else needs them.

```bash
brew uninstall lld@19 llvm@19
```

```bash
brew autoremove
```

```bash
brew cleanup --prune=all
```

## 4. Caches

- [ ] npm cache (shared across all projects): `~/.npm/`. `npm cache clean --force` empties it.
- [ ] Homebrew download cache: `~/Library/Caches/Homebrew/` (cleared by `brew cleanup --prune=all`).
- [ ] pip cache, if the build's venv used it: `~/Library/Caches/pip/`

```bash
npm cache clean --force
```

## 5. Outside this Mac (optional)

- [ ] Your GitHub fork `lennyRBLX/orbit-store-ps5`: delete on GitHub if you want it gone entirely.
- [ ] Anything copied to the PS5 (e.g. `orbit_store.elf`, `/data/orbit-store/`, the `ORBT00001` icon).
- [ ] Terminal/shell history mentioning these paths: `~/.zsh_history`.
