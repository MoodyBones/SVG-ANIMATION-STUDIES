## Links

[ScrollTrigger 101](https://ihatetomatoes.net/store/)

## Installation

Simply clone this repo and follow the videos

I will be using [Live Server VSCode extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) to live reload any changes. Feel free to install it too.

# Notes by Mel

- ScrollTrigger is a GSAP extra and must be imported seperately

`index.html`

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.5.1/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.5.1/ScrollTrigger.min.js"></script>
```

`main.js`

```js
gsap.registerPlugin(ScrollTrigger)

function init() {}

window.addEventListener('load', function () {
  init()
})
```

## Simple fade out on Scroll Tween

- opacity reduces on scroll

```js
gsap.to('#intro img', {
  opacity: 0,
  scrollTrigger: {
    trigger: '#intro', // when we want the animation to trigger
    start: 'top top', // when top of #intro, hits the top of the viewport
    end: 'bottom center', // when the bottom of #intro, is in the center of the screen
    scrub: true, // we want the user to control the opacity/playback of the tween
    markers: true, // for debugging, shows start/end animations triggers  - SUPER HANDY
  },
})
```
