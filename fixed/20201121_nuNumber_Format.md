### Issue: 

If the nuNumber Format "N|$ 1,000" is used (no decimals), nuBuilder formats it as

*$ 123undefined*

The correct/expected output is $ 123


### Fix: 

Replace this line here : https://github.com/steven-copley/nubuilder4/blob/bb20b8a622b2e027f45541524a7035ad0cc387ca/nuformclass.js#L937

with these 2 lines:

```javascript
var decimals = splitNumber.length == 1 ? '' : splitNumber[1];
return String(CF[0] + ' ' + nuAddThousandSpaces(splitNumber[0], CF[1]) + CF[2] + decimals).trim();
```
