---
title: "Papermod - How To's Guide"
summary: FAQs
date: 2020-09-18T11:30:03+05:30
showtoc: true
tocOpen: true
aliases: ["/papermod-how-to-guide"]
tags: ["PaperMod"]
author: "Aditya Telange"
draft: true
---

## Intro

We'll be using `yml/yaml` format for all examples down below, I recommend using `yml` over `toml` as it is easier to read.

---

## Override theme template

By Hugo's Lookup Order, you can override any part of a theme that you want. The following is a quick example.

Let's say you wish the `list` was different. All you have to do is copy the `list` template:

```shell
your-site/themes/papermod/layouts/_defaults/list.html
```

And paste it under your own `layouts` folder:

```shell
your-site/layouts/_defaults/list.html
```

Then you're free to make any changes you want to the `list`.
When Hugo builds your site, your copy of `list.html` will be used instead of the theme's `list.html`.

---

## Enable Social-Metadata and SEO

These include OpenGraph, Twitter Cards and Schema.

```yml
params:
    env: production
```

or set `HUGO_ENV` as "production" in system env-vars

---

## Archive Page

```shell
.
├── config.yml
├── content/
│   ├── archives.md   <--- Create archive.md here
│   └── posts/
├── static/
└── themes/
    └── hugo-PaperMod/
```

and add the following to it

```yml
---
title: "Archive"
layout: "archives"
url: "/archives/"
summary: archives
---

```

---

## References

-   [Override a Hugo theme](https://zwbetz.com/override-a-hugo-theme/)
