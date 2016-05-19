Sass (130)

- what is sass?

- variables
- nesting
  - reference parent `&`
  - nested properties
- imports
- mixins
- extend/inherit
- operators - math


# Sass - Intro

## Learning Objectives

- Be able to explain what Sass is and why it's used
- Use variables to make code more flexible
- Use nesting to dry up CSS
- Use @include and @extend to create mixins and inherit from other rules

## Framing: What is Sass? (15 min)

![Sass Icon](http://sass-lang.com/assets/img/logos/logo-b6e1ef6e.svg)

---

### Some would say Sass is...

- Sass is a superset of CSS that adds power and elegance to the basic language. You can do all the normal CSS things plus way more!

- You write a combination of CSS and SassScript, which compiles to proper CSS.

- It allows you to use variables, nested rules, mixins, inline imports, and more, all with a fully CSS-compatible syntax.

- Sass helps keep large stylesheets well-organized, and helps get small stylesheets up and running quickly...

## The Finished Product

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

## Sass VS. scss

Sass syntax originated from [Haml](http://haml.info/). Some developers didn't
like a syntax that was so foreign from CSS and so the developers that created
Sass introduced SCSS which is 'the new main syntax' for Sass.

# Variables

Sass allows us to use variables which are defined with `$`. Variables can store
strings, numbers, colors, arrays, and objects. Variable names should relate to
their useage and not there value e.g. ✅`$border-color` vs. ❌`$red`. One big
advantage to using variables it makes it easy to update properties.

Assignment:
```css
$base-color: blue;
```

Usage:
```css
body {
  background-color: $base-color;
}
```

Variables are scoped to the selector they are defined in - if they not defined in a selector they are global. Just like in other languages the local scope replaces the higher scope _locally_.

```css
$font-stack: Helvetica, sans-serif;

h1 {
  $font-stack: Raleway, sans-serif;
  font: 100% $font-stack;
}

p {
  font: $font-stack
}
```

> Variables in a selector can be hoisted to the global scope with `!global`

# Operations

Sass allows us to do smoe simple math in our stylesheets

| Symbol | Operation      |
|:-------|:---------------|
| +      | Addition       |
| -      | Subtraction    |
| *      | Multiplication |
| /      | Division       |
| %      | Modulous       |
| ==     | Equality       |
| !=     | Inequality     |

```css
$heading-height: 32px;

p {
  font-size: $heading-height / 2 - 4;
  // compiles to 12px;
}
```

# Nesting (10 min)

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

### The & selector (10 min)

Copy this scss into [precess.co](http://precess.co).

```css
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

```css
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


<details class="qa">
  <summary class="question">
  Compiles to:
  </summary>
  <details class="answer">
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
  </details>
</details>

# Comments

[Let's check out the docs](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#comments)

- CSS Style Comments remain (`/* comment */`).
- Single line comments do not (`// comment`)

# Imports



# Extends & Inheritance

```css
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

# Mixins (10 min)

Remember the clearfix problem from the CSS2 lesson.  We had to write specific
css to ensure floats did not effect the next element. Imagine trying to remember
that "fix" and typing it in correctly every time you needed it.  Now, you can
make a `clearfix` mixin that codifies the rules.  Then, those rules can be
included in any CSS rule we want.

Let's look at this in [precess.co](http://precess.co).

```css
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

# Functions

## Exercise: Flash (15 min)

[Flash Exercise](http://codepen.io/adambray/pen/bEgMXr)
<details>
  <summary>
	Hint
  </summary>
  [Solution](http://codepen.io/adambray/pen/yegjdj)
</details>

## Conclusion

- Name 3 benefits of Sass.
- How do `@mixin` and `@include` work together to make css more managable?

Want more?  
- [Build your own framework -scotch tutorial](https://scotch.io/tutorials/getting-started-with-sass#function-directives)
- Or, check out the follow-up lesson, [Sass Directives](https://github.com/ga-wdi-lessons/sass-directives)

## References

- [3D Buttons with Sass](https://jesse.sh/makes-3d-buttons-with-sass/)
- Github's Style Guide, [Primer CSS](http://primercss.io/about/)
- http://sass-lang.com/documentation/Sass/Script/Functions.html
