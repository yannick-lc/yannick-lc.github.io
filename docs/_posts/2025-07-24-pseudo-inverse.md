---
layout: post
title:  "\"Impossible\" systems of equations and pseudo-inverse"
date:   2025-07-24 10:22:40 +0200
update_date:  2025-07-24 11:22:40 +0200
categories: foundations
---

<img class="center-image" src="{{ '/assets/img/pseudo-inverse/mocking-spongebob.jpg' | relative_url }}" alt="Confused Neo" width="300"/>
<div class="figure-legend">
You may be laughing now, SpongeBob, but the joke might be on you after reading this article.
</div><br/>

What is the common thread between (least squares) linear regression, 3D hand landmarks localization, 3D facial shape estimation and wrist bone reconstruction from skin surface mesh?

Yes, these are all topics I worked on and for which blog posts are planned.

But, more to the point of this article: all these tasks can be reduced to the same mathematical problem, and solved with what is called a *pseudo-inverse*.
So I figured this is a topic that *might* deserve its own article — partly so that I can point to it from pretty much all future articles on this blog.

Similarly to the articles on [matrix notation][matrix-notation] and [matrix calculus][matrix-calculus], this post is another bastard child between machine learning and applied math: too basic and not rigorous enough to be fully math, but too generic and foundational to directly be machine learning.
Still, this is a super convenient and ubiquitous tool, that any Machine Learning Legend should have in its toolbox.

<!--- While I'm at it, I'll also generalize... -->

<details markdown="1">
<summary>TL;DR</summary>

A quick recap of this article is available [at the end][tldr].

</details>

## Well-behaved systems of equations

Let's start with the basics: simple  systems of equations.

Consider this system of 2 equations with 2 unknowns $x_1$ and $x_2$:

$$
\begin{equation}
\begin{cases}
2x_1 - x_2 = 6 \\
x_1 = 4
\end{cases}
\end{equation}
$$

This system is nice enough to already be in triangular form, so it is easy to see that there is exactly one solution:

$$\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 4 \\ 2 \end{pmatrix}$$

If the system was not in triangular form, e.g.

$$\begin{cases}
2x_1 - x_2 = 6 \\
x_1 + x_2 = 6
\end{cases}$$

we could simply express $x_2$ as a function of $x_1$ using the first line (e.g. $x_2 = 2x_1 - 6$), replace the value of $x_2$ in the second line by this expression and develop to obtain $3x_1 = 12$ i.e. $x_1 = 4$. And *voilà*!

More generally, given a system of $N$ equations with $N$ unknown $x_1, \dots, x_N$

$$
\begin{equation}
\begin{cases}
a_{1,1}x_1 + a_{1,2}x_2 + \dots + a_{1,N}x_N = b_1 \\
a_{2,1}x_1 + \dots + a_{2,N}x_N = b_2 \\
\vdots \\
a_{N,1}x_1 + \dots + a_{N,N}x_N = b_N \\
\end{cases}
\end{equation}
$$

