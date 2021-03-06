# Misc PW Modules

## MiscShippingFees

Eg. in *templates/padloper/cart-edit.php*:

```
    <div class='misc-shipping-fees'>
<?php
  $shipping = $this->modules->get('MiscShippingFees');
  $shipping_fees = $shipping->getTotalShippingFees($items);

  echo '<table><th colspan="2">+ ' . __('Shipping') . ' (' . __("incl. VAT") . ')</th>';

  foreach($shipping_fees as $country => $price) {
    if($country == '*') {
      $country = __("Elsewhere in Europe");
    }

    $price = $cart->renderPriceAndCurrency($price);

    echo "<tr><td>{$country}</td><td class='miscshippingfees-price'>{$price}</td></tr>";
  }

  echo '</table>';
?>
    </div>
```

## MiscPricePerKg

Eg. in *site/templates/category.php* or *site/templates/products.php*:

```
<?php
$price_variations= $this->modules->get('MiscVariationsPrices');
$price = $price_variations->getVariationsPricesText($article);
?>

<h1><?php echo $article->title ?></h1>
<h2><strong><?= $price ?></strong></h2>
```

Eg. in *site/templates/product.php*:

```
$cart = $modules->get('PadCart');
$price_variations= $this->modules->get('MiscVariationsPrices');
$price_details = '';

if($price_variations->hasPricePerKg($page)) {
  list($price, $weight, $unit, $unit_price) = $price_variations->getPricePerKg($p);
  $price_details .= " ({$cart->renderPriceAndCurrency($unit_price)}/$unit)";
}

$content .= "<input type='radio' name='product_id' value='{$p->id}' checked><div class='price'>" . $cart->renderPriceAndCurrency($p->product_price) . "</div><div class='size'> " . $p->product_size . " $price_details</div></input>";
```
