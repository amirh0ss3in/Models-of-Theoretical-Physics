# Notes on Gaussian Integrals and Characteristic Functions
*From course: Models of T.P. (Lectures from 30/9/25 & 3/10/25)*

## 1. The Gaussian Integral

### 1.1 The Basic Integral
We begin by considering the Gaussian probability distribution function (PDF):
$$
P(x) = C e^{-\frac{ax^2}{2}}, \quad a > 0
$$
For this to be a valid PDF, it must be normalized over its domain $(-\infty, +\infty)$, meaning:
$$
\int_{-\infty}^{+\infty} P(x)dx = 1 \implies C \int_{-\infty}^{+\infty} e^{-\frac{ax^2}{2}} dx = 1
$$
This requires us to solve the simplest Gaussian integral. The standard result is:

> **① The Fundamental Gaussian Integral**
> $$
> \int_{-\infty}^{+\infty} e^{-\frac{ax^2}{2}} dx = \sqrt{\frac{2\pi}{a}}
> $$

From this, we can see the normalization constant for the Gaussian PDF is $C = \sqrt{\frac{a}{2\pi}}$.

### 1.2 The General 1D Gaussian Integral
A more general form of the integral includes a linear term in the exponent:
$$
\text{②} \quad \int_{-\infty}^{+\infty} e^{-\frac{ax^2}{2} + bx} dx = ?
$$
To solve this, we "complete the square" in the exponent. The core idea is to shift the integration variable to center the Gaussian. The maximum of the exponent occurs where its derivative is zero:
$$
\frac{d}{dx} \left(-\frac{ax^2}{2} + bx\right) = -ax + b = 0 \implies x = \frac{b}{a}
$$
This suggests the change of variables $y = x - \frac{b}{a}$, which means $x = y + \frac{b}{a}$ and $dx = dy$. Substituting this into the exponent:
$$
\begin{aligned}
-\frac{ax^2}{2} + bx &= -\frac{a}{2}\left(y + \frac{b}{a}\right)^2 + b\left(y + \frac{b}{a}\right) \\
&= -\frac{a}{2}\left(y^2 + \frac{2by}{a} + \frac{b^2}{a^2}\right) + by + \frac{b^2}{a} \\
&= -\frac{ay^2}{2} - by - \frac{b^2}{2a} + by + \frac{b^2}{a} \\
&= -\frac{ay^2}{2} + \frac{b^2}{2a}
\end{aligned}
$$
The integral becomes:
$$
\int_{-\infty}^{+\infty} e^{-\frac{ay^2}{2} + \frac{b^2}{2a}} dy = e^{\frac{b^2}{2a}} \int_{-\infty}^{+\infty} e^{-\frac{ay^2}{2}} dy
$$
Using the result from **①**, we arrive at the general solution, which holds even if $b$ is a complex number.

> **③ The General 1D Gaussian Integral**
> $$
> \int_{-\infty}^{+\infty} e^{-\frac{ax^2}{2} + bx} dx = \sqrt{\frac{2\pi}{a}} e^{\frac{b^2}{2a}} \quad (a>0, b \in \mathbb{C})
> $$

---

## 2. Characteristic Functions

The **characteristic function (c.f.)** of a probability distribution $p(x)$ is its Fourier transform, and it is a powerful tool for analyzing distributions.

> **④ Definition: Characteristic Function**
> $$
> \varphi(k) = \int_{-\infty}^{+\infty} e^{ikx} p(x) dx = \langle e^{ikx} \rangle
> $$

### 2.1 Moments of a Distribution
A key property of the characteristic function is that its derivatives at $k=0$ generate the moments of the distribution ($ \langle x^n \rangle = \int x^n p(x)dx $).

> **⑤ Moments from the Characteristic Function**
> $$
> \langle x^n \rangle = (-i)^n \left. \frac{d^n\varphi(k)}{dk^n} \right|_{k=0}
> $$

