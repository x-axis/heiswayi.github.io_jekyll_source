---
layout: post
title: Singular Value Decomposition on Presidential Elections
description: Analyzing voter demographics for past U.S. presidential elections from 1976 to 2012. 
keywords: svd, statistics, code
---

We analyze the singular value decomposition of voter demographics for past United States presidential elections from 1976 to 2012. We aim to identify the demographics that have best predicted presidential election outcomes from the Carter presidency to the current Obama presidency. 

### Data
Unfortunately, I was unable to obtain a census of voter data from the U.S. Census Bureau. Instead, national exit polls from New York Times, CNN, Politico, and Gallup were aggregated into a raw data set. These polls captured 45 demographic groups which can be further grouped into 12 categories.

| Ideology | Party | Gender | Married | Race | Religion |
| --- | --- | --- | --- | --- | --- |
| Liberals | Democrats | Men | Married | White | Protestant |
| Moderates | Republicans | Women | Unmarried | Black | Catholic
| Conservatives | Independent | | | Asian | Jewish |
| | | | | Hispanic | Evangelical |
| | | | | Other | |


Import the ggplot library. 

```r
library(ggplot)
```

Import datasets.

```r
data <- read.csv("complete_dataset.csv");
A = t(df);			# Take the transpose 
svd_A = prcomp(A);		# R uses the SVD method to perform PCA. 
summary(svd_A);			# Output summary of SVD
```

Function to draw a biplot in a pretty way.
What about this method?

{% highlight r %}
PCbiplot <- function(PC, x="PC1", y="PC2") {
	# Create new dataset of only first two principal components
	data <- data.frame(obsnames=row.names(PC$x), PC$x)
	
	# Plot the Presidential Outcomes (blue for Democrat, red for Republican)
  plot <- ggplot(data, aes_string(x=x, y=y)) 
		+ geom_text(alpha=.4, size=4, aes(label=obsnames), 
		  col=ifelse(
				data$obsnames=="X2012" | 
				data$obsnames=="X2008" | 
				data$obsnames=="X1996" | 
				data$obsnames=="X1992" | 
				data$obsnames=="X1976", 
				"blue", 
				"red"
				)
			) 
{% endhighlight %}

### Analysis
Carrying out the SVD in R, we can see the proportion of variance in the data that each principal component accounts for. Three principal components explains a cumulative 82.58% of the variance while four principal components explains 88.92%. 

| | PC1 | PC2 | PC3 | PC4 | PC5 | PC6 | PC7 | PC8 | PC9
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Proportion of Variance | 0.6023 | 0.1401 | 0.08354 | 0.06334 | 0.03156 | 0.02662 | 0.02079 | 0.01767 | 0.01415
| Cumulative Proportion | 0.6023 | 0.7523 | 0.82588 | 0.88922 | 0.92078 | 0.94739 | 0.96818 | 0.98585 | 1.00000

Projection!
