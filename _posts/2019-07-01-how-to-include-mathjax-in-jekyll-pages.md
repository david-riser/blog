---
layout: post
author: David
---

In the welcome post, you'll notice that I used latex-like math symbols.  Those are powered by MathJax, and here is how I made it work. 

### Create an Include File 
Create a new file in your _includes folder called math.html with the following contents:

{% highlight html %}
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    extensions: [
      "MathMenu.js",
      "MathZoom.js",
      "AssistiveMML.js",
      "a11y/accessibility-menu.js"
    ],
    jax: ["input/TeX", "output/CommonHTML"],
    TeX: {
      extensions: [
        "AMSmath.js",
        "AMSsymbols.js",
        "noErrors.js",
        "noUndefined.js",
      ]
    }
  });
</script>

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
{% endhighlight %}

this part is based on the following [post](https://quuxplusone.github.io/blog/2018/08/05/mathjax-in-jekyll).

### Inject This Into Your Layout
In your _layouts folder, you can include this in the default header as shown below.

{% highlight html %}

<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: "en" }}">
  <%- include head.html -%>
  <%- include math.html -%>

  <body>

    <%- include header.html -%>

    <main class="page-content" aria-label="Content">
      <div class="wrapper">
        {{ content }}
      </div>
    </main>

    <%- include footer.html -%>

  </body>

</html>
{% endhighlight %}

In the block above, I replaced the liquid command "{" symbol with a "<" symbol so that the text would render properly, you'll need to change those back to liquid tags in order for everything to work.

### Test Your MathJax 
You should now be able to include equations using the simple latex-like syntax. 

{% highlight latex %}
$$ f(x) = \frac{x^2}{\ln(x)} $$
{% endhighlight %}

Which renders as:
$$ f(x) = \frac{x^2}{\ln(x)} $$

Very nice!  You can also use full latex environments like align and gather. The following gather block produces a nice output.

{% highlight latex %}
$$
\begin{gather}
x = 5 & y = 7 \\
z = 3 & k = -1
\end{gather}
$$
{% endhighlight %}

$$
\begin{gather}
x = 5 & y = 7 \\
z = 3 & k = -1
\end{gather}
$$
