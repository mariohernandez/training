# Quote Component

The Quote component is a more complex component than the Hero because in addition to using more fields, it also requires we crate variations that look different than the original Quote component. More on [component variations](component-variations.md) later. Just like we did with the Hero, with the Quote we will reuse other components.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the Quote component.

First let's take a look at how this component looks so we can identify the different data fields we need.

![Quote component](../.gitbook/assets/quote.png)

As we can see we need the following fields:

* **image**: Quote image
* **title**: Quote title
* **body\_text**: Quote text
* **name**: Quote author's name
* **job title**: Author's job title
* **city**: Author's city name

## Let's start

### Component's stock content

1. Inside _components_ create a new directory called **quote**
2. Inside the _quote_ directory create a new file called **quote.json**
3. Inside _quote.json_ add the following code:

{% tabs %}
{% tab title="quote.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/TuIcz8wgB74/960x540' alt='A wonderful image' />",
  "heading": {
    "title": "Learn all about our retirement plans",
    "heading_level": "2",
    "modifier": "quote__title",
    "url": ""
  },
  "body_text": "I've trusted Principal with my retirement because of the simplicity and transparency in their experience.",
  "author": {
    "name": "Sarah Lakos",
    "job_title": "Chief Technology Officer",
    "city": "San Francisco California"
  },
  "modifier": ""
}
```
{% endtab %}
{% endtabs %}

We're declaring 4 fields in the Quote component: **image**, **heading/title, body\_text**, and **author**.

### Component's Markup

Now let's write some HTML for the component.

1. Inside the _quote_ directory create a new file called **quote.twig**
2. Inside `quote.twig` add the following code:

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
  </div>
</section>
```
{% endtab %}
{% endtabs %}

#### Some things to notice:

* Once again we are starting off with a `<section>` HTML5 tag.  This is the parent selector of the component and therefore it should be named **quote**.  We do this by using the class of `quote.`
* We are using a placeholder for the `modifier` key so if a value is passed from JSON to Twig, we will use that value as an extra CSS class on the Quote wrapper \(i.e. `quote quote__white`\).
* As we did with the Hero, we are passing the `attributes` array which will be handy when we integrate the component with Drupal.  Moe on this later.
* For each field we want to print, we first check with an `if` statement whether there is content to print.  This is a good practice so we don't print empty HTML wrappers.
* Notice how every field uses a css class that starts with `quote__`.  In some cases the class is declared in the JSON file, and in for other fields is done in the Twig code.  Defining relationships between the parent elements and child elements by using the same namespace \(`quote__`\), makes it easier to identify elements when inspecting code as well as finding those elements in our project.
* **Lastly, and super important**, we make use of Twig's `include` statement to include or nest the previously built components into the quote.

### Component's styles

We'll skip styles for now, but let's at least create a Sass file for when we need to write styles.

1. Inside the _quote_ directory create a new file called **quote.scss**
2. Inside `quote.scss` add this code:

{% tabs %}
{% tab title="quote.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.quote {
  display: flex;
  background-color: blue;
  color: white;
}


.quote__content {
  padding: 40px;
}

```
{% endtab %}
{% endtabs %}

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass. More on this later.

### Compiling the code

Now that the quote component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Quote component under components.

