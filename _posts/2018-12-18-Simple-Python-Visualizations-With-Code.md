---
layout: single
excerpt: "Data Visualization is a big part of a data scientist’s jobs. Creating visualizations helps make your analysis clearer and easier to understand, especially with larger, high dimensional datasets."
title: "Data Visualizations in Python with Code"
tags: [ python, jupyter notebooks ]
--- 
<div>
<img src="/assets/images/easy-plotting-header.png">
</div>

# Simple Data Visualizations in Python with Code

Creating visualizations of your data helps make your analysis clearer and easier to understand, especially with larger, high dimensional datasets. At the end of your project, it’s important to be able to present your final results in a clear, concise, and compelling manner that your audience (esp. non-technical clients) can understand.

Matplotlib is a popular Python library that can be used to create your Data Visualizations quite easily. However, setting up the data, parameters, figures, and plotting can get quite messy and tedious to do every time you do a new project. In this blog post, we’re going to look at 5 data visualizations and write some quick and easy functions for them with Python’s Matplotlib. 

**A chart for selecting the proper data visualization technique for a given situation:**
<img src="/assets/images/easy-plotting-1.jpeg">

Exploratory Data Analysis (EDA) 




### Scatter Plots

Scatter plots are great for showing the relationship between two variables since you can directly see the raw distribution of the data. You can also view this relationship for different groups of data simple by colour coding the groups: 

<img src="/assets/images/easy-plotting-2.png">

Want to visualize the relationship between three variables? No problemo! Just use another parameters, like point size, to encode that third variable:

**Scatter plot with colour groupings and size encoding for the third variable of country size:**
<img src="/assets/images/easy-plotting-3.png">

Now for the code. We first import Matplotlib’s pyplot with the alias “plt”. To create a new plot figure we call plt.subplots() . We pass the x-axis and y-axis data to the function and then pass those to ax.scatter() to plot the scatter plot. We can also set the point size, point color, and alpha transparency. You can even set the y-axis to have a logarithmic scale. The title and axis labels are then set specifically for the figure. That’s an easy to use function that creates a scatter plot end to end!

<script src="https://gist.github.com/loganblackstad/a8f219a5910f47c0d324a72f3158a8d7.js"></script>



### Line Plots
Line plots are best used when you can clearly see that one variable varies greatly with another i.e they have a high covariance. Lets take a look at the figure below to illustrate. We can clearly see that there is a large amount of variation in the percentages over time for all majors. Plotting these with a scatter plot would be extremely cluttered and quite messy, making it hard to really understand and see what’s going on. Line plots are perfect for this situation because they basically give us a quick summary of the covariance of the two variables (percentage and time). Again, we can also use grouping by colour encoding.

**Example line plot**
<img src="/assets/images/easy-plotting-4.png">


<script src="https://gist.github.com/loganblackstad/f903720bacd6a17dd3d1941599f62653.js"></script>



Histograms
Histograms are useful for viewing (or really discovering)the distribution of data points. Check out the histogram below where we plot the frequency vs IQ histogram. We can clearly see the concentration towards the center and what the median is. We can also see that it follows a Gaussian distribution. Using the bars (rather than scatter points, for example) really gives us a clearly visualization of the relative difference between the frequency of each bin. The use of bins (discretization) really helps us see the “bigger picture” where as if we use all of the data points without discrete bins, there would probably be a lot of noise in the visualization, making it hard to see what is really going on.


Histogram example
The code for the histogram in Matplotlib is shown below. There are two parameters to take note of. Firstly, the n_bins parameters controls how many discrete bins we want for our histogram. More bins will give us finer information but may also introduce noise and take us away from the bigger picture; on the other hand, less bins gives us a more “birds eye view” and a bigger picture of what’s going on without the finer details. Secondly, the cumulative parameter is a boolean which allows us to select whether our histogram is cumulative or not. This is basically selecting either the Probability Density Function (PDF) or the Cumulative Density Function (CDF).


