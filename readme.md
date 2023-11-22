# Bigup Web Dashicons

This is a custom dashicons font that allows you to use and insert custom icons the same way you'd do with built-in WP dashicons.


## Icon regeneration

The custom font is generated using [Glyphter](http://www.glyphter.com) and should be regenerated using the same on each change.

There are 3 things to ensure on updates to save breakages:

1.) To save icons getting their indexes mixed up on each generation, check the CSS file to ensure icons are assigned to the same alphabetical 'slot'. In the snippet below, you can see the CSS classes relate to glyph codes e.g. `\0041`. If this changes, the icons will appear in the wrong places after pulling in the update!

The font glyphs are generated sequentially starting at '0041' for 'A', '0042' for 'B' etc.

```
.dashicons-bigup-logo:before{content:'\0041';}
.dashicons-bigup-fist:before{content:'\0042';}
.dashicons-bigup-boot:before{content:'\0043';}
```

Currently, Glyphter has a GUI that allows you to drag and drop the SVG files into the alphabetical slots on a grid, so as long as you reference the CSS class to glyph codes when doing so, you should be good to go.

2.) Name the font the same as in the previous CSS iteration so CSS 'fontFamily' doesn't break.

3.) Once downloaded, edit the CSS file and update the classes to match the WordPress dashicons convention:

```
/* before */
[class*='icon-']:before{...}

/* after */
[class*='dashicons-bigup-']:before{...}


/* before */
.icon-logo:before{content:'\0041';}

/* after */
.dashicons-bigup-logo:before{content:'\0041';}

```


## Usage


Place `/dashicons` in the project root and enqueue the icons as a style. Remember to enqueue the dashicons everywhere you want to use them.

```
/**
 * Register admin scripts and styles.
 */
public function admin_scripts_and_styles() {
    ...

    // Check to see if 'bigup_icons' dashicons have already been registered by another package.
    if ( ! wp_script_is( 'bigup_icons', 'registered' ) ) {
        wp_register_style( 'bigup_icons', BIGUPCF_URL . 'dashicons/css/bigup-icons.css', array(), filemtime( BIGUPCF_PATH . 'dashicons/css/bigup-icons.css' ), 'all' );
    }
    if ( ! wp_script_is( 'bigup_icons', 'enqueued' ) ) {
        wp_enqueue_style( 'bigup_icons' );
    }
}
add_action( 'admin_enqueue_scripts', [ $this, 'admin_scripts_and_styles' ], 10, 0 );

```


Now you can insert icons into markup that same way WP does!
```
<span class="dashicons-bigup-logo"></span>
```


Use them anywhere you'd use WP dashicons!

```
add_menu_page(
    ...
    'dashicons-bigup-fist', // $icon_url
    ...
);
```
