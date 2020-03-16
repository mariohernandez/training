# Drupal Libraries

In a Drupal 8 theme, stylesheets \(CSS\) and JavaScript \(JS\) are loaded through the same system for modules \(code\) and themes, for everything: [asset libraries](https://www.drupal.org/node/2274843).

Drupal uses a high-level principle: assets \(CSS or JS\) are still only loaded if you tell Drupal it should load them. Drupal does not load all assets on every page because it slows down front-end performance.

​[Learn more about Drupal libraries.](https://www.drupal.org/docs/8/theming-drupal-8/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-theme)​

In the context of component-based theming, we are going to create a library for each individual component we build. Each library will have all the CSS and Javascript \(if any\), the component needs to render as expected.

{% hint style="info" %}
**Drupal libraries are only intended to work in Drupal**. They have no effect in Pattern Lab. In Pattern Lab we use Gulp tasks to make the CSS and Javascript we write for components.
{% endhint %}

### Structure of a library

In your editor, open `theme_name.libraries.yml` \(located in your theme's root\). You will notice the global library already declared which includes all of the global theme styles that apply to all pages on the site \(i.e. font color, font-size, font-family, line-height, etc.\). The global library looks something like this:

```yaml
global:  
  css:    
    base:      
      dist/css/global.css: {}
```

1. **Library name**: In our case this name will always be the name of our component to easily identify what a library is for.
2. **Asset**: The asset we want to include in the library. Usually `css` and/or `js`.
3. **Loading ordering**: Ordering category, in this case `base`, is loaded before other categories. Drupal 8 loads stylesheets based on the [SMACSS](https://smacss.com/) ordering: `base`, `layout`, `component`, `state`, and `theme`. All of the components we create will use the `component` ordering.
4. **The path**: The path to the asset relative to the root of the theme. All assets in our theme are compiled into `dist/css` or `dist/js`. 

### Creating a new library for the Hero component

Let's write a new Drupal library for the Hero component so we can apply all css we've written for it in Drupal.

* Open `theme_name.libraries.yml` in your editor
* Copy and paste a the bottom of the file the code above from the Global library
* Modify the code to look like this:

```text
hero:  
  css:    
    component:      
      dist/css/hero.css: {}
```

There is a lot more to Drupal libraries and we encourage you to learn more about them in the URL above.

Libraries are great because Drupal only loads what we need when we need it to avoid having to load assets that our page or component may never use. This helps with the site's performance.

#### **Clear Drupal's cache**

Don't forget to clear your caches when adding new libraries to your theme.

* Use the admin menu to flush all caches
* Or if you have Drush setup, run this command:

```text
drush cr
```

### Attaching a library

Now that the Hero component's library is ready, we need to make Drupal aware of it so it can use it.

1. In your editor, open `src/patterns/components/hero/hero.twig`
2. Edit the file by adding the following code at the first line in the file:

```text
{{ attach_library('theme_name/hero') }}
```

The `attach_library` function takes a path parameter which we are declaring by using the theme's namespace \(the namespace is created by the [Components Libraries module](https://www.drupal.org/project/components)\), then the name of the library we want to attach \(i.e. `theme_name/hero`\).

With the code above, we are telling Drupal that whenever we render the Hero component, its library should be attached so the styles for the component can be applied.

## Creating libraries for each component <a id="creating-libraries-for-each-component"></a>

From now on for every new component we create in Pattern Lab, we are going to create a new library for it.  In addition, we are going to attach the new library to the corresponding component.  As I mentioned before, libraries have no effect . in Pattern Lab, but it is a good practice to create and attach a component's library while you are working on it as it can be easy to forget to do it later.

{% hint style="info" %}
**More on Drupal Libraries:** Mediacurrent's Director of Front-End Development, Zack Hawkins, explains libraries in detail: [https://www.youtube.com/watch?v=V8hnfxSx4Ck](https://www.youtube.com/watch?v=V8hnfxSx4Ck)
{% endhint %}