### 2.2 Characteristic Function of the Gaussian Distribution
We can find the c.f. of a zero-mean Gaussian distribution, $p(x) = \sqrt{\frac{a}{2\pi}} e^{-\frac{ax^2}{2}}$, by using our general integral result **③**. We set $b=ik$:
$$
\varphi(k) = \sqrt{\frac{a}{2\pi}} \int_{-\infty}^{+\infty} e^{-\frac{ax^2}{2} + ikx} dx = \sqrt{\frac{a}{2\pi}} \left( \sqrt{\frac{2\pi}{a}} e^{\frac{(ik)^2}{2a}} \right) = e^{-\frac{k^2}{2a}}
$$
It is standard to write the Gaussian PDF in terms of its variance, $\sigma^2$. The relationship is $a = 1/\sigma^2$.

> **⑥ C.F. of the Gaussian Distribution**
> For $p(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{x^2}{2\sigma^2}}$, the characteristic function is:
> $$
> \varphi(k) = e^{-\frac{\sigma^2 k^2}{2}}
> $$

### 2.3 Exercises

**Ex 1:** Show that when the mean of the Gaussian is $\mu$, the characteristic function is $\varphi(k) = e^{ik\mu - \frac{\sigma^2k^2}{2}}$.

Solution:

A Gaussian with mean $\mu$ and variance $\sigma^2$ has the PDF:
$$ p(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}} $$
The characteristic function is:
$$ \varphi(k) = \int_{-\infty}^{+\infty} e^{ikx} \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}} dx $$
Let's make the substitution $y = x - \mu$, so $x = y + \mu$ and $dx = dy$.
$$
\begin{aligned}
\varphi(k) &= \frac{1}{\sqrt{2\pi\sigma^2}} \int_{-\infty}^{+\infty} e^{ik(y+\mu)} e^{-\frac{y^2}{2\sigma^2}} dy \\
&= e^{ik\mu} \left( \frac{1}{\sqrt{2\pi\sigma^2}} \int_{-\infty}^{+\infty} e^{iky} e^{-\frac{y^2}{2\sigma^2}} dy \right)
\end{aligned}
$$
The expression in the parenthesis is just the characteristic function of a zero-mean Gaussian, which we already found in **⑥**. Therefore:
$$ \varphi(k) = e^{ik\mu} \cdot e^{-\frac{\sigma^2k^2}{2}} = e^{ik\mu - \frac{\sigma^2k^2}{2}} $$

**Ex 2:** Calculate the c.f. of the uniform distribution $U([a, b])$.

Solution:

The PDF for the uniform distribution on $[a, b]$ is $p(x) = \frac{1}{b-a}$ for $x \in [a, b]$ and 0 otherwise.
$$
\begin{aligned}
\varphi(k) &= \int_a^b e^{ikx} \frac{1}{b-a} dx \\
&= \frac{1}{b-a} \left[ \frac{e^{ikx}}{ik} \right]_a^b \\
&= \frac{e^{ikb} - e^{ika}}{ik(b-a)}
\end{aligned}
$$

**Ex 3:** Calculate the c.f. of the Gamma distribution $p(x) = \frac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x}$ for $x > 0$.

Solution:

The characteristic function is defined for $x>0$:
$$
\begin{aligned}
\varphi(k) &= \int_0^\infty e^{ikx} \frac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x} dx \\
&= \frac{\beta^\alpha}{\Gamma(\alpha)} \int_0^\infty x^{\alpha-1} e^{-(\beta - ik)x} dx
\end{aligned}
$$
We use the standard integral definition of the Gamma function, $\Gamma(z) = \int_0^\infty t^{z-1} e^{-t} dt$. Let $u = (\beta - ik)x$, so $x = u/(\beta-ik)$ and $dx = du/(\beta-ik)$.
$$
\begin{aligned}
\varphi(k) &= \frac{\beta^\alpha}{\Gamma(\alpha)} \int_0^\infty \left(\frac{u}{\beta-ik}\right)^{\alpha-1} e^{-u} \frac{du}{\beta-ik} \\
&= \frac{\beta^\alpha}{\Gamma(\alpha)} \frac{1}{(\beta-ik)^\alpha} \int_0^\infty u^{\alpha-1} e^{-u} du \\
&= \frac{\beta^\alpha}{\Gamma(\alpha)} \frac{\Gamma(\alpha)}{(\beta-ik)^\alpha} = \left(\frac{\beta}{\beta-ik}\right)^\alpha = \left(1 - \frac{ik}{\beta}\right)^{-\alpha}
\end{aligned}
$$

