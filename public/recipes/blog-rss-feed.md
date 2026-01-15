# How to generate an RSS feed file of your site

This recipe shows how to automatically generate an RSS feed for your blog.

## Overview

In the same way you might iterate over a list of posts on your blog’s index page, this file will iterate over all the posts in your blog, generating an item for each one. This snipped assumes that your blog posts are in a `_data.json` file in a `blog/` directory. If this is not the case for your site, feel free to modify it to suit your needs.

## `feed.xml.jade` or `feed.xml.ejs`

All we need is a `feed.xml.jade` file if you’re using Jade, or `feed.xml.ejs` if you prefer EJS.

The naming of the file is important. The `xxx.xml.xxx` tells Harp that you want that file to be served as XML, which is the RSS format. Learn more about this on the [Rules section](/docs/development/rules) under “Dead simple asset pipeline.”

## RSS Feed script

### The flexible metadata

Harp permits [flexible metadata](/docs/development/metadata), so your data might be named differently. For this example, the blog metadata in in `blog/_data.json` and is structured like this:

```json
{
  "my-first-post": {
    "title": "My post title",
    "date": "2013-01-01 PDT"
  },
  "my-second-post": {
    "title": "My second post",
    "date": "2013-02-02 PDT"
  }
}
```

If you have used different names for your posts’ titles or dates, just modify them accordingly in the following snippet. 

The snippet also assumes you have some information about your site as [Global variables](/docs/development/globals) in your in your `harp.json` or `_harp.json`:

```
{
  "globals": {
    "title": "My blog",
    "description": "This is where I write things",
    "url": "http://example.com"
  }
}
```

You can either add these items to your Global variables, or rename or replace them in the following code.

### Using Jade

Create a new file named `feed.xml.jade` and copy/paste the snippet below:

```jade
doctype xml
rss(version="2.0", xmlns:atom="http://www.w3.org/2005/Atom")
  channel  
    title= title
    link= url
    description= description
    atom:link(href="#{ url }/feed.xml", rel="self", type="application/rss+xml")
    for post, slug in public.blog._data
      item
        title= post.title
        description <![CDATA[!{ partial(slug) }]]>
        pubDate= new Date(post.date)
        link #{ url }/blog/#{ slug }
        guid(isPermaLink="true") #{ url }/blog/#{ slug }
```

If you’re using a [Layout](/docs/development/layout) `_layout.jade` file, it will wrap this `feed.xml.jade` file, causing errors. Create a `_data.json` file in the same directory you’ve placed the `feed.xml.jade` file, to opt out of a layout:

```json
{
  "feed": {
    "layout": false
  }
}
```

### Using EJS

Create a new file named `feed.xml.ejs` and copy/paste the snippet below:

```ejs
<?xml version="1.0" encoding="UTF-8"?>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title><%- title %></title>
    <link><%- url %></link>
    <description><%- description %></description>
    <atom:link href="<%- url %>/feed.xml" rel="self" type="application/rss+xml" />
    <% for(slug in public.blog._data) { %>
    <% var post = public.blog._data[slug] %>
      <item>
        <title><%- post.title %></title>
        <description><![CDATA[<%- partial("blog/" + slug) %>]]></description>
        <pubDate><%- new Date(post.date) %></pubDate>
        <link><%- url %>/blog/<%- slug %></link>
        <guid isPermaLink="true"><%- url %>/blog/<%- slug %></guid>
      </item>
    <% } %>
  </channel>
</rss>
```

If you’re using a [Layout](/docs/development/layout) `_layout.jade` file, it will wrap this `feed.xml.ejs` file, causing errors. Create a `_data.json` file in the same directory you’ve placed the `feed.xml.ejs` file, to opt out of a Layout:

```json
{
  "feed": {
    "layout": false
  }
}
```

## How does it work?

By iterating over the metadata in your `_data.json` file, you can create this RSS template just as you might create a list of your posts on a blog index page. By using [variables that you store in your `harp.json` file](/docs/development/globals), you can make sure that if anything changes, it will be easy to update everywhere at once.
