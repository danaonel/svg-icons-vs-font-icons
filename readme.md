## ABOUT

### Testing SVG icons versus font icons

-   Criteria used: number of server calls, number of new HTML nodes,
    number of CSS lines required, file size, file size after compression
    and responsiveness capability.

-   Test link:
    <http://danaonel.github.io/svg-vs-font-icons/demo.html>


<pre>
	
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| Stuff to measure                       | Server Calls          | HTML Nodes   |   CSS Lines     | File Size (CSS|HTML|IMG)| Gzip Compression      | Responsive            |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| Font icons (1 icon)                    | 3                     | 1 per icon   | 31              | 1.3k                    | NA                    | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| Font icons (21 icons)                  | 3                     | 1 per icon   | 91              | 3.9K                    | NA                    | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (1 icon) - CSS BG                  | 1                     | 1 per icon   | 15              | 0.5K|0.8K|0.7K          | 0.3K|0.7K|0.5K        | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (21 icons) - CSS BG Sprite         | 3                     | 1 per icon   | 133             | 2.3K|2.2K|18.1K         | 0.8K|1.0K|4.2K        | No                    |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (21 icons) - CSS BG Sprite URI     | 3                     | 1 per icon   | 133             | 26.5K|2.2K|0.0K         | 9.2K|1.0K|0.0K        | No                    |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (21 icons indiv) - CSS BG URI      | 2                     | 1 per icon   | 73              | 33.1K|2.2K|0.0K         | 7.6K|1.0K|0.0K        | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (42 icons) - CSS BG Sprite         | 3                     | 1 per icon   | 263             | 5.9K|3.6K|36.0K         | 1.1K|1.1K|4.7K        | No                    |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (42 icons) - CSS BG URI Sprite     | 2                     | 1 per icon   | 263             | 53.9K|3.6K|0.0K         | 16.2K|1.1K|0.0K       | No                    |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (1 icon) - INLINE                  | 2                     | 5 per icon   | 16              | 0.5K|1.2K|0.0K          | 0.2K|1.0K|0.0K        | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (21 icons) - INLINE                | 2                     | 105          | 16              | 0.5K|22.9K|0.0K         | 0.2K|4.6K|0.0K        | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (42 icons) - INLINE                | 2                     | 210          | 16              | 0.5K|45.4K|0.0K         | 0.2K|5.1K|0.0K        | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (1 icon) - OBJ                     | 2                     | 1 per icon   | 0               | 0.0K|0.9K|0.5K          | 0.0K|0.8K|0.7K        | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (21 icons) - OBJ                   | 21                    | 1 per icon   | 0               | 0.0K|4.6K|14.5K         | 0.0K|1.0K|14.1K       | Yes                   |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (1 icon) - XLINK                   | 3                     | 2 per icon   | 10              | 0.1K|0.9K|0.5K          | 0.4K|0.8K|0.7K        | Yes*                  |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (21 icons) - XLINK                 | 3                     | 44           | 10              | 0.1K|4.0K|9.5K          | 0.4K|1.0K|4.0K        | Yes*                  |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+
| SVG (42 icons) - XLINK                 | 3                     | 88           | 10              | 0.1K|7.3K|18.7K         | 0.4K|1.2K|4.4K        | Yes*                  |
+----------------------------------------+-----------------------+--------------+-----------------+-------------------------+-----------------------+-----------------------+

* The maximum size of the SVG icon is determined by the path size.

</pre>

### Font Icon - Server calls

-   HTML file

-   CSS file

-   Font file

### SVG icon as CSS BG image - Server calls

-   HTML file

-   CSS file

-   SVG file

### SVG icon as inline path - Server calls

-   HTML file

-   CSS file

### SVG icon object - Server calls

-   HTML file

-   SVG files (if the SVG file is Base 64 encoded, we have to add CSS
    separately, so that will make a 3rd server call)

### SVG icon xlink - Server calls

-   HTML file

-   CSS file

-   SVG file (the SVG file will contain all icons)

## Optimization notes

-   Optimization tool used <http://petercollingridge.appspot.com/svg_optimiser>

-   If the SVG file includes gradients, filters, effects or CSS, it
    is not recommended to use the optimiser because it removes ID and
    class attributes.

