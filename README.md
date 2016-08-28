
# Changing sidebar on wc vendor page so that it is different from main shop page#
If you are using WC Vendors Plugin you may notice that vendor pages inherit the shop page sidebar by default when most of the time they are irrelevant for the vendor pages. That is because WC Vendors is using the archive-product.php file which is also used for shop page views. To solve this issue we would have to update our archive-product.php with the conditional.

## Installation ##
1. Just copy the archive-product.php to your current theme folder/woocommerce/
2. Create a separate sidebar for vendor pages under Aappearance->Widgets and then update the name of widget area 'makers' on line 120 of archive-product.php with your newly created widget area name.
3. You have a new widget are that you could use now.

## Manual installation if you have different version of archive-product.php or custom code there ##
Instead of the line 114 that was `<?php do_action( 'woocommerce_sidebar' ); ?>` put :
```php
<?php $vendor_shop = urldecode( get_query_var( 'vendor_shop' ) );
$vendor_id   = WCV_Vendors::get_vendor_id( $vendor_shop );
if ( !$vendor_id ) {
  do_action( 'woocommerce_sidebar' );
} else { ?>
  <div id="sidebar" class="sidebar fusion-widget-area fusion-content-widget-area" style="float: left;">
  <?php   dynamic_sidebar( 'makers' ); ?>
  </div>
<?php } ?>
```
Note: don't forget to replace 'makers' with your widget area name.
