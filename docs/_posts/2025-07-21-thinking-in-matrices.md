---
layout: post
title:  "Thinking inside the Matrix"
rendered_title: "Thinking <del>outside</del> <em>inside</em> the Matrix"
date:   2025-07-21 11:22:40 +0200
update_date:  2025-07-24 11:22:40 +0200
categories: foundations
---

<img class="center-image" src="{{ '/assets/img/matrix-notations/matrix-illustration.jpg' | relative_url }}" alt="Matrix illustration" width="400"/>
<div class="figure-legend" markdown="1">
A Machine Learning Legend who can think inside the Matrix and knows when to avoid index notations.
</div>

One of the most underrated yet crucial skills to acquire in your machine learning journey is the ability to think and write in terms of matrices, vectors, or sometimes tensors.

*What do I even mean by that?*

Let's see a quick example. Below is a quantity expressed in what I call *index notations*, using sums over indices:

$$
\begin{equation}
\sum_{n=1}^N \left(y_n - \sum_{k=1}^K w_k x_{n,k}\right)^2
\end{equation}
$$

And here is the exact same quantity, but this time expressed using matrices and linear algebra operations, in what I call *matrix notations*:

$$
\begin{equation}
||\mathbf{Xw} - \mathbf{y}||_2^2
\end{equation}
$$

<sup><sub>(As you may have recognized, this corresponds to the least square linear regression loss — but this is not important for now).<sup><sub>

*Why should you care?*

Well first, if you're a student of mine who I practically forced reading this blog post in a somewhat blatant conflict of interest, just know that I mainly use matrix notations during class. So you better get used to it.
But, even if you're not one of my students:

<div class="silverhighlight" markdown="1">
Writing in matrix notations gives you two big advantages over writing in index notations: 
1. **Speed**. The implementation of the former may enable *huge* speedups in code execution when compared with the latter. And by huge, I mean hundred-plus fold speedups.

    Don't believe me? You should read [part 3][part-speed] of this article then, you may change your mind.

