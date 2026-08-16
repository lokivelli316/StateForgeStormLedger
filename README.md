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
4. Register existing local files. They enter as `LOCAL_PENDING_IMPORT`; the app hashes the bytes in your browser and does not upload them.
5. Post transactions for meaningful changes such as `BUILD`, `CHALLENGE`, `VERIFICATION`, `CORRECTION`, `MERGE`, `PUBLICATION`, or `ROLLBACK`.
6. Add reusable scripts, validators, dashboards, automations, routers, and launchers as **Infrastructure Assets**.
7. Run **Reconciliation**. It reports exceptions but never repairs them automatically.
8. Review **Trial Balance**.
9. Export JSON or a new self-contained HTML snapshot for a milestone or weekly close.

## The books

| Book | Purpose |
|---|---|
| Asset Registry | Durable things that exist: files, datasets, code, builds, frozen versions, publications, local inventory |
| Transaction Journal | Meaningful state changes and custody moves |
| Provenance Accounts | Humans, models, agents, automations, projects, repositories, review stages, publication boundaries, evidence classes |
| Infrastructure Assets | Reusable workflow machinery and its lifecycle |
| Release Status | Claim/thesis state separated from publication/deployment state |
| Reconciliation | Read-only exception detection |
| Trial Balance | Whether the current state reconciles under the recorded history |
| Adjusting Entries | Proposed corrections/reclassifications that remain separate until explicitly posted |

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

Registering a local file:

- computes a SHA-256 hash in the browser;
- records file size and local path/name;
- does **not** upload the file;
- does **not** infer the original creation date;
- does **not** claim the file exists anywhere else.

When the file is later uploaded or committed, record that as an `IMPORT`, `EXPORT`, `COPY`, `MIRROR`, or other explicit custody transaction.

## Trial Balance states

- `BALANCED`
- `BALANCED_WITH_ADJUSTING_ENTRIES_REQUIRED`
- `MATERIALLY_UNRECONCILED`
- `UNRECONCILABLE_FROM_AVAILABLE_RECORD`

The result is diagnostic, not a truth score.

## Persistence

The app stores the working state in browser `localStorage` when available. For durable custody, export one or both of:

- JSON — machine-readable ledger.
- Standalone HTML — the application plus the current ledger snapshot baked into one file.

For stronger history, store milestone/weekly snapshots in Git or another independent custody system.

## Files in this repository

- `index.html` — self-contained application.
- `starter-ledger.json` — clean generic seed ledger.
- `ARCHITECTURE.md` — data model, invariants, reconciliation rules, and extension guidance.
- `EXAMPLE_WORKFLOW.md` — a small worked example showing how a normal person can post a project without accounting jargon.

## Privacy

The starter application contains no personal project inventory or private manuscript data. All browser operations are local unless the user separately chooses to move exported files somewhere else.
