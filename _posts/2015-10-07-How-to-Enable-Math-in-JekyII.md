---
layout: post
title: How to enable math in JekyII
---

As a scientific worker, math description is inevitable. `Latex` is powerful and necessary tool for those writing scientific paper or notes. To share the idea or work online, I am searching for easy way to display the math.

My first trial is `JekyII` and `MathJax`, which is simple to set up.



* Edit the `_config.yml` to use `kramdown` as the markdown
   {% highlight yaml %}   
   markdown: kramdown
   kramdown:
     math_engin: mathjax
     {% endhighlight %}
* Add the `Mathjax` in the template `_layout\post.html`
   {% highlight html %}
   <article ...>
   ...
    <script type="text/javascript"
        src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
    </script>
   </article>
   {% endhighlight %}

Now you can enjoy playing with math

* Inline expression like $$ E = m c^2 $$

  ```
  Inline expression like $$ E = m c^2 $$
  ```
  
* Block expression 

$$
\begin{align}
f(x) & \sim \mathcal{GP}(\mathcal{K}) \tag{1}\\
g(x) & = ax + b \tag{2}
\end{align}
$$

{% highlight tex%}
$$
\begin{align}
f(x) & \sim \mathcal{GP}(\mathcal{K}) \tag{1}\\
g(x) & = ax + b \tag{2}
\end{align}
$$
{% endhighlight %}



   


