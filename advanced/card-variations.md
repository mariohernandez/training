# Card Variations

Probably the first thing you should look at to determine if a component is a candidate for variations, is the data fields, and second, the component's markup.

Here's what the markup for the original Card component looks like:

```php
<section class="card{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="card__content">
    {% if title %}
      {%
        include '@training_theme/heading/heading.twig' with {
          "heading": heading
        } only
      %}
    {% endif %}

    {% if body_text %}
      {%
        include '@training_theme/body-text/body-text.twig' with {
          "body_text": body_text
        } only
      %}
    {% endif %}

    {% if author %}
      <cite class="card__author">
        <p class="card__author--name">{{ author.name }}</p>
        <p class="card__author--job-title">{{ author.job_title }}</p>
        <p class="card__author--city">{{ author.city }}</p>
      </cite>
    {% endif %}
  </div>
</section>
```

Visually we know the 3 different variations look similar, however, if we pay close attention we will notice that the data fields among some of the variations are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes among the variations that we should have no problem going the variation route vs. new components. Let's start!

## Creating the White Card variation

![White Card](../.gitbook/assets/card-white.png)

We can see that the overall layout of the "white" version of the component lends itself nicely to a variation. However, we see that some of the fields found in the original card are not present here \(title and Author info\), and there is also a new field in this variation that is not part of the original card \(button\).

Before we can create a new variation, we need to make some updates to the original Card component so it is easier to adapt it to new variations.

## Updating the original Card component

Some variations of the Card can be accomplish by simply passing a modifier/CSS class, but others will require a little more work and the use of [Twig Blocks](../getting-started/twig-blocks.md), which we discussed before.

### Modifier class approach

