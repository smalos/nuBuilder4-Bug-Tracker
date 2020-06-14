### Issue: 

Call nuSetVerticalTabs() (to sets the Tabs of an Edit Form Vertically to the Left).

Then resize the browser window (e.g. full screen / F11).

What happens? All objects are shifted downwards.



<p align="left">
  <img src="screenshots/nuSetVerticalTabs_bug.gif">
</p>


### Fix

In nuforms.js, add this line (e.g. after line 51):

```javascript
window.nuVerticalTabs = false;
```

In nuforms.js, replace nuSetVerticalTabs() with this one:

```javascript
function nuSetVerticalTabs(){
   
   $('#nuTabHolder').css('display', 'inline-block');
   $('.nuTab').css('display', 'block');
   $('#nuRecord').css('display', 'inline-block');
   $('.nuTab').css('padding', '8px 2px 0px 2px');
   $('#nuTabHolder').css('height', window.innerHeight)

   var w   = 0;

   var s = '&nbsp;&nbsp;&nbsp;';   
   $('.nuTab').each(function( index ) {
      $(this).html($(this).html().includes(s) ? $(this).html() : s + $(this).html());
      w   = Math.max(w, nuGetWordWidth($(this).html()));

   });

   $('#nuTabHolder').css('width', w);
   $('.nuTab').css('width', w);
   
   window.nuVerticalTabs = true;
}

```


Replace nuResize() in index.php with this function:

```javascript
function nuResize() {

    var w = window.innerWidth;
    $('#nuActionHolder').css('width', w);
    $('#nuBreadcrumbHolder').css('width', w);
    $('#nuTabHolder').css('width', w);
    $('.nuTabTitleColumn').css('width', w);
    $('body').css('width', w);

    if (window.nuVerticalTabs) {
        nuSetVerticalTabs();
    }
}
```  
