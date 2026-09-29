# Rhodes Financial

Rhodes Financial is a private, local-first household finance app for macOS. It runs in Docker Desktop, binds only to localhost, and stores each user's financial data on that user's Mac rather than in this repository.

## Requirements

- macOS
- Docker Desktop

## First-time setup

1. Install and start Docker Desktop.
2. Download this repository with **Code → Download ZIP**, or clone it with Git.
3. Unzip the download if needed.
4. Right-click `start.command` and choose **Open**. macOS may ask you to approve the script the first time.
5. Rhodes Financial opens at `http://localhost:8000`.

`start.command` automatically creates the local data folders it needs.

## Where your financial data lives

Rhodes Financial stores persistent data in:

`~/Documents/Rhodes Financial/`

That folder contains the local SQLite database, backups, exports, and temporary import staging. It is **not** part of this Git repository.

Typical contents:

```text
~/Documents/Rhodes Financial/
├── rhodes_financial.db
├── backups/
├── exports/
└── imports/
```

## Privacy model

- The web service binds only to `127.0.0.1`.
- No banking credentials are stored.
- No cloud AI or external financial service is required.
- Uploaded CSV/PDF files are deleted after successful import.
- The local database and generated reports are excluded from Git.
- Ollama/local AI remains optional and disabled by default.

## Updating without losing data

If you already use Rhodes Financial:

1. Download or pull the newest code.
2. Make sure Docker Desktop is running.
3. Run `update.command`.

The updater creates a database safety copy, rebuilds the app, and reconnects to the same local data folder. Existing transactions, accounts, balances, category rules, tags, budgets, and settings remain in place.

## Main navigation

- **Dashboard** — household totals and shortcuts
- **Import** — CSV/PDF preview and import
- **Transactions** — editable ledger and filters
- **Expenses** — month-by-month spending with category filters

Additional pages are available under **More**.

## Imports

Rhodes Financial accepts:

- CSV
- Searchable PDF statements

The app previews transactions before importing and asks for the target account if it cannot confidently identify one.

## Excel exports

Reports can export the current month, current year, or all history. Monthly files use names such as:

`september_26.xlsx`

Exports are also saved under:

`~/Documents/Rhodes Financial/exports/`

## Backups

Rhodes Financial can create manual backups and automatically creates backups before major changes. `update.command` also creates a pre-update database safety copy.

## Starting and stopping

Start:

```bash
./start.command
```

Stop:

```bash
./stop.command
```

Or use Docker Compose directly:

```bash
docker compose up -d --build
docker compose down
```

## Time zone

The Docker configuration defaults to `America/Denver`. To use another timezone, set the standard `TZ` environment variable before starting Docker Compose.

Example:

```bash
TZ=America/New_York docker compose up -d --build
```

## Repository safety

The `.gitignore` excludes local databases, imports, exports, backups, `.env` files, Python caches, and common macOS metadata. Financial files should never be committed to this repository.