we could use the [Gauss elimination method](https://en.wikipedia.org/wiki/Gaussian_elimination) to similarly put the matrix in [row echelon form](https://en.wikipedia.org/wiki/Row_echelon_form) and solve the system*.

Even better yet, after reading the [article on matrix notation][matrix-notation], we can acknowledge that it is usually a good idea to write everything in matrix form whenever possible, and rewrite the system as

$$
\begin{equation}
\mathbf{A}\mathbf{x} = \mathbf{b}
\end{equation}
$$

with
$$\mathbf{A} = \begin{pmatrix}
a_{1,1} & \dots & a_{1,N} \\
\vdots & \ddots & \vdots \\
a_{N,1} & \dots & a_{N,N}
\end{pmatrix} \in \mathbb{R}^{N \times N}$$
and
$$\mathbf{b} = (b_1 ~\dots ~ b_N)^\top \in \mathbb{R}^{N}$$ being the *parameters* of our system,
and $\mathbf{x} = \begin{pmatrix} x_1 \\ \vdots \\ x_N \end{pmatrix} = (x_1 ~\dots ~ x_N)^\top \in \mathbb{R}^{N}$ being the *unknowns* whose values we are looking for.

<details markdown="1">
<summary>Example with previous system</summary>

With the system from Equation (2), we have
$$\mathbf{A} = \begin{pmatrix}
2 & 1 \\
1 & 0
\end{pmatrix} \in \mathbb{R}^{2 \times 2}$$
and $$\mathbf{y} = \begin{pmatrix} 6 \\ 4 \end{pmatrix} \in \mathbb{R}^{2}$$.

The solution to this system is $$\mathbf{x} = \begin{pmatrix} 4 \\ 2 \end{pmatrix} \in \mathbb{R}^{2}$$, and indeed we can check that $\mathbf{Ax} = \mathbf{b}$.

</details>

Now, we can remember from linear algebra classes that:

<div class="silverhighlight" markdown="1">
The system $\mathbf{A}\mathbf{x} = \mathbf{b}$ has a unique solution if and only any of these is true:
- the rows of $\mathbf{A}$ are linearly independant
- the columns of $\mathbf{A}$ are linearly independant
- $\mathbf{A}$ is inversible
- $\text{det}(\mathbf{A}) \neq 0$
- etc. etc.

in which case the solution is given by

$$
\mathbf{x} = \mathbf{A}^{-1}\mathbf{b}
$$

</div>

*<sup><sub>(To obtain $\mathbf{x} = \mathbf{A}^{-1}\mathbf{b}$, we simply left-multiply both sides of $\mathbf{A}\mathbf{x} = \mathbf{b}$ by $\mathbf{A}^{-1}$, such that $\mathbf{A}^{-1}\mathbf{A}$ cancels on the left of $\mathbf{x}$)</sub></sup>*

OK, there shouldn't be anything new so far.

### Constraint optimization formulation

One equivalent way to look at this is to consider this problem as a *constraint satisfaction* problem.

We are looking for a vector $\mathbf{x} = (x_1, \dots, x_N)^\top$ which *satisfies* a number of constraint. Line 1 of Equation (2) states that the vector $\mathbf{x}$ we are looking for *must* be such that:

$$
a_{1,1}x_1 + \dots + a_{1,N}x_N = b_1
$$

Similarly, line 2 of Equation (2) states that $\mathbf{x}$ must satisfy
$a_{2,1}x_1 + \dots + a_{2,N}x_N = b_2$, and so on and so on for each of the $N$ constraints.

The fact that the matrix is invertible means that we have the "right" constraints in some sense: enough constraints to ensure the solution is unique, but not too many such that there is no solution.

*Of course, having the right number of constraints ($N$) is <u>necessary</u> but <u>not sufficient</u>. What is important here is also the "unicity" of each constraint: a constraint that is identical to a previous constraint does not bring anything new to the table, and can be discarded as redondant. In general, any constraint that is a linear combination of previous contraints is redondant. So to ensure that a solution exists and is unique, we need a set of $N$ (linearly) <u>independant</u> constraints.*

The rest of this series of articles explores what happens when we have either "too many" or "too few" constraints to have a "well-behaved" system with a unique solution.

## Over-constrained systems of equations

### A seemingly impossible system

OK, so what if we add one more "constraint" in the system from Equation (1), for instance:

$$
\begin{equation}
\begin{cases}
2x_1 - x_2 = 6 \\
x_1 = 4 \\
x_1 = 6
\end{cases}
\end{equation}
$$

Wait... How can that make any sense, [Yannick][yannick]? You must have made a typo or something: this system obviously can't be solved anymore, as $x_1$ cannot be simultaneoulsy equal to 4 *and* to 6.

True, true. If we look at the corresponding matrix
$$
\mathbf{A} = \begin{pmatrix}
2 & -1 \\
1 & 0 \\
1 & 0
\end{pmatrix}
$$,
we see that it is not even a square matrix, so its rows cannot be linearly independent and it cannot be invertible, so indeed there is not one unique solution. This would also be true even if we added a "virtual" variable $x_3$ to make $\mathbf{A}$ a square matrix, such that
$$
\mathbf{A} = \begin{pmatrix}
2 & -1 & 0 \\
1 & 0 & 0 \\
1 & 0 & 0
\end{pmatrix}
$$.

So, there seems to be no solution at all.

### The next best thing

But I find you rather pessimistic, dear reader. You say there is no solution. I say, if there is no solution, what is the next best thing? What would be the closest thing to a solution?

Intuitively, choosing $x_1=5$ seems closer to a solution than choosing $x_1 = 10^{10^{100}}$, since 5 is fairly close to both 4 and 6 (constraints of lines 2 and 3 in Equation (4)), whereas $10^{10^{100}}$ is not by any reasonable measure.
So, how could we formulate this idea in a more mathematical way?

Perhaps we could "loosen" our constraints a bit: instead of requiring that $\mathbf{x}$ must exactly satisfy each equality, we could merely ask that it is kind of close to satisfying each constraint. This would be analoguous to rewriting our system from Equation (4) as:

$$
\begin{equation}
\begin{cases}
2x_1 - x_2 \approx 6 \\
x_1 \approx 4 \\
x_1 \approx 6
\end{cases}
\end{equation}
$$

<div class="silverhighlight" markdown="1">
Or, in matrix form, we want to find $\mathbf{x}$ such that $\mathbf{Ax}$ approximates $\mathbf{b}$:

$$\mathbf{A}\mathbf{x}  \approx  \mathbf{b}$$

</div>

Notice that this time, $\mathbf{A}$ is not a square matrix: in general, assuming that we have a total of $N$ constraints for $K$ unknowns $(x_1, \dots, x_K)^\top = \mathbf{x} \in \mathbb{R}^K$, then $\mathbf{A} \in \mathbb{R}^{N \times K}$ and $\mathbf{b} \in \mathbb{R}^N$.

<sup><sub>(Since we are considering "over-constrained" systems of equations in this section, we assume for now that $N > K$).</sub></sup>

OK, how do we find $\mathbf{x}$ such that $\mathbf{A}\mathbf{x}  \approx  \mathbf{b}$? Actually, what do we even *mean* by that mathematically speaking?

If you're reading this blog, you're [supposed to be][about-ml] somehow into machine learning. So you may recall that in e.g. linear regression, we want to *approximate* targets $y_n$ for each sample $n \in \{1, \dots, N\}$ in our training dataset, so that our predictions $\hat{y}_n$ are close to the targets: $\hat{y}_n \approx y_n ~~ \forall n$. In the least square formulation, this is done by finding parameters that minimize the sum of the squared residues:

$$
\begin{equation}
\underset{}{\text{minimize}} ~
\sum_{n=1}^N (\hat{y}_n - y_n)^2
\end{equation}
$$

Or, in matrix form:

$$
\begin{equation}
\underset{}{\text{minimize}} ~
||\hat{\mathbf{y}} - \mathbf{y}||_2^2
\end{equation}
$$

*(If the jump from Equation (6) to Equation (7) above looks somehow confusing to you, you may want to read this other [article on matrix notation][matrix-notation], which I consider to be a prerequisite to all my blog posts including this one.)*

So, let's apply the same idea here, and penalize the squares of the differences between the elements of $\mathbf{A}\mathbf{x}$ and the elements of $\mathbf{b}$. We are trying to find a "pseudo-solution" $\mathbf{x} = (x_1, \dots, x_N)^\top$, a term I just made up to describe something close to a solution, which minimizes the sum of the squared differences.
That is:

<div class="silverhighlight" markdown="1">
We want to solve the following optimization problem:

$$
\begin{equation}
\underset{\mathbf{x}}{\text{minimize}} ~ ||\mathbf{Ax} - \mathbf{b}||_2^2
\end{equation}
$$

</div>

<details markdown="1">
<summary><em>Side note: why the *square* of the residues?</em></summary>

This quickly leads to a pretty deep rabbit hole, but very briefly, the argument is the same as for linear regression: we assume that the *residues*, or the training errors in the case of linear regression, are independant and are normally distributed. In this case, using maximum likelihood to estimate the parameters of the model, which are our unknowns $x_1, \dots, x_K$ in this case, is equivalent to minimizing the squares of the errors.

Maybe I'll write a more detailed blog post about this topic some day. But for now, you don't really need to bother with any of that. Just know that there is a reason why we are doing that.
</details>

<details markdown="1">
<summary>A few interesting* observations</summary>

**at least according to me at, but I'm sure you'll agree.*

First, if our system of equations is not overconstrained and does admit a unique solution

$$\mathbf{x} = \mathbf{A}^{-1}\mathbf{b}$$

then
$$\mathbf{A}\mathbf{x} = \mathbf{b}$$ and thus $||\mathbf{Ax}-\mathbf{b}||_2^2 = 0$, which is the lowest possible cost since $\forall \mathbf{z}, ~ ||\mathbf{z}||_2^2 \geq 0$. So our new formulation is a generalization of the previous one: if the system is solvable exactly, it yields the solution; otherwise it yields the best approximation of a solution, according to our definition of "best".

Second, you may recognize that this problem is very similar to the optimization problem for linear regression from e.g. [this article][matrix-calculus], namely:

$$
\underset{\mathbf{w}}{\text{minimize}} ~ ||\mathbf{Xw} - \mathbf{y}||_2^2
$$

And indeed, *they are the exact same problem mathematically speaking*. The only difference is in the names of the variables we use: in the previous article, $\mathbf{X} \in \mathbb{R}^{N \times K}$ was not the unknowns whose values we are looking for, but denoted the training features of our samples, and was thus a known parameter of our problem formulation. Instead, the unknowns were the parameters $\mathbf{w} \in \mathbb{R}^{K}$ of the linear regression model, which we were trying to estimate from the training features $\mathbf{X}$ and labels $\mathbf{y} \in \mathbb{R}^{N}$.
But the general idea and its mathematical formulation remain exactly the same.

</details>

### Solving the optimization problem

All of this may be nice conceptually but of very little practical use if we can't solve Equation (8). But as you may expect, I was not going to [rant] for multiple pages to conclude by *"This problem has no solution, too bad, all we just did was utterly useless"*.

So spoiler, alert:

<div class="goldhighlight" markdown="1">
The problem
$$\underset{\mathbf{x}}{\text{minimize}} ~ ||\mathbf{Ax} - \mathbf{b}||_2^2$$
does have* a neat, analytical solution, which is given by

$$\mathbf{x} = (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top\mathbf{b}$$

</div>

Getting to this result is not too difficult, and is a nice application of [matrix calculus][matrix-calculus-plat].
I am now going to briefly summarize how we can get to this result.

*Feel free to skip this part if you're OK with just admitting that this is true.*

First step: let's (re)clarify what we are looking for.

Although the expression
$$||\mathbf{Ax} - \mathbf{b}||_2^2$$ contains matrices and vectors, the quantity itself is a scalar. We are trying to minimize this quantity with respect to $\mathbf{x} \in \mathbb{R}^K$, so the (loss) function we are interested in is:

$$
\mathcal{L}: \mathbb{R}^K \rightarrow \mathbb{R}, \quad \mathbf{x} \mapsto ||\mathbf{A}\mathbf{x} - \mathbf{b}||_2^2
$$

We are trying to find a vector $\mathbf{x}^*$ that minimizes this function. Assuming this function admits a global minimum, the gradient of $\mathcal{L}$ with respect to $\mathbf{x}$,
$\frac{\partial \mathcal{L}}{\partial \mathbf{x}} \in \mathbb{R}^K$, is going to be equal to $\boldsymbol{0}$ at this minimum.

Using matrix calculus, we can establish that the gradient is

$$
\frac{\partial ||\mathbf{A}\mathbf{x} - \mathbf{b}||_2^2}{\partial \mathbf{x}}
= 2\mathbf{A}^\top(\mathbf{A}\mathbf{x} - \mathbf{b})
$$

<details markdown="1">
<summary>Where does this come from?</summary>

For a derivation of the gradient of
$$||\mathbf{A}\mathbf{x} - \mathbf{b}||_2^2$$ with respect to $\mathbf{x}$, you may want to check out this [other post][matrix-calculus-gradient] on matrix calculus.
<!--If you were already redirected to this post from [this post](), I promise this is the last post you will need to check before having the full explanation for why [solution to linear regression]-->
</details>

Now, we want this gradient to be equal to $\boldsymbol{0}$: this is the case if

$$
\mathbf{x} = (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top\mathbf{b}
$$

<details>
<summary>"Proof"*</summary>

$$
\begin{align*}
&2\mathbf{A}^\top(\mathbf{A}\mathbf{x} - \mathbf{b}) = \boldsymbol{0} \\
\iff &\mathbf{A}^\top\mathbf{A}\mathbf{x} = \mathbf{A}^\top\mathbf{b}
\end{align*}
$$
<em>(distributing $2\mathbf{A}^\top$ on $\mathbf{A}\mathbf{x}$ and $-\mathbf{b}$, moving $-2\mathbf{A}^\top\mathbf{b}$ on the right side and dividing both sides by 2)</em><br/><br/>

Left-multiplying both sides by $(\mathbf{A}^\top\mathbf{A})^{-1}$:
$$
\begin{align*}
(\mathbf{A}^\top\mathbf{A})^{-1}(\mathbf{A}^\top\mathbf{A})\mathbf{x} &= (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top\mathbf{b} \\
\iff \mathbf{x} &= (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top\mathbf{b}
\end{align*}
$$
</details>

And there we have it! $\mathbf{x} = (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top\mathbf{b}$ corresponds to the minimum of $\mathcal{L}$ as defined above.

<details markdown="1">
<summary>*A couple of precisions</summary>

Now, I admitedly took a few shortcuts in the "proof" above.

First, one assumption that we implicitly made is that $\mathbf{A}^\top\mathbf{A}$ is invertible. But is it true?

It turns out that yes, as long $N \geq K$ and the columns of $\mathbf{A}$ are linearly independent, i.e. $\text{rank}(\mathbf{A}) = K$. Or, simply speaking and slightly oversimplifying things: the constraints on $\mathbf{x}$ must be strong enough so that there is at most one possible value for each unknown, and possibly zero value.

Second, assuming that $\mathbf{A}^\top\mathbf{A}$ is indeed invertible, we found a point where the gradient is zero, i.e. we found a local extremum of $\mathcal{L}$. But is this extremum is a minimum or a maximum? Is it a local one or a global one?

One intuitive way to think about it is to see that $\mathcal{L}$ does seem to have a global minimum, as it makes sense that a set of variables which minimizes our loss $\mathcal{L}$ exists. On the other hand, there is no "worst" set of variables, because parameters can get arbitrarily bad: if $10^{100}$ is not a "bad enough" value for one of the unknowns, we can always use $10^{10^{100}}$, or $10^{10^{10^{100}}}$ and so on. So $\mathcal{L}$ does not seem to have a maximum.

For a little bit more information about why this true based on a reasoning that relies on the linear regression formulation, you may want to check out [this article][matrix-calculus-precisions].

<!--For a fully rigorous derivation of this result, you may enroll in a graduate class in multivariate calculus.-->
</details>

### Introducing pseudo-inverses

OK, let's compare the solution to our "impossible" system of equations with the solution of a "well-behaved" system of equations from earlier.

Let's start with the "well-behaved" system: for square matrix $\mathbf{A} \in \mathbb{R}^{N \times N}$, if

$$
\mathbf{Ax}=\mathbf{b}
$$

is a "well-behaved" system of equation with a unique solution $\mathbf{x}$, then this solution can be obtained thanks to the inverse $\mathbf{A}^{-1} \in \mathbb{R}^{N \times N}$ of matrix $\mathbf{A}$:

$$
\mathbf{x}=\mathbf{A}^{-1}\mathbf{b}
$$

Now let's consider a (possibly non square) matrix
$$\mathbf{A} \in \mathbb{R}^{N \times K}$$,
and an "impossible" system of equations $\mathbf{Ax}=\mathbf{b}$ that has no exact solution. Instead, we decided to solve the optimization problem: $\underset{\mathbf{x}}{\text{minimize}} ~ ||\mathbf{Ax} - \mathbf{b}||_2^2$, such that

$$
\mathbf{Ax} \approx \mathbf{b}
$$

Writing $\mathbf{A}^\dagger = (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top \in \mathbb{R}^{K \times N}$ and based on Equation (X), the solution to our optimization problem can be obtained with*:

$$
\mathbf{x}=\mathbf{A}^\dagger\mathbf{b}
$$

See what happens? In our "relaxed" problem formulation, $\mathbf{A}^\dagger$ plays a role similar to $\mathbf{A}^{-1}$ in a "strict" problem formulation, enabling us to find our pseudo-solution.
For this reason:

<div class="silverhighlight" markdown="1">
Given matrix $\mathbf{A} \in \mathbb{R}^{N \times K}$ and provided the following quantity is well defined*:

$$\mathbf{A}^\dagger = (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top \in \mathbb{R}^{K \times N}$$

$\mathbf{A}^\dagger $ is called the *pseudo-inverse* of matrix $\mathbf{A}$.
</div>

*\* i.e. provided $\text{rank}(\mathbf{A}) = K$, cf. subsection "A couple of precisions" above.*

This time, it is not a term I just made up: it really does exist, as evidenced by this [Wikipedia page](https://en.wikipedia.org/wiki/Generalized_inverse).
In general, the definition of a pseudo-inverse is a bit wider than this, but it is does not really matter for the purpose of this article.

### NumPy implementation and previous example

Going back to our previous example:

$$
\begin{equation}
\begin{cases}
2x_1 - x_2 = 6 \\
x_1 = 4 \\
x_1 = 6
\end{cases}
\end{equation}
$$

We can rewrite it in matrix notation as $\mathbf{Ax}=\mathbf{b}$ with
$$
\mathbf{A} = \begin{pmatrix}
2 & -1 \\
1 & 0 \\
1 & 0
\end{pmatrix}
$$
and
$$\mathbf{b} = \begin{pmatrix} 6 \\ 4 \\ 6 \end{pmatrix}$$.
Or, using NumPy:

```python
A = np.array([[2, -1], [1, 0], [1, 0]])
b = np.array([6, 4, 6])
```

The solution is then given by this very long, one-full-line of code implementation:
```python
x = np.linalg.pinv(A) @ b
# or equivalently: x = np.linalg.inv(A.T @ A) @ A.T @ b
```
This yields $(x_1,x_2) = (5,4)$, which is exactly what we expected!

We could also check that *if* a system has an exact solution, for instance

$$
\begin{cases}
2x_1 - x_2 = 6 \\
x_1 = 4 \\
\end{cases}
$$

i.e.
```python
A = np.array([[2, -1], [1, 0]])
b = np.array([6, 4])
```
then both $\mathbf{A}^\dagger\mathbf{b}$ and $\mathbf{A}^{-1}\mathbf{b}$ will yield the same result $(x_1,x_2) = (4,2)$.

### Wrapping up

OK, this may have been a lot to digest, so here is a quick recap of what we just discussed.

<div class="goldhighlight" markdown="1">
<a id="tldr"></a>

Some systems of equations, such as

$$
\begin{cases}
2x_1 - x_2 = 6 \\
x_1 = 4 \\
x_1 = 6
\end{cases}
$$

have too many or mutually exclusive constraints, and as a result there is no exact solution, i.e. there is no $\mathbf{x}$ such that $\mathbf{Ax}=\mathbf{b}$. Instead, we want to find *approximate solutions*, such that

$$
\mathbf{Ax} \approx \mathbf{b}
$$

This is achieved by solving the following optimization problem:

$$
\underset{\mathbf{x}}{\text{minimize}} ~ ||\mathbf{Ax} - \mathbf{b}||_2^2
$$

This problem (usually) has a neat analytical solution:

$$
\mathbf{x} = \mathbf{A}^\dagger\mathbf{b}
$$

where $\mathbf{A}^\dagger = (\mathbf{A}^\top\mathbf{A})^{-1}\mathbf{A}^\top$ is called the *pseudo-inverse* of $\mathbf{A}$.

If the system does admit an exact solution, i.e. if
$\underset{\mathbf{x}}{\text{minimum}} ~ ||\mathbf{Ax} - \mathbf{b}||_2^2 = 0$, then the pseudo-inverse is equal to the inverse: $\mathbf{A}^\dagger = \mathbf{A}^{-1}$. Thus, we can consider the pseudo-inverse to be a generalization of the inverse of a matrix.

</div>


### Conclusion

As stated in the introduction, being able to solve the problem 
$$
\underset{\mathbf{x}}{\text{minimize}} ~ ||\mathbf{Ax} - \mathbf{b}||_2^2
$$
is very, *very* useful, as this has *many* applications.
Practical examples of such applications are coming soon.

A second part to this article, dealing with *under*-constrained, i.e. systems of equations with *too few* constraints to have a unique solution, is also "dans les cartons".

So stay tuned!


<!-- Comment
Very, *very* useful! At least if you want to go beyond .fit .predict in machine learning.
Probably one of the most useful properties. I use it all the time.
With the ability to [increase performance 100-fold], it's another very cool way to come accross as a machine learning wizard.
(That's a cool title, maybe I should change my LinkedIn title to "machine learning wizard").
Rest of the article is not as essential so you may stop reading now if you want. Although it is still interesting and on the same topic.
-->

[matrix-notation]: {% link _posts/2025-07-21-matrix-notation.md %}
[matrix-calculus]: {% link _posts/2025-07-22-matrix-calculus.md %}
[yannick]: {% link about.md %}#who-are-you-again
[about-ml]: {% link about.md %}#who-is-it-for

[matrix-calculus-plat]: {% link _posts/2025-07-22-matrix-calculus.md %}#le-plat-de-résistance
[matrix-calculus-gradient]: {% link _posts/2025-07-22-matrix-calculus.md %}#least-squares-gradient-derivation
[matrix-calculus-precisions]: {% link _posts/2025-07-22-matrix-calculus.md %}#not-so-fast

[tldr]: #tldr
