### Issue: 

When using the nuNumber type, nuBuilder's internal function addFormatting() trims off the additional decimal places instead of doing mathematically correct rounding.
E.g. the value 5.29 is in a database field and in the Browse Screen the nuNumber format is set to 1000.0 (show one decimal): 
5.2 is displayed instead of 5.3

Reported in this topic: https://forums.nubuilder.com/viewtopic.php?f=20&t=10320

### Fix:

Replace this line in nuformclass.js 
```javascript
var s		= String(d + String(0).repeat(100)).substr(0, F.places).trim();
```

With this :
```javascript
var s = Number('0.'+ d).toFixed(F.places).slice(2);
```
