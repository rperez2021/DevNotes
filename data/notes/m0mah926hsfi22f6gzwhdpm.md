## General Info

Animations let you animate elements from one style configuration to another.

Animations consist of two components, a style describing the CSS animation and a set of keyframes that indicate the start and end states of the animation's style, as well as possible intermediate waypoints.

They are similar to transitions but differ in the following ways:

- Transitions were designed to animate an element from one state to another. They can loop, but they weren’t designed for that. Animations, on the other hand, were designed with the purpose of explicitly enabling loops.

- Transitions need a trigger, such as the use of pseudo-classes like :hover or :focus, or by adding/removing a class via JavaScript. Animations, on the other hand, do not need such a trigger. Once you have your elements in place and CSS defined, an animation will start running immediately if that’s what you told it to do.

- Transitions are not as flexible as using animations. When you define a transition, imagine you are sending that element on a journey in a straight line from point A to point B. Yes, the transition-timing-function can add some variation to the timing of this change, but it doesn’t compare to the amount of flexibility added by using animations.

## Animation Properties

The main animation property is `animation` and it can be used as a shorthand for:

`animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count, animation-direction, animation-fill-mode, and animation-play-state`

### Animation Name

Specifies the name of the `@keyframes` rule but this can be chosen by the user it is not a keyword

`animation-name: change-color;`

### Animation Duration

Configures the length of time that an animation should take to complete one cycle.

`animation-duration: 2s;`

### Animation Timing Function

Configures the timing of the animation; that is, how the animation transitions through keyframes, by establishing acceleration curves.

`animation-timing-function: ease-in;`

or

`animation-timing-function: steps(6, start);`

or

`animation-timing-function: cubic-bezier(0.1, 0.7, 1.0, 0.1);`

### Animation Delay

Configures the delay between the time the element is loaded and the beginning of the animation sequence.

`animation-delay: 2s;`

### Animation Iteration Count

Configures the number of times the animation should repeat; you can specify infinite to repeat the animation indefinitely.

`animation-iteration-count: infinite;`

or

`animation-iteration-count: 3;`

### Animation Direction

Sets whether an animation should play forward, backward, or alternate back and forth between playing the sequence forward and backward.

`animation-direction: normal;`

`animation-direction: reverse;`

### Animation Fill Mode

Configures what values are applied by the animation before and after it is executing.

`animation-fill-mode: forwards;`

### Animation Play State

Lets you pause and resume the animation sequence.

`animation-play-state: running;`

or

`animation-play-state: paused;`

## Keyframes

This is done by establishing two or more keyframes using the `@keyframes` at-rule. Each keyframe describes how the animated element should render at a given time during the animation sequence.

Since the timing of the animation is defined in the CSS style that configures the animation, keyframes use a `<percentage>`to indicate the time during the animation sequence at which they take place. 0% indicates the first moment of the animation sequence, while 100% indicates the final state of the animation. Because these two times are so important, they have special aliases: from and to. Both are optional. If from/0% or to/100% is not specified, the browser starts or finishes the animation using the computed values of all attributes.

## Color Changing Circle Example

```css
.container {
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}

#ball {
  width: 100px;
  height: 100px;
  background-color: red;
  border: 1px solid black;
  border-radius: 50%;
  animation-duration: 2s;
  animation-name: change-color;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

@keyframes change-color {
  from {
    background-color: red;
  }

  to {
    background-color: green;
  }
}
```

```html
<div class="container">
  <div id="ball"></div>
</div>
```
