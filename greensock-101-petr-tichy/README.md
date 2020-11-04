# Links

[GreenSock 101](https://ihatetomatoes.net/store/)

# Installation

GSAP

- add minified script in html
- you must add it before `main.js`
- you can also import it if using React or Vue.js
- on this example we will only work with

## To Tween

```js
gsap.to('header', { duration: 3, y: 20 })
```

- we take the element based on where the CSS has positioned it (the starting point)
- and we are animating the header element **to** 20 pixels along the y axis and with a duration of 3 seconds (the destination)
- you target the elements similar to CSS

On refresh you can see the translate3d changing
![translate3d](/img/Screen Shot 2020-10-20 at 13.27.01.png)

### Ease

- none/linear is good for fading in and out
- if the curve is steeper then the effect is stronger

```js
gsap.to('ul', {
  duration: 0.7,
  x: 40,
  ease: 'bounce.out',
})
```

### Stagger

- to move and animate things in a sequence

```js
gsap.to('ul li', {
  duration: 0.7,
  x: 40,
  ease: 'power2.out',
  stagger: 0.1,
})
```

## From Tween

- if we starting on the left side and bringing it back to the original CSS position
- the syntax is the same the **to tween**

```js
gsap.from('ul li', {
  duration: 0.7,
  x: -40,
  ease: 'power2.out',
  stagger: 0.1,
})
```

### repeatDelay

- will add a little pause between the second repeat

```js
gsap.from('ul li', {
  duration: 0.7,
  x: -40,
  ease: 'power2.out',
  stagger: 0.1,
  repeat: 2,
  repeatDelay: 1,
})
```

### yoyo

- replays the tween in the reverse order

```js
gsap.to('ul li:last-child', {
  duration: 0.7,
  y: 40,
  ease: 'power2.out',
  repeat: -1,
  repeatDelay: 1,
  yoyo: true,
  yoyoEase: 'none', // here you can control/change the ease on the way back!
})
```

## fromTo Tween

- define the start (from) and end (to) point
- and ignore the CSS positioning
- extra parameters are always added to the 'to' brackets
- 'from' only takes the position

```js
gsap.fromTo('element', { from }, { to })

gsap.fromTo('header', { x: -40 }, { x: 40 })

gsap.fromTo(
  'header',
  { x: -40 }, // from - only the position
  { x: 40, repeat: 2, duration: 1, ease: 'power2' } // to - extra parameters are always added here
)
```

### set

- doesn't do any animation, just moves it somewhere

```js
gsap.set('ul', { y: 100 })
```

# Practice / Play

1 - my version

```js
gsap
  .timeline({
    defaults: {
      stagger: 0.2,
    },
  })
  .fromTo(
    'h1 span',
    {
      y: -10,
      opacity: 0,
    },
    {
      duration: 0.3,
      y: 0,
      opacity: 1,
      ease: 'power2.out',
    }
  )
  .fromTo(
    'h1 em',
    {
      y: -10,
      opacity: 0,
    },
    {
      duration: 0.3,
      y: 0,
      opacity: 1,
      ease: 'power2.out',
    }
  )
  .fromTo(
    '.intro',
    {
      y: -10,
      opacity: 0,
    },
    {
      duration: 0.5,
      y: 0,
      opacity: 1,
      ease: 'power2.out',
    }
  )
  .fromTo(
    'img, h2',
    {
      opacity: 0,
    },
    {
      delay: 0.75,
      duration: 1,
      opacity: 1,
      ease: 'power2.out',
    }
  )
  .fromTo(
    'ul li',
    {
      y: -10,
      opacity: 0,
    },
    {
      delay: 0.75,
      duration: 1,
      y: 0,
      opacity: 1,
      ease: 'power2.out',
    }
  )
```

1 - Petr version

```js
gsap.from('body', {
  backgroundColor: '#fff',
  duration: 1.7,
  ease: 'none',
})

gsap.fromTo(
  ['h1', '.intro'],
  {
    y: -20,
    opacity: 0,
  },
  {
    y: 0,
    opacity: 1,
    duration: 0.6,
    ease: 'power1.out',
    delay: 1.5,
    stagger: 0.2,
  }
)

gsap.from(['img', 'h2'], {
  opacity: 0,
  duration: 0.7,
  ease: 'none',
  delay: 2.8,
})

gsap.fromTo(
  'ul li',
  {
    y: -20,
    opacity: 0,
  },
  {
    y: 0,
    opacity: 1,
    duration: 0.6,
    ease: 'power2.out',
    stagger: 0.2,
    delay: 4,
  }
)
```

**The above exercises can be done much cleaner and more editable with the use of...**

## Timelines

- you can declare it as a variable
- `const timeline = gsap.timeline`
- there are two ways that you can use Timelines

### timeline.add() method

- store each tween as a variable then add them to the method

```js
const timeline = gsap.timeline()

const tween1 = gsap.from('body', {
  backgroundColor: '#fff',
  duration: 1.7,
  ease: 'none',
})

timeline.add(tween1)
```

### chain tweens to the timeline

But the more simple (& preffered) way is

```js
const timeline = gsap
  .timeline()

  .from('body', {
    backgroundColor: '#fff',
    duration: 1.7,
    ease: 'none',
  })
  .fromTo(
    ['h1', '.intro'],
    {
      y: -20,
      opacity: 0,
    },
    {
      y: 0,
      opacity: 1,
      duration: 0.6,
      ease: 'power1.out',
      stagger: 0.2,
    }
  )
  .from(['img', 'h2'], {
    opacity: 0,
    duration: 0.7,
    ease: 'none',
  })
  .fromTo(
    'ul li',
    {
      y: -20,
      opacity: 0,
    },
    {
      y: 0,
      opacity: 1,
      duration: 0.6,
      ease: 'power2.out',
      stagger: 0.2,
    }
  )
```

- the delays have been removed
- delays are not useful anymore, unless you want to create a gap between tweens

### Overlap tweens

```js
  .fromTo(
    ['h1', '.intro'],
    {
      y: -20,
      opacity: 0,
    },
    {
      y: 0,
      opacity: 1,
      duration: 0.6,
      ease: 'power1.out',
      stagger: 0.2,
    },
    '-=1' // this brings the tween forward by 1 second - it will now overlap with the previous
  )

// position parameter (controls placement)
tl.to(target, {toVars}, positionParameter);

0.7 // exactly 0.7 seconds into the timeline (absolute)
"-=0.7" // overlap with previous by 0.7 sec
"+=0.7" // delay start 0.7 sec after previous finishes
"myLabel" // insert at "myLabel" position
"myLabel+=0.2" // 0.2 seconds after "myLabel"
"<" // align with start of most recently-added child
"<0.2" // 0.2 seconds after ^^

```

- tweens with the same label will start at the same time

## Timeline contols

- see `/js/timeLineControls.js
- GSAP cheatsheet

## Timeline callbacks

- we can fire off specific events (can be not related the the animation) when the animation starts
- we can see the progress of the animation on update
- we can fire something off at the end when the animation finishes
- **this applies to tweens as well as timelines**

```js
const runStart = () => {
  console.log('onStart')
}

const runUpdate = () => {
  console.log('onUpdate')
}

const runComplete = () => {
  console.log('onComplete')
}

const timeline = gsap.timeline({
  duration: 1,
  paused: true,
  onStart: runStart,
  onUpdate: runUpdate,
  onComplete: runComplete,
})

// returns
//  onStart
// (337) onUpdate //  is good for progress bars!
//  onComplete
```
