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
![Sass Glasses](http://sass-lang.com/assets/img/illustrations/glasses-2087d741.svg)

---

### Some would say Sass is...

## [Syntactically Awesome Stylesheets](http://codepen.io/mattscilipoti/full/xwKrMR).

> Sass is an extension of CSS that adds power and elegance to the basic language.

> You write a combination of CSS and SassScript, which compiles to proper CSS.

> It allows you to use variables, nested rules, mixins, inline imports, and more, all with a fully CSS-compatible syntax.

> Sass helps keep large stylesheets well-organized, and helps get small stylesheets up and running quickly...


## The Finished Product

Here are a few examples of Jesse playing with CSS/Sass.  Let's look at the css that is required to produce this effect.  Then, compare that to the Sass we used to generate the css (by clicking "View Compiled").

- [BAMSAY](http://codepen.io/jshawl/pen/cLJal)
- [Boxes](http://codepen.io/jshawl/pen/nHDLz)
- [Bullseye](http://codepen.io/jshawl/pen/wpeit)
- [A Button](http://codepen.io/jshawl/pen/bcjyH)
- [Forest](http://codepen.io/jshawl/pen/cJjIm)
- [Space Invader](http://codepen.io/jshawl/pen/cnyrJ)

### Bonus

Whenever you are looking for something to do, come back and analyze these examples.  How did we create that Space Invader?  You'd be surprised.  I was.


## Variables

Sass allows us to intermingle css and SassScript.  Similar to how ERB allowed us to embed Ruby in our html.  One thing this gives us the variable.

Assignment (note the dollar sign):
``` sass
$variableName: value
```

Usage:
``` sass
css_declaration: $variableName
```

### Real world example:

Assignment:
``` sass
$colorPrimary: blue;
```

Usage:
``` sass
background-color: $colorPrimary;
```

## Nesting (10 min)

As we've seen, CSS isn't very dry.  Take this nested CSS, for example.

```scss
.nav a{
  text-decoration:none;
}

.nav li{
  display: inline-block;
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

An ecosystem that encourages best practices?  I love that.

## Mixins & Inheritance (10 min)

Remember the clearfix problem from the CSS2 lesson.  We had to write specific css to ensure floats did not effect the next element. Imagine trying to remember that "fix" and typing it in correctly every time you needed it.  Now, you can make a `clearfix` mixin that codifies the rules.  Then, those rules can be included in any CSS rule we want.

Let's look at this in [precess.co](http://precess.co).

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

### Comments

While we're here, make note of those comments.  Some are in the compiled CSS.  Some are not.

[Let's check out the docs](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#comments)

- CSS Style Comments remain (`/* comment */`).
- Single line comments do not (`// comment`)


<details class="qa">
  <summary class="question">
    **Q.** Why would we want that?
  </summary>
  <blockquote class="answer">
**A.** Sometimes we want a comment for the builders/writers of the css/sass.  Sometimes we want a comment for those using our css.
  </blockquote>
</details>

Note the ability to interpolate in the comment.

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

Want more?  Check out the follow-up lesson, [Sass Directives](https://github.com/ga-wdi-lessons/sass-directives)

## References

- [3D Buttons with Sass](https://jesse.sh/makes-3d-buttons-with-sass/)
- Github's Style Guide, [Primer CSS](http://primercss.io/about/)
- http://sass-lang.com/documentation/Sass/Script/Functions.html
