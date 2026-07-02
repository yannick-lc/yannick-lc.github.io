---
layout: post
title:  "AI will destroy the world (through homework)"
rendered_title: "AI will destroy the world (through homework)"
date:   2026-07-03 00:08:00 +0200
last_modified_at:  2026-07-03 00:08:00 +0200
categories: essay
permalink: /blog/ai-homework/
description: "AI may put an end to civilization, but not the way you think. It will be because of homework."
comments: true
---

{% capture em_dash %}
<span title='"An EM dash! This is an AI-written article, I knew it!" (Please read the link for further info.)'>[--][ai-disclosure]</span>
{% endcapture %}

{% capture em_dash_joke %}
<span title='This EM dash and AI pattern is actually meant as a joke. It was still written by me, sorry.'>[--][ai-disclosure]</span>
{% endcapture %}


It's 2026. Artificial Intelligence exists. Since ~last year, it has been capable of giving a reasonably good answer to pretty much any question I typically ask students in homework assignments.

So far, so good. Yay science!

But, there's a teeny tiny problem: *students also know this*.

<details markdown="1">
<summary>TL;DR (click me to expand)</summary>

<a id="tldr"></a>

*Don't want to read this whole article, but directly want the key points instead? Fear not, I've got you covered.*
<span style="font-size:60%;"> *(But if you disagree with any of the points below, I'm afraid you'll have to read the full article, if only to realize how wrong you are.)* </span>
<br/><br/>

<!-- <div class="goldhighlight" markdown="1"> -->

Thinking hard about challenging problems is to intellectual development what physical exercise is to building muscle: a necessary {{ em_dash }} if not always pleasant {{ em_dash }} endeavor.

Graded homework *used to* be a great way to ensure students did exactly this.
However, recent progress in AI has turned it into a convenient shortcut to a good grade, requiring very little effort.
Which is *precisely* the objective of students, according to the

<div class="silverhighlight" markdown="1" style="padding: 10px;">
<ins>Grand Axiom of Student Psychology (GASP)</ins>:
a student wants to get the best possible grade while minimizing effort spent.

</div>

This is a challenge for teachers, who pursue their own, somewhat conflicting objective:

<div class="silverhighlight" markdown="1" style="padding: 10px;">
<ins>Grand Objective of the Astute Lecturer (GOAL):</ins>
maximize students' learning while minimizing their own effort.
</div>

