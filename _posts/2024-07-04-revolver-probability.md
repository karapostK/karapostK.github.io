---
layout: post
title: Probability and Survival 
date: 2024-07-04 08:57:00-0400
description: Answering a simple probability riddle with some code
tags: code, probability
categories: code
giscus_comments: true
related_posts: false
---

Recently I got an quiz as first step for a ML interview. I had 40 questions over several aspects of Machine Learning, Deep Learning, Probability, and simple Practical Intuition for Model Training/Evaluation.
I had 1 minute each for each question so I was pretty under time constraints. However there is a riddle in the interview that stuck with me:


You are given a revolver with six slots. There are two adjacent bullets. You have to
shoot twice and are given the chance to rotate the cylinder randomly in-between. How
do you maximize your chance of survival?

- [ ] Rotate cylinder
- [ ] Do not rotate cylinder
- [ ] It does not matter, as the survival chance is the same in both cases
- [ ] The question does not give all information required to answer the question

Under pressure I selected to rotate the cylinder. After all, it generally makes sense. You reset your chances after you do the first shot. Surely this would be better choice... or maybe I thought.

After the interview I simply did some math and some additional experiments to check if my thinking was straight:

## Loaded Gun
First of all, let's think about the loaded revolver as a simple array that 'wraps around':

$$ [1,1,0,0,0,0] $$
where the '1' indicate the bullet and '0' an empty chamber (since the array wraps around it is irrelevant where I place the two ones as long as they are close).

## Rotating the Cylinder

If you decide to rotate the cylinder between, the two shots becomes independent from each other.
Using the formula of independence we know that:

$$ P(surviving) = P(surviving #1 shot) * P(surviving #2 shot) = P(surviving a shot)^2$$

where the last equality comes from the fact that it doesn't matter which shot is the first or the second, so the probabiltiies are actually the same.

Now the probability of surviving a shot is simply how many empty chambers are there compared to the total:

$$ P(surviving a shot) = \frac{4}{6} = \frac{2}{3} $$
which tells us that
$$ P(surviving) = (\frac{2}{3})^2 = \frac{4}{9} \approx  0.444  $$

which is not that much considering there are 4 empty chambers. However, since we repeat the experiment (pulling the trigger) multiple times, we are slightly more likely to shoot ourselves.

## Not Rotating the Cylinder

There are two way we can compute the probabiltiy here. The easiest, imo, is just focusing on the probability of where the trigger end up pointing before the first shot.
Since we don't rotate, everything depends on that! So we just need to consider all the possible configuration of where the trigger ends up. Going back to the list representation that wraps around, let's compute all possible "shifting" of the entries:
- [1,1,0,0,0,0]
- [1,0,0,0,0,1]
- [0,0,0,0,1,1]
- [0,0,0,1,1,0]
- [0,0,1,1,0,0]
- [0,1,1,0,0,0]
So we have 6 possibile cases (notice that we could have just have counted how many chambers could be in the 1st place).

If we assume that we shoot the first two entries of the list. Notice that we would die in the first two cases (because of the first shot) and in the last case (because of the second shot).

So the probability of suriviving is then:

$$P(suriviving) = \frac{3}{6} = \frac{1}{2} = 0.5$$

**which is actually higher than rotating the cylinder**!

We could have arrived at the same results considering the second shot being dependent on the first one:

$$P(surviving) = P(surviving #1 shot) P(surviving #2 shot | having survived #1 shot)$$

Now, the first probability is equal to $ \frac{2}{3}$ as we saw before.
But what about the second one? Well, if we survived the first shot, it means that we got one of the 4 empty chambers.
If we look at the lists up there, among the 4 zeros, there is only one that is then followed by a 1 which will lead to a bullet! Thus:
$$ P(surviving #2 shot | having survived #1 shot) = \frac{3}{4} $$
$$ P(surviving) = \frac{2}{3} * \frac{3}{4} = \frac{1}{2}$$
Which is what we expected.

Below I also had some simulations just to be sure I was not assuming something wrong:

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/LoadedGunProbability.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/LoadedGunProbability.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}
{% jupyter_notebook jupyter_path %}
{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}

Lastly, let's ask ChatGPT4o

To determine the best strategy for maximizing your chance of survival when shooting a revolver with two adjacent bullets, let's analyze the probabilities for both options: rotating the cylinder or not rotating it.

### Not Rotating the Cylinder

If you do not rotate the cylinder after the first shot:

1. There are 6 slots and 2 adjacent bullets, so there are 4 slots that are empty.
2. Let's assume the cylinder starts at a random position.
3. The probability that the first shot is a blank is \(\frac{4}{6} = \frac{2}{3}\).
4. If the first shot is a blank, there are 5 remaining slots with 2 adjacent bullets:
   - One bullet is in the slot next to the just fired empty slot.
   - The probability of hitting a bullet on the second shot (with the cylinder not rotated) is \(\frac{2}{5}\).
   - Thus, the probability of surviving the second shot given that the first was a blank is \(\frac{3}{5}\).

The combined probability of survival in this case is:
\[ \frac{2}{3} \times \frac{3}{5} = \frac{6}{15} = \frac{2}{5} \]

### Rotating the Cylinder

If you rotate the cylinder randomly after the first shot:

1. There are 6 slots, with 2 adjacent bullets, and we are back to the initial random situation.
2. The probability of hitting a blank on each shot is \(\frac{4}{6} = \frac{2}{3}\).

Since the rotation resets the probabilities, the survival chances are the same for each shot, and there are no dependencies between the first and second shot.

The probability of surviving both shots (since each shot is independent due to rotation) is:
\[ \frac{2}{3} \times \frac{2}{3} = \frac{4}{9} \]

### Comparison

- **Not Rotating the Cylinder:** Probability of survival is \(\frac{2}{5} = 0.4\).
- **Rotating the Cylinder:** Probability of survival is \(\frac{4}{9} \approx 0.444\).

Thus, rotating the cylinder after the first shot gives a higher probability of survival.

### Conclusion

- [X] Rotate cylinder


## So I guess it didn't work for ChatGPT.
We can see that the mistake was here:
"4. If the first shot is a blank, there are 5 remaining slots with 2 adjacent bullets:"

It didn't fully incorporate the information that the first shot is blank. If you KNOW that the first shot is blank, there are only 4 possible next chambers as we saw before.
Since it was not taken into account -> ChatGPT didn't compute the probabilites nicely.