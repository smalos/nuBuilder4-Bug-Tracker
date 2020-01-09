### Issue: 

When I use the 'nuSetVerticalTabs()' Javascript procedure in any form with the latest version of NuBuilder, I have a problem with the first tab : an HTML code appears instead of the tab title.
Does anyone else have the same problem ? ([Source:](https://forums.nubuilder.com/viewtopic.php?f=20&t=10200&p=20165#p20165))

### Fix: 

Add this function in the Header (under Setup) and login into nuBuilder.

```
function nuSetVerticalTabs(){
	
	$('#nuTabHolder').css('display', 'inline-block');
	$('.nuTab').css('display', 'block');
	$('#nuRecord').css('display', 'inline-block');
	$('.nuTab').css('padding', '8px 2px 0px 2px');
	$('#nuTabHolder').css('height', window.innerHeight)

	var w   = 0;

	$('.nuTab').each(function( index ) {
		$(this).html('&nbsp;&nbsp;&nbsp;' + $(this).html());
		w   = Math.max(w, nuGetWordWidth($(this).html()));

	});

	$('#nuTabHolder').css('width', w + 30);
	$('.nuTab').css('width', w + 30);

}
```
