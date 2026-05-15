# EJ Rolls — Features

A detailed look at what EJ Rolls does. (Marketing documentation — no implementation details.)

## Electronic Journal Parsing

EJ Rolls reads ATM Electronic Journals in the two shapes banks actually produce:

- **Printer-style `.txt`** — every line carries the `01:` (or other 1-3 digit) log-id prefix. The parser strips the prefix transparently.
- **EJ viewer `.pdf`** — multi-page exports from the journal viewer, with clean text.

The same parser handles both. For every host transaction block, it extracts:

- Transaction date and time
- ATM ID
- STAN and RRN
- PAN (masked, as the ATM prints it)
- Transaction type (withdrawal, balance check, invalid transaction, etc.)
- Amount
- Status code (APPROVED, LOW BALANCE, HOT CARD, TIMED OUT, …)

Result: one structured row per transaction, ready for analysis.

## GL Reconciliation

EJ Rolls matches every EJ transaction against the core-banking General Ledger:

- **Temenos T24 statement** format
- **TransactionsDetail** format

Both formats are auto-detected — the tool inspects the file structure and chooses the right parser.

Matching is keyed on **STAN** (the System Trace Audit Number — the primary transaction identifier shared across the ATM and the host), with amount and date used as confirmation.

The output classifies every row as:

- **Matched** — found in both EJ and GL with consistent amount/date.
- **Unmatched** — appears on one side but not the other.

## Status Categorisation

Raw ATM status codes are translated into three actionable buckets:

- **Approved** — `APPROVED`
- **Unable to Process** — `UNABLE TO PROCESS`, `TIMED OUT`, `SUSPECT : FAULTY DISPENSE`, `DISP REVERSAL`
- **Disapproved** — everything else (`LOW BALANCE`, `BAD PIN`, `HOT CARD`, `TXN NOT ALLOWED`, …)

The mapping is configurable.

## Excel Output

Three workbook types, all with consistent column ordering:

- **Full reconciliation workbook** — every transaction, matched or not.
- **Unmatched-only workbook** — same layout, filtered to investigation candidates.
- **EJ-only workbook** — for the case where you have EJ data but not yet the GL.

Each row contains: STAN, transaction amount, transaction date, time, masked PAN, transaction type, raw status, status category, ATM ID, RRN, GL match status.

## Multi-ATM Batch Processing

Handle a full ATM estate in one pass:

- Upload a **ZIP** of per-ATM subfolders.
- Upload a **folder** directly (browser directory upload).
- Upload **individual files**.
- Mix EJ and GL together; the tool routes each file to the right parser.

## Resilient Upload Sessions

A long reconciliation run shouldn't be lost to a server restart:

- Each upload session has a unique ID and is cached **both in memory and on disk**.
- The Flask debug auto-reloader (or any process restart) cannot lose your records.
- Idle sessions expire after 6 hours.

## Two-Stage Upload

Real banking workflows rarely deliver EJ and GL at the same moment:

- Upload **EJ first** — the tool keeps it and prompts for the GL when it's ready.
- Upload **GL first** — the tool keeps it and prompts for the EJ.
- Either way: the reconciliation runs the moment both sides are present.

## Live Preview

Before downloading the workbook, see the result in the browser:

- First 300 rows of the reconciliation.
- Matched / Unmatched / Unable-to-Process summary counts.
- Per-file ingest report — what was parsed, how many records, any skipped files.

## Built for Banking Operations

- Production-grade Python / Flask backend.
- Handles real-world ATM journal volume — thousands of records per file, hundreds of files per upload.
- Structured logging (workflow log + error log, both rotated).
- 200 MB total upload size — sized for full-day estate uploads.
