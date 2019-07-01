---
layout: post
author: David
---

In many scientific and computing blog posts, it is useful to be able to insert forumlas.  Most scientists use a typesetting language called latex to format equations, and it is quite easy to add support for latex to Jekyll using MathJax.    

Using MathJax, you can write simple equation blocks: 
{% highlight latex %}
$$ f(x) = \frac{x^2}{\ln(x)} $$
{% endhighlight %}

which render as, 

$$ f(x) = \frac{x^2}{\ln(x)} $$

as well as more complex latex structure such as:
{% highlight latex %}
$$
\begin{gather}
x = 5, & y = 7 \\
z = 3, & k = -1
\end{gather}
$$
{% endhighlight %}

which also render nicely.

$$
\begin{gather}
x = 5, & y = 7 \\
z = 3, & k = -1
\end{gather}
$$

### Overview
In order to achieve this, we will: 
- Add the required Javascript to your `_includes` directory
- Make sure those lines are included in your layout by adding them to the default layout header
That is it! 

### Create an Include File 
Create a new file in your `_includes` folder called `math.html` with the following contents:

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
In your `_layouts` folder, you can include this in the default header as shown below.

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
You should now be able to include equations using the simple latex-like syntax shown in the introduction. 
