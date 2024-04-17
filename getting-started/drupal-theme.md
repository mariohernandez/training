# Drupal theme

For this training we need a custom theme that includes Storybook.  In the interest of time, I have written about creating a Drupal 10 theme with Storybook so rather than having you go through that process, you can simply download/clone the pre-built Storybook theme.

## Tooling

The Drupal theme is a brand new theme using some of the latest tools out there. These tools include:

* Storybook
* ViteJS
* NodeJS
* NPM
* PostCSS
* Twig & TwigJS
* React

## Grabbing the theme

1. Create a new Drupal 10 website. [I recommend using DDEV](https://ddev.readthedocs.io/en/stable/users/quickstart/#drupal).
1. In your new Drupal site, [clone or download the Storybook repo](https://github.com/mariohernandez/storybook) into **/web/themes/custom/**. The theme name used in this training is **storybook**, keep this in mind if you decide to change the theme name.

## Building and using the theme

**Note**: You need [NodeJS 19](https://nodejs.org/en/download) or higher as well as [NVM](https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide/)

1. In your command line navigate into **web/themes/custom/storybook/**
1. Run `nvm install`: It will install the node version specified in `.nvmrc`
1. Run `npm install`: It will install all the node packages found in `package.json`
1. Run `npm run build`: It will build your theme and generate the necessary static assets like CSS and JS
1. Run `npm run storybook`: It will build the theme and launch Storybook in your browser using port 6006.
