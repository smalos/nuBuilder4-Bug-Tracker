### Issue: 

German umlauts are not shown in reports.

Reported here: https://forums.nubuilder.com/viewtopic.php?f=19&t=10654

### Fix: 

"Fix unsupported operand types error when codepoints arrays are merged"
https://github.com/tecnickcom/TCPDF/commit/b9b5a0b77f1e660e1ff60d9534f8a43da592e6be

Replace the function UTF8StringToArray() in the file tcpdf_fonts.php with this function:

```javascript
 public static function UTF8StringToArray($str, $isunicode=true, &$currentfont) {
        if ($isunicode) {
            // requires PCRE unicode support turned on
            $chars = TCPDF_STATIC::pregSplit('//','u', $str, -1, PREG_SPLIT_NO_EMPTY);
            $carr = array_map(array('TCPDF_FONTS', 'uniord'), $chars);
        } else {
            $chars = str_split($str);
            $carr = array_map('ord', $chars);
        }
        if (is_array($currentfont['subsetchars']) && is_array($carr)) {
            $currentfont['subsetchars'] += array_fill_keys($carr, true);
        } else {
            $currentfont['subsetchars'] = array_merge($currentfont['subsetchars'], $carr);
        }
        return $carr;
    }
```



