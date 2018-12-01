---
layout: user_manual
title: Examples
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

# Examples

## Creating efficient search strings

## Screening with multiple reviewers

## Tracking hot topics
Understanding which topics are popular or unpopular at any given time is a common question when investigating scientific literature. This is an easy task with revtools - first you need to run a topic model as we have already seen:

```
library(revtools)
data <- read_bibliography("your_dataset.ris")
dtm <- make_DTM(data)
model <- topicmodels::LDA(
  dtm,
  k = 15,
  LDA.control = list(
    burnin = 1000,
    iter = 6000,
    keep = 100
  )
)
```
Then it is simply a case of cross-tabulating the number of topics per year, and modelling those counts.
```
articles <- as.data.frame(data)
articles$topic <- topics(model)

# cross-tabulate to show number of articles per topic per year
popularity <- as.data.frame(
  xtabs(
    ~ year + topic,
    data = articles,
    drop.unused.levels = FALSE
  ),
stringsAsFactors = FALSE
)
popularity$year <- scale(
  as.numeric(popularity$year)
)
popularity$topic <- as.factor(popularity$topic)

# create a mixed model
library(lme4)
popularity_model <- glmer(Freq ~ 1 + (1 | topic) + (year -1 | topic),
	family = poisson(link="log"),
	data = popularity
)

# export the results of this model
popularity_results <- ranef(popularity_model)$topic
colnames(popularity_results) <- c("intercept", "slope")
```

Here we have assumed that each topic has a unique slope and intercept. If we wanted to investigate non-linear changes over time, then we might want to try using GAMs instead.

Finally, we can plot the results:

```
library(ggplot2)
p <- ggplot(popularity_results,
  aes(x = intercept, y = slope)
) +
geom_point()
p
```

<a href="/user_manual/6_screening_with_topic_models.html">Previous: Screening with topic models</a>