### Issue: 

I just created a test form with 3 Fields on it. 
If I add an entry and don't fill in all 3 fields I get a SQL ERROR. Here I only fill in field 1 and 2:

````
CODE: SELECT ALL
===PDO MESSAGE===

SQLSTATE[HY000]: General error: 1364 Field 'field01' doesn't have a default value

===SQL===========

INSERT INTO test         (test_id, `field00`, `field02`)  VALUES ('5ebbf910018af47', '1', '2.00');
````

https://forums.nubuilder.com/viewtopic.php?f=19&t=10336&p=20934&hilit=fast#p20934

### Fix:

Replace the function nuBuildNewTable() in nubuilders.php with the one below so that DEFAULT NULL is set for each field.

```php
	function nuBuildNewTable($tab, $array, $newT){

	$id			= $tab . '_id';
	$start	= "CREATE TABLE $tab";
	$a			= Array();
	$a[] 		= "$id VARCHAR(25) NOT NULL";

	$ff_type	= nuHash()['fastform_type'];
	$ff_fk		= nuHash()['fastform_fk'];

	if($ff_type == 'subform' && $newT){
		$a[] 	= "$ff_fk VARCHAR(25) DEFAULT NULL";
	}

	for($i = 0 ; $i < count($array) ; $i++){

		$f = $array[$i]['name'];
		$t = $array[$i]['type'];
		
		if($t == 'id'){			$a[] = "$f VARCHAR(25) DEFAULT NULL";}
		if($t == 'varchar'){		$a[] = "$f VARCHAR(1000) DEFAULT NULL";}
		if($t == 'int'){		$a[] = "$f INT DEFAULT NULL";}
		if($t == 'textarea'){		$a[] = "$f TEXT DEFAULT NULL";}
		if($t == 'decimal'){		$a[] = "$f DECIMAL(12,4) DEFAULT NULL";}
		if($t == 'date'){		$a[] = "$f DATE DEFAULT NULL";}
		if($t == 'longtext'){		$a[] = "$f LONGTEXT DEFAULT NULL";}
		
	}
	
	$a[] = "PRIMARY KEY  ($id)";
	$im  = implode(',', $a);

	return "$start ($im)";

}
```



