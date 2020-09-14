### Issue: 

Browse Screen:

There's an issue when using nuSearchAction() and passing an argument while being on page > 1

1. Add an action button: nuAddActionButton('filterDisplay', 'Show Only Display', 'nuSearchAction("display", "")');
2. Go to any page > 1
3. Hit the action button
4. --> No Results!

Reported here: https://forums.nubuilder.com/viewtopic.php?f=19&t=10519&p=21843#p21843

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

