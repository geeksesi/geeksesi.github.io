---
title: wrodpress payment plugin Part1
comments: true
tags:
- wordpress
- php
- payment
- woocommerce
- wordpress_plugin
categories: 
- [php, wordpress]
---

<style>
img { width: 200px; }
</style>

![Mohammad Javad Ghasemy](/images/geeksesi-ir_wordpress_payment_plugin_p1.jpg)

## The Story
Hey there, how are you ?
i want to write a little about my experince as a wordpress plugin developer.

you can find some of my plugin in [github](https://github.com/geeksesi).

so let's start to know what we need. and make a payment plugin like this : [wp-zilon-woocommerce](https://github.com/geeksesi/wp-zilon-woocommerce)

## Wordpress
i don't want to explain what is the wordpress but you know wordpress is one of the popular CMS for make website and because Woocommerce, wordpress now is a good choice to make a shop Website.

we want to make a simple plugin here. so you need some basics tools like :
- Wordpress installed on a webservice (you can use remote host or install and configure Apache || if you are in windows use [Xampp](https://www.apachefriends.org/index.html))
- not bad knowledge of PHP (you can grow in project so if you are not good in php also you can make it)
- a little funny code editor (i use both Vscode and Vim)

if you have a problem to make your enviroment tell me and i will help you as far as I can.

### wordpress structure
when you install wordpress you have something like this :
```
- wp-admin/
- wp-include/
- wp-content/
    - plugins/
    - themes/
    - uploads/
    - upgrade/
    - and some other things...
- other files here...
```
we must to put our plugin in `wp-content/plugins/`.
just choice a name for your plugin ( if you want to publish plugin in wordpress repo start name of your plugin must be include `wp-` character ) and make a folder in above directory.
we must to make something like this :
```
- wp-content
    - plugins
        - PLUGIN_NAME
            - PLUGIN_NAME.php
```
* care about name choicing because duplicate name and functions will make confilict in wordpress.

### plugin explain
we are in peace here :D and we need some comments in our plugin. something like this :

```
/*
Plugin name: NAME_OF_PLUGIN
Plugin URI: URL_OF_PLUGIN_HOME_PAGE
Description: EXPLAIN What is this :) 
Version: 1.0.0
Author: what is your name ? 
Author URI: have you a website ? if not put your github url :D
Text Domain: -e('NAME OF PLUGIN','NAME_OF_PLUGIN')
 */
```
* i will explain more about text domain in future.

* you must to put this comment on first of your plugin file.

### detect a problem
in php user can access to you plugin directly. (it's a problem for our wordpress security) worpdress has a easy way to fix this issue.
you must to put `defined('ABSPATH') || exit('No Direct Access.');` after `<?php` in your each file.
this code will check if a ABSPATH (it's a wordpress local variable) isset means user running this plugin how we want.
but if not set means user want to make a not valid request to our serve and we must to kill this connection.


### some usefull defines 
it's good to make some routes define in our plugin. always i will make this :
```
define('WP_ZILON_WOOCOMMERCE_DIR', plugin_dir_path(__FILE__));
define('WP_ZILON_WOOCOMMERCE_URL', plugin_dir_url(__FILE__));
define('WP_ZILON_WOOCOMMERCE_ASSETS_URL', trailingslashit(WP_ZILON_WOOCOMMERCE_URL.'assets/'));
define('WP_ZILON_WOOCOMMERCE_INC_DIR', trailingslashit(WP_ZILON_WOOCOMMERCE_DIR.'app/'));
```
this const variables will help us in future :)

### start coding.
now your plugin is ready.
i will show how to make shortcode in next part of this post.

be happy untile the next post :) good luck.