Imagine we want to compare the distribution of two variables in our data. One might think that you’d have to make two separate histograms and put them side-by-side to compare them. But, there’s actually a better way: we can overlay the histograms with varying transparency. Check out the figure below. The Uniform distribution is set to have a transparency of 0.5 so that we can see what’s behind it. This allows use to directly view the two distributions on the same figure.


Overlaid Histogram
There are a few things to set up in code for the overlaid histograms. First, we set the horizontal range to accommodate both variable distributions. According to this range and the desired number of bins we can actually computer the width of each bin. Finally, we plot the two histograms on the same plot, with one of them being slightly more transparent.


Bar Plots
Bar plots are most effective when you are trying to visualize categorical data that has few (probably < 10) categories. If we have too many categories then the bars will be very cluttered in the figure and hard to understand. They’re nice for categorical data because you can easily see the difference between the categories based on the size of the bar (i.e magnitude); categories are also easily divided and colour coded too. There are 3 different types of bar plots we’re going to look at: regular, grouped, and stacked. Check out the code below the figures as we go along.

The regular barplot is in the first figure below. In the barplot() function, x_data represents the tickers on the x-axis and y_data represents the bar height on the y-axis. The error bar is an extra line centered on each bar that can be drawn to show the standard deviation.

Grouped bar plots allow us to compare multiple categorical variables. Check out the second bar plot below. The first variable we are comparing is how the scores vary by group (groups G1, G2, ... etc). We are also comparing the genders themselves with the colour codes. Taking a look at the code, the y_data_list variable is now actually a list of lists, where each sublist represents a different group. We then loop through each group, and for each group we draw the bar for each tick on the x-axis; each group is also colour coded.

Stacked bar plots are great for visualizing the categorical make-up of different variables. In the stacked bar plot figure below we are comparing the server load from day-to-day. With the colour coded stacks, we can easily see and understand which servers are worked the most on each day and how the loads compare to the other servers on all days. The code for this follows the same style as the grouped bar plot. We loop through each group, except this time we draw the new bars on top of the old ones rather than beside them.


Regular Bar Plot

Grouped Bar Plot

Stacked Bar Plot

Box Plots
We previously looked at histograms which were great for visualizing the distribution of variables. But what if we need more information than that? Perhaps we want a clearer view of the standard deviation? Perhaps the median is quite different from the mean and thus we have many outliers? What if there is so skew and many of the values are concentrated to one side?

That’s where boxplots come in. Box plots give us all of the information above. The bottom and top of the solid-lined box are always the first and third quartiles (i.e 25% and 75% of the data), and the band inside the box is always the second quartile (the median). The whiskers (i.e the dashed lines with the bars on the end) extend from the box to show the range of the data.

Since the box plot is drawn for each group/variable it’s quite easy to set up. The x_data is a list of the groups/variables. The Matplotlib function boxplot() makes a box plot for each column of the y_data or each vector in sequence y_data; thus each value in x_data corresponds to a column/vector in y_data. All we have to set then are the aesthetics of the plot.


Box plot example

Box plot code
Conclusion
There are your 5 quick and easy data visualizations using Matplotlib. Abstracting things into functions always makes your code easier to read and use! I hope you enjoyed this post and learned something new and useful.















## Simple Example

Here is a simple first example.  First we'll import the [`figure`](https://bokeh
.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.figure)
function from [`bokeh.plotting`](https://bokeh.pydata.org/en/latest/docs/user_gu
ide/plotting.html), which will let us create all sorts of interesting plots
easily. We also import the `show` and `ouptut_notebook` functions from
`bokeh.io` &mdash; these let us display our results inline in the notebook. 

<!---  <span style="color:rgb(56,63,155)">In [1]:</span>  --->

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [1]:</p>
{% highlight python %}
from bokeh.plotting import figure 
from bokeh.io import output_notebook, show
{% endhighlight %}
 
Next, we'll tell Bokeh to display its plots directly into the notebook.
This will cause all of the Javascript and data to be embedded directly
into the HTML of the notebook itself.
(Bokeh can output straight to HTML files, or use a server, which we'll
look at later.) 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [2]:</p>
{% highlight python %}
output_notebook()
{% endhighlight %}



    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="8a0d67fd-5bd9-4344-8e7c-9a9b90455d51">Loading BokehJS ...</span>
    </div>



 
