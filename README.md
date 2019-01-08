# PostgreSQL-Python3-DB-Cursor
A Python 3 PostgreSQL database cursor allowing easy queries from python to a PostgreSQL DB.

# Usage
Add the correct login information to the `config.json` file. Then import the cursor using `import dbCursor as db`. You can then use a with and a try/except block to query the database. An empty file  named `__init__.py` will be needed in the base directory of the python file you are importing the DBCursor into. `%s` can be used to create dynamic queries my inserting that string into the query. Commiting the cursor (`cur.commit()`) is not nessicary in the try/except block for `UPDATE` and `SET` queries. Use `cur.fetchall()` to extract all data that is returned in the query and `cur.fetchone()` to extract the first row returned by a query.

# Example Code
```Python3
import dbCursor as db

class PostgreSQLError(Exception):
     pass

id = 1028473
with db.DatabaseCursor('./config.json') as cur:
  try:
    cur.execute('''SELECT * FROM "table" WHERE "id" = %s''', (id,))
    ret = cur.fetchone()
  except Exception as e:
    print(e)
    raise PostgreSQLError(errStr)

col = 'column'    
with db.DatabaseCursor('./config.json') as cur:
  try:
    cur.execute('''SELECT %s FROM "table" WHERE "id" = %s''', (col, id,))
    ret = cur.fetchall()
  except Exception as e:
    print(e)
    raise PostgreSQLError(errStr)
```
```
