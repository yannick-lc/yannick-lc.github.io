---
layout: post
title:  "Matrix Reloaded: introduction to matrix calculus"
date:   2025-07-24 10:22:40 +0200
update_date:  2025-07-24 11:22:40 +0200
last_modified_at:  2025-07-29
categories: foundations
permalink: /blog/matrix-calculus/
description: "A gentle introduction to matrix calculus for machine learning. Learn derivatives of scalars, vectors and matrices w.r.t. one another. With examples & exercises."
image: /assets/img/matrix-calculus/neo-confused2.jpg
---

<img class="center-image" src="{{ '/assets/img/matrix-calculus/neo-confused2.jpg' | relative_url }}" alt="Confused Neo" width="300"/>
<div class="figure-legend">
Poor Neo doesn't know the Matrix has a derivative with respect to a vector and is all confused.<br/>
But he won't be anymore if he reads this article.
</div>

<br/> 

As anyone who graduated from kindergarten knows, given $N$ vectors of $K$-dimensional features stacked in a matrix $\mathbf{X} = (\mathbf{x}_1, \dots, \mathbf{x}_N)^\top \in \mathbb{R}^{N \times K}$ and a vector of $N$ labels $\mathbf{y} = (y_1, \dots, y_N)^\top \in \mathbb{R}^{N}$, the weights $\mathbf{w} \in \mathbb{R}^{K}$ of the least square linear regression model can be obtained with

$$
\mathbf{w} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}
$$

*Nah*, just kidding.

I mean, yes, it's true. But I'd say it's really not *that* obvious.

In fact, this result is something I used to try to memorize before my first machine learning interviews. You know, in case this came up in the discussion.
I think it was mentioned in the slides on linear regression in a course I took at university, but at the time, I did not fully understand where this result came from — partly because I was not well-versed in matrix calculus.

This article is thus meant to be a gentle introduction to vector/matrix calculus for past [Yannick][yannick]. Or, more generally, for people who never took a formal math class in multivariate calculus, and who, when first confronted with the idea of taking the derivative of something with respect to a matrix, reacted with:

*"Wait... What? You can do that?"*

I will try to explain how we can go from simple definitions, that rely only on basic calculus and algebra, to deriving more interesting and useful results like the one above. This should hopefully be useful to:
1. Get a better understanding of standard machine learning algorithms and results
2. Develop the ability to identify situations where matrix calculus may be useful to derive analytical solutions

Similarly to the habit of [writing everything in matrix notation][matrix-notation], the latter skill has helped me achieve 100-fold speedups of machine learning code quite a few times, in both academic and industrial projects. So I'd say that it's a trick that any Machine Learning Legend should have up their sleeve.

<details markdown="1">
<summary>Disclaimer for math purists</summary>

The objective of this article is to provide a *gentle* introduction to the topic of matrix calculus as used in the field of machine learning.
As such, I focus mainly on providing basic definitions and the intuitions behind those, as well as a few applications of matrix calculus.

I apologize in advance to pure math majors for lacking mathematical rigor in some/most parts of the article. In particular, I generally won't bother to first question if the derivative of a function exists etc etc: I just assume it does and that what we are doing makes sense, as doing otherwise would unnecessarily complexify an already fairly long article.

Finally, I focus mostly on the algebraic aspect of matrix calculus, mostly skipping the geometric intuition for now.
</details>

The objective is to move gently with a step-by-step approach, so that everything in the summary below makes perfect sense by the end of this article.

<details markdown="1">
<summary>TL;DR</summary>

<a id="tldr"></a>

Here is a brief and slightly indigestible summary of the content covered in the article, for future reference or to check if you would benefit from reading it.

Summary of definitions:
<div class="goldhighlight" markdown="1">
Given a real-valued quantity $f(\mathbf{X}) \in \mathbb{R}$ that depends on $M \times N$ variables organized in a matrix
$\mathbf{X} \in \mathbb{R}^{M \times N}$,
the gradient $\frac{\partial f}{\partial \mathbf{X}} \in \mathbb{R}^{M \times N}$ of $f(\mathbf{X})$ with respect to $\mathbf{X}$ is given by

$$
\left( \frac{\partial f}{\partial \mathbf{X}}\right)_{m,n} = \frac{\partial f}{\partial x_{m,n}}
\quad \forall m,n
$$

Given a function which maps a scalar $x \in \mathbb{R}$ to a matrix $\mathbf{F}(x) \in \mathbb{R}^{M \times N}$, the derivative $\frac{\partial \mathbf{F}}{\partial x} \in \mathbb{R}^{M \times N}$ of $\mathbf{F}$ with respect to $x$ is given by

$$
\left( \frac{\partial \mathbf{F}}{\partial x}\right)_{m,n} = \frac{\partial f_{m,n}}{\partial x}
\quad \forall m,n
$$

Given a function which maps a vector $\mathbf{x} \in \mathbb{R}^N$ to another vector $\mathbf{f}(\mathbf{x}) \in \mathbb{R}^M$, the derivative $\frac{\partial \mathbf{f}}{\partial \mathbf{x}} \in \mathbb{R}^{M \times N}$ of $\mathbf{f}$ with respect to $\mathbf{x}$ is given by

$$
\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{m,n} = \frac{\partial f_{m}}{\partial x_n}
\quad \forall m,n
$$

</div>

Summary of the summary:

<div class="goldhighlight" markdown="1" style="background-color: #fef3d5;">
Given a rank-$P$ tensor $\mathcal{F} \in \mathbb{R}^{M_1 \times \dots \times M_P}$ whose coordinates
$$\mathcal{f}_{m_1, \dots, m_P}$$ are defined in terms of an input rank-$R$ tensor $\mathcal{X} \in \mathbb{R}^{N_1 \times \dots \times N_R}$ with coordinates $x_{n_1, \dots, n_R}$, the coordinates of the rank-$(P+R)$ tensor derivative $$\frac{\partial \mathcal{F}}{\partial  \mathcal{X}} \in \mathbb{R}^{M_1 \times \dots \times M_P \times N_1 \times \dots \times N_R}$$ of $\mathcal{F}$ with respect to $\mathcal{X}$ are given by

$$
\left( \frac{\partial \mathcal{F}}{\partial \mathcal{X}}\right)_{m_1, \dots, m_P, n_1, \dots, n_R} = \frac{\partial f_{m_1,\dots,m_P}}{\partial x_{n_1, \dots, n_R}}
\quad \forall m_1, \dots, m_P, n_1, \dots, n_R
$$

</div>

Summary of the part on linear regression:

<div class="silverhighlight" markdown="1">
Given $N$ vectors of $K$-dimensional features stacked in a matrix $\mathbf{X} = (\mathbf{x}_1, \dots, \mathbf{x}_N)^\top \in \mathbb{R}^{N \times K}$ and a vector of $N$ labels $\mathbf{y} = (y_1, \dots, y_N)^\top \in \mathbb{R}^{N}$, the least square linear regression model aims to find the weights $\mathbf{w} \in \mathbb{R}^{K}$ which minimize the training loss

$$
\mathcal{L}(\mathbf{w}) = ||\mathbf{Xw} - \mathbf{y}||_2^2
$$

The gradient of this training loss $\mathcal{L}(\mathbf{w})$ with respect to parameters $\mathbf{w}$ is

$$
\frac{\partial \mathcal{L}(\mathbf{w})}{\partial \mathbf{w}} = 2\mathbf{X}^\top (\mathbf{Xw} - \mathbf{y})
$$

The training loss is minimized when the gradient of the training loss is zero, which happens when

$$
\mathbf{w} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}
$$

</div>
</details>

## Derivatives of everything with respect to everything

### The basics: (partial) derivative of a scalar with respect to a scalar

I am assuming you are already familiar with univariate calculus. For example, given the function

$$
f: \mathbb{R} \rightarrow \mathbb{R}, \quad x \mapsto x^3 -2x +1
$$

we can say that the *derivative* of $f(x)$ with respect to $x$ is

$$
f^\prime(x) = \frac{d f(x)}{d x} = 3x^2 -2
$$

In the case of an expression that contains several variables, such as

$$
f(x,y) = 2x^2 + 4y
$$

we can obtain the *partial derivative* of $f$ with respect to $x$ by pretending that $y$ is a constant, and similarly obtain the partial derivative of $f$ with respect to $y$:

$$
\begin{align*}
\frac{\partial f(x,y)}{\partial x} = 4x + 4y \\
\frac{\partial f(x,y)}{\partial y} = 2x^2 + 4 \\
\end{align*}
$$

The vector
$$\begin{pmatrix}
\frac{\partial f(x,y)}{\partial x} \\
\frac{\partial f(x,y)}{\partial y}
\end{pmatrix}
$$, also written $\left(\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}\right)^\top$ to declutter notation\*,
is called the *gradient* of $f$ with respect to $$\begin{pmatrix}x \\ y\end{pmatrix} \in \mathbb{R}^2$$, the vector of input variables.

*\*You may want to check [this article][matrix-notation] on matrix notations if this notation is unclear. In fact, you should probably read it first.*

### Derivatives of a scalar with respect to things

We can then fairly easily generalize this result to functions of $N$ variables:

