# CMSimple - A cms that doesn't try that hard.

A simple, directory based cms which helps people execute complex websites with a minimum
amount of cognitive complexity. (We think / hope, anyway.)

## What it is for

Need a marketing site for an application? That's why we originally built this. It
powers our little site, www.vidpresso.com.

When we running Vidpresso, we realized it
was prohibitively difficult to update the marketing site when it was coupled with our main application, and that was really slowing
us down. We did a bunch of research (see prior art) and weren't happy when we tried
to implement any of those solutions on our own. (It's entirely possible we were
too lazy and didn't fully grasp the other solutions, so we encourage you to try
them first.)

We think there are probably other applications too... perhaps personal blogs, or other
types of content sites perhaps. But at it's core, we want users to feel like they
can look at a directory structure, and know exactly what they're going to get on
their website.

## What it isn't for

We really think our app fits small, technically minded teams. Basically, you should
probably be familiar with Markdown, likely YAML / JSON, HTML / template engines
in general, and preferably Node.js / Express.

If you don't know any of those things, this still might be an ok fit for you, but
it's likely you'll want to try something else like Wordpress, Tumblr, or something
else first. (We especially think Tumblr's markdown support is splendid.)

## Prior art

The CMS was built after looking at many differing CMSes, with a preference toward markdown based apps.

  * Wordpress
  * Jekyll
  * Prismic
  * Tumblr
  * Joomla (we really don't like this and don't recommend it.)

The key thing all those apps lack was essentially they're either easy to use,
somewhat customizable, somewhat blog-centric, or somewhat complex. We think what we've
done merges our favorite parts of those platforms together. But you should probably
look at their solutions before using ours, because it's extremely likely they'll
have the features you need, and we won't.

Our design objectives were:

  * Easy to publish / update / change
  * Simple to maintain
  * Simple scaling (Given the simplicity of the app, we think a single instance
    will serve most applications. But if not, horizontal heroku-style scaling.)
  * Simple SEO (multiple content types in the same domain preferably. blog.whatever.com
    should die, in our uninformed opinion.)
  * Multiple content types

## How it works

We've tried to create something at it's core that requires very little overarching
knowledge, and has a predictable, understandable pattern.

Overarching knowledge required:

* Directory structures
* `_schema.md`
* Front matter
* Filenames to URL slugs
* Creating views.

## Directory Structures

Directory structure is king. Directory structure often equates directly with views,
URLs, list pages, etc. Most of the simplicty of the system starts by assuming that
you'll order the stuff you need in folders. We allow for / encourage cross functional
tags, but the primary unit of organization is definitely the directory structure.

`/content` is how you practically design your website's structure. Each folder represents
a content type. Content types describe individual units of content that you'd probably
want to reuse in a bunch of different contexts potentially.

## `_schema.md`

Each contnet type folder in `/content` should contain a file called `_schema.md`.
These files are like starting points for content types. Ideally to create
a new post, you'd duplicate the `_schema.md` file, rename it, and write away.

Schema attempts to standardize YAML-style front-matter at creation. We envision
some command line tool to update front-matter in the future, since it'll be kind
of a pain to individually update each file. However, we think smart, tech savvy
nerdish people would figure this out. (Pull requests / proposals accepted!)

## Front matter

(This concept is inspired / stolen from Jekyll)

Front matter attempts to give structure to each document. Essentially, at the top
of a document, you can define arbitrary metadata that's important to each content
type. For instance, if I were setting up a CMS for a company with multiple products,
I'd probably define the price, a big pretty picture, and perhaps related tags in
the front matter section.

An example from Vidpresso's blog.
```
---
PublishedAt: 2013-11-13 9:00 -0600
Type: Blog Post
Tags: Tag, Tag, Tag
Title: The Secret Vidpresso Master Plan (just between you and me)
MainImage: http://media.vidpresso.com/blog/no_to_racks.jpg
Person: Randall Bennett
---
```

In front-matter you only have one required field: `type`. The `type` field maps
directly to the permalink view that gets used for display. (More on that later.)

## URLs as slugs

Each filename turns into a slug. `/content/people/my-cool-friend.md` -> url: `/people/my-cool-friend`

For chronological (ie blog) content, prefix the filename with a `YYYYMMDD` date.
ie: `/content/blog/20150113_happy-new-year.md` -> url: `/blog/2015/01/13/happy-new-year`

## Views

`/views` never contains content. Ever. Try to almost always splinter content
into `/content`. It's simpler to update, simpler to find, and generally just easier.

Index views are determined by folder name.

## What we're not totally sure of

* We don't really know how subfolders should map in views.

## License

MIT. We try to be permissive about what we do.
