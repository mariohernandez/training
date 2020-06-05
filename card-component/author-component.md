# Author component

As we just saw, the Card wide variant uses some information from the article author.  We don't have a component for users or authors so we need to quickly build one.

1. Inside `src/patterns/components` create a new folder called **author**
2. Inside the _author_ folder create **author.json**, **author.twig**, **author.scss**
3. Add the code below to each of the respective files

{% tabs %}
{% tab title="author.json" %}
```php
{
  "author": {
    "photo": "<img src='https://source.unsplash.com/_cvwXhGqG-o/100x100' alt='Author's headshot' />",
    "name": "Valentina De Leon",
    "title": "Digital Strategist"
  }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="author.twig" %}
```php
{{ attach_library('training_theme/author') }}

<div class="author{{ modifier ? ' ' ~ modifier }}
  {{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  <div class="author__meta">
    <div class="author__name">{{ author.name }}</div>
    <div class="author__title">{{ author.title }}</div>
  </div>
  <div class="author__photo">{{ author.photo }}</div>
</div>
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="author.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.author {
  align-items: center;
  color: $color-gray-dark;
  display: flex;
  flex-direction: row;
  font-size: 1.3rem;
  height: 70px;
}

.author__photo {
  height: 70px;
  width: 70px;

  img {
    border-radius: 50%;
  }
}

.author__meta {
  text-align: right;
  padding-right: 10px;
}

.author__name {
  text-align: right;
  text-transform: uppercase;
}

.author__title {
  font-style: italic;
}

```
{% endtab %}
{% endtabs %}

* Create the **author** library in `training_theme.libraries.yml`.

### Update the Card component with new Author component

Let's update the card component so we make use of the newly built Author component.

1. Edit `card.twig` by replacing the current code for author information with the code below:

{% tabs %}
{% tab title="card.twig" %}
```php
{% block author %}
  {% if author %}
    {%
      include '@training_theme/author/author.twig' with {
        "author": author
      } only
    %}
  {% endif %}
{% endblock author %}
```
{% endtab %}
{% endtabs %}

1. Rebuild your theme by running

```text
npm run build && npm run watch
```

Windows users may need to run the two commands above separately \(`npm run build` then `npm run watch`

### Full Card code

{% tabs %}
{% tab title="card.twig" %}
```php
{{ attach_library('training_theme/card') }}

<article class="card{{ modifier ? ' ' ~ modifier }}
  {{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>

  {# Date for featured content cards. #}
  {% if 'card--wide' in modifier %}
    {% block featured_date %}
      <div class="card__featured--date">
        {{ date }}
      </div>
    {% endblock featured_date %}
  {% endif %}

  {% if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
  <div class="card__content">
    {% if title %}
      {{ title_prefix }}
      {%
        include '@training_theme/heading/heading.twig' with {
          heading: heading
        } only
      %}
      {{ title_suffix }}
    {% endif %}

    {# Date for featured content cards. #}
    {% if 'card--wide' not in modifier %}
      {% block card_date %}
          <div class="eyebrow card__date">
            {{ date }}
          </div>
      {% endblock card_date %}
    {% endif %}

    {% if category %}
      <div class="eyebrow card__category">
        {{ category }}
      </div>
    {% endif %}

    {% if body_text %}
      <div class="card__body">
        {{ body_text }}
      </div>
    {% endif %}

    {% block tags %}
      {% if tags %}
        <ul class="tags">
          {% for item in tags %}
            <li class="tag__item">
              <a href="{{ item.url }}" class="tag__link">
                {{ item.name }}
              </a>
            </li>
          {% endfor %}
        </ul>
      {% endif %}
    {% endblock tags %}

    {% block author %}
      {% if author %}
        {%
          include '@training_theme/author/author.twig' with {
            "author": author
          } only
        %}
      {% endif %}
    {% endblock author %}
  </div>
</article>
```
{% endtab %}
{% endtabs %}

