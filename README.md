# Adversarial-AI-Greenroom

[![License](https://img.shields.io/github/license/ScottColeSW/Adversarial-AI-Greenroom)](LICENSE)

> A local testbed that measures what actually contains an AI agent: charters, enforcement levels, trust tiers, and human versus automatic approval.

## Status: design stage

Nothing in this repository has been built or measured yet. The design is in [`docs/SPEC.md`](docs/SPEC.md). Every claim this repository will make must come from a saved run, with predictions written down before the runs and misses reported. Until there are runs, there are no results, and this README makes none.

## What this is, and what it is not

**What it will be.** A local, keyless testbed for one question: how much authority should an AI agent get, and what is the evidence? An agent is given a declared charter, every action it proposes passes through an enforcement layer it cannot reach, and a trust ladder decides when it earns more authority. The testbed attacks that arrangement with scripted and adaptive adversaries and reports what held, what it cost in lost legitimate work, and how much damage a fully compromised agent could still do.

**What it is not.**
- It is not a security product. The scenarios will be written by the author, and no outside adaptive attacker has tried to beat the design.
- It does not claim that charters, policy enforcement, audit logs, trust tiers, or human approval are new. Other agent governance projects have them. The contribution is meant to be the measurements.
- It is not a comparison against other governance tools.
- It does not enforce an agent's intent in v0.
- The pure Python mode proves policy logic against a virtual world. Only the container mode tests operating system containment.

## The four questions

The design is organized around what executives keep asking, and each question maps to a mechanism and a measurement.

- What can it do if it goes wrong? Charter, enforcement, tiers. Measured as blast radius and attack success rate.
- Who is responsible for it? A named owner, a registry, and delegation rules.
- Can we stop it and undo it? A kill switch, snapshots, and rollback.
- Can you prove what it did? A hash-chained ledger and a verifier.

Underneath is a fifth: what does all this cost in speed? Utility is always reported beside protection.

## How it is meant to work

- **Charter.** A declarative file per agent role, the job description. Default deny.
- **Arch.** The enforcement layer between the agent and the world. Every proposed action is canonicalized, matched against the charter, checked against the agent's tier, and classified as allow, deny, or hold.
- **Ledger.** A tamper-evident record of every attempt, written before anything executes.
- **Trust ladder.** A new agent starts in the green room, where it proposes and nothing executes. It earns reads, then reversible writes, then committed actions, from evidence, and any violation demotes it.
- **Enforcement levels.** From no enforcement, through prompt-only, to the arch, to the arch plus a hardened container. The experiments compare them head to head.
- **Decision switch.** Holds and promotions can be decided automatically, by a human, or by both with the human binding and the disagreement measured.

The name comes from the theater metaphor of the Agent Theater Framework: the charter is the theater, the arch is the proscenium, and the green room is where performers wait before they go on stage.

## Documents

- [`docs/SPEC.md`](docs/SPEC.md): the full design specification, currently draft 0.4.
- [`docs/aux/PALIMPSEST-INTEGRATION.md`](docs/aux/PALIMPSEST-INTEGRATION.md): how the memory gate is used, and the changes it needs.

## First milestone

A single command that runs a scripted chmod attempt against an agent with no enforcement and against the arch, and prints the ledger so the difference is visible. The agent runs against a virtual world, so the demonstration cannot touch your machine. No API key or Docker is required for this step.

## Related projects

- [Project Aegis Vector](https://github.com/ScottColeSW/Project-Aegis-Vector): the adversarial testbed whose method this project follows.
- [Palimpsest](https://github.com/ScottColeSW/Palimpsest): the curated memory library used as the memory gate.

Built by Scott A. Cole ([github.com/ScottColeSW](https://github.com/ScottColeSW)).

## License

MIT. See the [LICENSE](LICENSE) file.