-   Other optimization tools: grunt-svgmin task. *Edit:* grunt-svgmin task seems to
    shave off a third of the file size and it can be combined with
    grunticon (basically killing two birds with one stone, the stone
    being Grunt and the birds being file size optimizations and
    conversion to Data URI)

## Gzip compression notes

-   SVG can be turned into SVGZ files by compressing them with gzip
    (e.g. using the command line "gzip -9 filename") It makes the files
    *way* smaller, and can be used as long as the SVG files are not
    inline. The only thing you have to do is put the following lines
    inside the .htaccess file into your doc root:

    `AddType image/svg+xml svg svgz`

    `AddEncoding gzip svgz`

-   Alternativiely you can configure your Apache server to do this
    server-wide.

## Data URI Encoder used

-   <http://www.mobilefish.com/services/base64/base64.php>

-   Alternativelly we can use grunticon task to automate the conversion
    to Data URI.

## Fall back IE8

-   PNG for SVG (there are a variety of fallbacks both javascript based
    and pure CSS)

-   Grunticon task does a great job at converting the svg files to png
    and writing javascript fallback for IE8 and below.

## Font Icons Concerns

-   Font icon fiddly to position

-   Problems with :before :after pseudo classes in the sense that they
    might be used for something else thus conflicting with the icon
    which relies on these pseudoclasses (.nav:before { content:
    "fonticon"; })

-   Font Icons are monochrome and don't support animation capabilities

-   SVG is more robust when it comes to browser support (Chrome font
    bugs, Firefox renders icon fonts crisper, some mobile browsers can
    be tricky with web fonts)

-   More control over SVG code

-   Issues with font-smoothing. You cannot guarantee how the font is
    going to be rendered, because Windows, OSX and Linux render them
    differently.

-   In Windows, font-smoothing can be turned off at the strangest times
    (for example, when doing a webex or a similar screenshare)

-   CSS3 Transforms have some unexpected effects on effects on
    typography when animating them.


## SVG Concerns

-   Larger file sizes

-   More DOM nodes when SVG is inline

-   Less CSS control

-   SVG accessible to Javascript, thus we can manipulate parts of the
    image with client-side scripts

-   Need extra time for SVG creation in Illustrator (adds to creative
    timeline)

## SVG Creation

-   Open Illustrator file from designer

-   The illustrator file should already have paths

-   Save file as SVG

-   Optimize the SVG file using any of the above tools

-   Encode the optimized SVG file to Data URI

## Conclusions

- Avoid linking to individual SVGs because this will increase the number of server calls and slow down the page load. So no object or image embed.

- Avoid adding inline SVGs because this will increase the number of HTML nodes significantly.

- There is no significant difference between using SVG sprite and SVG converted to Data URI sprite, unless the SVG is minified and optimized before converting to Data URI. In the last case, the Data URI is better than the SVG sprite.

- The best solution for single color icons is to use SVG's xlink property. One SVG file will contain all the icons layered on top of each other and it allows the developer to set the color and hover color via CSS.

- The best solution for multi color non-authorable icons is to use SVG sprites. If the icons have to be authorable, SVGs converted to Data URIs are a better solution. Just make sure the source SVG file is optimized and minified before converting to Data URI or you'll end up with a humongous file.

## Reference

-   <http://24ways.org/2014/an-overview-of-svg-sprite-creation-techniques>

-   <http://css-tricks.com/icon-fonts-vs-svg/>

-   <http://toddmotto.com/mastering-svg-use-for-a-retina-web-fallbacks-with-png-script/>

-   <http://ianfeather.co.uk/ten-reasons-we-switched-from-an-icon-font-to-svg/>

-   <http://css-tricks.com/using-svg/>

-   <http://www.hongkiat.com/blog/scalable-vector-graphic-css-styling/>

-   <http://codepen.io/chriscoyier/pen/evcBu>

-   <http://caniuse.com/#feat=svg-css>

-   <http://demosthenes.info/blog/675/Create-Adaptive-SVG-Illustrations-With-CSS>

-   <http://www.w3.org/TR/SVGMobile/>

-   <http://www.w3.org/TR/SVG/>

-   <https://github.com/filamentgroup/grunticon>

-   <https://github.com/sindresorhus/grunt-svgmin>


