# S V G | A N I M A T I O N | S T U D I E S

- Study Notes by Mel Jones

- CodePen [Mel Jones](https://codepen.io/collection/AOzgOR)

- Twitter [\_moodybones](https://twitter.com/_moodybones)

## REFERENCE: CSS Properties / GSAP Syntax

```jsx
x: 100 // transform: translateX(100px)
y: 100 // transform: translateY(100px)
z: 100 // transform: translateZ(100px)
// you do not need the null transform hack or hardware acceleration, it comes baked in with
// force3d:true. If you want to unset this, force3d:false
scale: 2 // transform: scale(2)
scaleX: 2 // transform: scaleX(2)
scaleY: 2 // transform: scaleY(2)
scaleZ: 2 // transform: scaleZ(2)
skew: 15 // transform: skew(15deg)
skewX: 15 // transform: skewX(15deg)
skewY: 15 // transform: skewY(15deg)
rotation: 180 // transform: rotate(180deg)
rotationX: 180 // transform: rotateX(180deg)
rotationY: 180 // transform: rotateY(180deg)
rotationZ: 180 // transform: rotateZ(180deg)
perspective: 1000 // transform: perspective(1000px)
transformOrigin: '50% 50%' // transform-origin: 50% 50%
```

# How to Animate on the Web With GreenSock - CSS Tricks

[Amazing Article on CSS Tricks by Sarah Drasner](https://css-tricks.com/how-to-animate-on-the-web-with-greensock/)

### GreenSock Ease Visualizer

Link: [https://greensock.com/ease-visualizer](https://greensock.com/ease-visualizer)

### I made a collection on CodePen

Link to whole collection: [https://codepen.io/collection/AOzgOR](https://codepen.io/collection/AOzgOR)

## Animating a DOM element

Link to CodePen: [https://codepen.io/MoodyBones/pen/jOqYWyq](https://codepen.io/MoodyBones/pen/jOqYWyq)

It’s grabbing the element with the class `.ball` on it, and translating those properties.

Since SVGs are literally DOM elements, we can slap a class on any one of them and animate them just the same way!

```html
<!-- SVG BALL -->
<svg viewBox="0 0 500 400">
  <circle class="ball" cx"80" cy="80" r="80"></circle>
</svg>

<!-- DIV BALL -->
<!-- <div class="ball"></div> -->
```

```css
:root {
  --primary-brand-color: #b9e972;
  --background-color: #faf9f0;
}

body {
  background: var(--background-color);
  display: flex;
  width: 99vw;
  height: 99vh;
  justify-content: center;
  align-items: center;
}

// SVG BALL STYLE
.ball {
  fill: var(--primary-brand-color);
}

svg {
  width: 400px;
  height: 200px;
}

// DIV BALL STYLE
// .ball {
//   background: var(--primary-brand-color);
//   width: 80px;
//   height: 80px;
//   border-radius: 50%
// }
```

```jsx
gsap.to('.ball', {
  duration: 1,
  x: 200,
  scale: 2,
})

// take the element with class ball
// move it .to()

// Shortened CSS props
// transform: translateX(200px)
// x: 200  (note there’s no need for the units, but you can pass them as a string)
// transform: scale(2)
```

## Eases

Link to CodePen: [https://codepen.io/MoodyBones/pen/gOroqPa](https://codepen.io/MoodyBones/pen/gOroqPa)

```jsx
gsap.to('.ball', {
  duration: 1.5,
  x: 200,
  scale: 2,
  ease: 'bounce',
})

// this assumes that you want to use `ease-out` timing, which is good for entrances
// then specify 'bounce'

// duration has been lengthed, because the ball now has more 'work' between the intial & end states.
// A one-second duration, though lovely for linear or sine easing, is a little too quick for a bounce or an elastic ease
```

## Delays and Timelines

Link to CodePen: [https://codepen.io/MoodyBones/pen/ExKoMVY](https://codepen.io/MoodyBones/pen/ExKoMVY)

```jsx
gsap.to('.ball', {
  duration: 1.5,
  x: 200,
  scale: 2,
  ease: 'bounce',
})

gsap.to('.ball', {
  duration: 1.5,
  delay: 1.5, // matched to previous animation duration
  x: 0,
  scale: 1,
  ease: 'back.inOut(3)', // checkout in GreenSock Ease Visualizer
})
```

- adding a delay based on the previous, only works for a simple animation
- because if you want to change the duration of the first, then you also have to change the delay on second
- and if you had more animations that follow, you would need to manually edit them all ☹️
- so instead use **Timelines!**

```jsx
// This instantiates a timeline and then chains the two animations off of it.

gsap
  .timeline()
  .to('.ball', {
    duration: 1.5,
    x: 200,
    scale: 2,
    ease: 'bounce',
  })
  .to('.ball', {
    duration: 1.5,
    x: 0,
    scale: 1,
    ease: 'back.inOut(3)',
  })
```

- we are repeating `duration: 1.5` in each animation
- we can create a default for that instead
- a default is an option passed to the timeline

### Pass Defaults to the Timeline

```jsx
gsap
  .timeline({
    defaults: {
      duration: 1.5,
    },
  })
  .to('.ball', {
    x: 200,
    scale: 2,
    ease: 'bounce',
  })
  .to('.ball', {
    x: 0,
    scale: 1,
    ease: 'back.inOut(3)',
  })
```

### Use `repeat: -1` to make it loop

- this can be added to either a single animation or the entire timeline

```jsx
gsap
  .timeline({
    repeat: -1,
    defaults: {
      duration: 1.5,
    },
  })
  .to('.ball', {
    x: 200,
    scale: 2,
    ease: 'bounce',
  })
  .to('.ball', {
    x: 0,
    scale: 1,
    ease: 'back.inOut(3)',
  })
  .to('.ball', {
    // mirror the first two aniamtions to go in the other direction
    x: -200,
    scale: 2,
    ease: 'bounce',
  })
  .to('.ball', {
    x: 0,
    scale: 1,
    ease: 'back.inOut(3)',
  })
```

### Repeat playback and forth like a `yoyo: true`

```jsx
gsap
  .timeline({
    repeat: -1,
    yoyo: true,
    defaults: {
      duration: 1.5,
    },
  })
  .to('.ball', {
    x: 200,
    scale: 2,
    ease: 'bounce',
  })
```

## Overlaps & Labels

Link to CodePen: [https://codepen.io/MoodyBones/pen/ZEWvPNb?editors=1010](https://codepen.io/MoodyBones/pen/ZEWvPNb?editors=1010)

- It’s great that we can chain animations with ease, but real-life motion doesn’t exactly work this way.
- If you walk across the room to get a cup of water, you don’t walk. Then stop. Then pick up the water. Then drink it.
- You’re more likely to do things in one continuous movement.
- We can use **overlaps** for this
- We can use a **incrementer or decrementer** passed in as strings e.g. '-=1'

### Overlaps

```jsx
gsap
  .timeline({
    defaults: {
      duration: 1.5,
    },
  })
  .to('.ball', {
    x: 300,
    scale: 2,
    ease: 'bounce',
  })
  .to(
    '.ball2',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    '-=1'
  )
  .to(
    '.ball3',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    '-=1'
  )
```

### Labels

- Another way we can do the above is with a label
- This makes sure that things fire off at a particular point in time in the playhead os the animation
- It looks like: `.add('labelName')`

```jsx
gsap
  .timeline({
    defaults: {
      durations: 1.5,
    },
  })
  .add('start')
  .to(
    '.ball',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    'start'
  )
  .to(
    '.ball2',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    'start'
  )
  .to(
    '.ball3',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    'start'
  )
```

- you can also increment and decrement from the label
  `start+=0.25`

```jsx
gsap
  .timeline({
    defaults: {
      durations: 1.5,
    },
  })
  .add('start')
  .to(
    '.ball',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    'start'
  )
  .to(
    '.ball2',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    'start+=0.25'
  )
  .to(
    '.ball3',
    {
      x: 300,
      scale: 2,
      ease: 'bounce',
    },
    'start+=0.5'
  )
```

Here’s an example of an animation that puts a lot of these premises together, with a bit of interaction using vanilla JavaScript. Be sure to click on the bell.

Link to Sarah Drasner's Pen: [https://codepen.io/sdras/pen/LYELqPX](https://codepen.io/sdras/pen/LYELqPX)

Big thanks to Sarah & CSS Tricks! <3
