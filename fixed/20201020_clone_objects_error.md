**Issue:**

When cloning an object, you might see an error like this:

SQLSTATE[22007]: Invalid datetime format: 1366 Incorrect integer value: '' for column `nubuilder`.`zzzzsys_object`.`sob_input_count` at row 1

The error only occurs when sql_mode=strict

https://dba.stackexchange.com/questions/212358/assigning-empty-string-to-int-null-field-in-mysql

Reported here: https://forums.nubuilder.com/viewtopic.php?f=19&t=10606

**Fix:**

Run these queries on your database:

```
ALTER TABLE `zzzzsys_object` CHANGE `sob_input_count` `sob_input_count` BIGINT(20) NULL DEFAULT '0';
ALTER TABLE `zzzzsys_object` CHANGE `sob_all_order` `sob_all_order` INT(11) NULL DEFAULT '0';
```
