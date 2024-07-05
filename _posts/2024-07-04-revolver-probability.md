---
layout: post
title: Loaded Revolver and Probability 
date: 2024-07-04 08:57:00-0400
description: Answering a riddle on probability and running some simulations.
tags: code, probability
categories: code
giscus_comments: false
related_posts: false
---

# Loaded Revolver and Probability 
Recently, I took a quiz as the first step of a machine learning interview. The quiz consisted of several questions covering various aspects of machine learning, deep learning, probability, and practical intuition for model training and evaluation. One particular question, however, stuck with me:


> You are given a revolver with six slots. There are two adjacent bullets. You have to
shoot twice and are given the chance to rotate the cylinder randomly in-between. How
do you maximize your chance of survival?
> - [ ] Rotate cylinder
> - [ ] Do not rotate cylinder
> - [ ] It does not matter, as the survival chance is the same in both cases
> - [ ] The question does not give all information required to answer the question

Under pressure, I chose to rotate the cylinder. After all, it generally made sense at the time. By resetting your chances after the first shot, it seemed like the better choice—or so I thought.

After the interview, I decided to delve deeper. I did some math and conducted a few experiments to verify if my thinking was correct.

## Settings
First, let's think about the loaded revolver as a simple array that loops back on itself:

$$[1,1,0,0,0,0]$$

Here, '1' represents a bullet, and '0' represents an empty chamber. Since the array loops back, it doesn't matter where the two bullets ('1's) are placed as long as they are next to each other.

## Option 1: Rotating the Cylinder
If you decide to rotate the cylinder between shots, the two shots become independent of each other. Using the formula for independent events, we know that:

$$ P(\text{surviving}) = P(\text{surviving 1st shot}) * P(\text{surviving 2nd shot}) = P(\text{surviving a shot})^2$$

This equality holds because the probability of surviving each shot is the same, regardless of the order.

Now, the probability of surviving a single shot is simply the number of empty chambers divided by the total number of chambers:

$$ P(\text{surviving a shot}) = \frac{4}{6} = \frac{2}{3} $$

Therefore, the probability of surviving both shots is:

$$ P(\text{surviving}) = (\frac{2}{3})^2 = \frac{4}{9} \approx  0.444  $$

This result shows that there is only a 44.4% chance of surviving both shots, despite there being four empty chambers. This lower probability arises because repeating the experiment (pulling the trigger) multiple times increases the overall risk.
If you decide to rotate the cylinder between, the two shots becomes independent of each other.
Using the formula of independence we know that:

## Option 2: Not Rotating the Cylinder

There are two ways to compute the probability of surviving. The easiest, in my opinion, is to focus on where the trigger ends up pointing before the first shot. Since we don't rotate the cylinder between shots, everything depends on that initial position. We need to consider all possible configurations of where the trigger ends up. Using our list representation that wraps around, let's compute all possible "shifts" of the entries:

- [1,1,0,0,0,0]
- [1,0,0,0,0,1]
- [0,0,0,0,1,1]
- [0,0,0,1,1,0]
- [0,0,1,1,0,0]
- [0,1,1,0,0,0]

So we have 6 possible cases (note that we could have simply counted how many chambers could be in the first place).

If we assume that we shoot the first two entries of the list, we can see that we would die in the first two cases (because of the first shot) and in the last case (because of the second shot).

Thus, the probability of surviving is:

$$P(\text{surviving}) = \frac{3}{6} = \frac{1}{2} = 0.5$$

** This is actually higher than rotating the cylinder!**

We could have arrived at the same result by considering the second shot as dependent on the first one:

$$P(\text{surviving}) = P(\text{surviving 1st shot}) P(\text{surviving 2nd shot | having survived 1st shot})$$

The probability of surviving the first shot is $ \frac{2}{3}$ as we saw before. But what about the second one? Well, if we survived the first shot, it means that we landed on one of the 4 empty chambers. Looking at the lists above, among the 4 zeros, there is only one that is followed by a 1 (a bullet). Thus:

$$ P(\text{surviving 2nd shot | having survived 1st shot}) = \frac{3}{4} $$

So, the overall probability of surviving is:

$$ P(\text{surviving}) = \frac{2}{3} * \frac{3}{4} = \frac{1}{2}$$

Which is what we expected.

For fun, I also coded some simple probability simulation to check the results:

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/LoadedGunProbability.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/LoadedGunProbability.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}
{% jupyter_notebook jupyter_path %}
{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}

The simulation results confirmed the previous calculations:

- Survival rate with rotating cylinder: $$\approx 0.444$$ 
- Survival rate without rotating cylinder:  $$0.5$$

So, again, not rotating the cylinder gives a slightly better chance of survival.

## Bonus: ChatGPT4o's Answer


> To determine the best strategy for maximizing your chance of survival when shooting a revolver with two adjacent bullets, let's analyze the probabilities for both options: rotating the cylinder or not rotating it.
>### Not Rotating the Cylinder
>If you do not rotate the cylinder after the first shot:
>
>1. There are 6 slots and 2 adjacent bullets, so there are 4 slots that are empty.
>2. Let's assume the cylinder starts at a random position.
>3. The probability that the first shot is a blank is $$\frac{4}{6} = \frac{2}{3}$$.
>4. If the first shot is a blank, there are 5 remaining slots with 2 adjacent bullets:
>   - One bullet is in the slot next to the just fired empty slot.
>   - The probability of hitting a bullet on the second shot (with the cylinder not rotated) is $$\frac{2}{5}$$.
>   - Thus, the probability of surviving the second shot given that the first was a blank is $$\frac{3}{5}$$.
>
>The combined probability of survival in this case is:
$$ \frac{2}{3} \times \frac{3}{5} = \frac{6}{15} = \frac{2}{5} $$
>
> ### Rotating the Cylinder
>
>If you rotate the cylinder randomly after the first shot:
>
>1. There are 6 slots, with 2 adjacent bullets, and we are back to the initial random situation.
>2. The probability of hitting a blank on each shot is $$\frac{4}{6} = \frac{2}{3}$$.
>
>Since the rotation resets the probabilities, the survival chances are the same for each shot, and there are no dependencies between the first and second shot.
>
>The probability of surviving both shots (since each shot is independent due to rotation) is:
>$$ \frac{2}{3} \times \frac{2}{3} = \frac{4}{9} $$
>
>### Comparison
>
>- **Not Rotating the Cylinder:** Probability of survival is $$\frac{2}{5} = 0.4$$.
>- **Rotating the Cylinder:** Probability of survival is $$\frac{4}{9} \approx 0.444$$.
>
>Thus, rotating the cylinder after the first shot gives a higher probability of survival.
>
>### Conclusion
>
>- [X] Rotate cylinder

We can see that the mistake was here: "If the first shot is a blank, there are 5 remaining slots with 2 adjacent bullets." However, since you **KNOW** that the first shot is blank, there are only 4 (and not 5) possibilities.

Always carefully check the output of generative LLMs; they are pretty good at spitting out things that might look correct but can contain errors.