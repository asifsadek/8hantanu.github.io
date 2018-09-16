---
title: "Mathjax Test"
categories:
  - gecko taco
tags:
  - problem solving
  - series
  - math
last_modified_at: 2018-09-06T12:30:00+05:30
---

**How to approach the following two dimensional recurrence relation ?**

For $$i,j\ge2$$,

$$a_{i,\ j}\ =\ a_{i,\ j-1}\ +\ a_{i-1,\ j-1}$$

where $$a_{p,\ 1}=1$$ (for $$p\ge1$$) and $$a_{1,\ q} = 1$$ (for $$q\ge1)$$.

**Solution**:

One way to go about this and generally about solving recurrence relations is to use generating functions, in this case this will lead to two variable generating function.

Let's suppose we have $$f(x,y)=\sum_{i,j=0}^{\infty}a_{i,j} x^i y^j$$ formal powers series which encodes coefficients of your sequence. For simplicity, here we have it shifted, so actually $$a_{0,q}=a_{p,0}=1$$, but don't worry about that, we can shift this back at the end. Now let's play with coefficients a little to see if we can get better form of $$f(x,y)$$:

$$
\begin{align}
f(x,y)&=\sum_{i,j=0}^{\infty}a_{i,j} x^i y^j \\
&=a_{0,0}+\sum_{i=1}^{\infty}a_{i,0} x^i+\sum_{j=1}^{\infty}a_{0,j} y^j + \sum_{i,j=1}^{\infty}a_{i,j} x^i y^j \\
\end{align}
$$

Now we have shifted the indices (you will see later why), but before proceeding, notice $$a_{0,0}=1$$ and that

$$
\sum_{i=1}^{\infty}a_{i,0} x^i = x+x^2+x^3+\dots = \frac{x}{1-x}
$$

and similarly for the second sum. So overall we have

$$
f(x,y) = 1+\frac{x}{1-x}+\frac{y}{1-y}+\sum_{i,j=1}^{\infty}a_{i,j} x^i y^j
$$

Now for the rightmost sum, lets write

$$
\begin{align}
\sum_{i,j=1}^{\infty}a_{i,j} x^i y^j &= \sum_{i,j=1}^{\infty}(a_{i,j-1}+a_{i-1,j-1}) x^i y^j \\
&= \sum_{i,j=1}^{\infty}a_{i,j-1} x^i y^j+\sum_{i,j=1}^{\infty}a_{i-1,j-1} x^i y^j \\
&= y\sum_{i,j=1}^{\infty}a_{i,j-1} x^i y^{j-1}+xy\sum_{i,j=1}^{\infty}a_{i-1,j-1} x^{i-1} y^{j-1}\\
\end{align}
$$

Here we have just applied the recurrence relation (this is why we moved the $$0$$ indices out before) and then moved the $$x$$,$$y$$ out of the sum, so that indices match. Now lets just re-index the sum

$$
\begin{align}
\sum_{i,j=1}^{\infty}a_{i,j} x^i y^j &= y\sum_{i,j=1}^{\infty}a_{i,j-1} x^i y^{j-1}+xy\sum_{i,j=1}^{\infty}a_{i-1,j-1} x^{i-1} y^{j-1}\\
&= y\sum_{i=1,j=0}^{\infty}a_{i,j} x^i y^{j}+xy\sum_{i,j=0}^{\infty}a_{i,j} x^{i} y^{j}\\
&= y\left(\sum_{i=0,j=0}^{\infty}a_{i,j} x^i y^{j}-\sum_{j=0}^{\infty}a_{0,j}\right)+xy\sum_{i,j=0}^{\infty}a_{i,j} x^{i} y^{j}\\
&= y\left(f(x,y)-\sum_{j=0}^{\infty}a_{0,j}\right)+xyf(x,y)\\
&= y\left(f(x,y)-\frac{1}{1-y}\right)+xyf(x,y)\\
\end{align}
$$


Here we have just substituted back the definition of $$f(x,y)$$ itself. Now putting back together we have

$$
\begin{align}
f(x,y)=1+\frac{x}{1-x}+\frac{y}{1-y}+ y\left(f(x,y)-\frac{1}{1-y}\right)+xyf(x,y)\\
\end{align}
$$

and after some simple algebraic manipulations we finally get:

$$
\begin{align}
f(x,y) = \frac{1}{(1-x)(1-y-xy)}\\
\end{align}
$$


Now the $$f(x,y)$$ encodes all of the coefficients in a compact way. We can now try to write it in a way that will allow us to see the coefficients more clearly.

For this notice that $$\frac{1}{1-x}=1+x+x^2+x^3+\dots$$. Also second expression is well known generating function $$\frac{1}{1-y-yx}=\frac{1}{1-y(x+1)}=\sum_{i,j=0}^{\infty}\binom{j}{i} x^i y^j.$$

So we can view our function in this form as a product

$$
f(x,y) = (1+x+x^2+x^3+\dots) \left(\sum_{i,j=0}^{\infty}\binom{j}{i} x^i y^j\right)
$$

Now to ask what is the value of $$a_{i,j}$$ is same as to ask what coefficient of $$x^i y^j$$ is in this product. It is not hard to see that it will be $$\binom{j}{i}+\binom{j}{i-1}+\dots+\binom{j}{0}$$. So overall, also with correcting the original offset from $$i$$ to $$i-1$$ and $$j$$ to $$j-1$$, we get

$$a_{i,j} = \sum_{k=0}^{i-1}\binom{j-1}{k}.$$
