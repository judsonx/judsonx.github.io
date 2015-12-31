---
layout: post
title:  "Jekyll with Bootstrap"
categories: tutorial jekyll
---

After using **[jekyll]** for a few weeks, I decided to make an attempt at
integrating **[Bootstrap]**. Fortunately, this is not an uncommon combination,
and there are a number tutorials available online. I decided to follow one
titled **[Jekyll with Twitter Bootstrap Sass][tutorial]**, but with some
modifications.

Here is how I added **Bootstrap** to my **jekyll** project (for **Bootstrap
3.3.5** and **jekyll 2.5.3**):

### First

Download [Bootstrap-Sass] and unzip the ``assets`` folder to the root folder
of your Jekyll project.

### Second

Create a Sass stylesheet that will be used to generate the CSS for Bootstrap.
I created ``assets/stylesheets/style.scss`` with the following content:

{% highlight sass %}
---
---

@import "../assets/stylesheets/bootstrap";
{% endhighlight %}

This will result in the generation of ``_site/assets/stylesheets/style.css``.

### Third

Add a link to the generated Bootstrap CSS file in ``_includes/head.html``:

{% highlight liquid %}{% raw %}
<link rel="stylesheet" href="{{ "/assets/stylesheets/style.css" | prepend: site.baseurl }}">
{% endraw %}{% endhighlight %}

The link should be added inside the ``<head>`` and ``</head>`` tags (I added
mine just before the closing tag).

### Almost Done

Add a link to [jQuery] and ``bootstrap.js`` in ``_layouts/default.html``:

{% highlight liquid %}{% raw %}
<script src="//code.jquery.com/jquery-1.11.3.min.js"></script>
<script src="{{ "/assets/javascripts/bootstrap.js" | prepend: site.baseurl }}"></script>

<div class="page-content">
...
</div>
{% endraw %}{% endhighlight %}

### Finally

Check to see if it works! Try adding the following HTML to one of your posts or
pages:

{% highlight html %}
<div class="panel panel-success">
  <div class="panel-heading">
    <h3 class="panel-title">
      <span class="glyphicon glyphicon-ok text-success"></span> Result
    </h3>
  </div>
  <div class="panel-body">
    Bootstrap features should now be available to all of your pages.
    <button type="button" class="btn btn-sm btn-default" data-toggle="popover"
      title="Popover"
      data-content="If you are seeing this, then it probably works!"
    >Show Popover</button>
  </div>
</div>
{% endhighlight %}

The above snippet also requires some initialization:

{% highlight html %}{% raw %}
<script>
$(function () { $('[data-toggle="popover"]').popover(); });
</script>
{% endraw %}{% endhighlight %}

The end result should look something like this:

<div class="panel panel-success">
  <div class="panel-heading">
    <h3 class="panel-title">
      <span class="glyphicon glyphicon-ok text-success"></span> Result
    </h3>
  </div>
  <div class="panel-body">
    Bootstrap features should now be available to all of your pages.
    <button type="button" class="btn btn-sm btn-default" data-toggle="popover"
      title="Popover"
      data-content="If you are seeing this, then it probably works!"
    >Show Popover</button>
  </div>
</div>

### Some Customization

  1. Increase font size.
  2. Make code blocks scroll instead of wrap. See also,
  [How to support scrolling when using pygments with Jekyll][so1].

I ended up with the following content in ``assets/stylesheets/style.scss``:

{% highlight sass %}
---
---

// Bootstrap overrides (before import)
$font-size-base: 16px;

@import "../assets/stylesheets/bootstrap";

// Don't wrap highlight code blocks.
.highlight {
  pre code * {
    white-space: nowrap;
  }

  pre {
    overflow-x: auto;
    word-wrap: normal;
  }

  pre code {
    white-space: pre;
  }
}
{% endhighlight %}

### Other Links:
  - [kramdown]
  - [Sass]
  - [jQuery CDN]
  - [Liquid]

<script>
$(function () { $('[data-toggle="popover"]').popover(); });
</script>

[jekyll]: http://jekyllrb.com 
[kramdown]: http://kramdown.gettalong.org
[Sass]: http://sass-lang.com
[Bootstrap]: http://getbootstrap.com
[Bootstrap-Sass]: https://github.com/twbs/bootstrap-sass/releases
[jQuery]: https://jquery.com
[jQuery CDN]: http://code.jquery.com
[Liquid]: http://jekyllrb.com/docs/templates/
[tutorial]: http://jekyll.pygmeeweb.com/2014/08/02/jekyll-with-twitter-bootstrap-sass/
[so1]: http://stackoverflow.com/questions/11093233/how-to-support-scrolling-when-using-pygments-with-jekyll
