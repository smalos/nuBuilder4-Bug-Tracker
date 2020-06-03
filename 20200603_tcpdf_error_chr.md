### Issue: 

TCPDF shows an error:

```
Warning: chr() expects parameter 1 to be int, string given in /tcpdf/include/tcpdf_fonts.php on line 1671
```

https://forums.nubuilder.com/viewtopic.php?f=21&t=10374


### Fix:

Appply this fix in tcpdf_fonts.php:

https://github.com/tecnickcom/TCPDF/commit/e2deae00e5ac436560667d6afe1fe2bac3ec8859
