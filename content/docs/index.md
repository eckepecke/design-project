---
Title: Docs
Description: Documentation that came with Pico.
# hidden: true
---

## Welcome to Pico

Congratulations, you have successfully installed [Pico][] %version%.
%meta.description% <!-- replaced by the above Description header -->

## Creating Content

Pico is a flat file CMS. This means there is no administration backend or
database to deal with. You simply create `.md` files in the `content` folder
and those files become your pages. For example, this file is called `index.md`
and is shown as the main landing page.

When you install Pico, it comes with some sample contents that will display
until you add your own content. Simply add some `.md` files to your `content`
folder in Pico's root directory. No configuration is required, Pico will
automatically use the `content` folder as soon as you create your own
`index.md`. Just check out [Pico's sample contents][SampleContents] for an
example!

If you create a folder within the content directory (e.g. `content/sub`) and
put an `index.md` inside it, you can access that folder at the URL
`%base_url%?sub`. If you want another page within the sub folder, simply create
a text file with the corresponding name and you will be able to access it
(e.g. `content/sub/page.md` is accessible from the URL `%base_url%?sub/page`).
Below we've shown some examples of locations and their corresponding URLs:

<table style="width: 100%; max-width: 40em;">
    <thead>
        <tr>
            <th style="width: 50%;">Physical Location</th>
            <th style="width: 50%;">URL</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>content/index.md</td>
            <td><a href="%base_url%">/</a></td>
        </tr>
        <tr>
            <td>content/sub.md</td>
            <td><del>?sub</del> (not accessible, see below)</td>
        </tr>
        <tr>
            <td>content/sub/page.md</td>
            <td><a href="%base_url%?docs/sub/page">?sub/page</a></td>
        </tr>
    </tbody>
</table>

If a file cannot be found, the file `content/404.md` will be shown. You can add
`404.md` files to any directory. So, for example, if you wanted to use a special
error page for your blog, you could simply create `content/blog/404.md`.

Pico strictly separates contents of your website (the Markdown files in your
`content` directory) and how these contents should be displayed (the Twig
templates in your `themes` directory). However, not every file in your `content`
directory might actually be a distinct page. For example, some themes (including
Pico's default theme) use some special "hidden" file to manage meta data (like
`_meta.md` in Pico's sample contents). Some other themes use a `_footer.md` to
represent the contents of the website's footer. The common point is the `_`: all
files and directories prefixed by a `_` in your `content` directory are hidden.
These pages can't be accessed from a web browser, Pico will show a 404 error
page instead.

As a common practice, we recommend you to separate your contents and assets
(like images, downloads, etc.). We even deny access to your `content` directory
by default. If you want to use some assets (e.g. a image) in one of your content
files, use Pico's `assets` folder. You can then access them in your Markdown
using the <code>&#37;assets_url&#37;</code> placeholder, for example:
<code>!\[Image Title\](&#37;assets_url&#37;/image.png)</code>

### Text File Markup

Text files are marked up using [Markdown][] and [Markdown Extra][MarkdownExtra].
They can also contain regular HTML.

At the top of text files you can place a block comment and specify certain meta
attributes of the page using [YAML][] (the "YAML header"). For example:

    ---
    Title: Welcome
    Description: This description will go in the meta description tag
    Author: Joe Bloggs
    Date: 2001-04-25
    Robots: noindex,nofollow
    Template: index
    ---

These values will be contained in the `{{ meta }}` variable in themes (see
below). Meta headers sometimes have a special meaning: For instance, Pico not
only passes through the `Date` meta header, but rather evaluates it to really
"understand" when this page was created. This comes into play when you want to
sort your pages not just alphabetically, but by date. Another example is the
`Template` meta header: It controls what Twig template Pico uses to display
this page (e.g. if you add `Template: blog`, Pico uses `blog.twig`).

In an attempt to separate contents and styling, we recommend you to not use
inline CSS in your Markdown files. You should rather add appropriate CSS
classes to your theme. For example, you might want to add some CSS classes to
your theme to rule how much of the available space a image should use (e.g.
`img.small { width: 80%; }`). You can then use these CSS classes in your
Markdown files, for example:
<code>!\[Image Title\](&#37;assets_url&#37;/image.png) {.small}</code>

There are also certain variables that you can use in your text files:

* <code>&#37;site_title&#37;</code> - The title of your Pico site
* <code>&#37;base_url&#37;</code> - The URL to your Pico site; internal links
  can be specified using <code>&#37;base_url&#37;?sub/page</code>
* <code>&#37;theme_url&#37;</code> - The URL to the currently used theme
* <code>&#37;assets_url&#37;</code> - The URL to Pico's `assets` directory
* <code>&#37;themes_url&#37;</code> - The URL to Pico's `themes` directory;
  don't confuse this with <code>&#37;theme_url&#37;</code>
* <code>&#37;plugins_url&#37;</code> - The URL to Pico's `plugins` directory
* <code>&#37;version&#37;</code> - Pico's current version string (e.g. `2.0.0`)
* <code>&#37;meta.&#42;&#37;</code> - Access any meta variable of the current
  page, e.g. <code>&#37;meta.author&#37;</code> is replaced with `Joe Bloggs`
* <code>&#37;config.&#42;&#37;</code> - Access any scalar config variable,
  e.g. <code>&#37;config.theme&#37;</code> is replaced with `default`

## Documentation

For more help have a look at the Pico documentation at http://picocms.org/docs.

[Pico]: http://picocms.org/
[PicoTheme]: https://github.com/picocms/pico-theme
[SampleContents]: https://github.com/picocms/Pico/tree/master/content-sample
[Markdown]: http://daringfireball.net/projects/markdown/syntax
[MarkdownExtra]: https://michelf.ca/projects/php-markdown/extra/
[YAML]: https://en.wikipedia.org/wiki/YAML
[Twig]: http://twig.sensiolabs.org/documentation
[UnixTimestamp]: https://en.wikipedia.org/wiki/Unix_timestamp
[Composer]: https://getcomposer.org/
[FeaturesHttpParams]: http://picocms.org/in-depth/features/http-params/
[FeaturesPageTree]: http://picocms.org/in-depth/features/page-tree/
[FeaturesPagesFunction]: http://picocms.org/in-depth/features/pages-function/
[WikiThemes]: https://github.com/picocms/Pico/wiki/Pico-Themes
[WikiPlugins]: https://github.com/picocms/Pico/wiki/Pico-Plugins
[OfficialThemes]: http://picocms.org/themes/
[PluginUpgrade]: http://picocms.org/development/#upgrade
[ModRewrite]: https://httpd.apache.org/docs/current/mod/mod_rewrite.html
[AllowOverride]: https://httpd.apache.org/docs/current/mod/core.html#allowoverride
[NginxConfig]: http://picocms.org/in-depth/nginx/
