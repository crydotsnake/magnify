# jQuery Magnify

Magnify is a simple, lightweight jQuery plugin that adds a magnifying glass style zoom functionality to images. It is a useful feature to have for product images on ecommerce websites, or if you just want people to be able to zoom into an image without spawning additional overlays or popup windows that may cover your content. Magnify is based on [this tutorial](http://thecodeplayer.com/walkthrough/magnifying-glass-for-images-using-jquery-and-css3).

If you don't use jQuery, then you can use [TrySound's vanilla JS version](https://github.com/TrySound/magnify/tree/fix-vanillajs).

**[See a demo &raquo;](https://thdoan.github.io/magnify/demo.html)**

**[See a demo with mobile plugin &raquo;](https://thdoan.github.io/magnify/demo-mobile.html)**

**[See a demo with an image map &raquo;](https://thdoan.github.io/magnify/demo-map.html)**

**[See a demo inside an accordion &raquo;](https://thdoan.github.io/magnify/demo-accordion.html)**

## Getting Started

### Step 1: Link the required files

```
<link rel="stylesheet" href="/css/magnify.css">
<script src="//code.jquery.com/jquery-2.2.4.min.js"></script>
<script src="/js/jquery.magnify.js"></script>
<!-- Optional mobile plugin (uncomment the line below to enable): -->
<!-- <script src="/js/jquery.magnify-mobile.js"></script> -->
```

You have complete control over the style and size of the lens by modifying `magnify.css`. Magnify has support for touch devices, but for a better zoom experience you can load the optional mobile plugin by uncommenting the last line above. It is recommended to load the JavaScript files at the bottom just before the closing `</body>` tag if possible.

### Step 2: Specify the large image

The URI to the large image can be placed in the `data-magnify-src` attribute as shown below, or passed as the `src` option when calling the `.magnify()` function (see [Options](#options)).

```
<img src="/images/product.jpg" class="zoom" data-magnify-src="/images/product-large.jpg">
```

If the `data-magnify-src` attribute or `src` option is not used, then Magnify will try to grab the large image from the parent `<a>` tag. Example:

```
<a href="/images/product-large.jpg">
  <img src="/images/product.jpg" class="zoom">
</a>
```

NOTE: The large image needs to have the same aspect ratio as the main image.

### Step 3: Call the .magnify() function

Make sure this comes after the two required JavaScript files from Step 1 are loaded.

```
<script>
$(document).ready(function() {
  $('.zoom').magnify();
});
</script>
```

Calling the `.magnify()` function with options:

```
<script>
$(document).ready(function() {
  $('.zoom').magnify({
    speed: 200,
    src: '/images/product-large.jpg'
  });
});
</script>
```

## Options

The options below can be set in a JavaScript object when calling `.magnify()`.

Name              | Type     | Default | Description
-----------       | -------- | ------- | -----------
`speed`           | number   | 100     | The fade-in/out animation speed in ms when the lens moves on/off the image.
`src`             | string   | ''      | The URI of the large image that will be shown in the magnifying lens.
`timeout`         | number   | -1      | The wait period in ms before hiding the magnifying lens on touch devices. Set to `-1` to disable.
`afterLoad`       | function |         | Anonymous callback function to execute after magnification is loaded.
`imageWidth`      | number   |         | Override the image width
`imageHeight`     | number   |         | Override the image height
`magnifiedWidth`  | number   |         | Override the large image width
`magnifiedHeight` | number   |         | Override the large image height

Options can also be set directly in the `<img>` tag by adding the following data attributes, which will take precedence over the corresponding options set inside an object:

- `data-magnify-speed` - equivalent to `speed`
- `data-magnify-src` - equivalent to `src`
- `data-magnify-timeout` - equivalent to `timeout`
- `data-magnify-afterload` - equivalent to `afterLoad`, except the value must be a declared function name
- `data-magnify-imagewidth` - equivalent to `imageWidth`
- `data-magnify-imageheight` - equivalent to `imageHeight`
- `data-magnify-magnifiedwidth` - equivalent to `magnifiedWidth`
- `data-magnify-magnifiedheight` - equivalent to `magnifiedHeight`

## Methods

To use a public method, you need to assign the element that you called `.magnify()` on to a variable. Example:

```
<script>
$(document).ready(function() {
  // Enable zoom
  var $zoom = $('.zoom').magnify();
  // Disable zoom
  $zoom.destroy();
});
</script>
```

Name        | Description
----------- | -----------
`destroy()` | Disable zoom and reset to the original state.

## Events

Magnify triggers two custom events on the `html` element: `magnifystart` when you enter zoom mode and `magnifyend` when you exit zoom mode. Example:

```
$('html').on({
  magnifystart: function() {
    console.log('magnifystart event fired');
  },
  magnifyend: function() {
    console.log('magnifyend event fired');
  }
});
```

When in zoom mode, the `magnifying` class is also added to the `<html>` tag, so you can change the style while zooming.

## Lens Style

The lens style can be altered by overriding `.magnify > .magnify-lens`. Example:

```
/* Shrink the lens to half size */
.magnify > .magnify-lens {
  width: 100px;
  height: 100px;
}
```

## Installation

Choose from one of the following methods:

- `git clone git@github.com:thdoan/magnify.git`
- `git clone https://github.com/thdoan/magnify.git`
- `bower install magnify`
- `npm install magnify`
- [Download ZIP](https://github.com/thdoan/magnify/archive/master.zip)
