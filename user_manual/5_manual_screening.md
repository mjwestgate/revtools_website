---
layout: user_manual
title: Manual screening
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

As with <code>screen duplicates</code>, you get the same app - but slightly different behaviour - depending on how you launch the app:

```
screen_titles()  # standalone; load in data in the app
result <- screen_titles() # ditto, but save back to workspace on exit

data <- read_bibliography("my_data.ris") # load in data
screen_titles(data)  # launch the app using data from the workspace
result <- screen_titles(data) # specify an object to return data to
```

Once you've loaded the app using <code>screen_titles</code>, you will see the 'data' tab open in the dashboard:

<img src="/assets/screenshots/screen_titles_data_tab.png" width="200"/>

These four options work as follows:

<b>Import:</b> If you haven't passed any data to <code>screen_titles</code>, then this allows you to drag-and-drop a dataset directly in to the app. If you _have_ loaded <code>screen_titles</code> with data, or you have already added some data, then dragging and dropping here will add the new dataset to the existing one (using <code>merge_columns</code> in the background).

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
Abstract screening is achieved using the function <code>screen_abstracts</code>. Unlike <code>screen_titles</code>, <code>screen_abstracts</code> only shows data for one article at a time; but the two apps are otherwise identical.

<img src="/assets/screenshots/screen_abstracts.png"/>

<a href="/user_manual/4_removing_duplicates.html">Previous: Removing duplicates</a> | <a href="/user_manual/6_screening_with_topic_models.html">Next: Screening with topic models</a>