Next, we'll import NumPy and create some simple data. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [3]:</p>
{% highlight python %}
from numpy import cos, linspace
x = linspace(-6, 6, 100)
y = cos(x)
{% endhighlight %}
 
Now we'll call Bokeh's `figure` function to create a plot `p`. Then we call the
`circle()` method of the plot to render a red circle at each of the points in x
and y.

We can immediately interact with the plot:

  * click-drag will pan the plot around.
  * mousewheel will zoom in and out (after enabling in the toolbar)

The toolbar below is the default one that is available for all plots. It can be
configured further via the `tools` keyword argument. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [4]:</p>
{% highlight python %}
p = figure(width=500, height=500)
p.circle(x, y, size=7, color="firebrick", alpha=0.5)
show(p)
{% endhighlight %}








  <div class="bk-root" id="6945ed26-b12e-411a-a983-e404d5cb4a65"></div>




 
# Bar Plot Example


Bokeh's core display model relies on *composing graphical primitives* which are
bound to data series.  This is similar in spirit to Protovis and D3, and
different than most other Python plotting libraries.

A slightly more sophisticated example demonstrates this idea.

Bokeh ships with a small set of interesting "sample data" in the
`bokeh.sampledata` package.  We'll load up some historical automobile mileage
data, which is returned as a Pandas `DataFrame`. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [5]:</p>
{% highlight python %}
from bokeh.sampledata.autompg import autompg

grouped = autompg.groupby("yr")

mpg = grouped.mpg
avg, std = mpg.mean(), mpg.std()
years = list(grouped.groups)
american = autompg[autompg["origin"]==1]
japanese = autompg[autompg["origin"]==3]
{% endhighlight %}
 
For each year, we want to plot the distribution of MPG within that year. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [6]:</p>
{% highlight python %}
p = figure(title="MPG by Year (Japan and US)")

p.vbar(x=years, bottom=avg-std, top=avg+std, width=0.8, 
       fill_alpha=0.2, line_color=None, legend="MPG 1 stddev")

p.circle(x=japanese["yr"], y=japanese["mpg"], size=10, alpha=0.5,
         color="red", legend="Japanese")

p.triangle(x=american["yr"], y=american["mpg"], size=10, alpha=0.3,
           color="blue", legend="American")

p.legend.location = "top_left"
show(p)
{% endhighlight %}








  <div class="bk-root" id="329642c6-19d6-4b67-bf7b-936c79aed714"></div>




 
