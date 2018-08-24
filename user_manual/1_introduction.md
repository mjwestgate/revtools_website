---
layout: user_manual
title: Introduction
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

# Introduction

<code>revtools</code> is an R package to support researchers working on evidence synthesis projects. It provides a free, easy-to-use, open-source environment to conduct your literature review or meta-analysis.

Evidence synthesis is the process of searching, collating and interpreting scientific information. Of course, this definition covers a whole range of possible  activities, from simple literature searches on a single topic or question, right through to a full systematic review or meta-analysis. Whatever their goal, however, many researchers are finding it increasingly difficult to keep track of the amount of literature that they must read to gain an overview of a given research field. This is where <code>revtools</code> can help.

In practical terms, <code>revtools</code> provides some simple functions for importing and managing 'bibliographic' data; i.e. lists of books or articles, when they were published, and who they were authored and published by. Rather than just import these data, however, <code>revtools</code> also includes a number of functions to help you interactively sort and categorize that content. These functions are built using the R package <code>Shiny</code>, and support a range of tasks from manually sorting article titles or abstracts, right through to automated cluster identification using topic models. By default, each interface hides identifying information of each article, meaning that <code>revtools</code> is consistent with the screening guidelines for systematic reviews given by the <a href="https://www.cochrane.org">Cochrane</a> or <a href="https://campbellcollaboration.org">Campbell</a> Collaborations, or the <a href="http://www.environmentalevidence.org">Collaboration for Environmental Evidence</a>.

This manual provides an overview of the key functions and apps available in <code>revtools</code>, and gives some examples of how you might want to use them in practice. If you choose to use <code>revtools</code> in your research, please cite it as:
Westgate, MJ (2018) revtools: Tools for Evidence Synthesis. R package version 0.3.0, https://CRAN.R-project.org/package=revtools

Thanks for trying <code>revtools</code>, and I hope you find it useful in your research.

Martin Westgate
Maintainer, revtools
August 2018