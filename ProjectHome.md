## Vector Graphics Support for Android! ##

**Please note: the latest source code for this project is now on Github:**
https://github.com/pents90/svg-android

This is a compact and straightforward library for parsing SVG files and rendering them in an Android Canvas. By using vector art, the pain of supporting various screen sizes and densities in Android can be reduced. This was the library used to render the artwork and the interface of [Androidify](http://androidify.com).

The project also includes a **Live Wallpaper** app extracted from [Androidify](http://androidify.com). The app shows off the SVG library, and demonstrates the rendering pipeline used to draw the Androids.

![http://svg-android.googlecode.com/svn/trunk/svgwallpaper/screenshots/ws11.png](http://svg-android.googlecode.com/svn/trunk/svgwallpaper/screenshots/ws11.png)
![http://svg-android.googlecode.com/svn/trunk/svgwallpaper/screenshots/ws6.png](http://svg-android.googlecode.com/svn/trunk/svgwallpaper/screenshots/ws6.png)
![http://svg-android.googlecode.com/svn/trunk/svgwallpaper/screenshots/ws9.png](http://svg-android.googlecode.com/svn/trunk/svgwallpaper/screenshots/ws9.png)

## Simple To Use ##

Just place SVG files in the `res/raw` folder of your project, then load them as resources in your activity and work with them as `android.graphics.Picture` objects or as drawables:

```
    SVG svg = SVGParser.getSVGFromResource(getResources(), R.raw.filename);
    Picture picture = svg.getPicture();
    Drawable drawable = svg.createPictureDrawable();
```

See the [Tutorial](Tutorial.md) for more information, [SampleImages](SampleImages.md) for more examples of what you can do, or the [Javadocs](http://svg-android.googlecode.com/svn/trunk/svgandroid/docs/index.html) for the complete API.


## Release Notes ##

See [here](ReleaseNotes.md) for the release notes.