If you look at the [Card's JSON](https://mariohernandez.gitbook.io/training/building-components/card#components-stock-content) file you will see one of the keys is `modifier.`The **modifier** key in JSON means we can use it to pass a value to the Card as a CSS class. However, before the Card can make use of that value, it needs to know where to place it. If you look at the [Card's markup](https://mariohernandez.gitbook.io/training/building-components/card#components-markup), you will see the following line which acts as a placeholder for when a modifier value is passed:

```php
<section class="card{{ modifier ? ' ' ~ modifier }}...">
```

The part `{{ modifier ? ' ' ~ modifier }}` is basically a Twig conditional statement asking "Is there a value for modifier in JSON? if so, print it here along with the class of `card`, but add an empty space in between the two classes. For example, if the value for modifier in JSON is, `card--white`, when the Card is rendered in the browser the `section` wrapper will now look like this:

```php
<section class="card card--white">
```

Now with this new class available, we can do all kinds of changes to the card variation without affecting the original Card. A couple of simple changes we can make to the white card variation are changing the card's background color from cyan to white, change the text color from white to gray, and change the quote's color to cyan as you see in the Card image above.

### Omitting fields in Card variations

So the modifier class helped us achieve some of the updates to the white variation, but there is still more to do. For example, the white variation does not use a Title field or any of the Author-related fields \(name, job title, city\). How do we exclude those fields in this variation?  Read on.

### Pseudo Patterns in Pattern Lab

Before we can omit fields in the white card we need to create the necessary files in Pattern Lab.  Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variations of components. Let's take a look at an example of how pseudo patterns work.

This is the current structure of the Card component

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
```

* To create a new pseudo pattern, or variation for the card component, we create a new Twig file with the following naming convention: `card~white.twig` \(notice the **tilde** in the file name\).  The term following the tilde \(white\), becomes the name by which the variation is know.
* Next we create a new JSON file with the same naming convention `card~white.json`.  So the new Twig template will look into the new JSON file for its data.  This means we can be selective as to which fields we include in the new JSON file based on the requirements for this variation.  
* The structure of the Card component should now look like this:

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
|  |-- card~white.twig
|  |-- card~white.json
```

* Now let's copy the content of `card.json` into `card~white.json`
* Since the white version of the Card does not use a Title or Author info, let's remove those fields from `card~white.json`
* In `card~white.twig` add the following code:

{% tabs %}
{% tab title="card~white.twig" %}
```php
{% include '@theme_name/card/card.twig' with {
    "image": image,
    "body_text": body_text,
  } only
%}
```
{% endtab %}
{% endtabs %}

The white variation now only uses two of the fields from the original card \(`image` and `body_text`\). What's going to happen to the remaining fields? Well, if you remember when we built the original Card component, we wrapped each field in conditional `if` statements. This means if the fields don't exist or have no values, they will never get printed or rendered on a page. Since we are only passing a limited number of fields in the white variation, the missing fields will simply be ignored.

* Rebuild your project \(`npm run build && npm run watch`\)
* You should now see two Card components in Pattern Lab.  The second one should not have a title or author-related fields.

### How do we add new fields to a variation? 🤔

So far we have been able to create a new card variation by using Pattern Lab's pseudo patterns feature.  We were able to change the background color of the white card variation by using a modifier css class, and were able to remove or omit fields from the white card by proactively using `if` statements in the original Card component.  Now the question is; How do we add new fields to a variation but not to the original component? 

## Twig blocks

The idea of Twig Blocks is to place them on areas of Twig templates where the desired content change is expected. If not used, Twig blocks have no effect on your templates which is a way of saying, you can add Twig blocks to your templates or components, and if you don't use them, don't worry, they won't break anything.

Twig blocks are a great way to alter content on Twig templates, including components, prior to rendering the content. With a Twig block we can add or remove content during a component nesting or integration with Drupal.

Let's update the `card.twig` template below by scrolling to the bottom of the template and adding a Twig block in the place where we expect the button to display. In this example, that will be around line 35.

{% tabs %}
{% tab title="card.twig" %}
```php
<section class="card{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="card__content">
    {% if title %}
      {%
        include '@training_theme/heading/heading.twig' with {
          "heading": heading
        } only
      %}
    {% endif %}

    {% if body_text %}
      {%
        include '@training_theme/body-text/body-text.twig' with {
          "body_text": body_text
        } only
      %}
    {% endif %}

    {% if author %}
      <cite class="card__author">
        <p class="card__author--name">{{ author.name }}</p>
        <p class="card__author--job-title">{{ author.job_title }}</p>
        <p class="card__author--city">{{ author.city }}</p>
      </cite>
    {% endif %}

    // Placeholder for a button to be added.
    {% block card_cta %}
    {% endblock %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

* We added a Twig block called **card\_cta** \(`{%  block card_cta  %}`\). Currently  the Twig block is empty but we will make use of it in our variation.
* Update the `card~white.json` file so it includes the **button/cta** field, like this \(starting  on line 4\):

```text
{
  "image": "<img src='https://source.unsplash.com/TuIcz8wgB74/960x540' alt='A wonderful image' />",
  "body_text": "Easy additions such as a “skip to” links, focus indicators, and the ability to resize text makes a big difference in the lives of real people, every day.",
  "cta": {
    "text": "Learn more here",
    "modifier": "card__cta",
    "url": "#"
  },
  "modifier": "card__white"
}
```

Although the data file now reflects the button field, we have no way to add it to the `card~white.twig` template because Twig `include` statements can't alter the included template's data. Before we can make use the the Twig block we added in the original Card component, we need to update the `card~white.twig` template by using instead an `embed` statement to nest the original  Card component. Like so:

{% tabs %}
{% tab title="card~white.twig" %}
```php
{% embed '@theme_name/card/card.twig' with {
    "image": image,
    "body_text": body_text,
    "modifier": modifier
  }
%}
  {% block card_cta %}
    {%
      include '@theme_name/button/button.twig' with {
        "text": cta.text,
        "url": cta.url,
        "modifier": cta.modifier
      } only
    %}
  {% endblock %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

Thanks to Twig's `embed` statements, we can take advantage of Twig blocks to add new content to the Card variation.  In this case we included the button component. This is extremely powerful because in addition to be able to inherit most of the attributes from the original Card component, we still have the flexibility to modify the data in the component variation to achieve the outcome we wanted.

If you rebuild your project \(`npm run build && npm run watch`\), you should now see two Card components, the second instance should have a button in addition to the class of `card__white` next to `card`. How cool is this? 🧠 😮

## Next exercise

Now that you have a good idea of how to handle component variations, go ahead and build the other Card variation. You can call it **Card Reverse**.

