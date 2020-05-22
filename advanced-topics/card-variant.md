# Card Variant

Probably the first thing you should look at to determine if a component is a candidate for variants, is the data fields, and second, the component's markup.

Visually we know the two different variants look similar, however, if we pay close attention we will notice that the data fields between the variants are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes between the variants that we should have no problem going the variant route vs. new components. Let's start! The new variant will be called **Card wide**.

## Creating the Card variant

![Card Wide variant](../.gitbook/assets/card-wide.png)

We can see that the overall layout of the "Card wide" lends itself nicely to a variant. However, we see that some of the fields found in the original card are not present here \(tags\), and, there is also a new field in this variant that is not part of the original card \(button\).

Before we can create a new variant, we need to make some updates to the original Card component so it is easier to adapt it to new variants.

## Modifier class

A CSS modifier class is a pretty common way to make changes to any element. For example, let's say we use two types of buttons in our website; one red and one blue. Using CSS classes like say, `button--blue`, and `button--red` will allow us to change their colors without altering the original button. We will use a similar approach to achieve some of the changes in the Card wide variant.

* Notice that **card.json** already has a key for `modifier`.  This will allows us to pass a value to card.twig so we can implement some of the changes on the card wide variant.

{% tabs %}
{% tab title="card.json" %}
```yaml
{
  "modifier": "",
}
```
{% endtab %}
{% endtabs %}

* If you look at card.twig, notice we have a placeholder for modifier:

{% tabs %}
{% tab title="card.twig" %}
```php
<article class="card{{ modifier ? ' ' ~ modifier }}......">
```
{% endtab %}
{% endtabs %}

The part `{{ modifier ? ' ' ~ modifier }}` is a Twig conditional statement asking "_Is there a value for modifier in JSON?_" if so, print it here along with the class of `card`, but first add an empty space in between the two classes ``(` ` ~)``. For example, if the value for modifier in JSON is, `card--wide`, when the card is rendered in Pattern Lab, the `article` wrapper will look like this:

{% tabs %}
{% tab title="Pattern Lab" %}
```php
<article class="card card--wide">
```
{% endtab %}
{% endtabs %}

Now that we have the modifier key available, you can test it by adding any value to the `modifier` key and running `npm run watch` to view the card component in Pattern Lab. The Card component should now have, in addition to `card`, the value you added as an extra CSS class.

## CSS updates

In the interest of time, our CSS styles for the card already include styles for when we have a `card--wide` class in addition to `card`. So if you did use **card--wide** as the example value above, you should actually see the card looking different than the original card.

Our test above proves that using a CSS modifier class can help achieve some of the changes in the card variant, however, the goal is to not alter the original Card component when creating the variant. To accomplish this we need to work with Pattern Lab's Pseudo Patterns.

