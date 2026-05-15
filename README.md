# EJ Rolls — ATM Electronic Journal & GL Reconciliation

> **Turn ATM Electronic-Journal rolls and core-banking GL statements into a clean, matched Excel reconciliation — in seconds, not days.**

EJ Rolls is an ATM reconciliation tool for banking operations teams. It parses Electronic Journal (EJ) logs from ATMs — straight from the journal printer (.txt) or the EJ viewer (.pdf) — and reconciles every transaction against the core-banking General Ledger (T24 Temenos and TransactionsDetail formats), producing a complete Excel report of matched and unmatched activity.

[![Status](https://img.shields.io/badge/status-active-success)]()
[![Type](https://img.shields.io/badge/type-banking%20ops%20tool-blue)]()
[![Use case](https://img.shields.io/badge/use%20case-ATM%20reconciliation-orange)]()
[![Stack](https://img.shields.io/badge/stack-Python%20%7C%20Flask-yellow)]()

---

## Screenshots

A look at the EJ Rolls reconciliation workflow.

> Screenshots coming soon — the tool exposes three primary screens: **Upload**, **Reconciliation Preview**, and **Status / Download**.

---

## What is EJ Rolls?

**EJ Rolls is an ATM Electronic-Journal log parser and General-Ledger reconciliation web app.** You drop in your EJ files (TXT from the journal printer, PDF from the EJ viewer, or a ZIP of many ATMs) plus your T24/GL statement, and EJ Rolls returns a reconciliation spreadsheet — one row per transaction — showing which EJ records matched the GL and which need investigation.

It is designed for **end-of-day balancing, ATM exception management, and dispute investigation** — anywhere a banking operations team would otherwise eyeball thousands of journal lines against a GL extract.

---

## Key Features

- **EJ parser** — reads ATM Electronic-Journal logs in both `.txt` (printer dump with line prefixes) and `.pdf` (EJ viewer export) formats; same parser, same output.
- **GL reconciliation** — matches EJ transactions against core-banking GL statements (T24 Temenos format and TransactionsDetail format).
- **Status categorisation** — every transaction is bucketed into Approved, Disapproved, or Unable-to-Process for fast triage.
- **Multi-ATM batch processing** — upload a ZIP or a whole folder of per-ATM directories at once.
- **Bulk Excel export** — full reconciliation workbook plus an "Unmatched-only" workbook for investigation teams.
- **Live preview** — see the first 300 rows and the matched/unmatched summary in the browser before downloading.
- **Resilient sessions** — uploaded records survive web-server restarts via on-disk session caching, so a long reconciliation isn't lost.
- **Two-stage upload** — drop EJ files first or GL files first; the app waits and prompts for the missing side.
- **Clean web interface** — drag-and-drop, folder upload, ZIP support, no command line required.

---

## Who It's For

| Audience | Why EJ Rolls helps |
|----------|--------------------|
| **Bank operations / ATM teams** | End-of-day balancing across the ATM estate without manual line-by-line review. |
| **Reconciliation analysts** | Get a clean Excel of every matched and unmatched transaction, ready for investigation. |
| **Internal audit & compliance** | Verify ATM cash activity against the GL with full traceability. |
| **Dispute & exception managers** | Pull the unmatched-only report to focus on what actually needs work. |
| **Core-banking & Temenos T24 implementers** | A reconciliation layer that speaks T24 statement formats out of the box. |
| **Financial-systems consultants** | Drop-in tool for UAT and production reconciliation engagements. |

---

## How It Works

1. **Upload** your EJ files (`.txt`, `.pdf`, or ZIP) and your GL statement (`.xlsx` — T24 or TransactionsDetail format).
2. **EJ Rolls parses** every transaction block — date, time, STAN, RRN, PAN, transaction type, amount, status, ATM ID.
3. **Reconciliation runs automatically** — EJ records are matched against the GL by STAN, amount, and date.
4. **Preview** the matched / unmatched / unable-to-process summary and the first 300 rows in the browser.
5. **Download** the full reconciliation workbook, or the unmatched-only workbook for the exception team.

*No spreadsheets opened by hand. No copy-pasting STANs across files.*

---

## Technology

EJ Rolls is built on a focused, production-grade stack:

- **Backend:** Python 3.12, Flask
- **PDF parsing:** pdfplumber for EJ viewer exports
- **Text parsing:** regex-based journal-record extractor (handles both printer-prefixed and viewer-clean shapes)
- **Excel:** openpyxl for both reconciliation workbooks and EJ-only exports
- **GL formats supported:** T24 Temenos statement, TransactionsDetail
- **UI:** server-rendered HTML + minimal JavaScript (folder upload via `webkitdirectory`, ZIP support)
- **Session resilience:** in-memory + tempfile-backed session cache

> This repository is a **public showcase**. It documents the product — it does not contain the proprietary parsing, matching, or reconciliation logic.

---

## Frequently Asked Questions

**What ATM journal formats does EJ Rolls support?**
Both `.txt` files straight from the journal printer (with the `01:` line-id prefix) and `.pdf` files exported from the EJ viewer. The same parser handles both shapes once the printer prefix is stripped.

**Which core-banking GL formats are supported?**
Temenos T24 statement exports and the TransactionsDetail format. Both are auto-detected from the file contents.

**Can it handle multiple ATMs at once?**
Yes. Upload a ZIP, a folder of per-ATM subfolders (e.g. `0074/`, `0075/`), or a mixed set of files — EJ Rolls processes them all in one pass.

**What does the output look like?**
Two Excel workbooks: a full reconciliation (every transaction, matched or not) and an unmatched-only workbook for the investigations team. Both have a consistent column layout — STAN, RRN, PAN, transaction date/time, amount, type, EJ status, GL match status, ATM ID.

**Does it categorise transaction outcomes?**
Yes. Every EJ status is bucketed into **Approved**, **Unable to Process** (timeouts, faulty dispenses, reversals), or **Disapproved** (low balance, bad PIN, hot card, etc.) so triage is fast.

**Is EJ Rolls open source?**
No. This repository is a marketing showcase. The product is proprietary — see the license below.

**How do I get access or a demo?**
See the **Contact & Demo** section below.

---

## Why EJ Rolls

- ⚡ **Speed** — minutes instead of days for full-day estate-wide reconciliation.
- 🎯 **Accuracy** — every record matched on STAN with amount/date confirmation.
- 🧩 **Format-flexible** — TXT, PDF, ZIP, folder uploads; T24 and TransactionsDetail GL formats.
- 🏦 **Banking-aware** — speaks the language of core banking and ATM operations.
- 🔒 **Private** — runs in your environment; transaction data never leaves your network.

---

## Contact & Demo

Interested in deploying EJ Rolls inside your bank, integrating it with your core-banking pipeline, or seeing a live demo? Get in touch with the development team.

| Developer | Email | WhatsApp |
|-----------|-------|----------|
| **Muhammad Maaz** | [mazwaseem098@gmail.com](mailto:mazwaseem098@gmail.com) | [+92 323 7609712](https://wa.me/923237609712) |
| **Muhammad Tanveer** | [mtanveertahir66@gmail.com](mailto:mtanveertahir66@gmail.com) | [+92 320 6688665](https://wa.me/923206688665) |

- **Company:** [Advenno](https://advenno.com)
- **GitHub:** [@maaz-gobi](https://github.com/maaz-gobi)

We work with banks and financial-systems consultancies to automate reconciliation and exception management — get in touch to discuss your environment.

---

## License

This is a proprietary product. This repository contains documentation and marketing materials only. See [LICENSE](LICENSE) for terms.

---

<sub>**Keywords:** ATM reconciliation, ATM Electronic Journal, EJ log parser, EJ to Excel, GL reconciliation, T24 Temenos reconciliation, core banking reconciliation, ATM operations software, ATM end of day balancing, ATM journal extractor, EJ viewer PDF parser, ATM exception management, banking reconciliation tool, STAN matching, ATM dispute investigation, Python Flask banking app.</sub>
