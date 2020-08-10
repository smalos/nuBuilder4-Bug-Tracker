### Issue: 

If you use MySQL Server 8 then your INFORMATION_SCHEMA database has all tables and fields names written in CAPS, 
including INFORMATION_SCHEMA.TABLES which is used in nuBuildTableSchema function. 

https://forums.nubuilder.com/viewtopic.php?f=19&t=10187&p=20198&hilit=subform+valid#p20116

### Fix: 

Get rid of the errors by replacing these two functions in nucommon.php 

```
function nuBuildTableSchema(){

   $a            = array();
   $t            = nuRunQuery("SELECT table_name as TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE table_schema = DATABASE()");

   while($r = db_fetch_object($t)){
      
      $tn         = $r->TABLE_NAME;
      $a[$tn]    = array('names' => db_field_names($tn), 'types' => db_field_types($tn), 'primary_key' => db_primary_key($tn), 'valid' => 1);
      
   }
   
   return $a;

}



function nuBuildViewSchema(){

   $a            = array();
   $t            = nuRunQuery("SELECT table_name as TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE = 'VIEW' AND table_schema = DATABASE()");

   while($r = db_fetch_object($t)){
      $a[]      = $r->TABLE_NAME;
   }
   
   return $a;

}
```