<div class="goldhighlight" markdown="1">
Given a function $f: \mathbb{R}^N \rightarrow \mathbb{R}$ of $N$ variables $$\mathbf{x} = \begin{pmatrix}x_1 \\ x_2 \\ \vdots \\ x_N\end{pmatrix}$$, the gradient of $f$ with respect to $\mathbf{x}$ is

$$
\frac{\partial f}{\partial \mathbf{x}} = 
\begin{pmatrix}
\frac{\partial f}{\partial x_1} \\
\vdots \\
\frac{\partial f}{\partial x_N} \\
\end{pmatrix} \in \mathbb{R}^N
\quad \quad \quad \quad
\text{i.e.} \quad
\left( \frac{\partial f}{\partial \mathbf{x}}\right)_n = \frac{\partial f}{\partial x_n}
\quad \forall n
$$

</div>

A few important things to notice: here, $f$ maps multiple input values $x_1, \dots, x_N$, or equivalently a vector input $\mathbf{x} = (x_1, \dots, x_N)^\top \in \mathbb{R}^N$, to a *single*, real-valued output $f(\mathbf{x}) \in \mathbb{R}$.

In this case, the gradient $\frac{\partial f}{\partial \mathbf{x}}$, sometimes also written $\nabla f$ or $\nabla_\mathbf{x}f$, has the same dimension as the input vector $\mathbf{x} \in \mathbb{R}^N$.

The function does not have to be explicitly defined as a function: any real-valued expression that involves multiple variables, e.g. $\frac{2x_1 + x_2^2}{1 - x_3}$, can be considered to be an implicit function from $\mathbb{R}^N$ to $\mathbb{R}$ for which we may want to estimate a gradient.

*(Quick exercise: determine the gradient of $\frac{2x_1 + x_2^2}{1 - x_3}$ with respect to $\mathbf{x} = (x_1, x_2, x_3)^\top$)*

<details>
<summary><em>Solution</em></summary>

Writing $f(x_1, x_2, x_3) = f(\mathbf{x}) = \frac{2x_1 + x_2^2}{1 - x_3}$,

$$
\frac{\partial f(\mathbf{x})}{\partial \mathbf{x}}
= \left(\frac{\partial f(\mathbf{x})}{\partial x_1}, \frac{\partial f(\mathbf{x})}{\partial x_2}, \frac{\partial f(\mathbf{x})}{\partial x_3}\right)^\top
= \left(\ \frac{2}{1 - x_3}, \frac{2x_2}{1 - x_3}, \frac{2x_1 + x_2^2}{(1 - x_3)^2} \right)^\top
$$

</details>

Can we generalize this to objects other than vectors? Yes, again quite easily:

<div class="goldhighlight" markdown="1">
Given a real-valued quantity $f(\mathbf{X}) \in \mathbb{R}$ that depends on $M \times N$ variables organized in a matrix
$$\mathbf{X} = \begin{pmatrix}
x_{1,1} & \dots & x_{1,N} \\
\vdots & \ddots & \vdots \\
x_{M,1} & \dots & x_{M,N} \\
\end{pmatrix} \in \mathbb{R}^{M \times N}$$,
the derivative/gradient of $f(\mathbf{X})$ with respect to $\mathbf{X}$ is

$$
\frac{\partial f}{\partial \mathbf{X}} = 
\begin{pmatrix}
\frac{\partial f}{\partial x_{1,1}} & \dots & \frac{\partial f}{\partial x_{1,N}}\\
\vdots & \ddots & \vdots \\
\frac{\partial f}{\partial x_{M,1}} & \dots & \frac{\partial f}{\partial x_{M,N}} \\
\end{pmatrix} \in \mathbb{R}^{M \times N}
\quad \quad \quad \quad
\text{i.e.} \quad
\left( \frac{\partial f}{\partial \mathbf{X}}\right)_{m,n} = \frac{\partial f}{\partial x_{m,n}}
\quad \forall m,n
$$

</div>

