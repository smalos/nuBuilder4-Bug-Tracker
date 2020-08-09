### Issue: 

Events are not fired for Lookup Objects.

E.g. add an Event onblur (or any other event) in the "Custom Code" Tab with the Javascript:

```javascript
alert('you will never see me!');
```

https://forums.nubuilder.com/viewtopic.php?f=19&t=10471

### Fix: 

Not available!

### Workaround: 

Add events with JS or jQuery.

```javascript
$('#your_fieldcode').on('blur',function() {
       alert('You are going to see me!');
});
```
