### Issue: 

I upgraded to newest nuBuilder4 from version may 2019. After that all my forms have a big bottom margin. It's not possible to reduce it by editing the form.
Does somebody have an easy way to remove this extra margin?

https://forums.nubuilder.com/viewtopic.php?f=19&t=10240

### Fix:

Replace the function nuFormDimensions() in nuform.php with this one (taken from an older nuBuilder version).

```
function nuFormDimensions($f){

	$d			= array();
	$t			= nuRunQuery("SELECT * FROM zzzzsys_form WHERE zzzzsys_form_id = '$f'");
	$r			= db_fetch_object($t);
	
	$bt			= 57; 	//-- browse title
	$rh			= intval($r->sfo_browse_row_height)    == 0 ? 25 : $r->sfo_browse_row_height;
	$rs			= intval($r->sfo_browse_rows_per_page) == 0 ? 25 : $r->sfo_browse_rows_per_page;
	$bb			= 25;   //-- browse footer
	$t			= nuRunQuery("SELECT * FROM zzzzsys_object WHERE sob_all_zzzzsys_form_id = '$f'");
	$h			= 0;
	$w			= 0;
	$gh			= 0;
	$gw			= 0;
	
	while($r	= db_fetch_object($t)){
		
		if($r->sob_all_type == 'lookup'){
			
			$w 	= max($w, $r->sob_all_left + $r->sob_all_width + $r->sob_lookup_description_width + 40);
			$gw	= $gw + $r->sob_all_width + $r->sob_lookup_description_width + 40;
			
		}else{
			
			$w 	= max($w, $r->sob_all_left + $r->sob_all_width + 40);
			$gw = $gw + $r->sob_all_width + 4;
			
		}

		$h		= max($h, $r->sob_all_top + $r->sob_all_height);
		$gh 	= max($r->sob_all_height, 25, $gh);

	}

	$bh			= $bt + ($rs * $rh) + $bb;
	$bw			= nuGetBrowseWidth($f);	

	$grid		= ['height'=>$gh, 'width'=> $gw];
	$browse		= ['height'=>$bh, 'width'=> $bw];
	$edit		= ['height'=>$h,  'width'=> $w];


	
	$d[]		= $bt + ($rs * $rh) + $bb;    		//-- lookup browse height
	$d[]		= nuGetBrowseWidth($f);	
	$d[]		= $h  + 0;							//-- lookup form height
	$d[]		= $w  + 0;							//-- lookup form width
	$d[]		= $h  + 0;							//-- form height
	$d[]		= $w  + 50;							//-- form width
	$d[]		= $gh + 0;							//-- grid height
	$d[]		= $gw + 55;							//-- grid width
	
	$d[]		= ['browse'=>$browse, 'edit'=>$edit, 'grid'=>$grid];

	return ['browse'=>$browse, 'edit'=>$edit, 'grid'=>$grid];
	
}
```


