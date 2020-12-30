# A simple, basic, grid-based design framework

## What is this?

I built this framework as the final project in the HTML/CSS module of [The Odin Project](https://www.theodinproject.com). I decided to keep it quite minimalistic for starters. The goal was to create something that provides a basic setup at the beginning of a project. This framework is supposed to be open-ended and content will be added, changed, and removed when I use it in the future. Only by building something with it can be seen what works and what doesn't, what is necessary and what isn't.

## What's in it?

1. **CSS reset by Eric Meyer:** I used this one in most of my other projects and am very happy with it. So I copied it into the framework. For information on the version and license (and a link to the author's homepage), see the comment directly in the file.
2. **Variables:** SASS variables for fonts, colors and other stuff. An explanation on how to use them follows below.
3. **General stuff & Typography:** Some general settings that are, I believe, universally useful. This includes setting everything to border-box, giving images a max-width of 100% and setting line-height to the standard 150%. Also, the `<h1>` - `<h6>` elements get a bigger font-size to introduce some visual hierarchy from the start.
4. **Grid-System:** The grid is based on CSS Grid and features 12 columns and two breakpoints. See below on how to use it.
5. **Styles for form-elements:** Some basic styling for buttons and `<input>`-fields.
6. **Utilities:** For now, this section contains only two things: a class for styling lists as navigation and a class for manipulating the aspect ratio of images.

## So, how do I use it?

### Setup & file-structure

You can download and/or fork this repository and get started! Let's take a look at the file-structure:

- design-framework
  - .prettierignore
  - index.html
  - README.md
  - css
    - style.css
    - style.css.map
    - scss
      - \_base.scss
      - style.scss

The index.html is an empty HTML document that gets you started. It already uses style.css as its stylesheet, so you can immediately start writing your HTML.
The style.css and style.css.map are created by SASS. In the scss-directory there are two files: \_base.scss contains the framework. I recommend not to modify it (unless you want to use it as a base for your own framework). The style.scss imports this file via the `@use`-rule and is supposed to contain your custom CSS.
You can ignore the .prettierignore. I use it to disable auto-formatting in \_base.css. Oh, and of course you want to write your own README.md or delete it altogether.

### OK, I know now how it's structured, but how do I acutally use it?

There are two ways to use the framework: Using SASS or not using SASS. I recommend using SASS.

#### Using SASS:

Write your code into style.scss and compile it to style.css. I recommend using the `--watch` feature to automatically compile the SCSS everytime you save. If you open your terminal in the design-framework folder, the command looks like this:

```
sass css/scss/style.scss css/style.css --watch
```

##### Using SASS variables:

By default, \_base.scss is imported to style.scss via the `@use`-rule. This means that the variables in \_base.scss have their own namespace and must be prefixed in order to be used. For example:

```
p {
    color: base.$link-default;
}
```

If you want to reassign a value to a variable, use the `@use with`-syntax:

```
@use "base" with (
    $primary-color: rgb(0, 128, 128),
    $font-serif: 100% 'Times New Roman', Times, serif,
    );
}
```

For further information on how to work with SASS, see the [SASS documentation](https://sass-lang.com/documentation).

#### Not using SASS:

If you don't want to use SASS, I recommend to write your CSS in a separate stylesheet and link to it in index.html below style.css. You may want to delete the scss-folder in that case.

### Using the grid

The grid is based on CSS Grid and features 12 columns and two breakpoints: one "medium" @768px and one "large" @980px.

Give the element that contains your grid-items the class `grid-container`. Each item gets a class that defines how many columns it spans (spanning 1 column is the default. There's no class for that). These classes are:

- `col-2` up to `col-12`: These are the default classes that will apply on all screen resolutions, unless overwritten
- `col-m-2` up to `col-m-12`: These classes apply if the screen width is at least 768px.
- `col-l-2` up to `col-l-12`: These classes apply if the screen width is at least 980px.

Apply classes for each resolution to each grid-item, make sure they add up to a sum of 12, and enjoy the simple, responsive layout that you just created. An example would be:

```
<div class="grid-container">
  <div class="col-12 col-m-6 col-l-9">Some content</div>
  <div class="col-12 col-m-6 col-l-3">Maybe a sidebar</div>
</div>
```

The two elements would sit below each other and span the full width of the container on screensizes up to 767px.
They would sit next to each other and equally divide the space inside the container on screensizes between 768px and 979px.
They would sit next to each other and the first element would take up 75% of the space and the second one 25% on screensizes greater than 980px.

### Using utilities

#### Turning a list into a navigation bar

Simply add the class `nav-list` to the `<ul>` that you want to style as navigation:

```
<ul class="nav-list">
  <li><a href="some-page.html">Link 1</a></li>
  <li><a href="some-other-page.html">Link 1</a></li>
</ul>
```

#### Setting the aspect ratio of images

This utility uses the "padding bottom hack" to display images at a certain aspect ratio. I first read about it [here](https://www.smashingmagazine.com/2013/09/responsive-images-performance-problem-case-study/).

Wrap the image with another element that gets the class `image-wrapper`.

```
<div> <!-- Some sort of container is necessary for the wrapped image -->
  <div class="image-wrapper">
    <img src="some-image.jpg" alt="some description">
  </div>
</div>
```

**Note** that this class uses the variable `$aspect-ratio` that you can also redefine to match a certain aspect ration. The default is 56.25% which corresponds to the ratio 16:9.

**Note** that the element with the class `image-wrapper` needs to be put in some sort of container itself. This is because its height is sized with the `padding-bottom` property, which refers to the width of the _containing_ block. So far, I found this to be unproblematic, since in practice you will have such a container anyway.

## Built with

[SASS](https://sass-lang.com/)
