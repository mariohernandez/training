# Card Component

A component that will introduce us to a more useful technique for working with components is the image you see below. A Card component is a great way to display all sorts of content \(news, blog posts, events, etc.\), and you will see it in many websites nowadays. The card is not typically displayed on its own, although sometimes it is, but its most common use is as a collection of content. For example, we could use a collection of cards to display latest blog posts or upcoming events. In this training we will use the card component to build two content lists; Featured Content, and Blog Content.

![Example of a Card component](../.gitbook/assets/card.png)

Although we could build the content list components already as a collection of content, a better approach is to first build a single instance of a card component that then we can reuse over and over. Having a single card component available makes it possible to even build other types of content collections.

## Exercise:  Card component

As we've did with the Hero component, one of the first things we need to define are the data fields that makeup the component. If you look at the image above, a single Card has the following data fields:

* image
* title \(link to full article\)
* date
* body
* & tags

Now that we have identified the fields our card component needs, let's start building it.

### Component's stock content

1. Inside `src/patterns/components` create a new folder called **card**
2. Inside the _card_ folder create a new file called **card.json**
3. Inside _card.json_ add the following code:

{% tabs %}
{% tab title="card.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/BJrgqUKYx8M/640x360' alt='Women running' />",
  "heading": {
    "heading_level": "2",
    "modifier": "card__title",
    "title": "Level up your game",
    "url": "#"
  },
  "date": "March 16 2020",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
  "tags": [
    {
      "name": "Photography",
      "url": "#"
    },
    {
      "name": "Sports",
      "url": "#"
    },
    {
      "name": "Outdors",
      "url": "#"
    }
  ],
  "modifier": ""
}
```
{% endtab %}
{% endtabs %}

By now we should be well familiar with the fields structure above. The one field type we probably have not seen until now is an array. In the code above we are declaring the tags as an array of items. Each tag item inside the array has a `text` and `url` keys so they can become links to tag-driven pages on our site.

### Component's markup

1. Inside the _card_ folder create a new file called **card.twig**
2. Inside _card.twig_ add the following code:

{% tabs %}
{% tab title="card.twig" %}
```php
{{ attach_library('training_theme/card') }}

<article class="card{{ modifier ? ' ' ~ modifier }}{{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>

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

    {% if date %}
      <div class="eyebrow card__date">
        {{ date }}
      </div>
    {% endif %}

    {% if body_text %}
      <div class="card__body">
        {{ body_text }}
      </div>
    {% endif %}

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
  </div>
</article>
```
{% endtab %}
{% endtabs %}

* Just as we did with the Hero, we are including the `attributes` placeholder so when we integrate the card with Drupal the attributes Drupal provides can be available in our card.
* Once again we are making use of the Heading component by using a Twig include statement.
* With the tags we loop through the `tags` array and then add each  tag item as a list item in an unordered list.

{% hint style="warning" %}
Don't forget to create and attach the Card's library.
{% endhint %}

### Component styles

1. Inside the _card_ folder create a new file called **card.scss**
2. Inside _card.scss_ add the following code:

{% tabs %}
{% tab title="card.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.card {
  background-color: $color-white;
  box-shadow: 0 10px 15px -3px rgba($color-black, 0.1), 0 4px 6px -2px rgba($color-black, 0.05);
  box-sizing: border-box;
  display: flex;
  flex: 0 0 auto;
  flex-direction: column;
  max-width: 320px;
  position: relative;

  @media screen and (min-width: $bp-md) {
    flex: 0 0 45%;
  }

  img {
    display: block;
    width: 100%;
  }

  .card__content {
    padding: 10px 20px 20px;
  }

  // ========== Card wide styles=========
  &.card--wide {
    border: 1px solid darken($color-gray-light, 10%);
    box-shadow: none;
    flex-direction: column;

    // Adds blue corner ship to card wide.
    &::before {
      border-right: 70px solid transparent;
      border-top: 70px solid $color-navy-blue;
      display: block;
      content: '';
      height: 0;
      left: -1px;
      position: absolute;
      top: -1px;
      width: 0;
      z-index: $zi-lowest;
    }

    // Positions date in 45 degrees over blue chip.
    .card__featured--date {
      color: $color-white;
      font-size: 1.2rem;
      font-weight: bold;
      left: 0;
      line-height: 1;
      position: absolute;
      text-transform: uppercase;
      top: 18px;
      transform: rotate(-45deg);
      z-index: $zi-lowest;
    }

    // Changes card layout on larger screens.
    @media screen and (min-width: $bp-sm) {
      flex-direction: row;
      max-width: 720px;

      .card__content {
        flex: 0 0 70%;

        @include breakpoint($bp-sm) {
          display: flex;
          flex-direction: column;
          flex-grow: 1;
        }
      }

      img {
        max-width: 100%;
      }
    }

    .card__media {

      @include breakpoint($bp-sm) {
        flex: 0 0 30%;
      }
    }
  }

  .eyebrow {
    border-bottom: 1px solid $color-gray-med;
    font-size: 1.3rem;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding-bottom: 8px;
  }

  .author {
    margin-top: auto;
    justify-content: flex-end;
  }
}

.card__body {
  margin-bottom: 20px;
}

.card__title {
  font-size: 2.4rem;
  font-weight: 600;
  margin: 0;
}
```
{% endtab %}
{% endtabs %}

* We'll get into the styles above in more detail later on.

### Compiling the code

Now that the card component is done, let's compile the code so we can see it in Pattern Lab. If the watch task is running you should be able to see the card component in Pattern Lab, otherwise follow these steps:

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Card component under components.

### Accessing Pattern Lab from within Drupal

When working with Pattern Lab locally it makes sense to use [http://localhost:3000](http://localhost:3000) to view your work. However, if you are viewing your project from a server during development, or want to show your work and progress to a stakeholder or client, this approach will not work. Luckily for us, we can access Pattern Lab using Drupal's URL as follows:

`/themes/custom/training_theme/patternlab/index.html`

Two things to keep in mind with the path above:

1. The path above is appended to your Drupal's base URL.  For example, if your Drupal's address is _https://dev.pantheon.io_, the full URL would become **https://dev.pantheon.io/themes/custom/training\_theme/patternlab/index.html**
2. Replace `training_theme` with your project's theme name if your theme name is different.

