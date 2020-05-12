# Create a new D8 theme

### Mediacurrent Theme Generator

The [Mediacurrent theme generator](https://github.com/mediacurrent/theme_generator_8) is a scaffolding tool that has evolved with the years to provide a production-ready Drupal 8 theme that is component-based ready out of the box.

## Exercise:  Create a new D8 theme

The instructions below will get you up and running with the Theme Generator:

1. In your Drupal 8 site, create a new directory for your theme \(i.e. `/themes/custom/training_theme`\)
2. In your command line app, change into the newly created directory \(**training\_theme**\),  type the following command and press **Return**:

```bash
nvm install node && node -v > .nvmrc
```

_The command above will install the latest stable version of NodeJS and create a new hidden file in your project called `.nvmrc` where that version of Node will be declared as the default version for this project._

* Run the following command:

```bash
npm create yo mc-d8-theme
```

#### Respond to the on-screen prompts as follows:

1. Assign a Human readable name to your theme
2. **IMPORTANT:** When the **What is your theme's machine name?** question comes up, be sure it matches the name of the directory you created in step 1 above \(i.e. `training_theme`\).  By default the system will try to use a similar name to the human readable name, but you need to make sure you type the name of the directory you created or you will run into issues in Drupal.
3. Type a description for your theme
4. Select **Use stable** **as your base theme**
5. Type **Y** and press **Return** when **Should we update the .gitignore to ignore compiled files?** comes up.  This ensures already committed/compiled code does not keep showing as modified every time code gets compiled.
6. While you can select any demo components from the list, select the followings to start with \(use your space bar to select an item and up/down arrows to move through the list\):
   1. Button
   2. Eyebrow
   3. Drupal Messages
   4. Drupal Tabs

{% hint style="warning" %}
**WARNING:**  The theme's machine name should always match the directory you created in the first step above \(i.e. `training_theme`\).
{% endhint %}

* After the theme has been successfully created, type the following commands:

```bash
npm run build

npm run watch
```

* Click the URL provided at the end of the last command's output \(http://localhost:3000\), to access Pattern Lab.

If you wish to access Pattern Lab using Drupal's URL, use the following path:

* http://**&lt;drupal-url&gt;**/themes/custom/**training\_theme**/patternlab/index.html

_Update **&lt;drupal-url&gt;** and **training\_theme** to match your environment_.

## Resources

Project: [https://github.com/mediacurrent/theme\_generator\_8](https://github.com/mediacurrent/theme_generator_8)