The "minimizing effort" part is not *purely* laziness: with 30+ students per teacher, there is only so much time a teacher can dedicate to each student.
To make matters worse, accurately estimating whether AI was used for a given question may not be practically feasible, due to a recent update to [Brandolini's law][brandolinis-law]:

<div class="silverhighlight" markdown="1" style="padding: 10px;">
<ins>Yayanini's law:</ins>
proving that a text is AI-generated is not just harder than generating it {{ em_dash_joke }} it's orders of magnitude harder.
</div>

The challenge is thus to design class rules that *incentivize students not to use AI for homework* {{ em_dash }} so that they keep learning {{ em_dash }} while *keeping the teacher's workload manageable*.

Some obvious ideas can be eliminated right away:
- **Completely removing homework assignments**: this throws away a valuable opportunity to make students think long and hard, which is difficult to recreate in other settings.
- **Penalizing detected AI use question by question**: this would require far more time than the teacher has available. And the low risk of getting caught on any single question may still make AI use rational from a risk/reward perspective.

A seemingly more reasonable option: **give the entire homework a grade of 0 upon any evidence of AI use.**

However, this rule may be hard to enforce in practice: caught cheaters have a strong incentive to deny accusations and waste the teacher's time, in the hope the teacher will eventually give up the fight.
A viable set of rules must both deter students from cheating, and ensure that arguing in bad faith remains a losing strategy for caught cheaters.

As a result, this is the deterrence doctrine I'm currently experimenting with:

<div class="silverhighlight" markdown="1" style="padding: 10px;">
Evidence of AI use on any part of a homework assignment warrants a grade of 0 for the entire homework.

A repeated offense warrants a failing grade for the entire course.

<div style="font-size: 80%;">
The teacher may opt for a more lenient approach at their sole discretion, with no obligation whatsoever.

<br/>

Accusations of AI use may be challenged by students who believe they were wrongly accused. Doing so will trigger a re-evaluation with a strict application of the official policy.

</div>
</div>


Whenever possible, such rules should be backed by matching university-level policies, so that sanctions can actually be enforced and deterrence remains credible.

<!-- </div> -->


</details>

## Homework assignments and the imminent collapse of civilization

As it turns out, the objective of the homework assignments I give was never to provide *me* with the solution since, in principle, I already know it. It's not even really about evaluating the students either, although assignments *are* graded in my class.
No, the real objective is to ensure students think hard about interesting\* problems, and learn cool\* things along the way.

<sup><sub>(\*Yes, *interesting* and *cool* indeed. Don't be too quick to shout "neeerd", as I gently remind you that you are currently reading a machine learning blog.)</sub></sup>

To use a metaphor I'm fond of: working hard on a problem is to intellectual development what physical exercise is to muscle building.
A coach may assign a 10km run to a student athlete, who later shows the GPS-tracked route as proof of completion. But if the route was covered by car, the exercise becomes entirely pointless: *the goal was never to trace a path on a map*.

Similarly, if current students don't put in intellectual effort anymore, they won't build intellectual muscles. We will then have an entire generation of intellectual weaklings, our leaders will be <sub><sup>(even more)</sup></sub> incompetent <sub><sup>(than now)</sup></sub>, and human civilization will collapse.

I might be slightly exaggerating here, but honestly not that much.

So, as a (not so) humble teacher, what can I do to save the world?
There are a couple of immediate possibilities I could consider to solve my AI problem:

1. **Completely remove these now obsolete homework assignments.** This would be equivalent to cutting trainees' physical exercise altogether: see the previous part about the collapse of civilization.
2. **Keep homework assignments, but stop grading them.** Let's be honest, in practice this would be equivalent to proposition #1. Civilization collapses again.
3. **Continue grading homework assignments as I used to.** Then students continue using AI. Civilization goes boom. 🏛️💥
4. **Book special slots to have students work on the homework assignments while under my constant scrutiny.** Well... while I *should* be concerned about civilizational collapse, I also have a life outside of work. So I'd rather not do that.
<!-- <sub><sup>(see [this part][goal])</sup></sub>. -->

None of these solutions is great.
To save the world, we must find a way to ensure students keep thinking hard about cool problems.



## The cat-and-mouse problem

There's an elephant in the (class)room that I didn't address yet: *how do I know students actually use AI?*

There are a few bodies of evidence.
First, based on the stellar quality of last semester's average homework: either I happened to have the brightest cohort ever by far, *or* many students used AI.
The average quality of the supervised, on-paper final exam was somewhere around *"meh"*. This tips the scales towards the latter hypothesis.

In addition, some students are *really bad* at covering their tracks. Subtle hints of AI use that I've seen in submissions include:
- Leaving the *"Your Name"* placeholder generated by ChatGPT/whatever.ai as-is instead of replacing it with their actual name.
- Keeping AI follow-up questions like *"Would you like further clarification?"* in the submission. No, I would not.
- Answering hallucinated questions that were never asked <sub><sup>(although they were sometimes good questions, so thanks for the suggestions!)</sup></sub>

<!-- I've compiled a list of additional real-life examples [here][ai-examples], for those who'd like to laugh/cry some more. -->

<details markdown="1">
<summary>Further evidence for the non-believers in the upcoming AI-pocalypse</summary>

*You may skip this part and continue reading* <span style="font-size: 80%;">if you're already convinced that students' use of AI for homework is indeed a problem.</span>
<br/>

I teach graduate-level classes at arguably the [best university in France][shanghai-ranking]. Even there, many if not most students are willing to take shortcuts to get a good grade if they think they can get away with it.
So I think it's reasonable to assume that this is true for almost all educational institutions, including middle and high schools.

One faint hope one might be tempted to cling to: my students are, after all, graduate students in the field of AI, and should thus have AI skills well above mere mortals'.
Let me shatter your dreams right here and now: using AI to cheat on homework doesn't require any skill more advanced than typing [chatgpt.com][chatgpt] in a web browser.

So this problem is unfortunately not restricted to my university or field of study.
As a matter of fact, similar situations have been reported at or by [Harvard][harvard-cheating], [Cornell][cornell-cheating], [Stanford][stanford-cheating], etc.

So, students' AI use really is on the rise. All right.

Is it really that bad though?
Or, does using AI to do homework actually impede learning?

I'm convinced this is true to some extent at least.

For a start, in my classes, there is an inverse correlation between the "AI-ness" of homework submissions and actual performance on the AI-free final exam.
Quite paradoxically, the best final exam results now tend to come from students with the worst homework grades. This used to be the complete opposite.

I know that correlation is not causation, and there may be confounding factors like intrinsic motivation, which influence both homework dedication and final exam result.
Still, I believe this counts as suggestive evidence that unchecked AI use actively impairs students' learning.

Moreover, even though this debate is fairly recent, studies suggesting that this is indeed the case are slowly [starting][mit-deskilling] [to emerge][pnas-deskilling].
A [recent study][nature-deskilling] in Nature argues that AI-induced "deskilling" affects not only students, but even established professionals.

So, there you go. Imminent civilizational collapse is coming.

</details>


The previous clues were left even though, at the beginning of the semester, I humbly inform my students that I 
- have a PhD in AI
<!-- - have been working and teaching in the field for 10+ years -->
<!-- - have been working with [transformers][transformer] since before [GPT1][gpt1] -- itself released 4 years before ChatGPT -->
- have been working with [Transformers][transformer] <span style="font-size: 70%;">*--the "T" in [ChatGPT][chatgpt-wiki]--*</span> since before [GPT1][gpt1] -- <span style="font-size: 70%;">*itself released 4 years before ChatGPT's 1<sup>st</sup> version*</span>
<!-- am a regular user of frontier models, -->
- am being paid (handsomely) to advise Fortune 500 companies on the latest AI developments

and that as such, maybe they ought to assume that I'm *somewhat* competent at detecting AI-generated content.

However, I have a confession to make: 
even for me, most situations are far from black and white.

There are many cases where I have strong suspicions that AI was used, without necessarily having conclusive evidence.
<!-- -- e.g. I would estimate the probability of AI-generation at 80%. -->
There are cases where I'm virtually certain that AI was used but still don't have evidence that would hold up in court.
And there are many situations where it is practically impossible to tell AI from non-AI.
<!-- -- e.g. answers to the question *"How much is 2+2? Answer using only a number"* -->
<!-- <sub><sup>(although questions on my assignments tend to be a bit more difficult than this).</sup></sub> -->

<details markdown="1">
<summary>What about AI detectors? Short answer: <b>they're not reliable.</b></summary>

<br/>

*Everything you need to know is stated in the title of this collapsible section.*

*You may now resume reading the main article.*

<!-- <div style="text-align: center;">...</div> -->
*...*
<br/>
<br/>

Still here? Fine, I'll elaborate.

<!-- First, to get it out of the way: even if we had access to a very reliable AI detector, this wouldn't solve the issue that many estimates are probabilistic by nature, and also couldn't magically determine whether the digit "4" was typed by an AI or a human. -->

Existing AI detectors can lead to both false positives and false negatives, as has been documented by [a][ai-detection-1] [number][ai-detection-2] [of][ai-detection-3] [studies][ai-detection-4].
But the strongest argument might be that OpenAI, the company behind ChatGPT, has notoriously [discontinued their own AI-detection tool][openai-detection-discontinued] because of its poor accuracy.

<!-- On the one hand, there are e.g. PhD thesis written well before AI-generated text [existed] which are detected as mostly AI.
This is because scientific writing style is somehow specific, and AI writing and human writing are fairly similar in this situation.
On the other hand, adding typos and gramar mistakes to AI generated text may be enough to fool AI detector (and occasionaly the teacher too, to be honest). -->

It's not that everyone at OpenAI and all the referenced AI-detection companies are incompetent: creating a foolproof AI detector is fundamentally doomed to failure, for [reasons outside the scope of this essay][ai-detection-impossible].

There are [horror stories][reddit-horror]* of students facing severe academic consequences because of false flags from AI detectors, despite being willing to prove that no malpractice occurred.
<!-- I hope we can all agree that this is not great for anyone. -->

<sub><sup>*I have no way of knowing how accurate this specific story is, but I have no doubts that similar situations did and will occur.</sup></sub>

So, the conclusion is: AI detectors alone should ***NOT*** be used as definitive evidence that a text was written by an AI or a human.

</details>

So, to sum up: students do tend to use AI for homework.
In rare cases, we can get conclusive evidence that AI was used to write at least part of the solution.
But in general, AI detection is unfortunately not practically feasible.

Are we cooked?


<!-- ## Incentives, meta-incentives and the Grand Axiom of Students' Psychology -->
## Incentives and the Grand Axiom of Student Psychology

<!-- Maybe, maybe not. -->

To find out, I'd like to go on yet another metaphorical journey. Since I live in Paris, journeys typically start with the Métro.
It's not free to operate, so metro tickets were invented.

Great (allegorical) news: we have just been appointed as BOSS (Behavioral Optimization & Sanctions Supervisor) of the metro. We are in charge of ensuring passengers actually buy a ticket, as opposed to hopping on trains as free riders.
We *could* simply ask people nicely to buy a ticket.
Although, maybe... well... Finding the limits of such an approach is left as an exercise for the reader.

OK, new brilliantly original idea: we could randomly check passengers' tickets, and impose fines on those without a valid ticket.

This is where we embark on an expedition into the fabulous world of *rational agents* and *incentives*! 🌈👮‍♂️🥕🪵

<!-- <sup><sub>(\*Really not talking about *AI* agents for now, although articles on this topic are coming. Stay tuned!)</sub></sup> -->


### Setting incentives like a BOSS

Let's assume passengers want to minimize their average cost of using public transportation.

For a start, if the fine is simply the ticket price, buying a ticket is actually irrational: cheating will never cost more than being honest, and will cost less whenever one is not caught.
So in such a situation, we can expect people to *not* buy a ticket.

<details markdown="1">
<summary>On the existence of honest people, and economists</summary>

I am aware that the model above has its limits: for a start, it's *possible* that not everyone is fully rational, or thinks in terms of expected cost.

In particular, this framework excludes any moral consideration. In real life, some people will *always* buy the ticket regardless of any cost/benefit analysis, simply because they believe it's the right thing to do. Others will *never* buy a ticket for various reasons.
Still, economists often use this type of framework as a useful simplification to reason about how people are likely to behave in different situations.

So, please don't force me to make this post longer than it already is, and please address all complaints about forgetting (to account for) the existence of honesty to economists instead.

</details>

In general, given a ticket price $t_p$, a probability $p$ of getting checked and a fine price $f_p$, it becomes rational to buy the ticket if the corresponding cost is less than the expected cost of cheating, i.e. if

$$
t_p < p \cdot f_p
$$

If we want to increase the number of people paying their ticket, we have 3 levers:
1. **Decrease the price of the ticket $t_p$.** This has the obvious disadvantage of also decreasing revenue, which may not be economically sustainable.
<!-- (*ignoring any effect of the price elasticity of demand on the ground that it is totally unrelated to the point I'm trying to make). -->
2. **Increase the probability $p$ of ticket checks.** One thing to keep in mind is that this lever also comes at a cost: in extreme cases, stationing a controller between every pair of stations could end up costing more than what the tickets bring in, making the whole operation unviable.
<!-- (Assumption: checks are manual; in practice, checks might be partly automated, but AI detection may not (yet)). -->
3. **Increase the amount of the fine $f_p$.** In practice, this tends to be the most practical option. With a small nuance though: $p$ and $f_p$ must remain reasonably balanced for the system to be socially acceptable. Saving costs by checking a single passenger per year, i.e. setting $p$ to 0.0001% while increasing $f_p$ to $5,000,000 to compensate would probably receive some backlash.

Right, my girlfriend just reminded me that I'm not the BOSS; I'm merely a teacher trying to save humanity from AI-induced brainrot.
Back to reality then.



### Introduction (and conclusion) to student psychology

So. The goal of the rational passenger in the previous example was to minimize the (expected) cost of using public transportation.
Can we also model students' goal to predict their behavior?

Behold, for after years of tireless field studies,
<!-- standing <del>on the shoulders of</del> *alongside* giants like Maxwell who unified the very forces of nature, -->
I have at long last succeeded in distilling the entirety of student psychology into this [elegant equation][spherical-cow]:

<div class="silverhighlight" markdown="1">
<ins>Grand Axiom of Student Psychology</ins> (GASP):

The objective of a student is to get the best possible grade $G$ while minimizing effort spent $E$.

</div>

<details markdown="1">
<summary><em>"This feels like a slight oversimplification. Yolo 67."</em> — a student</summary>
<a id="gasp-details"></a>

\**sigh*\* Fine, let's make this blog post even longer, after all why not?

So, a few additional comments about this objective.

**Firstly.** The most immediate remark I'd expect from any of my *good* students is to notice that it's a dual objective: we're trying to maximize/minimize 2 things at the same time, namely grade $G$ and effort $E$. So we should probably specify a trade-off $\lambda$ between the two and write our objective as e.g.

$$
\text{maximize}~~ G - \lambda E
$$

Another way to look at this would be to state that given a maximum effort $E_{max}$ that a student is willing to dedicate to the class, they would like to maximize their grade:

$$
\text{maximize}~~ G \quad \text{such that}~~ E \leq E_{max}
$$

Or, that given a minimal grade $G_{min}$ that they would like to obtain (e.g. the one enabling them to pass the class or graduate), they would like to minimize their effort:

$$
\text{minimize}~~ E \quad \text{such that}~~ G \geq G_{min}
$$

All of these formulations are equivalent given the right choice of $\lambda$, $E_{max}$ or $G_{min}$ (see [this post][pseudo-inverse] on constrained optimization if it's not clear why). So if you agree with any of them, you agree with me.
And if you don't agree with any of them, i.e. you disagree with me, then *you're wrong* -- cf. disclaimer in the footer of the blog.

In addition, this trade-off varies from student to student, and is arguably one of the main parameters explaining grade variance among students, along with initial familiarity with adjacent material and innate abilities.
So explicitly estimating this trade-off is not what I'm after here; I'm mostly interested in the general idea, and will thus omit the $\lambda$.

**Secondly.** A much more minor remark could be that this *might* indeed be an oversimplification of student psychology.
For instance, it doesn't account for the possibility that *some* students are interested in learning for its own sake, not just as a proxy to get good grades.
However, I believe the GASP hypothesis above is a better heuristic to predict students' behavior than relying on an entirely hypothetical intrinsic motivation to learn.

At least, *my* hypothesis explains pretty well why most students used to do graded homework assignments, used to *not* do *ungraded* ones, and started using AI once this became possible.

**Finally.** As before, I invite you to address any remaining concerns to economists.

</details>

Under the GASP assumption above, using AI to do homework is entirely rational, as it enables students to both get a better grade $G$ *and* spend less effort $E$.
<!-- Even looks like a good couter-example to the No free lunch theorem. -->
And we shouldn't put the blame entirely on this generation: as a notorious procrastinator myself, I cannot guarantee that I would never have been tempted to trade a dull-but-imminently-due essay for a few hours of video games.

<!-- But, as we've seen, this still leads to the collapse of civilization, which most of my friends consider to be a bad thing. -->
<!-- So we still ought to do something about this, at the expense of fellow lazy video-gamers. Sorry. -->
But, as we've seen, this still leads to the collapse of civilization.
Which is generally considered to be a bad thing,
<!-- which is inherently bad for video gaming. -->
so we still ought to do something about this.


### The teacher's side of the equation


OK, not to make this about me, but: what about *MY* objective?
<!-- Or by extension, what about *The Teacher*'s objective in a more abstract and generalized sense, for my entire being is merely reduced to a synecdochic incarnation of the whole teaching body in this essay. -->
Or more abstractly, what about *The Teacher*'s objective, for my entire being is merely reduced to a synecdochic incarnation of the whole teaching body in this essay.

Let me try to offer yet another brilliant distillation of human psychology:

<div class="silverhighlight" markdown="1">
<a id="goal"></a>
<ins>Grand Objective of the Astute Lecturer (GOAL):</ins>

The objective of the teacher is to maximize students' learning $L$ while minimizing their own effort $E$.
</div>

<sub><sup>Note: in this essay, we focus mostly on the "make students think instead of using AI" component of the learning objective, although there are obviously many other aspects to it.</sup></sub>

<details markdown="1">
<summary><em>"Are you implying that I'm lazy?"</em> — a teacher</summary>

**Firstly.** A more charitable phrasing of "while minimizing their own effort" could have been "while keeping their own involvement under a manageable threshold $E_{max}$" {{ em_dash }} as I hope everyone agrees that even teachers only have a finite amount of time to dedicate to their job. E.g.:

$$
\text{maximize}~~ L \quad \text{such that}~~ E \leq E_{max}
$$

But as discussed [earlier][gasp-details], given the right trade-off $\lambda$ or threshold $E_{max}$, these 2 formulations are functionally equivalent.

**Secondly.** We could waste time making the same remarks as for the previous students objective: teachers *may* have objectives other than making students learn.

Worse, though, is that some of these objectives may involve feeding their own family. Which may involve keeping their job, which may involve not going to war with the administration, who themselves may have yet more objectives such as e.g. keeping the university funded. Which may involve not failing half the students, which may involve not penalizing cheaters too harshly. So some of these objectives may actually be *opposite* to our stated GOAL, and it can get pretty complicated.

<a id="common-good"></a>
*However*, I believe a functional society should have rules that incentivize individuals to maximize the common good, which here would mean that one of society's goals should be that teachers' goal is to make students learn as much as possible.

But crafting rules for the entirety of society is slightly too ambitious for this blog post. So I will refrain from discussing meta-incentives further and try to focus on classroom rules instead.

**Finally:** talk to <del>the hand</del> economists.

</details>

There is one problem: the students' objective is somehow conflicting with my own GOAL, as learning typically requires effort. Which they'd rather not put in.

However, as the teacher, I have one ace up my sleeve: *I* set the rules in my class.

Thus, I should define rules such that while trying to achieve their objective, students will actually achieve *MY* goal.
<!-- <sub><sup>(yeah, no more [common good][common-good], just MY own goals now 😈)</sup></sub>. -->
That is, I should set incentives such that when trying to maximize their grade while minimizing effort, students will learn as much as possible {{ em_dash }} while also keeping my involvement at a manageable level.

<!-- Hopefully, this should involve them working on hard problems presented in HW assignments. -->

<!-- ## The first rule of ML101 and the first rule of command -->
<!-- ## 1<sup>st</sup> rule of ML101, 2<sup>nd</sup> law of Brandolini and 1<sup>st</sup> rule of command -->
## Rules and laws

For now, let's focus on incentivizing students to *not* use AI for their homework {{ em_dash }} in order to increase learning $L$ in case you haven't been listening.
We can capitalize on our past experience as BOSS: we still have 3 levers to increase the incentive to be honest.

1. **Decrease initial price.**
In our GOAL example, this would be equivalent to decreasing the difficulty of homework. Not an option.

2. **Increase probability of getting caught when cheating.**
As we've discussed, getting proof that AI was used for any specific question
<!-- -- or sentence, paragraph etc. depending on the context of the work --  -->
is often not feasible.
<!-- Checking all tickets all the time may cost more than what the tickets bring in; in the same way, conducting detailed investigations for each submitted answer to estimate whether it was AI generated may require more time than I have available for the entire course (and even then, lead to possibly mixed results). -->
   However, we can sometimes get proof that AI was used for *at least one question*, in the same way that one failed ticket check conclusively proves that *some fraud occurred*.
This way, even though the probability of getting (indisputably) caught for *any individual question* remains low, the probability of getting caught *at some point* becomes non-negligible.

3. **Increase the cheating penalty.**
One implicit justification for the fine is that if we have been caught cheating for one ride, we've probably been cheating for more rides. And we should make up for that.
Plus, as we've seen, small fines make it irrational not to cheat. To deter effectively, the cost of the penalty must thus be (much) higher than the cost of being honest.

As a direct consequence of points 2 and 3, I propose:

<div class="silverhighlight" markdown="1">
<ins>A first rule:</ins>

Evidence of AI use on any part of a homework assignment warrants a grade of 0 for the entire homework.
</div>

<!-- [Missing: annoucement and acceptance of the rule] -->

<details markdown="1">
<summary><em>"That's too harsh! Skibidi."</em> — a student again</summary>

Some students sometimes object to this rule for being too harsh -- typically, right after getting caught.

From experience, such students *will* demand to only be penalized for questions with overwhelming evidence of AI use, swear they did not cheat on the more ambiguous ones, and argue that the penalty is *totally unreasonable*.

Exactly like caught fare-dodgers will swear this is the first time in their life they forgot to buy a ticket, offer to simply buy one now, and find the fine *totally unreasonable*.

This is to be expected, and is not a reason to comply: as discussed, asking a fare-dodger to simply buy a ticket is totally ineffective as a deterrent.

</details>


One important comment: while devising this rule, we mostly focused on the 1<sup>st</sup> component $L$ of the GOAL.
But the 2<sup>nd</sup> component {{ em_dash }} keeping the teacher's workload reasonable {{ em_dash }} is *just as critical* for our solution to be viable.

In particular, there is an important asymmetry that must be taken into account: students and teachers are not on equal footing when it comes to the effort component of their respective objectives.
Before you call me lazy *(again)*: let me explain.

Up until not so long ago, crafting a solution to a homework problem
<!-- (an essay, a mathematical proof, a design, whatever) -->
took way longer than grading it.
This is why we can have classes of 30 students for 1 professor.
However, *conclusively proving that* or even *correctly estimating if* a solution is AI-generated may now take far longer than generating it.
This is obviously an issue: reversing the previous ratio and having 30 professors for 1 student is not realistic.

This is analogous to an idea called [Brandolini's law][brandolinis-law] or the *bullshit asymmetry principle*: stating something false takes seconds. Proving that it is false can take hours, days or weeks.
There is a severe asymmetry between liars and debunkers, or more generally between bad faith actors and good faith actors.

To account for the latest developments in the field of AI, I hereby suggest amending Brandolini's law with:

<div class="silverhighlight" markdown="1">
<ins>Yayanini's law:</ins>

Proving that a text is AI-generated is not just harder than generating it {{ em_dash_joke }} it's orders of magnitude harder.
</div>

<!-- [As a general rule, the time of the teacher is much more valuable than the time of the student (sorry students).] -->
Thus, it is paramount that the teacher-side effort to detect and penalize AI content remains tightly contained, lest the effort required becomes unsustainable, the probability of getting caught and penalized plummets, and civilization collapses.

Good news, for once: even taking this into account, the proposed first rule still holds up from a game-theoretic perspective.

To recap: the proposed class policy acts as a strong deterrent against AI use by making it unattractive from a risk-reward analysis (significant risk of getting caught, high cost to pay if so). This results in students hopefully doing homework the good old-fashioned way, namely, using their brain. Consequently, students learn more: $L \nearrow$.
And, should the need arise, identifying a single piece of evidence of AI use should remain manageable from a teacher's effort perspective. Consequently, $E \leq E_{max}$.

Therefore, this seems to be aligned with both components of the GOAL.
<!-- Among all the solutions that I have seen proposed, [the one above is one of the only ones] that accomplishes this. -->

<div style="text-align: center;">...</div>
<br/><br/>


Now, this begs the question: did I really need to write all this simply to justify why I have a strict no-AI rule in my class?

Well, first, very few of the solutions that I have seen proposed actually manage to handle both the $L$ and the $E$ components of the GOAL. So getting there wasn't *that* straightforward.
But as it turns out, there's still an insidious problem left. So this essay is not entirely finished yet. Sorry.


## Dura lex sed lex, but sadly not really

<!-- As I said, the teacher gets to set the rules in their class. Which makes them a commander <sub><sup>(kindof I guess? I dunno man, I'm just trying to make a transition here)</sup></sub>. And thus subject themselves to a different first rule: -->

As the person in command, the teacher is themself subject to a different first rule:

<div class="silverhighlight" markdown="1">
<ins>First rule of command:</ins>

Never give an order you know won't be obeyed.
</div>

Or, to be more specific to our setting: never make a threat you can't follow through on.

<!-- Why am I bringing up this so-called rule of command? Didn't we say earlier that reinventing society's organization was outside the scope of this essay? -->
<!-- Well, let me get there. -->

Here's the thing: I can promise you from experience that whatever your initial warnings and however harsh the promised sanctions, at least *some* students will think they are smart enough to cheat and get away with it.

So, in theory, the previous rule deters students from using AI; in practice, some of them will still try their luck.
And we're now forced to consider a scenario *that wasn't even supposed to happen!*

<details markdown="1">
<summary>What went wrong with our model?</summary>

We made sure that the expected cost of cheating is higher than the cost of being honest. Are cheating students irrational? Was our GASP hypothesis wrong?

Well, respectively: 1. not necessarily (although I do wonder sometimes), and 2. *certainly not*.
<!-- (you may reread this blog's footer as a reminder of what the most likely hypothesis is when someone disagrees with me). -->

In short: there is an *actual* probability of getting caught when cheating. And there is a *perceived* probability, which may differ.
If the perceived probability is erroneously estimated to be lower than the actual probability, cheating might still *look* like the rational choice.

As it turns out, people in general are pretty bad at estimating probabilities (a post about that should be coming soon). And I've been told that students are supposedly people.

By the way, one alternative strategy could be to increase deterrence by focusing on perceived probability, i.e. making students *believe* they will get caught if they cheat -- even if that's not necessarily the case.
At least, this would be a sound strategy for someone who is not blogging about it.
For my part, I'll stick to the standard strategy to increase the perceived probability, which is to increase the actual probability.

Finally, let's not be too proud of how much better we are than these students who fancied themselves smart enough to cheat.
Because to be honest, maybe some of them are.
We only know of students whose risk estimate was off: from our point of view, all students whom we know cheated were clumsy enough to get caught.
But this is [survivorship bias][survivorship-bias].
We simply don't know about the ones who cheated and did not get caught. From all we know, this could very well be *all the other students* -- although I certainly hope not.

<div style="font-size: 70%;">
I actually have good reason to believe at least some of the submissions I received were written by humans, because they contain typical (cute) student mistakes, jokes, etc. Either that, or these students are expert manipulators. I guess we'll never know.
</div>

</details>

<!-- Why is this an issue? After all, students were warned; some cheated anyway, got caught and are now simply facing the consequences. -->

<!-- <div style="color: red; font-size: 50%;">
As we've seen, large asymetry time wise.
Assuming that students and the teacher value their *own* time about the same (since each of them have a budget of around 24 hours a day, to spend as they see fit).
From a class organization perspective,
An hour of teacher's time is supposed to be (much) more valuable than an hour of student's time, because there are 30 students while there is only 1 teacher.
To make things worse, the tyranny of Yayanini's law [somethign something], because proving a solution was AI-generated may prove to be much more time consuming than generating it.
[amplifies the issue]
</div> -->

<!-- In particular, I believe it is necessary to take the following into account: . -->

Why is this an issue?
<!-- Well, we've seen that when considering the effort component of the students' and teachers' conflicting objectives, the scales can tip heavily against the teacher, because -->
Well, we've seen that the effort component of the students' and teachers' conflicting objectives is heavily asymmetric and tipping against the teacher, because 1. there are more students than teachers and 2. proving misconduct may take longer than misconducting.
Yet, even facing the tyranny of Yayanini's law <sub><sup>(yes, that's a thing now)</sup></sub>,
<!-- we managed to propose a rule that should keep the required effort under control. -->
we managed to keep the required teacher-side effort under control.

Until now.
Because when a student is caught, this dual effort asymmetry is compounded by yet another asymmetry, this time in terms of personal stakes.

<!-- For a student, the personal impact of crossing the passing/failing grade boundary is enormous. As a result, failed students have a huge incentive to spend time disputing accusations and challenging the validity of the (agreed-upon) rules, even in bad faith, if it has a chance to improve their grade.
For the teacher, ensuring that an undeserving student fails the class is worthwhile, but not nearly as immediately and personally consequential.
So given their GOAL, the teacher has only so much energy they are willing to spend on this. -->
For the teacher, ensuring that an undeserving student fails the class is worthwhile, but not nearly as immediately and personally consequential as for the affected student, for whom the impact of crossing the pass/fail boundary is enormous. As a result, failed students have a huge incentive to spend time disputing accusations and challenging the validity of the (agreed-upon) rules, even in bad faith, if it has a chance to improve their grade.

Wasting the teacher's time is not simply collateral damage here. It may be the entire point of this deliberate attrition war, based on the hope that the enemy (a.k.a. *me* in this instance) will eventually give up due to lack of energy.

<div style="font-size: 70%;">
To be clear, this whole situation is <em>not</em> purely hypothetical: despite making the no-AI rule and its consequences clear from the start, I still had to waste a <em>lot</em> of time dealing with peevish cheaters.
It even got to the point where it felt tempting to write <em>a whole damn*d essay</em> about this, can you imagine?
</div>

<details markdown="1">
<summary>It gets worse (of course it does).</summary>

As if the situation was not tricky enough already, this problem is further compounded by additional factors:

1. The time required to handle disputes is evidently multiplied by the number of affected students: more disgruntled cheaters, more time wasted.
<!-- The rewarding part of my job is not to spend dozens of hours arguing why a few students should not pass the class. It is certainly not the reason why I started teaching. -->
2. Cheating is not necessarily binary: there are degrees to which students cheat.
From personal experience, many students will cheat at least *a little*. Fighting 10 hours to fail 1 student whose submissions are 100% AI-generated is one thing -- fighting 10 hours *each* to fail 20 students who cheated on 10% of the homework is another.
3. Cheaters who have nothing to lose may try to drag the school administration into their war, particularly if they represent a non-negligible fraction of the class. This (infuriatingly effective) strategy may result in further time wasted having to justify decisions. Again, I speak from experience.
<!-- This further wastes time, and increases the risk that the fight is ultimately deemed not worth it. -->
<!-- giving up and not failing some students. -->

It gets even better though -- and by "better", I mean "significantly worse" of course.
There are also psychological factors which may serve as tempting excuses to end the war.

{:start="4"}
4. The cost of errors in AI detection is highly asymmetric: as a human with *some* degree of empathy, I tend to consider that unfairly punishing an honest student is worse than being somewhat lenient toward a cheater.
5. There may oftentimes be uncertainty remaining regarding the reality of AI use. This can make it tempting to convince oneself that we end up passing undeserving students because we cannot be *absolutely sure* they cheated, while the real reason was actually to minimize effort.

</details>

<!-- So, detecting and punishing cheaters may be initially cheap. But handling the consequences may not be. -->
<!-- Thus, if the time required to effectively enforce the promised sanction becomes too high, we run the risk that the teacher estimates that [this issue] is not worth it, and turns a blind eye to the [issue]. *Just this one time.* -->

If enforcing the promised sanction becomes too costly, the teacher may decide it's simply not worth it, and end up turning a blind eye. *Just this one time.* *Pinky promise.*

Which is of course *bad* for a number of reasons. In particular:
<!-- knowing there is a significant chance to get a lenient treatment when being sufficiently annoying and time consuming obviously incentivises future cheaters to [do just that][tantrum].
This then further increases the time that needs to be dedicated to the issue, further increasing the likelihood of just giving up, and so on.
Worse, this also has the effect of decreasing the expected cost of getting caught, thus increases the expected reward for cheating.
This may then lead to more students cheating, spending more time arguing in bad faith, wasting even more time for the teacher, thus increasing leniancy, thus further decreasing the expected cost of cheating and so on and so on. -->
knowing there is a reasonable chance of getting lenient treatment by being sufficiently annoying obviously incentivizes future cheaters to do just that. This further increases the time the teacher needs to dedicate to the issue, further increasing the future likelihood of giving up. Which in turn lowers the expected cost of cheating, encourages more students to cheat, and so on.

As a consequence: civilization 💥.

So, detecting and punishing cheaters may be initially cheap, but handling the consequences may not be. Which makes our meticulously crafted previous rule moot.


## Qui vis pacem para nuclear bellum

### Skirmishes and nuclear war

I'll let you in on a secret: in practice, here is what I do.
If there is significant evidence of at least *some* AI-generated content, I grade based on my own estimate of what is AI and what is not.
For example, the ~50% of the homework I estimate is AI-generated gets a 0, and the rest I grade normally albeit a bit more harshly than usual.
In particular, all AI-suspected questions are marked as "AI-generated" by default.

<details markdown="1">
<summary>To my current students: a friendly <del>threat</del> note</summary>

Dear Student,

You somehow managed to learn one of my secrets. Well done.
<!-- Very well done. -->

However, allow me to offer a friendly warning: it would be unwise to assume that I will continue to use this exact grading scheme.
<!-- Nothing, absolutely *nothing*, requires me to do so. -->
Nothing requires me to do so.

<!-- I may change my mind tomorrow. I may have changed it already. -->
I may change my mind at any time.
And when I do, I may not feel any particular need to update my blog.
Should that happen, I am afraid there will be precisely nothing you can do about it.

<!-- I truly hope you shall be wise enough to keep assuming that a single trace of AI may earn you a nice, round zero. -->
<!-- It is the safest assumption you have. -->
Your safest bet is to keep assuming that a single trace of AI will earn you a nice, round zero.

<!-- I have the high ground. Don't try it. -->

With pedagogical affection,

<!-- Your Benevolent Teacher -->
Your Teacher

</details>

One advantage is that I don't need to justify each deduction individually, or prove AI use for each question, which as we've seen isn't feasible.
So the effort component of the GOAL is safe. There is also reasonable incentive for the students to *not* use AI, as it is still likely to result in a bad grade.

However, in these aspects, it's not really better than the previous rule. It's even a bit worse in terms of incentives.

<!-- The thing is, I also include two additional changes to the previous policy: -->
<!-- What I didn't tell you is that I also surreptitiously included two changes to the previous policy: -->
<!-- - The official policy is updated so that repeated cheating now warrants a failing grade for the entire course. -->
<!-- This serves to strenghten deterrence, which was slightly weakened by the more leniant approach to grading. -->
There is a catch, though.
*If* there is any dispute about the grade, particularly about the extent of AI use, I roll back to the previous strict policy: mere suspicion of AI use is not penalized, but one indisputably proven AI sentence results in an automatic 0.

<!-- Most cheaters know this is likely to result in an actively worse situation -- at least, that's been the case for all the ones I've encountered so far. -->
The whole idea is that arguing in bad faith is no longer a winning strategy for caught cheaters. On the contrary, it is likely to make things actively worse for them.

<details markdown="1">
<summary>What about students who used AI for 100% of the assignment? <em>(spoiler: new rule)</em></summary>

It is true that cheaters who, by my estimate, did 100% of an assignment with AI continue to receive a 0. As such, they may still be tempted to be a pain in the nether regions.

The same idea as before applies: ensure that even these students have something to lose if they try to push it. So that they hopefully don't.

This can get tricky though: enabling grades of *less than zero* would be handing them the stick to beat you with if they decide to escalate to the school administration.
A rule stating that one conclusively proven AI sentence warrants failing *the entire course*, as opposed to a single assignment, might seem more defensible. But they could call your bluff:
why didn't you fail *all* students with traces of AI in their submission? And why is there a difference in treatment if they're the only ones affected? We're back to square one.

Instead, I can suggest this fair middle ground: a repeated offense -- i.e. more than one homework assignment positively containing AI content -- warrants a failing grade for the entire course.
This seems reasonable enough to be accepted by everyone, school administration included.
And it ensures you have enough leverage to deal with any given student acting in bad faith *at most once*.
<!-- This is partly why the rule on repeated offense was introduced: even though their homework grade cannot get any lower, their course grade still can. Which should act as a strong enough deterrent. -->

Anyway, from my experience, students who do *all* homework with AI tend to have such abysmal results on the supervised final exam that convincing anyone why they should fail the class is not really difficult.
One alternative strategy I've used in the past for such students is to offer to skip the whole what-is-AI-and-what-is-not debate: that is, to base the course grade solely on what can confidently be attributed to them, namely the final exam. In practice, this has the same effect on the pass/fail decision anyway.

<!-- Such students were not the main reason why the rule was updated anyway. -->
</details>

Here is a summary of the full updated policy:
<div class="silverhighlight" markdown="1">
<ins>Updated nuclear doctrine:</ins>

Evidence of AI use on any part of a homework assignment warrants a grade of 0 for the entire homework.

A repeated offense warrants a failing grade for the entire course.

<div style="font-size: 80%;">
The teacher may opt for a more lenient approach at their sole discretion, with no obligation whatsoever.
<br/>

Accusations of AI use may be challenged by students who believe they were wrongly accused. Doing so will trigger a re-evaluation with a strict application of the official policy.
</div>
</div>

I believe this set of rules is both reasonably fair and effective.

Incidentally, the fine print of the policy may not even need to be official. So far, no one has complained that I was too generous with their grade.
But you never know.

The main advantage of this approach is that I don't *need* to give a 0 to all students who cheated "just a little" in order to maintain a credible threat {{ em_dash }} which as discussed would be hard to enforce in practice.
I have more gradual responses than a full-on nuclear war at my disposal:
<!-- But I also now have a weapon even more destructive than before. -->
similarly to real life, my nuclear arsenal exists to hopefully never be used.
However, if provoked, I still *can* order a swift and decisive strike, which is essential for deterrence to be effective.

<sub><sup>
As a reminder for international students and in all seriousness, [French nuclear doctrine][french-nuclear] provides for the possibility of a limited nuclear strike as a warning shot. You've been forewarned.
</sup></sub>

<!-- As a side note, the part of the doctrine written in a smaller font may not even need to be official.
In case of emails seeking to discuss the perceived unfairness related to the harshness of AI use penalization,
copy-pasting from an email template suggesting that further discussion on this topic will result in a strict application of the official policy has proved sufficiently effective to quickly shut down any time wasting debate.
And so far, no one has issued a formal complaint about me being too generous with the grades I give compared to what they should be according to official class policy.
But you never know. -->

<!-- <details markdown="1">
<summary>The previous idea still didn't work though. Why should this one?</summary>

We already assumed students were rational before, with little success.

Short answer: cheating was likely caused by miscalibrated probability estimates.
Knowing they've been caught and punishments are applied leads to swift re-evaluation of probabilities/priors whatever.
Now posteriors are (ideally) more closely aligned to truth, and rational behavior matches what I want.

At least been true empirically until now.

</details> -->

### Amendments, case law and the Geneva Convention

So, my deterrence metaphors went from fines in the metro to nuclear Armageddon. Boy, that escalated quickly.

Fortunately, we're pretty much done. Before I conclude, here are just a few clarifications I would like to emphasize.

<!-- The only way I see to escalate this further would be Eternal Hell, but even I would consider this to be a bit harsh. -->
<!-- I would like to emphasize just a few clarifications. Don't worry, I promise we're almost done. -->

<details markdown="1" open>
<summary><b>The applicable policy must be clearly announced.</b></summary>

Quite obviously, students need to know the rules from the start and accept them, even implicitly -- taking the class may count as acceptance.
After all, a deterrent is only effective if people know about it.

Having the rules plainly written also makes enforcing sanctions easier should the need arise. Trust me, I've been there.

<!-- I don't think any country has secret nuclear weapons they will only reveal by using them if attacked, as this would defeat the entire concept of nuclear deterrence. -->
<!-- Entire point of the rule is not to be mean to students and give bad grades (might be surprising to some, but this is not the main reason why I'm doing this job), it's to align incentives. This does not work if rule is not clearly announced. -->
<!-- (Same for metro ticket: if we ask people to pay for ticket but don't tell them that there is a fine if they don't, we can't be surprised if e.g. 80% don't actually buy one. This is also opening the door wide open to massive contestation.) -->

</details>



<details markdown="1" open>
<summary><b>Dispute of AI accusations must be possible.</b></summary>

As far as I know, I've never wrongly accused anyone of cheating:
so far, a grand total of zero students I accused have claimed to be fully innocent.
Even then, since no one is 100% infallible, I guess we should contemplate the possibility that [I am no exception][categorical-imperative].
<!-- Because Kant's [categorical imperative][categorical-imperative], blablabla. -->

Thus, the possibility of appeal is essential.
We just need to ensure that only *unfair* accusations are worth challenging, in order not to waste everyone's time -- and by everyone's, I mean *mine*.
I believe the proposed system is already fairly efficient in this respect.

<details markdown="1" style="background-color: #ffffff;">
<summary>Yeah, but what if there is an appeal though?</summary>

Right: what happens if there *is* an appeal? To avoid any unfair outcome or the re-emergence of misaligned incentives, it is imperative that the appeal determines whether AI was used as accurately as possible.
As a result, it may be worth dedicating significantly more resources than usual. If the proposed policy is effective, this shouldn't happen too often anyway.

If the evidence of AI is deemed already strong: I suggest asking for a second opinion from a neutral third party, briefed on the fact that one strong piece of evidence is all that's needed.

If there was doubt from the start or the third party cannot conclusively estimate whether the submission contains AI,
I suggest organizing an oral examination.
From experience, if a student did not write their submission themself, it is fairly easy to poke holes in their solution by asking them to clarify certain concepts that I suspect they may not be familiar with.
For example, what do they mean by suggesting to use [Platt calibration][platt-calibration]? Or if they proved that a function was a kernel using [Mercer's theorem][mercer-theorem], can they briefly explain what this theorem states?

The specifics will of course vary by subject, but the general idea should hold.

<div style="font-size: 70%;">
The example questions above are drawn from real-life oral defenses, though not related to AI-use disputes. In both instances, the unfortunate student had no idea what these concepts were about.
<br/>

</div>
<br/>

Ideally, the student should have little notice about this oral exam.
After all, they should already be familiar with the material they allegedly produced.
To ensure the oral defense is as unbiased as possible, it can also be conducted by or in the presence of another teacher.

Although establishing guilt is the responsibility of the accuser (a.k.a. me), the student should also be given an opportunity to present evidence in their favor: for instance any draft, notes, or intermediate version worth considering, provided it couldn't easily have been forged after the accusation.

If, after this due diligence, the use of at least some AI is established: the official policy is applied, resulting in a grade of 0, and possibly further sanctions.

If not: well, there may have been a mistake after all. This is a great opportunity to learn what went wrong with our assumptions, and to update our AI detection skills accordingly.

(But to reiterate, I've never been in this situation thus far.)

</details>

</details>


<details markdown="1">
<summary><b>The proposed policy can be most effectively applied if there is at least one strong piece of evidence.</b></summary>

In other words, accumulating weak evidence of cheating may not be sufficient.

This is for two reasons: first, not having conclusive evidence would risk getting dragged into challenges one may not win, thus undermining the perceived risk of cheating.
Besides, not having conclusive evidence would also risk unfairly penalizing an honest student for cheating, something I -- surprisingly -- do not wish to do.

</details>


<details markdown="1">
<summary><b>Any use of AI for legitimate reasons must be strictly disclosed.</b></summary>

There may be cases where using AI is legitimate and does not hinder learning given the context of the class.

One example from my class would be plotting graphs with [Matplotlib](https://matplotlib.org/), which can be notoriously tedious, and doesn't teach you much to be honest.
Time saved on this menial task may be better spent on learning more relevant concepts.

Depending on specific class policy, partial AI use may thus be occasionally tolerated, provided that its scope is explicitly disclosed.
Failure to disclose AI use and its exact scope must be interpreted as cheating.
This measure is necessary to avoid leaving the door open to post-hoc excuses.

<span style="font-size: 90%;">(As a token of good faith, I would like to disclose that [I did use AI][ai-disclosure] to proofread this article).</span>

However, allowing even some AI use may also be a double-edged sword.
In particular,
<!-- however convenient it may be, -->
I would not advise allowing AI for formatting or rewording in general, since it would make it basically impossible to separate its use for form from its use for substance -- and thus to prove its illicit use for the latter.

</details>


<details markdown="1">
<summary><b>On-paper exams should be included whenever possible.</b></summary>

This one should go without saying.

Even though they are arguably out of the scope of this essay, I believe having supervised, on-paper examinations is more important now than ever, for several reasons:
- First and quite obviously, this remains the only reliable way to measure student performance. Ensuring students meet a minimum ability threshold (different from the ability to coast through thanks to their AI buddy) is essential if we want diplomas to mean anything.

  I'm not planning to stop bragging about my [PhD][phd] anytime soon, so please make it retain its value. (Did I mention that I have a [PhD][phd]?)

- Since cheating at a supervised exam remains much more difficult, one of the easiest ways to obtain a passing grade is to actually learn the material that will be needed for the exam. Which, as a reminder, is what we would like the students to do as per the GOAL.

- As a bonus, exams are useful to "recalibrate" our internal AI detectors: if a student consistently turns in perfect assignments that don't look like AI, but dramatically blunders the final exam... it's possible something fishy was going on after all. And vice versa. This is an opportunity for the teacher to find out what went wrong and learn from it.

</details>


<details markdown="1">
<summary><b>If accusations of AI use have not been formally challenged, the evidence that led to the accusation need not be provided.</b></summary>

This hopefully should *not* discourage honest students from speaking up if they believe there has been a mistake.

But not knowing the extent of the evidence makes it difficult for dishonest students to estimate their chance of winning a bad faith argument with high stakes, ideally discouraging it.
In a way, this is the fog of war working in our favor for once.

Also, the last thing I want to do is to help students get better at cheating by "learning from their mistakes".
I'm the *only one* allowed to learn from mistakes related to this topic.

</details>


<details markdown="1" open ontoggle="this.open = true">
<summary><b>The teacher must retain full liberty to apply the full range of sanctions if (even limited) use of AI is formally established.</b></summary>

This final one is probably the most important.

I won't rehash why this matters from an incentive and effort perspective.
I would however like to emphasize that unconditional support from the university is critical. Having to fight the administration to fail a student for (proven) AI use would undermine everything we've been trying to build here.

In particular, I believe that strict, *official* rules regarding academic integrity which explicitly cover AI content would be a valuable addition to existing university policies.
Most American universities already had such rules about plagiarism when I was studying there: instances of proven plagiarism could go as far as getting you expelled. These rules had to be unconditionally accepted by all students.
I think this idea should be extended to unauthorized AI use and rolled out to more universities or schools in general, including in France.

<span style="font-size: 90%;"> *[**Update**: some universities such as [Oxford][oxford-ai-policy] or [Stanford][stanford-ai-policy] have started implementing such a policy.]* </span>

It is true that such rules may sometimes be genuinely painful to enforce: there is no denying that failing 20% of a cohort is extremely unpleasant for everyone involved.
However, I believe the alternative (🏛️💥) is even worse.

</details>



<!--
<details markdown="1">
<summary>On justice and society</summary>

I'm gonna briefly break my promise of not trying to reorganize society at large.
Sue me. This is *my* blog after all.

(Same rule is sometimes applied to other fields: immediately accepting and paying fine may result in smaller fee, reducing incentives to be an ass about it and waste everyone's time. Imo this approach should be generalized much more broadly: i.e. not having immediately recognized a fault which is later proven to have occured should have significant deterrent, as I think this would help to greatly shorten judicial procedures. But this is kinda outside the main topic).

From a game theoretical and utility maximization point of view,
So I don't really understand the point of having the right to remain silence.
Same for not knowing the 

I believe it would be much more efficient if everyone was incentivized to be honest, knowing there might be consequences for not doing so.

There are things I may miss though.
I'd be glad if someone could clarify if that's the case.

However, having no background in law or behovarial psychology in spite of my grand claims, maybe I am [naively mistaken].

</details>
-->


## Final dispatch

<!-- Congrats, you made it to the end! A summary of the main points is available at the beginning of the article. -->

Many of the ideas from this essay were introduced with my own classes in mind, but should be applicable much more broadly.

Some adjustments to different classes are straightforward: you may e.g. easily replace "answer to a homework question" with "part of an essay" depending on the context.
<!-- The scope and severity of the proposed sanctions can similarly be adapted to fit a different setting. -->
Other transpositions may not be so seamless, particularly everything related to AI detection.
Here, I'm afraid I have significant advantages over almost all other contexts:
I have a directly relevant background, and detecting AI in code is arguably much easier than in other submission formats.
<!-- Or maybe I'm just deluded -- although in this context I'd almost like it be the case. -->
Unfortunately, I don't yet have a universal solution for AI detection and sanction adaptation.
<!-- This will need to be evaluated on a case by case basis, although I believe the overall approach remains broadly relevant. -->
<!-- I experimented with variations of previous policies, but just started with the latest one. I'll let you know how it goes. -->

<details markdown="1">
<summary>I'm working on it though</summary>

I can actually almost pretend that I'm making progress: I am currently experimenting with possible "AI traps" in future homework assignments. The idea is to design questions so that an AI, while answering, generates subtle telltale patterns, constituting irrefutable proof of AI use if found.
This is still a work in progress for now, but if it bears fruit, I will update this post accordingly.
Stay tuned!

</details>

Finally, please bear in mind that I am *not* saying that AI has *no place at all* at work or in universities, or that we should ban computers altogether and write with quills and parchment instead.
On the contrary, AI can be a fantastic tool for learning, allowing self-driven students to benefit from individual tutoring, tailored explanations and detailed feedback {{ em_dash }} things that traditional teachers unfortunately can't offer to everyone, through no fault of their own.
I also believe that all <del>students</del> *humans* would benefit from at least a basic understanding of how AI works and how to use it effectively.

However, there is a time and place for everything.
Copy-paste is a tremendously useful invention {{ em_dash }} but using it to turn in a Wikipedia article as-is instead of an expected thorough reflection on a given topic is dishonest and educationally harmful.
The same goes for AI.

<!-- As a tangential note: -->
<!-- On a related topic -->
<!-- To hammer my point: as part of my work, I see people using AI more and more in large companies. -->
Incidentally, I also see problems related to uncritical reliance on AI at work.
Some people do use it fruitfully, while others use it to avoid a week's work by presenting slides visibly copy-pasted from ChatGPT, with no critical thinking whatsoever.
It might be argued that, since the latter group brings about as much value as a ChatGPT subscription but typically costs way more, there are big savings just waiting to be made.

Therefore, *training students to belong to this group is not helping them.*

Beyond that, keeping the ability to think, write, and perform other intellectual tasks by oneself is valuable in its own right.
As a case in point, writing this article [by hand][ai-disclosure] has greatly helped me clarify my thoughts on this matter, something that would not have happened had I delegated the task to an AI.

So, let's keep on thinking for ourselves!

<!-- ## Appendix -->

<!-- [Side bonus: using this approach and assuming teacher is not too bad at detecting AI, the grade reflects the actual effort/learning that took place.
So students are incentivized to maximize learning to maximize grade. This is exactly what we want.]    -->

<!-- Oxford agrees that efforts are better spent on deterrence than detection. -->

<!---
Left to do:

Include more examples of obvious AI use patterns.
Link to post about people in being bad at estimating probabilities.

-->

[pseudo-inverse]: {% link _posts/2025-07-24-pseudo-inverse.md %}
[ai-examples]: https://todo.com <!-- TODO -->
[ai-disclosure]: {% link about.md %}#do-you-use-ai-to-write-your-posts
[phd]: {% link about.md %}#who-are-you-again

[common-good]: {% link _posts/2026-06-16-ai-homework.md %}#common-good
[goal]: {% link _posts/2026-06-16-ai-homework.md %}#goal
[gasp-details]: {% link _posts/2026-06-16-ai-homework.md %}#gasp-details

[spherical-cow]: https://en.wikipedia.org/wiki/Spherical_cow
[brandolinis-law]: https://en.wikipedia.org/wiki/Brandolini%27s_law
[categorical-imperative]: https://en.wikipedia.org/wiki/Categorical_imperative
[force-dissuasion]: https://en.wikipedia.org/wiki/Force_de_dissuasion
[platt-calibration]: https://en.wikipedia.org/wiki/Platt_scaling
[mercer-theorem]: https://en.wikipedia.org/wiki/Mercer%27s_theorem
[transformer]: https://en.wikipedia.org/wiki/Transformer_(deep_learning)
[gpt1]: https://en.wikipedia.org/wiki/GPT-1
[chatgpt-wiki]: https://en.wikipedia.org/wiki/ChatGPT
[survivorship-bias]: https://en.wikipedia.org/wiki/Survivorship_bias
[french-nuclear]: https://en.wikipedia.org/wiki/Force_de_dissuasion

[stanford-cheating]: https://ed.stanford.edu/news/what-do-ai-chatbots-really-mean-students-and-cheating
[harvard-cheating]: https://www.thecrimson.com/article/2026/4/24/students-ai-usage-by-the-numbers/
[cornell-cheating]: https://news.cornell.edu/stories/2026/05/widespread-ai-misuse-means-higher-ed-must-rethink-assessment

[nature-deskilling]: https://www.nature.com/articles/d41586-026-01947-1
[mit-deskilling]: https://www.media.mit.edu/publications/your-brain-on-chatgpt/
[pnas-deskilling]: https://www.pnas.org/doi/10.1073/pnas.2422633122

[ai-detection-1]: https://www.cell.com/patterns/fulltext/S2666-3899(23)00130-7
[ai-detection-2]: https://link.springer.com/article/10.1007/s40979-023-00146-z
[ai-detection-3]: https://arxiv.org/pdf/2303.13408
[ai-detection-4]: https://www.sciencedirect.com/science/article/abs/pii/S305047592600093X
[ai-detection-impossible]: https://arxiv.org/abs/2303.11156

[openai-detection-discontinued]: https://decrypt.co/149826/openai-quietly-shutters-its-ai-detection-tool
[reddit-horror]: https://www.reddit.com/r/tech_x/comments/1trs1bt/new_york_university_student_spends_6_months/

[stanford-ai-policy]: https://news.stanford.edu/stories/2025/10/academic-integrity-working-group-generative-ai-exam-policies
[oxford-ai-policy]: https://libguides.bodleian.ox.ac.uk/using-ai-to-support-academic-work/university-policies

[shanghai-ranking]: https://www.shanghairanking.com/institution?n&r=France
[chatgpt]: https://chatgpt.com/
