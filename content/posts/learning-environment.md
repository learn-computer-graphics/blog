---
author: "Guillaume Haerinck"
title: "Making a feature-rich environment through Jupyter Notebooks"
date: "2022-11-02"
summary: "Analysis and description of our organization technical architecture"
tags: ["iframe", "jupyter"]
ShowToc: true
---

> Analysis and description of our organization technical architecture

## Our prerequisites

The *Learn Computer Graphics* organization aims to store computer science knowledge into a friendly visual format that can be picked-up anytime as a refresher. We view this as a long-term project so it is crucial for our content to stay **modern**, mobile-friendly, and **easy to maintain**. Whenever we want to deal with a new subject it should have a clean separation with the other ones so that it can be **worked-on independently**.

When looking for a piece of information there can be a lot of noise surrounding it. You can be lost between the resources, each one using its style and language with a varying degree of quality. We believe that if our website stays consistent by abiding to an unified look and a **common page structure** it should be straightforward to find what you are looking for. Less time lost to search is more time to think 🥸 !

Another central point is for our content is to be **trustworthy**. Multiple solutions can be applied such as always **providing the sources** to our explanations, use a **peer-review process** and allow any user to **raise an issue**. When dealing with experimental results such as diagrams or interactive exemples, the code has to be provided and easy to run so that it is reproducible in a controlled environment.

## Independent projects under the same banner

[Jupyter Notebooks](https://jupyter.org/) is a powerful ecosystem that filled most of our prerequisites right away. It is well known by researchers working with the python language as it provide an **easy framework to mix code and explanations** within the same page. While we were heavily inspired by the [Nature of code](https://natureofcode.com/book/chapter-1-vectors/) by Daniel Shiffman, the versatility of the notebooks finally got us in.

### Easy maintenance

Given its popularity and the other child projects it is spawning we believe that it won't go away soon.

- CI
- Markdown
- valid in a few years
- custom server, no github.io

### Unified look

- The blog to tie them all
- Usage of subdomains for each project
- Independent repository for each subject, and use of blog to glue them all into one website

### Testable content

- testable widget -> python
- interactive environment -> notebook and iframes
To have access to a python interpreter means that it is also easy to **generate diagrams from code** with the help of [matplotlib](https://matplotlib.org/) or similar other libraries. 

## Limit-less embedding

- Usage of iframe inside of notebook to display about anything, and be independent from version breaks
- A dependency repo hidden from public to get js dependencies

## Wanted list

- C++ kernel
- Better support for iframe (pull request ongoing)
