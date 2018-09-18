---
layout: user_manual
title: manual screening
---
<head>
  <!-- Global site tag (gtag.js) - Google Analytics -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=UA-121833450-2"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());

    gtag('config', 'UA-121833450-2');
  </script>
</head>

# Manual screening
In the systematic review community, the standard method to sort scientific material (such as articles and reports) is via manual screening. In general, this screening process is split into several stages: first titles are screened and the relevant articles kept; then the abstracts are screened for retained articles to see which of those may still be useful; and finally full-text articles are screened. <code>revtools</code> currently supports title and abstract screening only.

## Title screening
Title screening is achieved using the function <code>screen_titles</code>. You can run this function without any commands to launch the app in 'empty' mode, allowing you to load data via the 'browse' button; or with an object of class <code>bibliography</code> or <code>data.frame</code>.

## Abstract screening
Abstract screening is achieved using the function <code>screen_abstracts</code>. Unlike <code>screen_titles</code>, <code>screen_abstracts</code> only shows data for one article at a time.