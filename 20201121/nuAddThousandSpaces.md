### Issue: 

Formatting / grouping of thousands is incorrect for negative values.

E.g. -123 is formatted as $ -,123.00

The expected output is $ -123.00

(Tested with format N|$ 1,000.00 )

### Fix: 

Replace nuAddThousandSpaces() in nucommon.js 
https://github.com/steven-copley/nubuilder4/blob/45129e344acf92fddfd822cffa2d89cb9ead6c23/nucommon.js#L884

```javascript
function nuAddThousandSpaces(s, c){

	var a	= String(s).split('');
	var r	= [];
	debugger;
	r		= a.reverse();
		
	if(r.length > 3){r.splice(3, 0, c);}
	if(r.length > 7){r.splice(7, 0, c);}
	if(r.length > 11){r.splice(11, 0, c);}
	if(r.length > 15){r.splice(15, 0, c);}
	if(r.length > 19){r.splice(19, 0, c);}
	if(r.length > 23){return 'toobig';}

	r		= r.reverse();
	
	return r.join('');
	
}

```

with this (shorter) function:

```javascript
function nuAddThousandSpaces(s, c){
    return s.replace(/\B(?=(\d{3})+(?!\d))/g, c)
}
```
