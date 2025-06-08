---
title: Fourier Transform
---

# The Fourier Transform
## Context
Suppose we have a series of complex numbers
$$
c_1, c_2, c_3, c_4 \dots c_n
$$

Let these numbers represent a "signal" we're receiving. Now suppose that given this signal, I wanted to find the original frequencies making up this signal. How can I do this? 
> This signal could be an audio file, and by finding the frequencies, I'm finding the pitches in the audio file.

Introducing, the **Fourier Transform**. This is a mathematical operation that can transform our signal into a series of complex-valued frequencies making up the original signal.
$$
f_1, f_2, f_3, \dots f_n
$$
In other words, the transform can decompose our signal into a series of sine functions (described by the frequencies) that together, can reconstruct our signal. There also exists an **Inverse Fourier Transform** that gives us back our original signal.

What makes Fourier Transform useful is the fact that it establishes a bijection between our signal and the resulting frequencies. This allows for many use cases, such as:
- Decomposing an image and blurring it by removing high frequencies
- Decomposing an audio signal to see what pitches (frequencies) it's composed of- Creating wave simulations using a real-world frequency data 

## Discrete Transform
The Fourier Transform has continuous and discrete variants. For our case, it's more common to use the discrete transform. 

The **Discrete Fourier Transform (DFT)** is defined as
$$
F[n] = \sum_{k=0}^{N-1} f[k] e^{-i \frac{2\pi}{N} nk}
$$
In other words, for the $n^{th}$ frequency, we need to compute this sum. The definition looks scary, so let's break it down. 
- $f[k]$ represents our $N$ input data points.
- The exponent $e$ represents a rotation in the complex plane. Recall that $e^{-i \theta}$ for varying theta creates a circle in the complex plane.

What we're doing is using $n$ to set how fast $e$ rotates along the complex plane. This represents a sine wave with a set frequency, and we use each input data point, we're augmenting the magnitude of the wave at that location. Summing each of these samples gives us our result.

> [!Info] Euler's Formula:
> The complex exponential is defined as follows. For real number $x$,
> $$
> e^{ix} = \cos(x) + i \sin(x) 
> $$

We can also find the $DFT$ in matrix form as follows:
$$
\begin{bmatrix}
F[0] \\ F[1] \\ F[2] \\ \vdots \\ F[N - 1]
\end{bmatrix}
= 
\begin{bmatrix}
1 & 1 & 1 & 1 & \dots & 1 \\
1 & W & W^2 & W^3 & \dots & W^{N-1} \\
1 & W^2 & W^4 & W^6 & \dots & W^{N-2} \\ 
1 & W^3 & W^6 & W^9 & \dots & W^{N-3} \\ 
\vdots \\
1 & W^{N-1} & W^{N-2} & W^{N-3} & \dots & W \\ 
\end{bmatrix}
$$
For $W = e^{-i \frac{2\pi}{N}}$. Note that $W = W^{2N} = 1$. 

## Fast Fourier Transform
Simply performing the multiplication and summing as above takes $O(n^2)$ time. We can do better than this! By grouping terms in the summation together, we can reuse repeated computations.

The derivation is as follows. For discrete Fourier Transform $X[k]$, separate our transform into an even and odd case.
- When $k = 2s$ (even),
  $$
  \begin{align*}
  X[2s] &= \sum_{p=0}^{N-1} x[p] W_N^{2s * p}
  \end{align*}
  $$
