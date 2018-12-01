---
layout: user_manual
title: Getting started
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

# Getting Started
<code>revtools</code> is built to perform some useful tasks with as few functions as possible, so you should be able to use it even if you have no coding experience. However, there are a few steps that you will need to take to get it to work.

## Downloading and Installing R
<code>revtools</code> is a package that runs in the <code>R</code> environment; it can't be used by itself. Consequently, the first thing you'll need to do is download and install <code>R</code>.

Before we do that, a quick note on terminology: <code>R</code> is both a program that you can download, and a language that you use to get that program to run. This can be a little confusing for new users, but just stick with me!

You can download <code>R</code> from a couple of different places. Perhaps the easiest option is to use <a href="https://www.rstudio.com" target="_blank" rel="noopener">RStudio</a>, which gives a very stable, familiar-looking statistical interface to the <code>R</code> language. If you'd prefer something simpler, you can get the 'default' version from the <a href="https://cran.r-project.org" target="_blank" rel="noopener">Comprehensive R Archive Network</a>. CRAN are the people who actually build and maintain <code>R</code>, but their user interface is fairly basic, which can be off-putting for some users.

Regardless of which 'type' of <code>R</code> you prefer, it's straightforward to download and install it from either of these sites.

## Installing revtools
Assuming that your installation has worked and you can open <code>R</code>, now you can install <code>revtools</code>. Once you've loaded R, you're faced with the command window. Paste in the following code:

<code>install.packages("revtools")<br>
library(revtools)</code>

That's it! If everything goes well, this should install <code>revtools</code>, as well as all the other software packages needed to get <code>revtools</code> to work. If it doesn't work for some reason, or you want to use the 'development' version, you can try downloading it from GitHub instead:

<code>install.packages("devtools")<br>
install_github("mjwestgate/revtools")<br>
library(revtools)</code>

At this point you should be ready to go.

<a href="/user_manual/1_introduction.html">Previous: Introduction</a> | <a href="/user_manual/3_importing_data.html">Next: Importing data</a>