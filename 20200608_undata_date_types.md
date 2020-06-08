### Issue: 

Empty date values are stored as 0000-00-00 instead of null in MySQL

https://forums.nubuilder.com/viewtopic.php?f=19&t=10377


### Fix:

In nudata.php, replace this code fragment


```php
						if(in_array($fields[$R], $CTSTN)){								//-- valid field names

							if($isAN){
								$v	= nuAutoNumber($sf->object_id, $fields[$R], $row[$R]);
							}else{
								$v	= $row[$R];
							}
							
							$add	= addslashes($v);
							$fld	= $fields[$R];
							$V[]	= "'$add'";
							$I[]	= "`$fld`";
							$F[]	= "`$fld` = '$add'";
							
						}
```

...with this one:

```php
						$idx = array_search($fields[$R], $CTSTN);
						if($idx != false){								//-- valid field names

							if($isAN){
								$v	= nuAutoNumber($sf->object_id, $fields[$R], $row[$R]);
							}else{
								$v	= $row[$R];
							}
							
							$fld	= $fields[$R];
														
							$type = $cts[$table]['types'][$idx]; 	//-- date types: null if empty
							if (in_array($type, array('date','datetime','timestamp','year')) && $v == '') {
								$V[] 	= "null";
								$F[]	= "`$fld` = null";
							} else
							{
								$add = addslashes($v);	
								$V[]	= "'$add'";
								$F[]	= "`$fld` = '$add'";
							}
									
							$I[]	= "`$fld`";
							
							
						}
```