---

## 3. The Multidimensional Gaussian Integral

### 3.1 The Basic Multidimensional Integral
We now generalize the integral to $n$ dimensions. The exponent is now a quadratic form defined by a symmetric, positive-definite matrix $A$.
$$
Z(A) = \int_{\mathbb{R}^n} d^n\vec{x} \, e^{-\frac{1}{2} \vec{x}^T A \vec{x}}
$$
Since $A$ is symmetric, it can be diagonalized by an orthogonal matrix $O$ (where $O^T O = I$), such that $A = O^T \Lambda O$, where $\Lambda$ is a diagonal matrix of the positive eigenvalues $\lambda_i$ of $A$.

We perform a change of variables $\vec{y} = O\vec{x}$, so $\vec{x} = O^T\vec{y}$. The Jacobian of this transformation is $|\det(O^T)| = 1$. The exponent becomes:
$$
\vec{x}^T A \vec{x} = (O^T\vec{y})^T (O^T \Lambda O) (O^T\vec{y}) = \vec{y}^T O O^T \Lambda O O^T \vec{y} = \vec{y}^T \Lambda \vec{y} = \sum_{i=1}^n \lambda_i y_i^2
$$
The integral separates into a product of $n$ one-dimensional Gaussian integrals:
$$
Z(A) = \int_{\mathbb{R}^n} d^n\vec{y} \, e^{-\frac{1}{2}\sum_i \lambda_i y_i^2} = \prod_{i=1}^n \int_{-\infty}^{+\infty} e^{-\frac{\lambda_i y_i^2}{2}} dy_i = \prod_{i=1}^n \sqrt{\frac{2\pi}{\lambda_i}}
$$
Since $\det(A) = \det(O^T \Lambda O) = \det(\Lambda) = \prod \lambda_i$, we get the final result.

> **⑧ The Multidimensional Gaussian Integral**
> $$
> \int_{\mathbb{R}^n} d^n\vec{x} \, e^{-\frac{1}{2}\vec{x}^T A \vec{x}} = \frac{(2\pi)^{n/2}}{\sqrt{\det A}}
> $$

**Exercise:** Using formula **⑧**, show that $\int_{-\infty}^{\infty}\int_{-\infty}^{\infty} dx_1 dx_2 \, e^{-\frac{3}{2}(x_1^2+x_2^2) + x_1x_2} = \frac{\pi}{\sqrt{2}}$.

Solution:

First, we write the exponent in the matrix form $-\frac{1}{2}\vec{x}^T A \vec{x}$:
$$ -\frac{3}{2}(x_1^2+x_2^2) + x_1x_2 = -\frac{1}{2} (3x_1^2 - 2x_1x_2 + 3x_2^2) = -\frac{1}{2} \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 3 & -1 \\ -1 & 3 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} $$
So the matrix is $A = \begin{pmatrix} 3 & -1 \\ -1 & 3 \end{pmatrix}$. The dimension is $n=2$.
The determinant is $\det(A) = (3)(3) - (-1)(-1) = 9 - 1 = 8$.
Using formula **⑧**, the value of the integral is:
$$ \frac{(2\pi)^{2/2}}{\sqrt{\det A}} = \frac{2\pi}{\sqrt{8}} = \frac{2\pi}{2\sqrt{2}} = \frac{\pi}{\sqrt{2}} $$

