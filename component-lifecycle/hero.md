# Hero Component

The Hero component is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the Hero we will reuse other components by using twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the Hero component.

First let's take a look at how this component looks so we can identify the different data fields we need.

![](../.gitbook/assets/hero.png)

Based on the design above, we need the following fields:

* **title or heading**: Hero titl
* **image**: Hero image
* **call to action \(CTA\)**: A call to action button/link

## Exercise:  Build the Hero component

### Component's stock content

1. Inside _components_ create a new directory called **hero**
2. Inside the _hero_ directory create a new file called **hero.json**
3. Inside _hero.json_ add the following code:

{% tabs %}
{% tab title="hero.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/FIKD9t5_5zQ/1400x787' alt='A wonderful image' />",
  "eyebrow": "Understanding the benefits",
  "heading": {
    "heading_level": "1",
    "modifier": "hero__title",
    "title": "Why be accessible",
    "url": ""
  },
  "body_text": "Accessibility lawsuits have more than tripled in the last few years, but it's not all bad news!",
  "cta": {
    "text": "More about accessibility?",
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

* The `eyebrow` `heading` and `cta` fields were declared as JSON objects with `key|value`properties within them.  Typically these object's data structure matches the original components.  For example, if you look at the data structure for the **Heading** component you will see it is the same as what we have here in the Hero.  When component's data structures match it makes it easier to nest components into other components.  More on this later.
* Almost all the fields provide the ability to add a `modifier` css class \(i.e. `hero__*`\).  This is handy because it establishes a relationship between child and parent elements \(using the [BEM](https://css-tricks.com/bem-101/) methodology\), but it also facilitates styling those elements differently than the original components.

### Component's Markup

Now let's write some HTML for the component.

1. Inside the _hero_ directory create a new file called **hero.twig**
2. Inside `hero.twig` add the following code:

{% tabs %}
{% tab title="hero.twig" %}
```php
<section class="hero{{ modifier ? ' ' ~ modifier }}{{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% if image %}
    <div class="hero__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="hero__content">
    {% if eyebrow %}
      <div class="hero__eyebrow">
        {{ eyebrow }}
      </div>
    {% endif %}
    {% if heading %}
      {%
        include '@training_theme/heading/heading.twig' with {
          "heading": heading
        } only
      %}
    {% endif %}

    {% if body_text %}
      <div class="hero__body-text">
        {{ body_text }}
      </div>
    {% endif %}

    {% if cta %}
      <a href="{{ cta.url }}" class="hero__cta">
        {{ cta.text }}
      </a>
    {% endif %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
In the interest of addressing the basics of component-building, we are going to ignore for now  Drupal-specific elements found in line 1 above. We will discuss those elements as part of other exercises in this training.
{% endhint %}

#### Some things to notice:

* We're starting off with a `<section>` HTML5 tag.  Learn more about the [section](https://www.w3schools.com/tags/tag_section.asp) tag.  This is the parent selector of the component and therefore it should be named **hero**.  We do this by using the class of `hero.`
* For each field we want to print, we first check if there is content to print using a Twig conditional statement \(`if`\).  This is a good practice so we don't print empty HTML.
* Notice how every field uses a css class that starts with `hero__*`. Defining relationships between the parent elements and child elements by using the same namespace \(hero\_\_\), makes it easier to identify elements when inspecting code as well as finding those elements in our project.
* **Lastly, and super important**, we make use of Twig's `include` statement to include or nest previously built components into the Hero. This is extremely powerful and we will be talking more about it later.  Biggest benefit of include statements is that we can reuse other components to avoid duplicating code.

### Component's styles

We'll skip styles for now, but let's at least create a Sass file for when we need to write styles.

1. Inside the _hero_ directory create a new file called **hero.scss**
2. Inside `hero.scss` add this code:

{% tabs %}
{% tab title="hero.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.hero {
  background-color: $color-white;
}

.hero__content {
  background-color: $color-white;
  margin: 0 auto;
  padding: 1.6rem;

  @include breakpoint ($bp-md) {
    position: absolute;
    left: 40px;
    top: calc(50% - 75px);
    width: 60%;
  }
}

.hero__body-text {
  font-weight: 300;
  margin-bottom: 20px
}

```
{% endtab %}
{% endtabs %}

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass. More on this later.

### Compiling the code

Now that the Hero component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

{% hint style="info" %}
**TIP:** Since we created a whole new component; if you had the watch task running, it is recommended you stop it by pressing **Ctrl + C** on your keyboard, and run the commands above.  This will ensure the new component will be generated and all related code will be compiled.
{% endhint %}

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Hero component under components.

