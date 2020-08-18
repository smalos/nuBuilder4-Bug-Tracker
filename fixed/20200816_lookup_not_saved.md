### Issue: 

#### Scenario 1:

If a value is entered manually in a Lookup Object (without pressing tabulator), It is not stored in the database.
(Because the Lookup's AJAX request is not finished by the time the form is saved.)

#### Scenario 2:

1. A value has been picked in a lookup field (e.g. FF1).
2. Clear the field
3. Hit Save

Result: FF1 is still stored to the DB.


### Reference: 

https://forums.nubuilder.com/viewtopic.php?f=19&t=10498

### Fix/Workaround:

Replace nuSaveAction() in nuform.js and add nuLookupPending() there.

```javascript
function nuLookupPending() {

   var p = false;
   
   $('[data-nu-type="lookup"][id$="code"]').each(function(){   
      var d = $('#' + this.id.slice(0, -4) + 'description');            
      p = (d.val() == '' && $(this).val() !== '') || (d.val() !== '' && $(this).val() == '')
      return false;
   });
   
   return p;
   
}

function nuSaveAction(){
      
   if (nuLookupPending()) {
      nuMessage([nuTranslate('A lookup operation is still in progress. Please save again when complete.')]);
      return;
   }
      
   if(nuNoDuplicates()){
      nuUpdateData('save');
   }

}
```
