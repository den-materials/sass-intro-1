# Intro to Sass

<!--11:15 5 minutes-->

<!-- OK, so this week we made HTML easier to write and DRYer with EJS.  It's too bad there's no way to do that with CSS...but wait, there is!  That way is Sass. -->

## Learning Objectives

- **Explain** what Sass is and why it's used
- **Use** variables to make code more flexible
- **Understand** how to use nesting to help DRY up selectors and properties
- **Differentiate** between `@extend`, `@import`, `@mixin` & `@include`, and `@function`

## Framing: What is Sass?

![Sass Icon](http://sass-lang.com/assets/img/logos/logo-b6e1ef6e.svg)

---

### Syntactically Awesome Stylesheets

Sass is a superset of CSS that adds power and elegance to the basic language. You can do all the normal CSS things plus way more!
- You write a combination of CSS and SassScript, which compiles to proper CSS.
- It allows you to use variables, nested rules, mixins, inline imports and more, all with a fully CSS-compatible syntax.
- Sass helps keep large stylesheets well-organized, and helps get small stylesheets up and running quickly.

> Sass syntax originated from [Haml](http://haml.info/). Some developers didn't like a syntax that was so foreign from CSS and so the developers that created Sass introduced SCSS which is 'the new main syntax' for Sass.

<!--11:20 10 minutes -->

## You Do: Explore Sass Examples

Explore these Codepens. When you open them, you'll notice that the CSS column has a header of `CSS (SCSS)`. This means that you're currently looking at Sass. Compare this to what you see when you click on the drop-down arrow at the top-right of the column and click "View Compiled CSS". Now you're looking at the CSS after it's been compiled from Sass.

Some things to consider...
* In what ways does Sass look different than Vanilla CSS?
* How might writing out Sass be easier / faster than writing out vanilla CSS?

#### Sass Examples

- [BAMSAY](http://codepen.io/jshawl/pen/cLJal)
- [Boxes](http://codepen.io/jshawl/pen/nHDLz)
- [Bullseye](http://codepen.io/jshawl/pen/wpeit)
- [A Button](http://codepen.io/jshawl/pen/bcjyH)
- [Forest](http://codepen.io/jshawl/pen/cJjIm)
- [Space Invader](http://codepen.io/jshawl/pen/cnyrJ)

> We don't expect you to understand exactly what the Sass is doing in these examples. Just think about it on a higher level.

<!--11:30 45 minutes -->

## You Do: Teachbacks

<!-- 25 minutes exercise. 20 minutes presentations. -->

For the remainder of the class, you will be divided into group that will research a certain aspect of Sass and teach it back to the class. Each group must create and demo a Codepen that shows their designed topic in action.

### I. Variables

#### Questions

* What are Sass variables? What problem do they solve?
* How do you define a variable?
* What values can you store in a variable?
* What are some common use cases?
* How does scope work with Sass variables?

Sass allows us to use variables which are defined with `$`. Variables can store
strings, numbers, colors, arrays, and objects. Variable names should relate to
their usage and not there value e.g. ✅`$border-color` vs. ❌`$red`. One big
advantage to using variables it makes it easy to update properties.

#### Resources

* [Sass Documentation](http://sass-lang.com/guide)
* [Sass Variables](https://robots.thoughtbot.com/sass-variables)
* [Getting Started with Sass](http://alistapart.com/article/getting-started-with-sass)

### II. Nesting

#### Questions

* What does "nesting" mean in Sass? What problem does it solve?
* What does `&` mean?
* What's the difference between selector nesting and property nesting? Show examples of each.
* How much nesting is too much nesting?

#### Resources

* [Sass Documentation](http://sass-lang.com/guide)
* [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)

### III. Extends & Inheritance

#### Questions

* What is Sass inheritance? What problem does it solve?
* How do we use `@extend` to implement inheritance?
* What does an `@extend` example look like when compiled to vanilla CSS.
* What are some common use cases?

#### Resources

* [Sass Documentation](http://sass-lang.com/guide)
* [Extending In Sass Without A Mess](https://www.smashingmagazine.com/2015/05/extending-in-sass-without-mess/)
* [The Extend Concept](https://css-tricks.com/the-extend-concept/)

### IV: Mixins

#### Questions

* What are mixins? What problem do they solve?
* How do we define and use a mixin?
* In what way might a mixin resemble a programming language?
* What is a common example of a mixin?

#### Resources

* [Sass Documentation](http://sass-lang.com/guide)
* [The Mixin Directive](https://www.sitepoint.com/sass-basics-the-mixin-directive/)
* [Handy Sass Mixins](https://web-design-weekly.com/2013/05/12/handy-sass-mixins/)
* [The Extend Concept](https://css-tricks.com/the-extend-concept/)

### V: Functions

If a group is looking for a challenge, look into Sass functions!

#### Resources

* [Sass Documentation](http://sass-lang.com/documentation/Sass/Script/Functions.html)
* [Pure Sass Functions](http://thesassway.com/advanced/pure-sass-functions)

<!--12:15 5 minutes -->

## Compiling to CSS

Webpages don't know what to do with raw Sass/SCSS, these files need to be compiled to regular CSS to be used.

This can be done a number of different ways...
- Installing the sass gem `gem install sass` and compile with `$ sassc <whatever-input-filename.scss> <whatever-output-filename.css>`
  - There is also a `--watch` flag that allows you to watch a file and auto-compile every time you save it.
- Using a GUI program/plugin like `sass-autocompile`
  - `apm install sass-autocompile`
- Letting a build tool like Grunt/Gulp/Webpack/npm-scripts handle the compilation with an additional package/plugin.

------

### Libraries/Frameworks

There a good number of [libraries](http://www.hongkiat.com/blog/mixin-library-for-sass/) of mixins and functions that can extend the functionality of Sass. Most are used by `@import`ing the library `@include`ing the mixins where desired.

Bourbon + Neat are similar to bootstrap but are a lot more flexible and don't
require a bunch of classes everywhere. Super cool!
- [Bourbon](http://bourbon.io/) is "a simple and lightweight mixin library."
  - [Neat](http://neat.bourbon.io/) is "a lightweight semantic grid framework for Sass and Bourbon."

Compass is another framework that adds a bunch of extra features, a lot of the most useful ones are mixins that add vendor prefixes to styles. I've never
used it but it's out there and pretty popular.
- [Compass](http://compass-style.org/examples/compass/tables/all/)

If you're worried about vendor prefixes there is also [autoprefixer](https://github.com/postcss/autoprefixer). It's not a sass thing but cool regardless and potentially a good alternative to compass if you're only concerned with prefixes.

<!--12:20 5 minutes -->

# Conclusion

- Name 3 benefits of Sass.
- Describe how variables work in Sass
- Understand how to use nesting to help DRY up selectors and properties
- Describe what `@extend` does

### Want more?  

- [Super cool custom framework](http://www.sassmeister.com/gist/0a041d0fb2d72758c280)
  - From the scotch.io tutoral - [build your own framework](https://scotch.io/tutorials/getting-started-with-sass#function-directives)
]
- Or, check out the follow-up lesson, [Sass Directives](https://github.com/ga-wdi-lessons/sass-directives)

# Exercise: Flash

> If you would like to practice Sass, give this exercise a shot.

[Flash Exercise](http://codepen.io/adambray/pen/bEgMXr)

Use Sass to style the provided elements to recreate the image at bottom of the Codepen. You shouldn't need to modify the HTML at all.

Don't try to implement all the above Sass features at once. Instead, take the following steps...
* Complete the exercise, making sure to use variables for repeated values and nesting selectors where applicable.
* Once you're done, identify repeated chunks of code and define them in single selectors. Then apply them throughout your code using `@extend` statements.
* **BONUS:** Use mixins and/or functions to to generate the font and background colors for each button.

<details>
  <summary>
	 **SOLUTION:**
  </summary>
  [Only take a peek. No copy-and-pasting.](http://codepen.io/adambray/pen/yegjdj)
</details>


### References

Guides:
- [Official getting started guide](http://sass-lang.com/guide)
- [Scotch.io - Build your own framework](https://scotch.io/tutorials/getting-started-with-sass#function-directives)
- [TheSassWay - Pure sass functions](http://thesassway.com/advanced/pure-sass-functions)
- [Sitepoint - Function basics](https://www.sitepoint.com/sass-basics-function-directive/)
- [Sitepoint - Control directives](https://www.sitepoint.com/sass-basics-control-directives-expressions/)
- [Docs for functions](http://sass-lang.com/documentation/Sass/Script/Functions.html)

Examples:
- [3D Buttons with Sass](https://jesse.sh/makes-3d-buttons-with-sass/)
- Github's Style Guide, [Primer CSS](http://primercss.io/about/)
