### Issue: 

When using a  shared hosting environment where the user has no control of the web server, set_time_limit() might be disabled (in php.ini)

### Fix:

Suggestion: Replace 
```php
set_time_limit(0);
```

https://github.com/steven-copley/nubuilder4/blob/d569bb0d6a19dcaf4aa291bdcea1352ea183fa10/nucommon.php#L11

with 
```php
nuSetTimeLimit(0);
```

Declaration of nuSetTimeLimit():

```php
function nuSetTimeLimit(){
	if (function_exists('set_time_limit')) {
		set_time_limit(0);
	}
}
```

A similar code is used in \nudb\libraries\classes\Util.php