An example of such a function could be
$$f(\begin{pmatrix}x_{1,1} & x_{1,2} \\ x_{2,1} & x_{2,2}\end{pmatrix}) = x_{1,1}x_{2,2} - x_{1,2}x_{2,1}$$, which would be the definition of the [determinant](https://en.wikipedia.org/wiki/Determinant) of a $2 \times 2$ matrix.

*Exercise: determine the derivative of $f$ above with respect to its input $\mathbf{X}$.*

<details>
<summary><em>Solution</em></summary>

$$
\frac{\partial f(\mathbf{X})}{\partial \mathbf{X}}
= \begin{pmatrix}
\frac{\partial f(\mathbf{X})}{\partial x_{1,1}} & \frac{\partial f(\mathbf{X})}{\partial x_{1,2}} \\
\frac{\partial f(\mathbf{X})}{\partial x_{2,1}} & \frac{\partial f(\mathbf{X})}{\partial x_{2,2}}
\end{pmatrix}
= \begin{pmatrix}
x_{2,2} & -x_{2,1} \\
-x_{1,2} & x_{1,1}
\end{pmatrix}
$$

</details>

We could even further generalize this to any scalar-valued function of a tensor, although this would be slightly out of the scope I initially planned for this article *(and if you don't know what a tensor is, don't worry about it for now)*.

<details markdown="1">
<summary>Bonus: gradient with respect to a tensor</summary>

<div class="goldhighlight" markdown="1">
Given a scalar-valued function $f(\boldsymbol{\mathcal{X}}) \in \mathbb{R}$ of a rank-$R$ tensor $\boldsymbol{\mathcal{X}} \in \mathbb{R}^{N_1 \times \dots \times N_R}$, the gradient of $f$ with respect to $\boldsymbol{\mathcal{X}}$ is given by

$$
\left( \frac{\partial f}{\partial \boldsymbol{\mathcal{X}}}\right)_{n_1,\dots,n_R} = \frac{\partial f}{\partial x_{n_1,\dots,n_R}}
\quad  \forall n_1,\dots,n_R
$$

</div>
</details>

*All right, that's a good start!*

We only started a few minutes ago, and unlike past Yannick, we now know what it means to take the derivative of a function with respect to a matrix! Are we done?

Sorry, nope. So far, we have only considered *scalar-valued* functions. Let's change that.

### Derivatives of things with respect to a scalar

So, what happens if the output of our function is not a scalar? For example, what if it's a vector instead?

Let's consider functions of one variable only for now.

<div class="goldhighlight" markdown="1">
Given a function $\mathbf{f}: \mathbb{R} \rightarrow \mathbb{R}^N$ which maps a single value $x \in \mathbb{R}$ to an $N$-dimensional vector $\mathbf{f}(x) \in \mathbb{R}^N$, the derivative of $\mathbf{f}$ with respect to $x$ is

$$
\frac{\partial \mathbf{f}}{\partial x} = 
\begin{pmatrix}
\frac{\partial f_1}{\partial x} \\
\vdots \\
\frac{\partial f_N}{\partial x} \\
\end{pmatrix} \in \mathbb{R}^N
\quad \quad \quad \quad
\text{i.e.} \quad
\left( \frac{\partial \mathbf{f}}{\partial x}\right)_n = \frac{\partial f_n}{\partial x}
\quad \forall n
$$

</div>

An example of such a function or expression could be
$$\mathbf{f}(x) = \begin{pmatrix}2x^2 \\ 2 \\ -x\end{pmatrix}$$, in which case the derivative would be
$$\frac{\partial \mathbf{f}(x)}{\partial x} = \begin{pmatrix}4x \\ 0 \\ -1\end{pmatrix}$$.

Again, note the dimensions of each entity: the derivative $\frac{\partial \mathbf{f}}{\partial x}$ has as many dimensions as the output of the function $\mathbf{f}(x)$. Also note that since $x$ is a scalar, it is written in a non bold fold, whereas the output of $\mathbf{f}$ is a vector, so it is written with a bold lowercase letter, in accordance with the conventions explained in [this blog post][matrix-notation-notation].

The outputs of the function can also be arranged in a matrix:

<div class="goldhighlight" markdown="1">
Given a function $\mathbf{F}$ which maps a scalar $x \in \mathbb{R}$ to a matrix $\mathbf{F}(x) \in \mathbb{R}^{M \times N}$, the derivative of $\mathbf{F}$ with respect to $x$ is given by

$$
\frac{\partial \mathbf{F}}{\partial x} = 
\begin{pmatrix}
\frac{\partial f_{1,1}}{\partial x} & \dots & \frac{\partial f_{1,N}}{\partial x}\\
\vdots & \ddots & \vdots \\
\frac{\partial f_{M,1}}{\partial x} & \dots & \frac{\partial f_{M,N}}{\partial x} \\
\end{pmatrix} \in \mathbb{R}^{M \times N}
\quad \quad \quad \quad
\text{i.e.} \quad
\left( \frac{\partial \mathbf{F}}{\partial x}\right)_{m,n} = \frac{\partial f_{m,n}}{\partial x}
\quad \forall m,n
$$

</div>

An example of such a function could be
$$\mathbf{F}(x) = \begin{pmatrix}\sqrt{x} & 1 \\ x & x^2\end{pmatrix}$$. Computing its derivative is left as an exercise.

Generalizing this to tensors is straightforward.

<details markdown="1">
<summary>Derivative of a tensor with respect to a scalar</summary>

<div class="goldhighlight" markdown="1">
Given a function $\mathcal{F}$ which maps a scalar $x \in \mathbb{R}$ to a rank-$R$ tensor $\mathcal{F}(x) \in \mathbb{R}^{N_1 \times \dots \times N_R}$, the derivative of $\mathcal{F}$ with respect to $x$ is given by

$$
\left( \frac{\partial \boldsymbol{\mathcal{F}}}{\partial x}\right)_{n_1,\dots,n_R} = \frac{\partial f_{n_1,\dots,n_R}}{\partial x}
\quad  \forall n_1,\dots,n_R
$$

</div>

</details>

### Derivatives of vectors with respect to vectors

OK, so we have covered derivatives of vectors with respect to scalars, of scalars with respect to vectors... How about vectors with respect to vectors?

Ask and you shall receive!

<div class="goldhighlight" markdown="1">
Given a function $\mathbf{f}$ which maps a vector $\mathbf{x} \in \mathbb{R}^N$ to another vector $\mathbf{f}(\mathbf{x}) \in \mathbb{R}^M$, the derivative of $\mathbf{f}$ with respect to $\mathbf{x}$ is given by

$$
\frac{\partial \mathbf{f}}{\partial \mathbf{x}} = 
\begin{pmatrix}
\frac{\partial f_{1}}{\partial x_1} & \dots & \frac{\partial f_{1}}{\partial x_N}\\
\vdots & \ddots & \vdots \\
\frac{\partial f_{M}}{\partial x_1} & \dots & \frac{\partial f_{M}}{\partial x_N} \\
\end{pmatrix} \in \mathbb{R}^{M \times N}
\quad \quad \quad \quad
\text{i.e.} \quad
\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{m,n} = \frac{\partial f_{m}}{\partial x_n}
\quad \forall m,n
$$

</div>

$\frac{\partial \mathbf{f}}{\partial \mathbf{x}}$ is also called the *Jacobian matrix* of $\mathbf{f}$.
Note that the output vector $\mathbf{f}(\mathbf{x}) \in \mathbb{R}^M$ does not need to have the same dimension as the input vector $\mathbf{x} \in \mathbb{R}^N$, nor does the mapping between the two need to be linear.

An example of such a function could be
$\mathbf{f}(x_1,x_2,x_3)=\begin{pmatrix}x_1 + x_2 \\ -x_3^2\end{pmatrix}$.

*Exercise: compute the Jacobian $\frac{\partial \mathbf{f}}{\partial \mathbf{x}}$.*

<details>
<summary><em>Solution</em></summary>

$$
\frac{\partial \mathbf{f}(\mathbf{x})}{\partial \mathbf{x}} = \begin{pmatrix}
1 & 1 & 0 \\
0 & 0 & -2x_3
\end{pmatrix}
$$

</details>

<details markdown="1">
<summary>Why $m,n$ and not $n,m$?</summary>

A question one may ask is: why are the indices in this order in the definition? More specifically, why did we decide that
$$\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{m,n} = \frac{\partial f_{m}}{\partial x_n}$$,
and not
$$\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{n,m} = \frac{\partial f_{m}}{\partial x_n}$$?

If you asked me this question before 9AM, my answer would probably have been *"Mrmpf that's the convention, I don't make the rules. Where's my coffee?"*.

Fortunately, I am now more awake and in a good mood, so: one way to see why it makes sense is to consider the function $\mathbf{f}(\mathbf{x}) = \mathbf{Ax}$, with $\mathbf{x} \in \mathbb{R}^N$, $\mathbf{A} \in \mathbb{R}^{M \times N}$ and thus $\mathbf{f}(\mathbf{x}) \in \mathbb{R}^M$.

With our initial definition
$$\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{m,n} = \frac{\partial f_{m}}{\partial x_n}$$,
we can prove (and we will in a few sections) that

$$
\frac{\partial \mathbf{Ax}}{\partial \mathbf{x}} = \mathbf{A}
$$

which pleasantly reminds us of the identity $\frac{\partial ax}{\partial x} = a$ for scalars. What a delightful extension from the one-dimensional scalar world to the multi-dimensional matrix universe! Isn't nature wonderful?

With the definition
$$\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{n,m} = \frac{\partial f_{m}}{\partial x_n}$$ however, we would get

$$
\frac{\partial \mathbf{Ax}}{\partial \mathbf{x}} = \mathbf{A}^\top
$$

which feels... awkward and not quite right. So,
$$\left( \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\right)_{m,n} = \frac{\partial f_{m}}{\partial x_n}$$ it is then!

There are also other reasons for why it makes more sense to define it the way we did, but the example above should already give you a rough idea of why this might be.

</details>


### Derivatives of other things with respect to other things

OK, we have covered most of the things we will typically need in practice.

But I feel like stopping there would leave a bit of an itch, as some tempting generalizations were kept under the rug: what about derivatives of matrices with respect to vectors? And vectors w.r.t. matrices, matrices w.r.t. matrices, etc?

Let's try to answer the first question to see what happens. Let's consider a matrix $\mathbf{F} \in \mathbb{R}^{M \times N}$, whose coordinates $f_{m,n}$ are defined from a vector $\mathbf{x} \in \mathbb{R}^{K}$.
We could generalize the definition of the derivative of a vector w.r.t. a vector from earlier to consider our matrix output $\mathbf{F}$ instead of a vector output:

$$
\left( \frac{\partial \mathbf{F}}{\partial \mathbf{x}}\right)_{m,n,k} = \frac{\partial f_{m,n}}{\partial x_k}
\quad \forall m,n,k
$$

Notice the "issue"? Since $\mathbf{F}$ has 2 indices $m,n$ and $\mathbf{x}$ has 1 index $k$, we need a total of 3 indices $m,n,k$ to express the derivative of every element of $\mathbf{F}$ with respect to every element of $\mathbf{x}$.
So $\frac{\partial \mathbf{F}}{\partial \mathbf{x}}$ is neither a vector nor a matrix: it is a rank-3 tensor.

Now I don't want to spend too much time here explaining what a tensor is, but simply put: it can be seen as a generalization of vectors and matrices. A vector has 1 index so it is a rank-1 tensor, a matrix has 2 indices so it is a rank-2 tensor, and we can generalize to rank-3, 4, 5 or rank-$R$ tensors.
While being a tensor is not an issue per se (every mathematical object deserves respect, regardless of its rank), they are mostly out of the scope of this article.

*Want to learn more about tensors? Fear not, a more detailed but still gentle blog post about these cute little objects is in preparation.*

We can nonetheless attempt an ultimate definition, mostly to feel the satisfaction of finally having defined the derivative of everything with respect to everything.*

<sup><sub>*\*at least within a limited scope of (multi)linear algebra.*</sub></sup>

<div class="goldhighlight" markdown="1">
Given a rank-$P$ tensor $\mathcal{F} \in \mathbb{R}^{M_1 \times \dots \times M_P}$ whose coordinates
$$\mathcal{f}_{m_1, \dots, m_P}$$ are defined in terms of an input rank-$R$ tensor $\mathcal{X} \in \mathbb{R}^{N_1 \times \dots \times N_R}$ with coordinates $x_{n_1, \dots, n_R}$, the coordinates of the rank-$(P+R)$ tensor derivative $$\frac{\partial \mathcal{F}}{\partial  \mathcal{X}} \in \mathbb{R}^{M_1 \times \dots \times M_P \times N_1 \times \dots \times N_R}$$ of $\mathcal{F}$ with respect to $\mathcal{X}$ are given by

$$
\left( \frac{\partial \mathcal{F}}{\partial \mathcal{X}}\right)_{m_1, \dots, m_P, n_1, \dots, n_R} = \frac{\partial f_{m_1,\dots,m_P}}{\partial x_{n_1, \dots, n_R}}
\quad \forall m_1, \dots, m_P, n_1, \dots, n_R
$$

</div>

And there it is!

Technically, simply stating this pretty much sums up everything we have seen so far. Yet, I feel that limiting this blog post to this definition may not have been the most pedagogical approach imaginable. Let me know what you think in the comments!

## Interlude/practice time!

Phew! That may have been a lot to digest. But at least now we know what it means to take the derivative of something with respect to a matrix etc etc.

Now. You know what's a great way to make sure that we don't forget what we just saw?

*Practice, of course!*

This way, we can consolidate what we just learned, continue building intuition *and* in the process derive a few useful results. How cool is that?

In case you want to blatantly disregard what I just recommended and are mostly interested in seeing the derivation of the "main" result from the introduction, feel free to skip directly to the next section, *Le plat de résistance*.
Be warned though: some of the intermediate results from this section may be used to derive this "main" result, so it's always interesting to see where they come from.

#### Result 1 — derivative of a dot product

A first simple result we may want to prove is that, for vectors $\mathbf{x}, \mathbf{a} \in \mathbb{R}^N$,

$$
\frac{\partial \mathbf{a}^\top\mathbf{x}}{\partial \mathbf{x}} = \mathbf{a}
$$

First, notice that the dimensions of every entity here seem to be consistent: $\mathbf{a}$ and $\mathbf{x}$ have the same dimension so $\mathbf{a}^\top\mathbf{x}$ is defined and $\mathbf{a}^\top\mathbf{x} \in \mathbb{R}$. $\mathbf{a}^\top\mathbf{x}$ is a scalar so its gradient with respect to $\mathbf{x}$ should have the same dimension as $\mathbf{x}$: this is indeed the case here. In this example, we are thus considering *the gradient of a scalar with respect to a vector*.

In general, it is good practice to always do this type of sanity check before jumping into calculations. It helps clarify the role of each entity, and trains your muscle memory to detect inconsistencies when [writing in matrix notation][matrix-notation].

OK, onto the calculations then.

<details markdown="1">
<summary>Calculations</summary>

$\mathbf{a}^\top\mathbf{x} = \sum_{k=1}^K a_k x_k$

so
$$\forall i, \left(\frac{\partial \mathbf{a}^\top\mathbf{x}}{\partial \mathbf{x}}\right)_i = \frac{\partial \mathbf{a}^\top\mathbf{x}}{\partial x_i} = \frac{\partial \sum_{k=1}^K a_k x_k}{\partial x_i} = \sum_{k=1}^K \frac{\partial a_k x_k}{\partial x_i}$$

$$\frac{\partial a_k x_k}{\partial x_i} =
\begin{cases}
a_k \text{ if } k=i \\
0 \text{ if } k \neq i
\end{cases}$$

so $\sum_{k=1}^K \frac{\partial a_k x_k}{\partial x_i} = a_i$ (all the elements in the sum are 0 except when $i=k$, where it is equal to $a_k = a_i$ since $i=k$)

$\forall i \left( \frac{\partial \mathbf{a}^\top\mathbf{x}}{\partial \mathbf{x}}\right)_i =  \frac{\partial \mathbf{a}^\top\mathbf{x}}{\partial x_i} = a_i$,
so $\frac{\partial \mathbf{a}^\top\mathbf{x}}{\partial \mathbf{x}} = \mathbf{a}$

And *voilà*!

</details>

Since $\mathbf{a}^\top\mathbf{x} = \mathbf{x}^\top\mathbf{a}$, this means that we also have $\frac{\partial \mathbf{x}^\top\mathbf{a}}{\partial \mathbf{x}} = \mathbf{a}$.

#### Exercise 1 — derivative of a matrix-vector product

Your turn! Using the same method, prove that for matrix $\mathbf{A} \in \mathbb{R}^{N \times K}$ and vector $\mathbf{x} \in \mathbb{R}^K$

$$
\frac{\partial \mathbf{Ax}}{\partial \mathbf{x}} = \mathbf{A}
$$

<details markdown="1">
<summary>Solution</summary>

First, a quick check on the dimensions: $\mathbf{Ax} \in \mathbb{R}^{N}$, $\mathbf{x} \in \mathbb{R}^{K}$, so we should have $\frac{\partial \mathbf{Ax}}{\partial \mathbf{x}} \in \mathbb{R}^{N \times K}$. Indeed, $\mathbf{A} \in \mathbb{R}^{N \times K}$. All good! ✅ In this example, we are considering *the derivative of a vector with respect to a vector*.

$$(\mathbf{Ax})_i = \sum_{k=1}^K a_{i,k} x_k$$

So $$\frac{\partial (\mathbf{Ax})_i}{\partial x_j} = \frac{\partial}{\partial x_j} \left(\sum_{k=1}^K a_{i,k} x_k \right)= \sum_{k=1}^K a_{i,k} \frac{\partial x_k}{\partial x_j} = a_{i,j}$$

since $\frac{\partial x_k}{\partial x_j} = 0$ everywhere except where $k=j$ in which case $\frac{\partial x_j}{\partial x_j} = 1$

$$\forall i,j, \left(\frac{\partial \mathbf{Ax}}{\partial \mathbf{x}}\right)_{i,j} = \frac{\partial (\mathbf{Ax})_i}{\partial x_j} = a_{i,j}$$

So $\frac{\partial \mathbf{Ax}}{\partial \mathbf{x}} = \mathbf{A}$ *Q.E.D.*



</details>

#### Exercise 2 — another derivative of a matrix-vector product?

Is it true that

$$
\frac{\partial \mathbf{Ax}}{\partial \mathbf{A}} = \mathbf{x}?
$$

<details markdown="1">
<summary>Solution</summary>

Absolutely not.

This equation does not even seem to make sense:  assuming as in the previous exercise that $\mathbf{A} \in \mathbb{R}^{N \times K}$ and $\mathbf{x} \in \mathbb{R}^K$, then $\mathbf{Ax} \in \mathbb{R}^{N}$. So $\frac{\partial \mathbf{Ax}}{\partial \mathbf{A}}$ should be a rank-3 tensor in $\mathbb{R}^{N \times N \times K}$, with
$$\left(\frac{\partial \mathbf{Ax}}{\partial \mathbf{A}}\right)_{i,j,k} = \frac{\partial (\mathbf{Ax})_{i}}{\partial a_{j,k}}$$. Here, $\mathbf{x} \in \mathbb{R}^K$ is a vector, so the two cannot be equal.

</details>

#### Exercise 3 — derivative of a matrix product

<a id="exercise-matrix-product"></a>

Let's consider two matrices $\mathbf{A}(x) \in \mathbb{R}^{P \times Q}$ and $\mathbf{B}(x) \in \mathbb{R}^{Q \times R}$ whose coordinates depend on a scalar-valued variable $x \in \mathbb{R}$. To simplify notations, we will simply write $\mathbf{A}$ and $\mathbf{B}$, making their dependency on variable $x$ implicit.

Show that

$$
\frac{\partial \mathbf{AB}}{\partial x} = \frac{\partial \mathbf{A}}{\partial x}\mathbf{B} + \mathbf{A}\frac{\partial \mathbf{B}}{\partial x}\mathbf{}
$$

<details markdown="1">
<summary>Solution</summary>

In this example, we are considering *the derivative of a matrix with respect to a scalar*.
I will let you check that the dimensions make sense.

Element with index $i,j$ of matrix product $\mathbf{AB}$ is given by
$$(\mathbf{AB})_{i,j} = \sum_{k} a_{i,k} b_{k,j}$$

So element $i,j$ of derivative $\frac{\partial \mathbf{AB}}{\partial x}$ is

$$
\begin{align*}
\left(\frac{\partial \mathbf{AB}}{\partial x}\right)_{i,j}
& = \frac{\partial (\mathbf{AB})_{i,j}}{\partial x} \\
&= \frac{\partial}{\partial x} \left(\sum_{k} a_{i,k} b_{k,j}\right) \\
&= \sum_{k} \frac{\partial}{\partial x}(a_{i,k} b_{k,j}) \\
\end{align*}
$$

Here, remember that $\mathbf{A}(x)$ explicitly or implicitly depends on $x$, thus so does element $a_{i,k}(x)$. Same for $b_{k,j}(x)$. So

$$
\frac{\partial}{\partial x}(a_{i,k} b_{k,j}) = \frac{\partial a_{i,k}}{\partial x}b_{k,j} + a_{i,k}\frac{\partial b_{k,j}}{\partial x}
$$
([product rule](https://en.wikipedia.org/wiki/Product_rule) of calculus)

And

$$
\begin{align*}
\sum_{k} \frac{\partial}{\partial x}(a_{i,k} b_{k,j})
& = \sum_{k} \left( \frac{\partial a_{i,k}}{\partial x}b_{k,j} + a_{i,k}\frac{\partial b_{k,j}}{\partial x} \right)\\
&= \sum_{k} \frac{\partial a_{i,k}}{\partial x}b_{k,j} + \sum_{k} a_{i,k}\frac{\partial b_{k,j}}{\partial x}
\end{align*}
$$

By definition, we have

$$\left(\frac{\partial \mathbf{A}}{\partial x}\right)_{i,j} = \frac{\partial a_{i,j}}{\partial x}$$

and

$$\left(\frac{\partial \mathbf{B}}{\partial x}\right)_{i,j} = \frac{\partial b_{i,j}}{\partial x}$$

So

$$
\begin{align*}
\left(\frac{\partial \mathbf{A}}{\partial x}\mathbf{B}\right)_{i,j} &= \sum_k \frac{\partial a_{i,k}}{\partial x} b_{k,j} \\
\left(\mathbf{A} \frac{\partial \mathbf{B}}{\partial x}\right)_{i,j} &= \sum_k a_{i,k} \frac{\partial b_{k,j}}{\partial x}
\end{align*}
$$

And finally

$$
\forall i,j, \quad
\left(\frac{\partial \mathbf{AB}}{\partial x}\right)_{i,j}
= \left(\frac{\partial \mathbf{A}}{\partial x}\mathbf{B}\right)_{i,j} + \left(\mathbf{A} \frac{\partial \mathbf{B}}{\partial x}\right)_{i,j}
$$

*Q.E.D.*

</details>

#### Exercise 4 — a final useful result <sub><sup>(for now)</sup></sub>

Let's consider two vectors $\mathbf{a}(\mathbf{x}) \in \mathbb{R}^{N}$ and $\mathbf{b}(\mathbf{x}) \in \mathbb{R}^{N}$ whose coordinates depend on a vector $\mathbf{x} \in \mathbb{R}^K$. Show that

$$
\frac{\partial \mathbf{a}^\top\mathbf{b}}{\partial \mathbf{x}} = \left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)^\top \mathbf{b} + \left(\frac{\partial \mathbf{b}}{\partial \mathbf{x}}\right)^\top \mathbf{a}
$$

<details markdown="1">
<summary>Solution</summary>

OK, before we dive into the calculations, there's a lot to unravel here, starting with the dimensions of every object.

As a dot product between two vectors, $\mathbf{a}^\top\mathbf{b} \in \mathbb{R}$. So $\frac{\partial \mathbf{a}^\top\mathbf{b}}{\partial \mathbf{x}}$ is the gradient of a scalar w.r.t. a vector $\mathbf{x}$, so it should be a vector with the same dimension as $\mathbf{x}$, i.e. $\frac{\partial \mathbf{a}^\top\mathbf{b}}{\partial \mathbf{x}} \in \mathbb{R}^K$.

$\frac{\partial \mathbf{a}}{\partial \mathbf{x}}$ is the derivative of $\mathbf{a} \in \mathbb{R}^{N}$ w.r.t. $\mathbf{x} \in \mathbb{R}^{K}$, so it is a matrix of size $N \times K$. So as its transpose, $\left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)^\top \in \mathbb{R}^{K \times N}$. And finally, $\left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)^\top \mathbf{b} \in \mathbb{R}^{K}$ as a matrix-vector product.
Similarly, $\left(\frac{\partial \mathbf{b}}{\partial \mathbf{x}}\right)^\top \mathbf{a} \in \mathbb{R}^{K}$.

