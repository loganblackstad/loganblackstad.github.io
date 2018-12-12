---
title: Jekyll Markdown Style Guide - Quick Reference
date: 2018-12-12
tags: [ Jekyll, Markdown ]
---


Let's see how `markdown` is rendered in `HTML`.

First, let's take a look at some raw markdown(displayed in the window below).  Then we can compare it to the HTML output rendered under it. 

```markdown
This is a demo of some styled elements: 

[View the markdown used to create this post](https://github.com/loganblackstad/loganblackstad.github.io/blob/master/_posts/2018-12-12-Jekyll-Markdown-Quick-Reference.md).


This is a paragraph, it's surrounded by whitespace. Next up are some headers, they're heavily influenced by GitHub's markdown style.

## Header 2 (H1 is reserved for post titles)##
### Header 3
#### Header 4
 
A link to my [GitHub Repositories](https://github.com/loganblackstad/). 
A literal link: <https://github.com/loganblackstad/>
  
An image, located within "/assets/images" :
![Coding Icon Image]({{ site.baseurl }}/assets/images/icon-sencha-test-studio-1.png "Coding Icon Image")


* A bulletted list
- alternative syntax 1
+ alternative syntax 2
  - an indented list item

1. An
2. ordered
3. list

Inline markup styles: 

- _italics_
- **bold**
- `code()` 
 
> Blockquote
>> Nested Blockquote 
 
Syntax highlighting can be used by wrapping your code in a liquid tag like so:

{{ "{% highlight javascript " }}%}  
/* Some pointless Javascript */
var rawr = ["r", "a", "w", "r"];
{{ "{% endhighlight " }}%}  

creates...

{% highlight javascript %}
/* Some pointless Javascript */
var rawr = ["r", "a", "w", "r"];
{% endhighlight %}
 
Use two trailing spaces  
on the right  
to create linebreak tags  
 
Finally, horizontal lines
 
----
****
```

--------------

Now let's see how it renders in `HTML`:

----
This is a demo of some styled elements: 

[View the markdown used to create this post](https://github.com/loganblackstad/loganblackstad.github.io/blob/master/_posts/2018-12-12-Jekyll-Markdown-Quick-Reference.md).


This is a paragraph, it's surrounded by whitespace. Next up are some headers, they're heavily influenced by GitHub's markdown style.

## Header 2 (H1 is reserved for post titles)##
### Header 3
#### Header 4

<br>
<br>
A link to my [GitHub Repositories](https://github.com/loganblackstad/).  
A literal link: <https://github.com/loganblackstad/>
  
An image, located within "/assets/images" :  
![Coding Icon Image]({{ site.baseurl }}/assets/images/icon-sencha-test-studio-1.png "Coding Icon Image")


* A bulletted list
- alternative syntax 1
+ alternative syntax 2
  - an indented list item

1. An
2. ordered
3. list

Inline markup styles: 

- _italics_
- **bold**
- `code()` 
 
> Blockquote
>> Nested Blockquote 
 
Syntax highlighting can be used by wrapping your code in a liquid tag like so:

{{ "{% highlight javascript " }}%}  
/* Some pointless Javascript */
var rawr = ["r", "a", "w", "r"];  
{{ "{% endhighlight " }}%}  

creates...

{% highlight javascript %}
/* Some pointless Javascript */
var rawr = ["r", "a", "w", "r"];
{% endhighlight %}
  
<br>
Use two trailing spaces  
on the right  
to create linebreak tags  

<br> 
Finally, horizontal lines
 
----
****