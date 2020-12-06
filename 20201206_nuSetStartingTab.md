### Issue: 

nuSetStartingTab() raises an error if there are no objects on the form (which is e.g. the case for nuuserhome after a fresh installation)

```
nuform.js?ts=20201206090157:1812 Uncaught TypeError: Cannot read property 'id' of undefined
    at nuSetStartingTab (nuform.js?ts=20201206090157:1812)
    at nuAddEditTabs (nuform.js?ts=20201206090157:1759)
    at nuBuildForm (nuform.js?ts=20201206090157:107)
    at successCallback (nuajax.js?ts=20201206090157:118)
    at Object.success (nuajax.js?ts=20201206090157:17)
    at c (jquery.js?ts=20201206090157:2)
    at Object.fireWith [as resolveWith] (jquery.js?ts=20201206090157:2)
    at l (jquery.js?ts=20201206090157:2)
    at XMLHttpRequest.<anonymous> (jquery.js?ts=20201206090157:2)
```

<p align="left">
  <img src="screenshots/nuSetStartingTab.png">
</p>


### Fix: 

Add a return statement if w.tabs.length == 0 

```javascript
function nuSetStartingTab(p, w){
	
	var t 				= window.nuFORM.getProperty('tab_start');
	
	if(w.tabs.length == 0){
		nuFORMHELP[p] 	= ''
		return
	}else{
		nuFORMHELP[p] 	= nuTABHELP[w.tabs[0].id]
	}
	
	for(var i = 0 ; i < t.length ; i++){
		
		nuFORMHELP[p] 	= nuTABHELP[w.tabs[0].id];
		
		if(t[i].prefix == p){return;}
		
	}

	t.push(new nuStartingTab(p));
	
}

```



