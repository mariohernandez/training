# Heading Component

Following the [Atomic Design ](https://bradfrost.com/blog/post/atomic-web-design/)methodology we are going to build a simple component or pattern. The Heading pattern is an atom which prints a string of text as the title for a page, paragraph, or other component.

As we saw in the [Component Architecture](https://github.com/mariohernandez/training/tree/fca41f8d153f177c347617210b4e3e2fbc4bcc0b/components/essentials/untitled-3.md) page, most components will need the following files:

| File type | Purpose |
| :--- | :--- |
| `.twig` | Component's HTML and Twig logic |
| `.scss` | Component's styles |
| `.json` or `.yml` | Component's stock content |

Some components may also include:

| File type | Purpose |
| :--- | :--- |
| `.js` | Component's interactive behavior |
| `.md` | Component's annotations or specs details |

## Building the component

### Component's stock content

Let's start by first identifying the content for the component. Since this is a title field, we only need a string of text. We'll dive into more complex components in future exercises.

{% hint style="info" %}
**NOTE:** All components will be created inside `src/patterns/components`

On a typical Drupal project the full path may look something like this: `<drupal-root>/web/themes/custom/<your-theme-name>/src/patterns/components/`
{% endhint %}

1. Inside _components_ create a new directory called **heading**
2. Inside the _heading_ directory create a new file called **heading.json**
3. Inside _heading.json_ add the following code:

{% tabs %}
{% tab title="heading.json" %}
```yaml
{
  "title": "Welcome to the best training workshop!"
}
```
{% endtab %}
{% endtabs %}

We just created key/value pair for the heading with a key of **title** and **value** of _Welcome to the best training workshop!_.

### Component's Markup

Now let's write some HTML to be able to see the Heading component in the browser.

1. Inside the _heading_ directory create a new file called **heading.twig**
2. Inside `heading.twig` add the following code:

{% tabs %}
{% tab title="heading.twig" %}
```php
<h1 class="heading">{{ title }}</h1>
```
{% endtab %}
{% endtabs %}

We created a **h1** heading in which we pass the value of title from the `json` file.

### Component's styles

We don't need to write any CSS for this component, but let's at least create a Sass file for when we need to write styles.

1. Inside the _heading_ directory create a new file called **heading.scss**
2. Inside `heading.scss` add this code:

{% tabs %}
{% tab title="heading.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';
```
{% endtab %}
{% endtabs %}

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass. More on this later.

## Compiling the code

Now that the Heading component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

The **build** command above compiles all scss, twig and js. files, and should build the new Heading component in Pattern Lab. The **watch** command watches for changes to your code and automatically compiles them. This is great so you don't have to keep running commands every time you make a change.

At the bottom of the watch command you will notice a list of URLs. In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Heading pattern under components.

