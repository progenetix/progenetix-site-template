---
title:  "Website: Directories and Files"
permalink: /howto/templatefiles/
layout: default
date:   2019-03-14
author: "@mbaudis"
excerpt_link: https://progenetix.github.io/progenetix-site-template/howto/templatefiles/
excerpt_separator: <!--more-->
category:
  - howto
tags:
  - Jekyll
  - documentation
  - website
  - FAQ
  - Markdown
---

## {{page.title}}

The _Progenetix Jekyll template_ modifies the standard Jekyll file structure.

<!--more-->

<!--
This page is updated at the "excerpt_link" location linked in the header.
-->

Generally, "_underscore" directories contain specific support files are not evaluated for website content. The exception here are collection directories; however, in standard configuration this would only be the `_posts` directory. This behavior has been modified (see also inline documentation in the `_config.yml` file).

* `_data`
    - special directory for e.g. JSON data files, if needed (see [Jekyll](https://jekyllrb.com) documentation)
    - optional
* `_includes`
    - special directory for page elements etc., if needed (see [Jekyll](https://jekyllrb.com) documentation)
    - optional
* `_layouts`
    - directory for one or more layout pages which are used as templates when processing the Markdown or HTML files
    - the corresponding layout is selected in the page's YAML header
    - layout contain a mix of HTML and _Liquid_ instructions
    - the Progenetix template project uses a single `default.html` template file
* `_site`
    - a directory generated when locally serving the site; can be ignored (except for debugging)
    - should be added to  `.gitignore`
* `_templates`
    - templates for individual pages and for category etc. listing pages
    - the "_underscore.md" files are the listing page templates which are being used by the `bootstrap_site.pl` site creation script
* `_tools`
    - e.g. containing the `bootstrap_site.pl` site creation script, which should be run for site setup and after changes to the `_config.yml` configuration file
* `assets`
    - a static directory containing resource files (images, css, js ...)
    - this is directly copied to the root of the website; so files can be statically linked
    - the internal structure is flexible
* `categories`
    - created by the `bootstrap_site.pl` script
    - contains per category listing pages, based on the entries in `_config.yml`
    - please do not add/modify the content; this would be overridden
    - changes should be applied to the template files and/or `_config.yml`, with subsequent running of `bootstrap_site.pl`
* `tags`
    - as for `categories`
* `pages`
    - the root directory for directly adding pages or "collections" of Markdown (or HTML) files, to be processed for the website
    - directories inside have to be registered as "collections" in `_config.yml` (see there), but with a leading "\_" for the directory
    - the `/pages/_posts/` directory is special, in that it requires date-prefixed page names (`2019-03-14-the-weather-today.md`)
    

#### Additional root directories
    
One can add any number of directories to the project root. Their behaviour in the context of the website depends on naming and content:
    
* Any `_underscore` directory will be ignored, if it is not one of the special cases described below. It will *not* be copied to the website. A typical case would be to use a `_drafts` directory.
* Standard `directory-name` directories will be copied top the website's root. Markdown files in them will *not* be interpreted by the Jekyll parser, even if having a YAML header. 
* However, standard directories specified in the `include` directive in `_config.yml` will be interpreted, though it is a good practice to limit those to the `tags` and `categories` directories, which contain the respective listing pages.
    
