# cooknship-machine releases

Binaries of **cooknship**, a delivery machine for software agents: you park the work, any number of agents in any harness plan, build, review and land it in parallel, and a pure kernel refuses every step that breaks a law. The ledger is a branch of your git host; there is no server.

This repo holds releases only, not the source. The release workflow of the source repo writes this README (from `release/README.md` and `release/quickstart.md` there) at each release; edits here are overwritten.

<!-- quickstart: generated from release/quickstart.md; do not edit here -->
## Quick start

In a clone of the GitHub repo to run cooknship on (you need push access, and `gh` logged in). The repo is the one you are in (its `origin`): don't look for others.

The source repo is private: this release (its notes, the releases repo's README, what `install.sh` prints) and the `AGENTS.md` init writes have everything you need. Don't inspect the binary or look for the source; ask the CLI: `cooknship --help`, `cooknship schema [COMMAND]`.

```bash
curl -fsSL https://github.com/alebairos/cooknship-machine-releases/releases/download/v0.1.22/install.sh | sh
cooknship init     # at a terminal: guided; an agent gets the two choices, with their commands
cooknship doctor   # checks the host; changes nothing
cooknship next
```

- **At a terminal**, bare `cooknship init` asks for the host, the products and the tokens (the test, the check and the toolchains are your agent's, from `next`), shows the plan (`will do`, `nothing to do`, or `needs <who>`: an admin, you, a signer, the HITL, or another step first) and runs it once you confirm. It starts with `signer: <login> (this session's GitHub login; …)`.
- **An agent** gets the two choices (the host is its own product, or products in their own repos) as `choices`, each with its command: show them to your human and run the one they pick, with the `handoff` lines as printed.
- **Rerun `init` any time:** the same flags change nothing, and on a set-up host bare `init` is the doctor. To change the test, the products or AGENTS.md: `cooknship init --refresh`.
- **Creates:** the `cooknship/ledger` branch, and `AGENTS.md` and the agent skills on `main` (one commit). `cooknship/book` comes with the first landing or `init --refresh`. It fast-forwards your clone when it is clean on `main`; otherwise run the `local` command it prints, before the workflow step.
- **The land workflow** (step `workflow`: `cooknship init --workflow --single-repo --land <mode>` into `.github/workflows/cooknship-land.yml`, `pr` by default, `direct` with `--land direct`): init does not commit it for an agent; at a terminal it writes it into your clone and offers to push it. The required `cooknship` check on `main` waits for it: run `cooknship init --refresh` after (it adds the check); `cooknship doctor` shows when it is in place.
- **Admin rights** on the repo are needed to protect the ledger branch, require the check, turn rebase merging off and, in `pr` mode, "Allow GitHub Actions to create and approve pull requests" (step `pull-requests`). Without them, init does the rest and prints the exact handoff for someone who has them; list them for your human in your report and continue: an agent session never runs them, even when its token can.
- **Then** init's last line is `cooknship: Done. Next: cooknship next`. This session runs the command on that line, with no `--as`: a bare `next` runs as your GitHub login, the signer. `AGENTS.md` says how sessions the human starts later get their ids; don't invent one.
<!-- quickstart end -->

## Install

```bash
curl -fsSL https://github.com/alebairos/cooknship-machine-releases/releases/latest/download/install.sh | sh
cooknship --version
```

`install.sh` carries the sha256 of each archive of its release and refuses anything that does not match. It installs `cooknship` and `cooknship-gate` into `~/.local/bin` (set `COOKNSHIP_BIN` to change it). Builds: Linux x86_64 (static), macOS arm64.
