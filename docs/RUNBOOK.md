# Runbook (Local)

## Option A — SQL Server in Docker (recommended)

1. Start SQL Server container (example docker-compose in `/docker`).
2. Copy the CSVs into the container path used by `BULK INSERT` (default: `/var/opt/mssql/`).
3. Execute scripts in order:
   - `sql/01_setup_schemas.sql`
   - `sql/02_bronze_load.sql`
   - `sql/03_silver_transform.sql`
   - `sql/04_gold_star_schema_views.sql`

## Option B — Local SQL Server + SSMS

Same sequence as above, but update the `BULK INSERT ... FROM '<path>'` file paths to your local CSV locations.

## Validation

Run quick sanity checks (see `/tests/data_quality_checks.sql`).
