# ETL Subsystems and Techniques 

## CDC: Change Data Capture systems 

- isolating the latest source data
- transfer the data that has changed since the last load
- capture all changes (deletions, edits, and insertions) made to the source data
- tag changed data with reason codes to distinguish error corrects from true updates  

Audit Columns:
- e.g. updated_at
- date and time a record was added/modified
- if there are any NULL values, find another way to detect updates
- when fields are populated by the source application and not database triggers, then there can be data quality issues  


Timed Extracts:
- loading records based purely on time is a common mistake
- this loads duplicate rows when it is restarted from mid-process failures
(well what if you have unique constraints on the target table?)

Full Diff Compare:
- keep a full snapshot of yesterday's data, compares it, record by record, against today's data to see what has chanegd.
- this is thorough
- very resource intensive

