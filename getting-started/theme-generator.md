# Mediacurrent Theme Generator

In a fast moving industry like ours, it is imperative that we have tools that allow us to build environments \(front and back-end\), quickly while providing consistency. The same way we have DevOps processes for quickly spinning off a complete Drupal website built with composer, drush, Drupal console and more, we need a system that automates the Drupal theme creation process in an effort to provide all the essential tools needed for a modern, best practices, and standards compliant front-end environment.

The [Mediacurrent's theme generator](https://github.com/mediacurrent/theme_generator_8) is a scaffolding tool which has evolved with the years to provide a production-ready Drupal 8 theme that is component-based ready out of the box.

## Working with the theme generator

The repo below provides all the instructions for getting, running and working with the Theme Generator.  Here are the basic steps for creating a Drupal 8 theme:

* Install NVM, NodeJS, & NPM
* In your Drupal 8 site, create a new directory for your theme \(i.e. `/themes/custom/my_awesome_them`\)
* Inside **my\_awesome\_theme** \(or any whatever directory name you created, type the following command:

```bash
nvm install node && node -v > .nvmrc
```

_The command above will install the latest stable version of NodeJS and create a new file in your project called `.nvmrc` where that version of Node will be declared as the default version for this project._

* Run the following command:

```bash
npm create yo mc-d8-theme
```

This command will begin the process to create your new theme.  Follow the on-screen instructions.

{% hint style="warning" %}
**WARNING:**  The theme's machine name should always match the directory you created on the first step above.
{% endhint %}

* After the theme has been successfully created, type the following commands:

```bash
npm install

npm run build && npm run watch
```

* Click the URL provided at the end of the last command's output \(http://localhost:3000\), to access Pattern Lab.

If you wish to access Pattern Lab using Drupal's URL, use the following path:

* http://**&lt;drupal-url&gt;**/themes/custom/**&lt;theme-name&gt;**/patternlab/index.html

_Update &lt;drupal-url&gt; and &lt;theme-name&gt; to match your environment_.

## Resources

Project: [https://github.com/mediacurrent/theme\_generator\_8](https://github.com/mediacurrent/theme_generator_8)

