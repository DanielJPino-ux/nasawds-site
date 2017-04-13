---
permalink: /getting-started/developers/
layout: styleguide
title: For developers
category: Getting started
lead: The UI components are built on a solid HTML foundation, progressively enhanced to provide core experiences across browsers. All users will have access to the same critical information and experiences regardless of what browser they use, although those experiences will render better in newer browsers. If JavaScript fails, users will still get a robust HTML foundation.
subnav:
- text: Installation
  href: '#installation'
- text: CSS architecture
  href: '#css-architecture'
- text: Customization
  href: '#customization-and-theming'
- text: Where things live
  href: '#where-things-live'
- text: Accessibility
  href: '#notes-on-accessibility'
- text: Contributions
  href: '#contribution-guidelines'
---

## Installation

Here are a few different ways to use the Standards within your project.

### Download

To use the Web Design Standards on your project, you’ll need to include the CSS and JavaScript files in each HTML page in your project.

First, download the Web Design Standards assets:

<a class="link-download" href="https://github.com/bruffridge/web-design-standards/releases/download/v{{ site.version }}-nasa/nasawds-{{ site.version }}.zip">Download code</a>
<span class="link-download-subtext">Version {{ site.version }}</span>

Then, add the following folders into a relevant place in your code base — likely a directory where you keep third-party libraries:

```
nasawds-{{ site.version }}/
├── js/
│   ├── nasawds.min.js.map
│   ├── nasawds.min.js
│   └── nasawds.js
├── css/
│   ├── nasawds.min.css.map
│   ├── nasawds.min.css
│   └── nasawds.css
├── img/
└── fonts/
```

Refer to these files by adding the following `<link>` and `<script>` elements
into your HTML pages:

Add this to your `<head>` element:

```html
<link rel="stylesheet" href="/path/to/your/assets/css/lib/nasawds.min.css">
```

Add this before the closing `</body>` tag:

```html
<script src="/path/to/your/assets/js/lib/nasawds.min.js"></script>
```

We offer two versions — a minified version, and an un-minified one. Use the minified version in a production environment or to reduce the file size
of your downloaded assets. And the un-minified version is better if you are in a
development environment or would like to debug the CSS or JavaScript assets in
the browser. The examples above recommend using the minified versions.

And that’s it — you should be set to use the Standards.

### Using npm

Note: Using npm to install the Standards will include jQuery version `2.2.0`. Please make sure that you’re not including any other version of jQuery on your page.

If you have `node` installed on your machine, you can use npm to install the Standards. Add `nasawds`
to your project's `package.json` as a dependency:

```shell
npm install --save nasawds
```

The package will be installed in `node_modules/nasawds`. You can use the un-compiled files
found in the `src/` or the compiled files in the `dist/` directory.

```
node_modules/nasawds/
├── dist/
│   ├── css/
│   ├── fonts/
│   ├── img/
│   ├── js/
└── src/
    ├── fonts/
    ├── img/
    ├── js/
    └── stylesheets/
```

`require('nasawds')` will load all of the NASA GRC Web Design Standard's JavaScript onto the page. The `nasawds` module itself does not export anything.

The main Sass (SCSS) source file is here:

```
node_modules/nasawds/src/stylesheets/nasawds.scss
```

The non-minified CSS that’s been precompiled is here:

```
node_modules/nasawds/dist/css/nasawds.css
```

### Using another framework or package manager

