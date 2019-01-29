---
layout: home
title: revtools
description: Tools for Evidence Synthesis in R
---
# Tools for Evidence Synthesis in R

<code>revtools</code> is an R package to support researchers working on evidence synthesis projects. It provides a free, easy-to-use, open-source environment to conduct your literature review or meta-analysis. You can use it to visualise patterns in bibliographic data, interactively select or exclude individual articles or words, and save the results for later analysis.

You can get it from <a href="https://cran.r-project.org/package=revtools" target="_blank" rel="noopener">CRAN</a>, download the development version from <a href="https://github.com/mjwestgate/revtools" target="_blank" rel="noopener">GitHub</a>, or read about it in <a href="https://doi.org/10.1101/262881" target="_blank" rel="noopener">this pre-print on bioarxiv</a>.


## What is evidence synthesis?
Evidence synthesis is the process of searching, collating and interpreting scientific information. Of course, this definition covers a whole range of possible  activities, from simple literature searches on a single topic or question, right through to a full systematic review or meta-analysis. Whatever their goal, however, many researchers are finding it increasingly difficult to keep track of the amount of literature that they must read to gain an overview of a given research field. This is where <code>revtools</code> can help.

In practical terms, <code>revtools</code> provides some simple functions for importing and managing 'bibliographic' data; i.e. lists of books or articles, when they were published, and who they were authored and published by. Rather than just import these data, however, <code>revtools</code> also includes a number of functions to help you interactively sort and categorize that content. These functions are built using the R package <code>Shiny</code>, and support a range of tasks from manually sorting article titles or abstracts, right through to automated cluster identification using topic models. By default, each interface hides identifying information of each article, meaning that <code>revtools</code> is consistent with the screening guidelines for systematic reviews given by <a href="https://www.cochrane.org" target="_blank" rel="noopener">Cochrane</a>, the <a href="https://campbellcollaboration.org" target="_blank" rel="noopener">Campbell Collaboration</a>, or the <a href="http://www.environmentalevidence.org" target="_blank" rel="noopener">Collaboration for Environmental Evidence</a>.


<img align="left" height="120" src="/assets/img/revtools_hex.png"> <b>Citation</b>  
If you use <code>revtools</code> in your research, please cite it as:

<font color="black">Westgate, M.J. (2018) revtools: Tools for Evidence Synthesis. R package version 0.3.0, <a href="https://CRAN.R-project.org/package=revtools" target="_blank" rel="noopener">https://CRAN.R-project.org/package=revtools</a></font>
<br>