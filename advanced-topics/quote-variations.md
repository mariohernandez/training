# Quote Variations

Probably the first thing you should look at to determine if a component is a candidate for variations, is the data fields, and second, the component's markup.

Here's what the markup for the original Quote component looks like:

{% tabs %}
{% tab title="quote.twig" %}
```php
<section class="quote{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if image %}
    <div class="quote__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="quote__content">
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
      <cite class="quote__author">
        <p class="quote__author--name">{{ author.name }}</p>
        <p class="quote__author--job-title">{{ author.job_title }}</p>
        <p class="quote__author--city">{{ author.city }}</p>
      </cite>
    {% endif %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

Visually we know the 3 different variations look similar, however, if we pay close attention we will notice that the data fields among some of the variations are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes among the variations that we should have no problem going the variation route vs. new components. Let's start!

## Creating the White Quote variation

![](../.gitbook/assets/quote-white%20%281%29.png)

We can see that the overall layout of the "white" version of the component lends itself nicely to a variation. However, we see that some of the fields found in the original quote are not present here \(title and Author info\), and there is also a new field in this variation that is not part of the original quote \(button\).

Before we can create a new variation, we need to make some updates to the original Quote component so it is easier to adapt it to new variations.

## Updating the original Quote component

Some variations of the Quote can be accomplish by simply passing a modifier/CSS class, but others will require a little more work and the use of [Twig Blocks](../getting-started/twig-blocks.md), which we discussed before.

### Modifier class approach

If you look at the [Quote's JSON](https://mariohernandez.gitbook.io/training/building-components/quote#components-stock-content) file you will see one of the keys is `modifier.`The **modifier** key in JSON means we can use it to pass a value to the Quote as a CSS class. However, before the Quote can make use of that value, it needs to know where to place it. If you look at the [Quote's markup](https://mariohernandez.gitbook.io/training/building-components/quote#components-markup), you will see the following line which acts as a placeholder for when a modifier value is passed:

{% tabs %}
{% tab title="quote.twig" %}
```php
<section class="quote{{ modifier ? ' ' ~ modifier }}...">
```
{% endtab %}
{% endtabs %}

The part `{{ modifier ? ' ' ~ modifier }}` is basically a Twig conditional statement asking "Is there a value for modifier in JSON? if so, print it here along with the class of `quote`, but add an empty space in between the two classes. For example, if the value for modifier in JSON is, `quote--white`, when the Quote is rendered in the browser the `section` wrapper will now look like this:

```php
<section class="quote quote--white">
```

Now with this new class available, we can do all kinds of changes to the quote variation without affecting the original Quote. A couple of simple changes we can make to the white quote variation are changing the quote's background color from cyan to white, change the text color from white to gray, and change the quote's color to cyan as you see in the Quote image above.

### Omitting fields in Quote variations

So the modifier class helped us achieve some of the updates to the white variation, but there is still more to do. For example, the white variation does not use a Title field or any of the Author-related fields \(name, job title, city\). How do we exclude those fields in this variation? Read on.

### Pseudo Patterns in Pattern Lab

Before we can omit fields in the white quote we need to create the necessary files in Pattern Lab. Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variations of components. Let's take a look at an example of how pseudo patterns work.

This is the current structure of the Quote component

```text
|--quote
|  |-- quote.scss
|  |-- quote.twig
|  |-- quote.json
```

### Creating a new variation

* Inside the _quote_ directory, create a new Twig file with the following naming convention: `quote~white.twig` \(notice the **tilde** in the file name\).  The term following the tilde \(white\), becomes the name by which the variation is know.
* Next we create a new JSON file with the same naming convention `quote~white.json`.  So the new Twig template will look into the new JSON file for its data.  This means we can be selective as to which fields we include in the new JSON file based on the requirements for this variation.
* The structure of the Quote component should now look like this:

```text
|--quote
|  |-- quote.scss
|  |-- quote.twig
|  |-- quote.json
|  |-- quote~white.twig
|  |-- quote~white.json
```

* Now let's copy the content of `quote.json` into `quote~white.json`
* Since the white version of the Quote does not use a Title or Author info, let's remove those fields from `quote~white.json`
* In `quote~white.twig` add the following code:

{% tabs %}
{% tab title="quote~white.twig" %}
```php
{% include '@training_theme/quote/quote.twig' with {
    "image": image,
    "body_text": body_text,
    "modifier": modifier
  } only
%}
```
{% endtab %}
{% endtabs %}

The white variation now only uses two of the fields from the original quote \(`image` and `body_text`\). What's going to happen to the remaining fields? Well, if you remember when we built the original Quote component, we wrapped each field in conditional `if` statements. This means if the fields don't exist or have no values, they will never get printed or rendered on a page. Since we are only passing a limited number of fields in the white variation, the missing fields will simply be ignored.

`npm run build`

`npm run watch`

You should now see two Quote components in Pattern Lab. The second one should not have a title or author-related fields.

### How do we add new fields to a variation? 🤔

So far we have been able to create a new quote variation by using Pattern Lab's pseudo patterns feature. We were able to change the background color of the white quote variation by using a modifier css class, and were able to remove or omit fields from the white quote by proactively using `if` statements in the original Quote component. Now the question is; How do we add new fields to a variation but not to the original component?

## Twig blocks

The idea of Twig Blocks is to place them on areas of Twig templates where the desired content change is expected. If not used, Twig blocks have no effect on your templates which is a way of saying, you can add Twig blocks to your templates or components, and if you don't use them, don't worry, they won't break anything.

Twig blocks are a great way to alter content on Twig templates, including components, prior to rendering the content. With a Twig block we can add or remove content during a component nesting or integration with Drupal.

Let's update the `quote.twig` template below by scrolling to the bottom of the template and adding a Twig block in the place where we expect the button to display. In this example, that will be around line 35.

{% tabs %}
{% tab title="quote.twig" %}
```php
<section class="quote{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if image %}
    <div class="quote__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="quote__content">
    {% if title %}
      {%
        include '@training_theme/heading/heading.twig' with {
          "heading": heading
        } only
      %}
    {% endif %}

    {% if body_text %}
      <div class="quote__body-text">
        {{ body_text }}
      </div>
    {% endif %}

    {% if author %}
      <cite class="quote__author">
        <p class="quote__author--name">{{ author.name }}</p>
        <p class="quote__author--job-title">{{ author.job_title }}</p>
        <p class="quote__author--city">{{ author.city }}</p>
      </cite>
    {% endif %}

    {# Placeholder for a button to be added. #}
    {% block quote_cta %}
    {% endblock %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

* We added a Twig block called **quote\_cta** \(`{%  block quote_cta  %}`\). Currently  the Twig block is empty but we will make use of it in our variation.
* Update the `quote~white.json` file so it includes the **button/cta** field, like this \(starting  on line 4\):

{% tabs %}
{% tab title="quote~white.json" %}
```text
{
  "image": "<img src='https://source.unsplash.com/TuIcz8wgB74/960x540' alt='A wonderful image' />",
  "body_text": "Easy additions such as a “skip to” links, focus indicators, and the ability to resize text makes a big difference in the lives of real people, every day.",
  "cta": {
    "text": "Learn more here",
    "modifier": "quote__cta",
    "url": "#"
  },
  "modifier": "quote__white"
}
```
{% endtab %}
{% endtabs %}

Although the data file now reflects the button field, we have no way to add it to the `quote~white.twig` template because Twig `include` statements can't alter the included template's data. Before we can make use the the Twig block we added in the original Quote component, we need to update the `quote~white.twig` template by using instead an `embed` statement to nest the original Quote component. Like so:

{% tabs %}
{% tab title="quote~white.twig" %}
```php
{% embed '@training_theme/quote/quote.twig' with {
    "image": image,
    "body_text": body_text,
    "modifier": modifier
  }
%}
  {% block quote_cta %}
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

Thanks to Twig's `embed` statements, we can take advantage of Twig blocks to add new content to the Quote variation. In this case we included the button component. This is extremely powerful because in addition to be able to inherit most of the attributes from the original Quote component, we still have the flexibility to modify the data in the component variation to achieve the outcome we wanted.

### Compiling the code

If you rebuild yoouor project you should see two Quote components.  The second variation should have a buttoon in addition to the class of `quote__white` along with `quote`.  How cool is this? 🧠 😮

`npm run build`

`npm run watch`

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). 

## Exercise:  Build the remaining variation

Now that you have a good idea of how to handle component variations, go ahead and build the other Quote variation. You can call it **Quote Reverse**.

