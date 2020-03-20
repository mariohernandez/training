# Component collection

A component that will introduce us to a few more useful techniques for working with components is the image you see below.   The image  shows a typical type of content that you will most likely find on most websites.  We will refer to this as **Cards Collection**, but this could be  called many other things \(Card grid, article collection, latest news, etc.\).  Whatever the name is, the point is that we have a component repeated multiple times.  Some may build this a single component and there is nothing wrong with that approach, however, we could probably get more out of building a single card component first, then repeating it as many times as we want to.  By doing this, we have an individual card component we could use not only for this type of content by for various types of content.

![Example of Card Collection](../.gitbook/assets/collection.jpg)

### Planning for an individual Card component

We will start by building a single component called **Card** which as we can see, has the following data fields:

* image
* title
* body
* & button

#### Your assignment

Following the same directions for building the Hero or Quote components, build a Card component which reflects one of the items in the image above.

### Building the Card Collection component

Once the single Card component has been built, it is time to build the collection of Cards as shown in the image above.

This component will be completely different than the ones we've built thus far.  All previous components have been a single item, this one will have an unlimited number of items.  Let's start

### Component's stock content

1. Inside _components_ create a new directory called **card-collection**
2. Inside the _card-collection_ directory create a new file called `card-collection.json`
3. Inside _card-collection.json_ add the following code:

{% tabs %}
{% tab title="card-collectioon.json" %}
```yaml
{
  "heading": {
    "heading_level": "2",
    "modifier": "card-collection__title",
    "title": "All you need to know about components",
    "url": ""
  },
  "items": [
    {
      "image": "<img src='https://source.unsplash.com/FIKD9t5_5zQ/720x405' alt='Card image' />",
      "title": {
        "heading_level": "3",
        "modifier": "card-collection__title",
        "text": "Want to learn about components?",
        "url": ""
      },
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "cta": {
        "text": "Getting started",
        "url": "#",
        "modifier": "card-collection__cta"
      },
      "modifier": ""
    },
    {
      "image": "<img src='https://source.unsplash.com/FIKD9t5_5zQ/720x405' alt='Card image' />",
      "title": {
        "heading_level": "3",
        "modifier": "card-collection__title",
        "text": "Top benefits of components",
        "url": ""
      },
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "cta": {
        "text": "Advantages of components",
        "url": "#",
        "modifier": "card-collection__cta"
      },
      "modifier": ""
    },
    {
      "image": "<img src='https://source.unsplash.com/FIKD9t5_5zQ/720x405' alt='Card image' />",
      "title": {
        "heading_level": "3",
        "modifier": "card-collection__title",
        "text": "Where to go from here?",
        "url": ""
      },
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "cta": {
        "text": "What's next?",
        "url": "#",
        "modifier": "card-collection__cta"
      },
      "modifier": ""
    }
  ]
}

```
{% endtab %}
{% endtabs %}

There is a lot going on in this file let's go over it and you will see that it's actually relatively straight forward.

* First we defined the `heading`  object which will be used as the title for the entire collection.
* At around line 8, we declared an `items` array.  This will help us mimic the array of content to build the collection.  
* Each item in the items array represents a card.  Inside each card item we have defined the card's fields \(`image`, `title`, `body_text`, `cta` \).  We have repeated this 3 times to achieve the collection shown in the Card Collection image above.

### Component markup

So the data is ready, let's go ahead and add the markup for the component.

1. Inside the _card-collection_ directory create a new file called `card-collection.twig`
2. Inside _card-collection.twig_ add the following code:

{% tabs %}
{% tab title="card-collection.twig" %}
```php
{{ attach_library('theme_name/card-collection') }}

<section class="card-collection{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if heading %}
    {%
      include '@theme_name/heading/heading.twig' with {
        "heading": heading
      } only
    %}
  {% endif %}

  {% if items %}
    <ul class="card-collection__items">
      {% for item in items %}
        <li class="card-collection__item">
          {%
            include '@theme_name/card/card.twig' with {
              "image": item.image,
              "title": item.title,
              "body_text": item.body_text,
              "cta": item.cta,
              "modifier": item.modifier
            } only
          %}
        </li>
      {% endfor %}
    </ul>
  {% endif %}
</section>
```
{% endtab %}
{% endtabs %}

> As I mentioned earlier, this is like no other component we've built.  Let's go over what we are doing here.
>
> * As usual, first we attach the library for the component.  Don't forget to create that library
>
> As I mentioned earlier, this is like no other component we have built.  Let's take a closer look:
>
> * First we attach the component's library.  **Don't forget to create the library.**
> * Next we add a `section` element to wrap the entire component.  Here we add the corresponding css class \(`card-collection`\) and we append the `attributes` array as usual.
> * Next we make use of the **Heading** component to print the component's main title and we wrap it in an `if` statement.
> * Next we check if the `items` array exists, and if does, we open a `<ul>` element to which we pass the class of `card-collection__items`.  Notice how the classes associated with these elements describe not only what component they belong to, but also the relationship among the elements.
> * Then, for the first time we use a `for loop` function.

