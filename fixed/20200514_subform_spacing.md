### Issue: 

A few columns are set to Hidden in a subform. But there's a space in between. The hidden objects also have a width of 0, so it should not display a spacing.


Reported in this topic: https://forums.nubuilder.com/viewtopic.php?f=19&t=10309

### Fix:

Replace this line in function nuINPUT(), nuform.js 
```javascript
return Number(prop.objects[i].width) + 4;
```

With this:
```javascript
return Number(prop.objects[i].width) + (prop.objects[i].read == 2 ? -2 : 4);
```

and..

Replace this line in function nuGetSubformRowSize(), nuform.js 
```javascript
l = l + w + 6;
```

With this:
```javascript
l = l + w + (o[i].read == 2 ? 0 : 6);
```
