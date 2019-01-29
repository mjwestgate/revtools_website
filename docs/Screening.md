---
layout: default
title: Screening
---
# Manual screening
In the systematic review community, the standard method to sort scientific material (such as articles and reports) is via manual screening. In general, this screening process is split into several stages: first titles are screened and the relevant articles kept; then the abstracts are screened for retained articles to see which of those may still be useful; and finally full-text articles are screened. <code>revtools</code> currently supports title and abstract screening only.

## Title screening
Title screening is achieved using the function <code>screen_titles</code>. You can run this function without any commands to launch the app in 'empty' mode, allowing you to load data via the 'browse' button; or with an object of class <code>bibliography</code> or <code>data.frame</code>. As with <code>screen duplicates</code>, you get the same app - but slightly different behaviour - depending on how you launch it:

```
# 1. standalone; load in data in the app
screen_titles()

# 2. the same, but save back to workspace on exit
result <- screen_titles() # ditto,

data <- read_bibliography("my_data.ris") # load in data

# 3. launch the app using data from the workspace
screen_titles(data)  

# 4. specify an object to return data to
result <- screen_titles(data)
```

Once you've loaded the app using <code>screen_titles</code>, you will see the 'Data' tab open in the dashboard:

<img src="/assets/screenshots/screen_titles_data_tab.png" width="200"/>

These four options work as follows:

<b>Import</b> allows you to drag-and-drop a dataset directly in to the app. If you've loaded <code>screen_titles</code> with data, or you have already added some data, then dragging and dropping here will add the new dataset to the existing one (using <code>merge_columns</code> in the background).

<b>Save Data</b> Allows you to save your progress to a <code>.rds</code> or <code>.csv</code> file.

<b>Clear Data</b> Wipes all data from the app (with a warning first to prevent mistakes).

<b>Exit App</b> closes the app, but also invisibly returns a <code>data.frame</code> to the workspace.


The 'Appearance' tab doesn't affect the data itself, but how it is displayed.

<img src="/assets/screenshots/screen_titles_appearance_tab.png" width="200"/>

This tab has the following options:

<b>Number of articles shown</b> allows you to increase or decrease the amount of information on your screen.

<b>Order citations by</b> enables you to shuffle between the order of the original dataset; alphabetical order by title; and random (set with <code>rnorm</code>).

<b>Hide identifying information</b> is set to TRUE by default, and means only the titles are shown. If set to FALSE, author and journal names are also shown.

Once you have loaded the app and added some data, you will be able to manually select or deselect articles one at a time, or in groups using the 'select all' and 'exclude all' buttons. You can also navigate between pages using the arrow buttons, or choose 'unknown' for ambiguous articles. As you make decisions about which titles to include, the color of the text will update to match your selection.

<img src="/assets/screenshots/screen_titles.png"/>


## Abstract screening
Abstract screening is achieved using the function <code>screen_abstracts</code>. Unlike <code>screen_titles</code>, <code>screen_abstracts</code> only shows data for one article at a time; but the two apps are otherwise identical, with the exception that <code>screen_abstracts</code> allows you to make notes for each article should you wish.

<img src="/assets/screenshots/screen_abstracts.png"/>

<a href="/user_manual/4_removing_duplicates.html">Previous: Removing duplicates</a> | <a href="/user_manual/6_screening_with_topic_models.html">Next: Screening with topic models</a>

# Screening with topic models

The main way to investigate the results of a topic model in revtools is via the command <code>screen_topics</code>. This function behaves similarly to the other apps in this package, but it has many more options.

## Selecting data
If you load <code>screen_topics</code> without any data, it will initially look quite empty:

<img src="/assets/screenshots/screen_topics_initial.png"/>

From here there are a series of stages before you can see the results of your topic model. The first thing you should do is import data via the 'Import' button:

<img src="/assets/screenshots/screen_topics_data_tab_empty.png" width="200"/>

One you have done this, you will be faced with some new options:

<img src="/assets/screenshots/screen_topics_data_tab_full.png" width="200"/>

