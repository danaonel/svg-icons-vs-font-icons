## Illustrator best practices

-   Create the SVG at the mobile size of the icon, not desktop.

-   Add a transparent square path at the bottom. This will serve as
    canvas when exporting to CSS background-image in Data URI format.

-   Ideally you would use one layer with only one simplified path.
    Multiple layers are used to add structure and depths to an SVG file,
    however our icons are flat.

-   Use symbols and simplify the paths in your artwork to improve SVG
    performance. Also avoid using brushes that produce a lot of path
    data, such as the Charcoal, Fire Ash, and Scroll Pen, if performance
    is a high priority.

-   To reduce file size, try reducing the number of objects (including
    groups) or making it less complex (fewer points). Using fewer points
    significantly reduces the amount of textual information needed to
    describe the artwork in the SVG file. To reduce points, select
    Object \> Path \> Simplify and try different combinations to find a
    balance between quality and number of points.

-   The simpler the image, the more consistent it will display across
    all platforms. Use Merge Shapes to combine different shapes into one
    layer.

-   Delete any hidden layers.

-   Do not use clipping paths.

-   The id of the layer is important, so use semantic names. This helps
    the developer later on in case she needs to modify the svg data.

-   If you need transparency, adjust the onject opacity as opposed to
    layer opacity.

-   Do not use the Rasterize, Artistic, Blur, Brush Strokes, Distort,
    Pixelate, Sharpen, Sketch, Stylize, Texture, and Video effects.
    These type of effects are rasterized when saved in SVG format.

-   Also do not use any raster data such as images, gradient meshes or
    objects that use above effects. They are not going to be scalable
    nor editable like other SVG elements, therefore defeating the
    purpose of svg.

-   Use SVG effects to add graphic effects without causing
    rasterization.

-   When you save artwork in SVG format, each layer is converted to a
    group () element. (For example, a layer named Button1 becomes in the
    SVG file.) Nested layers become SVG nested groups, and hidden layers
    are preserved with the display="none" SVG styling property.

    -   The AI layers below result in 263 lines of resulting SVG code.\

![][]

![][1]

-   When saving as SVG, do not go beyond two decimal points, unless
    really necessary. The more decimal points, the more accurate the
    path, but also more complex, hence the bigger file size.

-   Example of good AI practices\

![][2]

![][3]

### Reference

-   <http://help.adobe.com/en_US/illustrator/cs/using/WS714a382cdf7d304e7e07d0100196cbc5f-6360a.html#WS714a382cdf7d304e7e07d0100196cbc5f-635fa>

-   <http://help.adobe.com/en_US/illustrator/cs/using/WS714a382cdf7d304e7e07d0100196cbc5f-636fa.html#WSC97B6FDD-B90E-4f1b-B2F0-6D7B9A3DFC26>

-   <https://helpx.adobe.com/creative-cloud/tutorials/videos/responsive-svg-files-in-illustrator.html?product=illustrator&path=whats-new>

-   <http://joshuasortino.com/journal/creating-a-responsive-svg>

-   <http://demosthenes.info/blog/744/Make-SVG-Responsive>

-   <http://blogs.msdn.com/b/ie/archive/2011/10/27/best-practices-for-getting-started-with-svg.aspx>

  []: img/ai-layers-bad.png
  [1]: img/svg-bad.png
  [2]: img/ai-layers-good.png
  [3]: img/svg-good.png
