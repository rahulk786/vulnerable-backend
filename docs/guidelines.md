# Developer Documentation 

## Table Of Contents

* [SQL Injection](#sqli)
    * [Input Validation](#inputval)
    * [Escaping](#escape)
    * [Parameterized Statements](#parameterize)
    * [Object Relation Mapping Frameworks](#orm)
    * [Avoid admininstrative priviliges](#admin)
* [References](#references)


<a name="sqli" />

## SQL Injection

<a name="inputval" />

### Input Validation

Regular expressions can be used to whitelist structured data
In case of fixed values, determine if user input matches one of the fixed value

```python
match = re.search(r"^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$", user_email_input)
db_input = match.span()
```
<a name="escape" />

### Escaping 

Use character escaping functions for user input. 

```python
_mysql.escape_string(query)
```

<a name="parameterize" />
### Parameterized Statements

Parameterized statements make sure that the parameters (i.e. inputs) passed into SQL statements are treated in a safe manner.

Avoid doing 

```python
sql = "INSERT INTO TABLE_A (COL_A,COL_B) VALUES (%s, %s)" % (val1, val2)
cursor.execute(sql)
```

Instead use

```python
sql = "INSERT INTO TABLE_A (COL_A,COL_B) VALUES (%s, %s)"
cursor.execute(sql, (val1, val2))
```
<a name="orm" />

### Use Object Relation Mapping Frameworks

Many development teams prefer to use Object Relational Mapping (ORM) frameworks to make the translation of SQL result sets into code objects more seamless. ORM tools often mean developers will rarely have to write SQL statements in their code – and these tools thankfully use parameterized statements under the hood.  

<a name="admin" />

### Avoid admininstrative priviliges

Dont connect application to the database using an account with root access

<a name="references" />

## References

[1] https://www.ptsecurity.com/ww-en/analytics/knowledge-base/how-to-prevent-sql-injection-attacks/
[2] https://www.hacksplaining.com/prevention/sql-injection