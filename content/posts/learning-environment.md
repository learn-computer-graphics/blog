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

The *Learn Computer Graphics* organization aims to store computer science knowledge into a friendly visual format that can be picked-up anytime as a refresher. As a long term project we need to put some rules in place so that we **keep our goals in focus**. 

*Let's review them* 🥸.

### Stay sharp

Given that we're in for a long time, it is crucial for our content to stay **modern**, mobile-friendly, and **easy to maintain**. It's always tempting to deal with something fresh, and there is no reason to restrict that. Whenever we want to handle a new subject it should have a clean separation with the other ones so that it can be **worked-on independently**.

One point that drove us to make this site was to reduce the noise induced by browsing through multiple websites. When you look for something, it is easy to get lost between the resources, each one using its style and language with a varying degree of quality. We believe that if our content stays consistent by abiding to an unified look and a **common page structure** it should be straightforward to find what you are looking for (or be aware that it's not there). Less time lost to search is more time to think !

### Be open

We have to create the right environment to produce **trustworthy** articles. Multiple solutions can be applied but they can be summed up by "openness".

Our content should always **provide adequate sources** following any explanations. Each production should ideally go through a **peer-review process** and we have to allow any user to **raise an issue** if he find mistakes while reading. When dealing with experimental results such as diagrams or interactive exemples, the code has to be provided and easy to run so that it is reproducible in a controlled environment.

## Independent projects under the same banner

[Jupyter Notebooks](https://jupyter.org/) is a powerful ecosystem that filled most of our prerequisites right away. It is well known by researchers working with the python language as it provide an **easy framework to mix code and explanations** within the same page. While we were heavily inspired by the [Nature of code](https://natureofcode.com/book/chapter-1-vectors/) by Daniel Shiffman, the versatility of the notebooks finally got us in.

### Easy maintenance

First of all, it's **easy to get and run** : install python, get [jupyterlab](https://jupyter.org/) with pip and execute the book. It can either render markdown files - an awesome and simple text format - or custom `.ipynb` interactive notebook format. The raw notebook file is not easy to read, but given its popularity many text editor can render it right away. We believe that **it's not going away anytime soon**.

As we want our content to be accessible through a website, we **build those notebooks as web pages** using [jupyter-book](https://jupyterbook.org/en/stable/intro.html). We only provide a "table of content" file so that the command knows what to build and then it's just one keypress away to get a running website from our notes. Given that there is **almost no settings to set**, our content can be updated alongside the new version of these tools for the years to come.

The source of our content is publicly hosted on [Github](https://github.com/learn-computer-graphics) so we get a few features for free. It's easy to add contributors to our organization, easy for anyone to open an issue if they find a mistake, and easy to get the code from anywhere without restriction.

We also use **continuous integration** with [Github actions](https://github.com/features/actions). These are simple scripts that can be triggered under certain conditions. In our case we build the notebooks as a website and update it on our custom server anytime someone push a change. We used-to use [Github pages](https://pages.github.com/) as a web-server, but as the performance were poor we prefered to rent a web-server for ourselves.

### Unified look

Each subject is handled in a separate Github repository (Maths, AI, Graphics, etc) and **built into separate websites**. This approach has several advantages, such as limiting the total size, dependencies and being easier to reason about. As they are all powered using the same technology, they **still look and feel the same when navigating**. However we wanted to be able to switch between each book easily, and for that we needed another solution.

Hence we **created this blog to tie all of our content**. A blog is useful to make a one-shot about something and given that it serves a different purpose than notebooks we could make it with another technology. The idea is to use it as landing page and then embed each books under its category using `iframe` html tags. **The top navigation bar always stay visible, but what's below changes dynamically**. The whole setup is hidden to the visitor who's just browsing through the website.

![iframe structure](/img/iframe.webp)

In terms of performance it **worked well on the phones** we tested. As we host all of the websites under in the same server - only relying on subdomains to redirect to each ones - there is not much indirections. In any case we put a message at the start of each notebook to access the site directly without going through the embeding process (it is always `https://`*category-name*`.learn-computer-graphics.com/`. For exemple with [maths](https://mathematics.learn-computer-graphics.com/)).

Displaying our books through iframes also means that most of the **hyperlinks only works if you open them in a new window/tab** (it is a security used by web browsers to prevent websites from stealing content). So we have to make this the default behavior for every links inside notebooks content (it is [in progress](https://github.com/executablebooks/sphinx-book-theme/pull/626)).

### Testable content

The killer-feature of notebooks is that they are able to **show python code to your reader, execute it and display the result**. Whenever you need to use an equation, your can explain it step by step and demonstrate that it works by displaying the result. It is even possible to **generate diagrams** from your code with the help of [matplotlib](https://matplotlib.org/). Some libraries (such as [plotly](https://plotly.com/python/)) even allows you to display interactive 3D figures.

While the environment is powerful, it is mostly limited to the python ecosystem. It's easy to miss some other libraries made for the web in javascript. We could have created a [language kernels](https://jupyter-client.readthedocs.io/en/stable/kernels.html) or made similar [modifications](https://jupyter-notebook.readthedocs.io/en/stable/examples/Notebook/JavaScript%20Notebook%20Extensions.html) to run our javascript, yet we prefer not to as those kind of changes are very likely to break with a version update. Instead we picked the easier path : **embed webpage in notebooks using `iframe` with built-in IPython methods** (example below).

{{< iframe "https://deps.learn-computer-graphics.com/libs/blueprint-ue-viewer/" >}}

This way we can use [p5](https://p5js.org/) to render small games or even show Unreal Engine Blueprints with [BlueprintUE](https://blueprintue.com/). We host these libraries in a custom subdomain so that we are free from potential version breaks. The only annoyance is that **jupyter-book build will not move our `.html` pages to embed into the build folder**, so by default they will be missing from the server. We added the bash command below to our github actions in order to copy them to the build folder.

`find . -name '*.html' ! -path './_build/*' | cpio -pdm './_build/html/'`

## Wanted list

- C++ kernel
- Online interactive ipywidget https://ipywidgets.readthedocs.io/en/stable/
