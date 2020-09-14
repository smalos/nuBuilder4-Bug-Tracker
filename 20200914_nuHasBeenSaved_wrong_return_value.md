### Issue: 

When the form is saved for the first time, nuHasBeenSaved() returns a wrong result. (It returns 0 instead of 1)

### Fix: 

Replace this line

https://github.com/steven-copley/nubuilder4/blob/b027cb8df222f2ed0ac2f2784f8929bade70afbf/nuform.js#L27

```
if(window.nuLastForm != f.form_id || nuLastRecordId != f.record_id){
```

with 

```
if(window.nuLastForm != f.form_id || (nuLastRecordId != f.record_id && nuLastRecordId !== "-1")) {
```




