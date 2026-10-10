# GhostGuard Distribution — local deliverables

Five standalone plays that take GhostGuard to where agents already
run. Built Oct 10, 2026 on Ryan's "Knock em out" — **nothing here
is published, pushed, or deployed**; the package is `private: true`,
zero runtime dependencies, Node ≥ 18, ESM.

Every suite runs against the **real** GhostGuard engine, imported
read-only from `~/workspace/ghostguard/dist`. The core package and
`~/workspace/agent-seatbelt` are never modified.

| Folder | What it is | Suite |
|---|---|---|
| `github-action/` | Composite GitHub Action + gate script: a workflow step fails unless the trail records the required action allow/pre_approved (optionally + matching approval). Delivered as files + local simulation. | 9 cases |
| `redteam-bench/` | Versioned attack corpus (**v1**, 16 cases): injection-shaped + encrypted-looking payloads, hostile overlays, approval spoofs, classification spoofs, benign controls — asserting no attack executes a consequential action. | 16 cases |
| `policy-author/` | Controlled-English → GhostGuard `policy.json` + generated behavior tests from the same statements. Unsupported sentences error loudly, never silently drop. | 18 checks |
| `approval-channels/` | Ask-notifier: POSTs a pending ask to a generic webhook (generic/Slack/Discord/Telegram shapes) with escalation metadata and **timeout = deny** as a fail-closed decisions-JSONL entry. Tests hit a local stub server only. | 18 checks |
| `browser-lite/` | Single-file `ghostguard-lite.js`: classifyAction for DOM-ish actions, mini policy evaluator, record sink — with verdict parity vs the real engine on shared fixtures. | 30 checks |

## Verify everything
```sh
npm run verify   # 5 suites, 91 checks total
```

See `REPORT.md` for the full results and honest limits, and each
subfolder's `README.md` for its own details.

## Repository layout note

This add-on imports the GhostGuard core engine from a **sibling checkout**:
`../../ghostguard/dist/index.js` (its source and/or tests do; nothing in the
core is modified). To run it, clone the core next to this repo so both folders
share a parent directory:

```sh
git clone https://github.com/littlestjames82-sys/ghostguard
git clone https://github.com/littlestjames82-sys/ghostguard-distribution
# build the core once so dist/ exists:
cd ghostguard && npm run build && cd ..
cd ghostguard-distribution && npm test
```

Part of the GhostGuard family by **Ghost Developer Studio**.
