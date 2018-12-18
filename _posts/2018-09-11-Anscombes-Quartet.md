---
layout: single
title: Anscombe’s Quartet, and Why Summary Statistics Don’t Tell the Whole Story
excerpt: "Anscombe's quartet comprises four datasets that have nearly identical simple descriptive statistics, yet appear very different when graphed. Each dataset consists of eleven (x,y) points."
date: 2018-09-11
tags: [ anscombe, data statistics, data stories ]
---

Anscombe's quartet comprises four datasets that have nearly identical simple descriptive statistics, yet appear very different when graphed. Each dataset consists of eleven (x,y) points. They were constructed in 1973 by the statistician Francis Anscombe to demonstrate both the importance of graphing data before analyzing it and the effect of outliers on statistical properties. He described the article as being intended to counter the impression among statisticians that "numerical calculations are exact, but graphs are rough."


_Anscombe’s Quartet Visualization Python Code:_
<script src="https://gist.github.com/loganblackstad/16ad035daf360cdeb8e092951a7ed97f.js"></script>

<br>
<p style="font-family:Consolas; font-size:70%; color:rgb(209,51,35); ">Out []:</p>
<img src="https://loganblackstad.github.io/assets/images/anscombes_quartet.png">

### All the summary statistics you’d think to compute are close to identical:

- The average x value is 9 for each dataset
- The average y value is 7.50 for each dataset
- The variance for x is 11 and the variance for y is 4.12
- The correlation between x and y is 0.816 for each dataset
- A linear regression (line of best fit) for each dataset follows the equation y = 0.5x + 3

But if we take a look back at the visualized data above, we see the real relationships in the datasets emerge. Dataset I consists of a set of points that appear to follow a rough linear relationship with some variance. Dataset II fits a neat curve but doesn’t follow a linear relationship (maybe it’s quadratic?). Dataset III looks like a tight linear relationship between x and y, except for one large outlier. Dataset IV looks like x remains constant, except for one outlier as well.

Computing summary statistics or staring at the data wouldn’t have told us any of these stories. Instead, it’s important to visualize the data to get a clear picture of what’s going on.


### When should you use summary statistics?
This isn’t to say that summary statistics are useless. They’re just misleading on their own. It’s important to use these as just one tool in a larger data analysis process.

Visualizing our data allows us to revisit our summary statistics and recontextualize them as needed. For example, Dataset II from Anscombe’s Quartet demonstrates a strong relationship between x and y, it just doesn’t appear to be linear. So a linear regression was the wrong tool to use there, and we can try other regressions. Eventually, we’ll be able to revise this into a model that does a great job of describing our data, and has a high degree of predictive power for future observations.

----
----
### References:
* https://seaborn.pydata.org/_downloads/anscombes_quartet.py
* https://en.wikipedia.org/wiki/Anscombe%27s_quartet