### 3.2 The General Multidimensional Integral
As in the 1D case, we can add a linear term $\vec{b}^T \vec{x}$:
$$
\text{⑨} \quad Z(A, \vec{b}) = \int d^n\vec{x} \, e^{-\frac{1}{2}\vec{x}^T A \vec{x} + \vec{b}^T \vec{x}}
$$
We complete the square again. The shift is $\vec{y} = \vec{x} - A^{-1}\vec{b}$. The exponent becomes:
$$
-\frac{1}{2}\vec{y}^T A \vec{y} + \frac{1}{2}\vec{b}^T A^{-1} \vec{b}
$$
The integral becomes:
$$
Z(A, \vec{b}) = e^{\frac{1}{2}\vec{b}^T A^{-1} \vec{b}} \int d^n\vec{y} \, e^{-\frac{1}{2}\vec{y}^T A \vec{y}} = e^{\frac{1}{2}\vec{b}^T A^{-1} \vec{b}} Z(A, 0)
$$
> **⑩ The General Multidimensional Gaussian Integral**
> $$
> \int d^n\vec{x} \, e^{-\frac{1}{2}\vec{x}^T A \vec{x} + \vec{b}^T \vec{x}} = \frac{(2\pi)^{n/2}}{\sqrt{\det A}} e^{\frac{1}{2}\vec{b}^T A^{-1} \vec{b}}
> $$

This allows us to find the characteristic function of a multivariate Gaussian, $p(\vec{x}) \propto e^{-\frac{1}{2}\vec{x}^T A \vec{x}}$, by setting $\vec{b} = i\vec{k}$.

> **⑪ C.F. of the Multivariate Gaussian Distribution**
> $$
> \varphi(\vec{k}) = \langle e^{i\vec{k}^T \vec{x}} \rangle = e^{-\frac{1}{2}\vec{k}^T A^{-1} \vec{k}}
> $$

---

## 4. Correlation Functions and Wick's Theorem

### 4.1 Correlation Functions from the C.F.
From result **⑪**, we see that the inverse of the matrix $A$ in the PDF is directly related to the characteristic function. The derivatives of $\varphi(\vec{k})$ give the correlation functions (or moments).

The **s-point correlation function** is given by:
$$
\text{⑫} \quad \langle x_{i_1} x_{i_2} \dots x_{i_s} \rangle = (-i)^s \left. \frac{\partial^s \varphi(\vec{k})}{\partial k_{i_1} \partial k_{i_2} \dots \partial k_{i_s}} \right|_{\vec{k}=0}
$$
Let's compute the 2-point correlation function:
$$
\begin{aligned}
\langle x_i x_j \rangle &= (-i)^2 \left. \frac{\partial^2}{\partial k_i \partial k_j} e^{-\frac{1}{2}\sum_{l,m} k_l (A^{-1})_{lm} k_m} \right|_{\vec{k}=0} \\
&= -\left. \frac{\partial}{\partial k_i} \left[ -\frac{1}{2} \sum_{l,m} (\delta_{jl}(A^{-1})_{lm}k_m + k_l(A^{-1})_{lm}\delta_{jm}) e^{-\frac{1}{2}\vec{k}^T A^{-1} \vec{k}} \right] \right|_{\vec{k}=0} \\
&= -\left. \frac{\partial}{\partial k_i} \left[ -\sum_m (A^{-1})_{jm}k_m e^{-\frac{1}{2}\vec{k}^T A^{-1} \vec{k}} \right] \right|_{\vec{k}=0} \quad (\text{since } A^{-1} \text{ is symmetric}) \\
&= \left. \left( -(A^{-1})_{ji} e^{-\dots} + (\dots)k_m(\dots) \right) \right|_{\vec{k}=0} \\
&= (A^{-1})_{ij}
\end{aligned}
$$

> **⑬ The 2-Point Correlation Function**
> The matrix $A^{-1}$ is the covariance matrix of the distribution. Its elements are the 2-point correlation functions:
> $$
> \langle x_i x_j \rangle = (A^{-1})_{ij}
> $$