**This kind of approach can be used to generate other kinds of interesting
plots. See many more examples in the [Bokeh Documentation
Gallery](https://bokeh.pydata.org/en/latest/docs/gallery.html). ** 
 
## Linked Brushing

To link plots together at a data level, we can explicitly wrap the data in a
`ColumnDataSource`. This allows us to reference columns by name.

We can use a "select" tool to select points on one plot, and the linked points
on the other plots will highlight. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [7]:</p>
{% highlight python %}
from bokeh.models import ColumnDataSource
from bokeh.layouts import gridplot

source = ColumnDataSource(autompg)

options = dict(plot_width=300, plot_height=300,
               tools="pan,wheel_zoom,box_zoom,box_select,lasso_select")

p1 = figure(title="MPG by Year", **options)
p1.circle("yr", "mpg", color="blue", source=source)

p2 = figure(title="HP vs. Displacement", **options)
p2.circle("hp", "displ", color="green", source=source)

p3 = figure(title="MPG vs. Displacement", **options)
p3.circle("mpg", "displ", size="cyl", line_color="red", fill_color=None, source=source)

p = gridplot([[ p1, p2, p3]], toolbar_location="right")

show(p)
{% endhighlight %}








  <div class="bk-root" id="a86d0d31-997d-4276-8e1e-90d59ccc58e0"></div>




 
You can read more about the `ColumnDataSource` and other Bokeh data structures
in [Providing Data for Plots and
Tables](https://bokeh.pydata.org/en/latest/docs/user_guide/data.html) 
 
## Standalone HTML

In addition to working well with the Notebook, Bokeh can also save plots out
into their own HTML files.  Here is the bar plot example from above, but saving
into its own standalone file.

Now when we call `show()`, a new browser tab is also opened with the plot. If we
just wanted to save the file, we would use `save()` instead. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [8]:</p>
{% highlight python %}
from bokeh.plotting import output_file

output_file("barplot.html")

p = figure(title="MPG by Year (Japan and US)")

p.vbar(x=years, bottom=avg-std, top=avg+std, width=0.8, 
       fill_alpha=0.2, line_color=None, legend="MPG 1 stddev")

p.circle(x=japanese["yr"], y=japanese["mpg"], size=10, alpha=0.3,
         color="red", legend="Japanese")

p.triangle(x=american["yr"], y=american["mpg"], size=10, alpha=0.3,
           color="blue", legend="American")

p.legend.location = "top_left"
show(p)
{% endhighlight %}








  <div class="bk-root" id="a3fbb3bd-5e38-4110-bb97-3dccf780acf7"></div>




 
## Bokeh Applications

Bokeh also has a server component that can be used to build interactive web
applications that easily connect the powerful constellation of PyData tools to
sophisticated Bokeh visualizations. The Bokeh server can be used to:

* respond to UI and tool events generated in a browser with computations or
queries using the full power of python
* automatically push server-side updates to the UI (i.e. widgets or plots in a
browser)
* use periodic, timeout, and asynchronous callbacks to drive streaming updates

The cell below shows a simple deployed Bokeh application from
https://demo.bokehplots.com embedded in an IFrame. Scrub the sliders or change
the title to see the plot update. 

<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [9]:</p>
{% highlight python %}
from IPython.display import IFrame
IFrame('https://demo.bokehplots.com/apps/sliders/', width=900, height=410)
{% endhighlight %}





        <iframe
            width="900"
            height="410"
            src="https://demo.bokehplots.com/apps/sliders/"
            frameborder="0"
            allowfullscreen
        ></iframe>
        


 
Click on any of the thumbnails below to launch other live Bokeh applications.

<center>
<a href="https://demo.bokehplots.com/apps/crossfilter">
  <img
    width="30%" height="30%" style="display: inline ; padding: 10px;"
    src="https://bokeh.pydata.org/static/crossfilter_t.png"
  >
</a>

<a href="https://demo.bokehplots.com/apps/movies">
  <img
    width="30%" height="30%" style="display: inline ; padding: 10px;"
    src="https://bokeh.pydata.org/static/movies_t.png"
  >
</a>

<a href="https://demo.bokehplots.com/apps/gapminder">
  <img
    width="30%" height="30%" style="display: inline ; padding: 10px;"
    src="http://bokeh.pydata.org/static/gapminder_t.png"
  >
</a>
</center>

Find more details and information about developing and deploying Bokeh server
applications in the User's Guide chapter [Running a Bokeh
Server](https://bokeh.pydata.org/en/latest/docs/user_guide/server.html). 
 
## BokehJS

At its core, Bokeh consists of a Javascript library,
[BokehJS](https://github.com/bokeh/bokeh/tree/master/bokehjs), and a Python
binding which provides classes and objects that ultimately generate a JSON
representation of the plot structure.

You can read more about design and usage in the [Developing with
JavaScript](https://bokeh.pydata.org/en/latest/docs/user_guide/bokehjs.html)
section of the Bokeh User's Guide. 
 
## More Information

Find more details and information at the resources listed below:

*Documentation:* https://bokeh.pydata.org/en/latest

*GitHub:* https://github.com/bokeh/bokeh

*Mailing list:* [bokeh@anaconda.com](mailto:bokeh@anaconda.com)

*Gitter Chat:* https://gitter.im/bokeh/bokeh

Be sure to follow us on Twitter [@bokehplots](http://twitter.com/BokehPlots>)
and on [Youtube](https://www.youtube.com/c/Bokehplots)!

<img src="/assets/images/bokeh-transparent.png" width="64px" height="64px"> 


