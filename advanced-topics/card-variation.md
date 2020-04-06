# Card Variation

Probably the first thing you should look at to determine if a component is a candidate for variations, is the data fields, and second, the component's markup.

Here's what the markup for the original Card component looks like:

{% tabs %}
{% tab title="card.twig" %}
```php
{{ attach_library('training_theme/card') }}

<article class="card{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {%  if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
  {% if title or date or body or tags %}
  <div class="card__content">
    {% if title %}
      {%
        include '@training_theme/heading/heading.twig' with {
          heading: title
        } only
      %}
    {% endif %}
    {% if date %}
      {%
        include '@training_theme/eyebrow/eyebrow.twig' with {
          eyebrow: {
            text: date,
            modifier: 'card__date'
          }
        } only
      %}
    {% endif %}
    {% if body %}
      <p class="card__body">
        {{ body }}
      </p>
    {% endif %}
    {% if tags %}
      <ul class="card__tags--items">
        {% for item in tags %}
          <li class="card__tag--item">
            <a href="{{ item.url }}" class="card__tag--link">
              {{ item.text }}
            </a>
          </li>
        {% endfor %}
      </ul>
    {% endif %}
  </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

Visually we know the two different variations look similar, however, if we pay close attention we will notice that the data fields between the variations are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes between the variations that we should have no problem going the variation route vs. new components. Let's start! The new variation will be called **Card wide**.

## Exercise: Creating the Card variation

![](../.gitbook/assets/card-wide.png)

We can see that the overall layout of the "Card wide" version of the component lends itself nicely to a variation. However, we see that some of the fields found in the original card are not present here \(tags\), and there is also a new field in this variation that is not part of the original card \(button\).

Before we can create a new variation, we need to make some updates to the original Card component so it is easier to adapt it to new variation.

## Updating the original Card component

The card variation can be accomplished with a combination of a modifier CSS class and the use of [Twig Blocks](../getting-started/twig-blocks.md), which we discussed before.

### Modifier class approach

If you look at the [Card's JSON](https://mariohernandez.gitbook.io/training/advanced-topics/card#components-stock-content) file you will see one of the keys is `modifier.`The **modifier** key in JSON means we can use it to pass a value to the Card as a CSS class. However, before the Card can make use of that value, it needs to know where to place it. If you look at the [Card's markup](https://mariohernandez.gitbook.io/training/advanced-topics/card#components-markup), you will see the following line which acts as a placeholder for when a modifier value is passed:

{% tabs %}
{% tab title="card.twig" %}
```php
<article class="card{{ modifier ? ' ' ~ modifier }}...">
```
{% endtab %}
{% endtabs %}

The part `{{ modifier ? ' ' ~ modifier }}` is basically a Twig conditional statement asking "Is there a value for modifier in JSON? if so, print it here along with the class of `card`, but add an empty space in between the two classes. For example, if the value for modifier in JSON is, `card__wide`, when the card is rendered in the browser the `article` wrapper will now look like this:

```php
<article class="card card__wide">
```

Now with this new class available, we can do all kinds of changes to the card variation without affecting the original card. One simple change we can make to the **card\_\_wide** variation is changing the card's layout so the image is moved to the left and the rest of the content is moved to the right.

#### CSS updates

{% tabs %}
{% tab title="card.scss" %}
```css
.card {
  ...
  display: flex;
}

.card__media,
.card__content {
  flex: 0 0 50%;
}
```
{% endtab %}
{% endtabs %}

The styles above help float the image and content side by side, plus assign each a 50% width so things are evently sized.  The card markup was written this way by design.  Placing the image and remaining of content in two separate wrappers \(`card__media` & `card__content`\), makes things kind of layout changes extremely easy.

### Omitting fields in Card wide variations

So the modifier class helped us achieve some of the updates to the card wide variation, but there is still more to do. For example, the card wide variation does not use the tags. How do we exclude those fields in this variation? Read on.

### Pseudo Patterns in Pattern Lab

Before we can omit fields in the card variation we need to create the necessary files in Pattern Lab. Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variations of components. Let's take a look at an example of how pseudo patterns work.

This is the current structure of the Card component

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
```

### Creating a new variation

