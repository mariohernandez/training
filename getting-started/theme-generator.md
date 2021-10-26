# Create a new D9 theme

### Mediacurrent Theme Generator

The [Mediacurrent theme generator](https://github.com/mediacurrent/theme\_generator\_8) is a scaffolding tool that has evolved with the years to provide a production-ready Drupal 8 theme that is component-based ready out of the box.

## Exercise:  Create a new D9 theme

[Watch the video tutorial,](https://www.youtube.com/watch?v=cVyA2v-UwSQ\&feature=youtu.be) or follow the instructions below.

1. In your Drupal 8 site, create a new folder for your theme (i.e. `/themes/custom/training_theme`).  Although you can use any name you wish, all exercises in this curriculum use **training\_theme**.
2. In your command line app, change into the newly created directory (**training\_theme**),  type the following command and press **Return**:

```bash
nvm install 14.16.1 && node -v > .nvmrc
```

_The command above will install the NODEJS \`14.16.1\` and create a new hidden file in your project called `.nvmrc` where that version of Node will be declared as the default version for this project._

* Next run this command:&#x20;

```
npm install -g npm@6.14.12
```

The theme generator is compatible with NPM 6.

* Run the following command:

```bash
npm create yo mc-d8-theme
```

#### Respond to the on-screen prompts as follows:

1. Assign a Human readable name to your theme
2. **IMPORTANT:** When the **What is your theme's machine name?** question comes up, be sure it matches the name of the directory you created above (i.e. `training_theme`).
3. Type a description for your theme
4. Select **Use stable** **as your base theme**
5. Type **Y** and press **Return** when **Should we update the .gitignore to ignore compiled files?** comes up.  This will hide `/dist` from git to avoid having to commit already compiled files.
6. While you can select any demo components from the list, we recommend the following ones:
   1. Drupal Messages
   2. Drupal Tabs

{% hint style="warning" %}
**WARNING:** The theme's machine name should always match the directory you created in the first step above (i.e. `training_theme`).
{% endhint %}

* After the theme has been successfully created, type the following commands from the theme's root:

```bash
npm run build

npm run watch
```

* Click the URL provided at the end of the last command's output ([http://localhost:3000\\](http://localhost:3000)), to access Pattern Lab.

If you wish to access Pattern Lab using Drupal's URL, use the following path:

* [https://drupaltraining.ddev.site/themes/custom/training\_theme/patternlab/index.html](https://drupaltraining.ddev.site)&#x20;

_If you don't have HTTPS enabled, use HTTP in the url above._

## Resources

Project: [https://github.com/mediacurrent/theme\_generator\_8](https://github.com/mediacurrent/theme\_generator\_8)