### Pseudo Patterns in Pattern Lab

Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variants of components. Pseudo-patterns are similar to [pattern-specific JSON files](https://patternlab.io/docs/data-pattern-specific.html) but are hinted in such a way that a developer can build a variant of an existing pattern. The idea of Pseudo Patterns is that Pattern Lab will create new instances of the source component, but it will not alter the source component. This is perfect because in the example of the card, we don't want to modify or change the way the original card component looks or behaves, when we create the **Card Wide** variant. The basic syntax for pseudo patterns is:

```text
patternName~pseudoPatternName.json
```

The tilde \(~\) and .json file extension are the hints that Pattern Lab uses to determine that this is a pseudo-pattern. The **patternName** tells Pattern Lab which existing pattern it should use when rendering the pseudo-pattern. The **pesudoPatternName** tells Pattern Lab the name for the new variant. The JSON file itself works exactly like the [pattern-specific JSON file](https://patternlab.io/docs/data-pattern-specific.html) . But it has the added benefit that the pseudo-pattern will also inherit any values from the existing pattern’s JSON file. This is not always a good thing and we will need to address this in our exercise.

From a navigation and naming perspective **patternName** and **pseudoPatternName** will be combined.

### Exercise: Creating a new variant

1. Inside the _card_ folder create a new JSON file with the following name: `card~wide.json` \(notice the tilde \(~\)  in the file name\). We don't need to create a new Twig file because by default Pattern Lab will use the original pattern's.twig template.  This also will need updating in order for us to achieve our card variant.  More on this later.
2. Copy all the code from `card.json` into `card~wide.json`

### Selecting the right fields for the card variant

As indicated above, by default the pseudo pattern file \(`card~wide.json`\), inherits all the fields from `card.json`. This is usually good but in our case, we don't need some of the fields in the Card variant. For example, we don't need the tags or the date fields. In addition, the card title in the variant should not be a link. And finally, the card variant uses a button but the original card does not. So how do we manage those fields without affecting the original Card component? Let's take a look:

* Update `card~wide.json` as shown below:

{% tabs %}
{% tab title="card~wide.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/BJrgqUKYx8M/640x640' alt='Women running' />",
  "title": {
    "heading_level": "2",
    "modifier": "",
    "title": "Level up your game",
    "url": ""
  },
  "date": "",
  "category": "Sports",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
  "tags": "",
  "cta": {
    "text": "Read the full article",
    "url": "#",
    "modifier": "button--ghost"
  },
  "modifier": "card--wide"
}
```
{% endtab %}
{% endtabs %}

* Let's start with the new fields.  As you can see we have added the **category** and **CTA** fields.  If you are wondering, Why not use the date field for the category since they look exactly the same? A date and text fields hold different type of data.  You can't enter text in a date field.  In addition, using the right field type for the type of data expected, will help editors when the content is being entered in the form.  In a date-type filed, the editor entering the content will be able to select the date from a calendar or date picker.  This is why we are using different fields here.
* Next, for those fields we don't need in the card wide variant, we are declaring them with no values.  If we simply remove them, they would be inherited from `card.json` It is best to leave them empty. They will not be printed on the page because in `card.twig` we first check if the field exists or it has content by using an `if` statement.  So any field that is empty above, will not be used.

### Twig blocks

Now that the variant's JSON is ready with only the fields we want, it's time to update **card.twig** to ensure the right card variant is rendered. Here is what we are going to do:

* Open `card.twig` and at around line 10 \(line numbers may not match your project\), we need to update the `if` statement by including the new fields used in the card wide variant \(category and CTA\).  Update the conditional statement as follows:

```php
{% if title or date or category or body_text or tags or cta %}
```

If you are wondering, Why are we doing this? It's considered best practice to ensure we check for whether there is content to render before we start writing HTML. If we don't check for this, we may end up with an empty `<div class="card__content">...</div>` wrapper in Pattern Lab and that's not cool 😃

* Next, at around line 24 \(directly after the `{% endif %}` statement for **date**\), add the following code:

```php
{% if category %}
  <div class="card__category">{{ category }}</div>
{% endif %}
```

The above is one of the new fields found in the card wide variant. Again, the line numbers in this exercise my not match the ones in your code.

* Finally, at around line 45 \(directly after the `{% endif %}` statement for **tags**\), add the following code:

```php
{% if cta %}
  {%
    include '@atoms/button/button.twig' with {
      button: cta
    } only
  %}
{% endif %}
```

{% hint style="info" %}
If you are wondering why are we placing the code snippets in those very locations within the file, the simple answer is that that's where those fields appear in the card. If we were to add the button or category fields at the top or bottom of card.twig, they would display at the top or bottom of the card in Drupal or Pattern Lab.
{% endhint %}

The full `card.twig` template should now look like this:

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
  {% if title or date or category or body_text or tags or cta %}
    <div class="card__content">
      {% if title %}
        {%
          include '@training_theme/heading/heading.twig' with {
            heading: title
          } only
        %}
      {% endif %}
      {% if date %}
       <div class="card__date">
          {{ date }}
        </div>
      {% endif %}
      {% if category %}
        <div class="card__eyebrow">
          {{ category }}
        </div>
      {% endif %}
      {% if body_text %}
        <p class="card__body">
          {{ body_text }}
        </p>
      {% endif %}
      {% if tags %}
        <ul class="card__tags">
          {% for item in tags %}
            <li class="card__tag--item">
              <a href="{{ item.url }}" class="card__tag--link">
                {{ item.text }}
              </a>
            </li>
          {% endfor %}
        </ul>
      {% endif %}
      {% if cta %}
        {%
          include '@training_theme/button/button.twig' with {
            button: cta
          } only
        %}
      {% endif %}
    </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

Now if we save our changes, we should see the two card variants in Pattern Lab, one with tags and a date field, and the other one without tags or date fields, but with a button and a category field. In addition, the Card wide variant's layout is horizontal vs. the original card has a vertical layout.

If you don't have Pattern Lab running, run this command:

```php
npm run watch
```

