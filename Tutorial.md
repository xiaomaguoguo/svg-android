## Downloading ##

Download the jar file [here](http://code.google.com/p/svg-android/downloads/detail?name=svg-android.jar) and place it in the `libs` folder of your project.

## A Simple Example ##

Suppose we have a new Android project with a blank Activity, the svg-android.jar file in the `libs` directory, and [this](http://code.google.com/p/svg-android/downloads/detail?name=android.svg) SVG file in the `res/raw` folder.

The following code in the `onCreate` method will make the activity render the SVG file:

```
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // Create a new ImageView
        ImageView imageView = new ImageView(this);
        // Set the background color to white
        imageView.setBackgroundColor(Color.WHITE);
        // Parse the SVG file from the resource
        SVG svg = SVGParser.getSVGFromResource(getResources(), R.raw.android);
        // Get a drawable from the parsed SVG and set it as the drawable for the ImageView
        imageView.setImageDrawable(svg.createPictureDrawable());
        // Set the ImageView as the content view for the Activity
        setContentView(imageView);
    }
```

## How to Prepare Your Vector Images ##

This library supports a subset of the [SVG Basic 1.1](http://www.w3.org/TR/SVGMobile/) specification. Typically, you can just load your vector artwork in Illustrator and then save it as a SVG file (selecting the SVG Basic 1.1 option when asked) and it will work fine. Inkscape does not have direct support for SVG Basic, but many drawings will just work when saved as SVG from Inkscape. These are the features of SVG Basic not supported:

  * All text and font features.
  * Raster images (bitmaps).
  * Symbols, conditional processing.
  * Patterns.
  * Masks, filters and views.
  * Interactivity, linking, scripting and animation.

If your artwork includes text, you can right-click on the text object in Illustrator and choose _Create Outlines_. This converts the text in to standard paths, which will then work fine with the library.

Not all Illustrator effects (such as drop shadow) will work as they result in the creation of raster images when saved as SVG Basic.

## Some Tricks ##

**Canvas Drawing**

If you are drawing the SVG directly on to a Canvas, as opposed to populating an ImageView or some other pre-built container, then just use the `android.graphics.Picture` object instead:

```
    Canvas canvas;
    // ...
    // Parse the SVG file from the resource
    SVG svg = SVGParser.getSVGFromResource(getResources(), R.raw.android);
    // Get the picture
    Picture picture = svg.getPicture();
    // Draw picture in canvas
    // Note: use transforms such as translate, scale and rotate to position the picture correctly
    canvas.drawPicture(picture);
    // ...
```

**Bounds and Limits**

It is useful when working with an SVG to know the rectangular bounds of the content. The document (artboard) bounds themselves are typically not useful for this, as few artists will size the content to those bounds. Instead, we offer two approaches:

  1. **Bounds** If there is a layer in the artwork called _bounds_, it will not be drawn. Rather, the first rectangle found in that layer will be interpreted as the bounds of the artwork. This makes it easy for an artist to specify the right bounds right in the artwork without the developer having to do additional work.
  1. **Limits** While the parser is reading the SVG, it estimates the bounds of the artwork from what is read. This may not always be correct, but can often be relied upon for simple artwork.

Here is how to access the bounds and the limits:

```
    // Parse SVG
    SVG svg = SVGParser.getSVGFromResource(getResources(), R.raw.android);
    // Get the artist-specified bounds (will be null if not specified)
    RectF bounds = svg.getBounds();
    // Get the parser-estimated bounds (could also be null, for example if it is a blank SVG)
    RectF limits = svg.getLimits();
```

**Loading SVGs From Other Sources**

In addition to loading SVGs from resources, they can also be placed in the project's `assets` directory, and then loaded using the application's asset management facility:

```
    try {
        // Specify the path (relative to the 'assets' folder)
        final SVG svg = SVGParser.getSVGFromAsset(getAssets(), "android.svg");
    } catch (IOException e) {
        // Handle IOException here
    }
```

For complete control, an SVG can be loaded from a raw `InputStream` (UTF-8 encoding is assumed):

```
        InputStream input;
        // ...
        final SVG svg = SVGParser.getSVGFromInputStream(input);
```

**Color Substitution**

Upon loading the SVG, you can substitute one color in the SVG for another. For example, to make the green Android blue instead:

```
        // 0xFF9FBF3B is the hex code for the existing Android green, 0xFF1756c9 is the new blue color
        SVG svg = SVGParser.getSVGFromResource(getResources(), R.raw.android, 0xFF9FBF3B, 0xFF1756c9);
```

Future versions of the library will support substitutions of multiple colors.

## More Information ##

To learn more, visit the [Javadocs](http://svg-android.googlecode.com/svn/trunk/svgandroid/docs/index.html) or browse the [source code](http://code.google.com/p/svg-android/source/browse/#svn%2Ftrunk%2Fsvgandroid%2Fsrc%2Fcom%2Flarvalabs%2Fsvgandroid) directly. Also be sure to take a look at how the SVG library is used in the extensive [Androidify Wallpaper](http://code.google.com/p/svg-android/source/browse/#svn%2Ftrunk%2Fsvgwallpaper) demo, for which the full source code is available.