<b>Show one point per</b> allows you to select what will be displayed by <code>screen_topics</code>. By default this is 'label', which is simply an index giving a unique value for each entry in the dataset, usually corresponding to a single book or article However, you can use this option to plot other interesting information. If, for example, you'd like each point to represent one journal, or one year, then you set that here.

<b>Select included variables</b> shows you a series of checkboxes that correspond to the columns of the underlying <code>data.frame</code>. Selecting a checkbox means that the text in that column will be passed to the the topic model. If you want to run the topic model only on titles, for example, then select 'titles' here; whereas if you'd like to include titles, abstracts and keywords you can select all three.

Once you have selected your data you are ready to go; but you still don't have a plot to work with. To do that you have to use the 'Model' tab.

## Topic model options
The 'Model' tab has only a few options, but they strongly affect the outcome of the plot displayed by <code>screen_topics</code>, as well as how long the code will take to run.

<img src="/assets/screenshots/screen_topics_model_tab.png" width="200"/>

There are three choices:

<b>Model Type</b> currently only supports Latent Dirichlet Allocation (LDA; the default) or Correlated Topic Models (CTMs). From what I've read, CTMs generally fit better, but generate topics that can be harder to distinguish.

<b>Number of topics</b> is a key parameter. There is no 'correct' answer to what the optimal number of topics should be: smaller numbers will give a broad overview but may group unlike concepts; while larger numbers will be more precise but potentially too atomized. Selecting larger number of topics also increases the time taken for the model to calculate.

<b>Number of iterations</b> is ignored for CTMs, but for LDA affects how hard the algorithm looks for an optimal fit. Smaller values will calculate quicker, but will be less reliable. The default (10k iterations) has been chosen as a pragmatic tradeoff between these considerations, and should not be considered ideal.


## Running the topic model
One you hit 'Calculate Model', <code>screen_topics</code> first constructs a Document Term Matrix (DTM) from the specified data, and then runs the function <code>make_dtm</code>. This function performs the following transformations:

1. converts all text to lower case
2. removes punctuation, 'stop words' (defaulting to <code>revwords</code>) and numbers
3. performs stemming on all words (warning: requires the <code>SnowballC</code> package)
4. removes all words with <3 letters, <5 appearances, or that are in <1% of documents
5. replaces stemmed words with the most common 'full' version of that word in the corpus

Once the DTM has been constructed, <code>screen_topics</code> runs the specified topic model. This can take a very long time for large corpora, so don't be surprised if you are waiting a while looking at this screen:

<img src="/assets/screenshots/screen_topics_calculating_modal.png"/>


## Interpreting the plot
Once the topic model has finished running, it generates a plot known as an 'ordination'. The axes on this plot don't have any implicit meaning, and are unlabelled. Instead, points that are closer together are interpreted as containing similar topics, and therefore similar words. If you hover over a point on this plot, it will show you the title of the paper in question, as well as the highest-weighted topic for that article:

<img src="/assets/screenshots/screen_topics_ordination.png"/>

If you click on an article, then further information on that article will be displayed, including an abstract if one is available. You will also be given the option to select or exclude that article, and to make notes:

<img src="/assets/screenshots/screen_topics_article.png"/>

If you would prefer to see information on topics, you can hover over the barplot on the right-hand side of the window. Here you can also select topics by clicking, and to select or exclude whole topics (note in this plot the sidebar has been minimized):

<img src="/assets/screenshots/screen_topics_barplot.png"/>

Finally, it is possible to investigate highly-weighted words in each topic by selecting 'Show Words' from the 'Display' tab:

<img src="/assets/screenshots/screen_topics_display_tab.png" width="200"/>

This will show you the topics barplot, and invite you to select a topic to investigate further.

<img src="/assets/screenshots/screen_topics_words_initial.png"/>

If you select a topic in the bar plot on the right of the screen, you will now be shown a barplot of highly-weighted words in that topic. You can then select and exclude words that you don't want to contribute to your enxt topic model. Alternatively, you can search for words and exclude them manually.

<img src="/assets/screenshots/screen_topics_words_selected.png"/>