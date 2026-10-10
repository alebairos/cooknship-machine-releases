# cooknship-machine releases

Binaries of **cooknship**, a delivery machine for software agents: you park the work, any number of agents in any harness plan, build, review and land it in parallel, and a pure kernel refuses every step that breaks a law. The ledger is a branch of your git host; there is no server.

This repo holds releases only, not the source.

## Install

```bash
curl -fsSL https://github.com/alebairos/cooknship-machine-releases/releases/latest/download/install.sh | sh
cooknship --version
```

`install.sh` carries the sha256 of each archive of its release and refuses anything that does not match. It installs `cooknship` and `cooknship-gate` into `~/.local/bin` (set `COOKNSHIP_BIN` to change it). Builds: Linux x86_64 (static), macOS arm64.
