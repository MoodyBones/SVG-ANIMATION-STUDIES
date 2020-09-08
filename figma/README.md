# S V G | A N I M A T I O N | S T U D I E S

- Study Notes by Mel Jones
- CodePen [Mel Jones](https://codepen.io/collection/AOzgOR)
- Twitter [\_moodybones](https://twitter.com/_moodybones)

# Figma - Drawing SVG

[Tut by Kezz Bracey](https://webdesign.tutsplus.com/courses/using-figma-for-svg-design/lessons/drawing-tools-overview)

## SVG Basic Shapes

[https://www.w3.org/TR/SVG/shapes.html](https://www.w3.org/TR/SVG/shapes.html)

SVG contains the following set of basic shape elements:

- rectangles (including optional rounded corners), created with the `rect` element,
- circles, created with the `circle` element,
- ellipses, created with the `ellipse` element,
- straight lines, created with the `line` element,
- polylines, created with the `polyline` element, and
- polygons, created with the `polygon` element

Mathematically, these shape elements are equivalent to a `path` element that would construct the same shape.

The basic shapes may be stroked, filled and used as clip paths. All of the properties available for `path` elements also apply to the basic shapes.

If it can't be built with one of the above basic shapes then you must use path! **But any shape created using a basic shape is going to use less code to create the same result as a path would.**

If possible always use basic shapes, more info on that here... [CSS Tricks Article - How to Simplify SVG Code Using Basic Shapes](https://css-tricks.com/how-to-simplify-svg-code-using-basic-shapes/)

## Figma Vector Drawing Tools

### Shapes Tools

- Rectangle - `rect` element
- Line - `line` element
- Arrow - path element
- Ellipse - `ellipse` element
- Polygon - path element
- Star - path element

  ![Screenshot of Figma Shape tools](/images/Screen_Shot_2020-09-08_at_11.04.53.png)

### Path Tools

- Pen - path element
- Pencil - path element

  ![Screenshot of Figma Path tools](/images/Screen_Shot_2020-09-08_at_11.05.56.png)

- **Important! if using Pen or Pencil, Figma will export in SVG as a path elements, even if they are shaped like a basic shape!**

### Rectangle

- to add radius grab and drag circle in the inner corner of the recangle
- it is also reflected on the right

  ![Rectangle Vector Shape](/images/Screen_Shot_2020-09-08_at_11.14.54.png)

- you can also select independent corners and edit them individually

### Ellipse

- grab dot on right, to create differrent types of archs

  ![Ellipse Vector Shape](/images/Screen_Shot_2020-09-08_at_11.17.19.png)

- ![Ellipse Vector Shape that looks like pacman](/images/Screen_Shot_2020-09-08_at_11.17.30.png)

### Polygon

- you can change the number of sides on the top right

  ![Polygon Vector Shape](/images/Screen_Shot_2020-09-08_at_11.20.13.png)

  - and the radius of the corners

  ### Star

  - essentially a polygon
  - you can change the number of points
  - and the angle
  - and radius

  ### Line

  - can change the rotation
  - good thing about using the line tool, is that you will export a `line` element, rather than a path

  ### Arrow

  - it's just a path
  - to see the arrow head you must increase the stroke

  ### Pen

  - click to draw out your points
  - click and drag to get round corners
  - if you don't want it to be self closing, hit enter to end the path

  ### Pencil

  - essential a drawing pencil
  - and not very good for SVG creation, unless you have a very steady hand, because you would need to mainly adjust the path to clean it up. There is any type of stabiliser or node reduction or clean up tool built into figma yet.

# Extra Figma Video Tutorials

    - [The Pen Tool & Vector Networks](https://www.youtube.com/watch?v=5x2uHUB_pzw&ab_channel=Figma)
