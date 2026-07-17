# Payroll Import & Cost Dashboard — Google Apps Script Template

A configurable Google Sheets add-on that imports a monthly payroll/roster export
into a single master sheet, rolls people up into Groups and Group Leads via a
mapping you control, and renders a lightweight cost dashboard. Optional
narrative insights are generated through the Anthropic API.

Everything environment-specific — API key, sheet and tab names, an optional
default source URL — is entered through a **⚙️ Setup** menu and stored in Script
Properties. No secrets, file IDs, or organization-specific data live in the code.

## What it does

- **Import** a month of data from a source spreadsheet into a master sheet.
- **Assign** each row a Group and Group Lead from a configurable mapping, with
  rules for excluding site/field-level roles.
- **Dashboard** reads a summary sheet you maintain (pivot tables or formulas)
  and shows net pay, employer cost, revenue, and a revenue-per-salary ratio.
- **AI insights** (optional) decompose month-over-month changes into components
  before flagging anomalies.

## Setup

1. Open your spreadsheet → **Extensions → Apps Script**.
2. Paste `Code.gs` into the script editor. Add two HTML files
   (**File → New → HTML**): `ImportSidebar` and `Dashboard`.
3. Back in the sheet, run `onOpen` once (or reload) to get the **⚙️ Setup** menu.
4. In **⚙️ Setup**, configure:
   - **Set Anthropic API Key** — stored in Script Properties, never in code.
     *(Skip if you don't want AI insights.)*
   - **Set Model** — the model id you want the insights call to use.
   - **Set Sheet / Tab Names** — the source export tab, your master sheet, your
     summary sheet, and the insights output sheet.
   - **Set Default Source URL** — optional; leave blank to paste a URL each time.
5. Adjust `SCHEMA`, `RULES`, and `SUMMARY_LAYOUT` in `Code.gs` to match your own
   columns and summary-sheet layout (see caveat below).
6. Use **⚙️ Setup → Import Payroll Month** and **Open Dashboard**.

## Caveat: some logic is intentionally simplified

The author works with confidential HR data and cannot publish production
specifics. Two areas are therefore **example-only** and must be replaced before
real use:

- **Import schema** (`SCHEMA`): a minimal synthetic set of columns
  (`Base Pay`, `Allowances`, `Bonus`, `Net Pay`, etc.) with placeholder header
  names. Your real payroll export will have a different, larger schema — map it
  in `IMPORT_FIELD_MAP` and `MASTER_COLUMNS`.
- **Summary layout** (`SUMMARY_LAYOUT`): the row/column offsets and the
  Group/Lead labels are placeholders tied to a specific summary-sheet shape.
  Point them at your own rows.

The one-time-bonus and benchmark figures are likewise placeholders, not real
market or company data.

## Note on Script Properties

Config values live in the Apps Script project's Script Properties, not in this
source file — so nothing sensitive is published to the repository. Anyone you
grant **edit access to the script/spreadsheet** can still read those properties,
so treat edit access as trusted.

## Attribution

100% AI-generated, 100% human-directed.

---

## Suggested repository "About" section

**Description (one line):**
> Configurable Google Apps Script template: import monthly payroll/roster data into a master sheet, roll up costs by group, and view a lightweight dashboard with optional AI insights.

**Topics / tags:**
`google-apps-script` · `google-sheets` · `payroll` · `hr-tools` · `dashboard` ·
`anthropic-api` · `template` · `automation`
