# Global styles

Make the updates below to improve our theming experience.

### Global

* Update `src/patterns/global/global.scss` with the following changes.  Leave all other code in `html` and `body` as is.

{% tabs %}
{% tab title="global.scss" %}
```css
html {
  @include font-stack-primary;
  font-size: 62.5%;
}

body {
  font-size: 1.8rem;
  line-height: 1.5;
}
```
{% endtab %}
{% endtabs %}

### Mixins

* Add the following mixins at the bottom of `src/patterns/global/util/_mixins.scss`.

{% tabs %}
{% tab title="\_mixins.csss" %}
```css
// Crop image in the middle and
// set a fixed height.
@mixin image-crop($height: 100%) {
  height: $height;
  overflow: hidden;
  position: relative;
  width: 100%;

  img {
    height: 100%;
    left: 50%;
    max-width: none;
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
    width: auto;
  }
}

// vertical align mixin
@mixin vertical-align($position: relative) {
  display: block;
  position: $position;
  top: 50%;
  transform: translateY(-50%);
}

// horizontal align mixin
@mixin horizontal-align($position: relative) {
  display: inline-block;
  left: 50%;
  position: $position;
  transform: translateX(-50%);
}

// center align mixin
@mixin center-align($position: relative) {
  display: block;
  left: 50%;
  position: $position;
  top: 50%;
  transform: translate(-50%, -50%);
}

// Mixin for adding consistent spacing on components.
@mixin component-spacing($margin: 100px, $max-width: 1900px) {
	margin: 0 auto $margin;
  max-width: $max-width;
}
```
{% endtab %}
{% endtabs %}

### Color variables

* Replace all existing color variables in `src/patterns/global/colors/_colors.scss` with the code below.

{% tabs %}
{% tab title="\_colors.scss" %}
```css
//Colors

// Standard.
$color-white: #fff;
$color-black: #1b2b34;

// Primary.
$color-navy-blue : #003954;

// Grays.
$color-gray: #808080;
$color-gray-light: #eeeeee;
$color-gray-med: #cccccc;
$color-gray-dark: #444444;
$color-gray-darker: #131313;
$color-gray-lt: #65737e;
$color-gray-xlt: #a7adba;

// Misc
$color-catskill-white : #edf2f7;
$color-error : #f00;
$color-success : #089e00;
$color-warning : #fff664;
$color-info : #000db5;
$color-gray-mid:  #cccccc;
$color-gray-lt: #444444;
$color-gray-xlt: #131313;
$color-tan-hide: #f99157;
```
{% endtab %}
{% endtabs %}