### 4.2 Wick's Theorem
For a zero-mean Gaussian distribution, any correlation function of an odd number of variables is zero due to symmetry. For an even number of variables, we can use a powerful shortcut instead of taking many derivatives.

> **Wick's Theorem**
> The expectation value of a product of an even number, $s$, of zero-mean Gaussian random variables is the sum over all possible distinct pairings of the variables. Each pairing contributes a product of $s/2$ two-point correlation functions.

For example, for four variables:
$$
\langle x_a x_b x_c x_d \rangle = \langle x_a x_b \rangle \langle x_c x_d \rangle + \langle x_a x_c \rangle \langle x_b x_d \rangle + \langle x_a x_d \rangle \langle x_b x_c \rangle
$$
In general:
> **⑭ Wick's Theorem Formula**
> $$
> \langle x_{i_1} x_{i_2} \dots x_{i_s} \rangle = \sum_{\text{all pairings } P} \prod_{(j,k) \in P} \langle x_j x_k \rangle = \sum_{\text{all pairings } P} \prod_{(j,k) \in P} (A^{-1})_{jk}
> $$

**Exercise:** For the distribution defined by $A = \begin{pmatrix} 3 & -1 \\ -1 & 3 \end{pmatrix}$, we found $A^{-1} = \frac{1}{8}\begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix}$. Use Wick's theorem to calculate $\langle x_1^2 x_2^2 \rangle$ and $\langle x_1^4 \rangle$.

Solution:
We have the 2-point functions: $\langle x_1^2 \rangle = (A^{-1})_{11} = 3/8$, $\langle x_2^2 \rangle = (A^{-1})_{22} = 3/8$, and $\langle x_1 x_2 \rangle = (A^{-1})_{12} = 1/8$.

**1. Calculating $\langle x_1^2 x_2^2 \rangle$**
We need to evaluate $\langle x_1 x_1 x_2 x_2 \rangle$. The three possible pairings are:
- Pair the first two $x_1$'s and the two $x_2$'s: $\langle x_1 x_1 \rangle \langle x_2 x_2 \rangle$
- Pair the first $x_1$ with the first $x_2$, and the second $x_1$ with the second $x_2$: $\langle x_1 x_2 \rangle \langle x_1 x_2 \rangle$
- Pair the first $x_1$ with the second $x_2$, and the second $x_1$ with the first $x_2$: $\langle x_1 x_2 \rangle \langle x_1 x_2 \rangle$

Summing them up:
$$
\begin{aligned}
\langle x_1^2 x_2^2 \rangle &= \langle x_1^2 \rangle \langle x_2^2 \rangle + 2 \langle x_1 x_2 \rangle^2 \\
&= \left(\frac{3}{8}\right)\left(\frac{3}{8}\right) + 2\left(\frac{1}{8}\right)^2 \\
&= \frac{9}{64} + \frac{2}{64} = \frac{11}{64}
\end{aligned}
$$

**2. Calculating $\langle x_1^4 \rangle$**
We need to evaluate $\langle x_1 x_1 x_1 x_1 \rangle$. The indices are all the same. Let's label them for clarity: $\langle x_{1a} x_{1b} x_{1c} x_{1d} \rangle$. The pairings are:
- (ab)(cd) $\implies \langle x_1 x_1 \rangle \langle x_1 x_1 \rangle$
- (ac)(bd) $\implies \langle x_1 x_1 \rangle \langle x_1 x_1 \rangle$
- (ad)(bc) $\implies \langle x_1 x_1 \rangle \langle x_1 x_1 \rangle$
All three pairings give the same result.
$$
\langle x_1^4 \rangle = 3 \langle x_1^2 \rangle^2 = 3 \left(\frac{3}{8}\right)^2 = 3 \left(\frac{9}{64}\right) = \frac{27}{64}
$$