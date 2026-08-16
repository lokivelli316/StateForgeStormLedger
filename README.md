# State Forge Storm Ledger

A standalone, local-first provenance ledger for projects, research, software, creative work, reviews, publications, and automation.

The application is a **single HTML file**. Open `index.html` in a normal browser. No server, database service, account, or network connection is required.

## What the name means

- **State** — what is recorded as current now.
- **Forge** — the controlled changes that move one state into another: build, test, challenge, repair, merge, publish, rollback.
- **Storm** — failures, uncertainty, disagreement, pressure, blocked releases, and other conditions that must remain visible rather than being cleaned out of the history.
- **Ledger** — the append-only-in-meaning record connecting assets, actors, transactions, evidence, and custody.

This is not financial accounting software. It borrows double-entry discipline to enforce a provenance invariant:

> Every current state must have an origin, and every state that stops being current must land somewhere rather than silently disappear.

A failed test can balance. An unresolved question can balance. A rejected claim can balance. Balance means the recorded state can be explained by the recorded history.

## Five-minute start

1. Open `index.html`.
2. Read **Start Here**.
3. Create accounts for yourself, your project, and any model/agent/tool that materially acts.
4. Register existing local files. They enter as `LOCAL_PENDING_IMPORT`; the app does not upload them.
5. Post transactions for meaningful changes such as `BUILD`, `CHALLENGE`, `VERIFICATION`, `CORRECTION`, `MERGE`, `PUBLICATION`, or `ROLLBACK`.
6. Run **Reconciliation**. It reports exceptions but never repairs them automatically.
7. Review **Trial Balance**.
8. Export JSON or a standalone HTML snapshot for durable custody.

## The books

| Book | Purpose |
|---|---|
| Asset Registry | Durable things that exist: files, datasets, code, builds, frozen versions, publications, local inventory |
| Transaction Journal | Meaningful state changes and custody moves |
| Provenance Accounts | Humans, models, agents, automations, projects, repositories |
| Reconciliation | Read-only exception detection |
| Trial Balance | Whether the current state reconciles under the recorded history |

## Important rules

- `VERIFIED` is not the same as `DISCOVERED`.
- `PUBLISHED` is not the same as `VERIFIED`.
- Model agreement is not proof.
- A later reviewer does not become the discoverer of an earlier finding.
- `SUPERSEDED` does not erase the predecessor.
- `FAIL` does not delete the claim or test.
- `UNKNOWN` cannot silently become `PASS`.
- A merge preserves parentage.
- A correction preserves the state that required correction.
- A copied file is a custody event, not independent evidence.
- Automation does not erase the human transaction that designed or authorized the automation.
- Reconciliation diagnoses. It does not silently repair.

## Local / Pending Import

`LOCAL_PENDING_IMPORT` is a legitimate inventory state for work that exists locally but has not yet been posted into Git, Drive, a publication system, or another custody store.

## Files in this repository

- `index.html` — self-contained application
- `starter-ledger.json` — clean generic seed ledger
- `LEDGER_CONTRACT.md` — portable rules to give any assistant
- `PRIVACY_AND_SECRETS.md` — hard privacy boundary
- `examples/jamie-weather-station/` — fictional worked example
- `docs/superpowers/specs/2026-08-15-public-replication-kit-design.md` — original design intent

## Privacy

This public kit contains only generic and fictional data.
It is designed so another person can take the method without inheriting any private history of the original operator.

See `PRIVACY_AND_SECRETS.md`.

## Design principle

Leave the tool. Not the monument.
