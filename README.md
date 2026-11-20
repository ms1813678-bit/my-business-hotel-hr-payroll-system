# M.Y. Business Hotel — HR & Payroll System

A local-first HR and payroll application for M.Y. Business Hotel, Maadi, Cairo. The target is a **Windows 10 or Windows 11** computer running a local FastAPI application and PostgreSQL database. The only application user is the HR Manager / System Administrator.

## Delivery status

**Feature-complete on the final-acceptance track for local testing — not yet production-accepted.**  
Do **not** enter real employee or payroll data until Windows installation, backup/restore, and owner acceptance are completed. `main` remains unchanged until the owner explicitly approves a merge.

### Verified on this acceptance branch

- Single administrator authentication, session security, CSRF protection, and immutable audit history.
- Employee register, department/branch assignment, non-reusable employee codes, archive/rehire history.
- Attendance workbook imports, raw source retention, reconciliation, exception review, daily/monthly approval.
- Security roster import and proposal with approved 12-hour / 8-hour coverage rules (working guards after OFF).
- Leave types, opening balances, confirmation/cancellation, balance transaction history.
- Salary advances (regular 25% cap; installment advances 1–36 periods) with payroll installment ledger.
- Sanctions and rewards with manual amounts and payroll-month assignment.
- Monthly payroll runs, snapshots, overtime approval gate, close/reopen, payment ledger.
- Manual Excel/PDF reports with date range and employee scope; local file save only.
- Optional local AI assistant (available in the UI when enabled). If the local model is temporarily unavailable, core HR/payroll continues. Write actions require explicit administrator approval. Security roster vs fingerprint comparison is available as a read-only review report.
- Arabic / English / Simplified Chinese UI with RTL Arabic and LTR English/Chinese layouts, plus live dashboard metrics.
- Final acceptance CI on the cleaned acceptance branch commit `7bc1ac97e9093363145d5fd23ece901da69550d5` completed successfully: Linux/PostgreSQL test suite 322 passed (16 warnings), Windows runner test suite 315 passed (1 warning), and all three PowerShell scripts passed syntax checks. [View workflow run](https://github.com/ms1813678-bit/my-business-hotel-hr-payroll-system/actions/runs/44735532293).

### Still required before production release

1. Run PostgreSQL migration and concurrency tests against a real local PostgreSQL instance.
2. Full backup and restore verification on the target computer (including external drive if used).
3. Windows 10/11 installation via `docs/WINDOWS_INSTALL.md` and `scripts/windows/setup.ps1` on the hotel PC.
4. Owner end-to-end acceptance: attendance month → variable-size security roster → payroll → report with synthetic data only.
5. Explicit owner approval to merge `feature/bilingual-ui-rtl-ltr` into `main` after all acceptance gates pass.

## Local Windows setup

See docs/WINDOWS_INSTALL.md for the current installation path (Windows 10 and Windows 11), and docs/ACCEPTANCE_CHECKLIST_AR.md for the Arabic step-by-step acceptance record. The application binds to 127.0.0.1 only and must not be exposed to the public internet.

## Business rules and scope

See docs/PROJECT_SPEC.md for the approved product scope and detailed HR rules. Purchasing, inventory, accounting, and other future modules are intentionally separate from this HR system.

## Safety

- Use synthetic test records only until release approval.
- Never commit .env, database passwords, session secrets, or real employee data.
- Payroll must not be approved before the exact month's attendance is reviewed and approved.
- Reports are read-only and generated manually by the administrator for a selected date range and employee scope; files are saved locally and are not emailed or scheduled automatically.
- main remains unchanged until the user explicitly approves integration.
