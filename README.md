sql_diagnostix
==============

Stored Routines for MariaDB, Percona Server and Oracle MySQL.
They allow you to materialize the Diagnostics Area into a temporary table,
or show it.

Syntax:

```
_.materialize_diagnostics_area()
Create and populate a _.DIAGNOSTICS_AREA temporary table.

_.show_diagnostics_area()
SHOW common information about error conditions.

_.show_full_diagnostics_area()
SHOW all information about error conditions,
including the properties which can only be set via SIGNAL or RESIGNAL.
```

Usage example:

```
MariaDB [test]> INSERT INTO `t` VALUES (1/0), (1/0), (1/0), (-1);
Query OK, 4 rows affected, 4 warnings (0.07 sec)
Records: 4  Duplicates: 0  Warnings: 4
 
MariaDB [test]> CALL _.show_diagnostics_area();
+----+----------+-------------+--------------------------------------------+
| ID | SQLSTATE | MYSQL_ERRNO | MESSAGE_TEXT                               |
+----+----------+-------------+--------------------------------------------+
|  1 | 22012    |        1365 | Division by 0                              |
|  2 | 22012    |        1365 | Division by 0                              |
|  3 | 22012    |        1365 | Division by 0                              |
|  4 | 22003    |        1264 | Out of range value for column 'c' at row 4 |
+----+----------+-------------+--------------------------------------------+
4 rows in set (0.09 sec)
```

More info:

http://falseisnotnull.wordpress.com/2013/08/23/mariadbmysql-procedures-to-easily-access-the-diagnostics-area/
