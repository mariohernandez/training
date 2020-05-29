# Author component

As we just saw, the Card wide variant uses some information from the article author.  We don't have a component for users or authors so we need to quickly build one.

1. Inside `src/patterns/components` create a new folder called **author**
2. Inside the _author_ folder create **author.json**, **author.twig**, **author.scss**
3. Add the code below to each of the respective files

{% tabs %}
{% tab title="author.json" %}
```php
{
  "photo": "<img src='https://source.unsplash.com/_cvwXhGqG-o/100x100' alt='Author's headshot' />",
  "name": "Valentina De Leon",
  "title": "Digital Strategist"
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
    <div class="author__name">{{ name }}</div>
    <div class="author__title">{{ title }}</div>
  </div>
  <div class="author__photo">{{ photo }}</div>
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
  justify-content: flex-end;
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



