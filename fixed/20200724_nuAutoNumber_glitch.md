### Issue: 

1. Pick nuAutoNumber from the select.
2. Save the Form
3. Result: The save button is still red (=form appears as not saved)
4. Cause: function nuShowInputJS() calls $('#sob_input_javascript').val('').change(); when the form is loaded which sets the nuEdited class for sob_input_javascript

Reported here: https://forums.nubuilder.com/viewtopic.php?f=19&t=10442

### Fix: not available!
