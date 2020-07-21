### Issue: 

Sometimes data subform are recorded twice when the user just click on the Save button. How is this possible? 

### Workaround: 

Add the following code in the Header (under Setup) This will prevent a user from double-clicking am Action Button (of any form)

```
// After clicking a nuActionButton (Save, Delete, Print, Clone etc.), disable it for 1.5 secs to prevent a user from double-clicking it.
function preventButtonDblClick() {

   $('.nuActionButton').click(function() {   
      var id = $(this).attr("id");   
      nuDisable(id);
      setTimeout(
         function() {
            nuEnable(id);
         }, 1500);
   });
}

function nuOnLoad() {

   preventButtonDblClick();
   
}
```
