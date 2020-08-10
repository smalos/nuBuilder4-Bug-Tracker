### Issue: 

When I try to save data in a form which contains a subform with this following config, I have this error message that should not happen.The row 5 doesn't exist because of the subform config (--> add : no).

https://forums.nubuilder.com/viewtopic.php?f=19&t=10198&hilit=addable#p20157

### How to fix: 

The function nuValidateSubforms() needs fixing so that the error "cannot be left blank" will not be displayed if addable & deleteable are set to false.

### Fix: not available!
