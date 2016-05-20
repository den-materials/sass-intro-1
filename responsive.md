# Responsive Web Design

## Learning Objectives

- Explain the difference between a responsive website and a mobile-specific website.
- Use media queries to adjust styles for different viewport sizes.
- Identify and use relative units like `em`, `rem`, `vh`, `vw`, etc..

# Opening

Ultimately we are trying to answer the question:

>How do we build web applications and sites for an optimal interaction
experience on a multitude of devices?

## You do: Turn and Talk (10 min / 10)

What makes a design fixed? What makes a design fluid? What makes a site responsive?

Check out [mediaqueri.es](http://mediaqueri.es) for inspiration.

>What are the most common dimensions for a website design?

You tell me! http://screensiz.es

## Mobile Specific Sites (5 min / 15)

One way to create optimal experiences for mobile users is a dedicated mobile site.

You know you're on one when you see `m.` in the url!

Compare https://m.ups.com with https://ups.com

![](http://imgs.xkcd.com/comics/server_attention_span.png)

Avoid these... please.

# The Three Components of Responsive Web Design (10 min / 25)

1. Flexible (or Fluid) Grids
1. Flexible Images (or Media)
1. Media Specific Layouts

## Flexible Grids

Already covered in [grids lesson](https://github.com/ga-wdi-lessons/css-grids)

<details>
  <summary>
	Refresher:
  </summary>
  <br>
  ```css
  .row, .column {
    /* By default, box-sizing is set to content-box */
    box-sizing: border-box;
  }

  .row {
    /* Let's add a border so we can see our rows better */
    border: 2px solid rebeccapurple;
  }

  /* Clear fix*/
  .row:before, .row:after {
    content: "";
    display: table;
  }

  .row:after {
    clear: both;
  }

  .column {
    /* Let's add another border so we can see our columns better */
    position: relative;
    border: 2px solid tomato;
    float: left;
    border-radius: 20px;
    text-align: center;
  }

  .column .column {
    border: 2px solid springgreen;
  }

  .header > .column,
  .footer > .column {
    padding: 25px;
  }

  .middle > .column {
    height: 400px;
    line-height: 400px;
  }

  .header ul {
    margin: auto;
  }

  .header li {
    display: inline-block;
    list-style-type: none;
  }

  .module {
    /* Let's add a background color to our modules so they're clearly visible.*/
    background: lightblue;

    /* Now let's give our modules a left and right margin of 10px */
    margin: 0 10px 0 10px;
  }

  .column-1 { width: 8.333%; }
  .column-2 { width: 16.66%; }
  .column-3 { width: 25%; }
  .column-4 { width: 33.33%; }
  .column-5 { width: 41.66%; }
  .column-6 { width: 50%; }
  .column-7 { width: 58.33%; }
  .column-8 { width: 66.66%; }
  .column-9 { width: 75%; }
  .column-10 { width: 83.33%; }
  .column-11 { width: 91.66%; }
  .column-12 { width: 100%; }
  ```
  <br>
</details>

## Flexible Media & Units

We need images that fit their containers.  
It turns `max-width: 100%` is the answer.  Most of the time.  For any media.

Even as our flexible container resizes, shrinking or enlarging our image, the
image’s aspect ratio remains intact.

```css
img,
embed,
object,
video {
  max-width: 100%;
}
```

### Relative units of measurement (10 min / 35)

So far, we've been working mostly with pixels (absolute unit of measurement) and
percentages (relative unit of measurements)

- em and rem
- vh and vw
- vmin and vmax
- ex and ch

[Doc dive](https://developer.mozilla.org/en-US/docs/Web/CSS/length)

## Media Queries (10 min / 45)

One way to adjust the styles depending on the device's size is by using media queries:

```css
body{
  background: papayawhip;
}

@media (max-width: 400px){
  body{
    background: tomato;
  }
}
```

Using media queries, we can group our css rules according to the size of our
expected viewing devises.  This media query says, if our viewport is less than
400px, use the following css rules.

The 400px corresponds to the device's viewport.  A device's viewport is
different from both its screen size and resolution.  Check out [this
article](http://www.quirksmode.org/mobile/viewports.html) if you're interested
in why.

Other possible values include

```
/* these are most commonly used */
min-width | max-width | min-height | max-height

/* these are possible, but less common */
| width | height
| device-width | min-device-width | max-device-width
| device-height | min-device-height | max-device-height
| aspect-ratio | min-aspect-ratio | max-aspect-ratio | max-device-aspect-ratio
| device-aspect-ratio | min-device-aspect-ratio |
| color | min-color | max-color
| color-index | min-color-index | max-color-index
| monochrome | min-monochrome | max-monochrome
| resolution | min-resolution | max-resolution
| scan | grid
```

## Meta name="viewport"

Be sure to include

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

This tells the browser to render the width of the page to match the screen-width which vastly improves the experience on mobile if the site is designed to be responsive.

_**Note:**_ don't use this tag if your site isn't designed to be responsive. You'll make the user experience worse.

This is the most common option, but not the only one. If you're curious:
- [CSS-tricks article](https://css-tricks.com/snippets/html/responsive-meta-tag/)
- [MDN article](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag)


# Exercise: Media Queries (15 min / 60)

Working with the example above, create a
[codepen](http://codepen.io/pen/) that includes at least two media
queries.

When the viewport is less than 800px wide, make the background yellow. When the viewport is less
than 400px wide, make the background green.

| < 400px wide | < 800px wide | else |
|:-------------|:-------------|:-----|
| green        | yellow       | red  |

![](https://dl.dropboxusercontent.com/s/o8xh3hdql9oijo2/mediaqueries.gif?dl=0)

### Bonus

Try out a few of the properties above. You can combine media queries to get several different results.

i.e. what combination of media queries could produce the following grid as the
viewport [changes size](http://maximin.tv/srm/)?

|           |        |        |
|:----------|:-------|:-------|
| green     | yellow | red    |
| turqouise | green  | purple |

[Like this.](http://recordit.co/UfnuMHQbWa)

More:
- [See more here](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
- [Read more](https://css-tricks.com/logic-in-media-queries/)

## Break (10 min / 70)

# Bonus exercise: Convert the "Craigslist Grid" (15 min)

https://github.com/ga-dc/craigslist_grid

## Cheatsheet:

- Sizes, sizes, and more sizes
- fluid media: `img, embed, object, video { max-width: 1 };`
- `@media (max-width: 400px) { ... }`
- min/max-width, min/max-height
- And: `@media (max-width: 400px) and (orientation: portrait) { ... }`
- Or (comma separated): `@media (min-width: 700px), handheld and (orientation: landscape) { ... }`

## Resources

- The post that introduced us to [responsive web design](http://alistapart.com/article/responsive-web-design)
- http://screensiz.es
- http://mediaqueri.es
- Media Query [Logical Operators](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Logical_operators)
- [Viewports](http://www.quirksmode.org/mobile/viewports.html)
- Book: Responsive Web Design, Ethan Marcotte

## [<- Back to main page](./readme.md)
