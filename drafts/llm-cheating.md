# Title to be found.

<!-- Spoiler: this blog post is about saving the world. -->

It's 2026. AI exists. It has been capable of giving a reasonably good answer to pretty much any question I typically ask students in homework assignments for a few years.

So far, so good. Yay science!

But, there's a teeny tiny problem: students also know this.



## On homework assignments and why they're directly related to the imminent collapse of civilization

As it turns out, the objective of the homework assignments I give was never to provide *me* with the solution, as in principle, I already know it. It's not even really about evaluating the students either, although assignments *are* graded in my class.
No, the real objective is to ensure they think hard about interesting* problems, and learn things along the way.

<sup><sub>(*Yes, *interesting* indeed. Don't be too quick to shout out "neeerd", as I gently remind you that you are currently reading a machine learning blog).</sup></sub>

To use an analogy I'm fond of: I believe working hard on a problem is the intellectual equivalent of doing physical exercise to build muscles.
A sport coach may assign a 10km track run to a coachee as an exercise; the coachee may later show them the registered route in Strava/their favorite training app as evidence this was completed. But if the route was done using an electric scooter, the exercice becomes entirely pointless, as the objective was never to ensure that the track itself is run around.

Similarly, if current students don't do intellectual effort/training anymore, they won't build intellectual muscles. We will then have an entire generation of intellectual weaklings, our leaders will be (even more) incompetent (than now), and human civilization will collapse.
I might be slightly exagerating here, but honestly not that much.

So, as a (not so) humble teacher, what can I do to save the world?

There are a couple of immediate possibilities I could consider:
1. Completely remove homework assignments. This would be equivalent to stop making trainees do physical exercise altogether: see the previous part about the collapse of civilization.
2. Keep homework assignments, but stop grading them. Let's be honest, in practice this would be equivalent to proposition n°1. Civilization collapses again.
3. Continue grading homework assignments as I used to. Then students use AI. Civilization goes boom.
4. Book special slots to have students work on the homework assignments while under constant scrutiny. Well... I know I'm supposed to be concerned about civilizational collapse, but on the other hand I have a life outside of work, so I'd rather not do that.

So, none of these solutions is great.
I need to find a way to ensure students continue working on hard problems.

Conclusion: saving the world requires finding a way to ensure students continue thinking hard on problems.

<!-- There's an elephant in the (class)room that I somehow failed to address so far.
How do I know students use AI? Does civilization actually require saving? -->



## The (not quite) hopeless fight for AI detection

Conclusion: as of now, students do use AI. Reliable AI detection is sometimes possible but difficult.
(Rule later: probability of check is low, so fine must be high)



## Incentives, meta-incentives and the Grand [Unifying] of Students' Psychology

But first, another analogy!

Consider a public transportation network like the Parisian metropolitan. It's not free to operate, so metro tickets were invented.
As the hypothetical [leader of Paris metro], we could [be content with] asking people to please buy a ticket, as opposed to hopping on trains as free riders. But hum, yeah, I think you can see the limit with that approach.

Instead, we can create a system of random ticket checks, with fines for people who don't have a valid ticket.

This is where we enter the fabulous world of *rational agents** and *incentives*! [rainbow emoji and other emojis to represent agents/incentives? e.g. policeman, carrot and stick?]

Let's assume people want to minimize the average cost of using public transportation.

For a start, if caught fraudsters are simply made to buy a ticket, i.e. the fine is the price of the ticket, it is actually irrational to buy a ticket: cheating will never cost more than being honest, and will be cheaper every time one is not caught.
So in such a situation, we can expect people to continue not buying a ticket.

<details markdown="1">
<summary>On the existence of honest people, and economists</summary>

I am aware that the model above has its limits: for a start, it's *possible* that not everyone is fully rational, or reasoning in terms of expected cost. In particular, this framework completely excludes any moral consideration; in real life, some people will still buy the ticket regardless of any cost/benefit analysis, just because they believe it's the right thing to do.
Still, the above framework provides a useful simplification enabling us to reason about how people are likely to behave in different situations.

So, please don't force me to make this post longer than it already is, and please address any complaint about forgetting to account for the existence of honest people to economists instead.

</details>


In general, given a ticket price $t_p$, a fine price $f_p$ and a probability $p$ of getting checked, it becomes rational to buy the ticket if the corresponding expected cost (the price of the ticket) is less than the expected cost of cheating, i.e. if
$t_p < p \cdot f_p$.

If we want to increase the number of people paying their ticket, we have 3 levers:
0. Decrease the price of the ticket $t_p$. This has the obvious disadvantage of also decreasing revenue*, which may not be economically sustainable.
(*ignoring any effect of the price elasticity of demand on the ground that it is totally unrelated to the point I'm trying to make).
1. Increase the probability $p$ of ticket checks. One thing to keep in mind is that this lever also comes at a cost: in extreme cases, checking everyone all the time could end up costing more than what the tickets bring in, making the whole [business] unviable.
2. Increase the amount of the fine $f_p$. Probably what we should do here.

Right, I just remembered that I'm not actually [leader of RATP], I'm merely a teacher trying to save humanity from LLM-induced brainrot.

OK, so the goal of the agent in the previous example was to minimize the (expected) cost of using public transportation.
Can we also model students's goal to predict their behavior?

Behold, for after many years of studies, standing on the shoulders of giants like Maxwell unifying electricity and magnetism, I have been able to reduce the entirety of student psychology to this elegant equation:

<div class="silverhighlight" markdown="1">
A student's objective is to get the best possible grade $G$ while minimizing effort spent $E$.
</div>

(GASP)(link to spherical cow)

<details markdown="1">

<summary>"I have a complaint about this result!"</summary>

*sigh* Fine, let's make this blog post even longer, after all why not?

First, a few additional comments about this objective:

1. The most immediate remark I would expect from any of my students is to notice that it's a dual objective (we're trying to maximize/minimize 2 things at the same time, namely grade/effort), so we should probably specify a trade-off $\lambda$ between the two and write e.g.

$$
\text{maximize} G - \lambda E
$$

Another, equivalent way to look at this would be to state that given a maximum effort $E_{max}$ that a student is willing to dedicate to the class, they would like to maximize their grade:

$$
\text{maximize} G \quad \text{s.t. } E \leq $E_{max}$
$$

Or, that given a minimal grade $G_{min}$ that they would like to obtain (e.g. the one enabling them to pass the class or graduate), they would like to minimize their effort:

$$
\text{minimize} E \quad \text{s.t. } G \geq $G_{min}$
$$

All of these formulations are equivalent given the right choice of $\lambda$, $E_{max}$ or $G_{min}$. So if you agree with any of them, you agree with me.
You may want to have a look at [this post on constrained optimization] if this is not clear why. But I don't think it's entirely necessary to continue reading, so you may proceed if you want.
(and if you don't agree with any of them i.e. with me, then you're wrong - cf. disclaimer in the footer of the blog).

In addition, this trade-off varies from student to student, and is one of the main parameters explaning grade variance among students (along with initial familiarity with adjacent material and innate abilities).

So explicitly setting trade-off not interesting here, I'm mostly interested in the general idea.

2. A much more minor remark could be that this *might* be an oversimplification of student psychology.
For instance, it doesn't account for the fact that *some* students *might* actually be interested in learning for the sake of learning, not just as a proxy to get good grades.
However, I believe the previous hypothesis is a better heuristic to predict students' behavior than relying on an entirely hypothetical self-driven motivation to learn.

At least, *my* hypothesis explains pretty well why most students used to do graded homework assignments, used to *not* do *ungraded* homework assignments, and started using LLMs to do homework assignments when this became possible.

As precedently, I invite you to address any concern you may have to an economist.

</details>


Under this assumption, using LLMs to do homework assignments is entirely rational, as it enables to both get a better grade $G$ *and* spend less effort *E*. Even looks like a good couter-example to the No free lunch theorem.

And we shouldn't put the blame entirely on this generation of students: as a notorious procrastinator, I cannot guarantee that I would never have been tempted by an opportunity to play video games instead of working on some dull-but-imminently-due essay.

But, as we've seen, this still leads to the collapse of civilization, which most persons I know consider to be a bad thing.
So we still ought to do something about this, at the expense of fellow lazy video-game-enjoyers. Sorry.

Quick introspection:

What about MY objective?
Here I assume that my objective, and by extension *the teacher*'s (in a more abstract and generalized sense) objective is that students learn as much as possible, while also minimizing my own effort.

Same remarks as students objectives:
Many incentives other than making students learn exist (keeping their job/career progression, which may involve not going to war with administration, who themselves may have other incentives which may involve not failing half the students)...
Anyway, I think society's goal should be that teachers' goal is to make students learn as much as possible.

Or, even more generally, a functional society should have rules that incentivize indivuals to maximize common good.

But, for the sake of brevity I will refrain from talking about meta-incentives.
Also, selecting rules for the entirety of society may be slightly too ambitious for this blog post, so let's focus on classroom rules instead.

Good news: as the teacher, I AM the one setting rules in my class.

Thus, I should set rules such that while trying to achieve their goals, students will actually achieve MY objective. (Yeah, no more common good, just MY own goals 😈)

I.e., I should set incentives so that while trying to maximize grade with set amount of effort (or minimizing effort for given objective grade, or any other trade-off), students learn as much as possible.
While also keeping my involvement below a certain threshold (this will be important later).