2. **Superpowers**. More precisely, the ability to use the unreasonable effectiveness of linear algebra. But asking the linear algebra overlords for help requires speaking their language, namely, that of matrices and matrix operations.
This shall be demonstrated in [part 2][part-gifts].

    <!--- Plus, as will be evidenced in part [part 2]({% link _posts/2025-07-21-thinking-in-matrices.md %}#other-gifts-from-the-linear-algebra-overlords), many if not most ML algorithms rely heavily on linear algebra, and can only be truly understood through this lense. -->
</div>

So, if you want to go beyond just calling *.fit* and *.predict* on your machine learning journey and become a true Machine Learning Legend, thinking in matrices is an essential step forward.

<details markdown="1">
<summary>Side note: machine learning, chess, and algebraic notations</summary>

One metaphore which I think nicely illustrates my point is chess notations.

For a beginner, it requires some effort to visualize the actual moves of the pieces on a chessboard from algebraic chess notations such as

*1. e4 e5 2. Nf3 Nc6 3. Bb5 a6...*

Most of us mere mortals find it much more intuitive to understand chess moves through actual board diagrams.

<div style="text-align: center;">
    <img src="{{ '/assets/img/matrix-notations/chess1.jpg' | relative_url }}" alt="Chess game 1" width="200"/> &nbsp;&nbsp;
    <img src="{{ '/assets/img/matrix-notations/chess2.jpg' | relative_url }}" alt="Chess game 2" width="200"/> &nbsp;&nbsp;
    <img src="{{ '/assets/img/matrix-notations/chess3.jpg' | relative_url }}" alt="Chess game 2" width="200"/>
</div>
<div class="figure-legend" markdown="1">
A not particularly interesting chess game.
</div>

However, getting used to going back and forth between the two representations enables keen players to tackle more advanced chess books, ones that don't spoon-feed you with board diagrams for every move.
Ultimately, this is  necessary to reach a certain level.

Similarly, writing quantities with sums and indices may be more intuitive to many people* at first, particularly people coming from a Computer Science background, who tends to think in terms of for loops. But being able to effortlessly translate index notations to matrix operations and vice versa is ultimately necessary to go beyond surface-level understanding of machine learning.

**Myself included. I personnaly only started actively developping this skill during my PhD, after a MSc in machine learning and a couple of years of professional experience as a data scientist. So whatever your current level of machine learning proficiency, there is not shame to have. It's always better to start now than never.*

</details>

The objective of this article is to let you take that initial step, and make you a seasoned machine learning walker who can effortlessly tread through the hills of more advanced linear algebra.
In particular, throughout other posts in this blog, I mostly assume you are well-versed in this exercise.

But I promise, with enough practice, it's really not that difficult. So let's get started!


## A first example: linear regression

### Basic "naive" formulation

To understand how all of this works, let's start with a very basic example: (multivariate) linear regression.

<sup><sub>*Note: my goal here is to use linear regression as an example, not explain how it works. [I assume readers are already somehow familiar][about] with basic machine learning concepts, including linear regression.*</sub></sup>

Let's say we have $K$ input variables $x_1, x_2, \dots, x_K$ — for instance, the square footage of an appartment $x_1$, its number of bedrooms $x_2$ and distance to city center $x_3$, in which case $K=3$. We want to estimate the price of this appartment.
Our estimation or *prediction* $\hat{y}$ will be a linear combination of the inputs:

$$
\begin{align*}
\hat{y} &= w_1 \cdot x_1 + w_2 \cdot x_2 + \dots + w_D \cdot x_D \\
&= \sum_{k=1}^K w_k x_k
\end{align*}
$$

where $w_1, \dots, w_D$ are the *parameters* or *weights* of the model.


In standard linear regression, the parameters are learned on a bunch of labeled training examples to minimize some training error. So let's say we have a total of $N$ different samples: for instance, we may have access to the data (square footage, bedrooms etc) of $N=100$ appartments, along with corresponding actual selling prices $y_1, y_2, \dots, y_N$.
For appartment number $n$, we consider features $x_{n,1}, \dots, x_{n,K}$ (such that $x_{n,k}$ is the $k^\text{th}$ feature of the $n^\text{th}$ appartment), and again make a prediction with

$$\hat{y}_n = \sum_{k=1}^K w_k x_{n,k}$$

In the usual least square formulation of linear regression, we want to find parameters $w_1, \dots, w_D$ which minimize the squares of the prediction errors on the training dataset.
For appartment number $n$, the squared difference between prediction $\hat{y}_n$ and the actual price $y_n$ is $$(\hat{y}_n - y_n)^2$$.
Thus,

<div class="silverhighlight" markdown="1">
The error or *loss* $\mathcal{L}$ for the whole training dataset is: 

$$
\begin{align*}
\mathcal{L} &= \sum_{n=1}^N (\hat{y}_n - y_n)^2 \\
&= \sum_{n=1}^N \left(\left(\sum_{k=1}^K w_k x_{n,k} \right) - y_n\right)^2
\end{align*}
$$

</div>

OK, looks easy enough.

So then, please remind me why would there by any issue with this notation?
Why should we prefer *matrix notations* such as

$$
||\mathbf{Xw} - \mathbf{y}||_2^2
$$

(which we will derive shortly in part 2) over the previous nice, easy to implement double sum with *index notations* from Equation (1)?

Well, as I said, two things: speed, and the ability to use linear algebra results. I promise, I will make these two advantages as explicit as I possibly can in very short order. But for now, let's rather focus on how we can transform Equation (1) into Equation (2), so that we can compare the two approaches.

### The Golden Rule of matrix thinking

Below is the central idea of matrix thinking, which I will refer to as the Golden Rule*.

**I don't think that's a real name, I just made it up for dramatic purposes. But it's a neat name to really drive my point accross.*

<div class="goldhighlight">
A sum of products $\sum_{k=1}^K a_k b_k$ iterated over the same index $k$ can be written as a dot product $<\cdot,\cdot>$ between two $K$-dimensional vectors $\mathbf{a}$ and $\mathbf{b}$:

$$\sum_{k=1}^K a_k b_k = <\mathbf{a}, \mathbf{b}> = \mathbf{a}^\top\mathbf{b} = \mathbf{b}^\top\mathbf{a}$$

with $\mathbf{a} = \begin{pmatrix} a_1 \\ \vdots \\ a_K \end{pmatrix} \in \mathbb{R}^K$
and $\mathbf{b} = \begin{pmatrix} b_1 \\ \vdots \\ b_K \end{pmatrix} \in \mathbb{R}^K$
</div>

Please note: the latter notation $\mathbf{a}^\top\mathbf{b}$ is the one I use most commonly to denote a dot product.

<details markdown="1">
<summary><em>Where does this notation come from?</em></summary>

The notation $\mathbf{a}^\top\mathbf{b}$ implicitly turns the *column* vector
$$\mathbf{a} = \begin{pmatrix} a_1 \\ a_2 \\ \vdots \\ a_K \end{pmatrix} \in \mathbb{R}^K$$
into a row vector
$\mathbf{a}^\top = \begin{pmatrix} a_1 ~ a_2 ~ \dots ~ a_K \end{pmatrix}$
with the transpose operation $(\cdot)^\top$.

Vector $\mathbf{a}$ can also be viewed as a matrix with $K$ rows and $1$ column, so
$\mathbf{a}^\top$ can be viewed as a matrix of size $1 \times K$.

$\mathbf{a}^\top$ is then matrix-multiplied with the column vector
$$\mathbf{b} = \begin{pmatrix} b_1 \\ b_2 \\ \vdots \\ b_K \end{pmatrix} \in \mathbb{R}^K$$, which is also a matrix of size $K \times 1$.
The matrix multiplication $\cdot$ of $\mathbf{a}^\top \in \mathbb{R}^{1 \times K}$ with $\mathbf{b} \in \mathbb{R}^{K \times 1}$ results in a matrix $\mathbf{a}^\top \cdot \mathbf{b}$ of size $1 \times 1$, implicitly cast as a scalar $\in \mathbb{R}$.

I typically use this type of notation a lot, as this is quite convenient.

</details>

Depending on your background, this so-called "Golden Rule" may seem painfully obvious. But, similarly to the [pigeonhole principle](https://en.wikipedia.org/wiki/Pigeonhole_principle), stupidly obvious statements can sometimes lead to interesting and far from obvious results.

### Applying the Golden Rule to linear regression

Let's see how we can apply the Golden Rule to get rid of the sums and indices in Equation (3) and transform it into Equation (4).

#### First sum over $k$

From our example from earlier: for appartment/sample number $n$, the predicted price/target is given by

$$
\hat{y}_n = \sum_{k=1}^K w_k x_{n,k}
$$

Using the Golden Rule™, this can be rewritten as 

$$
\hat{y}_n = \mathbf{w}^\top \mathbf{x}_n
$$

where $$\mathbf{w} = \begin{pmatrix} w_1 \\ \vdots \\ w_K \end{pmatrix} \in \mathbb{R}^K$$ represents the $K$ parameters of the linear model as a column vector, and
$$\mathbf{x}_n = \begin{pmatrix} x_{n,1} \\ \vdots \\ x_{n,K} \end{pmatrix}\in \mathbb{R}^K $$
corresponds to the $K$ input variables of the $n^\text{th}$ sample, also stacked in a vector.

We can go a step further: if we define a vector $\hat{\mathbf{y}} \in \mathbb{R}^N$ whose elements are 
$$\begin{pmatrix} \hat{y}_1 \\ \vdots \\ \hat{y}_N \end{pmatrix}$$, we have

$$
\hat{\mathbf{y}} = \begin{pmatrix} \mathbf{x}_1^\top\mathbf{w} \\ \vdots \\ \mathbf{x}_N^\top\mathbf{w} \end{pmatrix}
$$

Notice anything? A vector whose elements are given by different linear combinations $\mathbf{x}_1, \dots, \mathbf{x}_N$ of the same vector $\mathbf{w}$ is pretty much the definition of a matrix-vector multiplication.

Thus, we can "stack" all the $N$ sample vectors $\mathbf{x}_1, \dots, \mathbf{x}_N$ into a matrix with $N$ rows and $K$ columns:

$$\mathbf{X} = \begin{pmatrix}
x_{1,1} & x_{1,2} & \dots & x_{1,k} & \dots & x_{1,K} \\
x_{2,1} & x_{2,2} & \dots & x_{2,k} & \dots & x_{2,K} \\
\vdots & \vdots & & \vdots & & \vdots \\
x_{n,1} & x_{n,2} & \dots & x_{n,k} & \dots & x_{n,K} \\
\vdots & \vdots & & \vdots & & \vdots \\
x_{N,1} & x_{N,2} & \dots & x_{N,k} & \dots & x_{N,K}
\end{pmatrix}
= \begin{pmatrix} \mathbf{x}_1^\top \\ \vdots \\ \mathbf{x}_N^\top \end{pmatrix}
= \begin{pmatrix} \mathbf{x}_1 & \dots & \mathbf{x}_N \end{pmatrix}^\top
\in \mathbb{R}^{N \times K}$$

<details markdown="1">
<summary><em>A quick word on notations</em></summary>

In general throughout this blog, matrices are denoted by uppercase bold letters (e.g. $\mathbf{X}$), vectors by lowercase bold letters (e.g. $\mathbf{x}$), and scalars by non-bold letters (e.g. $k$, $N$ or $x_{n,k}$). This is a fairly common and quite useful convention, as this makes the nature of each variable/object much clearer in equations.

Using this convention, the matrix $$\mathbf{X} = \begin{pmatrix} x_{1,1} & \dots & x_{1,K} \\ \vdots & \ddots & \vdots \\ x_{N,1} & \dots & x_{N,K} \end{pmatrix} \in \mathbb{R}^{N \times K}$$ can also be more succintly expressed as $$\mathbf{X} = \begin{pmatrix} \mathbf{x}_1^\top \\ \vdots \\ \mathbf{x}_N^\top \end{pmatrix}$$ *(column vectors $\mathbf{x}_n \in \mathbb{R}^{K}$ are transposed as row vectors and then vertically stacked)* or as $\mathbf{X} = \begin{pmatrix} \mathbf{x}_1 ~\dots ~ \mathbf{x}_N \end{pmatrix}^\top$ *(column vectors $\mathbf{x}_n$ are horizontally aligned next to each other, and the resulting $K \times N$ matrix is transposed to obtain the desired $N \times K$ matrix).*

</details>

And finally, we can directly express $\hat{\mathbf{y}}$ as the matrix-vector multiplication of $\mathbf{X}$ and $\mathbf{w}$:

$$
\begin{equation}
\hat{\mathbf{y}} = \mathbf{Xw} \in \mathbb{R}^N
\end{equation}
$$

We can double check that $$\hat{y}_n = \sum_{k=1}^K x_{n,k} w_k$$ indeed corresponds to the formula for the $n^\text{th}$ row of a matrix-vector multiplication between a matrix $\mathbf{X}$, whose element at row $n$ and column $k$ is given by $x_{n,k}$, and the vector $\mathbf{w}$ whose $k^\text{th}$ element is $w_k$.


<details markdown="1">
<summary><em>Vectors as operators on matrices</em></summary>

In general, for expressions of the form $\mathbf{Ab}$, we tend to think of matrix $\mathbf{A}$ as a linear operator, which applies a different linear map (defined by $\mathbf{a}_k$ the $k^\text{th}$ row of $\mathbf{A}$) to every element $b_k$ of vector $\mathbf{b}$, such that element $k$ of vector $\mathbf{Ab}$ is given by
$$
(\mathbf{Ab})_k = \mathbf{a}_k^\top\mathbf{b} = \sum_i a_{k,i} b_i
$$

In our specific case here, we would be tempted to say that the *opposite* is happening: the coefficients $\mathbf{w}$ of the linear regression define a linear map that is applied to every sample $\mathbf{x}_n$ to obtain a prediction $\hat{y}_n = \mathbf{w}^\top \mathbf{x}_n$.
In my explanation earlier, I stated instead that $\mathbf{x}_n$ is a linear map that is applied to $\mathbf{w}$ to obtain row $\hat{y}_n$, which may sound a bit weird.

However, since $\mathbf{w}^\top \mathbf{x}_n = \mathbf{x}_n^\top\mathbf{w}$, the two formulations are equivalent in this situation, and the latter makes the matrix-vector multiplication relationship between $\hat{\mathbf{y}}$, $\mathbf{X}$ and $\mathbf{w}$ a bit more evident IMHO.

Thinking in terms of tensors with covariant and contravariant coordinates may be sometimes helpful to keep ideas clear about what is an operand and what is on operator.
A blog post on this topic should be coming soon.

[comment]: # (Update when blog post on tensors is available)
[comment]: # (For a fairly gentle introduction to tensors, you may check out my [blog post on this topic])

However, I would advise that you don't try this until you are already quite familiar with matrix notations.
A good test of readiness may be your ability to effortlessly solve the exercises included at the end of this article.

</details>

<div class="silverhighlight" markdown="1">
A piece of advice that will return frequently throughout this article: it is pretty much *always* a good idea to quickly check that the dimensions of our mathematical objects (matrices, vectors and others) are consistent.

As an example, in Equation (3), $\mathbf{X} \in \mathbb{R}^{N \times K}$ and $\mathbf{w} \in \mathbb{R}^{K}$, so $\mathbf{Xw} \in \mathbb{R}^{N}$. We were supposed to have $\hat{\mathbf{y}} \in \mathbb{R}^{N}$, so all is good. ✅
</div>

#### Second sum over $n$

OK, we got rid of one of the sums in Equation (3), the one over $k$. What about the second one, the one over $n$?

$$
\sum_{n=1}^N (\hat{y}_n - y_n)^2
$$

Is this a sum of products?

Well, yes: $(\hat{y}_n - y_n)^2 = (\hat{y}_n - y_n)(\hat{y}_n - y_n)$ *(duh!)*

So writing e.g. $\mathbf{z} = \hat{\mathbf{y}} - \mathbf{y}$ (i.e. $z_n = \hat{y}_n - y_n ~~ \forall n$), we can use the same idea as previously:

$$
\sum_{n=1}^N (\hat{y}_n - y_n)^2
= \sum_{n=1}^N z_n z_n
= \mathbf{z}^\top\mathbf{z}
= (\hat{\mathbf{y}}-\mathbf{y})^\top(\hat{\mathbf{y}}-\mathbf{y})
$$

In general, instead of
$$\mathbf{z}^\top\mathbf{z}$$,
we tend to write
$$||\mathbf{z}||_2^2$$,
but the idea is the same.

<details markdown="1">
<summary>🧮 Why are they equal?</summary>

By definition 
$$||\mathbf{z}||_2 = \sqrt{\sum_{k=1}^K z_k^2}$$

So
$$||\mathbf{z}||_2^2 = \sum_{k=1}^K z_k^2$$

</details>

Thus,

$$\sum_{n=1}^N (\hat{y}_n - y_n)^2 = ||\hat{\mathbf{y}} - \mathbf{y}||_2^2$$

And finally, since $\hat{\mathbf{y}} = \mathbf{Xw}$, we can write:

<div class="silverhighlight">
$$
\begin{align*}
\mathcal{L} &= \sum_{n=1}^N (\sum_{k=1}^K w_k x_{n,k} - y_n)^2 \\
&= ||\mathbf{Xw} - \mathbf{y}||_2^2
\end{align*}
$$
</div>

Again, depending on your background, what we just did may look either super obvious or needlessly complicated.
But again, doing this can be a *really* ***really*** powerful tool when used correctly in the right context, because this then enables us to leverage the 🌈*full power of linear algebra*🌟.

### Making use of our newly unlocked power

<img class="center-image" src="{{ '/assets/img/matrix-notations/fullpower.jpg' | relative_url }}" alt="The full power of linear algebra (poor Sylvester)" width="400"/>

<div class="figure-legend" markdown="1">
A poorly disguised Sylvester equation about to be anihilated by the full power of linear algebra ([exercise 9][part-exercise-9]).
</div>

What do I mean by this? Well, recall that in linear regression, we want to find weights $w_1, \dots, w_K$ that minimize our loss $\mathcal{L}$ (the sum of squared residues) on our training dataset. Directly minimizing our cost function written in index notations with respect to its parameters does not seem to be an easy problem, at least to me:

$$
\underset{w_1, \dots, w_K}{\text{minimize}}  \sum_{n=1}^N (y_n - \sum_{k=1}^K w_k x_{n,k})^2
$$

How about this exact same problem, but formulated with matrix notations?

$$
\underset{\mathbf{w}}{\text{minimize}} ~ ||\mathbf{Xw} - \mathbf{y}||_2^2
$$

Turns out, problems of the form
$$\underset{\mathbf{w}}{\text{minimize}} ~ ||\mathbf{Aw} - \mathbf{b}||_2^2$$
are [super standard problems][pseudo-inverse] with a well-known solution, in this case:

$$
\mathbf{w} = \mathbf{X}^\dagger\mathbf{y}
$$

where $\mathbf{X}^\dagger = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$ is called the *pseudo-inverse* of $\mathbf{X}$.

*(You may also read [this other post][matrix-calculus] for more details about where this formula comes from. However, the post assumes that you are already reasonably familiar with matrix notations, so I would advise you practice with the [exercises][part-exercises] below first).*

So this is one possible implementation of linear regression:
```python
def get_linear_regression_coefficients(samples: np.ndarray, labels: np.ndarray) -> np.ndarray:
    """
    Given training matrix of samples of shape (N,K) and vector of labels of shape (N,),
    return the coefficients of the least square linear regression model
    as an array of shape (K,).
    """
    return np.linalg.inv(samples.T @ samples) @ samples.T @ labels
```

Boom. We just solved linear regression in one line. No need for gradient descent or any of that, we can get the optimal parameters of our model in litterally one line of code.

## Other gifts from the linear algebra overlords

***Important preambule***: *This part provides additional examples of problems that seem hard when written in index notations, but become fairly easy when written in matrix notations. This section moves at a rather brisk pace: its purpose is more to show what you can do once you get familiar with matrix notations and [matrix calculus][matrix-calculus], rather than really explaining how to get there. So if you're reading this article for the first time, feel free to skip ahead to the next section for now. It is probably more relevant to do some practice exercises (graciously provided [at the end of the article][part-exercises]) first, before trying to read this section for the first time.*

<details markdown="1">
<summary style="font-size: 1.2em;">I'm not afraid, show me your full power!</summary>

OK, so, is writing in matrix notation mostly useful to solve one problem, namely least square linear regression?

Well, of course not. Did you really think I would make an entire post just to talk about linear regression? I mean, yeah, I absolutely *could have done that*, fair enough. But no, in this case I didn't.

Getting back to our main topic: writing in matrices really is a ubiquitous tool, especially when combined with other tools like [matrix calculus]().

### Principal Component Analysis

Let's quickly consider another example: Principal Component Analysis (a.k.a. PCA for family and friends). In PCA, given $N$ unlabeled training samples $(\mathbf{x}_1, \dots, \mathbf{x}_N)^\top$ in $K$ dimensions, we want to find a direction $\mathbf{w} \in \mathbb{R}^K$ (a unit-norm vector) along which variance is maximized when points are projected onto this direction.

<img class="center-image" src="{{ '/assets/img/matrix-notations/pca.png' | relative_url }}" alt="Principal Component Analysis" width="300"/>
<div class="figure-legend" markdown="1">
Illustration of the principal components of a 2-dimensional multivariate Gaussian distribution, from [Wikipedia](https://en.wikipedia.org/wiki/Principal_component_analysis).
</div>

The norm of the projection of vector $\mathbf{x}_n$ along vector $\mathbf{w}$ is given by $\mathbf{x}_n^\top\mathbf{w}$ when 
$$||\mathbf{w}||_2 = 1$$ (cf. [exercise 4][part-exercise-4] below), so assuming points are centered, we want to solve:

$$
\underset{\mathbf{w}}{\text{maximize }} \left(\frac{1}{N}\right) \sum_{n=1}^N (\mathbf{x}_n^\top\mathbf{w})^2
\quad \text{such that } ||\mathbf{w}||_2=1
$$

If we insist on writing this is full index notations, this is our problem:

$$
\underset{w_1, \dots, w_K}{\text{maximize }}
\sum_{n=1}^N \left( \sum_{k=1}^K x_{n,k}w_k\right)^2
\quad \text{s.t. } \sqrt{\sum_{k=1}^K w_k^2} = 1
$$

Again, this problem does not seem so easy at first glance.

But wait... A bunch of elements with the $n^\text{th}$ element being equal to $\mathbf{x}_n^\top\mathbf{w}$? We've seen that already, that's $\mathbf{Xw}$. The sum of the squares of these elements? That's the $\ell 2$ norm of this vector. The constraint on the norm of $\mathbf{w}$ is slightly trickier to deal with, but can be tackled with a [Lagrange multiplier](https://en.wikipedia.org/wiki/Lagrange_multiplier) $\lambda$ *(maybe I'll write an article on this topic some day).*

So in matrix form, our problem can be written as

$$
\underset{\mathbf{w}}{\text{maximize }} ||\mathbf{Xw}||_2^2 + \lambda(1-||\mathbf{w}||_2^2)
$$

A trivial application of [matrix calculus][matrix-calculus] ([exercise 8][calculus-exercise-8] of referenced blog post) yields that the quantity above is maximized if

$$
\mathbf{X}^\top\mathbf{Xw} = \lambda \mathbf{w}
$$

i.e. if $\mathbf{w}$ is an eigenvector of the covariance matrix $\mathbf{X}^\top\mathbf{X}$.

Wanna try getting this result without explicitly writing $\mathbf{X}$ as matrix? Good luck with that.

And we could even continue further with PCA: once we have computed the first $C$ principal components $\mathbf{P} = (\mathbf{p}_1, \dots, \mathbf{p}_C)^\top \in \mathbb{R}^{C \times K}$ as the first $C$ eigenvectors of the covariance matrix $\mathbf{X}^\top\mathbf{X} \in \mathbb{R}^{K \times K}$ (one line of code using numpy), the *transform* operation is $\mathbf{Z} = \mathbf{XP}^\top$. The *inverse transform* operation is $\hat{\mathbf{X}} = \mathbf{ZP}$.

So there you have it: once you speak the language of the gods (i.e. the language of matrices, in case you haven't been following *at all*), deriving PCA is a few lines of calculations. A working implementation is a few lines of code.

### Syvester equations

OK, one last (optional) example to really hammer it in.

Given $3 \times N \times N$ values $a_{m,n}, b_{m,n}, c_{m,n}$ for $(m,n) \in \\{1, \dots, N \\}^2$, find $N \times N$ values $x_{m,n}$ such that

$$
\sum_k (a_{m,k}x_{k,n} + b_{k,n}x_{m,k} - \frac{1}{N^2}c_{m,n}) = 0 \quad \forall m,n
$$

Finished yet? No? Yeah, I didn't think so.

Let's rewrite it in matrix form ([exercise 9][part-exercise-9]):

$$
\mathbf{AX} + \mathbf{XB} = \mathbf{C}
$$

Boom! That's a [Sylvester equation](https://en.wikipedia.org/wiki/Sylvester_equation). It's as good as solved.

Now, I need to refrain myself from going on and on about how the exact same trick can be applied to low-rank matrix factorization for recommendation systems, to Support Vector Machines, to everything related to deep learning...
I think you get my point.

### The point.

Hopefully, I managed to convince you that many machine learning methods can only be truly understood through the lense of linear algebra.

But, what is really the point of all of this? Is being able to derive the analytical solution to least square linear regression or similar problems of any practical use? After all, there are litteraly dozens of libraries that can do this automatically for us.

Well, I'm glad you asked!

First, I 100% guarantee that someone mindlessly *.fit.predicting* (yes, that's a word now) their way to predictions using existing implementations without understanding how the underlying algorithm works is bound to make some dumb mistakes sooner or later. I could tell you quite a few horror stories on this topic, and I probably will in a future blog post. So in general, the more you know, the less likely you are to do something stupid.

Second, truly mastering the basics is a pre-requisite to identifying situations where the same ideas can be applied to obtain non-trivial results.
After all, this is what this blog is supposed to be about — and this should hopefully be illustrated soon enough with real case studies on e.g. 3D facial shape estimation from photos, or internal bone shape estimation from 3D surface mesh. So stay tuned!

And of course, mastering the basics is also a pre-requisite to work on cutting-edge topics. Mastering PCA is a first step in mastering auto-encoders. Auto-encoders lead to VAEs. VAEs lead to diffusion models; diffusion models lead to <del>the dark side</del> image generation models — which are great to generate awesome illustrations for ridiculously technical blog posts.

And guess what? Being really confortable with matrix notations can be of *huge* help when learning about these topics. So let's continue!

</details>

## The case for speed

In addition to the ability to easily solve seemingly hard problems, I mentioned that a second big advantage to writing everything in matrix/vector format is speed of execution.

So, let's do a very quick test that should hopefully help me convert any remaining non-believer.

### Implementation with index notation

Let's first create a reasonably large dummy dataset for test purposes using [numpy](https://numpy.org/).

```python
# Let's define some randomly generated test data
import numpy as np
np.random.seed(42)

N, K = 50000, 1000 # number of samples N and dimension K of feature space
X = np.random.randn(N, K) # our feature matrix, shape (N,K)
y = np.random.randn(N) # our target vector, shape (N,)
w = np.random.randn(K) # some weights for our linear model, shape (K,)
```

Let's try a first approach where we compute the error $\mathcal{L}$ on this fairly large dataset using sums and for loops, based on the index notation:

$$
\mathcal{L} = \sum_{n=1}^N (\sum_{k=1}^K w_k x_{n,k} - y_n)^2
$$

```python
def make_prediction(weights: list, sample: list) -> float:
    """Make one prediction as a linear combination of inputs and weights."""
    total = 0
    for wi, xi in zip(weights, sample):
        total += wi * xi
    return total

def compute_error(weights: list[float], samples: list[list[float]], targets: list[float]) -> float:
    """Compute the sum of the squared error between the prediction and the target on the full dataset."""
    total_error = 0
    for xn, yn in zip(samples, targets):
        prediction = make_prediction(weights, xn)
        error = prediction - yn
        total_error += error ** 2
    return total_error
```

Running this:
```python
print(compute_error(w, X, y))
```
takes about 3.4 seconds on my computer.

Notice that there is nothing particularly wrong with this code, it is a mostly straightforward Python implementation of the formula above.

### Implementation with matrix notation

Now let's compute the exact same thing, this time using linear algebra operations from numpy to implement the loss directly from matrix notation:

$$
\mathcal{L} = ||\mathbf{Xw} - \mathbf{y}||_2^2
$$

```python
def compute_error_with_linear_algebra(weights: np.ndarray, samples: np.ndarray, targets: np.ndarray) -> float:
    """Same as above, this time using the linear algebra formulation."""
    return np.linalg.norm(X @ w - y) ** 2

print(compute_error_with_linear_algebra(w, X, y))
```

The numerical result we obtain is exactly the same, but this time the code ran in...

🥁

🥁

🥁

22 milliseconds. That is ***more than 100 times faster***!

<details markdown="1">
<summary>Why is it so fast?</summary>

Very briefly: Python is an interpreted language that is quite slow overall, whereas there are hyper-optimised linear algebra libraries (on top of which Python wrappers such as numpy are built) which make smart use of CPU caches and specific CPU instructions to do matrix multiplication very, very efficiently. Hence the performance difference when we use the latter, even when they are called from our slow Python code.

And we did not even go into GPU territory! Writing native, efficient CUDA code is a huge pain in the *gluteus maximus*, but simply writing everything in terms of matrices/tensors makes it super easy to run our pipeline with Pytorch or other specialised frameworks that do all the heavy-lifting for us.

</details>

Also, it is noteworthy that *we are not even solving the linear regression problem yet*. We were merely computing the cost. If we instead compare our analytical solution from earlier with a multistep gradient descent solver with a numerical gradient estimation implemented using sums over indices, we're not talking about a 100-fold performance gain anymore. More likely a 10000-fold. To emphasize, this is not an instance where I'm deliberately exagerating to prove a point: I quite literally mean that the latter approach would converge approximately 10000 times more slowly.

Don't believe me? I am currently in the process of writing a bonus part to this (already way too long) blog post, in which I should hopefully be able to demonstrate a *billion*-fold speed-up thanks to the power of matrix notations. So stay tuned!

OK, we are running short on time, so we only have time for one more question from the imaginary audience. Mmmmh, you there, please go ahead.

*"One toy example is nice, but my question is: does this translate to actual improvements in practice?"*

*Yes*. Yes yes yes. Oh yes, trust me, it does. There were several occasions where I was able to achieve similar or even higher performance improvements to existing code. And let me tell you, achieving a 1000-fold speedup in production code is a great way to come across as a true Machine Learning Legend™.

## Practice time!

Congrats on following so far! Hang in there, you only have a few steps left before completing your initiation to the divine language of matrix notations. But first, I have some good news and some bad news.

The bad news: seamlessly translating sums and loops to vector and matrix operations or vice versa is (generally) not an innate ability — at least it wasn't for me. As with everything worth doing, it takes some practice to get confortable in this exercise.

The good news: practice is what this section is for! 
For each of the examples below, try to either write it in matrix notation if it is written with sums over indices, or vice versa. As a bonus, you can also try to write the corresponding code with a linear algebra library such as numpy.

You may look at the solution of the first exercise (which is a really basic example) to clarify what is being asked if you want. But ideally, you should try to do the other ones yourself.

<div class="silverhighlight" markdown="1">
Hints: some of these exercises may require the use of:

- The $\ell 1$ norm
$$||\cdot||_1$$: for vector $\mathbf{a} \in \mathbb{R}^K$,

$$||\mathbf{a}||_1 = \sum_k |a_k| $$

- The element-wise or *Hadamart* product $\odot$: for matrices $\mathbf{A}$ and $\mathbf{B}$ with compatible dimensions:

$$(\mathbf{A} \odot \mathbf{B})_{m,n} = a_{m,n} b_{m,n}$$

- The all-$0$ or all-$1$ *vectors* $\boldsymbol{0}$ or $\boldsymbol{1}$:

$$ \boldsymbol{0} = \begin{pmatrix} 0 \\ \vdots \\ 0 \end{pmatrix}, \quad \boldsymbol{1} = \begin{pmatrix} 1 \\ \vdots \\ 1 \end{pmatrix}$$

</div>

A final piece of advice: before diving headfirst into the calculations, questions that should be asked include: what is the nature of the result and the different operands involved? Are they scalars, vectors, matrices? Are their dimensions compatible?

All right! I have been doing all the work so far, now it is your turn!

#### Exercise 0 (demo)

$$\sum_j a_{i,j} b_j$$

<details markdown="1">
<summary>Solution</summary>

There are two indices $i$ and $j$ for object $a$, so it seems to be a matrix, which we can write $\mathbf{A}$ (*cf.* the quick note on notations earlier). Assuming $i$ ranges from $1$ to some integer $I$, and $j$ from $1$ to $J$, $\mathbf{A}$ is of size $I \times J$, i.e. $\mathbf{A} \in \mathbb{R}^{I \times J}$.

Similarly, there is only one index $j$ for $b$, so it is probably a vector, which we can write $\mathbf{b} \in \mathbb{R}^J$.

We are summing over index $j$, multiplying $a_{i,j}$ with $b_j$. This is a dot product between $\mathbf{a}_i$, the $i^\text{th}$ row of $\mathbf{A}$, and $\mathbf{b}$. We are not summing over $i$, so we can assume that we are doing this operation for every $i$ in $\{1, \dots, I\}$, resulting in a vector of size $I$.

Performing $I$ distinct dot products, each defined by the row of a matrix, is the definition of a matrix-vector multiplication, so we can rewrite this as

$$\mathbf{A}\mathbf{b} \in \mathbb{R}^I, \quad \text{with } \mathbf{A} \in \mathbb{R}^{I \times J} \text{ and } \mathbf{b} \in \mathbb{R}^J$$

Numpy implementation: assuming variables `A` and `b` have been previously defined, for example with:
```python
# Initialize random matrix and vector
I, J = 3, 4
A = np.random.randn(I,J)
b = np.random.randn(J)
```
the operation above can be written as:
```python
# Perform matrix-vector multiplication
A @ b
# or equivalently: np.dot(A, b), or A.dot(b)
```
</details>

<details markdown="1" style="background-color: white;">
<summary>Show exercises</summary>

#### Other practice exercises

##### Exercise 1

$$\sum_i (a_{i} - b_i) b_i$$

<details markdown="1">
<summary>Solution</summary>

$a$ and $b$ have one shared index $i$, so they seem to be vectors with the same dimension. Assuming again that $i$ ranges from $1$ to some number $I$, we can write $\mathbf{a},\mathbf{b} \in \mathbb{R}^I$. We are summing over every index, so the result seems to be a scalar.

We have a sum of products: each $a_{i} - b_i$ is multiplied with each $b_i$, and the results are summed.
$a_i - b_i$ corresponds to element number $i$ of vector $(\mathbf{a} - \mathbf{b})$, and $b_i$ is element $i$ of vector $\mathbf{b}$, so our result corresponds to the dot product:

$$
(\mathbf{a} - \mathbf{b})^\top \mathbf{b}
$$

Numpy implementation: assuming variables `a` and `b` have been defined in a manner similar to previously, we can express this as:
```python
# Dot product of (a - b) and b
(a - b).T @ b
# in this case, numpy would also accept np.dot(a - b, b) or (a - b) @ b
```
</details>

##### Exercise 2

$$(\mathbf{A} \odot \mathbf{B}) \mathbf{c}$$

<details markdown="1">
<summary>Solution</summary>
This time, the quantity is expressed in matrix notation, so we are expected to convert it to index notation — which is generally easier.

Let's look at our objects: since $\mathbf{A}$ and $\mathbf{B}$ are written in bold, uppercase letters, we can expect them to be matrices, as per the note *"a quick note on notations"* in the article above. The Hadamart product implies that they are of the same size: let's write $\mathbf{A}, \mathbf{B} \in \mathbb{R}^{I \times J}$ for some $I$ and $J$.
$\mathbf{c}$ is written in a bold, lowercase letter, so it's probably a vector. For the expression to make sense, we need to have $\mathbf{c} \in \mathbb{R}^{J}$.
The result of the operation above should then be a vector of size $I$, with elements $i$ ranging from $1$ to $I$.

Each element $i,j$ of $\mathbf{A} \odot \mathbf{B}$ is given by $a_{i,j}b_{i,j}$ according to the definition of the Hadamart/element-wise product above. We then perform a matrix-vector multiplication between this matrix and vector $\mathbf{c}$, resulting in a vector whose $i^\text{th}$ element is given by

$$
\sum_{j=1}^J a_{i,j}b_{i,j}c_j
$$

Numpy implementation assuming `A`, `B` and `c` have been defined:
```python
(A * B) @ c
```
</details>

##### Exercise 3

$$\sum_j b_j  a_{j,i}$$


<details markdown="1">
<summary>Solution</summary>

Compared to exercise 0, $a$ and $b$ have switched places, which does not impact result as scalar multiplication is commutative. More importantly, indices $i$ and $j$ have also switched places with respect to $a$: so now, each dot product applied to $\mathbf{b} \in \mathbb{R}^J$ is defined by a *column* $\mathbf{a}_{:,i}$ of a matrix $\mathbf{A} \in \mathbb{R}^{J \times I}$, not by a row as previously.

To write this in terms of matrix/vector operations, we can simply *transpose* matrix $\mathbf{A}$ so that the resulting rows correspond to the previous column:

$$\mathbf{A}^\top\mathbf{b} \in \mathbb{R}^I, \quad \text{with } \mathbf{A} \in \mathbb{R}^{J \times I}, \mathbf{b} \in \mathbb{R}^J$$

Numpy implementation:
```python
A.T @ b
```
</details>

##### Exercise 4

$$\frac{\sum_j a_j b_j}{\sum_j b_j^2} b_i$$


<details markdown="1">
<summary>Solution</summary>

$\mathbf{a}$ and $\mathbf{b}$ are apparently both vectors with same dimension $\mathbb{R}^I$. We are summing over one index $j$ and there is one "free" index $i$ so the result is a vector with same dimension $\mathbb{R}^I$.

This is
$$
\frac{\mathbf{a}^\top\mathbf{b}}{||\mathbf{b}||_2^2}\mathbf{b}
$$
which is actually the definition of the vector projection of $\mathbf{a}$ onto $\mathbf{b}$ (and a useful formula to remember).

Numpy implementation:
```python
a @ b / np.linalg.norm(b)**2 * b
# or equivalently, since np.linalg.norm(b) = b @ b:
# a @ b / (b @ b) * b # check parentheses
```
</details>

##### Exercise 5

$$\sum_i \sum_j a_{i,j}b_j$$


<details markdown="1">
<summary>Solution</summary>

We seem to have $\mathbf{A} \in \mathbb{R}^{I \times J}$, $\mathbf{b} \in \mathbb{R}^{J}$.

$\sum_j a_{i,j}b_j$ is simply element $i$ of $\mathbf{Ab}$ (exercise 0).
Let's call this vector $\mathbf{c} = \mathbf{Ab} \in \mathbb{R}^{I}$ to simplify discussion.

We are summing over every element $c_i$ of $\mathbf{c}$ with $\sum_i c_i$. How can we express this in matrix notation?

Can we use
$$||\mathbf{c}||_1$$? Nope, this would be
$$\sum_i |c_i|$$. We don't want the absolute value
$$|\cdot|$$.

One possible trick is to use the all-$1$ vector $\boldsymbol{1}$:

$$\boldsymbol{1}^\top\mathbf{c} = \sum_i 1 \cdot c_i = \sum_i c_i$$.

So finally, we can write:

$$
\boldsymbol{1}^\top\mathbf{Ab}
$$

(This may seem a bit over-the-top, but this trick is sometimes useful).

Numpy implementation:
```python
# Direct implementation of the formula above:
ONE = np.ones(A.shape[0])
ONE.T @ A @ b
# However, using numpy function "sum" is probably more readable in this case:
(A @ b).sum() # or np.sum(A @ b) etc
```

</details>

##### Exercise 6

$$\sum_i a_i b_i c_i$$

<details markdown="1">
<summary>Solution</summary>

We have $\mathbf{a}, \mathbf{b}, \mathbf{c} \in \mathbb{R}^{I}$.

For a sum-product of the elements of 3 vectors, we need to multiply two of them pairwise with the Hadamart product:

$$
(\mathbf{a} \odot \mathbf{b})^\top \mathbf{c}
$$

or equivalently

$$
\mathbf{a}^\top (\mathbf{b} \odot \mathbf{c})
= \mathbf{b}^\top (\mathbf{a} \odot \mathbf{c})
= \mathbf{c}^\top (\mathbf{b} \odot \mathbf{a})
= \dots
$$

Numpy implementation:
```python
# Direct implementation :
(a * b) @ c
# as usual, there are many other possibilities, such as
# (a * b * c).sum() ...
```
</details>

##### Exercise 7

$$\sum_i \sum_j b_{i,j} a_i a_j$$

<details markdown="1">
<summary>Solution</summary>

At first glance, we seem to be summing over all listed indices $i$ and $j$ of present objects $a$ and $b$, so we can expect the result to be scalar. Here, $b$ has two indices so is probably a matrix $\mathbf{B} \in \mathbb{R}^{I \times J}$, and $a$ is a vector $\mathbf{a} \in \mathbb{R}^{J}$.

The identity can first be rewritten as $\sum_i a_i \sum_j b_{i,j} a_j$, since $a_i$ does not depend on $j$. We can notice that $\sum_j b_{i,j} a_j$ corresponds to element $i$ of vector $\mathbf{Ba} \in \mathbb{R}^I$ (see exercise 0), which we may write $(\mathbf{Ba})_i$.
Identity is thus $\sum_i a_i (Ba)_i$: this is simply a dot product between vector $\mathbf{a}$ and vector $\mathbf{Ba}$.

One important thing to notice: vector $\mathbf{a}$ must have as many elements as matrix $\mathbf{B}$ has columns for product $\mathbf{Ba}$ to be defined. But $\mathbf{a}$ must also have as many elements as vector $\mathbf{Ba}$ for $\sum_i a_i (\mathbf{Ba})_i$ to be defined, *i.e.* have as many elements as $\mathbf{B}$ has rows. So $I=J$ and $\mathbf{B}$ must be a square matrix.

So the final result is:

$$\mathbf{a}^\top\mathbf{B}\mathbf{a} \in \mathbb{R}, \quad \text{with } \mathbf{B} \in \mathbb{R}^{I \times I}, \mathbf{b} \in \mathbb{R}^I$$

In general, $\mathbf{a}^\top\mathbf{B}\mathbf{c}$ is called a [bilinear form](https://en.wikipedia.org/wiki/Bilinear_form).

Numpy implementation:
```python
a.T @ B @ a
```
</details>

##### Exercise 8

$$\sum_i a_i b_i b_j$$

<details markdown="1">
<summary>Solution</summary>

We have one free index $j$.

This is element $j$ of vector

$$
\mathbf{a}^\top \mathbf{b} \cdot \mathbf{b}
$$

(where $\cdot$ is the usual scalar-vector multiplication)

Numpy implementation:
```python
a @ b * b
```
</details>

##### Exercise 9

$$\sum_k (a_{i,k}x_{k,j} + b_{k,j}x_{i,k} + c_{i,j})$$

<details markdown="1">
<summary>Solution</summary>

Let's break things down:

$$
\begin{align*}
\sum_k (a_{i,k}x_{k,j} + b_{k,j}x_{i,k} + c_{i,j})
&= \sum_k a_{i,k}x_{k,j} + \sum_k b_{k,j}x_{i,k} + \sum_k c_{i,j} \\
&= \sum_k a_{i,k}x_{k,j} + \sum_k x_{i,k}b_{k,j} + IJ \cdot c_{i,j}
\end{align*}
$$

First sum corresponds to element $(i,j)$ of $\mathbf{AX}$,
second sum to element $(i,j)$ of $\mathbf{XB}$,
and third element to $IJ$ times element $(i,j)$ of $\mathbf{C}$

with $\mathbf{A} \in \mathbb{R}^{I \times J}$,
$\mathbf{X} \in \mathbb{R}^{I \times J}$,
$\mathbf{B} \in \mathbb{R}^{I \times J}$
and $\mathbf{C} \in \mathbb{R}^{I \times J}$.

Final result:

$$
\mathbf{AX} + \mathbf{XB} + \frac{1}{IJ}\mathbf{C}
$$

Equations of the form $\mathbf{AX} + \mathbf{XB} = \mathbf{D}$ are called [Sylvester equations](https://en.wikipedia.org/wiki/Sylvester_equation), and are easy to solve.

Numpy implementation:
```python
A @ X + X @ B + I * J * C
```
</details>

##### Exercise 10

$$\mathbf{a}\mathbf{b}^{\top}$$

<details markdown="1">
<summary>Solution</summary>

Here, $\mathbf{a}$ and $\mathbf{b}$ are implied to be vectors.

This is a (deliberately) slightly tricky question as the notation may be a bit ambiguous, but let's see if we can infer something.

I mentionned in comment *"Where does this notation come from?"* that $\mathbf{a}^{\top}\mathbf{b}$, a possible notation for the dot product of vectors $\mathbf{a}$ and $\mathbf{b}$, can be understood as initially considering the two vectors as $K \times 1$ matrices, transposing $\mathbf{a}$ to a $1 \times K$ matrix, performing a dot product and "casting" the resulting $1 \times 1$ matrix as a scalar.

We can do the exact same thing here: consider the matrix multiplication of implicit matrices $\mathbf{a} \in \mathbb{R}^{K \times 1}$ and $\mathbf{b}^\top \in \mathbb{R}^{1 \times K}$, whose result is e.g. $\mathbf{C} \in \mathbb{R}^{K \times K}$, a matrix with elements $c_{i,j}$ equal to:

$$a_i b_j \quad \text{with } (i, j) \in \{1, \dots, K\} \times \{1, \dots, K\}$$

$\mathbf{a}\mathbf{b}^\top$ is the *outer product* of vectors $\mathbf{a}$ and $\mathbf{b}$, as opposed to $\mathbf{a}^\top\mathbf{b}$ which is the *inner product*.

Numpy implementation:
```python
# Does a @ b.T work?
# It looks like it should, but unfortunately, it does not work if a and b have been defined as vectors.
# This is because numpy will be doing some implicit recasting/reshaping before doing the operation.
# However, this does work if we explicitly reshape a and b as matrices (-1 means as many rows as elements, 1 for 1 column):
a.reshape(-1, 1) @ b.reshape(-1, 1).T
# Another possibility is to directly use the outer product function from numpy:
np.outer(a, b)
```

</details>

##### Exercise 11

$$a_i b_j b_i$$

<details markdown="1">
<summary>Solution</summary>

This is equal to $a_i b_i b_j$. This is element $i,j$ of matrix

$$
(\mathbf{a} \odot \mathbf{b}) \mathbf{b}^\top
$$

Numpy implementation:
```python
np.outer(a * b, b)
```

</details>

##### Exercise 12

$$\sum_i c_{i,k} a_j \sum_k a_{k,i} b_j$$

<details markdown="1">
<summary>Solution</summary>

This one is simple:
$a$ sometimes has 1 index as in $a_j$, sometimes 2 as in $a_{k,i}$.

Is $a$ a matrix? A vector? We don't know and whatever the case, the formula doesn't really seem to make sense.

So whoever wrote this probably made a mistake somewhere*.

<sup><sub>*\*Either that, or this person wrote it as a pedagogical example for their machine learning blog. I guess we'll never know.*</sub></sup>

</details>

##### Exercise 13

$$\sum_i c_{i,j} a_i \sum_k b_{i,k} a_k$$

<details markdown="1">
<summary>Solution</summary>

This one does seem to make sense (I'll let you check, you should start getting used to it by now).

It corresponds to element $j$ of

$$
\begin{align*}
&\mathbf{C}^\top(\mathbf{a} \odot \mathbf{Ba}) \\
\big( = &\mathbf{a} \odot \mathbf{C}^\top\mathbf{Ba} = \dots\big)
\end{align*}
$$

</details>

##### Exercise 14

$$\sum_i b_i \mathbf{a}_i a_{i,j}$$

<details markdown="1">
<summary>Solution</summary>

At first glance, this one again doesn't seem to make sense: there is sometimes 1 index for $a$ as in
$$\mathbf{a}_i$$, sometimes 2 as in
$$a_{i,j}$$.

*However*, we can notice that when there is just 1 index, $\mathbf{a}$ is written in bold lowercase: we may thus interpret $\mathbf{a}_i$ as a vector corresponding to row number $i$ of matrix $\mathbf{A} \in \mathbb{R}^{I \times J}$.
Thus, $\mathbf{a}_i \in \mathbb{R}^J$.
This is similar to how previously, sample $\mathbf{x}_n$ was a $K$-dimensional vector, corresponding to training sample in row number $n$ of the feature matrix $\mathbf{X} \in \mathbb{R}^{N \times K}$.

$b_i$ and $a_{i,j}$ are both scalars, so $b_i \mathbf{a}_i a_{i,j} = b_i i a_{i,j} \mathbf{a}_i$ is a scalar multiplied by a vector, i.e. a vector with the same size as $\mathbf{a}_i \in \mathbb{R}^J$.

$$
\mathbf{Ab} \odot \mathbf{A}
$$

(Agreed, the notation for this exercise was a bit unclear. I would in fact strongly discourage you from using such notations without first being cristal clear about the nature of every object involved and whatever it is you are talking about.)

</details>

</details>

## Conclusion

Aaaaand... You made it to the end! Congratulations!

Now, what's next?

First and foremost, don't hesitate to let me know in the comments that you made it to the end, so that I know at least one person managed to survive this entire post. While you're at it, I'd also greatly appreciate your feedback.

After that, I'd suggest you continue practicing with the exercises, until they feel easy.
You can also invent new exercises if you want — and leave them in comments below, or email them to me.
Although it was not the main topic of this blog post, it is also particularly useful to practice using numpy functions like sum, mean, argmin etc. in conjunction with numpy axes. Other libraires like Pytorch work in a very similar way.

And finally, you may want to check out my other blog posts. A natural continuation of this one would be the one on [matrix calculus][matrix-calculus].

See you there, and thanks for reading! *(todo: find a catchier signature catch to conclude posts)*

<!---
This should be a hidden comment.

Notes: replace ref to article on tensors when ready. Same for Fibonacci bonus part.
Same for Lagrange multiplier (maybe one day).
#TODO A few parts left to complete.

Similarly, useful to pratice sum, mean, argmin etc and getting familiar with axes in e.g. numpy (other libraires like Pytorch work the same way)

Put exercises in details?
-->

[part-speed]: {% link _posts/2025-07-21-thinking-in-matrices.md %}#the-case-for-speed
[part-gifts]: {% link _posts/2025-07-21-thinking-in-matrices.md %}#other-gifts-from-the-linear-algebra-overlords
[part-exercises]: {% link _posts/2025-07-21-thinking-in-matrices.md %}#other-practice-exercises

[part-exercise-9]: {% link _posts/2025-07-21-thinking-in-matrices.md %}#exercise-9
[part-exercise-4]: {% link _posts/2025-07-21-thinking-in-matrices.md %}#exercise-4

[about]: {% link about.md %}
[matrix-calculus]: {% link _posts/2025-07-22-matrix-calculus.md %}
[calculus-exercise-8]: {% link _posts/2025-07-22-matrix-calculus.md %}#exercise-8
[pseudo-inverse]: {% link _posts/2025-07-24-pseudo-inverse.md %}
[introduction-tensors]: https://comingsoon.com/
