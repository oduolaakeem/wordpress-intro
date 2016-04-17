# Wordpress Theme Development

## Getting started with WordPress

WordPress is a content management system. You
get a nicely designed admin area for managing all of
your content on the site. WordPress allows for
plugins to extend the built in functionality of
WordPress. About 25% of all sites on the internet
are powered by WordPress. WordPress is an open
source project which means you can download and
use the files for free.

## wordpress.com vs wordpress.org

On wordpress.org you can download and install a software script called
WordPress. To do this you need a web host who meets the minimum
requirements and a little time. WordPress is completely customizable
and can be used for almost anything. There is also a service called
WordPress.com which lets you get started with a new and free
WordPress-based blog in seconds, but varies in several ways and is
less flexible than the WordPress you download and install yourself.

## Local WordPress Development

- Install MAMP (Mac) or XAMPP (Windows)
- Start local server (MAMP or XAMPP)
- Go to wordpress.org and download the most recent version of WordPress
- Go to ‘localhost’ in a web browser while your MAMP or XAMPP server is running to view your newly created ‘wordpress’ and ‘project’ site folder projects
- Click on your newly created project folder and follow the prompt to create your wp-config.php file
- Go to the start page for MAMP or XAMPP and go to the phpMyAdmin portal.
- Click on the database tab and create a new database which you can name the same as your project
- Go back to your web browser to finish setting up WordPress locally and enter in the database name you just created. Since we are working locally you can use ‘root’ for the database username and password.
- Run the install
- Enter a site title, username, and password and uncheck private so search engines do not index your site. This username and password is what you will use to login to localhost/projectname/wp-admin
- Click install WordPress and login to your newly created, locally hosted WordPress site!

### You do: Wordpress Admin

- Create at least two posts and two new pages.
- Change the site’s theme.

## WordPress Themes

- We can search for other themes and we are searching the WordPress.org theme repository
- Themeforest.net we can purchase themes and upload them
- Themes live in wp-content/themes in our wordpress folder

### We do:

    $ mkdir wp-content/themes/milky-way
    $ cd wp-contents/themes/milky-way
    $ touch index.php style.css functions.php

Add a `screenshot.jpg` file with the image of your choosing.

### Header and Footer

```html
<!-- header.php -->
<!doctype html>
<html>
  <head>
    <?php wp_head(); ?>
  </head>
  <body>
```

```html
<!-- index.php -->
<?php get_header(); ?>
<h1>Milky Way</h1>
<?php wp_nav_menu(); ?>
<?php get_footer(); ?>
```

```html
<!-- footer.php -->
  <?php wp_footer(); ?>
  </body>
</html>
```

### CSS & JS

- style.css under the meta data for the theme is where you can add your css

```css
/*
  Theme Name: Milky Way
  Theme URI: http://localhost:8888/
  Description: An out-of-this-world Wordpress theme.
  Author: Jesse Shawl
*/
```

- If you have additional css files, enqueue in the functions.php
- You can create a css and js folder in the root of your theme
- Function: wp_enqueue_style
  - https://codex.wordpress.org/Function_Reference/wp_enqueue_style
- Function: wp_enqueue_script
  - https://codex.wordpress.org/Function_Reference/wp_enqueue_script

```php
// functions.php
<?php
function milky_way_scripts(){
  wp_enqueue_style("styles", get_stylesheet_uri());
  wp_enqueue_script(
    "scripts",
    get_template_directory_uri() ."/js/app.js",
    array("jquery")
  );
}
add_action('wp_enqueue_scripts', 'milky_way_scripts');
?>
```

## What is the WordPress Codex?

- https://codex.wordpress.org/Theme_Development

## The Loop

It checks what is available for that particular page and then displays it.
The loop starts with an if statement, them moves into a while statement
as long as there is content to be displayed. Inside the loop is the HTML
and PHP markup to display what is in the loop.

https://codex.wordpress.org/The_Loop

```html
<!-- index.php -->
<?php if(have_posts()): while(have_posts()): the_post(); ?>
  <article>
    <h2><a href='<?php the_permalink(); ?>'><?php the_title(); ?></a></h2>
    <?php the_content(); ?>
  </article>
<?php endwhile; endif; ?>
```

### Changing Permalinks

Settings > Permalinks

## Custom Posts and Pages

https://developer.wordpress.org/themes/template-files-section/page-template-files/page-templates/

### Custom Page Templates

#### `page.php`

If a specialized template that includes the page’s ID is not found, WordPress looks for and uses the theme’s default page template.

#### `page-{slug}.php`

If no custom template has been assigned, WordPress looks for and uses a specialized template that contains the page’s slug.

### Global Page Templates

Sometimes you’ll want a template that can be used globally by any page, or by multiple pages.  Some developers will group their templates with a filename prefix, such as page_two-columns.php

To create a global template, write an opening PHP comment at the top of the file that states the template’s name.

```php
// page_two-column.php
<?php /* Template Name: Two Column */ ?>
```

## Reusing the Loop

```
<?php get_template_part('loop'); ?>
```

## Searching, Sorting, and Filtering

### Searching

```html
<!-- index.php -->
<?php get_search_form(); ?>
```

### Sorting

```html
<?php $posts = query_posts( $query_string . "orderby=title&order=ASC"); ?>
// the loop...
```

### Filtering

```html
<?php
  $current_year = date('Y');
  $current_month = date('m');
  query_posts("year=$current_year&monthnum=$current_month&order=ASC" );
?>
// the loop...
```

## Plugins

>Plugins are ways to extend and add to the functionality that already exists in WordPress.

https://codex.wordpress.org/Plugins

Plugins are installed in `wp-content/plugins/`

### [Advanced Custom Fields](http://www.advancedcustomfields.com/)

You do: Create a custom field.

### [Custom Post Type UI](https://wordpress.org/plugins/custom-post-type-ui/)

Custom Post Type UI is often used in conjunction with Advanced Custom Fields.

This is an example of a custom post type: http://www.eachpeachmarket.com/recipes/

## More Plugins

1. https://wordpress.org/plugins/shortcodes-ultimate/
2. https://wordpress.org/plugins/w3-total-cache/
3. https://wordpress.org/plugins/contact-form-7/
4. https://wordpress.org/plugins/wordpress-seo/
5. https://wordpress.org/plugins/portfolio-slideshow/
6. https://wordpress.org/plugins/nextgen-gallery/
7. https://wordpress.org/plugins/buddypress/

## Deployment


## References

- Screencasts
  - WDI7
    - https://vimeo.com/151079652
    - https://vimeo.com/151079655
    - https://vimeo.com/151079654
