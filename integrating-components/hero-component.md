# Hero Component

### What is component integration?

At a high level, component integration is making Drupal aware of components in Pattern Lab and passing Drupal data to the components. By default Drupal has no knowledge of any components in Pattern Lab, but through the use of Presenter templates, we can wire components so they get rendered in Drupal, using Drupal data, while using Pattern Lab as the single source of markup, css and javascript.

### Twig debugging

Before we can begin integrating components we need to turn on Twig debugging in Drupal.  This will allow us to identify the right Drupal templates we need to work with to integrate the hero and other components.

### Drupal entities

Typically in a component-based project, Drupal will use entities to build component equivalents in the back end.  Entities such as nodes, blocks, paragraph types, and even views, are great for building the infrastructure of a component in Drupal's back-end.

In the case of the Hero component, the Drupal equivalent could be a custom block or a paragraph type.  Either one would need to be build in drupal with the same fields the Hero component needs.  For the purpose of this exercise we will use a paragraph type called Hero.

### Template suggestions

[Template suggestions](https://www.drupal.org/docs/8/theming/twig/working-with-twig-templates) are copies of Drupal core or contrib modules templates. Template suggestions are saved in your theme's `/templates` directory. This is where Drupal knows to look for twig templates when rendering content. If it finds twig templates it uses those over the ones in core when rendering content.  Template suggestions are what we will use to integrate components with Drupal.  These template suggestions in the context of component integration, are typically referred to as **Presenter Templates**.

#### Naming template suggestions

If you have been using Drupal for a while you may be well familiar with where to get templates from or what to name them. However if you've never worked with template suggestion no worries, Twig debugging, which we enabled above, will help us identify the templates we need.

* In your Drupal site, visit a page where a hero is rendered.
* Right-click anywhere over the hero and select **Inspect**  or **inspect element**, depending on your browser.  This will display the page's HMTL that makes up the page you are currently viewing.  See the screenshot below:

&lt;insert image here&gt;

If you look at the screenshot above, you will see a few things that are extremely helpful for creating the right template suggestions.

* The last line of the green text \(`BEGIN OUTPUT...`\) shows where the template being used to render the movie node is located and what its name is. **Note:** The screenshot above demonstrates how to find the template within the Drupal core theme. The node template we want has already been placed into the correct location for the `nitflex_dev_theme` theme, so you should see a path to that theme.
* Just above that line, there is a list of files all of which begin with **node--**. This list is what we mean when we say _Template suggestions_.
* The file name with an **"x"** to the left of it is the template Drupal is currently using to render the movie node.

