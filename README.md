# Out of the Blue: Creating Floating Hearts with a Range Slider with CSS and JavaScript

[![dev.to](https://img.shields.io/badge/dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/rodrigoantunes/bringing-floating-hearts-to-life-with-css-and-javascript-2hcd)

## Demo

[![CodePen](https://img.shields.io/badge/Codepen-000000?style=for-the-badge&logo=codepen&logoColor=white)](https://codepen.io/rodrigoant/pen/zYVZrgW)

## Post 

Inspired by an [animation I saw this morning](https://www.linkedin.com/posts/chrisgannon_3d-interactive-ui-activity-7224371526127525888-djbb?utm_source=share&utm_medium=member_desktop), I decided to try creating something along those lines **— though not nearly as impressive —** using JavaScript 🎨. 
It seemed like a fun and challenging task.

So, let's dive in!


### HTML

We'll start with a simple structure:

```html
<main>
  <input type="range" min="0" max="100" value="0" />
  <div class="container"></div>  <!-- this is where we'll place the hearts -->
</main>
```
### CSS

The CSS plays a significant role in this project, and I'd like to highlight two key aspects:

- Accent Color
- CSS Animations

#### Accent Color
I couldn't remember how to change the default look of the `<input type="range" />` element. During my research, I came across various vendor-prefixed pseudo-elements like [::-webkit-slider-runnable-track](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-slider-runnable-track) and [::-moz-range-track](https://developer.mozilla.org/en-US/docs/Web/CSS/::-moz-range-track) but the support for these wasn't great.

Then I came across a handy little CSS property called **[accent-color](https://developer.mozilla.org/en-US/docs/Web/CSS/accent-color)**. I had seen it a couple of times before, but not often enough for it to stick in my memory. It's also a perfect fit for styling `checkbox` and `radio` input elements.

Good job, [CSS Working Group](https://www.w3.org/groups/wg/css/)! 🥳

```css
input {
  /* ... */
  accent-color: white;
}
```

#### CSS Animations

I usually enjoy coding CSS animations from scratch, fine-tuning them to align with the design goals or specific creative direction. But today, I wasn't feeling it, so I asked **ChatGPT** to write three _organic floating animations_ with some variations and randomness. It didn't nail it on the first try, so instead of tweaking the animations by hand, I modified the prompt. While it might have been faster to code manually, 
after some time, the result was good enough.

_edit:_ I fine-tuned the animations 😁

The one thing I was particularly picky about was the syntax. Initially, it generated something like this:
```css
0% {
  transform: translateX(0px) translateY(0px) rotateX(45deg) rotateY(30deg) scale(0.25);
}
```

My reaction was like Michael Scott’s famous "Oh God, Please No!" meme. The [CSS Transform Module Level 2](https://www.w3.org/TR/css-transforms-2/#individual-transforms) syntax looks so much cleaner:

```css
0% {
  translate: 0px 0px;
  rotate: 45deg 30deg;
  scale: 0.25;
}
```
But I'm still getting used to this 'new' syntax too, so no big problems here.


### Javascript

Okay, let's fire up the engine 🚛.

I found it challenging to explain my thought process, but I spent nearly an hour just thinking through the problem. Here’s a breakdown of my approach:

```
1. Listen to the input event.
2. Create a new element when the event fires.
3. Animate each element up from where the input is located.
4. Remove each element after it finishes animating.
```

However, there’s no straightforward way to determine where the "slider's thumb" is on the screen, just the input element itself. Turns out there was a simple solution to this:

```js
range.addEventListener('input', (e) => {
  // ...
  const heart = document.createElement('div');
  heart.style.left = `${e.target.value}%`;
  // ...
}
```

Feel free to check out the [code](https://codepen.io/rodrigoant/pen/zYVZrgW).

I could refine the code for readability, structure it better with functional programming, or even enhance the animations further, but it serves its purpose well for a quick experiment.

I hope you enjoy it, and happy coding!

A big thanks to [Chris Gannon](https://gannon.tv/) for his inspiring work.