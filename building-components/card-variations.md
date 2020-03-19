# Card variations

Probably the first thing you should look at  to determine if a component is a candidate to create variations of, is the data fields, and second, the component's markup.

Here's what the markup for the original Card component looks like:

```php
<section class="card{{ modifier ? ' ' ~ modifier }}">
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

Visually we know the 3 different variations looks similar, however, if we pay close attention we will notice that the data fields among some of the variations are different.  It is a good practice to create your original component with the most elements possible and use the variations to create the least complicated versions of the component.

### Creating the Card Inverse variation

![](../.gitbook/assets/card-inverse.png)

We can see that the overall layout of the inverse version of the component lends itself nicely to a variation.  However, we see that some of the fields found in the original card are not present here \(title and Author info\), and there is also a new field in this variation that is not part of the original card \(button\).

Before we can create a new variation, we need to make some updates to the original Card component so it is easier to adapt to new variations.

### Updating the Card component

Some variations of the Card can be accomplish by simply passing a modifier/CSS class, but others will require a little more work and will also need the use of [Twig Blocks](../essentials/twig-blocks.md), which we discussed before.

#### Modifier class approach

If you look at the [Card's JSON](https://mariohernandez.gitbook.io/training/building-components/card#components-stock-content) file you will see one of the keys is `modifier.`The **modifier** key in JSON means we can use it to pass a value to the Card as a CSS class.  However, before the Card can make use of that value, it needs to know where to place it.  If you look at the [Card's markup](https://mariohernandez.gitbook.io/training/building-components/card#components-markup),  you will see the following line which acts as a placeholder for when a modifier value is passed:

```php
<section class="card{{ modifier ? ' ' ~ modifier }}">
```

The part `{{ modifier ? ' ' ~ modifier }}` is basically a conditional statement asking "Is there a value for modifer in JSON?  if so, print it here along with the class of `card`, but add an empty space in between the two classes.  So if the value for modifier in JSON is say, `card--inverse`, the line above will look like this when it is rendered in the browser:

```php
<section class="card card--inverse">
```

Now with this new class available, we can do all kinds of changes to the card variation without affecting the original card.  A couple of simple changes we can make to the inverse card variation is changing the card's background color from cyan to white, and change the text color from white to gray as you see in the Card image above.  

Now let's see how we can add the button and also remove the title in a way that does not affect the original Card component.

#### Twig Blocks approach

So the idea of Twig Blocks is to place them on areas or fields you think may change from variation to variation.  

Before we get started, let's discuss how to create component variations in Pattern Lab.  [Pattern Lab uses Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variations of components.  Let's take a look at an example of how pseudo patterns work.

This is the current structure of the card component

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
```

* To create a new pseudo pattern for the card variation we create a new Twig file  with the following name: `card~inverse.twig` \(notice the tilde in the file name\).
* Next we create a new JSON file with the following name `card~inverse.json`.  The structure should now look like this:

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
|  |-- card~inverse.twig
|  |-- card~inverse.json
```

* Now let's copy the content of `card.json` into `card~inverse.json`
* Since the inverse version of the Card does not use a Title or Author info, let's remove those fields from `card~inverse.json`
* When we built the Card component we wrapped each field in Twig inside an `if` statement.  This means that if a particular field is not available in the JSON file, that field and its wrapper will not be printed at all.  This addresses removing the Title field in the Card Inverse variation since we are not providing that data.  The same applies to the Author info, since we are not providing those fields in JSON, they will not be rendered in the Inverse card.
* Now how do we add the CTA field to the inverse card since it does not exist in the original Card component?  This is where Twig Blocks come in

{% tabs %}
{% tab title="card.twig" %}
```php
<section class="card{{ modifier ? ' ' ~ modifier }}">
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

    {% block card_cta %}
    {% endblock %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}



