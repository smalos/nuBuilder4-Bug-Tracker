### Issue: 

When calling nuMessage() within a Popup/iFrame, the message box is displayed too far to the right, outside the visible area. 
Only if you scroll to the left, you will see the error message.

https://forums.nubuilder.com/viewtopic.php?f=19&t=10345&p=21009&hilit=numessage#p21009

### Fix: 

Center the message over the current window/iFrame/popup. This method takes into account the current horizontal scrolling position.

Replace [this line](https://github.com/steven-copley/nubuilder4/blob/407ccdaaea4d631d5d8a59094ef365beb5df8e05/nuform.js#L3505)

```javascript
var l		= ( $(window.top.document).width() - widest) / 2;
```

With these two lines:

```javascript
var w = $(this).innerWidth();
var l = $(this).scrollLeft() + ( w - widest) / 2;
```
