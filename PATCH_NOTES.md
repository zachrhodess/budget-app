# Rhodes Financial v1.3.0

This release keeps the existing persistent database at:

`~/Documents/Rhodes Financial/rhodes_financial.db`

It does **not** replace your database. `update.command` creates a pre-update safety copy before rebuilding the app.

## v1.3.0 changes

- Rebuilt CSV importing around bank-agnostic column detection instead of requiring exact bank headers.
- Recognizes common variations of Date, Posted Date, Description, Merchant, Memo, Amount, Debit, Withdrawal, Credit, Deposit, Balance, Type, and Classification columns.
- Supports comma, semicolon, tab, and pipe-delimited CSV files.
- Supports signed Amount columns and separate Debit/Credit layouts.
- Adds a manual CSV column-mapping screen when automatic detection is uncertain.
- Can remember a CSV layout locally so later statements with the same headers map automatically.
- Import previews now show detected column mappings, mapping confidence, skipped source rows, and clearer diagnostics.
- Expanded searchable-PDF handling with flexible date/description/amount pattern detection as a fallback to known statement layouts.
- Keeps image-only/scanned PDF OCR out of this release; the app explains that limitation instead of silently failing.
- Added a new **Income** page matching the Expenses experience: monthly summary, source filters, source totals, daily trend, and income transaction table.
- Moved **Transactions** into the **More** menu.
- Primary navigation is now Dashboard, Import, Expenses, Income.
- Dashboard monthly Income links now open the Income page.
- Added macOS quarantine troubleshooting to the README.
- Clarified that the `imports/` directory is temporary staging and is not a watched folder.

## Update steps

1. Make sure Docker Desktop is running.
2. Replace the app code with this release (or pull it from GitHub).
3. Run `update.command`.
4. The app backs up the existing database, rebuilds v1.3.0, and opens `http://localhost:8000`.