All is good, dimensions seem to check out! Notice that in this example, we are again considering *the gradient of a scalar with respect to a vector* as in result 1, only this time matrices appear in the solution. But since they are multiplied with vectors, the final result is indeed a vector.
All right, onto the calculations then.

<!-- To slightly simplify notations, we will write $\mathbf{A} = \frac{\partial \mathbf{a}}{\partial \mathbf{x}} \in \mathbb{R}^{N \times K}$ the matrix whose coordinates are given by
$A_{n,k} = \frac{\partial a_n}{\partial x_k}$. Similarly, $\mathbf{B} = \frac{\partial \mathbf{b}}{\partial \mathbf{x}} \in \mathbb{R}^{N \times K}$. -->

$\mathbf{a}^\top\mathbf{b} = \sum_{n=1}^N a_n b_n$ so

$$
\begin{align*}
\left(\frac{\partial \mathbf{a}^\top\mathbf{b}}{\partial \mathbf{x}}\right)_k
&= \frac{\partial \mathbf{a}^\top\mathbf{b}}{\partial x_k}
= \frac{\partial}{\partial x_k} \left( \sum_{n=1}^N a_n b_n\right) \\
& = \sum_{n=1}^N \frac{\partial a_n b_n}{\partial x_k} \\
&= \sum_{n=1}^N \left( \frac{\partial a_n}{\partial x_k} b_n + a_n \frac{\partial b_n}{\partial x_k} \right) \\
&= \sum_{n=1}^N \left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)_{n,k} b_n
+ \sum_{n=1}^N a_n \left(\frac{\partial \mathbf{b}}{\partial \mathbf{x}}\right)_{n,k} \\
&= \sum_{n=1}^N \left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)^\top_{k,n} b_n
+ \sum_{n=1}^N a_n \left(\frac{\partial \mathbf{b}}{\partial \mathbf{x}}\right)^\top_{k,n} \\
&= \left(\left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)^\top \mathbf{b}\right)_k + \left(\left(\frac{\partial \mathbf{b}}{\partial \mathbf{x}}\right)^\top \mathbf{a}\right)_k
\end{align*}
$$

