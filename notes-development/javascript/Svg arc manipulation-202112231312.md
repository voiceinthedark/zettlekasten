---
title: Svg arc manipulation
date: 23/12/23
tags: svg javascript mathematics pomodoro-timer
---

# **Svg arc manipulation** 202112231312 
> **299d79**

## Drawing the circle
`r` is the required radius
```html
<svg width="518" height="518" viewBox="0 0 518 518">
          <circle
            id="circle"
            stroke-width="9px"
            x="0"
            y="y"
            cx="259"
            cy="259"
            r="254"
          />
        </svg>
```
controlling the arc length is done by capturing the length mathematically $2 \times \pi \times r$
```js
let radiusOfTimerCircle = circle.getAttribute('r');
  // Length of the arc 2*π*r
  /* we need this for stroke-dasharray value */
  let lengthOfArc = 2 * Math.PI * radiusOfTimerCircle; // 1595.929068023615
```

then using the dasharray attribute of the circle we can calculate time passing in accordance to the length of the arc:
```javascript
function calculateTimeFraction() {
    let rawTimeLimit = time_left / time_limit;
    // to completely eliminates ring strokes, function need to work an extra second after the time limit
    return rawTimeLimit - (1 / time_limit) * (1 - rawTimeLimit);
  }

  // Update the dasharray value as time passes, starting with 283
  function setCircleDasharray() {
    const circleDasharray = `${(calculateTimeFraction() * lengthOfArc).toFixed(
      0
    )} ${lengthOfArc}`;
    document
      .querySelector('circle')
      .setAttribute('stroke-dasharray', circleDasharray);
  }
```

### reference
[CSS-Tricks](https://css-tricks.com/how-to-create-an-animated-countdown-timer-with-html-css-and-javascript/)
  

