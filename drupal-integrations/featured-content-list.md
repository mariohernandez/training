# Featured Content



{% tabs %}
{% tab title="featured-content.json" %}
```php
{
  "heading": {
    "heading_level": "2",
    "modifier": "heading--large center section-header",
    "title": "Our Featured Content",
    "url": ""
  },
  "items": [
    {
      "image": "<img src='https://source.unsplash.com/qQGAQMbURhU/640x360' alt='Man doing yoga' />",
      "title": {
        "heading_level": "3",
        "modifier": "",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "Jun 25",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "author": "<div class=\"author__photo\"><img src=\"https://source.unsplash.com/qzDF5PNEWKc/180x180\" alt=\"Author\"s headshot\" /></div><div class=\"author__name\"><span>Valentina Delgado</span><span>Digital Strategist</span></div>",
      "modifier": "card--wide"
    },
    {
      "image": "<img src='https://source.unsplash.com/HONJP8DyiSM/640x360' alt='Tech gadgets' />",
      "title": {
        "heading_level": "3",
        "modifier": "",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "Sep 27",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "author": "<div class=\"author__photo\"><img src=\"https://source.unsplash.com/qzDF5PNEWKc/180x180\" alt=\"Author\"s headshot\" /></div><div class=\"author__name\"><span>Valentina Delgado</span><span>Digital Strategist</span></div>",
      "modifier": "card--wide"
    }
  ]
}
```
{% endtab %}
{% endtabs %}



{% tabs %}
{% tab title="featured-content.twig" %}
```php
{{ attach_library('training_theme/featured-content') }}

<section class="featured-content{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if heading %}
    {%
      include '@training_theme/heading/heading.twig' with {
        "heading": heading
      } only
    %}
  {% endif %}

  <div class="featured-content__items">
    {% block featured_items %}
      {% for item in items %}
        {%
          include '@training_theme/card/card.twig' with {
            "image": item.image,
            "title": item.title,
            "date": item.date,
            "body_text": item.body_text,
            "author": item.author,
            "modifier": item.modifier
          } only
        %}
      {% endfor %}
    {% endblock featured_items %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}



{% tabs %}
{% tab title="featured-content.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.featured-content {
  @include component-spacing;
}

.featured-content__items {
  display: flex;
  justify-content: space-around;
}

.featured-content__card {
  flex: 0 0 22%;
  max-width: 400px;
}
```
{% endtab %}
{% endtabs %}

