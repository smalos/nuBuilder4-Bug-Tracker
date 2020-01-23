### Issue: 

I upgraded nuBuilder Forte to the latest version, downloaded from sourceforge, but, in nuDebug, I see many errors that I didn't see before.

https://forums.nubuilder.com/viewtopic.php?f=19&t=10189&p=20131&hilit=nuBrowseTotals#p20131
https://forums.nubuilder.com/viewtopic.php?f=19&t=10224&p=20270&hilit=nuBrowseTotals#p20270

### Workaround / temporary Fix: 

Looking at the error message, the error is caused by the nuBrowseTotals() function. 
The error occurs with forms that use a temporary table. At the time the SQL is executed in nuRunQuery(), the temporary table no longer exists.

Quick fix: Exclude this line in nuform.php:

```
// $f->browse_totals      = nuBrowseTotals($f);

```


