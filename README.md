# DSB Bootstrap

## Install
Include DSB bootstrap in your project by adding `dsb-bootstrap` to the list of dependencies in your project. Something like this will probably do:

```sh
npm install --save dsb-bootstrap
```

By doing this you'll get both the compiled CSS-file and the SCSS files in your `node_modules` folder in a sub-folder called `dsb-bootstrap`.

## Using it
In order to use the style you need to either load the pre-compiled CSS in the browser, or compile and pack the `dsb-bootstrap` sass files together with the rest of you projects SCSS files. If you want to do so, your SCSS file will probably look a bit like this:

```scss
/*
Include DSB style
*/
@include 'node_modules/dsb-bootstrap/dsb-bootstrap';

/*
Your stuff below..
*/

body {
  background: green;
  color: pink;
}
```

## Developing

Clone this repo and install package dependencies:

```sh
npm install
```

### Icons
In order to build the icon font, `fontcustom` must be installed on your system. Follow the installation instructions on https://github.com/FontCustom/fontcustom.

When you have fontcustom, build the icon font by going to the root of the project and issuing the following command:

```sh
npm run icons
```

### Styles
After doing changes to `_dsb-bootstrap.scss` you can run `npm run build`
in order to write a new `style.css` to the `dist` folder.

## Release

When committing changes to the master branch of this repo, the CI-system
will run the build and release a new version of it to Nexus.

Thus, it will automatically run the following command:

```sh
npm version patch -m "Bump to version %s"
```

This will commit a new version of package.json, bumping the version.

This means that you should pull the latest changes after committing to
master.

Note that it's not necessary to run the build prior to committing 
changes to the repo. The build system will do this automatically, as
noted above.
 
