# EJ Rolls — Frequently Asked Questions

## General

**What is EJ Rolls?**
EJ Rolls is an ATM Electronic-Journal log parser and General-Ledger reconciliation tool. It converts EJ logs (TXT or PDF) and GL statements into a clean Excel reconciliation report.

**What problem does it solve?**
It eliminates manual end-of-day ATM reconciliation — instead of eyeballing thousands of journal lines against a GL extract, the tool matches every transaction automatically and gives you a focused list of items that need investigation.

## File Formats

**What EJ formats are supported?**
- `.txt` from the journal printer (with the `01:` log-id prefix on every line)
- `.pdf` from the EJ viewer (multi-page, clean text)
- `.zip` containing many of the above

**What GL formats are supported?**
- Temenos T24 statement export (`.xlsx`)
- TransactionsDetail (`.xlsx`)

Both formats are auto-detected from the file's structure — you don't have to tell the tool which one you uploaded.

**Can I upload an entire folder of per-ATM data?**
Yes. The web upload accepts a folder via the browser's directory-upload, or you can ZIP everything and drop the ZIP.

## Capabilities

**What does the tool extract from each EJ record?**
STAN, RRN, PAN (masked), transaction date and time, transaction type, amount, status, ATM ID — one row per host transaction.

**How is matching performed?**
EJ records are matched against the GL by STAN (the primary key for a transaction), with amount and date as confirmation signals.

**Are statuses categorised?**
Yes. Each raw status is bucketed into **Approved**, **Unable to Process** (timeouts, faulty dispense, reversals), or **Disapproved** (everything else — low balance, bad PIN, hot card, txn not allowed, etc.).

**What about balance-check records that produce two journal entries per transaction?**
Kept as separate rows, keyed by STAN. The tool preserves the dual record so investigators can see both the balance-check and the actual withdrawal.

## Output

**What downloads are available?**
- **Full reconciliation workbook** — every transaction, matched or not.
- **Unmatched-only workbook** — same layout, filtered to rows that need investigation.
- **EJ-only workbook** — when you only uploaded EJ files (no GL yet).

**What's the output format?**
`.xlsx` with consistent column ordering across all reports.

**Can I preview before downloading?**
Yes. The browser preview shows the first 300 rows plus a matched/unmatched/unable-to-process summary.

## Workflow

**What if I only have EJ files (not GL yet)?**
Upload them. The tool keeps them in your session and prompts you to add the GL when it's ready.

**What if I only have GL files (not EJ yet)?**
Same — upload the GL first, then add EJ when it arrives. Either order works.

**What happens if the web server restarts mid-session?**
Records are persisted to disk per session, so a server restart (including the Flask debug auto-reloader) doesn't lose your upload.

## Access & Licensing

**Is EJ Rolls open source?**
No. This repository is a public showcase containing documentation only. The product is proprietary.

**How do I get a demo or deploy it in my environment?**
See the Contact section in the main [README](../README.md).

**Can I integrate EJ Rolls into our existing reconciliation pipeline?**
Yes — the parser and reconciler are callable programmatically, separate from the web UI. Get in touch for integration details.
