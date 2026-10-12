# SuperMart Manager — SQLite Edition

A small Flask application for managing multiple independent supermarkets using a local SQLite database.

## Features
- Separate supermarket registration and login; each store’s records are separated by its supermarket ID.
- Product catalogue, opening stock and low-stock warnings.
- Purchase entry that increases stock.
- Multi-item sales, stock checks, discounts, payment methods and printable receipts.
- Sales history and date-filtered reports.
- Printable reports and Excel (`.xlsx`) export.
- Other expense entry and a simple estimated profit/loss summary.

## Run on your computer
Requires Python 3.10 or newer. No separate database installation is needed. SQLite is included with Python.

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000 and choose **Create a store**. Each supermarket should use a different email address. The database is created automatically at `instance/supermart.db`.

## Database location and backup
- Default database file: `instance/supermart.db`
- To use another location, set the `DB_PATH` environment variable to a full file path before starting the app.
- Stop the app before copying the database file for a simple backup. Keep backups secure because the database contains business records.
- Do not delete `instance/supermart.db` unless you intend to start with an empty database.

## Hosting online
SQLite is best suited to a single server or a small local installation. If you deploy to Render or another host, its normal filesystem may be temporary, so data can disappear during redeploys/restarts. Use a host with a persistent disk and set `DB_PATH` to a file on that disk (for example `/var/data/supermart.db`). Confirm persistent-disk support and pricing with the host before deploying. Do not run multiple app instances against the same SQLite file.

## Important notes
- The current version provides one administrator login per supermarket; staff roles are not included.
- Each store’s data is separated by `supermarket_id`, but test account isolation before real use.
- Accounting figures are estimates for day-to-day management, not a complete double-entry ledger or statutory tax report. Cost of goods sold is based on the cost price saved on each sale line.
- Before real commercial use, set a strong `SECRET_KEY`, use HTTPS when hosted online, make regular backups, and test all workflows with sample data.
