# agent-specs

> Canonical agent definitions for **Mad River AI**. Prompts, tool schemas, behavior contracts, eval scenarios.

This is the "brain" of the operation. While [`osint-framework`](../osint-framework) is the runtime, this repo is the specifications that get loaded *into* the runtime. Treat these files as **versioned**, **reviewable**, and **diffable** — they are the product.

🔗 https://madriverai.com &nbsp;·&nbsp; 🐙 https://github.com/Mad-River-AI

---

## What lives here

```
agent-specs/
├── agents/                 # named agent definitions (one folder each)
│   ├── company-investigator/
│   │   ├── agent.yaml      # identity, goal, constraints
│   │   ├── system.md       # system prompt
│   │   ├── tools.yaml      # which tools it can call
│   │   ├── eval.yaml       # test scenarios
│   │   └── notes.md        # design rationale
│   ├── domain-recon/
│   ├── leak-triage/
│   └── ...
├── shared/                 # prompt fragments, style guides, personas
├── evals/                  # cross-agent eval suite
└── CHANGELOG.md            # semver of every agent version
```

## Agent definition format (v0.1)

A complete agent is **one folder** with these files:

- `agent.yaml` — machine-readable metadata: name, version, owner, status, tags
- `system.md` — the actual system prompt, written in markdown for readability
- `tools.yaml` — which tools (from `osint-framework/tools/`) the agent is allowed to call, plus per-tool constraints
- `eval.yaml` — at least 3 test scenarios: a happy path, an edge case, and a refusal/limit case
- `notes.md` — human prose: what this agent is for, when *not* to use it, known failure modes

## The roster (planned)

| agent | purpose | status |
|---|---|---|
| `company-investigator` | Given a name or domain, produce a structured company dossier (officers, filings, online presence, risk signals) | drafting |
| `domain-recon` | WHOIS/DNS/social handle sweep, brand conflict check, parking/for-sale signal | building (see `~/AppData/Local/hermes/scripts/madriverai-recon.py`) |
| `leak-triage` | Given a paste, file, or document, classify + verify + score sensitivity | planned |
| `person-trace` | Given name + context, build a public-source profile (social, court, business) | planned |
| `meta-agent` | Orchestrator that picks agents and pipelines for a goal | research |

## Status

🚧 **Pre-alpha.** The first agent (`domain-recon`) is already running nightly against `madriverai.com` and is being generalized. `company-investigator` is the next target.

## Why specs-as-code?

Because:

- **Reviewable.** A PR on an agent spec is the unit of work. Reviewers can read the diff and judge if the agent got dumber or smarter.
- **Reproducible.** Given the same spec + same tools, the same agent runs the same way.
- **Auditable.** "Why did the agent do X?" → open the spec, see the prompt + tool list.
- **Swappable.** Specs aren't tied to a single model. Same YAML works on MiniMax, Claude, GPT, local Ollama.

## License

MIT. See [LICENSE](LICENSE).

## Contact

- Issues: this repo
- Owners: [@muzzy111](https://github.com/muzzy111), [@trip7s](https://github.com/trip7s)

---

*Spec'd in Indiana. Run on whatever model the budget can carry.*
