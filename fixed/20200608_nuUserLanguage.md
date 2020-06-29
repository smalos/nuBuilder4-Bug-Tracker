### Issue: 

nuTranslate() doesn't work when the globeadmin is logged in.

### Fix:

In nucommon.php, replace the function nuUserLanguage() with this one:

https://github.com/steven-copley/nubuilder4/blob/d569bb0d6a19dcaf4aa291bdcea1352ea183fa10/nucommon.php#L1545

```php
function nuUserLanguage(){

   $user_id   = nuHash()['USER_ID'];
   
   if ($user_id == 'globeadmin') {
      $s = 'SELECT set_language as language FROM zzzzsys_setup WHERE zzzzsys_setup_id = 1';
   } else {
      $s = 'SELECT sus_language as language FROM zzzzsys_user WHERE zzzzsys_user_id = ?';
   }
   
   $t          = nuRunQuery($s, [$user_id]);
   $r          = db_fetch_object($t);
   $l          = $r->language;

   return $l;
   
}
```

