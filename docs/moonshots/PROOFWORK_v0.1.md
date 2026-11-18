# ProofWork v0.1 — Proof-Carrying Work

Status: SCHEMA SEED / NOT A STANDARD

ProofWork makes provenance and epistemic state travel with an artifact.

The core claim is narrow: a file can carry enough structured lineage to answer what it is, where it came from, what changed, which claims are merely proposed, what evidence exists, what tests ran, what failed, and what superseded what.

## Compatibility doctrine

- StateForge remains append-only-in-meaning.
- LokivelliLedger accounting semantics remain distinct from epistemic truth.
- Debleeder evidence remains evidence, not a verdict.
- Hashes prove byte identity, not truth.
- Verification requires recorded evidence; agreement is not verification.

## v0.1 artifact

`proofpack/proofpack.schema.json`

## Mandatory semantic gates for the future validator

- UNKNOWN cannot silently become PASS.
- DISCOVERED cannot silently become VERIFIED.
- CORRECTION creates a successor and preserves the predecessor.
- SUPERSEDED preserves parentage.
- FAIL remains in history.
- Publication status and epistemic status remain orthogonal.

## First reference workflow

```text
REGISTER ARTIFACT
 -> ATTACH CLAIMS
 -> ATTACH EVIDENCE / TESTS
 -> RECORD TRANSITION
 -> VALIDATE TRANSITION
 -> EMIT PROOFPACK
 -> OPTIONAL STATEFORGE TRANSACTION
 -> STATIC OFFLINE REVIEW
```
