---
title: "Using Clamp() for Responsiveness"
date: 2021-11-21T15:52:12+05:30
---

**Clamp()** is one of the most useful yet underrated functions in CSS to ensure responsiveness in web design.
Web pages can be viewed from multiple platforms, and you will have to ensure that the design won't break in any of the viewports.

---

Consider an id 'text' with font-size as 3rem.


```css
#text{
  font-size:3rem;
}
``` 

The problem is that irrespective of the viewport, font size remains constant. One way to deal with this is to replace rem with % or vw so that the font size becomes relative to the viewport.
```css
#text{
  font-size:7vw;
}
```
The issue that one could face with the above method is that there are no minimum and maximum limits. The text could get incredibly bigger or smaller depending upon the viewport.
This is where Clamp() comes to the rescue.
```css
#text {
  font-size:clamp(2rem,7vw,4rem);
}
```
Clamp() is a combination of min() and max(). It takes 3 arguments: the lower limit, the variable, and the upper limit. It clamps a value between the provided lower and upper limit. This ensures that the width remains relative to the viewport at the same time with a lower and upper bound.