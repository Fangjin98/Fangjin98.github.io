---
title: Application | DayDayUp
date: 2022-04-30 23:44:25
tags:
 - UWP
 - Windows App SDK
 - C#
---
> ~~Estimated release date: 2022.5.31.~~
> ~~Estimated release date: 2022.6.31.~~
> Published in <https://github.com/Fangjin98/DayDayUp>

<p align="center">
  An Easy-To-Use Todo Manager with Time Estimation Tracking.  
</p>

<p align="center"> <img src=1.png alt="screenshot" /> </p>

## Motivation

Time estimation is a key need for todo management. We help you to better estimate the completion time of todos via evidence-based scheduling (EBS). Specifically, we adopt the history duration of finished todos to predict the bias of estimated duration of unfinished todos.

## How to Estimate?

We first give the defintion of _duration_, _estimated duration_ and _real durations_.

1. _duration_ is the total time to complete a todo. When you completed a todo (pressed the checkbox), the application would calculate the _duration_ by subtracting the creation time from the completion time. Only finished todos have the _duration_.
2. _estimated duration_ is set when (after) you create a todo. It is the duration you expect to complete this todo. The _estimated duration_ is set by users for unfinished todos.
3. _real durations_ are calculated by DayDayUp based on the _duration_ of finished todos. It is a set of values, representing the _durations_ under different probabilities.

Then we give the definition of _bias rate_ of one finished todo as the _estimated duration/duration_ of it. And the set of _bias rates_ contains all the _bias rate_ of finished todos.

We adopt Monte Carlo Method to calculate _real durations_ for each todo. For each unfinished todo, we select one _bias rate_ from its set and calculate _real duration/bias rate_. We repeat the procedure for 100 times, then we obtain the _real durations_ of the unfinished todo.