## Readme File.

[![Build Status](https://api.travis-ci.org/manuelitox/generator-modules.svg?branch=master)](https://travis-ci.org/manuelitox/generator-modules)

Generate stylesheets with Sass, using Maps and Mixins.

The documentation you can find in the [sassdoc/index.html](https://github.com/manuelitox/generator-modules/blob/master/sassdoc/index.html) file

### Install:

1. ```$ npm i generator-modules ```
2. Import to your project ```@import 'node_modules/generator-modules/sass/main' ```

### Example:

First, we will declare the attributes that we want have in the style sheet.

```sass
$box: (
	background-color: red,
	color: white,
	margin: 20px
)!default;

$box-pseudo-class: (
	hover: (
		background-color: yellow
	),
	last-of-type: (
		margin-bottom: 0
	)
) !default;

$box-active: (
	background-color: gray,
	color: black
) !default;
```

Now, We go to work with the generator:

```sass
@include gen-component('box') {
	@include gen-attribute(padding, 10px);
	@include gen-attributes($box);
	@include gen-pseudo-selectors($box-pseudo-class);
	@include gen-state('active', $box-active);
	@include gen-internal-component('header') {
		@include gen-attribute(color, red);
	}
}
```


#### This's the result:

```css
.box {
	padding: 10px;
	background-color: red;
	color: white;
	margin: 20px;	
}
.box:hover {
	background-color: yellow;
}
.box:last-of-type {
	margin-bottom: 0;
}
.box.active {
	background-color: gray;
	color: black;
}
.box-header {
	color: red;
}
```