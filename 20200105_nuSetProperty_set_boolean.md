### Issue: 

If a boolean value is set with nuSetProperty, the Hash Cookie is empty when e.g. used in a Browse SQL.

```
nuSetProperty('test', true);
```

https://forums.nubuilder.com/viewtopic.php?f=19&t=10193&p=20136

nuDebug(nuHash());

Result:   
```
[test] => 
```


### Workaround:

Convert the boolean to a string with .toString() to make it work. Or pass "true" instead of true in the 2nd parameter of nuSetProperty()

```
nuSetProperty('test', "true");
```