*Q.E.D.*

</details>

*Is that all? I want more!*

Wow, I really appreciate your enthusiasm! I'll just move on to the next section for now as time is running out, but I added [a couple of exercises][additional-exercises] at the end in case you want to continue practicing.

## *Le plat de résistance*


OK, now that we're super familiar with matrix calculus, it's time for me to keep my promises, and show that finding a closed-form solution for least squares linear regression is really not that difficult — in fact, with enough practice, you should be able to do this is your sleep*.

*(\*True story: I did dream I was teaching this once, and only slightly struggled to derive this on the blackboard in my sleep. Yes, I've already been told I'm weird, no need to repeat it again.)*

<img class="center-image" src="{{ '/assets/img/matrix-calculus/spaghetti.jpg' | relative_url }}" alt="Yummy equations" width="300"/>
<div class="figure-legend">
Once you're done reading this article, you'll be eating matrix derivatives for breakfast.
</div>

### Problem formulation

A brief reminder of the context first: we have a training dataset of $N$ labeled samples. Each sample $$\mathbf{x}_n$$ consists of $K$ features i.e. $K$ dimensions, such that $$\mathbf{x}_n = (x_{n,1}, \dots, x_{n,K})^\top \in \mathbb{R}^{K}$$, and comes with a label $y_n \in \mathbb{R}$.
We are trying to approximate $y_n$ with a linear model consisting of weights $\mathbf{w} = (w_1, \dots, w_K)^\top \in \mathbb{R}^K$, such that

$$
\hat{y}_n = w_1 x_{n,1} + \dots + w_K x_{n,K}  = \mathbf{w}^\top\mathbf{x}_n \approx y_n
$$

All our training samples are stacked in a matrix of features $\mathbf{X} = (\mathbf{x}_1, \dots, \mathbf{x}_N)^\top \in \mathbb{R}^{N \times K}$ and a vector of labels $\mathbf{y} = (y_1, \dots, y_N)^\top \in \mathbb{R}^{N}$.
We are trying to find the weights $\mathbf{w}$ that minimize the following training loss:

$$
\mathcal{L}(\mathbf{w}) = \sum_{n=1}^N \left(\left(\sum_{k=1}^K w_k x_{n,k}\right) - y_n\right)^2 = ||\mathbf{Xw} - \mathbf{y}||_2^2
$$

*(If the reason why the two sides of the equation above are equal is not clear, now would be a great time to read [this article][matrix-notation]. Actually, any time would be a great time to read this article).*

### Solving least squares linear regression

The key idea here is:

<div class="goldhighlight" markdown="1">
If a scalar-valued function $\mathcal{L}(\mathbf{w}) \in \mathbb{R}$ of a vector $\mathbf{w} \in \mathbb{R}^K$ admits a local extremum $\mathbf{w}^*$ (either a minimum or a maximum), then its gradient $\frac{\partial \mathcal{L}}{\partial \mathbf{w}} \in \mathbb{R}^K$ is going to be $\boldsymbol{0}$ at this point:

$$
\frac{\partial \mathcal{L}}{\partial \mathbf{w}}(\mathbf{w}^*) = \boldsymbol{0}
$$

</div>

This is a direct generalization of the fact that at a local extremum of real-valued function $f: \mathbb{R} \rightarrow \mathbb{R}$ of a real variable $x \in \mathbb{R}$, its derivative $\frac{\partial f(x)}{\partial x}$ is 0. If we are looking for the maximum of a real-valued function, we can compute its derivative, and check points where the derivative is 0. Similarly, for a scalar-valued function $\mathcal{L}$ taking a vector $\mathbf{w}$ as input, we can check points where the gradient is $\boldsymbol{0}$.

OK sure, but how can we do that?

*JFC\**, have you been paying attention *at all*? Finding analytical formulas for gradients is all we've been doing for the past 30 minutes or so!

