# From our blog

So far we've been building individual components and built them in a way we can re-use them. Well, the time has come to build a list of content where we will re-use most components we've built. Using the designs below, we will build the **From our blog** content list. Here are some details about this component:

* It uses multiple instances of the card component
* The entire collection has a heading of "From our blog"
* It uses a button that links users to a page like `/blog`

![](../.gitbook/assets/blog-content.jpg)

### Exercise: Build the From our blog component

This component will be completely different than the ones we've built thus far. All previous components have been a single item, this one will have an unlimited number of items. Let's start

#### Component's stock content

1. Inside `src/patterns/components`create a new folder called **from-our-blog**
2. Inside the _from-our-blog_ folder create a new file called `from-our-blog.json`
3. Inside _from-our-blog.json_ add the following code:

{% tabs %}
{% tab title="from-our-blog.json" %}
```yaml
{
  "heading": {
    "heading_level": "2",
    "modifier": "heading--large center section-header",
    "title": "From our blog",
    "url": ""
  },
  "cta": {
    "modifier": "",
    "text": "See more articles",
    "url": "#"
  },
  "items": [
    {
      "image": "<img src='https://source.unsplash.com/qQGAQMbURhU/640x360' alt='Man doing yoga' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    },
    {
      "image": "<img src='https://source.unsplash.com/HONJP8DyiSM/640x360' alt='Tech gadgets' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    },
    {
      "image": "<img src='https://source.unsplash.com/4b9Talfia6c/640x360' alt='Candy in shape of heart' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    },
    {
      "image": "<img src='https://source.unsplash.com/hn6CC9aosEk/640x360' alt='Painting of a tiger' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

There is a lot going on in this file. Let's go over it and you will see that it's actually relatively straight forward.

* First we declared the `heading`  object which will be the title for the entire collection \(From our blog\)
* Directly under that we are declaring a `cta` object which will be the button at the bottom of the list.  The order in which we define these objects has no effect on how things will turn out.
* At around line 13, we declared an array, `items: [ ]` .  This will help us mimic the array of content to build the collection.
* Each item in the array represents a blog post.  Inside each item we have declared the card's fields \(`image`, `title`, `date`, `body_text`, `tags` \).  So we've basically copied the content from `card.json` and have repeated it 4 times inside the items array in `from-our-blog.json`.

#### Component markup

So the data is ready, let's go ahead and add the markup for the component.

1. Inside the _from-our-blog_ folder create a new file called `from-our-blog.twig`
2. Inside _from-our-blog.twig_ add the following code:

{% tabs %}
{% tab title="from-our-blog.twig" %}
```php
{{ attach_library('training_theme/from-our-blog') }}

<section class="from-our-blog{{ modifier ? ' ' ~ modifier }}{{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  {%
    include '@training_theme/heading/heading.twig' with {
      "heading": heading
    } only
  %}

  <div class="from-our-blog__items">
    {% block blog_items %}
      {% for item in items %}
        {% embed '@training_theme/card/card.twig' with
          {
            "image": item.image,
            "title": item.title,
            "date": item.date,
            "body_text": item.body_text,
            "tags": item.tags,
            "modifier": item.modifier
          } only
        %}
          {% block featured_date %}
          {# Purposely leaving empty. #}
          {% endblock featured_date %}
        {% endembed %}
      {% endfor %}
    {% endblock blog_items %}
  </div>
  <div class="from-our-blog__cta">
    {%
      include '@training_theme/button/button.twig' with {
        button: cta
      } only
    %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

As I mentioned earlier, this is a unique component and nothing like we've built thus far. Let's review:

* First we attach the component's library.  **Don't forget to create the library.**
* Next we add a `<section>` element to wrap the entire component.  As we've done before, the first and main component wrapper should always use the name of the component as its class \(`from-our-blog`\).  In addition we pass the `modifier` and `attributes` placeholders.
* Next we make use of the **heading** component to print the component's main title.
* Next we create a wrapper to hold all the blog posts/cards with the class of `from-our-blog__items`
* Next we create twig block \(`blog_items`\), which we will use later to print Drupal's nodes.
* Inside the twig block we run a `for` loop function.  We are iterating through the items array and for each item we find in it, we include a card component using an `embed` statement.
* Notice we are declaring the `featured_date` twig block.  This particular card or collection of cards does not need the date on the top-left corner of the card like the card wide does.  So by declaring an empty twig block for `featured_date`, we are basically excluding that content from rendering. 
* Finally we are including a button component so we can link it to `/blog` or `/news`.

#### Component's styles

1. Inside the _from-our-blog_ folder create a new file called **from-our-blog.scss**
2. Inside `from-our-blog.scss` add this code:

{% tabs %}
{% tab title="from-our-blog.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.from-our-blog  {
  @include component-spacing;
  padding: 0 20px;

  @media screen and (min-width: $bp-xl) {
    padding: 0;
  }
}

// On mobile the cards are displayed
// vertically as a group.
.from-our-blog__items {
  align-items: center;
  display: flex;
  flex-direction: column;

  // On larger screens cards are displayed
  // horizontally as a group.
  @media screen and (min-width: $bp-sm) {
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}

.from-our-blog__card {
  margin-bottom: 60px;

  @media screen and (min-width: $bp-sm) {
    flex: 0 0 45%;
  }

  @media screen and (min-width: $bp-lg) {
    flex: 0 0 22%;
    margin-bottom: 0;
  }
}

.from-our-blog__cta {
  margin: 50px auto 0;
  text-align: center;
}
```
{% endtab %}
{% endtabs %}

The styles are very simple as they only focus on aligning the cards side by side.  All other card-specific styles were written in the card component.

## Compiling the code to generate the From our blog

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

{% hint style="info" %}
**TIP:** Since we created a whole new component; if you had the watch task running, it is recommended you stop it by pressing **Ctrl + C** on your keyboard and run the commands above. This will ensure the new component will be generated and all related code will be compiled.
{% endhint %}

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). You should be able to find the _From our blog_ component. The styles we wrote already account for responsive behavior of this component.

