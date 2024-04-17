# Title Component

Following the [Atomic Design ](https://bradfrost.com/blog/post/atomic-web-design/)methodology we are going to build a simple component or pattern. The Title pattern is an atom which prints a string of text as the title for a page, paragraph, or other component.

As we saw in the [Component Architecture](https://github.com/mariohernandez/training/tree/fca41f8d153f177c347617210b4e3e2fbc4bcc0b/components/essentials/untitled-3.md) page, most components will need the following files:

| File type         | Purpose                         |
| ----------------- | ------------------------------- |
| `.twig`           | Component's HTML and Twig logic |
| `.css`            | Component's styles              |
| `.yml`            | Component's stock content       |
| `.stories.jsx`    | Storybook story                 |

Some components may also include:

| File type | Purpose                                  |
| --------- | ---------------------------------------- |
| `.js`     | Component's interactive behavior         |
| `.mdx`    | Component's annotations or specs details |

## Exercise: Building the Title component

### Component's stock content

Let's start by first identifying the content for the component. Since this is a title field, we only need a string of text. We'll dive into more complex components in future exercises.

{% hint style="info" %}
**NOTE:** All components will be created inside `src/patterns/components`.

On a typical Drupal project the full path may look something like this: `<project-root>/web/themes/custom/<your-theme-name>/src/patterns/components/`
{% endhint %}

1. Inside _components_ create a new folder called **title**
2. Inside the _title_ folder create a new file called **title.yml**
3. Inside _title.yml_ add the following code:

```yml
---
title: 'Component-driven development with Storybook'
```

We just created key/value pair for the title with a key of **title** and **value** of _Welcome to the best training workshop!_.

### Component's Markup

Now let's write some HTML to be able to see the title component in the browser.

1. Inside the _title_ folder create a new file called **title.twig**
2. Inside `title.twig` add the following code:

```php
<h1 class="title">{{ title }}</h1>
```

We created a **h1** title in which we pass the value of title from the `json` file.

### Component's styles

We don't need to write any CSS for this component, but let's at least create a Sass file for when we need to write styles.

1. Inside the _title_ folder create a new file called **title.scss**
2. Inside `title.scss` add this code:

```css
// Import site utilities
@import '../../global/utils/init';

.title {
  color: $color-gray;

  &.center {
    text-align: center;
  }

  &.section-header {
    margin-bottom: 20px;

    @media screen and (min-width: $bp-lg) {
      margin-bottom: 40px;
    }
  }

  // Styles for extra large titles.
  &.title--large {
    color: $color-gray;
    font-size: 3rem;
    text-align: center;

    @media screen and (min-width: $bp-sm) {
      font-size: 4rem;
    }

    @media screen and (min-width: $bp-md) {
      font-size: 6rem;
    }
  }
}

// Removes underline when titles are links.
.title a {
  text-decoration: none;
}
```

* First we import the theme's utilities so we have access to any Sass variables, mixins, breakpoints, etc.  We will do this with every new stylesheet we create.
* The remaining code are styles for the title which include styles for when we need to style titles differently.  More on this later.

### Compiling the code

Now that the title component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

The **build** command above compiles all scss, twig and js. files, and should build the new title component in Pattern Lab. The **watch** command watches for changes to your code and automatically compiles them. This is great so you don't have to keep compiling your code every time.

At the bottom of the watch command you will notice a list of URLs. In your browser of choice open the following url: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the title pattern under components.
