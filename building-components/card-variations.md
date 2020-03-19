# Card variations

Probably the first thing you should look at  to determine if a component is a candidate for variations, is the data fields, and second, the component's markup.

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

Visually we know the 3 different variations looks similar, however, if we pay close attention we will notice that the data fields among some of the variations are different.  In this particular case although some of the fields may be different, I feel we have enough of shared attributes on the variations that we should have no problem going that route.  Let's start!

### Creating the Card Inverse variation

![](../.gitbook/assets/card-inverse.png)

We can see that the overall layout of the inverse version of the component lends itself nicely to a variation.  However, we see that some of the fields found in the original card are not present here \(title and Author info\), and there is also a new field in this variation that is not part of the original card \(button\).

Before we can create a new variation, we need to make some updates to the original Card component so it is easier to adapt it to new variations.

### Updating the original Card component

Some variations of the Card can be accomplish by simply passing a modifier/CSS class, but others will require a little more work and will also need the use of [Twig Blocks](../essentials/twig-blocks.md), which we discussed before.

#### Modifier class approach

If you look at the [Card's JSON](https://mariohernandez.gitbook.io/training/building-components/card#components-stock-content) file you will see one of the keys is `modifier.`The **modifier** key in JSON means we can use it to pass a value to the Card as a CSS class.  However, before the Card can make use of that value, it needs to know where to place it.  If you look at the [Card's markup](https://mariohernandez.gitbook.io/training/building-components/card#components-markup),  you will see the following line which acts as a placeholder for when a modifier value is passed:

```php
<section class="card{{ modifier ? ' ' ~ modifier }}">
```

The part `{{ modifier ? ' ' ~ modifier }}` is basically a conditional statement asking "Is there a value for modifier in JSON?  if so, print it here along with the class of `card`, but add an empty space in between the two classes.  For example, if the value for modifier in JSON is, `card--inverse`, when the Card is rendered in the browser the section wrapper will now look like this:

```php
<section class="card card--inverse">
```

Now with this new class available, we can do all kinds of changes to the card variation without affecting the original Card.  A couple of simple changes we can make to the inverse card variation are changing the card's background color from cyan to white, and change the text color from white to gray as you see in the Card image above.  

#### Omitting fields in Card variations

So the modifier class helped us achieve some of the updates to the Inverse variation, but there is still more to do.  For example, the Inverse variation does not use a Title field or any of the Author-related fields \(name, job title, city\).  How do we exclude those fields in this variation?

Now let's see how we can add the button and also remove the title in a way that does not affect the original Card component.

#### Twig Blocks approach

So the idea of Twig Blocks is to place them on areas or fields you think may change from variation to variation.  

Before we get started, let's discuss how to create component variations in Pattern Lab.  [Pattern Lab uses Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variations of components.  Let's take a look at an example of how pseudo patterns work.

This is the current structure of the Card component

```text
|--card
|  |-- card.scss
|  |-- card.twig
|  |-- card.json
```

* To create a new pseudo pattern for the card variation we create a new Twig file  with the following name convention: `card~inverse.twig` \(notice the tilde in the file name\).
* Next we create a new JSON file with the same naming convention `card~inverse.json`.  The structure should now look like this:

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
* In `card~inverse.twig` add the following code:

{% tabs %}
{% tab title="card~inverse.twig" %}
```php
{%
  include '@training_theme/card/card.twig' with {
    "image": image,
    "body_text": body_text,
  } only
%}
```
{% endtab %}
{% endtabs %}

The inverse variation now only uses two of the fields from the original card.  What's going to happen to the remaining fields?  Well, if you remember when we built the original Card component, we wrapped each field in conditional `if` statements.  This means if the fields don't exist or have no values, they will never get printed or rendered on a page.  Since we are only passing a limited number of fields in the inverse variation, the missing fields will simply be ignored.

Now how do we add the CTA field to the inverse card since it does not exist in the original Card component?  This is where **Twig Blocks** come in

### Adding and using twig blocks

Twig blocks are a great way to alter content on Twig templates, including components, prior to rendering the content.  With a Twig block we can add or remove content during a component nesting or integration with Drupal.

Let's update the `card.twig` template below by scrolling to the bottom of the template and adding a Twig block in the place where we expect the button to be added.  In this example, that will be around line 33.

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
    
    // Placeholder for a button to be added.
    {% block card_cta %}
    {% endblock %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

* We added a Twig block called **card\_cta** \(`{%  block card_cta  %}`\). Currently  the Twig block is empty but we will make use of it in our variation.
* Update the `card~inverse.json` file so it includes the **button** field, like this \(starting  on line 4\):

```text
{
  "image": "<img src='https://source.unsplash.com/TuIcz8wgB74/960x540' alt='A wonderful image' />",
  "body_text": "Easy additions such as a “skip to” links, focus indicators, and the ability to resize text makes a big difference in the lives of real people, every day.",
  "cta": {
    "text": "Learn more here",
    "modifier": "card__cta",
    "url": "#"
  },
  "modifier": ""
}
```

Although the data file now reflects the button field, we have no way to add it to the `card~inverse.twig` template because Twig `include` statements can't alter the included template's data.  Before we can make use the the Twig block we added in the original Card component, we need to update the inverse twig template by using instead a `embed` statement.  Like so:

{% tabs %}
{% tab title="card~inverse.twig" %}
```php
{% embed '@training_theme/card/card.twig' with {
    "image": image,
    "body_text": body_text,
  }
%}
  {% block card_cta %}
    {%
      include '@training_theme/button/button.twig' with {
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

Thanks to the Twig's `embed` statements, we can take advantage of Twig blocks and in it we can include the  button  component.  This is extremely powerful because in  addition to be able to inherit most of the attributes from the original Card component, we still have the flexibility to modify the data in the component variation to achieve the outcome we wanted.

