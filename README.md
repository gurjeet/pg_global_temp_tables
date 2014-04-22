
# Global Temporary Tables in Postgres

This project aims to provide _some_ solution to the problem of migrating Global
Temporary Tables from Oracle.

The solution doesn't have to be transparent, meaning that the migration effort
may require recoding the application, but the end result should be that the
application behaves the same as before migration.

Note that this project specifically should not any of the restrictions on
global temporary tables as implemented in Oracle, because

1. these restrictions vary by Oracle version.
2. these restrictions may not make any sense in Postgres architecture, or
3. they may be impossible to implement in Postgres.

## Requirements

1. Globally visible structure
2. Always available structure
3. Private data
4. Drop/delete private data on session end
5. Drop all data on database restart
6. Ability to specify ON COMMIT {PRESERVER|DELETE} ROWS
7. TRUNCATE deletes only private data
8. Indexes, views and triggers can be created on these tables

## Plan

The initial plan is to provide a function-based infrastructure which the
application can use to create and access the GTTs.

The functions could be:

1. To declare a GTT.
2. To access session-private data stored in GTT.
3. To drop a GTT.
4. To get the actual name of the table, so that indexes, views etc. can be created on it.

