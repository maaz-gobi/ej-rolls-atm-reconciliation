# EJ Rolls — Use Cases

Real-world problems EJ Rolls solves for banks and financial-systems teams.

## End-of-Day ATM Balancing

The classic reconciliation use case. At end of day, every ATM in the estate must balance: what the ATM journal says it dispensed, against what the core-banking GL recorded. EJ Rolls automates the whole pass — upload the day's EJ rolls and the GL extract, get a matched / unmatched workbook in seconds.

## ATM Exception & Dispute Investigation

When a customer disputes a transaction or a cash variance is reported, the investigation team needs to trace one STAN across EJ and GL. EJ Rolls's unmatched-only workbook is exactly that focus list — one row per item that needs attention, with the raw status, the GL match status, and all the identifiers the team needs.

## Core-Banking UAT & Migration Cutovers

During a Temenos T24 (or other core-banking) upgrade or migration, ops teams reconcile production-like ATM activity against the upgraded GL to catch posting-rule changes early. EJ Rolls is built around exactly this workflow — the original engagement was a T24 UAT cycle.

## Multi-ATM Estate Reconciliation

Banks with dozens or hundreds of ATMs can't reconcile each terminal manually. EJ Rolls accepts a ZIP or folder structure organised by ATM ID, processes every terminal in one pass, and produces a single consolidated workbook covering the whole estate.

## Internal Audit & Compliance Sampling

When auditors need to verify that ATM cash activity reconciles to the GL with full traceability, EJ Rolls gives them a complete audit trail: every raw status, every matched and unmatched pair, every STAN. Stable column layout means the workbook is sampling-friendly.

## Faulty-Dispense and Reversal Tracking

The "Unable to Process" status bucket isolates timeouts, faulty dispenses, and dispense reversals — the categories that matter most for cash variance investigation. The investigations team can filter to this bucket and trace each event without scanning the full journal.

## Operations Teams Without Engineering Support

EJ Rolls runs as a self-contained web app — drag-and-drop upload, no command line, no scripts to maintain. Ops teams can use it directly without needing engineering help for every reconciliation cycle.

---

**Have a different use case?** See the Contact section in the main [README](../README.md) — we'd like to hear about it.
