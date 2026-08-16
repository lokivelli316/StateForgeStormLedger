# State Forge Storm Ledger — Public Replication Kit Design

Date: 2026-08-15
Status: APPROVED DESIGN

## Purpose

State Forge Storm Ledger is a public, reusable provenance-ledger kit that lets an ordinary person reproduce the same basic workflow with their own assistant and their own storage/custody systems.

The product is not a monument to one operator, one model, one repository, one cloud service, or one personal corpus. It must leave a tool behind.

A person should be able to find the repository and understand, through examples, how to:

1. connect or expose their normal work sources to an assistant;
2. tell the assistant what the ledger rules are;
3. inventory assets without silently modifying them;
4. post meaningful state changes as transactions;
5. preserve receipts, failures, corrections, and provenance;
6. reconcile the current state against the recorded history;
7. export or freeze a snapshot they can keep anywhere.

## Non-Negotiable Privacy Boundary

The public repository must contain none of the originating operator's private or personal ledger data.

Do not include:

- personal manuscripts;
- personal filenames;
- private repository names;
- personal Drive object IDs;
- personal hashes;
- private project history;
- personal model-seat history;
- real unpublished claims;
- personal account identifiers;
- real weekly ledger entries;
- copied private receipts.

The public starter and examples use fictional identities, fictional projects, synthetic hashes/commit IDs where examples need them, and generic account names.

## Product Shape

The public kit has four layers.

### 1. Standalone Ledger Application

A self-contained `index.html` remains the primary tool.

It must work locally in a normal browser without requiring a server or network connection for core ledger use.

Core books:

- Asset Registry
- Transaction Journal
- Provenance Accounts
- Infrastructure Assets
- Release Status
- Reconciliation
- Trial Balance
- Adjusting Entries

Core states include `LOCAL_PENDING_IMPORT`, so local work is legitimate inventory rather than falsely appearing missing.

### 2. Ledger Contract

`LEDGER_CONTRACT.md` is the portable behavioral contract a user can give to any capable assistant.

It defines the invariants that must survive changes in model or connector:

- `VERIFIED` is not `DISCOVERED`;
- `PUBLISHED` is not `VERIFIED`;
- agreement is not proof;
- supersession preserves the predecessor;
- failure does not erase the failed state;
- `UNKNOWN` cannot silently become `PASS`;
- merges preserve parentage;
- corrections preserve the state that required correction;
- copies are custody events, not independent evidence;
- infrastructure records who conceived, implemented, triggered, and retained authority;
- reconciliation diagnoses and never silently repairs.

A user should be able to say to an assistant:

> Read `LEDGER_CONTRACT.md` before touching my records. Inventory first. Do not edit source material unless I explicitly authorize it.

## 3. Connector / Assistant Replication Guide

The public documentation must not assume one assistant, one MCP client, or one storage provider.

The guide explains a connector ladder from easiest to most technical:

### Lane A — Built-in connection

If the user's assistant already has access to GitHub, Google Drive, Dropbox, OneDrive, local files, or another source, use that first.

### Lane B — Official MCP or native tool server

If the service exposes an official MCP server or equivalent tool interface, document that path with current official instructions.

### Lane C — Connector bridge

If the user wants one bridge to multiple services, document representative connector platforms such as Composio or Pipedream when current research confirms they support the needed service and client.

### Lane D — Direct API / CLI

For technical users, document ordinary REST/API or CLI access where appropriate.

### Lane E — Manual / no connector

The ledger must remain usable when no connector exists.

A person may:

- drag files into the local app;
- export JSON;
- paste commit SHAs or receipt text;
- manually register source locations;
- maintain the journal by hand.

Connectors reduce friction. They do not define the architecture.

## Connector Documentation Rule

Connector instructions age quickly. Before publishing or materially revising a connector page, research current official documentation first.

Each connector page should clearly separate:

- what is currently supported;
- what the user must configure;
- what permissions are being granted;
- whether the path is read-only or can write;
- how to test that the connection works;
- how to revoke access;
- what is unknown or provider-specific.

Do not copy secrets into examples.

Use placeholders such as:

- `GITHUB_TOKEN`
- `GOOGLE_CLIENT_ID`
- `MCP_SERVER_URL`

Secrets are not ledger data and must not be committed to the repository or stored in example ledgers.

## Permission Model

The beginner path is read-only first.

A new user should first prove that the assistant can:

1. see the intended source;
2. identify assets;
3. distinguish known facts from unknowns;
4. inventory without changing source material;
5. run reconciliation against the recorded ledger.

Write, delete, publish, merge, or remote mutation permissions belong behind a separate **Enable Actions** section.

The public kit must teach the difference between visibility and authority.

## Fictional Worked Example

The primary example operator is fictional.

### Jamie Rowan — Backyard Weather Station

Jamie is a hobby researcher building a backyard weather station.

Example custody:

```text
Google Drive
└── Weather Station/
    ├── Research Notes.docx
    └── Sensor Tests.xlsx

GitHub
└── jamie/weather-station
    ├── firmware/
    └── README.md
```

The walkthrough teaches by showing state transitions rather than by requiring accounting vocabulary first.

Example sequence:

