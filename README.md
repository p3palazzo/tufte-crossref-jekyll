# tufte-mistakes

This is a drop-in set of files for customizing the [Minimal Mistakes]
Jekyll theme with styles and page layouts from the [Tufte Pandoc Jekyll]
theme. This project has been forked from the Tufte Pandoc theme and
tries to keep up with its features and version numbering.

:warning: *This is not a self-contained theme and still requires Minimal
Mistakes to be installed*.

[Minimal Mistakes]: https://mmistakes.github.io/minimal-mistakes/
[Tufte Pandoc Jekyll]: https://github.com/jez/tufte-pandoc-jekyll

## Rationale

One might think, at first, that blending the minimalistic [Tufte CSS] with a
highly structured theme such as Minimal Mistakes would debase both
projects, so why bother? For starters, the Minimal Mistakes framework is
quite flexible and can easily be made very plain—all you have to do is
edit a few data and config files to disable the bells and whistles. Even
then, should you require the occasional frills or the robust support
Minimal Mistakes has for authors, archives, and collections, they are
easy to activate.

## Features

- [Tufte Pandoc CSS] forked from the [Tufte Pandoc Jekyll] theme (requires
  [Pandoc sidenote])
- Sass file structure from [Minimal Mistakes], including the ability to
  customize variables
- Sidenotes and margin notes are expanded only in the `wide` and
  `splash` page classes (see the Minimal Mistakes docs); elsewhere they
  use the toggle button for narrow screens
- Supports utility classes in Minimal Mistakes (use the Pandoc syntax
  `{.text-center}` rather than the Kramdown `{: .text-center}` and so
  on)

[Tufte CSS]: https://edwardtufte.github.io/tufte-css/
[Tufte Pandoc CSS]: https://jez.io/tufte-pandoc-css/
[Pandoc sidenote]: https://github.com/jez/pandoc-sidenote

## Installation

1. Download the repository folder to the root of your project and rename
   it to `_sass` (or add it as a submodule to keep up with future
   updates).
2. Edit `_config.yml` and `Gemfile` in your project as shown below.
3. All dependencies for [Tufte Pandoc Jekyll] and [Minimal Mistakes]
   apply, so check them carefully.

Follow the instructions below from the Tufte Pandoc Jekyll README:

<blockquote>

There are two external dependencies in order to use this theme. You can install
them through your package manager (like `apt-get` or `brew`):

```
# EXAMPLE: This is for macOS. Change if you're on Linux.
# Note: you must have pandoc version 2.0 or greater
brew install pandoc
brew install jez/formulae/pandoc-sidenote
```

</blockquote>

Or feel free to use my docker container that comes preinstalled with
Pandoc, Jekyll, and Pandoc-sidenote:

```
docker run --rm -v "`pwd`:/srv/jekyll" \
  palazzo/jekyll-tufte /bin/bash -c \
  "chmod 777 /srv/jekyll && jekyll build"
```

See the [Jekyll-Docker] project for more details on how to build your
website out of a Docker container.

[Jekyll-Docker]: https://github.com/envygeeks/jekyll-docker/

Next, add this line to your Jekyll site's Gemfile:

```ruby
gem "minimal-mistakes-jekyll"
```

And add these lines to your Jekyll site's `_config.yml`:

```yaml
theme: minimal-mistakes

gems:
  - jekyll-pandoc
```

And then execute:

    $ bundle

## Usage

> Note: while `tufte-pandoc-css` optionally includes the Solarized Light
> colorscheme, it's enabled by default here, with no easy way to opt-out. This is
> probably fine for you, but if it's not, feel free to make a PR that allows
> opting out.

## Sidenotes

By default, sidenotes and margin notes are collapsed in narrow screens
`@media(max-width: 768px)` as well as in regular pages. These notes can
then be expanded by clicking on the target symbol &#8853; placeholder.
See the [Tufte CSS] documentation for further details.

Sidenotes and margin notes will be visible by default when the screen is
wide enough, **but only if** the `wide` class is used in the page's YAML
front matter:

```
---
classes: wide
---
```

You can enable this by default for all pages, or for some pages (say,
for the pages that use the `single` layout), by adding `classes: wide`
to the `defaults` section in the `_config.yml` file. See the Minimal
Mistakes documentation on [layouts and page classes] and on
[front matter defaults].

[layouts and page classes]: https://mmistakes.github.io/minimal-mistakes/docs/layouts/
[front matter defaults]: https://mmistakes.github.io/minimal-mistakes/docs/configuration/#front-matter-defaults

### Customization

See the [Minimal Mistakes Stylesheets] documentation to find out where
to find the variables you might want to customize.

[Minimal Mistakes Stylesheets]: https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/

### `_config.yml`

You'll need to update your `_config.yml` to compile the site using Pandoc. Make
sure you've followed the installation instructions.

```
gems:
  - jekyll-pandoc

markdown: Pandoc
pandoc:
  extensions:
    - section-divs
    - from: 'markdown+tex_math_single_backslash'
    - filter: 'pandoc-sidenote'
```

Optional: remove `section-divs` if you want to insert `<section>` tags manually.

:warning: The automatic table of contents feature included in Minimal
Mistakes is dependent on the Kramdown processor, and therefore will not
work with Pandoc. You will need to generate a table of contents manually
by following [these instructions].

[these instructions]: https://mmistakes.github.io/minimal-mistakes/docs/navigation/#custom-sidebar-navigation-menu

## License

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](https://jez.io/MIT-LICENSE.txt)
