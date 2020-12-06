### Issue: 

When pressing Ctrl + f to search for something in a form and then clicking e.g. the "search" button, a *new* tab is opened.

Normally nuCtrlKeyupListener() is  called when the Ctrl key is released. This is the case when e.g. Ctrl + c is pressed.
But when invoking Ctrl + f a search window is opened (at least in Chrome) and then nuCtrlKeyupListener() is not triggered - probably because the focus is not on the html document anymore.

<p align="left">
  <img src="screenshots/nuCtrlKeyupListener.gif">
</p>


### Fix: 

Do not set window.nuNEW = 1 when Ctrl + f is pressed

https://github.com/steven-copley/nubuilder4/blob/a9d07a962f6bee0618c40a13d82c3a865c3945d4/nucommon.js#L532


```javascript
   var nuCtrlKeydownListener = function(e) {

        if (e.keyCode === 114 || (e.ctrlKey && e.keyCode === 70)) { // exclude Ctrl + f
            window.nuNEW = 0;
        } else {
            if (e.keyCode == 17) { //Ctrl                            
                window.nuNEW = 1;
            }

        }
      
    }

```