If you’re using another framework or package manager that doesn’t support NPM, you can find the source files in this repository and use them in your project. Otherwise, we recommend that you follow the [download instructions](#download). Please note that the core team [isn’t responsible for all frameworks’ implementations](https://github.com/18F/web-design-standards/issues/877).


### Need installation help?

Do you have questions or need help with setup? Did you run into any weird errors while following these instructions? Feel free to open an issue here:

[https://github.com/bruffridge/web-design-standards/issues](https://github.com/bruffridge/web-design-standards/issues).

You can also email us directly at grc-webteam@lists.nasa.gov.

## CSS architecture

* The CSS foundation of this site is built with the **[Sass](https://sass-lang.com)** preprocessor language.
* Uses **[Bourbon](http://bourbon.io/)** for its simple and lightweight Sass mixin library, and the **[Neat](http://neat.bourbon.io/)** library for the grid framework. Bourbon and Neat are open-source products from **[thoughtbot](https://thoughtbot.com/)**.
* The CSS organization and naming conventions follow **[18F’s CSS Coding Styleguide](https://pages.18f.gov/frontend/css-coding-styleguide/)**.
* CSS selectors are **prefixed** with `usa` (For example: `.usa-button`).
* Uses a **[modified BEM](https://pages.18f.gov/frontend/css-coding-styleguide/naming/)** approach created by 18F for naming CSS selectors. Objects in CSS are separated by single dashes. Multi-word objects are separated by an underscore (For example: `.usa-button-cool_feature-active`).
* Uses **modular CSS** for scalable, modular, and flexible code.
* Uses **nesting** when appropriate. Nest minimally with up to two levels of nesting.
* Hard-coded magic numbers are avoided and, if necessary, defined in the `core/variables` scss file.
* Media queries are built **mobile first**.
* **Spacing units** are as much as possible defined as rem or em units so they scale appropriately with text size. Pixels can be used for detail work and should not exceed 5px (For example: 3px borders).

**For more information, visit:
[https://pages.18f.gov/frontend/css-coding-styleguide/](https://pages.18f.gov/frontend/css-coding-styleguide/)**


## Customization and theming

The Standards can be customized to use different typography, colors and grid systems. The easiest way to do this is to use Sass and override the Standards’ global variables. If it isn’t possible to use Sass, do theming by overriding the CSS rules in the Standards set.

To start theming through Sass, copy the `core/variables` file into your own project’s Sass folder, changing applicable variable values, and importing it before the WDS. Below is an example of customizing the import of the Standards all.scss file.

```scss
// src/main.scss
@import 'path/to/my/scss/files/main/scss/my-custom-vars';
@import 'lib/nasawds/src/stylesheets/all';
```

```scss
// path/to/my/scss/files/main/scss/my-custom_vars.scss

// Colors
$color-primary: #2c3e50;
$color-secondary: #ad2020;
$color-secondary-dark: #b0392e;

// Typography
$font-serif: 'Georgia', 'Times', serif;
$h2-font-size: 2rem;
$h3-font-size: 1.75rem;
$heading-line-height: 1.4;

// Grid/breakpoints
$small-screen:  540px !default;
$medium-screen: 620px !default;
$large-screen:  1120px !default;
```

NOTE: If you plan on upgrading to newer versions of the Standards in the future, or are not using your own forked version of the Standards, try to avoid making changes in the Standards folder themselves. Doing so could make it impossible to upgrade in the future without undoing your custom changes.

### Main variables that can be customized
* Colors can be found in the `core/variables` [file, line 35](https://github.com/18F/web-design-standards/blob/develop/src/stylesheets/core/_variables.scss#L35).
* Font families can be found in the `core/variables` [file, line 28](https://github.com/18F/web-design-standards/blob/develop/src/stylesheets/core/_variables.scss#L28).
* Typography sizing can be found in `core/variables` [file, line 13](https://github.com/18F/web-design-standards/blob/develop/src/stylesheets/core/_variables.scss#L13).
* Grid and breakpoint settings can be found in `core/variables` [file, line 87](https://github.com/18F/web-design-standards/blob/develop/src/stylesheets/core/_variables.scss#L87).


## Where things live

* **HTML** markup for the components is located in: `src/html` in the site root.
* **Sass** styles are located in: `src/stylesheets/ (/core, /elements, /components)`. **Compiled CSS** is located in the [downloadable zip file]({{ site.repos[0].url }}/releases/download/v{{ site.version }}/nasawds-{{ site.version }}.zip) .
* **JS** is located in: `src/js/components (accordion.js, toggle-field-mark.js, toggle-form-input.js, validator.js)`.
* **Fonts** are located in: `src/fonts`.
* **Images** and icons are located in: `src/img`.

## Notes on accessibility

We’ve designed the Standards to support older and newer browsers through progressive enhancement, and they officially support Internet Explorer 9 and up, along with the latest versions of Chrome, Firefox, and Safari. Internet Explorer 8 and below generally see very low usage, and most agency websites should be able to safely begin support at Internet Explorer 9.

The Standards also meet the [WCAG 2.0 AA accessibility guidelines](https://www.w3.org/TR/WCAG20/) and are compliant with [Section 508 of the Rehabilitation Act](http://www.section508.gov/). We’re happy to answer questions about accessibility — email us for more information.
