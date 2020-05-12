# Local Setup

### Front-End tooling installation

1. Install **NVM** \([macOS](https://medium.com/@jamesauble/install-nvm-on-mac-with-brew-adb921fb92cc) or [Windows 10](https://www.youtube.com/watch?v=px9N1JOzRVU)\)
2. Install **NodeJS** & **NPM**.  You will do this when building the theme below.

### **Drupal 8**

Use one fo the options below to install Drupal 8.  Install the [latest Drupal 8 ](https://www.drupal.org/project/drupal/)release.

* [Acquia Dev Desktop](https://docs.acquia.com/dev-desktop/install/)
* You could also use [Lando](https://docs.lando.dev/basics/installation.html), [DDev](https://ddev.readthedocs.io/en/stable/#installation) or [Vagrant](https://www.vagrantup.com/intro/getting-started/install.html)

Regardless of which option you use to setup Drupal 8, the following modules need to be installed and enabled:

* [Components Libraries](https://www.drupal.org/project/components)
* [Paragraphs](https://www.drupal.org/project/paragraphs)
* [Entity Reference Revisions](https://www.drupal.org/project/entity_reference_revisions)
* [Devel & Kint](https://www.drupal.org/project/devel) \(both in same module\)
* [Admin toolbar and Admin toolbar Extras](https://www.drupal.org/project/admin_toolbar)
* [Twig Field Value](https://www.drupal.org/project/twig_field_value)
* [Focal Point](https://www.drupal.org/project/focal_point)
* [Crop API](https://www.drupal.org/project/crop)
* Responsive Images \(core\)
* Media & Media Library \(both on core\)

You also need the latest LTS versions of [NodeJS with NPM](https://nodejs.org/en/).  Ideally, if you can install NodeJS with [NVM](https://tecadmin.net/install-nodejs-with-nvm/) that would be preferred.

{% hint style="info" %}
**WINDOWS USERS**: Use Power Shell to run the commands in the instructions.
{% endhint %}

