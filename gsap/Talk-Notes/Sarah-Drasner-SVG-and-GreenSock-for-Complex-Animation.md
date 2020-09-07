# SVG and GreenSock for Complex Animation

## Talk by Sarah Drasner, notes by Mel Jones

### Link to video

[https://www.youtube.com/watch?v=ZNukcHhpSXg&ab_channel=InfoQ](https://www.youtube.com/watch?v=ZNukcHhpSXg&ab_channel=InfoQ) by Sarah Drasner

## Animation

### Why?

- is powerful to convey meaning
- can guide your users
- because otherwise we're not using the web to it's full potential
- fun

## SVG

### Why?

- Crisp on Display
- less HTTP requests to handle (not important for HTTP2, learn more about this)
- Easily scalable for responsive
- Small file size IF you design for performance
- Easy to animate - has a navigable DOM, intruitive
- Easy to make accessible
- Fun

## Optimize

- SVGOMG
- Peter Collingridges's SVG Editor
- SVGO/SVGO-GUI

## Animation Perfomance

- Web vs Mobile
  - With mobile we're loarding a ton of data through a less secure and less fast connection, it's not going to be as fast. So we need to think about perfomance
- [http://jankfree.org/](http://jankfree.org/)
  - Jank - stutter you get when you do a lot of repaints
- Performant way of working - transform and opacity
- Advanced Performance Audits with DevTools by Paul Irish
- CSS-Tricks Article: Weighing SVG Animation Techniques with Benchmarks (old article, a lot has changed)
- GSAP performs as well as native technologies
- Above all: test things yourself

## Fallbacks

- with modernizr
- look at the analytics

## Main Principles:

**Design everything first, slowly unveil things.**

## GSAP

- for complex animations
- solves cross-browser Inconsistencies
- solves other tranform-origin issues

## Timeline

- stack tweens
- set them a little before and after one another
- change their placement in time
- group them into scenes
- add relative labels
- animate the scenes
- make the whole thing faster, move the placement of the whole scene, nesting

## GSAP - Animation

- motion along a path
- dragable - drag & drop
- CSS properties
- drawSVG
- MorphSVG
- Relative Color Tweening
- CycleStagger

### Relative Color Tweening

- Hue
- Saturation
- Brightness

### Motion Along a Path for Realism

- an array of x & y coordiantes
- autorotate true
- type soft - or more

```jsx
t1.to($firefly1, 6, {
	bezier: {
		type: "soft":,
		values: [{x:10, y:30}, {x:-30, y:2-}, {x:-40, y:10},
						{x:3-, y:30}, {x:10, y:30}],
		autoRotate:true
	},
ease:Liner.easeNone, repeat:-1}, "start+=3")
```

### Curviness

- soft or numerical value
- 2 like a loop round
- think of it like a rubber band around the s & y coordinates, it is taut at 0, at 2 it gets loose, at 4 it unravels around
- David Walsh Blog article & series

### Autorotate

- true - moves along and rotates along the path

### Percentage-Based Transforms on SVG

- but maybe you don't need it

## Fully Responsive in every direction!

### Designing Interaction in Responsive Animations

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf1a998e-baf4-47ce-8d9f-a6d68fd689ab/Screen_Shot_2020-09-05_at_14.18.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf1a998e-baf4-47ce-8d9f-a6d68fd689ab/Screen_Shot_2020-09-05_at_14.18.05.png)

- Make it like Legos

  - every area has a basic format
  - desktop version, magenta box is moved to the right and flipped
  - each box is a function, and each function calls a different timeline
  - keeps code organised, and makes it easy to adjust and manipulate

- Repeating animation
  - set to keep repeating -1

```jsx
// variable decalration for the global repeated animation
var gear = $("#gear1, #gear2, #gear3");
...

//animation that's repated for all of the sections
function revolve() {
	var t1 = new TimelineMax();

	t1.add("begin")
	t1.to(gear, 4, {
		tranformOrigin: "50% 50%",
		rotation: 360,
		ease: Linear.easeNone
	}, "begin")
	...

	return 1
}

var repeat = new TimelineMax({repeat:-1})
repeat.add(revolve())
```

- Paint Panda
  - paused to begin within, then when you click it triggers a restart

```jsx
function paintPanda() {
	var t1 = new TimelineMax()

	t1.to(1h, 1, {
		scaleY: 1.2,
		rotation: -5,
		transformOrigin: "50% 0",
	ease: Circ.easeOut
	}, "paintIt+=1")
	...
	return t1
}

// create a timeline but initially pause it so that we can control it via click
var triggerPaint = new TimelineMax({
	paused: true
})
triggerPaint.add(paintPanda())

// this button kicks off the panda painting timeline
$("#button").on("click", functions(e) {
	e.preventDefault()
	triggerPaint.restart()
})
...
```

### Atmosphere

- theory of animation
- the atmosphere should be user

### Elemental Motion

- things that are further away have less contrast and are blurry
- does the air or environment effect movement
- reducing precision allows for understanding

## MorphSVG from GSAP

- Tween paths to paths
- Tween shapes to paths
- Make animation magic

Point from one `id` to another

```jsx
TweenMaxto("#start", 1, {morphSVG:{shape:"#end"}
	ease:Linear.easeNone})
```

Use shapeIndex

- Default is auto
- load the extra plugin and GUI will come up
- Usually auto will be correct, but you can pick
- use `findShapeIndex(#start,#end)`

```jsx
TweenMaxto('#start', 1, { morphSVG: { shape: '#end', shapeIndex: '1' } })
```

### Fire Animation

- Used Lucas Bebber Gooey Menu
- Sarah animated the filter
- anything that is an integer can be animated with GSAP
- can reach in and make the filter more and less gooey through the flame
- and if everything is named properly can use a for loop to go through all the different values and id's. and then add it incrementally to the timeline, so it's always morphing at the next piece

```jsx
MorphSVGPlugin.convertToPath('ellipse')

function flame() {
  var t1 = new TimelineMax()

  t1.add('begin')
  t1.fromTo(
    blurNode,
    2.5,
    {
      attr: {
        stdDeviation: 9,
      },
    },
    {
      attr: {
        stdDeviation: 3,
      },
    },
    'begin'
  )
  var num = 9
  for (var i = 1; i <= num; i++) {
    t1.to(
      fStable,
      1,
      {
        morphSVG: {
          shape: '#f' + i,
        },
        opacity: Math.random() * 0.7 + 0.7,
        ease: Linear.easeNone,
      },
      'begin+=' + i
    )
  }
}
```

## More than one way to work

- Blake Bowen - Catmull-Rom Spline
