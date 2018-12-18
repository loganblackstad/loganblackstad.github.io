---
title: Atlanta Weather Visualized
excerpt: "[Page in Development] I need to play with the formatting (text sizing, color, adding images, etc.)"
date: 2018-11-14
tags: [ python, notebook, Atlanta]
---


<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [1]:</p>

{% highlight python %}
import numpy as np
import matplotlib.pyplot as pp
import matplotlib as mpl
import pandas as pd
import scipy
import statsmodels
import ggplot
import seaborn as sb
import altair
import plotnine as pn
import collections
import datetime
import os
from ggplot import *
{% endhighlight %}


FIRST, get weather data:

I queried weather data from NOAA because it was free:
https://www.ncdc.noaa.gov/

Parameters: 
city  = Atlanta
dates = 01/01/2016 to 12/01/2018

NOAA sends an email file containing the csv of weather data to the email youy specify.

I then imported atlanta-weather.csv as a pandas DataFrame. (Important: the .csv file has to be in the same directory as your jupyter file.) 


<p style="font-family:Consolas; font-size:70%; color:rgb(56,63,155); ">In [2]:</p>
{% highlight python %}
test_w = pd.read_csv("test.csv")
test_w.head()
{% endhighlight %}

**In [3]:**
{% highlight python %}
atl_w = pd.read_csv("atlanta-weather.csv", dtype = object)
{% endhighlight %}

**In [4]:**
{% highlight python %}
atl_w_col_names = list(atl_w.columns.values)
print (atl_w_col_names, end = '')
{% endhighlight %}

**In [5]:**
{% highlight python %}
list(set(atl_w.dtypes))
{% endhighlight %}


**In [6]:**
{% highlight python %}
uniq_dict = {}
for col in atl_w:
    uniq_dict[col] = atl_w[col].value_counts().to_dict()
{% endhighlight %}

**In [7]:**
{% highlight python %}
uniq_dict

for key in uniq_dict: 
    print(key)
{% endhighlight %}

**In [None]:**

{% highlight python %}
days = datetime.datetime(2018, 12, 1) - datetime.datetime(2016, 1, 1)
print("There are {} days between Jan 01 2016 and Dec 01 2018 [inclusive]".format(days.days))
{% endhighlight %}

**In [None]:**

{% highlight python %}
records_per_station = atl_w.groupby('NAME')['DATE'].nunique().sort_values(ascending=False)
{% endhighlight %}

**In [None]:**

{% highlight python %}
records_per_station.head(10)
{% endhighlight %}

**In [None]:**

{% highlight python %}
df_temp = atl_w[['NAME', 'DATE', 'TAVG', 'TMAX', 'TMIN']].copy()
df_airport = df_temp.loc[df_temp['NAME'] == "ATLANTA HARTSFIELD INTERNATIONAL AIRPORT, GA US"]
df_airport.head()
{% endhighlight %}

**In [None]:**

{% highlight python %}
dfa = df_airport
dfa.info()
{% endhighlight %}

**In [None]:**

{% highlight python %}
dfa = dfa.astype({"TAVG": float, "TMAX": float, "TMIN": float})
{% endhighlight %}

**In [None]:**

{% highlight python %}
dfa.info()
{% endhighlight %}

**In [None]:**

{% highlight python %}
fig, ax = pp.subplots(figsize=(13,6))

mask2016 = dfa[(dfa['DATE']>='2016-1-1') & (dfa['DATE']<'2017-1-1')] 
mask2017 = dfa[(dfa['DATE']>='2017-1-1') & (dfa['DATE']<'2018-1-1')] 
mask2018 = dfa[(dfa['DATE']>='2018-1-1') & (dfa['DATE']<='2018-12-1')] 

mask2016.plot(kind='line',x='DATE',y='TMAX', ax=ax, color='red')
mask2016.plot(kind='line',x='DATE',y='TMIN', ax=ax, color='blue')


pp.ylabel('Temperature (°F)')
pp.title('\nATL Airport Temperature (min, avg, max)\n[Jan 01 2016 to Dec 01 2018]\n', fontsize=14)

{% endhighlight %}
<div>
<a><img src="/assets/images/atl-weather-1.png"></a>
</div>



**In [None]:**

{% highlight python %}
all_days = list(range(1,len(dfa)+1))

list_x = all_days
list_y = dfa['TMAX']


def plot_smoothed(drange, temp, win=10):
    smoothed = np.correlate(temp, np.ones(win)/win,'same')    
    pp.plot(drange,smoothed)

#pp.plot(list_x,list_y)
#plot_smoothed()

fig, ax = pp.subplots(figsize=(13,6))
plot_smoothed(all_days, dfa['TMAX'], 20)
plot_smoothed(all_days, dfa['TMIN'], 20)
{% endhighlight %}

<div>
<a><img src="/assets/images/atl-weather-2.png"></a>
</div>



