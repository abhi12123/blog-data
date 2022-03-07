---
title: "I made a portfolio website using only HTML without any Styles. This is what I learned"
date: 2022-02-27T18:29:59+05:30
---
I made a portfolio website using only HTML without any styles. The intention was to push the limits of pure HTML and see its capabilities, and it was worth it. These are some of the things I’ve learned during the process.   

![the html portfolio](https://miro.medium.com/max/542/1*6MnrGagtCj1Bb6_xG-2Z0Q.png)   

## 1.`<body>` tag has some styling properties

The body tag has some styling properties, but most of them are depreciated. There are attributes to change background color, text color, background image, hyperlink colors, and margin. But it is advisable to use CSS properties to achieve that as these are depreciated.

## 2.`<details>` can be used as a drop down element.

the `<details>` element is a widget that has an ‘open’ state which can be used to store information. Label can be provided inside the `<summary>` tag.
When the user clicks on the widget or focuses it then presses the space bar, it opens, revealing its contents.   
By default when closed, the widget only displays the disclosure triangle and summary. When open, it expands to display the details contained within.

```html
<details>
    <summary>Data</summary>
    <p>the data to display</p>
</details>
```

## 3.`target=’_blank’` and `target=’blank’`

The `<a>` has a href property which can be used to create hyperlinks. It also has a target property that decides where the linked URL has to be displayed. The keywords are :
 - `_self`: the current browsing context. (Default)
 - `_blank`: usually a new tab, but users can configure browsers to open a new window instead.
 - `_parent`: the parent browsing context of the current one. If no parent, behaves as `_self`.
 - `_top`: the topmost browsing context (the "highest" context that's an ancestor of the current one).  
 

Another keyword is `blank` where the URL will be displayed in a new tab, but on clicking again it will be reloaded in the same tab unlike _blank where new tabs are opened every time.

______

The website is hosted over [here](http://htmlportfolio.abhinavvp.com/)

