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

# Estimators 
## Definitions and Properties
Suppose we have a population parameter $\theta$, and we are interested in estimating it.

An **point estimator** $\hat{\theta}$ for the parameter $\theta$ (from a population) is a statistic calculated from a random sample $\{X_1, X_2 \dots X_n\}$. The values of $\hat{\theta}$ are used as estimates for $\theta$.

> [!Example]- Example: Estimators (Motivation)
> Say our population takes on the normal distribution $X \sim N(\mu, \sigma^2)$. To be able to make predictions about the population, we need to know $\mu$ and $\sigma^2$! However, in many cases we don't have this information. 
> 
> For example, say John got 30 on an exam. He wants to know how well he did compared to his peers, so he wants to standardize his scores.
> $$
> \frac{30 - \mu}{\sigma}
> $$
>
> We don't know $\mu$ and $\sigma$! So instead, we will estimate them as $\hat{\mu}$ and $\hat{\sigma}^2$. After this, we'll have a distribution that we can use to make predictions! We do this by taking a sample of our population, and using this sample to estimate our population parameter!
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
> > This analysis is not perfect! Not only is the sample small, but it may not even be random! The datapoint of 30 could be John manually adding his score to the sample.

> [!Example]+ Example: Examples of Estimators
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

For a point estimator $\hat{\theta}$ of the parameter $\theta$, we define the **bias** of $\hat{\theta}$ as
$$
\text{Bias} (\hat{\theta}) = E(\hat{\theta}) - \theta
$$
Where $E(\hat{\theta})$ denotes the average values of $\hat{\theta}$. Furthermore, we say that $\hat{\theta}$ is an **unbiased estimator** for $\theta$ if $\forall \theta \in \Theta$,
$$
\text{Bias} (\hat{\theta}) = 0 
$$
This tells us how closely our estimator matches the parameter!

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

We define the **variance** of an estimator $\hat{\theta}$ as
$$
V(\hat{\theta}) = E\left( (\hat{\theta} - E(\hat{\theta}))^2 \right)
$$
Or in other words, the expected squared deviation of the values of $\hat{\theta}$ from $E(\hat{\theta})$! Just because we have an unbiased estimator, does not mean that it can give good results- some estimators may be unbiased, but can give heavily varying results.

We also define the **mean squared error** as
$$
\text{MSE} (\hat{\theta}) = E\left( (\hat{\theta} - \theta)^2 \right)
$$
Which defines the expected deviation of the values of $\hat{\theta}$ from $\theta$! We say that $\hat{\theta}$ on a random sample $\{X_1, X_2, \dots X_n\}$ is  **consistent** if
$$
\lim_{n\to\infty} \text{MSE}(\hat{\theta}) = 0
$$
> Good estimators will have small or minimal MSE.

All of these estimator definitions can be related in the following theorem.

> [!Abstract] Theorem: Bias-Variance Tradeoff
> For a point estimator $\hat{\theta}$, 
> $$
> \text{MSE} (\hat{\theta}) = V(\hat{\theta}) + \left( \text{Bias}(\hat{\theta}) \right)^2
> $$

Some consequences of this theorem are as follows:
- **Principle of Unbiased Estimation**: Generally, we prefer unbiased estimators. Not only does it lower MSE, but it also makes it easier to minimize our MSE, by removing the influence of bias in the above relation!
- Consistent estimators tell us that we can make the MSE as small as we want by using sufficiently large sample sizes.
- For a fixed sample size $n$, we will have to make trade offs between reducing bias and reducing variance, as reducing one increases the other.
- For unbiased estimators, MSE is equal to the variance.
- We will typically need to know how to calculate or estimate the sampling distribution of a point estimator.

## Estimators for $\mu$ and $\sigma^2$
### $\bar{X}$, $S^2$, and the Central Limit Theorem
Here, we describe estimators for two very commonly used population parameters.

Let $\{X_1, X_2, \dots X_n\}$ is a random sample of size $n$, from a population with some distribution $X$. Furthermore, suppose that we know the population mean and variance as 
$$
E(X) = \mu \qquad V(X) = \sigma^2
$$

To estimate these parameters, we have the following estimators. For mean, we have $\bar{X}$:
$$
\bar{X} = \frac{1}{n} \sum_{i=1}^n X_i = \frac{X_1 + X_2 + \dots + X_n}{n}
$$
For variance, we have $S_{xx}$:
$$
S_{xx} = \sum_{i=1}^n (X_i - \bar{X})^2 = (X_1 - \bar{X})^2 + \dots + (X_n - \bar{X})^2
$$

> [!Abstract] Theorem: Bias $\bar{X}$ and $S_{xx}$
> We can find that
> 1. $\bar{X}$ is an unbiased estimator for $\mu$
> 2. $E(S_{xx}) = (n - 1) \sigma^2$
> 3. $S^2 = \frac{1}{n-1} S_{xx}$, the **sample variance**, is an unbiased esetimator for $\sigma^2$

Note that the above hold, **regardless** of the population distribution we're sampling from! 

However, if we know about the population distribution, we may be able to infer some more information.

> [!Abstract] Theorem: Distributions of $\bar{X}$ and $S^2$, Normal Case 
> If $\{X_1, X_2, \dots X_n\}$ is a random sample from a population with distribution $X \sim N(\mu, \sigma^2)$, then we can find that the distributions of $\bar{X}$ and $S^2$ can be found as:
> $$
> \bar{X} \sim N\left( \mu, \frac{\sigma}{n} \right)
> \qquad
> \frac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1}
> $$
>
> > Note that by definition, we can represent the chi-squared distribution as Gamma($\alpha = \frac{n}{2}, \beta = 2$).

Even without knowing the population distribution, we may still be able to infer our sampling distributions! This is a powerful theorem known as the **Central Limit Theorem**.

> [!Abstract] Theorem: Central Limit Theorem
> If $\{X_1, X_2, \dots X_n\}$ is a random sample from a population with distribution $X$ with $E(X) = \mu$ and $V(X) = \sigma^2 < \infty$, then with $n$ sufficiently large, $\bar{X}$ approximates the normal distribution.
> $$
> \bar{X} \sim^\text{approx} N\left( \mu, \frac{\sigma^2}{n} \right)
> $$
> > Note that this tells us, that as the sample size increases, our sample distribution will center in on $\mu$! 

### Critical Values
Suppose $X$ has the distribution with cdf  defined as
$$
F_X (x) = P(X \le x) 
$$
Then, for some $\alpha \in (0,1)$, we say the **$\alpha^{th}$ critical value for $X$** is the number $x_\alpha$ satisfying:
$$
P(X \ge x_\alpha) = \alpha
$$
In other words, the critical value defines the proportion of people who did better than $x_\alpha$!
> More formally, the critical value lets us define a region in our probability distribution that we deem is quite significant. See the below example.

> [!Example]+ Example: Critical Values
> Suppose $X \sim \text{Exam Scores}$, where $X(\omega)$ is the exam score of student $\omega$.
> 
> Suppose $\alpha = 0.05$. Then, $x_\alpha$ is the value such that the probability of any random exam score being larger than $x_\alpha$ is 0.05. Formally,
> $$
> P(X \ge x_\alpha) = \alpha
> $$
>
> So, for small $\alpha$, having a score that is larger than $x_\alpha$ is an exceptional score. This lets us make inferences about the data, which is very important in later hypothesis testing!

Let $p \in (0,1)$. Then, the $p^{th}$ percentile is the value $n_p$ satisfying:
$$
P(X \le n_p) = p
$$
In other words, the percentile defines the proportion of people who did worse than $n_p$! 

This is complementary to the critical value. If $n_p$ is the value satisfying $p$, then we can find $n_p = x_\alpha$ for $\alpha = 1 - p$ (and vice versa).

Percentiles and critical values let us make inferences about exceptional scores within our data. If the probability that a random value from our distribution falls above (or under) our value is low, then we know that we have an exceptional score!

But what is a "low" probability? Generally, the standard, recommended by satistician Fisher, is to take $\alpha = 0.05$. Thus, for a value to be exceptional, it should be within the top 5% of the distribution.

## Deducations with $\bar{X}$
So given $\bar{X} \sim N(\mu_x, \sigma_x)$, what is an exceptional observation on this distribution?

If we know what $\mu_x$ and $\sigma_x$ are, we can **deduce** information about $\bar{X}$!

Observe that we can standardize our sample mean distribution as
$$
Z = \left( \frac{\bar{X} - \mu_x}{\sigma_x} \right)
$$

Then, using what's known as the **empirical rule**, we can find that
- 68% of the distribution falls between the 1st standard deviation of the mean.
- 95% of the distribution falls between the 2nd standard deviation of the mean.
- 99.7% of the distribution falls between the 3rd standard deviation of the mean.

So, any observation outside of 2 z-scores of the mean is significant!

So given any random sample $\bar{x}$, we can find how significant its sample mean is by taking
$$
P(\bar{X} \ge \bar{x}) \qquad P(\bar{X} \le \bar{x} 
\Longrightarrow 
P\left(z \ge \frac{\bar{x} - \mu_x}{\sigma_x}\right) \qquad P\left(z \le \frac{\bar{x} - \mu_x}{\sigma_x}\right)
$$
And look to see how small the probabilities are!

## Inferences with $\bar{X}$
What if we want to make statements about $\mu_x$ or $\sigma_x$ without exactly knowing the value of $\mu_x$ or $\sigma_x$? Well, we could try to **infer** it by sampling from our population!

In **Point Estimation**, we take a random sample of outputs, to create a single point estimate. However, we can't just find the probability that our estimate equals the population parameter, as this is 0 for continuous distributions! So, how can we infer the true average?

Cosider the equation
$$
P(|\bar{X} - \mu_x| < \epsilon) = 0.95
$$
So, we are defining a probability, a **confidence** that our sample mean doesn't deviate from the population mean by too much ($\epsilon$)!
$$
P\left( \left| \frac{\bar{X} - \mu_x}{\sigma_x/\sqrt{n}} \right| \le \frac{\epsilon}{\sigma_x / \sqrt{n}} \right) = 0.95
$$
By the Central Limit Theorem, we can find that this is approximately equivalent to
$$
P \left(|Z| \le \frac{\sqrt{u} \epsilon}{\sigma_x}\right) = 0.95
$$ 
So if we wanted to increase our confidence to 95%, we want to find
$$
Z_{0.025} = \frac{\sqrt{n} \epsilon}{\sigma_x} \Longrightarrow \epsilon = Z_{0.025} \frac{\sigma_x}{\sqrt{n}}
$$
So, submitting this back in, we find that
$$
\begin{align*}
P\left( \left| \bar{X} - \mu_x \right| \le Z_{0.025} \frac{\sigma_x}{\sqrt{n}} \right) = 0.95 \\
P\left( \bar{X} - Z_{0.025} \frac{\sigma_x}{\sqrt{n}} \le \mu_x \le \bar{X} + Z_{0.025} \frac{\sigma_x}{\sqrt{n}} \right) = 0.95 \\
P\left( u_x \in \left[ \bar{X} - Z_{0.025} \frac{\sigma_x}{\sqrt{n}}, \bar{X} + Z_{0.025} \frac{\sigma_x}{\sqrt{n}} \right] \right) = 0.95 \\
\end{align*}
$$
So, we have found our probability that our population parameter is within this interval to give us a 95% probability of being right! We call this the **95% confidence interval**.


---

> Point estimation tells us how close our estimator is to the actual paramter! Later, we do interval estimation, which tells us if our estiamtor is within some interval of the actual parameter.




--- CONTINUE ---

---



> [!Example]+ Example: The Best Estimator for Population Mean
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

> [!Example]+ Example: The Best Estimator for Population Deviation
> Say we want an estimator for $\sigma^2$. Some possible estimators are as follows:
> 1. $s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2$
> 2. $\hat{\sigma}^2_1 = \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2$
> 3. $\hat{\sigma}^2_2 = \frac{1}{n} \sum_{i=1}^n (X_i - \mu)^2$
> 
> Intuitively, it makes sense for us to want to use (2) whenever we have $\mu$! But let's calculate this to confirm. We want to find the estimator bias, as well as the mean squared error.

> [!Abstract] Theorem: 
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

| Distribution | Associated Parameters | Parameter Space |
| :-: | - | - |
| Bernoulli($p$) | $p$, the probability of success | 0, 1 |
 | Binom($n,p$) | $n$, the number of trials <br/> $p$, the probability of success | $\mathbb{N} * (0,1)$ |
| NegBinom($r,p$) | $r$, the number of successes we are looking for <br/> $p$, the probability of success | $\mathbb{N} * (0,1)$ |
| Pois($\lambda$) | $\lambda$, the rate of success | $\mathbb{R}_{>0}$ |
| $N(\mu, \sigma^2)$ | $\mu$, mean <br/> $\sigma^2$, variance | |
| Gamma($\alpha, \beta$) | $\alpha$, the shape parameter <br/> $\beta$, the scale parameter | |
| Exp($\lambda$) | $\lambda$, the rate paramter | $\mathbb{N}$ |
| Chi-Sq($n$) | $df$, the degrees of freedom | $\mathbb{N}$ |
| Beta($\alpha, \beta$) | ...



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
