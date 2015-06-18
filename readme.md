## ABOUT

### Testing SVG icons versus font icons

-   Criteria used: number of server calls, number of new HTML nodes,
    number of CSS lines required, file size, file size after compression
    and responsiveness capability.

-   Test link:
    <http://www.voicefortheneedy.org/sapient/font-icon-svg-test/>

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

## Compression tool used

-   <http://petercollingridge.appspot.com/svg_optimiser>

-   Note: if the SVG file includes gradients, filters, effect or CSS, it
    is not recommended to use the optimiser because it removes ID and
    class attributes.

-   Other tools: grunt-svgmin task. *Edit:* grunt-svgmin task seems to
    shave off a third of the file size and it can be combined with
    grunticon (basically killing two birds with one stone, the stone
    being Grunt and the birds being file size optimizations and
    conversion to Data URI)

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


