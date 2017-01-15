+++
categories = ["math"]
comments = true
date = "2016-10-02T15:59:13-04:00"
draft = false
showpagemeta = true
showcomments = true
slug = ""
tags = ["mathjax", "math", "latex"]
title = "MathJax"
description = "Beautiful math in all browsers"

+++

One of the primary reason I switch to *hugo* is the the fact that I can write markdown files that will get formated and converted to static html files. The second reason is the ability to include `$ TeX Code $` style equations using mathjax.

#### MathJax
This is what they have on the mathjax website and its true [https://www.mathjax.org/](https://www.mathjax.org/)

<blockquote>
Beautiful math in all browsers. A JavaScript display engine for mathematics that works in all browsers. No more setup for readers. It just works.
</blockquote>

#### Setup MathJax with hugo

- All you need to know how to set up MathJax is here https://gohugo.io/tutorials/mathjax/
- include the following script tag in to your site

```js
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/
MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

- Start writing some math equations

<div>$$G_{\mu\nu} + \Lambda g_{\mu} = \frac{8 \pi G}{c^{4}}T_{\mu\nu}$$</div>


```   
    G_{\mu\nu} + \Lambda g_{\mu\nu}=\frac{8\pi G}{c^{4}}T_{\mu\nu}
```

- Inline equations:  `\( f(x) = sin(x^2) \)`

```
    `\( f(x) = sin(x^2) \)`
```