* Inside the _card_ directory, create a new Twig file with the following naming convention: `card~wide.twig` \(notice the **tilde** in the file name\).  The term following the tilde \(wide\), becomes the name by which the variation is known.
* Next we create a new JSON file with the same naming convention `card~wide.json`.  So the new Twig template will look into the new JSON file for its data.  This means we can be selective as to which fields we include in the new JSON file based on the requirements for this variation.
* The structure of the card component should now look like this:

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
|  |-- card~wide.twig
|  |-- card~wide.json
```

1. Now let's copy the content of `card.json` into `card~wide.json`
2. Since the wide version of the card does not use tags or date fields, let's remove those fields from `card~wide.json`
3. In `card~wide.twig` add the following code:

{% tabs %}
{% tab title="card~white.twig" %}
```php
{% include '@training_theme/card/card.twig' with {
    "body_text": body_text,
    "image": image,
    "modifier": modifier
    "title": title,
  } only
%}
```
{% endtab %}
{% endtabs %}

The card wide variation now excludes tags and date fields. When we built the card we wrapped each field in conditional `if` statements. This means if the fields don't exist or have no values, they will never get printed or rendered on a page .

`npm run build`

`npm run watch`

You should now see two Card components in Pattern Lab. The second one should not have tag or date fields. However, the variation is still missing a button and eyebrow fields. Let's work on this next.

### How do we add new fields to a variation? 🤔

So far we have been able to create a new card variation by using Pattern Lab's pseudo patterns feature. We were able to change the card's layout by using a modifier css class, and were able to remove or omit fields by using `if` statements in the original card component. Now the question is; How do we add new fields to a variation but not to the original component?

## Twig blocks

The idea of Twig Blocks is to place them on areas of Twig templates where the desired content change is expected. If not used, Twig blocks have no effect on your templates which is a way of saying, you can add Twig blocks to your templates or components, and if you don't use them, don't worry, they won't break anything.

Twig blocks are a great way to alter content on Twig templates prior to rendering the content. With a Twig block we can add or remove content during a component nesting or integration with Drupal.

Let's update the `card.twig` template below by scrolling to the bottom of the template and adding a Twig block in the place where we expect the button to display. In this example, that will be around line 35.

{% tabs %}
{% tab title="card.twig" %}
```php
{{ attach_library('training_theme/card') }}

<article class="card{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {%  if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
  {% if title or date eyebrow or body or tags or cta %}
  <div class="card__content">
    {% if title %}
      {%
        include '@training_theme/heading/heading.twig' with {
          heading: title
        } only
      %}
    {% endif %}
    {% if date %}
      {%
        include '@training_theme/eyebrow/eyebrow.twig' with {
          eyebrow: {
            text: date,
            modifier: 'card__date'
          }
        } only
      %}
    {% endif %}
    {% if job_title %}
      {%
        include '@training_theme/eyebrow/eyebrow.twig' with {
          eyebrow: {
            text: job_title,
            modifier: 'card__eyebrow'
          }
        } only
      %}
    {% endif %}
    {% if body %}
      <p class="card__body">
        {{ body }}
      </p>
    {% endif %}
    {% block card_cta %}
    {% endblock %}
  </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

* First, we added the **job title** field.  Reason for this is that the date field, although uses the eyebrow component, is its own field type \(date\), wheeas the _job title_ field is a text field type
* Then we added a Twig block called **card\_cta** \(`{%  block card_cta  %}`\). Currently  the Twig block is empty but we will make use of it in our variation.
* Update the `card~white.json` file so it includes the **button/cta** field, like this \(starting  on line 4\):

{% tabs %}
{% tab title="card.json" %}
```yaml
{
  "image": "<img src='https://placeimg.com/640/350/places' alt='Card image' />",
  "title": {
    "heading_level": "3",
    "modifier": "card__title",
    "text": "The beauty of nature",
    "url": "#"
  },
  "job_title": "Executive Producer",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
  "cta": {
    "text": "Read the full bio",
    "url": "#",
    "modifier": "card__cta"
  },
  "modifier": "card__wide"
}
```
{% endtab %}
{% endtabs %}

Although the data file now reflects the button field, we have no way to add it to the `card~wide.twig` template because Twig `include` statements can't alter the included template's data. Before we can make use the the Twig block we added in the original Card component, we need to update the `card~wide.twig` template by using instead an `embed` statement to nest the original Card component. Like so:

{% tabs %}
{% tab title="card~wide.twig" %}
```php
{% embed '@training_theme/card/card.twig' with
  {
    "title": title,
    "image": image,
    "job_title": job_title,
    "body_text": body_text,
    "modifier": modifier
  }
%}
  {% block card_cta %}
    {%
      include '@training_theme/button/button.twig' with {
        "button": cta
      } only
    %}
  {% endblock %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

Thanks to Twig's `embed` statements, we can take advantage of Twig blocks to add new content to the Card variation. In this case we included the button component. This is extremely powerful because in addition to being able to inherit most of the attributes from the original Card component, we still have the flexibility to modify the data in the component variation to achieve the outcome we wanted.

### Compiling the code

If you rebuild yoouor project you should see two card components. The second variation should have a button in addition to the class of `card__wide` along with `card`. How cool is this? 🧠 😮

`npm run build`

`npm run watch`

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000).  Now both component variations should match the expected components.

### Exercise: Create a Card paragraph type

Following the Hero's steps for creating a paragraph type in Drupal, do the same for a Card paragraph type which includes the fields for the **Card wide** variation \(title, image, job title, body text, and cta\).  In this particular case, the card title field will not be a link field.