*(\*This of course stands for Jamaican Fried Chicken, we don't curse on this blog.)*

Anyway, let's try to see if we can express $\frac{\partial \mathcal{L}}{\partial \mathbf{w}}$ in terms of $\mathbf{X}$, $\mathbf{y}$ and $\mathbf{w}$. You may give it a try first if you want.

<details markdown="1">
<summary>Show me how it's done</summary>

<a id="least-squares-gradient-derivation"></a>

First, a useful thing to notice:
$$||\mathbf{Xw} - \mathbf{y}||_2^2 = (\mathbf{Xw} - \mathbf{y})^\top(\mathbf{Xw} - \mathbf{y})$$

From exercise 3, we have:

$$
\frac{\partial \mathbf{a}^\top\mathbf{b}}{\partial \mathbf{x}} = \left(\frac{\partial \mathbf{a}}{\partial \mathbf{x}}\right)^\top \mathbf{b} + \left(\frac{\partial \mathbf{b}}{\partial \mathbf{x}}\right)^\top \mathbf{a}
$$

Applied to our problem, this yields:

$$
\begin{align*}
\frac{\partial}{\partial \mathbf{w}} \left( (\mathbf{Xw} - \mathbf{y})^\top(\mathbf{Xw} - \mathbf{y}) \right)
&= \left(\frac{\partial (\mathbf{Xw} - \mathbf{y})}{\partial \mathbf{w}}\right)^\top (\mathbf{Xw} - \mathbf{y})
+ \left(\frac{\partial (\mathbf{Xw} - \mathbf{y})}{\partial \mathbf{w}}\right)^\top (\mathbf{Xw} - \mathbf{y}) \\
&= 2 \left(\frac{\partial (\mathbf{Xw} - \mathbf{y})}{\partial \mathbf{w}}\right)^\top (\mathbf{Xw} - \mathbf{y})
\end{align*}
$$

We have

$$
\frac{\partial (\mathbf{Xw} - \mathbf{y})}{\partial \mathbf{w}} = \frac{\partial (\mathbf{Xw})}{\partial \mathbf{w}} - \frac{\partial \mathbf{y}}{\partial \mathbf{w}}
$$

From exercise 1, $\frac{\partial (\mathbf{Xw})}{\partial \mathbf{w}} = \mathbf{X}$. $\mathbf{y}$ does not depend on $\mathbf{w}$ so $\frac{\partial \mathbf{y}}{\partial \mathbf{w}} = \boldsymbol{0}$, and thus 

$$
\frac{\partial (\mathbf{Xw} - \mathbf{y})}{\partial \mathbf{w}} = \mathbf{X}
$$

And finally:
</details>

We get the result

$$
\frac{\partial ||\mathbf{Xw} - \mathbf{y}||_2^2}{\partial \mathbf{w}} = 2\mathbf{X}^\top (\mathbf{Xw} - \mathbf{y})
$$



<details markdown="1">
<summary>Alternative (direct) proof</summary>

In case you skipped the exercises above: well, first: boooh! You should do the exercises, it's very good practice. It is however possible to directly prove the result above directly from the definition, without using any of the intermediate results we derived in the previous section, by using sum and index notation — as opposed to [matrix notation][matrix-notation].

However, as you're about to see, this gets pretty cumbersome pretty quickly, so I'd *strongly* encourage you to make use of matrix notations and  intermediate results whenever possible.

$$
||\mathbf{Xw} - \mathbf{y}||_2^2 = \sum_{n=1}^N \left(\left(\sum_{k=1}^K w_k x_{n,k} \right) - y_n\right)^2
$$

so for index $i$:

$$
\begin{align*}
\frac{\partial ||\mathbf{Xw} - \mathbf{y}||_2^2}{\partial w_i}
&= \frac{\partial}{\partial w_i} \left( \sum_{n=1}^N (\sum_{k=1}^K w_k x_{n,k} - y_n)^2 \right) \\
&= \sum_{n=1}^N \frac{\partial}{\partial w_i} \left(\left(\sum_{k=1}^K w_k x_{n,k} \right)^2 - 2 y_n \sum_{k=1}^K w_k x_{n,k} + y_n^2 \right) \\
&= \sum_{n=1}^N\left( \frac{\partial}{\partial w_i}\left(\sum_{k=1}^K w_k x_{n,k}\right)^2 - 2 y_n \sum_{k=1}^K x_{n,k}\frac{\partial w_k}{\partial w_i} + \frac{\partial y_n^2}{\partial w_i}\right) \\
\end{align*}
$$

$y_n^2$ does not depend on $\mathbf{w}$ or $w_i$ so $\frac{\partial y_n^2}{\partial w_i} = 0$

$\frac{\partial w_k}{\partial w_i} = 0$ everywhere except where $k=i$ in which case $\frac{\partial w_k}{\partial w_i} = 1$ so
$2 y_n \sum_{k=1}^K x_{n,k}\frac{\partial w_k}{\partial w_i} = 2 y_n x_{n,i}$

Based on the [chain rule of calculus](https://en.wikipedia.org/wiki/Chain_rule),
$\frac{\partial f(w)^2}{\partial w} = 2f(w)\frac{\partial f(w)}{\partial w}$, so

$$
\frac{\partial}{\partial w_i}\left(\sum_{k=1}^K w_k x_{n,k}\right)^2
= 2 \sum_{k=1}^K w_k x_{n,k}\frac{\partial}{\partial w_i}\left(\sum_{k=1}^K w_k x_{n,k}\right)
= 2 \sum_{k=1}^K w_k x_{n,k} x_{n,i}
$$

So

$$
\begin{align*}
\frac{\partial ||\mathbf{Xw} - \mathbf{y}||_2^2}{\partial w_i}
&= \sum_{n=1}^N\left( 2 \sum_{k=1}^K w_k x_{n,k} x_{n,i} - 2 y_n x_{n,i} + 0\right) \\
&= 2 \sum_{n=1}^N x_{n,i} (\sum_{k=1}^K w_k x_{n,k} - 2 y_n) \\
&= 2 \sum_{n=1}^N x_{i,n}^\top (\mathbf{Xw} - \mathbf{y})_n \\
\frac{\partial ||\mathbf{Xw} - \mathbf{y}||_2^2}{\partial w_i}
&= (2 \mathbf{X}^\top(\mathbf{Xw} - \mathbf{y}))_i \quad \forall i \quad \text{Q.E.D.}
\end{align*}
$$

(where e.g. $(\mathbf{Xw} - \mathbf{y})_n$ is element $n$ of vector $(\mathbf{Xw} - \mathbf{y})$)

</details>


This result is already really useful in and of itself: this gives us a direct estimate of the gradient of the loss function $\mathcal{L}(\mathbf{w})$ with respect to the model parameters $\mathbf{w}$. In case we want to estimate $\mathbf{w}$ with gradient descent for example:

$$
\mathbf{w}^{(t+1)} = \mathbf{w}^{(t)} - \alpha \frac{\partial \mathcal{L}(\mathbf{w}^{(t)})}{\partial \mathbf{w}^{(t)}}
$$

we can directly compute the gradient
$\frac{\partial \mathcal{L}(\mathbf{w}^{(t)})}{\partial \mathbf{w}^{(t)}} = 2\mathbf{X}^\top (\mathbf{Xw}^{(t)} - \mathbf{y})$,
and plug its value into our parameter update formula above.

But we can do even better: we said that if $$\mathbf{w}^*$$ is a minimum of $\mathcal{L}$, then $\frac{\partial \mathcal{L}}{\partial \mathbf{w}}(\mathbf{w}^*) = \boldsymbol{0}$. Which means, if we can identify such points where $\frac{\partial \mathcal{L}(\mathbf{w})}{\partial \mathbf{w}} = \boldsymbol{0}$, the global minimum of $\mathcal{L}$, corresponding to the best possible parameters for the model, is going to be among them!

$$
\begin{align*}
\frac{\partial \mathcal{L}(\mathbf{w})}{\partial \mathbf{w}} = \boldsymbol{0}
&\iff 2\mathbf{X}^\top (\mathbf{Xw} - \mathbf{y}) = \boldsymbol{0} \\
\end{align*}
$$

*(You can try to go from this to the result below if you want.)*

<details markdown="1">
<summary>Show me how it's done</summary>

$$
\begin{align*}
&\iff \mathbf{X}^\top\mathbf{X}\mathbf{w} = \mathbf{X}^\top\mathbf{y}
\end{align*}
$$

*(we distribute $2\mathbf{X}^\top$ on $\mathbf{X}\mathbf{w}$ and $-\mathbf{y}$, move $-2\mathbf{X}^\top\mathbf{y}$ on the right side and divide both sides by 2)*

Left-multiplying both sides by $(\mathbf{X}^\top\mathbf{X})^{-1}$:

$$
\begin{align*}
\mathbf{X}^\top\mathbf{X}\mathbf{w} = \mathbf{X}^\top\mathbf{y}
&\iff \cancel{(\mathbf{X}^\top\mathbf{X})^{-1}}\cancel{(\mathbf{X}^\top\mathbf{X})}\mathbf{w} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y} \\
\end{align*}
$$

</details>

$$
\begin{align*}
&\iff \boxed{\mathbf{w} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}}
\end{align*}
$$

And *there*, we finally have it! This is where the analytical solution to least square linear regression comes from!

<details markdown="1">
<summary><em>"Wow wow, not so fast, cowboy!"</em> — a math purist (probably)</summary>

<a id="not-so-fast"></a>

***Preamble:*** *If you're reading this article for the first time, this more technical passage may be skipped.*

Before claiming victory, there are a few additional checks that we should have done: so far, we just proved that *if* there is a global extremum, then it occurs at the point $\mathbf{w} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}$.

So a first question could be: does this point actually exist? I.e., is it true that $\mathbf{X}^\top\mathbf{X}$ is invertible? It turns out that yes, as long as $N \geq K$ and the columns of $\mathbf{X}$ are linearly independent, i.e. $\text{rank}(\mathbf{X}) = K$. This is one reason why you may have heard that having collinear features is bad in linear regression: these make the rank of $\mathbf{X}$ $\text{rank}(\mathbf{X}) < K$, meaning that $(\mathbf{X}^\top\mathbf{X})^{-1}$ is no longer invertible and the solution may not be unique. To be fair, this is usually not a huge problem, as numerical solvers typically used for this kind of problem will usually still find a solution, but this may cause issues regarding e.g. interpretability *(blog post coming soon)*.
<!--- You can actually check out [this other blog post]() for more information about this. -->

Second, is this extremum a minimum or a maximum? Is it a local one or a global one? One intuitive way to think about it is to see that $\mathcal{L}$ does seem to have a global minimum, as it makes sense that a set of parameters which minimizes our loss $\mathcal{L}$ exists. On the other hand, there is no "worst" set of parameters, because parameters can get arbitrarily bad: if $10^{100}$ is not a bad enough value for one of the coefficients of the linear regression, we can always use $10^{10^{100}}$, or $10^{10^{10^{100}}}$ and so on. So $\mathcal{L}$ does not seem to have a maximum.

To prove this in a more rigorous way, in 1 dimension, we could compute the second order derivative and prove that $\frac{\partial^2 \mathcal{L}(w)}{\partial w^2} > 0$.
More generally, in $K$ dimensions, we could compute the Hessian matrix $\mathbf{H}$ defined by
$H_{i,j} = \frac{\partial^2 \mathcal{L}(\mathbf{w})}{\partial w_i \partial w_j}$ and show that it is positive definite, i.e. $\forall \mathbf{x} \in \mathbb{R}^K, \mathbf{x} \neq \mathbf{0} \implies \mathbf{x}^\top \mathbf{H} \mathbf{x} > 0$. But this is outside of the scope of this article.

