# Using SVGs

### Contents
- [SVG basics](#svg-basics)
- [Different ways of adding SVGs to a web page](#different-ways-of-adding-svgs-to-a-web-page)
- [Important elements in SVGs](#important-elements-in-svgs)
    - [Grouping with `<g>`](#grouping-with-g)
    - [Grouping with `<symbol>`](#grouping-with-symbol)
    - [Reusing elements with `<use>`](#reusing-elements-with-use)
- [Optimising SVGs](#optimising-svgs)
- [Styling SVGs with CSS](#styling-svgs-with-css)
- [Animating SVGs](#animating-svgs)
- [Spriting](#spriting)

## SVG basics
**Scalable Vector Graphics** (SVG) is an XML-based markup language for describing two-dimensional vector graphics. *SVG is essentially to graphics what HTML is to text.*

A ***vector graphic*** is composed of points in space (=vectors) each defined by an x- & y-coordinate, that are connected to create a shape. This means that, as opposed to raster graphics (like PNGs or JPGs), it won't become pixellated, no matter how much you zoom in.

**Tools for drawing & optimising vector graphics:**
- [Adobe Illustrator](https://www.adobe.com/uk/products/illustrator.html)
- [Sketch](https://www.sketchapp.com/)
- [Inkscape](https://inkscape.org/) (free software)
- [Method Draw](https://editor.method.ac/) (free online editor)
- [Ballpoint](https://ballpoint.io/) (free online editor)
- [SVG Edit](https://svg-edit.github.io/svgedit/releases/svg-edit-2.8.1/svg-editor.html) (free online editor)
- [SVGO](https://jakearchibald.github.io/svgomg/) (free online SVG optimiser; removes unneccesary metadata)

***SVG is a text-based open Web standard***, explicitly designed to work with other web standards such as CSS and DOM. SVG images and their related behaviors are defined in *XML text files* which means they can be searched, indexed, scripted and compressed. Additionally this means they can be created and edited with any text editor and with drawing software. 

**SVG or raster graphic??**
- If an image needs a great deal of variance in each pixel to render it properly (such as in a photograph or traditional artwork), storing the image as pixel data is more efficient than storing it as vector data.
- Typical uses cases for vector graphics include Vector logos, illustrations, technical drawings; but any image that can be drawn as a path by a computer is more efficiently stored as vector data.

## Different ways of adding SVGs to a web page
**Three different ways:**
1. **Image:** Use it just like a normal image file. All modern browsers will accept the SVG file format in the `<img>` element. SVGs can also be added as background images in the same way as other image formats.
1. **Inline:** Embed SVG markup directly into HTML documents. This allows to access and style parts of the SVG with CSS.
1. **Object:** Embed SVG using the HTML `<object>` element (using `<iframe>` or `<embed>` fall into the same category) - allows for browser caching *as well as* applying styling, but is more fiddly in assigning the right stylesheet and often not worth the resulting maintainability cost.

    ![3 Modes of SVG](/img/3-ways-with-svgs.png)
    *Source: [Front End Center — Why Inline SVG is Best SVG](https://www.youtube.com/watch?v=af4ZQJ14yu8)*

**Performance considerations:**
- inlining SVG code into HTML will reduce the number of HTTP requests required to load the page
- however, inliine SVGs will not be cached by the browser like other images, so will need to be reloaded every time
- therefore, inline SVGs should have a small file size

**Manageability:**
- stylesheets might affect SVGs that they shouldn't, and it can become hard to track what styles are applied to which SVGs.

> **Ideally add SVGs like a normal image, and only embed them if you absolutely have a requirement to style them.**

## Important elements in SVGs
Source: https://www.sarasoueidan.com/blog/structuring-grouping-referencing-in-svg/

### Grouping with `<g>`
`<g>` stands for ‘group’. The group element is used for logically grouping together sets of related graphical elements. In terms of graphics editors, the `<g>` element serves a similar functionality as the Group Objects function. You can also think of a group as being similar to the concept of a layer in a graphics editor, since a layer is also a grouping of elements.

Grouping allows you to apply certain actions to a whole set of items, for example:
- fill all elements in a group with a specified colour
- apply transformations (such as scale or rotation) to a group of items, whilst maintaining their spatial relations to one another
- attach mouse events etc. to a group of elements

Groups can also have their own `<title>` and `<desc>` tags, making it more accessible to screen readers, and making the code more readable:

```html
<g id="bird">
    <title>Bird</title>
    <desc>An image of a cute little green bird with an orange beak.</desc>
    <!-- ... -->
</g>
```

### Grouping with `<symbol>`
`<symbol>` is similar to `<g>` (group) in that it provides a way to group elements together. However, two main differences:

1. `<symbol>`s are not rendered. They are only displayed when they are `use`d.
1. `<symbol>`s can have their own viewBox and preserveAspectRatio attributes. 

`<symbol>` is therefore mostly suitable for defining reusable elements. It also serves as a template that is instantiated using the `<use>` element.

### Reusing elements with `<use>`
The <use> element lets you reuse existing elements, with the following benefits:
- avoid duplication
- useful in [SVG spriting](#spriting)

The `<use>` element takes `x`, `y`, `height`, and `width` attributes, and it references other content using the `xlink:href` attribute. So if you have defined a group (or `<symbol!>`) somewhere with an `id="bird"`, you use it as follows:

```html
<use xlink:href="#bird" />
```
The referenced element or group doesn't have to be in the same file.

## Optimising SVGs

https://jakearchibald.github.io/svgomg/


## Styling SVGs with CSS
- Make parts transparent with `opacity` and `stroke-opacity` (value between 0 and 1)
- Define the fill colour with `fill`
- Make things bolder with `stroke-width` - this can be useful for smaller screen sizes when styling responsive SVGs, as thicker stroke-widths can help lower resolution SVGs to retain detail and make it appear more iconographic.


## Animating SVGs
Internet Explorer does not support SVG animation, however you can use a polyfill such as [FakeSmile](https://leunen.me/fakesmile/) if you need it to work in IE too.

(W.I.P. section - to be continued...)


## Spriting
There are two approaches to spriting — in the first you define all the icons within `<symbol>` elements in the SVG but hide them. Then reference each later when needed with a `<use>` element referencing the `<symbol>` with `xlink:href="#id"`. The second uses the SVG viewbox attribute to crop the artboard (area of the SVG that shows) around a certain area.

Recommended article for learning how to implement these techniques: [An Overview of SVG Sprite Creation Techniques](https://24ways.org/2014/an-overview-of-svg-sprite-creation-techniques/) by Sara Soueidan.

**More resources:**
- [MDN SVG Documentation](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [Front End Center — Why Inline SVG is Best SVG](https://www.youtube.com/watch?v=af4ZQJ14yu8)
- [A practical guide to SVGs on the Web](https://svgontheweb.com/)
