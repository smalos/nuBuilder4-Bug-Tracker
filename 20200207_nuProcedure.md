### Issue: 

The function nuProcedure() was changed with that commit:
https://github.com/steven-copley/nubuilder4/commit/bc0f0f849379c222117468a3c2a2abe22bf3ab83#diff-19250e090060db50129e5bdaaaee6043

and no longer works as described in the wiki.

https://wiki.nubuilder.net/nubuilderforte/index.php/PHP#nuProcedure

Thread in nuBuilder Forum:
https://forums.nubuilder.com/viewtopic.php?f=20&t=10242#p20363

### Fix:

Replace the function nuProcedure in nucommon.php with this one:

```
function nuProcedure($c){

   $s                     = "SELECT * FROM zzzzsys_php WHERE sph_code = ? ";
   $t                     = nuRunQuery($s, [$c]);
   
   if (db_num_rows($t) > 0) {  // procedure exists
   
      $r                     = db_fetch_object($t);
      $php                  = nuReplaceHashVariables($r->sph_php);
      $php                  = "$php \n\n//--Added by nuProcedure()\n\n$"."_POST['nuProcedureEval'] = '';";
      $_POST['nuProcedureEval']   = "Procedure <b>$r->sph_code</b> - run inside ";
      return $php;
   } else
   {
      return '';
   }
   
}
```

