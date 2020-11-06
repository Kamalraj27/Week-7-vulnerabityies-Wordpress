Week-7-vulnerabityies-Wordpress

The code
$file_description = get_file_description( $filename );

if ( $filename !== basename( $absolute_filename ) || $file_description !== $filename ) {$file_description .= '<br /><span class="nonessential">(' . $filename . ')</span>';

}

if ( $absolute_filename === $file ) {
$file_description = '<span class="highlight">' . $file_description . '</span>';

}

$previous_file_type = $file_type;
?>
<li><a href="theme-editor.php?file=<?php echo urlencode( $filename ) ?>&theme=
<?php echo urlencode( $stylesheet ) ?>"><?php echo $file_description; ?></a></li>
<?php
endforeach;
?>
-------------------------------------------------------------------------------------------------------------------------------------
From this code, we can see that $file_description = get_file_description( $filename ); is getting declared and later on under <li><a> tags template name is printed on the page ...<?php echo $file_description; ?></a></li>

$file_description variable should be filtered before displayed to the user. For example, using htmlspecialchars() function.

If the victim clicks on the file that contains XSS payload, XSS will be executed because $description = get_file_description( $relative_file ); is displaying name of the active file the person is editing.

So what if we insert XSS payload after “Template Name, to see what happens watch the gif:
