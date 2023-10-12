---
title: "Prompt Engineering Mathematical Logic"
date: 2023-07-31T06:05:30-07:00
draft: true
tags: ["Data"]
---

This post is Part 2 in a series on Prompt Engineering for AI chatbots like ChatGPT and Bard. For Part 1, see:

**[Chat AI Prompt Engineering - Part 1 (Intro and Spark Example)](/posts/chat-ai-prompt-engineering-part1)**

That first part of the series focused on prompt engineering for code generation (in particular for a PySpark job file). In this part of the series, I'd like to take a look at a slightly different topic - **mathematical reasoning**.

First, let's use the chatbots to see if we can get some insight into the property that most of us learn in elementary or middle school that the sum of interior angles in a triangle is always 180 degree.

## Prompt: Prove That Triangle's Angles Always Sum to 180°

Initial prompt:
>**Can you walk me through a proof of the fact that the sum of all angles in a triangle is always 180 degrees?**

Certainly! The fact that the sum of all angles in a triangle is always 180 degrees is a fundamental property of Euclidean geometry. We can prove it using a simple geometric argument.

Let's consider a triangle ABC:


  A
 / \
/   \

/
/
B ------- C

We want to find the sum of the three angles: ∠A, ∠B, and ∠C.

Proof:
Step 1: Draw a line segment from vertex A to a point D on the opposite side BC such that AD is parallel to BC. This creates two new angles: ∠DAB and ∠DAC.


  A
 / \
/   \

/
/
B ------- C
|
D

Step 2: Since AD is parallel to BC, ∠DAB and ∠ABC are alternate interior angles, which means they are congruent (equal). Similarly, ∠DAC and ∠ACB are also congruent.

Step 3: Now let's look at the triangle ACD. The angles in triangle ACD also sum up to 180 degrees (this is true for any triangle). So, we have:

∠DAB + ∠DAC + ∠ACD = 180 degrees

Step 4: But, ∠ACD is just ∠B (they are corresponding angles). Therefore, we can rewrite the equation as:

∠DAB + ∠DAC + ∠B = 180 degrees

Step 5: Now let's go back to triangle ABC. Notice that ∠DAB and ∠DAC together form ∠A. So, we can substitute them with ∠A:

∠A + ∠B + ∠C = 180 degrees

Step 6: And there you have it! We have proved that the sum of all angles in a triangle is always 180 degrees.

This proof works for any type of triangle (scalene, isosceles, or equilateral) because it relies on the parallel line property and the fact that the sum of angles in any triangle is 180 degrees.

[make sure not to use the same fact in the proof]

As we can see, this prompt almost immediately requires some revision because both ChatGPT and Bard were pretty quick to make use, in the proofs, of the fact that the sum of angles in a triangle is 180 degrees (which, being the fact that we are trying to prove, is not admissible in the internal reasoning of the proof, because this creates circular logic)