1. Register existing Drive notes and GitHub repository as assets.
2. Record that the assistant inventoried them read-only.
3. Jamie creates a calibration-script requirement.
4. An assistant helps implement `calibration.py`.
5. Post a `BUILD` transaction with Jamie as conception/authority and the assistant as implementation assistance where appropriate.
6. A test fails; post `CHALLENGE` / `FAIL` without deleting the candidate.
7. Repair the script; post `CORRECTION`.
8. A separate check passes; post `VERIFICATION`.
9. Reconcile the project and inspect Trial Balance.
10. Export a JSON or standalone HTML snapshot.

The example should show that an AI generating code does not automatically become the inventor of the human's project.

## Beginner Documentation Style

Documentation must assume the reader may not know:

- MCP;
- OAuth;
- API;
- repository;
- commit;
- JSON;
- hash;
- provenance;
- custody;
- agent permissions.

Teach through concrete examples first, then name the technical concept.

Every setup guide should answer:

1. What am I connecting?
2. Why am I connecting it?
3. What can the assistant see?
4. What can the assistant change?
5. What should I click or configure?
6. How do I know it worked?
7. How do I undo or revoke it?
8. What should never be pasted into the ledger?

Avoid assuming expertise merely because a tool exposes an advanced interface.

## Repository Structure

Target structure:

```text
StateForgeStormLedger/
├── index.html
├── starter-ledger.json
├── example-ledger.json
├── README.md
├── START_HERE.md
├── CONNECT_YOUR_ASSISTANT.md
├── ARCHITECTURE.md
├── LEDGER_CONTRACT.md
├── PRIVACY_AND_SECRETS.md
├── examples/
│   └── jamie-weather-station/
│       ├── WALKTHROUGH.md
│       └── ledger.json
├── connectors/
│   ├── README.md
│   ├── github-mcp.md
│   ├── google-drive.md
│   ├── filesystem.md
│   ├── composio.md
│   ├── pipedream.md
│   ├── direct-api.md
│   └── manual-no-connector.md
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-08-15-public-replication-kit-design.md
```

Provider-specific files may change as the ecosystem changes; the ledger contract and core app must remain provider-agnostic.

## Data Flow

Default beginner flow:

```text
User's source systems
        ↓ read-only first
Assistant / MCP / connector / manual import
        ↓
Asset inventory
        ↓
Transaction posting
        ↓
Receipts + provenance accounts
        ↓
Reconciliation
        ↓
Trial Balance
        ↓
Export / freeze snapshot
```

Remote connectors never become the source of epistemic truth merely because they are connected. They are custody/access paths.

## Error Handling

The public kit must fail visibly.

Examples:

- connector cannot authenticate → mark connection unavailable; do not pretend inventory is complete;
- assistant cannot read a file → record `UNKNOWN` / inaccessible rather than inferring content;
- duplicate file appears → flag possible custody duplicate; do not count as independent evidence;
- source timestamp differs from upload timestamp → preserve both typed dates;
- assistant lacks write permission → keep operation read-only rather than silently asking for broader access;
- a write attempt fails → preserve failed execution receipt;
- example configuration is provider-stale → documentation must say the provider path requires re-verification.

## Testing Requirements

Before the public kit is considered ready:

1. **Privacy scan** — no originating operator private names, project names, hashes, filenames, or ledger records in public starter/example assets.
2. **Offline app test** — `index.html` opens and supports core ledger operations without network access.
3. **Starter-data test** — clean starter contains only generic/fake data.
4. **Example test** — Jamie walkthrough can be followed end-to-end and produces a coherent ledger.
5. **Reconciliation test** — intentionally broken fake records trigger the documented reconciliation findings.
6. **Read-only connector test** — at least one documented connector path proves inventory can occur without write authority.
7. **Manual fallback test** — a user with no connector can still complete the example using local/manual inputs.
8. **Secrets scan** — no literal credentials, tokens, API keys, cookies, or authorization headers committed.
9. **Provider-documentation check** — every connector page cites or points the reader to current official setup documentation and states the verification date.
10. **Terminology test** — a beginner can complete the first walkthrough without needing prior knowledge of provenance accounting.

## Success Criteria

The kit succeeds when a person unfamiliar with the originating project can:

- understand what the ledger is for;
- connect or manually expose at least one work source;
- give the ledger contract to their assistant;
- inventory assets without modifying them;
- post a build, failure/challenge, correction, and verification;
- understand why the original failed state remains visible;
- distinguish discovery, verification, publication, and custody;
- reconcile the example;
- export their own clean ledger snapshot;
- swap GitHub/Drive for another custody system without changing the ledger's core rules.

## Scope Boundary

This design does not attempt to build a universal connector runtime inside the single HTML file.

The ledger records and explains provenance. External assistants/connectors provide access to outside systems. Manual import remains a permanent supported path.

This keeps the application local-first, understandable, and portable while still teaching users how to integrate richer toolchains when they want them.

## Design Principle

The public project must optimize for transfer of capability, not preservation of personality.

If the original author disappears from the repository history, another person should still be able to understand the method, connect their own tools, operate the ledger, preserve their own receipts, and teach the next person.

**Leave the tool. Not the monument.**