</details>

## Now what?

OK, we are done with the main result from this article. Are there any questions from the imaginary audience?

*"Was this article just about linear regression?"*

Well, no. You may have noticed that the definition we gave in part 1 were broader than only what we needed for *le plat de résistance*.
In addition and somehow interestingly, the problem:

$$
\underset{\mathbf{w}}{\text{minimize}} ~ ||\mathbf{Xw} - \mathbf{y}||_2^2
$$

is relevant to a set of situations much, *much* broader than what we typically call linear regression. The quantity $(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$ has even earned its own name, the *pseudo-inverse* of $\mathbf{X}$.

In fact, this problem has been so ubiquitous in my work recently that it warranted I write its very own, dedicated [series of articles][pseudo-inverse]. Other posts about its practical applications are also coming soon. (*Spoiler alert*: this involves 3D facial shape estimation from photos, and bone shape estimation from 3D surface skin mesh).

*"OK, so the article was mostly about the problem above then?"*

Also no. This problem was used as an example of how we can apply matrix calculus to derive an (arguably) interesting result, using least squares linear regression as an example. But, the set of tools we familiarized ourselves with along the way has a much, much broader possible set of applications.
In machine learning, this includes Principal Component Analysis ([exercise 8][exercise-pca]), Ridge Regression ([exercise 10][exercise-ridge]), Support Vector Machines, Expectation-Maximization for Mixtures of Gaussians, Backpropagation in Deep Learning...

*"But solutions to all these problems are already available on the Internet and have been implemented in many libraries, right?"*

Right. But mastering the basics is a prerequisite to identifying situations where the same ideas can be applied to obtain non-trivial results, which is kind of [the point of this blog][matrix-notation-point].

*"How can I do that?"*

Well, now that you have the basics in matrix calculus, it's time for you to fly with your own wings. Good news though: I've included some flight lessons in the form of [additional exercises][additional-exercises] below!




## Additional exercises

##### Exercise 5

For $\mathbf{x} \in \mathbb{R}^{N}$, show that

$$
\frac{\partial ||\mathbf{x}||_2^2}{\partial \mathbf{x}} = 2\mathbf{x}
$$


<details markdown="1">
<summary>Solution</summary>

Regarding the dimensions first: $||\mathbf{x}||_2^2$ is a scalar, so $\frac{\partial ||\mathbf{x}||_2^2}{\partial \mathbf{x}}$ should be a vector with the same dimension as $\mathbf{x}$. ✅
We are considering the gradient of a scalar with respect to a vector.

There are a couple of ways to tackle this problem. One is "brute-force calculations":

$$
\begin{align*}
\frac{\partial ||\mathbf{x}||_2^2}{\partial x_i}
&= \frac{\partial}{\partial x_i}\sum_{n=1}^N x_n^2 \\
&= \sum_{n=1}^N \frac{\partial x_n^2}{\partial x_i} \\
&= \sum_{n=1}^N \begin{cases}
\frac{\partial x_i^2}{\partial x_i} = 2x_i \quad \text{when } n=i\\
0 \quad \text{otherwise}
\end{cases} \\
&= 2x_i
\end{align*}
$$

Another one consists in noticing that $||\mathbf{x}||_2^2 = \mathbf{x}^\top\mathbf{x}$. We can then use the result from exercise 4:

$$
\begin{align*}
\frac{\partial \mathbf{x}^\top\mathbf{x}}{\partial \mathbf{x}}
&= \left(\frac{\partial \mathbf{x}}{\partial \mathbf{x}}\right)^\top \mathbf{x} + \left(\frac{\partial \mathbf{x}}{\partial \mathbf{x}}\right)^\top \mathbf{x} \\
&= 2 \mathbf{I}_N^\top \mathbf{x} \\
&= 2\mathbf{x}
\end{align*}
$$

</details>



##### Exercise 6

For $x \in \mathbb{R}$ and $\mathbf{A}(x) \in \mathbb{R}^{N \times N}$ a matrix whose coordinates depend on $x$ and which we assume to be invertible, show that

$$
\frac{\partial \mathbf{A}^{-1}}{\partial x} = -\mathbf{A}^{-1}\frac{\partial \mathbf{A}}{\partial x}\mathbf{A}^{-1}
$$

<details markdown="1">
<summary><em>Dis iz hard, plz gibe hint</em></summary>

Use the fact that $\mathbf{A}^{-1}\mathbf{A} = \mathbf{I}_N$ and result from [exercise 3][exercise-matrix-product].
</details>

<details markdown="1">
<summary>Solution</summary>

Dimensions check: $\mathbf{A} \in \mathbb{R}^{N \times N}$ so $\mathbf{A}^{-1} \in \mathbb{R}^{N \times N}$. $x \in \mathbb{R}$ so $\frac{\partial \mathbf{A^{-1}}}{\partial x} \in \mathbb{R}^{N \times N}$. Everything on the right side of the equation is a square $N \times N$ matrix, so the resulting product is also a $N \times N$ matrix. ✅

From exercise 3:

$$
\frac{\partial \mathbf{A}^{-1}\mathbf{A}}{\partial x} = \frac{\partial \mathbf{A}^{-1}}{\partial x}\mathbf{A} + \mathbf{A}^{-1}\frac{\partial \mathbf{A}}{\partial x}
$$

We also have

$$
\frac{\partial \mathbf{A}^{-1}\mathbf{A}}{\partial x}
= \frac{\partial \mathbf{I}_N}{\partial x} = \boldsymbol{0}
$$

So

$$
\frac{\partial \mathbf{A}^{-1}}{\partial x}\mathbf{A} = -\mathbf{A}^{-1}\frac{\partial \mathbf{A}}{\partial x}
$$

Right-multiply by $\mathbf{A}^{-1}$:

$$
\frac{\partial \mathbf{A}^{-1}}{\partial x}\cancel{\mathbf{A}\mathbf{A}^{-1}}
=-\mathbf{A}^{-1}\frac{\partial \mathbf{A}}{\partial x}\mathbf{A}
$$

*Q.E.D.*

</details>


##### Exercise 7

Let's consider $\mathbf{x} \in \mathbb{R}^{N}$ and $\mathbf{A} \in \mathbb{R}^{N \times N}$. This time, we consider that coordinates of $\mathbf{A}$ do not depend on coordinates of $\mathbf{x}$, i.e. $\mathbf{A} \neq \mathbf{A}(\mathbf{x})$. Show that

$$
\frac{\partial \mathbf{x}^\top\mathbf{Ax}}{\partial \mathbf{x}} = (\mathbf{A} + \mathbf{A}^\top)\mathbf{x}
$$

This is an exercise I give to my students in a graded homework, and I (obviously) also encourage said students to read this blog, so unfortunately I'm not going to provide a solution for this one. It's really not that complicated though. You can do it!

##### Exercise 8

In Principal Component Analysis, given $N$ unlabeled training samples
$$\mathbf{X} = (\mathbf{x}_1, \dots, \mathbf{x}_N)^\top \in \mathbb{R}^{N \times K}$$, we want to find a unit-norm vector $\mathbf{w} \in \mathbb{R}^K$ such that variance is maximized when points are projected onto this direction. Introducing a Lagrange multiplier $\lambda$ to take the constraint $||\mathbf{w}||_2 = 1$ into account, we get the following optimization problem:

$$
\underset{\mathbf{w}}{\text{maximize }} \mathcal{L}(\mathbf{w}) = ||\mathbf{Xw}||_2^2 + \lambda(1-||\mathbf{w}||_2^2)
$$

Prove that if a vector $\mathbf{w}$ is the solution to this problem, $\mathbf{w}$ must be an eigenvector of the covariance matrix $\mathbf{X}^\top\mathbf{X} \in \mathbb{R}^{K \times K}$.

<details markdown="1">
<summary>Solution</summary>

If we are at the maximum of the cost function $\mathcal{L}(\mathbf{w})$ with respect to $\mathbf{w}$, then
$\frac{\partial \mathcal{L}}{\partial \mathbf{w}} = \boldsymbol{0}$.

$$
\begin{align*}
\frac{\partial \mathcal{L}(\mathbf{w})}{\partial \mathbf{w}}
&= \frac{\partial ||\mathbf{Xw}||_2^2}{\partial \mathbf{w}}
+ \frac{\partial \lambda}{\partial \mathbf{w}}
- \lambda\frac{\partial ||\mathbf{w}||_2^2}{\partial \mathbf{w}}
\end{align*}
$$

From the part on linear regression,
$\frac{\partial ||\mathbf{Xw}||_2^2}{\partial \mathbf{w}} = 2\mathbf{X}^\top\mathbf{Xw}$.

From exercise 4,
$\frac{\partial ||\mathbf{w}||_2^2}{\partial \mathbf{w}} = 2\mathbf{w}$.

$\lambda$ does not depend on $\mathbf{w}$ so
$\frac{\partial \lambda}{\partial \mathbf{w}} = \boldsymbol{0}$.

Thus:

$$
\begin{align*}
\frac{\partial \mathcal{L}(\mathbf{w})}{\partial \mathbf{w}} = \boldsymbol{0}
&\iff 2\mathbf{X}^\top\mathbf{Xw} - 2\lambda \mathbf{w} = \boldsymbol{0} \\
&\iff (\mathbf{X}^\top\mathbf{X})\mathbf{w} = \lambda \mathbf{w}
\end{align*}
$$

i.e. $\mathbf{w}$ is an eigenvalue of the covariance matrix $\mathbf{X}^\top\mathbf{X}$.


</details>

##### Exercise 9

For matrices $\mathbf{A} \in \mathbb{R}^{M \times N}$, $\mathbf{X} \in \mathbb{R}^{N \times O}$ and $\mathbf{B} \in \mathbb{R}^{O \times P}$, express in terms of $\mathbf{A}$, $\mathbf{X}$ and $\mathbf{B}$:

$$
\frac{\partial ||\mathbf{AXB}||_F^2}{\partial \mathbf{X}}
$$

where
$$||\cdot||_F$$ is the [Frobenius norm](https://en.wikipedia.org/wiki/Matrix_norm#Frobenius_norm) defined as
$$||\mathbf{Z}||_F = \sqrt{\sum_i \sum_j Z_{i,j}^2}$$.

***Disclaimer:*** *this exercise is not particularly hard but may take a while.*

<details markdown="1">
<summary>Solution</summary>

$$
\begin{align*}
(\mathbf{AXB})_{m,p} &= (\mathbf{A(XB)})_{m,p} \\
&= \sum_n a_{m,n}(\mathbf{XB})_{n,p} \\
&= \sum_n a_{m,n} \sum_o x_{n,o} b_{o,p} \\
&= \sum_n \sum_o a_{m,n} x_{n,o} b_{o,p}
\end{align*}
$$

$$
\begin{align*}
||\mathbf{AXB}||_F^2 &= \sum_m \sum_p (\mathbf{AXB})_{m,p}^2 \\
&= \sum_m \sum_p (\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p})^2
\end{align*}
$$

$$
\begin{align*}
\frac{\partial ||\mathbf{AXB}||_F^2}{\partial x_{i,j}}
&= \frac{\partial}{\partial x_{i,j}} \sum_m \sum_p (\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p})^2 \\
&= \sum_m \sum_p \frac{\partial}{\partial x_{i,j}} (\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p})^2
\end{align*}
$$

