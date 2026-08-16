# Ledger Contract

Give this file to any capable assistant before it touches your records.

## Purpose

This contract defines the invariants that must survive changes in model, connector, or operator.

## Core invariants

1. `VERIFIED` is not the same as `DISCOVERED`.
2. `PUBLISHED` is not the same as `VERIFIED`.
3. Model agreement is not proof.
4. A later reviewer does not become the discoverer of an earlier finding.
5. `SUPERSEDED` does not erase the predecessor.
6. `FAIL` does not delete the claim or the test.
7. `UNKNOWN` cannot silently become `PASS`.
8. A merge preserves parentage.
9. A correction preserves the state that required correction.
10. A copied file is a custody event, not independent evidence.
11. Automation does not erase the human transaction that designed or authorized the automation.
12. Reconciliation diagnoses. It does not silently repair.

## Inventory first

Before any mutation:

- inventory existing assets
- distinguish known facts from unknowns
- do not edit source material unless the human operator explicitly authorizes it

## Authority

Human final authority remains with the operator of the ledger.
Assistants, models, and automations are recorded as distinct actors.
They do not become the author of work they only assisted.

## Local / Pending Import

`LOCAL_PENDING_IMPORT` is a legitimate state.
Work that exists only on a local machine is still inventory.
Do not treat it as missing simply because it has not yet been committed or uploaded.

## Failure visibility

Failed tests, rejected claims, unresolved questions, and blocked releases must remain visible in the history.
Cleaning them out of the record is a violation of this contract.

## Export and custody

The working state in the browser is temporary.
Durable custody requires an explicit export (JSON or standalone HTML snapshot) stored under the operator's control.
