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
// Mixins.

// Headings mixins
@mixin heading1 {
  font-size: 3rem;

  @include breakpoint($bp-md) {
    font-size: 3.6rem;
  }
}

@mixin heading2 {
  font-size: 2.4rem;

  @include breakpoint($bp-md) {
    font-size: 3rem;
  }
}

@mixin heading3 {
  font-size: 2.1rem;

  @include breakpoint($bp-md) {
    font-size: 2.4rem;
  }
}

@mixin heading4 {
  font-size: 1.6rem;

  @include breakpoint($bp-md) {
    font-size: 2rem;
  }
}

// Clearfix
@mixin clearfix {
  &::after {
    content: '';
    display: table;
    clear: both;
  }
}

// Makes an element visually hidden, but accessible.
// @see http://snook.ca/archives/html_and_css/hiding-content-for-accessibility
@mixin element-invisible {
  position: absolute !important;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px, 1px, 1px, 1px);
}

// Turns off the element-invisible effect.
@mixin element-invisible-off {
  position: static !important;
  clip: auto;
  height: auto;
  width: auto;
  overflow: auto;
}

// Makes an element visually hidden by default, but visible when focused.
@mixin element-focusable {
  @include element-invisible;

  &:active,
  &:focus {
    @include element-invisible-off;
  }
}

// Helper function for working with Sass maps.
// Example: @include print($configuration);
@mixin print($declarations) {
  @each $property, $value in $declarations {
    #{$property}: $value;
  }
}

// Crop image in the middle and
// set a fixed height.
@mixin image-crop($height: 100%) {
  height: $height;
  overflow: hidden;
  position: relative;

  img {
    height: 100%;
    left: 50%;
    max-width: auto;
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
@mixin component-spacing($margin: 100px) {
	margin: 0 auto $margin;
  max-width: $bp-max;
}
```
{% endtab %}
{% endtabs %}

### Typography

* Replace all existing typography styles in `src/patterns/global/utils/_typography.scss` with the code below.

{% tabs %}
{% tab title="\_pography.scss" %}
```css
// Typography
//
// Typography variables.

$font-sans: 'Open Sans', sans-serif;
$font-serif: 'Georgia', serif;

@mixin font-stack-primary {
  font-family: $font-sans;
}

@mixin font-stack-secondary {
  font-family: $font-serif;
}

// Font-Weights.
$font-weight-light: 200;
$font-weight-normal: 400;
$font-weight-bold: 700;
$font-italic: italic;

// Heading mixins.
@mixin heading-1-style {
  @include font-stack-secondary;
  font-size: 1.5rem;
  // 28px.
  line-height: 1.16;

  @include breakpoint($bp-sm) {
    font-size: 3rem;
    // 56px.
    line-height: 1.16;
  }
}


h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0 0 1rem;
}

h1 {
  @include heading1;
}

h2 {
  @include heading2;
}

h3 {
  @include heading3;
}

h4 {
  @include heading4;
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
$color-navy-blue: #003954;

// Grays.
$color-gray: #808080;
$color-gray-light: #eeeeee;
$color-gray-med: #cccccc;
$color-gray-dark: #444444;
$color-gray-darker: #131313;
$color-gray-lt: #65737e;
$color-gray-xlt: #a7adba;

// Misc
$color-catskill-white: #edf2f7;
$color-error: #f00;
$color-success: #089e00;
$color-warning: #fff664;
$color-info: #000db5;
$color-gray-mid:  #cccccc;
$color-gray-lt: #444444;
$color-gray-xlt: #131313;
$color-tan-hide: #f99157;
$color-gray-dk: #444444;
$color-danube: $color-navy-blue;
```
{% endtab %}
{% endtabs %}

### Breakpoints

Add the following breakpoint to the existing list of breakpoints in `src/global/utils/_breakpoints.scss`

{% tabs %}
{% tab title="\_breakpoints.scss" %}
```css
$bp-max: 1900px;
```
{% endtab %}
{% endtabs %}
