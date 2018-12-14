---
title: Atlanta Weather Visualized
date: 2018-12-12
tags: [Atlanta, Data Visualization, Python]
use_math: true
---

You can find the beginning of my .ipynb test file here:
https://github.com/loganblackstad/nbviewer-test/blob/master/atlanta-weather-plotting.ipynb


# [ -->  PAGE UNDER CONSTRUCTION  <-- ]

### To Do

Skills:  
data cleaning - remove unnecessary columns  
deal with missing data - interpolate data with cross product  
data smoothing  
visualization  
insights  


Data:  
* Smooth data by year (2016,2017,2018)  
  - overlay smoothed data by year  
* Interpolate missing AVG Temp data   


Vizualization:  
* Label line graphs with:  title, axis, legend, coloring  
* Embed nbViewer Code in markdown/html  


<script src="https://gist.github.com/loganblackstad/42ed546ccd4e1cfef3857bec7cbf2098.js"></script>


<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="sd">&quot;&quot;&quot;</span>
<span class="sd">author:  Logan Blackstad</span>
<span class="sd">file:    atlanta-weather-plotting.py</span>
<span class="sd">date:    Dec 06 2018</span>

<span class="sd">Description:</span>
<span class="sd">Goal --&gt; Plot the daily min and max temps for ATL in 2016 vs 2017 vs 2018</span>


<span class="sd">&quot;&quot;&quot;</span>

<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">pp</span>
<span class="kn">import</span> <span class="nn">matplotlib</span> <span class="k">as</span> <span class="nn">mpl</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">scipy</span>
<span class="kn">import</span> <span class="nn">statsmodels</span>
<span class="kn">import</span> <span class="nn">ggplot</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sb</span>
<span class="kn">import</span> <span class="nn">altair</span>
<span class="kn">import</span> <span class="nn">plotnine</span> <span class="k">as</span> <span class="nn">pn</span>
<span class="kn">import</span> <span class="nn">collections</span>
<span class="kn">import</span> <span class="nn">datetime</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="kn">from</span> <span class="nn">ggplot</span> <span class="k">import</span> <span class="o">*</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">FIRST</span><span class="p">,</span> <span class="n">get</span> <span class="n">weather</span> <span class="n">data</span><span class="p">:</span>

<span class="n">I</span> <span class="n">queried</span> <span class="n">weather</span> <span class="n">data</span> <span class="kn">from</span> <span class="nn">NOAA</span> <span class="n">because</span> <span class="n">it</span> <span class="n">was</span> <span class="n">free</span><span class="p">:</span>
<span class="n">https</span><span class="p">:</span><span class="o">//</span><span class="n">www</span><span class="o">.</span><span class="n">ncdc</span><span class="o">.</span><span class="n">noaa</span><span class="o">.</span><span class="n">gov</span><span class="o">/</span>

<span class="n">Parameters</span><span class="p">:</span> 
<span class="n">city</span>  <span class="o">=</span> <span class="n">Atlanta</span>
<span class="n">dates</span> <span class="o">=</span> <span class="mi">01</span><span class="o">/</span><span class="mi">01</span><span class="o">/</span><span class="mi">2016</span> <span class="n">to</span> <span class="mi">12</span><span class="o">/</span><span class="mi">01</span><span class="o">/</span><span class="mi">2018</span>

<span class="n">NOAA</span> <span class="n">sends</span> <span class="n">an</span> <span class="n">email</span> <span class="n">file</span> <span class="n">containing</span> <span class="n">the</span> <span class="n">csv</span> <span class="n">of</span> <span class="n">weather</span> <span class="n">data</span> <span class="n">to</span> <span class="n">the</span> <span class="n">email</span> <span class="n">youy</span> <span class="n">specify</span><span class="o">.</span>

