title: What is Sass?
class: segue

<!-- Sass is a css pre-compiler, that augments existing css features, and adds a host of cool new ones, to make writing css easier. -->

---

section: What is Sass?
title: Setup

<!-- - You need ruby to install and run SASS, which is already on your system if you are a mac user, and probably is included in your linux distro -->
<!-- Windows users: http://rubyinstaller.org/ -->
- ``gem install sass``
- Command line: ``sass --watch style.scss:style.css``
- GUI: CodeKit, LiveReload, compass APP
---

section: What is Sass?
title: The Syntax
class:

<!-- Exp. SASS vs. SCSS -->
<div class="flexy">
<pre class="prettyprint" data-lang="sass">
$primary: #3bbfce;
$margin: 16px;

.content-navigation
  border-color: $primary
  color: darken($primary, 9%)

.border
  padding: $margin /2
  border-color: rgba($primary,0.8)

</pre>
<pre class="prettyprint" data-lang="scss">
$primary: #3bbfce;
$margin: 16px;

.content-navigation {
  border-color: $primary;
  color:
    darken($primary, 9%);
}

.border {
  padding: $margin / 2;
  border-color: rgba($primary,0.8)
}
</pre>
</div>

---
title: Why Sass?
class: segue

---

section: Why Sass?
title: SASS is DRY

- Variables and nesting
- @extend classes
- Functions, Mixins, and more

---
section: Why Sass?
title: Variables

<div class="flexy">
<pre class="prettyprint" data-lang="scss">
$primary: green;
$bodyMargin: 10px;

.page {
  border-color: $primary;
  margin-left: $bodyMargin;
}

</pre>

<pre class="prettyprint" data-lang="css">
.page {
  border-color:green;
  margin:10px;
}
</pre>
</div>
<!-- Imagine using this value throughout your stylesheet, but being able to change it in one place -->
---
section: Why Sass?
title: Nesting

<div class="flexy">
<pre class="prettyprint" data-lang="scss">
.contact-form {
  p {
    color:red;
  }

  a {
    background: blue;
    <b>&:hover</b> {
      background:red;
    }
  }

  label {
    padding:0;
  }
}
</pre>

<pre class="prettyprint" data-lang="css">
.contact-form p {
  color:red;
}

.contact-form a {
  background:blue;
}

.contact-form a:hover {
  background:red;
}

.contact-form label {
  padding:0;
}

</pre>
</div>

---

section: Why Sass?
title: @extend

<!-- I think this is great, because it gives more control to the CSS syler bring the power of OOCS into your spreadsheet, not your markup -->
<div class="flexy">
<pre class="prettyprint small" data-lang="scss">
  .btn {
    display:inline-block;
    border-radius:4p;
  }

  .cta {
    @extend .btn;
    font-weight:bold;
  }

  .warn {
    @extend .btn;
    @extend .cta;
    color:red;
  }


<!-- .widget .blog widget etc.   -->

</pre>
<pre class="prettyprint small" data-lang="css">

 .btn, .cta, .warn {
   display: inline-block;
   border-radius: 4p;
 }

 .cta, .warn {
   font-weight: bold;
 }

 .warn {
   color: red;
 }

</pre>
</div>

---
section: Why Sass?
title: Mixins: roll your own
build_lists: true

Automate common workflows

Effectively Leverage SASS functions

Easily develop your own toolkit or framework

- <b>Example: Named Media Queries (ala Chris Coyier)</b>

---
section: Why Sass?
title: Mixins: Setup

<div class="flexy">
<pre class="prettyprint small" data-lang="scss">

@mixin breakpoint($point) {
  @if $point == designer {
    @media (max-width: 1600px)
    { @content; }
  }

  @if $point == developer {
    @media (max-width: 1250px)
    { @content; }
  }
}

</pre>
<pre class="prettyprint small" data-lang="scss">

.breakpoint-example {

  @include breakpoint(designer) {
    color:red;
  }

  @include breakpoint(developer){
    color:blue;
  }
 }
}
</pre>
</div>
---
section: Why Sass?
title: Mixins: Result

<pre class="prettyprint small" data-lang="css">

@media (max-width: 1600px) {
  .breakpoint-example {
    color: red;
  }
}

@media (max-width: 1250px) {
  .breakpoint-example {
    color: blue;
  }
}
</pre>

<!-- Other examples: - REM sizer, responsive calculations, Compass -->
<!-- Not that we should be targeting breakpoints like this, but think about how this makes shifting things around easy -->
---
section: Why Sass?
title: built in functions

<pre class="prettyprint small" data-lang="scss">
  .btn {
    background:blue;
    padding: <b>round</b>(3.1415926)
    &:hover {
      background:<b>darken</b>(blue,10%);
    }
  }
</pre>
<pre class="prettyprint small" data-lang="css">

.btn {
  padding: 3;
}
.btn:hover {
  background: #0000cc;
}
<pre>

---
section: Why Sass?
title: Partials

<pre>
  styles
    |--- base.scss // the mothership
    |--- <b>_type.scss</b>
    |--- <b>_widgets.scss</b>
    |--- <b>_layout.scss</b>
</pre>

<pre class="prettyprint small" data-lang="scss">
// base.scss
@import "type";
@import "widgets";
@import "layout";
</pre>
<!-- Benefits: 1. Organization 2. Easier Version Control -->

