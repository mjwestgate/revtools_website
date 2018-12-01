---
layout: user_manual
title: Screening with topic models
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

# Screening with topic models

The main way to investigate the results of a topic model in revtools is via the command screen_topics.

You can run this with or without data; e.g.

## Selecting data
[How to choose what data to include in the model & what column to group by]


## Background
<code>make_DTM</code>, which takes a vector of strings and performs the following transformations on it:

1. converts all text to lower case
2. removes punctuation, 'stop words' (defaulting to <code>tm::stopwords</code>) and numbers
3. performs stemming on all words (warning: requires the <code>SnowballC</code> package)
4. removes all words with <3 letters, <5 appearances, or that are in <1% of documents
5. replaces stemmed words with the most common 'full' version of that word in the corpus

As these are all quite standard transformations in text mining, calling <code>make_DTM</code> can save you some time over performing these transformations manually.

Topic models are a relatively robust, accepted method for text classification.

Once you have calculated your DTM, you can construct a topic model by passing it directly to the functions in the <code>topicmodels</code> package (i.e. <code>LDA</code> or <code>CTM</code>), or via the wrapper function <code>revtools::run_LDA</code>. Either way the object returned is the same.

The defaults are not set to be the most statistically rigorous approach. In particular, 5 topics is unlikely to be optimal for any but the smallest corpora.

## Interpreting diagrams
screen_topics includes three kinds of plots. All of these are drawn using plotly for added interactivity.

The scatterplot that you see by default is calculated using ade4 and drawn using plotly.

The barplot on the right of the window shows the number of entries in each topic

Finally, the barplot that you can find under display > words shows the weight of the top X words in each topic.

## Screening
You can select or exclude any article or topic. Excluding by topic is risky. Excluding individual words will increase the rigour of your approach, but probably won't make a great deal of difference to the fit unless there are very common or influential words in the corpus. For example if your abstracts contain information on publishers, and those publishers differ in the nature of the content that they publish, then their names might acquire high weight in the topic model.

<a href="/user_manual/5_manual_screening.html">Previous: Manual screening</a> | <a href="/user_manual/7_examples.html">Next: Examples</a>