<span class="n">I</span> <span class="n">then</span> <span class="n">imported</span> <span class="n">atlanta</span><span class="o">-</span><span class="n">weather</span><span class="o">.</span><span class="n">csv</span> <span class="k">as</span> <span class="n">a</span> <span class="n">pandas</span> <span class="n">DataFrame</span><span class="o">.</span> <span class="p">(</span><span class="n">Important</span><span class="p">:</span> <span class="n">the</span> <span class="o">.</span><span class="n">csv</span> <span class="n">file</span> <span class="n">has</span> <span class="n">to</span> <span class="n">be</span> <span class="ow">in</span> <span class="n">the</span> <span class="n">same</span> <span class="n">directory</span> <span class="k">as</span> <span class="n">your</span> <span class="n">jupyter</span> <span class="n">file</span><span class="o">.</span><span class="p">)</span> 
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">test_w</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;test.csv&quot;</span><span class="p">)</span>
<span class="n">test_w</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">atl_w</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;atlanta-weather.csv&quot;</span><span class="p">,</span> <span class="n">dtype</span> <span class="o">=</span> <span class="nb">object</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">atl_w_col_names</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">atl_w</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">values</span><span class="p">)</span>
<span class="nb">print</span> <span class="p">(</span><span class="n">atl_w_col_names</span><span class="p">,</span> <span class="n">end</span> <span class="o">=</span> <span class="s1">&#39;&#39;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">list</span><span class="p">(</span><span class="nb">set</span><span class="p">(</span><span class="n">atl_w</span><span class="o">.</span><span class="n">dtypes</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">uniq_dict</span> <span class="o">=</span> <span class="p">{}</span>
<span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="n">atl_w</span><span class="p">:</span>
    <span class="n">uniq_dict</span><span class="p">[</span><span class="n">col</span><span class="p">]</span> <span class="o">=</span> <span class="n">atl_w</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">to_dict</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">uniq_dict</span>

<span class="k">for</span> <span class="n">key</span> <span class="ow">in</span> <span class="n">uniq_dict</span><span class="p">:</span> 
    <span class="nb">print</span><span class="p">(</span><span class="n">key</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">days</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="p">(</span><span class="mi">2018</span><span class="p">,</span> <span class="mi">12</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span> <span class="o">-</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="p">(</span><span class="mi">2016</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;There are </span><span class="si">{}</span><span class="s2"> days between Jan 01 2016 and Dec 01 2018 [inclusive]&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">days</span><span class="o">.</span><span class="n">days</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">records_per_station</span> <span class="o">=</span> <span class="n">atl_w</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;NAME&#39;</span><span class="p">)[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">nunique</span><span class="p">()</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">records_per_station</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df_temp</span> <span class="o">=</span> <span class="n">atl_w</span><span class="p">[[</span><span class="s1">&#39;NAME&#39;</span><span class="p">,</span> <span class="s1">&#39;DATE&#39;</span><span class="p">,</span> <span class="s1">&#39;TAVG&#39;</span><span class="p">,</span> <span class="s1">&#39;TMAX&#39;</span><span class="p">,</span> <span class="s1">&#39;TMIN&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">df_airport</span> <span class="o">=</span> <span class="n">df_temp</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">df_temp</span><span class="p">[</span><span class="s1">&#39;NAME&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s2">&quot;ATLANTA HARTSFIELD INTERNATIONAL AIRPORT, GA US&quot;</span><span class="p">]</span>
<span class="n">df_airport</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dfa</span> <span class="o">=</span> <span class="n">df_airport</span>
<span class="n">dfa</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dfa</span> <span class="o">=</span> <span class="n">dfa</span><span class="o">.</span><span class="n">astype</span><span class="p">({</span><span class="s2">&quot;TAVG&quot;</span><span class="p">:</span> <span class="nb">float</span><span class="p">,</span> <span class="s2">&quot;TMAX&quot;</span><span class="p">:</span> <span class="nb">float</span><span class="p">,</span> <span class="s2">&quot;TMIN&quot;</span><span class="p">:</span> <span class="nb">float</span><span class="p">})</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dfa</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">pp</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">13</span><span class="p">,</span><span class="mi">6</span><span class="p">))</span>

<span class="n">mask2016</span> <span class="o">=</span> <span class="n">dfa</span><span class="p">[(</span><span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">&gt;=</span><span class="s1">&#39;2016-1-1&#39;</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">&lt;</span><span class="s1">&#39;2017-1-1&#39;</span><span class="p">)]</span> 
<span class="n">mask2017</span> <span class="o">=</span> <span class="n">dfa</span><span class="p">[(</span><span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">&gt;=</span><span class="s1">&#39;2017-1-1&#39;</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">&lt;</span><span class="s1">&#39;2018-1-1&#39;</span><span class="p">)]</span> 
<span class="n">mask2018</span> <span class="o">=</span> <span class="n">dfa</span><span class="p">[(</span><span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">&gt;=</span><span class="s1">&#39;2018-1-1&#39;</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;DATE&#39;</span><span class="p">]</span><span class="o">&lt;=</span><span class="s1">&#39;2018-12-1&#39;</span><span class="p">)]</span> 

<span class="n">mask2016</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">&#39;line&#39;</span><span class="p">,</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;DATE&#39;</span><span class="p">,</span><span class="n">y</span><span class="o">=</span><span class="s1">&#39;TMAX&#39;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;red&#39;</span><span class="p">)</span>
<span class="n">mask2016</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">&#39;line&#39;</span><span class="p">,</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;DATE&#39;</span><span class="p">,</span><span class="n">y</span><span class="o">=</span><span class="s1">&#39;TMIN&#39;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">)</span>


<span class="n">pp</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Temperature (°F)&#39;</span><span class="p">)</span>
<span class="n">pp</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">ATL Airport Temperature (min, avg, max)</span><span class="se">\n</span><span class="s1">[Jan 01 2016 to Dec 01 2018]</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">14</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_days</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="nb">len</span><span class="p">(</span><span class="n">dfa</span><span class="p">)</span><span class="o">+</span><span class="mi">1</span><span class="p">))</span>

<span class="n">list_x</span> <span class="o">=</span> <span class="n">all_days</span>
<span class="n">list_y</span> <span class="o">=</span> <span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;TMAX&#39;</span><span class="p">]</span>


<span class="k">def</span> <span class="nf">plot_smoothed</span><span class="p">(</span><span class="n">drange</span><span class="p">,</span> <span class="n">temp</span><span class="p">,</span> <span class="n">win</span><span class="o">=</span><span class="mi">10</span><span class="p">):</span>
    <span class="n">smoothed</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">correlate</span><span class="p">(</span><span class="n">temp</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">ones</span><span class="p">(</span><span class="n">win</span><span class="p">)</span><span class="o">/</span><span class="n">win</span><span class="p">,</span><span class="s1">&#39;same&#39;</span><span class="p">)</span>    
    <span class="n">pp</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">drange</span><span class="p">,</span><span class="n">smoothed</span><span class="p">)</span>

<span class="c1">#pp.plot(list_x,list_y)</span>
<span class="c1">#plot_smoothed()</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">pp</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">13</span><span class="p">,</span><span class="mi">6</span><span class="p">))</span>
<span class="n">plot_smoothed</span><span class="p">(</span><span class="n">all_days</span><span class="p">,</span> <span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;TMAX&#39;</span><span class="p">],</span> <span class="mi">20</span><span class="p">)</span>
<span class="n">plot_smoothed</span><span class="p">(</span><span class="n">all_days</span><span class="p">,</span> <span class="n">dfa</span><span class="p">[</span><span class="s1">&#39;TMIN&#39;</span><span class="p">],</span> <span class="mi">20</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># </span>
</pre></div>

    </div>
</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>
