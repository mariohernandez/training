# Card Variant

Probably the first thing you should look at to determine if a component is a candidate for variants, is the data fields, and second, the component's markup.

Visually we know the two different variants look similar, however, if we pay close attention we will notice that the data fields between the variants are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes between the variants that we should have no problem going the variant route vs. new components. Let's start! The new variant will be called **Card wide**.

## Exercise: Creating the Card variant

![Card Wide variant](../.gitbook/assets/card-wide.png)

We can see that the overall layout of the "Card wide" lends itself nicely to a variant. However, we see that some of the fields found in the original card are not present here \(tags\), and there is also a new field in this variant that is not part of the original card \(button\).

Before we can create a new variant, we need to make some updates to the original Card component so it is easier to adapt it to new variant.

## Updating the original Card component

The card variant can be accomplished with a combination of a modifier CSS class and the use of [Twig Blocks](../getting-started/twig-blocks.md), which we discussed before.

### Modifier class

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

Now with this new class available, we can do all kinds of changes to the card variant without affecting the original card. One simple change we can make to the **card\_\_wide** variant is changing the card's layout so the image is moved to the left and the rest of the content is moved to the right.

#### CSS updates \(no need to this\)

{% tabs %}
{% tab title="card.scss" %}
```css
.card {
  display: flex;
  flex-direction: column;
  ...
  &.card__wide {

    @include breakpoint($bp-sm) {
      flex-direction: row;

      .card__media,
      .card__content {
        flex: 0 0 50%;
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

I've streamlined the styles above to show how we will turn the original card into the wider version. The styles above only apply if the card component has both, `card card__wide` classes to help float the image and content side by side, plus assign each a 50% width so things are evenly sized. The card markup was written this way by design. Placing the image and remaining of content in two separate wrappers \(`card__media` & `card__content`\), makes things extremely easy.

### Omitting fields in Card wide variants

So the modifier class helped us achieve some of the updates to the card wide variant, but there is still more to do. For example, the card wide variant does not use the tags. How do we exclude those fields in this variant? Read on.

### Pseudo Patterns in Pattern Lab

Before we can omit fields in the card variant we need to create the necessary files in Pattern Lab. Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variants of components. Let's take a look at an example of how pseudo patterns work.

This is the current structure of the Card component

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
```

### Creating a new variant

* Inside the _card_ directory, create a new JSON file with the following naming convention: `card~wide.json` \(notice the tilde \(~\)  in the file name\).  The tilde \(`~`\) and `.json` file extension are the hints that Pattern Lab uses to determine that this is a pseudo-pattern. The `card` part of the file name, tells Pattern Lab which existing pattern it should use when rendering the pseudo-pattern. The JSON file itself works exactly like the [pattern-specific JSON file](https://patternlab.io/docs/data-pattern-specific.html). It has the added benefit that the pseudo-pattern will also inherit any values from the existing pattern’s pattern-specific JSON file. This is not always a good thing and we will need to address this in our exercise.
* The structure of the card component should now look like below.  We don't need to create a new Twig file because by default Pattern Lab will use the original card.twig template.  This also will need updating in order for us to achieve our card variant.

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
|  |-- card~wide.json
```

### Displaying the right fields for the card variant

As indicated above, by default the pseudo pattern file \(`card~wide.json`\), inherits all the fields from `card.json`. This is usually good but in our case, we don't need some of the fields in the Card variant. For example, we don't need the tags or the article date fields. In addition, the card title in the variant should not be a link and its text should read "Marie The Producer". So how do we remove those fields without affecting the original Card component?

```yaml
{
  "title": {
    "heading_level": "3",
    "modifier": "card__title",
    "title": "Marie The Producer",
    "url": ""
  },
  "date": "",
  "job_title": "Executive Producer",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
  "tags": "",
  "cta": {
    "text": "Read the full bio",
    "url": "#",
    "modifier": "card__cta"
  },
  "modifier": "card__wide"
}
```

* Let's start with the new fields.  As you can see we have added the **job\_title** and **cta** fields
* Next, for those fields we don't need, we are declaring them with no values.
* Finally, for the fields we need to change, we can change their values as we've done with the **title**, **url**, and **modifier** fields.

The card wide variant now excludes tags and date fields. When we built the card we wrapped each field in conditional `if` statements. This means if the fields don't exist or have no values, they will never get printed or rendered on a page .

`npm run build`

`npm run watch`

You should now see two Card components in Pattern Lab. The second one should not have tag or date fields. We still have one thing to solve, although we have added the **cta** field to the JSON file, we are not seeing in the card variant. Let's fix that next.

### How do we add new fields to a variant? 🤔

So far we have been able to create a new card variant by using Pattern Lab's pseudo patterns feature. We were able to change the card's layout by using a modifier css class, and were able to remove or omit fields by using `if` statements in the original card component. Now the question is; How do we add new fields to a variant but not to the original component?

### Twig blocks

The idea of Twig Blocks is to place them on areas of Twig templates where the desired content change is expected. If not used, Twig blocks have no effect on your templates which is a way of saying, you can add Twig blocks to your templates or components, and if you don't use them, don't worry, they won't break anything.

Twig blocks are a great way to alter content on Twig templates prior to rendering the content. With a Twig block we can add or remove content during a component nesting or integration with Drupal.

### Exercise: Add a Twig block to the Card

* Edit `card.twig` and add the `job_title` field directly after the the **date** field \(around line 29\)
* Scroll to the bottom of the template and add a Twig block in the place where we expect the button to display. In this example, that will be around line 55.
* To ensure the button will only display if the field is not empty, we wrapped it in an `if` statement. This will ensure any markup related to the button will not print in the original card component since that field does not exist in `card.json`.

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
  {% if title or date or job_title or body or tags or cta %}
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
    {% if body_text %}
      <p class="card__body-text">
        {{ body_text }}
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
    {% block card_cta %}
      {% if cta %}
        {%
          include '@training_theme/button/button.twig' with {
            button: cta
          } only
        %}
      {% endif %}
    {% endblock %}
  </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

* First, we added the **job title** field.  Reason for this is that the `date` field, although uses the eyebrow component, is its own field type \(date\), whereas the `job_title`field is a text field type.  Although they may share the same styles when the content is entered in Drupal, date and job title will be separate fields.
* Then we added a Twig block called **card\_cta** \(`{%  block card_cta  %}`\).
* Inside the twig block we added the logic for the button and included the button component.

### Compiling the code

`npm run build`

`npm run watch`

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). Now both component variants should match the expected components. The second variant should have a button in addition to the class of `card__wide` along with `card`. How cool is this? 🧠 😮

### Next: Create a Card paragraph type

