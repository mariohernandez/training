# Hero Component

We are now finally at a point where we can integrate the Hero component using the Hero paragraph type in Drupal.

1. Open `/src/templates/paragraphs/paragraph--hero.html.twig` in your text editor
2. Remove all code in the file but leave all comments. It is good to leave the comments untouched as they provide helpful information regarding available variables and other useful Drupal-specific details.
3. Add the following code at the bottom of the template:

```php
{% set rendered_content = content|render %}

{%
  set hero_title = {
    heading_level: '1',
    modifier: ' hero__title',
    title: content.field_title|render|trim is not empty ? content.field_title,
    url: ''
  }
%}

{% set hero_cta = {
    text: content.field_cta|render|trim is not empty? content.field_cta|field_raw('title'),
    url: content.field_cta|render|trim is not empty? content.field_cta|field_raw('url'),
    modifier: 'button'
  }
%}

{%
  include '@theme_name/hero/hero.twig' with {
    attributes: attributes,
    title_prefix: title_prefix,
    title_suffix: title_suffix,
    image: content.field_image|render|trim is not empty ? content.field_image,
    eyebrow: content.field_eyebrow|render|trim is not empty ? content.field_eyebrow,
    heading: hero_title
    body: content.field_body|render|trim is not empty ? content.field_body,
    cta: hero_cta
  } only
%}
```

Let's go over what we are doing here:

* First, as mentioned in [Drupal Best Practices](https://mariohernandez.gitbook.io/training/essentials/drupal-best-practices#passing-fields-values-to-components), we're triggering a full render of the content array variable.
* Notice how with some fields we are making use of the `field_value` filter which is provided by the [Twig Field Value](https://www.drupal.org/project/twig_field_value) module to pass in the raw value of that field. Using this approach for pulling individual field values from the field's array is the recommended approach to ensure data caching is not compromised.
* Next, we are setting variable for the title \(`hero_title`\).  While we could do this in the include statement, doing it outside of the include makes things more readable and cleaner.
* We are also setting a variable for the Call to action button \(`hero_cta`\), but we're doing something slightly different with the values for the `url` and the `title` of the button. We are using Twig Field Value's `|field_raw('url')` & `('title')` as a way to individually extract each of those attributes from button's render array.
* Next we use an `include` twig statement to integrate the Hero component. In the include we are mapping all the Hero component's fields with Drupal's fields. We also pass in Drupal-specific items such as _title\_prefix_, _title\_suffix_, and _attributes_.
* Also notice that we are using `|render|trim is not empty ?` which is a technique for checking that a field is not empty before printing it.  [Read this thread](https://www.drupal.org/project/drupal/issues/2547559) for this and other similar techniques.

### 

#### 

