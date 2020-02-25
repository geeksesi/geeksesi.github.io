---
title: wordpress payment plugin part2
comments: true
categories:
  - - php
    - wordpress
date: 2020-02-26 02:04:11
tags:
  - wordpress
  - php
  - payment
  - woocommerce
  - wordpress_plugin
  - wordpress shortcodes
---


<style>
img { max-width: 350px !important; }
</style>

![wordpress payment plugin](/images/geeksesi-ir_wordpress_payment_plugin_p2.jpg "wordpress payment plugin part 2")

Hello again.
after 2 week i'm here.
my first payment plugin did accept by **Wordpress code review team** and for now i'm a little busy for my new project.
new project is for Tezos network it's a concept, the new one is harder than older and i think my skills did grow on it :D

ok let's talk about how make payment plugin in part 2 :)

in [last part](https://geeksesi.ir/2020/02/11/wordpress-payment-plugin-part1) we did speak about how make a wordpress plugin.
in this part we will talk about shortcode.

first step i will refer you to official wordpress document : [shortcode](https://codex.wordpress.org/Shortcode_API)\
i did this because i don't want to give a fish to you. you must to learn how find you problem answer.
and if you have problem with official document you must to learn to use it.
for now let's to explain shortcodes more.

## What is shordcode in wordpress.
did you ever seen something like this ? 
```
[gallery]
```
[more about gallery in wordpress](https://codex.wordpress.org/Gallery_Shortcode)

in wordpress, developers can do a lot of things with shortcodes.
in this plugin we must to handle a page refer user after any update of payment (success or fail).
we haven't access to make a route (with installed template) in plugin.
i'm using shortcode to make a redirect page for payment. like this picture : 

![Sample-of-my-payment-page](/images/geeksesi-ir_Sample-of-my-payment-page.jpg "Sample-of-my-payment-page")

so i'm bad to explain things without sample. let's talk about how we can made on of them.

## make a wordpress shortcode in our plugin.
it is tooooo much easy.
just we need to call a wordpress function and a function as a callback.
watch this :
```
    add_shortcode('my-awesome-name-for-shortcode', "my_awesome_name_for_callback_funciton");
    function my_awesome_name_for_callback_funciton(){
        // Put some Awesome code here please.
    }
```
it's realy easy.
so now we have a shortcode and we can put in on our post or page like this :
```
[my-awesome-name-for-shortcode]
```
if you want to refer callback to a class (playing with oop in wordpress :sweat_smile: ) just put array to callback place like this : [+](https://github.com/geeksesi/wp-zilon-woocommerce/blob/ea1373a1c3076898978077a0ce40fb61c6728a25/include/class/controller/WP_ZILON_WOOCOMMERCE_Controller.php#L17)

## final speek
it's too much easy. don't afraid to make a plugin and test it on your own local wordpress site :)
in next part we will talk about RestApi. there is to much things to say.

if you like start to make a plugin but u need help, don't afraid to contact with me  :wink: