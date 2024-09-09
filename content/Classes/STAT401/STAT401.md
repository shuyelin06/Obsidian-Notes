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

> [!Example] Example: Examples of Estimators
> Suppose we want to estimate a population with a normal distribution. The following are examples of estimators.
> 
> We could estimate $\mu$ as:
> 1. $\bar{X} = \frac{1}{n} (X_1 + X_2 + \dots + X_n)$
> 2. $\bar{X}_k = \frac{1}{k} (X_1 + X_2 + \dots + X_k)$ for $k \le n$.
> 
> We could estimate $\sigma^2$ as:
> 1. $\hat{\sigma}^2_1 = \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2$
> 2. $\hat{\sigma}^2_2 = \frac{1}{n} \sum_{i=1}^n (X_i - \mu)^2$

Suppose $\hat{\theta}$ is an estimator for $\theta$. We say that the **parameter space**, $\Theta$, is the set of all possible values that $\theta$ can take on.
> This defines what values our estimator can take on!

The **bias** of $\hat{\theta}$ is defined as
$$
\text{Bias} (\hat{\theta}) = E(\hat{\theta}) - \theta
$$
Where $E(\hat{\theta})$ denotes the average values of $\hat{\theta}$.

And furthermore, we say that $\hat{\theta}$ is an **unbiased estimator** for $\theta$ if $\forall \theta \in \Theta$,
$$
\text{Bias} (\hat{\theta}) = 0 
$$
This tells us how closely our estimator matches the parameter! We generally prefer unbiased estimators, in what is known as the **principle of unbiased estimation**.

> [!Info] Principle of Unbiased Estimation
> Among the possible estimators for $\theta$, we should choose an unbiased estimator.

> [!Example]+ Example: Unbiased Estimator for Population Mean
> Let $\hat{X}_k = \frac{1}{k} \sum_{i=1}^k X_i$.
>
> What is $E(\hat{X}_k)$? 
> $$
> \begin{align*}
> E\left( \frac{1}{k} \sum_{i=1}^k X_i \right) 
> &= \frac{1}{k} \sum_{i=1}^k E(X_i) \\
> &= \frac{1}{k} \left( \sum_{i=1}^k \mu \right) \\
> &= \mu
> \end{align*}
> $$
> 
> This means that $E(\hat{X}_k)$ is an unbiased estimator for $\mu$!

We can calculate how biased our estimator is! But there can be many unbiased estimators! So among these unbiased estimators, which one should we choose? 

We define the **variance** of an estimator $\hat{\theta}$ as
$$
V(\hat{\theta}) = E\left( (\hat{\theta} - E(\hat{\theta}))^2 \right)
$$
Or in other words, the expected squared deviation of the values of $\hat{\theta}$ from $E(\hat{\theta})$! Just because we have an unbiased estimator, does not mean that it can give good results- some estimators may be unbiased, but can give heavily varying results (which would also not be the best!).

We define the **mean squared error** as
$$
\text{MSE} (\hat{\theta}) = E\left( (\hat{\theta} - \theta)^2 \right)
$$
Which defines the expected deviation of the values of $\hat{\theta}$ from $\theta$! Note that it can be shown that
$$
\text{MSE} (\hat{\theta}) = V(\hat{\theta}) + \left( \text{Bias}(\hat{\theta}) \right)^2
$$
So if $\hat{\theta}$ is an unbiased estimator, it must be true that $\text{MSE}(\hat{\theta}) = V(\hat{\theta})$! Thus, we can use the MSE to measure the variance of unbiased estimators. 
> It is often the case that in minimizing either variance or bias, the other increases. So, typically a good estimator is one that aims to find a middle ground between both!

> [!Example] Example: The Best Estimator for Population Mean
> From our previous example, $\hat{\theta}_k = \bar{X}_k$. We can find the variance of our estimator as
> 
> $$
> \begin{align*}
> V(\hat{\theta}_k) &= V \left( \frac{1}{k} \sum_{i=1}^n X_i \right) \\
> &= \frac{1}{k^2} \sum_{i=1}^k V(X_i) \\
> &= \frac{1}{k^2} \sum_{i=1}^k \sigma^2 = \frac{\sigma^2}{k}
> \end{align*}
> $$
> 
> So we find that our variance depends on the number of samples we take! If we take less samples, we will have a higher variance in our estimator! 
> 
> So, in this example, our most optimal estimator is $\hat{\theta} = \hat{X} = \frac{1}{n} \sum_{i=1}^n X_i$ as it is an unbiased estimator with the least variance. 

> [!Example] Example: The Best Estimator for Population Deviation
> Say we want an estimator for $\sigma^2$. Some possible estimators are as follows:
> 1. $s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2$
> 2. $\hat{\sigma}^2_1 = \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2$
> 3. $\hat{\sigma}^2_2 = \frac{1}{n} \sum_{i=1}^n (X_i - \mu)^2$
> 
> Intuitively, it makes sense for us to want to use (2) whenever we have $\mu$! But let's calculate this to confirm. We want to find the estimator bias, as well as the mean squared error.

> [!Abstract]
> Suppose $\{X_1, X_2, \dots X_n\}$ is a random sample from $N(\mu, \sigma^2)$. 
>
> $$
> \begin{align*}
> \bar{X} = \frac{1}{n} \sum_{i=1}^n X_i \\
> S_{xx} = \sum_{i=1}^n (X_i - \bar{X})^2
> \end{align*}
> $$
> 
> Then, we can find that
> $$
> \frac{S_{xx}}{\sigma^2} \sim X^2_{n-1}
> $$
> Or in other words, this is equal to the Chi Squared Distribution with $n - 1$ degrees of freedom.
> 
>

> Before, CLT describes the distribution of X bar, the sample mean (for any distribution, given we take a random sample). 
>
> This theorem describes the distribution of $S^2$, **the sample variance**, given that the random sample is taken from a normal distribution... theorem describes distribution of the sample variance as:
> $$
> S^2 = \frac{X^2_{n-1}}{n=1} * \sigma^2
> $$
>
> We can find the expectation to be $\sigma^2$.
> 

> IT can be seen that $n - 1$ is best, and yields an unbiased estimator... WIP

> IT can be found that sample variance, $S^2$, is always equal to $\sigma^2$.

We can find the sample variance as
$$
S^2 = \frac{
$$

---


Ways to estimate..

Method of moments

Maximum likelihood estimation

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

$$
S^2 
$$
