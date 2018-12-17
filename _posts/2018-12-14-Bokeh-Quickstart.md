---
layout: single
excerpt: "Bokeh is a Python interactive visualization library that targets modern web browsers for presentation. Its goal is to provide elegant, concise construction of novel graphics in the style of D3.js, and to extend this capability..."
title: "Bokeh Quickstart"
tags: [ python, jupyter notebooks ]
--- 
<div>
<a href="http://bokeh.pydata.org/"><img src="/assets/images/bokeh-header.png"></a>
</div>

# Bokeh 5-minute Overview

Bokeh is a Python interactive visualization library that targets modern web
browsers for presentation. Its goal is to provide elegant, concise construction
of novel graphics in the style of D3.js, and to extend this capability with
high-performance interactivity over very large or streaming datasets. Bokeh can
help anyone who would like to quickly and easily create interactive plots,
dashboards, and data applications. 
 
## Simple Example

Here is a simple first example.  First we'll import the [`figure`](https://bokeh
.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.figure)
function from [`bokeh.plotting`](https://bokeh.pydata.org/en/latest/docs/user_gu
ide/plotting.html), which will let us create all sorts of interesting plots
easily. We also import the `show` and `ouptut_notebook` functions from
`bokeh.io` &mdash; these let us display our results inline in the notebook. 

<!---  <span style="color:rgb(56,63,155)">In [1]:</span>  --->

<p style="color:rgb(56,63,155)">In [1]:</p>

{% highlight python %}
from bokeh.plotting import figure 
from bokeh.io import output_notebook, show
{% endhighlight %}
 
Next, we'll tell Bokeh to display its plots directly into the notebook.
This will cause all of the Javascript and data to be embedded directly
into the HTML of the notebook itself.
(Bokeh can output straight to HTML files, or use a server, which we'll
look at later.) 

<p style="color:rgb(56,63,155)">In [2]:</p>
{% highlight python %}
output_notebook()
{% endhighlight %}



    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="8a0d67fd-5bd9-4344-8e7c-9a9b90455d51">Loading BokehJS ...</span>
    </div>



 
Next, we'll import NumPy and create some simple data. 

**In [3]:**

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

**In [4]:**

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

**In [5]:**

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

**In [6]:**

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

**In [7]:**

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

**In [8]:**

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

**In [9]:**

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

**In [None]:**

{% highlight python %}

{% endhighlight %}
