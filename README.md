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
