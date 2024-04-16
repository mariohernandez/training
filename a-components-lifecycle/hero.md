# Hero Component

The Hero component is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the Hero we will reuse other components by using twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the Hero component.

First let's take a look at how this component looks so we can identify the different data fields we need.

![Hero component](../.gitbook/assets/hero.jpg)

Based on the design above, we need the following fields:

* **title or heading**
* **image**
* **call to action (CTA)**

## Exercise:  Build the Hero component

### Component's stock content

1. Inside _components_ create a new folder called **hero**
2. Inside the _hero_ folder create a new file called **hero.json**
3. Inside _hero.json_ add the following code:

{% tabs %}
{% tab title="hero.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/DOoYFgTQWfs/1900x700' alt='Books on computer' />",
  "heading": {
    "heading_level": "1",
    "modifier": "hero__title",
    "title": "Today's trends",
    "url": ""
  },
  "cta": {
    "text": "Get started",
    "url": "#",
    "modifier": "hero__cta"
  },
  "modifier": ""
}
```
{% endtab %}
{% endtabs %}

Just as we did with the Heading component, we are using JSON to define the component's fields and add stock/dummy content to the component. Our goal here is to reuse previously built components by nesting them into the hero to avoid code duplicate and improve maintenance of component by having a single source of code.

#### Some things to notice:

* We created data objects for **heading** and **cta**.  Although this is not required, doing this helps to organize fields and their properties as well as it simplifies the component nesting process in Twig.  More on this shortly
* We added a `modifier` key with an empty value.  This will come in handy when we need to pass custom CSS classes to component to style them.

### Component's Markup

Now let's write some HTML for the component.

1. Inside the _hero_ folder create a new file called **hero.twig**
2. Inside `hero.twig` add the following code:

{% tabs %}
{% tab title="hero.twig" %}
```php
<section class="hero{{ modifier ? ' ' ~ modifier }}
  {{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  {% if image %}
    <div class="hero__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="hero__content">
    {% if heading %}
      {%
        include '@storybook/heading/heading.twig' with {
          "heading": heading
        } only
      %}
    {% endif %}

    {% if cta %}
      {%
        include '@storybook/button/button.twig' with {
          "button": cta
        } only
      %}
    {% endif %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

#### Some things to notice:

* We're starting off with a `<section>` HTML5 tag.  Learn more about the [section](https://www.w3schools.com/tags/tag\_section.asp) tag.  This is the parent selector of the component and therefore assigned the CSS class of **hero**, which also becomes the namespace for this component.  This namespace helps with CSS scope to ensure our styles are unique to this and this component only.
* In line 1, in addition to the component's class of **hero** we are writing a conditional statement to determine if there is a value being passed for the modifier (`{{ modifier ? '  ' ~ modifier }}`), and if so, we are printing it as an additional CSS class.
* Still in line 1, we are preparing this component for when we integrate it with Drupal by assigning a placeholder for any Drupal attributes that may be available.  We will make use of `attributes` later in the process.
* For each field we want to print, we first check if there is content to print using a Twig conditional statement (`if`).  This is a good practice so we don't print empty HTML tags.
* Notice how every field and div uses a css class that starts with `hero__*`. Defining relationships between the parent elements and child elements by using the same namespace (hero\_\_), makes it easier to identify elements when inspecting code as well as finding those elements in our project.
* **Lastly, and super important**, we make use of Twig's `include` statement to include or nest the Heading and Button components into the Hero. This is extremely powerful and we will be talking more about it later.  Biggest benefit of include statements is that we can reuse other components to avoid duplicating code.

### Component's styles

1. Inside the _hero_ folder create a new file called **hero.scss**
2. Inside `hero.scss` add this code:

{% tabs %}
{% tab title="hero.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.hero {
  @include component-spacing;
  @include image-crop (320px);
  margin-bottom: 0;

  @media screen and (min-width: $bp-sm) {
    height: 400px;
  }

  @media screen and (min-width: $bp-md) {
    height: 600px;
  }

  @media screen and (min-width: $bp-xl) {
    height: 700px;
  }

  // Styles heading when inside the hero.
  .heading {
    color: $color-navy-blue;
    font-size: 6rem;
    font-weight: 900;
    margin-bottom: 10px;
    text-transform: uppercase;

    @media screen and (min-width: $bp-md) {
      font-size: 8rem;
      margin-bottom: 25px;
    }

    @media screen and (min-width: $bp-lg) {
      font-size: 10rem;
      margin-bottom: 25px;
    }

    @media screen and (min-width: $bp-xl) {
      margin-bottom: 50px;
      font-size: 12rem;
    }
  }
}

.hero__content {
  @include center-align(absolute);
  text-align: center;
  width: 100%;
}

.hero__media {

  // Fixes drupal bug with position property when
  // rendering image in drupal.
  .contextual-region {
    position: unset;
  }
}

```
{% endtab %}
{% endtabs %}

We'll refine these styles later on.

### Compiling the code

If Pattern Lab is running you should see the Hero component in Pattern Lab under the Component menu item. Otherwise run the commands below:

```
npm run watch
```

{% hint style="info" %}
**TIP:** Since we created a whole new component; if you had the watch task running, you may need to stop it by pressing **Ctrl + C** on your keyboard, and run `npm run build`. This will ensure the new component will be generated and all related code will be compiled.
{% endhint %}

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Hero component under components.
