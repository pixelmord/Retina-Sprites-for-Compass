Retina Sprites for Compass
==========================

This is a fork from [Retina-Sprites-for-Compass by Gaya Kessler](https://github.com/Gaya/Retina-Sprites-for-Compass).

Modified the original mixin to be used with a single sprite folder/sprite map that contains regular images as well as their retina versions.

Allows you to use sprites in Compass with added retina variants. Works just like the normal sprite helpers, but has been made a lot easier with these mixins.

Take a look at the example to see the results.

##The problem:
You want your site to serve retina images to retina displays, but not to non-retina ones. This mixin / solution will make it very easy for you to use sprites and let Compass generate the mappings of the two different sizes.

Since we have to develop sites that serve retina images and background-images our sprites and background-image approaches might get a bit cluttered in our CSS. Using just one call, this mixin will know which image has to be served to the browser and will also resize it to show as if it was in your normal image dimentions.

##How to use:

First thing you'll need to do is to download the mixins and put them where your scss / sass files are located. Notice the underscore at the start of the filenames, this will prevent Compass from compiling these files to CSS.

1. Include the mixin in your SASS/SCSS file using:<br/>
`@import "retina-sprites";`

2. Create a folder in your images folder of your Compass project. By default the name is `icons`.

3. Save your sprite images in the folder. The pixel-ratio 1 variant in `./icons/sprite-base-name.png` and the retina variant in `./icons/sprite-base-name-2x.png`. Make sure there have the same base filename.

4. Use the sprite in your SASS/SCSS using: `@include use-sprite(<sprite-base-name>, true)`. (Note the missing .png, this is not needed.) The second parameter indicates that a retina version should be used for high resolution.

5. It is also possible to use sprites without a retina variant by simply omitting the second parameter odr setting it to false: `@include use-sprite(<sprite-base-name>)` or `@include use-sprite(<sprite-base-name>, false)`

It's really that easy!


##What it does:

Compass will create a nice sprite image from the images you put in the folder. Make sure you only use PNG files for the best result.

Using just the name of the file Compass will know where the image is located in the huge sprite image it will generate. The mixin will also get the retina variant if the browser is running in a pixel-ratio 2 environment.

This is the generated CSS from the example:

SCSS:
```scss
.sprite2 {
    @include use-sprite("sprite2", true);
}
```

CSS:
```css
.sprite2 {
  background-image: url('../images/icons-s5c7fdc1d93.png');
  background-position: 0 0;
  background-repeat: no-repeat;
  overflow: hidden;
  height: 25px;
  width: 25px;
}
@media (-webkit-min-device-pixel-ratio: 2), (-o-min-device-pixel-ratio: 3 / 2), (min--moz-device-pixel-ratio: 2), (min-device-pixel-ratio: 2), (min-resolution: 144dppx) {
  .sprite2 {
    background-size: 25px 85px;
    background-position: 0 -35px;
    height: 25px;
    width: 25px;
  }
}
```

##Bonus: retina background-images

With the same principles of the sprites I created a mixin that sets the background-image and it's retina version.

##How to use:

1. Include the mixin in your SASS/SCSS file using:<br/>
`@import "retina-background-image";`

2. Put a pixel-ratio 1 version and a retina version anywhere in your images folder.

3. Apply the style using: `@include background-retina(<filename.png>, <filename-retina.png>);`

The following code will generate:

SCSS:
```scss
.background {
	@include background-retina("background.gif", "background-2x.gif");
}
```

CSS:
```
.background {
	background-image: url('../images/background.gif');
}
@media (-webkit-min-device-pixel-ratio: 2), (-o-min-device-pixel-ratio: 3 / 2), (min--moz-device-pixel-ratio: 2), (min-device-pixel-ratio: 2), (min-resolution: 144dppx) {
	.background {
		background-image: url('../images/background-2x.gif');
		background-size: 25px 25px;
	}
}
```
