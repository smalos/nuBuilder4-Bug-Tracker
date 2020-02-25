### Issue: 

"When I add a row to the suborm then the Save button on the main form is changing to red but nuIsSaved() function shows "true".
When I modify the main form then nuIsSaved() works OK."

https://forums.nubuilder.com/viewtopic.php?f=20&t=10260

### Workaround:

nuFORM.edited seems to work more reliable:

```
if (nuFORM.edited) {
    alert('button should be red');
} else
    alert('button should be blue');
}
```

### Possible Fix:

Add window.nuSAVED  = false;  in nuHasBeenEdited()

```
function nuHasBeenEdited(){
   
   $('#nuSaveButton').addClass('nuSaveButtonEdited');
   nuFORM.edited   = true;
   window.nuSAVED   = false; 
}
```

