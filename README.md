# cooknship-machine releases

Binaries of **cooknship**, a delivery machine for software agents: you park the work, any number of agents in any harness plan, build, review and land it in parallel, and a pure kernel refuses every step that breaks a law. The ledger is a branch of your git host; there is no server.

This repo holds releases only, not the source. The release workflow of the source repo writes this README (from `release/README.md` and `release/quickstart.md` there) at each release; edits here are overwritten.

<!-- quickstart: generated from release/quickstart.md; do not edit here -->
## Quick start

In a clone of the GitHub repo to run cooknship on (you need push access, and `gh` logged in). The repo is the one you are in (its `origin`): don't look for others.

The source repo is private: this release (its notes, the releases repo's README, what `install.sh` prints) and the `AGENTS.md` init writes have everything you need. Don't inspect the binary or look for the source; ask the CLI: `cooknship --help`, `cooknship schema [COMMAND]`.

```bash
curl -fsSL https://github.com/alebairos/cooknship-machine-releases/releases/download/v0.1.28/install.sh | sh
cooknship init --single-repo --test '<the command that runs the whole suite>'
cooknship next
```

- **`init` never prompts and gives no advice:** one line per step, `will do`, `nothing to do`, or `needs <who>` (an admin, you, a signer, the HITL, or another step first) with the exact call it did not make. The test command is yours to pick by reading the product; without `--test` landings wait. Products in their own repos: `--product <name>=<url>` instead of `--single-repo`.
- **Rerun `init` any time:** the same flags change nothing, and on a set-up host bare `init` (or `init --plan`) is the checklist, exit 1 while anything is missing. To change the test, the products or AGENTS.md: `cooknship init --refresh`.
- **Creates:** the `cooknship/ledger` branch, and `AGENTS.md` and the agent skills on `main` (one commit). `cooknship/book` comes with the first landing or `init --refresh`. It fast-forwards your clone when it is clean on `main`; otherwise run the `local` command it prints, before the workflow step.
- **The land workflow** (step `workflow`: `cooknship init --workflow --single-repo --land <mode>` into `.github/workflows/cooknship-land.yml`, `pr` by default, `direct` with `--land direct`): init does not commit it. The required `cooknship` check on `main` waits for it: run `cooknship init --refresh` after.
- **Admin rights** on the repo are needed to protect the ledger branch, require the check, turn rebase merging off and, in `pr` mode, turn on merge commits and auto-merge and "Allow GitHub Actions to create and approve pull requests" (step `pull-requests`). Without them init does the rest; list them for your human in your report and continue: an agent session never runs them, even when its token can. `AGENTS.md`'s Onboarding says what to do with each line.
- **Then** init's last line is `cooknship: Done. Next: cooknship next`. This session runs the command on that line, with no `--as`: a bare `next` runs as your GitHub login, the signer. `AGENTS.md` says how sessions the human starts later get their ids; don't invent one.
- **The human** decides twice per intent, the plan and the result (plus a yes for a risky landing). They read the book (`cooknship/book`) and answer with `cooknship decide` or by telling their operator, who relays it under their signer id.
<!-- quickstart end -->

## Install

```bash
curl -fsSL https://github.com/alebairos/cooknship-machine-releases/releases/latest/download/install.sh | sh
cooknship --version
```

`install.sh` carries the sha256 of each archive of its release and refuses anything that does not match. It installs `cooknship` and `cooknship-gate` into `~/.local/bin` (set `COOKNSHIP_BIN` to change it). Builds: Linux x86_64 (static), macOS arm64.
