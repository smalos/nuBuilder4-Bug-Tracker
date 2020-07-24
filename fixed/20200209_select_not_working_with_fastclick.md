### Issue: 

In latest version of nuBuilder4 (updated yesterday) on my phone dropdownbuttons doesn't work. I don't see a list. Same issue on my tablet but not on our android-TV (no touch).
Also same issue in a brand new nuBuilder database (empty/no import) on my Windows-PC (Xampp webserver)

I tried in different forms. Also drop-down of language-field on Setup page of nuBuilder4

https://forums.nubuilder.com/viewtopic.php?f=19&t=10241

### Workaround:

Remove these 3 lines from nuform.js:
```
	$(function() {
		FastClick.attach(document.body);
	});
```

This issue has also been reported at Github: select not working on android mobile (Chrome , Firefox)

https://github.com/ftlabs/fastclick/issues/543