---

title: It's better with Compass
class: segue
<!-- All this is really great, but it leaves you to create all the mixins/functions/plugins that you need. That's where Compass comes in -->
<!-- Explain what compass is
1. Framework that:
  - Includes a host of plugins
  - Is project focused
  - Provides built in debugging features
 -->
---
section: Why Compass?
title: Compass is easy

- ``gem install compass``
- ``compass init``
- ``compass watch``

Compass will watch and compile all scss files in your stylesheet directory

---

section: Why Compass?
title: Killer Features
build_lists: true

- CSS3 Mixins
- Automatic spriting
- Grid plugins

---

section: Why Compass?
title: Prefix-free CSS3
class:
build_lists: true

<pre class="prettyprint" data-lang="scss">
  @import "compass/css3";

  body{
    @include background(linear-gradient(left top, white, #dddddd));
  }
</pre>


<!-- - You could use your own mixins, or a mixin pack from someone else, but compass is updated regularly, and stays very close
to accepted syntax. (it's not worth the hassle)
 -->
---

section: Why Compass?
title: Prefix-free CSS3
class:
build_lists: true

<pre class="prettyprint" data-lang="css">
body {
  background: -webkit-gradient(linear, 0% 0%, 100% 100%, color-stop(0%, #ffffff), color-stop(100%, #dddddd));
    background: -webkit-linear-gradient(left top, #ffffff, #dddddd);
    background: -moz-linear-gradient(left top, #ffffff, #dddddd);
    background: -o-linear-gradient(left top, #ffffff, #dddddd);
    background: linear-gradient(left top, #ffffff, #dddddd);
    // That was easy
}
</pre>

---
section: Why Compass?
title: Grids with Susy

<figure class="ag-test">
  <div class="ag1"><p><strong>Column</strong> 2 of&nbsp;10</p></div>
  <div class="ag2">
    <p><strong>Column</strong> 6 of&nbsp;10</p>
    <div class="ag4"><p><strong>Column</strong> 3 of&nbsp;6</p></div>
    <div class="ag5"><p><strong>Column</strong> 3 of 6&nbsp;(omega)</p></div>
    <div class="ag6"><p><strong>Column</strong> 2 of&nbsp;6</p></div>
    <div class="ag7">
      <p><strong>Column</strong> 4 of 6&nbsp;(omega)</p>
      <div class="ag8"><p><strong>Column</strong> 2 of&nbsp;4</p></div>
      <div class="ag9"><p><strong>Column</strong> 2 of 4&nbsp;(omega)</p></div>
      <div class="ag10"><p><strong>Column</strong>&nbsp;auto</p></div>
    </div>
  </div>
  <div class="ag3"><p><strong>Column</strong> 2 of 10&nbsp;(omega)</p></div>
</figure>
<!-- Include a grid built with SUSY? -->
<!--  ex. Greg and I developing our own patterns, mixins-->

---
section: Why Compass?
title: Grid code

<pre class="prettyprint" data-lang="scss">
.ag1 { @include span-columns(2,10); }
.ag2 { @include span-columns(6,10); }
.ag3 { @include span-columns(2 omega, 10); }
.ag4 { @include span-columns(3,6); }
.ag5 { @include span-columns(3 omega,6); }
.ag6 { @include span-columns(2,6); }
.ag7 { @include span-columns(4 omega,6); }
.ag8 { @include span-columns(2,4); }
.ag9 { @include span-columns(2 omega,4); }
</pre>

or "semantic" code

---

section: Why Compass?
title: Other Grids

- [Compass Blueprint](http://compass-style.org/reference/blueprint/grid/)
- [Baseline CSS grid](http://baselinecss.com/)
- [Drupal Zen](http://github.com/bangpound/compass-drupal-zen-plugin)
- [The Semantic Grid System](http://semantic.gs/)
- [Golden Grid System](http://goldengridsystem.com/)

---
section: Why Compass?
title: Spriting
class:

Our file structure:
<pre>
  img
    |--social
       |--- fb.png
       |--- tw.png
       |--- li.png
</pre>

---
section: Why Compass?
title: Spriting
class:

<!-- A folder of images,  -->

<pre class="prettyprint" data-lang="scss">
  .social {
  @import "social/*.png";
  @include all-social-sprites;
  }
</pre>

<pre class="prettyprint" data-lang="css">
  .social-sprite,
  .social-fb,
  .social-tw,
  .social-li   { background: url('/img/social-s34fe0604ab.png') no-repeat; }

  .social-fb   { background-position: 0 -32px; }
  .social-tw    { background-position: 0 -64px; }
  .social-li   { background-position: 0 -96px; }
</pre>

<!-- You can easily swap out sprites without having to resprite the whole image  -->

---
title: Onward and Upward
class: segue
<!-- Let's get practical :)  -->
---
title: Using Compass
build_lists:true

- Baby Steps: you can use as much or as little as you need
- Build your own workflow/mixin library
- Be amazed at the time you save

---
title: Resources

- [http://thesassway.com/](http://thesassway.com/)
- [http://chriseppstein.github.com/](http://chriseppstein.github.com/)
- [Compass-project.org](compass-project.org)
- [CSS-Tricks on sass](http://css-tricks.com/search-results/?q=sass)
- [#sass on Stack Oveflow](www.stackoverflow.com)
