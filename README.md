# SuperMart Manager — SQLite Edition

A small Flask application for managing multiple independent supermarkets using a local SQLite database.

## Features
- Separate supermarket registration and login; each store’s records are separated by its supermarket ID.
- Product catalogue, opening stock and low-stock warnings.
- Purchase entry that increases stock.
- Multi-item sales, stock checks, discounts, payment methods (Cash, UPI, Card, Bank transfer, Credit) and printable receipts showing amount received and balance due.
- Sales history and date-filtered reports.
- Printable reports and Excel (`.xlsx`) export.
- Other expense entry and a simple estimated profit/loss summary.
- Accounts Receivable report (customer balances), Accounts Payable report (supplier balances), printable reports and separate Excel export.
- Purchase payment type and amount paid, used to calculate supplier balances.

## Run on your computer
Requires Python 3.10 or newer. No separate database installation is needed. SQLite is included with Python.

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000 and choose **Create a store**. Enter the supermarket name, administrator name, email address, and your own password (minimum 8 characters). These become your login credentials; there is no universal default admin username/password. Each supermarket should use a different email address. The database is created automatically at `instance/supermart.db`.

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
- Receivables/payables are calculated from the invoice/purchase total less the amount recorded as paid. This version does not yet support posting later payment collections/settlements against an old invoice.
- Accounting figures are estimates for day-to-day management, not a complete double-entry ledger or statutory tax report. Cost of goods sold is based on the cost price saved on each sale line.
- Before real commercial use, set a strong `SECRET_KEY`, use HTTPS when hosted online, make regular backups, and test all workflows with sample data.
