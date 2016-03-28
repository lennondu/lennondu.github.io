---
layout: default
title: E(x^4)
permalink: /math/E(x^4)
category: math
---

# $\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{+\infty}x^4e^{-\frac{x^2}{2}}dx$

This is one way to compute the $E(x^4)$ when $x\sim N(0,1)$

$$\begin{align}\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{+\infty}x^4e^{-\frac{x^2}{2}}dx & =\frac{2}{\sqrt{2\pi}}\int_{0}^{+\infty}x^4e^{-\frac{x^2}{2}}dx \\ & \stackrel{t=x^2/2}= \frac{2}{\sqrt{2\pi}}\int_{0}^{+\infty}4t^2e^{-t}d\sqrt{2t} \\ &=\frac{4}{\sqrt\pi}\int_0^{+\infty}t^{3\over2}e^{-t}dt \\ &=\frac{4}{\sqrt\pi}\Gamma(\frac{5}{2}) \\ &=\frac{4}{\sqrt\pi}*\frac{3}{4}\sqrt{\pi}=3\end{align}$$

The fourth step is a gamma function.s
