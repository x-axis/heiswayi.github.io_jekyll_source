---
layout: post
title: Singular Value Decomposition on Presidential Elections
description: Analyzing voter demographics for past U.S. presidential elections from 1976 to 2012. 
keywords: svd, statistics, code
---

We analyze the singular value decomposition of voter demographics for past United States presidential elections from 1976 to 2012. We aim to identify the demographics that have best predicted presidential election outcomes from the Carter presidency to the current Obama presidency. 

### Data
National exit polls from Gallup and various news sources were aggregated into a raw data set. These polls captured 45 demographic groups which were further grouped into 12 categories.

| Ideology | Party | Gender | Married | Race | Religion |
| --- | --- | --- | --- | --- | --- |
| Liberal | Democrat | Men | Married | White | Protestant |
| Moderate | Republican | Women | Unmarried | Black | Catholic
| Conservative | Independent | | | Asian | Jewish |
| | | | | Hispanic | Evangelical |
| | | | | Other | |

| Age | Education | Income | Region | Community | Voting Status |
| --- | --------- | ------ | ------ | --------- | ------------- |
| 18-24 years | Less than HS | Under $30,000 | East | Urban | First-time voter |
| 25-29 years | High School | $30,000-49,999 | Midwest | Suburban | |
| 30-39 years | Some College | $50,000-99,999 | South | Rural | | 
| 40-49 years | College | $100,000-199,000 | West | | | 
| 50-64 years | Postgraduate | Over $200,000 | | | |
| 65 and older | | | | | |

Across each election, voting behavior of each demographic group are represented as a column vector capturing whether or not a majority voted for the winning presidential candidate.

$$
Demographic_i = 
\begin{cases}
1 & \text{if the higher share voted for the winning candidate} \\
0 &\text{if vote was split within 55/45 or closer} \\
-1 &\text{if the higher share voted for the losing candidate} 
\end{cases}
$$


Wave Equation 

$$\frac{\delta E_{x}}{\delta t} = \frac{\delta f(z-ct)}{\delta t} = f^{\prime}(z - ct)\Big(\frac{\delta(z-ct)}{\delta t}\Big) = -c*f^{\prime}(z - ct)$$


```latex
\frac{\delta E_{x}}{\delta t} = \frac{\delta f(z-ct)}{\delta t} = f^{\prime}(z - ct)\Big(\frac{\delta(z-ct)}{\delta t}\Big) = -c*f^{\prime}(z - ct)

\frac{\delta^2 E_{x}}{\delta t^2} = \frac{\delta}{\delta t} \Big(\frac{\delta Ex}{\delta t}\Big)= f^{\prime\prime}(z - ct)\Big(\frac{\delta(z-ct)}{\delta t}\Big) = c^2*f^{\prime\prime}(z - ct)
```

### Principal Components

Note that R uses the singular value decomposition method to perform principal component analysis, where the convention is to consider rows as observations and columns as variables, so our matrix needs to be in *election_year x demographic_group* format. The data for all 45 demographics then comprises a 10 x 45 matrix. Since each demographic is encoded on the same scale of {1, 0, -1}, no further processing is needed, e.g. mean-centering or normalization.  

```r
df <- read.csv("complete_dataset.csv");
svd_df = prcomp(df);    # R uses the SVD method to perform PCA. 
summary(svd_A);         # Output summary of SVD
```

In the summary, we can see the proportion of variance in the data that each principal component accounts for. Each principal component represents a "dimension" of the data, describing some underlying dynamic.

| | PC1 | PC2 | PC3 | PC4 | PC5 | PC6 | PC7 | PC8 | PC9
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Proportion of Variance | 0.6023 | 0.1401 | 0.08354 | 0.06334 | 0.03156 | 0.02662 | 0.02079 | 0.01767 | 0.01415
| Cumulative Proportion | 0.6023 | 0.7523 | 0.82588 | 0.88922 | 0.92078 | 0.94739 | 0.96818 | 0.98585 | 1.00000

More precisely, the principal components of a dataset form an orthogonal basis. Geometrically, basis vectors can be seen as the axes in a Cartesian coordinate system. Humans are comfortable seeing data represented in two dimensions: x and y, so we can project the first two principal components, PC1 and PC2, onto the standard x, y plane. Together, they capture 75% of variance in the data. 

{% img elections_biplot.png %}

Here, the two principal components form the axes of the biplot above. There are two things to interpret: points and vectors. Points (presidential election years) that are close together have similar demographics while vectors (demographic groups) that are close together have similar voting behavior. We see that Democratic presidences are grouped on the left while Republican presidences are grouped on the right. Several demographics are clustered together:

* **Green**: Democrat, Liberal, Hispanic, Urban, Jewish
* **Orange**: 18-24 years old, Women, Unmarried, East
* **Blue**: Post-graduate education, First-time voter
* **Yellow**: Republican, Protestant, $100,000-199,999 income

 
### Analysis

Let's focus on the first principal component, on how demographics are distributed along the x-axis. Demographics on the farthest left are Democrat, Liberal, Hispanic, Urban, and Jewish. On the farthest right, we have Republican, Conservative, Over $200k annual income, and Protestant. Recall that a principal component is supposed to capture some dimension dynamic of the data, so we can infer that the first component represents a political spectrum from Democrat to Republican. The farther away from the origin a demographic's vector points along the x-axis, the more extreme it is.

Interestingly, we see that the more recent the presidency, the more extreme they are on the x-axis. This reflects the historical trend that presidencies and voters have become more partisan over the years. Jimmy Carter's presidency in 1976 and Ronald Reagan's presidency in 1984 are much closer to the origin than Obama's presidency in 2012 and Bush's presidency in 2004.

The second principal component appears to represent the predictive power of a demographic. Above the scale, knowing which candidate that Liberals, Conservatives, or Married people support tells us little about who will win. Below the scale, support from Independents, the West, and First-time voters have major predictive power. This reflects the enormous influence that swing states and California brings to the election.

### Weaknesses 

The biggest weakness of the analysis lies in the unavoidable lack of sample data; forty years of history only yields ten samples. The analysis could also be expanded by breaking down demographics even more, e.g. 18-24 year old Independent voters or Rural first-time voters. Instead of looking at national exit polls, we can also focus on the specific exit polls for states with the most electoral votes: California, Texas, New York, or look at exit polls for swing states only: Ohio, Pennsylvania, Florida, Colorado.

### Conclusion

In order to capture the White House, this year's presidential candidates most likely need to be able to win Independents, the West, the blue cluster, and the orange cluster. 

### References

1. Shlens, J., 2014. A tutorial on principal component analysis. arXiv preprint arXiv:1404.1100. [pdf](http://arxiv.org/pdf/1404.1100.pdf)

2. "2012 President Exit Polls." The New York Times. [link](http://elections.nytimes.com/2012/results/president/exit-polls)

3. "How Groups Voted." Roper Center for Public Opinion Research, Cornell University. [link](http://ropercenter.cornell.edu/polls/us-elections/how-groups-voted/)

4. "2004 U.S. President National Exit Poll" CNN. [link](http://www.cnn.com/ELECTION/2004/pages/results/states/US/P/00/epolls.0.html)

5. 1992-1996 Voting Demographics. Gallup. [link](http://www.gallup.com/poll/9466/election-polls-vote-groups-19921996.aspx)

6. "CPI Inflation Calculator." Bureau of Labor Statistics. [link](http://www.bls.gov/data/inflation_calculator.htm)

*Used to normalize income across polling years.*