From the [chain rule of calculus](https://en.wikipedia.org/wiki/Chain_rule),
$\frac{\partial f(x)^2}{\partial x} = 2f(x)\frac{\partial f(w)}{\partial x}$, so

$$
\begin{align*}
\frac{\partial}{\partial x_{i,j}} (\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p})^2
&= 2 (\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p})\frac{\partial}{\partial x_{i,j}} \left(\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p}\right) \\
&= 2 \sum_n \sum_o a_{m,n} x_{n,o} b_{o,p} \sum_n \sum_o a_{m,n} \frac{\partial x_{n,o}}{\partial x_{i,j}}  b_{o,p}
\end{align*}
$$

$\frac{\partial x_{n,o}}{\partial x_{i,j}} = 0$ everywhere except where $(n,o)=(i,j)$ in which case $\frac{\partial x_{n,o}}{\partial x_{i,j}} = 1$ so

$$
\begin{align*}
\frac{\partial}{\partial x_{i,j}} (\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p})^2
&= 2 \sum_n \sum_o a_{m,n} x_{n,o} b_{o,p} a_{m,i} b_{j,p}
\end{align*}
$$

$$
\begin{align*}
\frac{\partial ||\mathbf{AXB}||_F^2}{\partial x_{i,j}}
&= 2 \sum_m \sum_p \left( \sum_n \sum_o a_{m,n} x_{n,o} b_{o,p} a_{m,i} b_{j,p} \right)\\
&= 2 \sum_m a_{m,i} \sum_p \left(\sum_n \sum_o a_{m,n} x_{n,o} b_{o,p} \right) b_{j,p} \\
&= 2 \sum_m a_{m,i} \sum_p (\mathbf{AXB})_{m,p} b_{p,j}^\top \\
&= 2 \sum_m a_{i,m}^\top \left((\mathbf{AXB})\mathbf{B}^\top\right)_{m,j} \\
&= 2 \left( \mathbf{A}^\top(\mathbf{AXB})\mathbf{B}^\top \right)_{i,j} \quad \forall i,j
\end{align*} 
$$

Thus

$$
\begin{align*}
\frac{\partial ||\mathbf{AXB}||_F^2}{\partial \mathbf{X}} = 2\mathbf{A}^\top(\mathbf{AXB})\mathbf{B}^\top
\end{align*} 
$$

Notice that exercise 4 is a special case of this more generic result, where $\mathbf{X}$ is a vector with $N$ dimensions or equivalently a matrix in $\mathbb{R}^{N \times 1}$, and both $\mathbf{A}$ and $\mathbf{B}$ are the identity matrix $\mathbf{I}_N$.

If you want to prove an even more generic result, you may want to show that

$$
\frac{\partial ||\mathbf{AXB+C}||_F^2}{\partial \mathbf{X}}
= 2\mathbf{A}^\top(\mathbf{AXB+C})\mathbf{B}^\top
$$

One possible solution can be viewed section *1.2.2 Ridge regression*, page 47 of my [PhD dissertation](https://theses.hal.science/tel-03153445), along with a few examples of applications of this type of results. Be warned though, my thesis was written in 2020, so in pre-historic times in terms of AI. Since the field has been advancing mind-bogglingly, superluminally quickly in the last few years, the models presented in that section are pretty dated and of no practical use nowadays as far as I know.

*(The mathematical tools themselves are still relevant though).*
</details>

##### Exercise 10

Given features $\mathbf{X} \in \mathbb{R}^{N \times K}$, labels $\mathbf{y} \in \mathbb{R}^{N}$ and regularization hyper-parameter $\lambda \in \mathbb{R}^{+*}$, find the weights $\mathbf{w} \in \mathbb{R}^{K}$ which minimize the ridge regression loss:

$$
\underset{\mathbf{w}}{\text{minimize }} \mathcal{L}(\mathbf{w}) = ||\mathbf{Xw} - \mathbf{y}||_2^2 + \lambda ||\mathbf{w}||_2^2
$$

<details markdown="1">
<summary>Solution</summary>

We have already established in section *Le plat de résistance* that

$$
\frac{\partial ||\mathbf{Xw} - \mathbf{y}||_2^2}{\partial \mathbf{w}} = 2\mathbf{X}^\top (\mathbf{Xw} - \mathbf{y})
$$

and in exercise 5 that

$$
\frac{\partial ||\mathbf{w}||_2^2}{\partial \mathbf{w}} = 2\mathbf{w}
$$

So

$$
\begin{align*}
\frac{\partial \mathcal{L}(\mathbf{w})}{\partial \mathbf{w}} = \boldsymbol{0}
&\iff 2\mathbf{X}^\top (\mathbf{Xw} - \mathbf{y}) + 2\mathbf{w} = \boldsymbol{0} \\
&\iff 2\mathbf{X}^\top\mathbf{Xw} - 2\mathbf{X}^\top\mathbf{y} + 2\mathbf{I}_K\mathbf{w} = \boldsymbol{0} \\
&\iff 2(\mathbf{X}^\top\mathbf{X} + \mathbf{I}_K)\mathbf{w} = 2\mathbf{X}^\top\mathbf{y} \\
&\iff (\mathbf{X}^\top\mathbf{X} + \mathbf{I}_K)\mathbf{w} = \mathbf{X}^\top\mathbf{y} \\
&\iff \mathbf{w} = (\mathbf{X}^\top\mathbf{X} + \lambda\mathbf{I}_K)^{-1}\mathbf{X}^\top\mathbf{y}
\end{align*}
$$ 

with the same reasoning as previously regarding the fact that this does correspond to the global minimum of the cost function with respect to $\mathbf{w}$ and not e.g. a local maximum.

Couple of interesting notes:
$\mathbf{X}^\top\mathbf{X}$ is symmetric positive semi-definite, $\lambda\mathbf{I}_K$ is symmetric positive definite, so $(\mathbf{X}^\top\mathbf{X} + \lambda\mathbf{I}_K)$ is positive definite and as such always invertible.
</details>

<!--- Comment

When article on tensors is ready, insert links.
Same for part 2 of impossible systems of equations, regarding interpretability.
Also include links to other problems related to pseudo inverse.

-->


[matrix-notation]: {% link _posts/2025-07-21-matrix-notation.md %}
[matrix-notation-notation]: {% link _posts/2025-07-21-matrix-notation.md %}#quick-word-notation
[matrix-notation-point]: {% link _posts/2025-07-21-matrix-notation.md %}#the-point
[yannick]: {% link about.md %}#who-are-you-again
[pseudo-inverse]: {% link _posts/2025-07-24-pseudo-inverse.md %}

[additional-exercises]: {% link _posts/2025-07-22-matrix-calculus.md %}#additional-exercises
[exercise-pca]: {% link _posts/2025-07-22-matrix-calculus.md %}#exercise-8
[exercise-ridge]: {% link _posts/2025-07-22-matrix-calculus.md %}#exercise-10
[exercise-matrix-product]: {% link _posts/2025-07-22-matrix-calculus.md %}#exercise-matrix-product
