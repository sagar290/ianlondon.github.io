---
title: "Configuration"
permalink: /docs/configuration/
excerpt:
sidebar:
  title: "v3.0"
  nav: docs
---

{% include base_path %}

Settings that affect your entire site can be changed in [Jekyll's configuration file](https://jekyllrb.com/docs/configuration/): `_config.yml`, found in the root of your project.

**Note:** for technical reasons, `_config.yml` is NOT reloaded automatically when used with `jekyll serve`. If you make any changes to this file, please restart the server process for them to be applied.
{: .notice--warning}

Take a moment to look over the configuration file included with the theme. Light comments have been added to provide examples and defaults values for most variables. Detailed explanations of each can be found below.

## Site Settings

### Site Locale

`site.locale` is used to declare the primary language for each web page within the site.

*Example:* `locale: "en-US"` sets the `lang` attribute for the site to *United States* flavor of English, while `en-GB` would be for the `United Kingdom` style of English. Country codes are optional and the shorter `locale: "en"` is also acceptable. To find your language and country codes check this [reference table](https://msdn.microsoft.com/en-us/library/ee825488(v=cs.20).aspx). 

Properly setting the locale is important for associating localized text found in the **UI Text** data file. For more information on that see below.

### Site Title

The name of your site. Is used throughout the theme in places like masthead and `<title>` tags.

*Example:* `title: "My Awesome Site"`

You also have the option of customizing the character used in SEO-friendly page titles.

*Example:* `title_separator: "|"` would produce page titles like `Sample Page | My Awesome Site`.

### Site Name

Used to assign a site author. Don't worry, you can assign different authors on specific posts, pages, or collections if you desire.

*Example:* `name: "Michael Rose"`.

**ProTip:** If you want to get crafty with your YAML you can use [anchors](http://www.yaml.org/spec/1.2/spec.html#id2785586) to reuse values. For example `foo: &var "My String"` allows you to reuse `"My String"` elsewhere in `_config.yml` like so... `bar: *var`. You'll see a few examples of this in the provided Jekyll config.
{: .notice--info}

### Site Description

Fairly obvious. `site.description` describes the site. Used predominantly in meta descriptions as part of SEO efforts.

*Example:* `description: "A flexible Jekyll theme for your blog or site with a minimalist aesthetic."`

### Site URL

The base hostname and protocol for your site. If you're hosting with GitHub Pages this will be something like `url: "http://github.io.mmistakes"`, or for self-hosting `url: "https://mademistakes.com"`.

**Note:** It's important to remember that when testing locally you need to change this. Ideally you'd use [multiple config files](https://mademistakes.com/articles/using-jekyll-2016/#environments-and-configurations) to override settings, but simply commenting out the line works as well `# url: "http://mmistakes.github.io"`. Just remember to uncomment it before pushing or else you'll have broken assets and links all over the place!
{: .notice--warning}

**ProTip:** GitHub serves pages over `http://` and `https://` so to take advantage of that go protocol-less like so `url: "//github.io.mmistakes"`.
{: .notice--info}

### Site Base URL

This little option causes all kinds of confusion in the Jekyll community. If you're not hosting your site as a GitHub Pages Project or in a subfolder (eg: `/blog`), then don't mess with it.

In the case of the Minimal Mistakes demo site it's hosting on GitHub Pages at <https://mmistakes.github.io/minimal-mistakes>. To correctly set this base path I'd use `url: "https://mmistakes.github.io"` and `baseurl: "/minimal-mistakes"`.

For more information on how to properly use `site.url` and `site.baseurl` as intended by the Jekyll maintainers, check [Parker Moore's post on the subject](https://byparker.com/blog/2014/clearing-up-confusion-around-baseurl/).

**Note:** When using `baseurl` remember to include it as part of your path when testing your site locally. Values of `url: ` and `baseurl: "/blog"` would make your local site visible at `http://localhost:4000/blog` and not `http://localhost:4000`.
{: .notice--warning}

### Site Default Teaser Image

To assign a fallback teaser image used in modules like the "**Related Posts**" module, place a graphic in the `/images/` directory and add the filename to `_config.yml` like so:

```yaml
teaser: "500x300.png"
```

This image can be overridden at anytime by applying the following to a document's YAML Front Matter.

```yaml
header:
  teaser: my-awesome-post-teaser.jpg
```

<figure>
  <img src="{{ base_path }}/images/mm-teaser-images-example.jpg" alt="teaser image example">
  <figcaption>Teasers images as shown in the grid archive view for related posts.</figcaption>
</figure>

### Breadcrumb Navigation (Beta)

Enable breadcrumb links to help visitors better navigate deeply structure sites. Because of the fragile method of implementing them they don't always produce accurate links reliably. For best results:

1. Use a category based permalink structure e.g. `permalink: /:categories/:title/`
2. Manually create pages for each category or use a plugin like Jekyll Archive to auto-generate. If these pages don't exist breadcrumb links to them will be broken.

![breadcrumb navigation example]({{ base_path }}/images/mm-breadcrumbs-example.jpg)

```yaml
breadcrumbs: true  # disabled by default
```

Breadcrumb start link text and separator character can both be changed in the UI Text data file.

### Reading Time

Enable estimated reading time snippets with `read_time: true` in YAML Front Matter. 200 has been set as the default words per minute, which can be changed by adjusting `words_per_minutes: 200` in `_config.yml`.

![reading time example]({{ base_path }}/images/mm-read-time-example.jpg)

Instead of adding YAML Front Matter to each document apply defaults in `_config.yml`. To enable the **reading time** snippet for all posts:

```yaml
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      read_time: true
```

If you add `read_time: false` to a post's YAML Front Matter it will override the default and disable it for just that post.