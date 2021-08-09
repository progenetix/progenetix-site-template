---
layout: default
permalink: /index.html
---

{% comment %}
################################################################################

The template for the index page is thought to provide both the option for
custom content, as well as a mechanism for the automated adding of excerpt
page links for other pages labeled for the "index" category.

Please add your content in Markdown or HTML below.

################################################################################
{% endcomment %}

## Progenetix Jekyll Website Template

Welcome to the Progenetix Jekyll Template.

This is a minimal repository which can be used to build static but "update on modification" websites using the Ruby based "Jekyll" framework.

A typical application here would be to have the root directory as a Github project, in which case Github will process the pages, create the corresponding website and handle updates upon changes. Examples here are e.g. several websites related to the Global Alliance for Genomics and Health ([GA4H](http://ga4gh.org)):

* [schemablocks.org](http://schemablocks.org)
* [ELIXIR Beacon](http://beacon-project.io)
* [ELIXIR Cloud and AAI](https://elixir-europe.github.io/cloud/)
* [GA4GH Discovery](http://ga4gh-discovery.github.io)
* [CompbioZurich](https://compbiozurich.org)
* ...

Alternatively, the site can be build locally (requiring some Ruby gems etc.), for either testing purposes or to serve the compiled site from your own hosting space. Examples here are our sites:

* [info.baudisgroup.org](http://info.baudisgroup.org)
* [internal.baudisgroup.org](http://internal.baudisgroup.org) (internal access only)
* [info.progenetix.org](http://info.progenetix.org) - Progenetix info page

#### External Information

* A nice [introduction into Github + Jekyll website management](https://carpentries-incubator.github.io/jekyll-pages-novice/) at _carpentries_, by Toby Hodges


----

{% comment %}
################################################################################

Below this will page excerpts for pages with the "index" category appear.

################################################################################
{% endcomment %}

{%- assign this_name = "index" -%}
{%- assign this_category = "index" -%}

{%- assign cat_posts = site.emptyArray -%}
{%- for post in site.documents -%}
  {%- if post.categories contains this_category -%}
    {%- assign cat_posts = cat_posts | push: post -%}
  {%- endif -%}
{%- endfor -%}

{%- assign cat_posts = cat_posts | sort: 'date' | reverse -%}

{%- comment -%}
  * special posts for prepending content to the listing pages
  * they are processed first, so separate loops are needed  
{%- endcomment -%}

{% comment %}
################################################################################
	Please keep this for an HTML break...
################################################################################
{% endcomment %}

{%- for post in cat_posts -%}
  {%- if post.tags contains '.prepend' -%}
<div style="margin-bottom: 20px;">
{{ post.content | markdownify }}
</div>
  {%- endif -%}
{%- endfor -%}

{%- comment -%}
  * no separate treatment of featured posts
{%- endcomment -%}

{%- for post in cat_posts -%}
  {% unless post.tags contains '.prepend' or post.tags contains '.append' %}
    {%- assign post_author = post.author | downcase -%}
    {%- assign excerpt_link = post.url | relative_url -%}
    {%- if post.excerpt_link contains '/' -%}
      {%- assign excerpt_link = post.excerpt_link -%}
    {%- endif -%}
<div class="excerpt">
<a href="{{ excerpt_link }}">{{ post.excerpt }}</a>
  <p class="footnote">
    {%- if post.author -%}{{ post.author | join: " | " }}&nbsp;{%- endif -%}
    {%- if post.date -%}{{ post.date | date: "%Y-%m-%d" }}: {% endif %}
 <a href="{{ excerpt_link }}">more ...</a>
  </p>
</div>
  {% endunless %}  
{%- endfor -%}

{%- for post in cat_posts -%}
  {%- if post.tags contains '.append' -%}
<div style="margin-top: 20px;">
{{ post.content | markdownify }}
</div>
  {%- endif -%}
{%- endfor -%}
