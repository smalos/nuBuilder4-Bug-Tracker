### Issue: 

Browse Screen:

nuSearchAction() can produce an "Uncaught TypeError: Cannot read property 'name' of null" if it's called from a Procedure or a Custom Code.

Reported here:https://forums.nubuilder.com/viewtopic.php?f=19&t=10555

### Fix: 

```
function nuSearchAction(S, F){

   if(arguments.length > 0){
      $('#nuSearchField').val(S);
   }
   if(arguments.length == 2){
      $('#nuFilter').val(F);
   }

   var s   = String($('#nuSearchField').val()).replaceAll("'","&#39;", true);
   var f   = String($('#nuFilter').val()).replaceAll("'","&#39;", true);
   
   window.nuFORM.setProperty('search', s);
   window.nuFORM.setProperty('filter', f);
   
   var c = arguments.callee.caller === null ? '' :  arguments.callee.caller.name;
   if(arguments.length === 0 && c != 'nuGetPage'){
      window.nuFORM.setProperty('page_number', 0);
   }
   if(arguments.length >= 1){
      window.nuFORM.setProperty('page_number', 0);
   }

   nuGetBreadcrumb();
   
}
```

