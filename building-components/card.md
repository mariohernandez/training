# Card Component

The Card component is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the Card we will reuse other components by using twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the Card component.

First let's take a look at how this component looks so we can identify the different data fields we need.

![Example of site&apos;s Card.](../.gitbook/assets/card.png)

As we can see we need the following fields:

* **image**: Card image
* **title**: Card title
* **body\_text**: Quote text
* **name**: Card's quote name
* **job title**: Card's quote job title
* **city**: Card's quote author

## Let's start

### Component's stock content

1. Inside _components_ create a new directory called **card**
2. Inside the _card_ directory create a new file called **card.json**
3. Inside _card.json_ add the following code:

```yaml
{
  "image": "<img src='https://source.unsplash.com/TuIcz8wgB74/960x540' alt='A wonderful image' />",
  "heading": {
    "title": "Small adjustments make a large impact",
    "heading_level": "2",
    "modifier": "card__title",
    "url": ""
  },
  "body_text": "Easy additions such as a “skip to” links, focus indicators, and the ability to resize text makes a big difference in the lives of real people, every day.",
  "author": {
    "name": "Sarah Lakos",
    "job_title": "Chief Technology Officer",
    "city": "San Francisco California"
  },
  "modifier": ""
}
```

We're declaring 3 fields in the Card component: **image**, **body_text**, and **author**.

### Component's Markup

Now let's write some HTML for the component.

1. Inside the _card_ directory create a new file called **card.twig**
2. Inside `card.twig` add the following code:

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

#### Some things to notice:

* Once again we are starting off with a `<section>` HTML5 tag.  This is the parent selector of the component and therefore it should be named **card**.  We do this by using the class of `card.`
* We are using a placeholder for the `modifier` key so if a value is passed from JSON to Twig, we will use that value as an extra CSS class on the Card wrapper (i.e. `card card__inverse`).
* For each field we want to print, we first check with an `if` statment whether there is content to print.  This is a good practice so we don't print empty HTML.
* Notice how every field uses a css class that starts with `card__`.  In some cases the class is declared in the JSON file, and in for other fields is done in the Twig code.  Defining relationships between the parent elements and child elements by using the same namespace \(card\_\_\), makes it easier to identify elements when inspecting code as well as finding those elements in our project.
* **Lastly, and super important**, we make use of Twig's `include` statement to include or nest the previously built components into the card.

### Component's styles

We'll skip styles for now, but let's at least create a Sass file for when we need to write styles.

1. Inside the _card_ directory create a new file called **card.scss**
2. Inside `card.scss` add this code:

```css
// Import site utilities
@import '../../global/utils/init';
```

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass. More on this later.

### Compiling the code

Now that the card component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build && npm run watch`

This command combines both the `build` and `watch` tasks.

In your browser of choice open the following url: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Card component under components.
