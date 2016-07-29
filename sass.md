# Intro to Sass

## Learning Objectives

- Be able to explain what Sass is and why it's used
- Use variables to make code more flexible
- Understand how to use nesting to help DRY up selectors and properties
- Differentiate between `@extend`, `@import`, `@mixin` & `@include`, and `@function`

## Framing: What is Sass?

![Sass Icon](http://sass-lang.com/assets/img/logos/logo-b6e1ef6e.svg)

---

### Syntactically awesome stylesheets (3 min)

- Sass is a superset of CSS that adds power and elegance to the basic language. You can do all the normal CSS things plus way more!

- You write a combination of CSS and SassScript, which compiles to proper CSS.

- It allows you to use variables, nested rules, mixins, inline imports, and more, all with a fully CSS-compatible syntax.

- Sass helps keep large stylesheets well-organized, and helps get small stylesheets up and running quickly...

## You Do: Turn and Talk (10 min / 12)

Here are a few examples of Jesse playing with CSS/Sass.  Let's look at the css
that is required to produce this effect.  Then, compare that to the Sass we used
to generate the css (by clicking "View Compiled").

- [BAMSAY](http://codepen.io/jshawl/pen/cLJal)
- [Boxes](http://codepen.io/jshawl/pen/nHDLz)
- [Bullseye](http://codepen.io/jshawl/pen/wpeit)
- [A Button](http://codepen.io/jshawl/pen/bcjyH)
- [Forest](http://codepen.io/jshawl/pen/cJjIm)
- [Space Invader](http://codepen.io/jshawl/pen/cnyrJ)

### Bonus

Whenever you are looking for something to do, come back and analyze these
examples.  How did we create that Space Invader?  You'd be surprised.  I was.

## Sass VS. scss (2 / 15)

Sass syntax originated from [Haml](http://haml.info/). Some developers didn't
like a syntax that was so foreign from CSS and so the developers that created
Sass introduced SCSS which is 'the new main syntax' for Sass.

# Variables (5/ 20)

Sass allows us to use variables which are defined with `$`. Variables can store
strings, numbers, colors, arrays, and objects. Variable names should relate to
their useage and not there value e.g. ✅`$border-color` vs. ❌`$red`. One big
advantage to using variables it makes it easy to update properties.

Assignment:
```scss
$base-color: blue;
```

Usage:
```scss
body {
  background-color: $base-color;
}
```

Variables are scoped to the selector they are defined in - if they not defined in a selector they are global. Just like in other languages the local scope replaces the higher scope _locally_.

```scss
$font-stack: Helvetica, sans-serif;

h1 {
  $font-stack: Raleway, sans-serif;
  font: 100% $font-stack;
}

p {
  font: 100% $font-stack;
}
```

<details class="qa">
  <summary class="question">
    Compiles to:
  </summary>
  <blockquote class="answer">
  <br>
  ```css
  h1 {
    font: 100% Raleway, sans-serif;
  }

  p {
    font: 100% Helvetica, sans-serif;
  }
  ```
  <br>
  </blockquote>
</details>

> Variables in a selector can be hoisted to the global scope with `!global`

# Operations

Sass allows us to do some simple math in our stylesheets

| Symbol | Operation      |
|:-------|:---------------|
| +      | Addition       |
| -      | Subtraction    |
| *      | Multiplication |
| /      | Division       |
| %      | Modulous       |
| ==     | Equality       |
| !=     | Inequality     |

```scss
$heading-height: 32px;

p {
  font-size: $heading-height / 2 - 4;
  // compiles to 12px;
}
```

> notice we can do multiple operations and mix and match units

# Nesting (10 min / 30)

As we've seen, CSS isn't very dry.  Take this nested CSS, for example.

```css
.nav li{
  display: inline-block;
}

.nav a{
  text-decoration:none;
}

.nav a:hover{
  text-decoration:underline;
}
```

<details class="qa">
  <summary class="question">
    **Q.** What does that css do?
  </summary>
  <blockquote class="answer">
    **A.** It styles nav elements.  Wouldn't it be nice if you could "group" it together?
  </blockquote>
</details>

### The & selector

Copy this scss into [sassmeister](http://www.sassmeister.com/).

```scss
.nav{
  li{
    display: inline-block;
  }
  a{
  text-decoration:none;
    &:hover{
      text-decoration:underline;
    }
  }
}
```

<details class="qa">
  <summary class="question">
    **Q.** What happened?  How can we use this?
  </summary>
  <blockquote class="answer">
**A.** It generated the same css we had before, but this is easier to reason about.

- Remove duplication.  
- Group similar rules together.  

  </blockquote>
</details>

> The Inception Rule: don't go more than four levels deep. - [thesassway](http://thesassway.com/beginner/the-inception-rule)

Ask yourself, can this style be achieved with fewer selectors?

### Property nesting

Properties can also be nested which is helpful to long ones

```scss
// SCSS
.card-right {
  border: {
    radius: 1em;
    top-left-radius: 0;
    bottom: {
      left-radius: 0;
      color: #333;
    }
  }
}
```


<details>
  <summary>
  Compiles to:
  </summary>
  <br>

  ```css
  /* CSS */
  .card-right {
    border-radius: 1em;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
    border-bottom-color: #333;
  }
  ```

  <br>
  <br>
</details>

# Comments

[Let's check out the docs](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#comments)

- CSS Style Comments remain (`/* comment */`).
- Single line comments do not (`// comment`)

## Break (10 min / 40)

# Extends & Inheritance (5 / 45)

The sass `@extend` directive lets a css selector inherit properties from another selector. This helps keep Sass super dry.

```scss
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}

.warning {
  @extend .message;
  border-color: yellow;
}
```

<details>
  <summary>
  Compiles to:
  </summary>
  <br>

  ```css
  .message, .success, .error, .warning {
    border: 1px solid #cccccc;
    padding: 10px;
    color: #333;
  }

  .success {
    border-color: green;
  }

  .error {
    border-color: red;
  }

  .warning {
    border-color: yellow;
  }
  ```

  <br>
  <br>
</details>

> example from [sass guide](http://sass-lang.com/guide)

# Imports

Very similar to `require` in node - allows an easy way to break styles into separate files and include them where you want. Makes it really easy to separate styling concerns without having a bunch of `<link src="">`

```scss
@import 'grids.scss';

// the file type is optional:

@import 'grids';
```

# Mixins (5 / 50)

Remember the clearfix problem from the CSS2 lesson.  We had to write specific
css to ensure floats did not effect the next element. Imagine trying to remember
that "fix" and typing it in correctly every time you needed it.  Now, you can
make a `clearfix` mixin that codifies the rules.  Then, those rules can be
included in any CSS rule we want.

```scss
// Make this in one file
@mixin clearfix(){
  /* clearfix */
  content: '';
  display:table;
  clear:both;
}

// Use it in many others
body::after{
  @include clearfix();
}

.nav::after{
  @include clearfix();
}
```

<details>
  <summary>
  Compiles to:
  </summary>
  <br>

  ```css
  body::after {
    /* clearfix */
    content: '';
    display: table;
    clear: both;
  }

  .nav::after {
    /* clearfix */
    content: '';
    display: table;
    clear: both;
  }
  ```

  <br>
  <br>
</details>

### Libraries/Frameworks (5 / 55)

There a good number of [libraries](http://www.hongkiat.com/blog/mixin-library-for-sass/) of mixins and functions that can extend the functionality of Sass. Most are used by `@import`ing the library `@include`ing the mixins where desired.

Bourbon + Neat are similar to bootstrap but are a lot more flexible and don't
require a bunch of classes everywhere. Super cool!
- [Bourbon](http://bourbon.io/) is "a simple and lightweight mixin library."
  - [Neat](http://neat.bourbon.io/) is "a lightweight semantic grid framework for Sass and Bourbon."

Compass is another framework that adds a bunch of extra features, a lot of the most useful ones are mixins that add vendor prefixes to styles. I've never
used it but it's out there and pretty popular.
- [Compass](http://compass-style.org/examples/compass/tables/all/)

If you're worried about vendor prefixes there is also [autoprefixer](https://github.com/postcss/autoprefixer). It's not a sass thing but cool regardless and potentially a good alternative to compass if you're only concerned with prefixes.

# Functions (5 / 60)

Sass comes with a [big list](http://sass-lang.com/documentation/Sass/Script/Functions.html) of built-in
functions. These built-in functions do a bunch of stuff like manipulating
colors, modifying strings/lists/maps(objects), and doing more complex math.

Some examples:
```scss
compliment($color)
// returns the compliment of a color

darken($color, $amount)
// makes a color darker

length($list)
// returns the length of a list

max($numbers...)
// finds the maximum of several numbers
```

### Custom Function Directives

You can also create your own custom function directives to define logic that can
be reused in your styles. There a bunch of control directives like `@if()`,
`@each`, and `@for` to do programmer-y things.

[Check out more](https://www.sitepoint.com/sass-basics-control-directives-expressions/)

### Functions vs. Mixins

For defining your own custom behavior you might be tempted to reach for a mixin
when you'd be better served by a function. They are similar because they both
accept variables.

- **Mixins** - should be used to generate styles
- **Functions** - are used to encapsulate logic like calculating a value

[Check out more](https://www.sitepoint.com/sass-basics-function-directive/)

# Exercise: Flash (15 minutes / 75)

[Flash Exercise](http://codepen.io/adambray/pen/bEgMXr)

Use SCSS to style the provided elements to recreate the image at bottom of the Codepen. You shouldn't need to modify the HTML at all.

Don't try to implement all the above Sass features at once. Instead, take the following steps...
* Complete the exercise, making sure to use variables for repeated values and nesting selectors where applicable.
* Once you're done, identify repeated chunks of code and define them in single selectors. Then apply them throughout your code using `@extend` statements.
* **BONUS:** Use a mixin or function to to generate the font and background colors for each button.

<details>
  <summary>
	 **SOLUTION:**
  </summary>
  [Only take a peek. No copy-and-pasting.](http://codepen.io/adambray/pen/yegjdj)
</details>

# Caveat

Webpages don't know what to do with raw Sass/SCSS, these files need to be
compiled to regular CSS to be used.

This can be done a number of different ways...
- Installing the sass gem `gem install sass` and compile with `$ sassc <whatever-input-filename.scss> <whatever-output-filename.css>`
  - There is also a `--watch` flag that allows you to watch a file and auto-compile every time you save it.
- Using a GUI program/plugin like `sass-autocompile`
  - `apm install sass-autocompile`
- Letting a build tool like Grunt/Gulp/Webpack/npm-scripts handle the compilation with an additional package/plugin.

# Conclusion

- Name 3 benefits of Sass.
- Describe how variables work in Sass
- Understand how to use nesting to help DRY up selectors and properties
- Differentiate between `@extend`, `@import`, `@mixin` & `@include`, and `@function`

### Want more?  

- [Super cool custom framework](http://www.sassmeister.com/gist/0a041d0fb2d72758c280)
  - From the scotch.io tutoral - [build your own framework](https://scotch.io/tutorials/getting-started-with-sass#function-directives)
]
- Or, check out the follow-up lesson, [Sass Directives](https://github.com/ga-wdi-lessons/sass-directives)

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
