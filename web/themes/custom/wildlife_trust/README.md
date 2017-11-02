# Using the Wildlife Trust theme

## Theme setup

This theme requires CTI Digitial's Jackdaw base theme to work correctly.

To compile the theme you will need:
* [Node.js](https://nodejs.org/en/)
* [Node Package Manager (npm)](https://www.npmjs.com/)
* [Bower](http://bower.io/) - A package manager we use for Javascript libraries.

To generate a Wildlife Trust theme from scratch:

1. Enable Jackdaw as the default theme (temporary, required to run the Drush commands)
2. Using Drush, run either:
  * `drush jwiz` - And follow the wizard
  * `drush jsub "Your Theme Name"` - to use the default settings

### Retrieving JS libraries, node modules and compiling the theme
1. Run `bower install` to retrieve the javascript libraries we might need.
2. Run `npm install` to install all the packages we will need for Grunt to work
3. Grunt tasks (see grunt/aliases.yml to see individual tasks run):
  * Production: `grunt` - The default task, compiles the theme to make it Production ready.
  * Development: `grunt dev` - Compiles the theme for use in development
  * Watcher: `grunt watcher` - Compiles the theme and watches for changes. Useful for ongoing theme development.
  * Docs: 'grunt docs' - Compile the in-theme documentation: SASSDocs and KSS.
  
When beginning work on a new project, the Gruntfile's (Gruntfile.js in the theme root) defaultConfig will need updating to add the site's URL:
```javascript
var defaultConfig = {
  localUrl: 'national.wt.v.ctidigital.com'
};
```

## Generated assets
The following folders in the theme root are generated by running the grunt tasks (1-3) outlined above:
* `css` - Generated from the `sass` folder (see `grunt/sass.js`, `grunt/sass_globbing.js` and `grunt/postcss.js`)
* `icons` - Generated from the `assets/icons` folder (see `grunt/svgmin.js` and `grunt/grunticon.js`)
* `images` - Generated from the `assets/images` folder (see `grunt/imagemin.js`)
* `js` - Generated from the `assets/js` folder (see `grunt/jshint.js` and `grunt/uglify.js`)

You should not be manually placing anything in to these folders as they are removed at the beginning of each grunt task run via the `clean` task.

The `libraries` folder is populated during `bower install`.

## Colour schemes
Colour schemes can be created in the theme that will be automatically picked up by the theme. They can be created via the following steps (in all cases, replace COLOUR with the name of your colour scheme):

1. Add a new colour scheme in the `sass` root, e.g. `wildife_trust.COLOUR.styles.scss` containing the following code:
  ```scss
    // Import external libraries.
    @import '_external';
    
    // Set the palette.
    @import 'palettes/_COLOUR';
    
    // Import core, base styles and components.
    @import '_internal';
  ```
  
2. Inside `sass/palettes` create your colour scheme, e.g. _COLOUR.scss containing the following code:
```scss
@import '_core';

$COLOUR_palettes: (
  // Theme Palette colours.
  primary: (
    base: #0079c8
  ),
  secondary: (
    base: #6ec3df
  ),
);

$palettes: map-merge($core_palettes, $COLOUR_palettes);
```

3. Add the colour scheme as a library to wildlife_trust.libraries.yml:
```yaml
colours-COLOUR:
  css:
    theme:
      css/wildlife_trust.COLOUR.styles.css: {}
```

4. Add an image palette for the colour scheme in the `colour_schemes` folder. This should be 100 x 50 with a 50 x 50 square for the primary and secondary colour.





