# Hero Component

The Hero component is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the Hero we will reuse other components by using twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) and [Embed](https://twig.symfony.com/doc/2.x/tags/embed.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles.  Let's do this with the hero component.

First let's take a look at how this component looks so we can identify the different data fields we need.  As we can see we need an image field, a title field, and a button or call to action.

## Let's start

### Component's stock content

1. Inside _components_ create a new directory called **hero**
2. Inside the _hero_ directory create a new file called **hero.json**
3. Inside _hero.json_ add the following code:

```yaml
{
  "image": "<img src='https://source.unsplash.com/FIKD9t5_5zQ/1400x787' alt='A wonderful image' />",
  "heading": {
    "title": "Scholar’s Edge has transitioned to Principal Funds",
    "heading_level": "1",
    "modifier": "hero__title",
    "url": ""
  },
  "cta": {
    "text": "Find out what's changed",
    "url": "#",
    "modifier": ""
  },
  "modifier": ""
}
```

As we did previously with the Heading component, we are using JSON to define the component's fields and add stock content to the component.
* We created an `image` field with a random image,
* then we created an object for the `heading` or title field.  Notice how the heading object structure matches that of the heading component.  This will help us reuse the heading compooonent more easily (more on this later),
* we added a `cta` field which has a `text` property for the button's text and a `url` which will help us link the button to any page.
* finally we are adding a `modifier` key so we have the option to pass a modifier class to the hero and update its look or behavior if needed.

### Component's Markup

Now let's write some HTML for the component.

1. Inside the _hero_ directory create a new file called **hero.twig**
2. Inside `hero.twig` add the following code:

```php
<section class="hero">
  {% if image %}
    <div class="hero__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="hero__content">
    {% if heading %}
      {%
        include '@training_theme/heading/heading.twig' with {
          "heading": heading
        } only
      %}
    {% endif %}

    {% if cta %}
      {%
        include '@training_theme/btn/btn.twig' with {
          "text": cta.text,
          "url": cta.url,
          "modifier": ' hero__cta'
        } only
      %}
    {% endif %}
  </div>
</section>
```

_In the interest of addressing the basics of component-building, we are going to exclude Drupal-specific elements.  We will comeback later to enhace the Hero with those elements_.

* We're starting off with a `<section>` HTML5 tag.  Learn more about the [<section>](https://www.w3schools.com/tags/tag_section.asp) tag.  This is the parent selector of the component and therefore it should be named **hero**.  We do this by using the class of `hero`,
* then we check whether there is an `image` available, and if there is, we print the `{{ image }}` variable within it s own div wrapper (`<div class="hero__media">`),
* **here's is something new and cool**, we make use of Twig's `include` statement to include or nest the **Heading** component we built in the previous exercise.  This is extremely powerful and we will be talking more about it later.
* Finally, we use another `include` statement to nest the button component which we have already built.

### Component's styles

We'll skip styles for now, but let's at least create a Sass file for when we need to write styles.

1. Inside the _hero_ directory create a new file called **hero.scss**
2. Inside `hero.scss` add this code:

```css
// Import site utilities
@import '../../global/utils/init';
```

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass. More on this later.

### Compiling the code

Now that the Hero component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build && npm run watch`

This command combines both the `build` and `watch` tasks.

In your browser of choice open the following url: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Hero component under components.
