#### The || Operator
||in SQLite is used to concatenate two or more strings together. Example: 
```sql
INSERT INTO users (username, email) VALUES ( 'george' || ' ' || 'ben', 'test@email.com' )
```
translates to 
```sql
INSERT INTO users (username, email) VALUES ( 'george ben', 'test@email.com' )
```
