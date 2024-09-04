---
title: STAT401
tags:
- stat401
---

# Basic Concepts
We say that an **experiment** is a repeatable task with well defined outcomes. The **sample space ($S$)** for this experiment is the set of all possible outcomes of the experiment.

Any subset $E$ of the sample space for an experiment is called an **event**. To say that **an event $E$ has happened** means that we performed the experiment, and had the outcome which was in the set $E$.
> Events with exactly one outcome are called **simple events**.

Given a sample space, we can define a **random variable**, which is a function $X : S \to \mathbb{R}$ which assigns a number to a given sample space outcome. This number will relate to what we're interested in measuring for the experiment.

> [!Example]+ Example: Random Variables
> Say we flip a coin 4 times.
>
> The size of the sample space would be $2^4$, the total number of possible outcomes after flipping the coin. One outcome, for example, is $HHTH$. 
>
> A random variable would take this outcome, $HHTH$, and assign some number to it relevant to our interests (ex. the number of heads 3, the number of tails 1, etc.)

Any collection of random variables $\{X_1, X_2, \dots X_n\}$ is called a **random sample** if the following conditions are met:
- All of the $X_i$'s are identically distributed.
- All of the $X_i$'s are mutually independent.

> [!Example] Example: Random Samples
> Say we have a collection of random variables $E_1, E_2, \dots E_4$, all representing scores on different exams. Does this constitute a random sample?
> 
> Not necessarily! These exam scores may not come from the same distribution. 

Given a population, we call a **parameter** a quantitative feature of the population. If we try to calculate this feature with a sample, we call it a **statistic**! More formally, statistics are functions of this random sample taking values in $\mathbb{R}$. 

Say we have a population, and we took a sample from it. With this, we often want to do 2 things:
1. **Deduction**: Given something known about the population, analyze the sample.
2. **Generalization**: Given the sample, try to make an inference about the population.

This is where random samples come in! With a random sample, we may be able to make inferences about our population! In fact, we call an **estimator** for the parameter $\theta$ a statistic that is calculated using a random sample from the population with parameter $\theta$.

Suppose our population is all students in the class, with our sample space being all students. 

Now suppose we have a random variable $E_1$, where given a student $\omega$, calculates and returns that student's score ($E_1(\omega)$). The distribution of $E_1$ then, is the same as the distribution of the exam scores for the class! In this setting, we know that the expected value of $E_1$ is the average score for the students on the exam.

We want the average score, but in many cases, we won't have all information about the population! So, instead, let's try to "guess" what the population data is given any subset of the data we can collect!

This process is called **Parametric Estimation**, and lets us make probabilistic statements about the population. It (generally) follows the following process:
1. **Step 1**: Assume that the population follows a particular distribution with parameters $\theta_1, \theta_2, \dots$.
2. **Step 2**: Use sample data from the population and our knowledge of the distribution to estimate the parameters of the distribution.
3. **Step 3**: Use the distribution (with found parameters) to deduce information about individuals in the population.

> [!Example]+ Example: Parametric Estimation with Exams
> Back to our previous example, say we want to estimate the average for the exam. We could do it as follows:
> 1. Assume a distribution on $E_1$.
> 2. Use sample data from the students in order to estimate the parameters of this assumed distribution.
>
> So, suppose we knew that $E_1 \sim N(\mu, \sigma^2)$, or in other words, was normal. Then, we would try to fit our normal distribution to our samples to find $\mu$ and $\sigma$, and find our average as $\mu$!
> > Note that based on the distribution that we assume on the population, we can get wildly differing results!

# Methods of Point Estimation 
Suppose $\theta$ is a paramter attached to a population distribution.

An **estimator** for $\theta$ is a statistic calculated from a random sample. The values of the statistic are estimates for $\theta$.

> [!Example] Example: Estimators
> Say our population takes on the normal distribution $X \sim N(\mu, \sigma^2)$.
>
> To be able to make predictions about the population, we need to know $\mu$ and $\sigma^2$! However, in many cases we don't have this information. For example, say John got 30 on an exam. He wants to know how well he did compared to his peers, so he wants to standardize his scores.
> $$
> \frac{30 - \mu}{\sigma}
> $$
>
> Instead, we will want to estimate $\hat{\mu}$ and $\hat{\sigma}^2$. Once we estimate these parameters, we'll have a distribution that we can use to make predictions! We can do this by taking a sample of our population, and using this sample to estimate our population parameter!
>
> So, John samples some of his friends to find scores $(30, 72, 95)$. With this data, he estimates the mean and standard deviation:
> $$
> \begin{align*}
>     &\hat{\mu} = \frac{30 + 72 + 95}{3} = 66 \\
>     &\hat{\sigma}^2 = \frac{1}{3 - 1} ( (30 - 66)^2 + (72 - 66)^2 + (95 - 66)^2 ) = 1086.5 \\
>     &\hat{\sigma} = \sqrt{\hat{\sigma}} = 32.96
> \end{align*}
> $$
> With these estimates, John can now standardize his scores to see how well he did.
> $$
> \frac{30 - 66}{32.96} = -1.09
> $$
> With this score, John can tell that he did poorly compared to the rest of his class. In fact, with the assumption that the scores are normally distributed, John finds that roughly 84% of the class did better than him!
> > Note that this analysis is not perfect! Not only is the sample small, but it may not even be random! The datapoint of 30 could be John manually adding his score to the sample.


---

Recall that we say $X$ is the **normal distribution** if the pdf of $X$ is given as
$$
f_x (x, \mu, \sigma^2) = \frac{1}{\sqrt{2\pi}} e^{-(x-\mu)^2/2 \sigma^2}
$$
With $E(X) = \mu$, $V(X) = \sigma^2$.

If we wanted to find the probability that $a \le x \le b$, we can find it by integrating our pdf!
$$
\int_a^b f_x (x, \mu, \sigma^2) dx
$$

---

