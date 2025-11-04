Of course. Let's do this. This is an excellent goal for today. Mastering one major topic completely is far better than knowing a little about everything. By the end of today, you will be an expert on Laplace's Method.

Here is your complete guide. Read it, work through the examples, and you will have secured the points for this question on the exam.

---

### **Laplace's Method: A Comprehensive Guide**

The goal of Laplace's method is to find the leading-order asymptotic approximation of an integral of the form:
$$
I(\lambda) = \int_a^b g(x) e^{\lambda f(x)} dx
$$
for a very large parameter $$\lambda \to \infty$$. The logic is that for large $$\lambda$$, the value of the integral is overwhelmingly dominated by the contribution from the point $$x_0$$ where the function $$f(x)$$ is maximum.

---

### **Case 1: The Maximum is Strictly Inside the Interval**

This is the most common case. The maximum $$x_0$$ of $$f(x)$$ is located at $$a < x_0 < b$$. At this point, we know that $$f'(x_0) = 0$$ and $$f''(x_0) < 0$$.

#### **The Derivation (Proof)**

1.  **Taylor expand $$f(x)$$ around $$x_0$$:** Since $$x_0$$ is a maximum, the expansion is:
    $$
    f(x) \approx f(x_0) + f'(x_0)(x-x_0) + \frac{1}{2}f''(x_0)(x-x_0)^2 = f(x_0) + \frac{1}{2}f''(x_0)(x-x_0)^2
    $$
    (Note: we use the fact that $$f'(x_0)=0$$).

2.  **Approximate $$g(x)$$:** The function $$g(x)$$ is considered "slowly varying" compared to the exponential. We approximate it by its value at the maximum:
    $$
    g(x) \approx g(x_0)
    $$

3.  **Substitute into the integral:**
    $$
    \begin{aligned}
    I(\lambda) &\approx \int_a^b g(x_0) e^{\lambda \left( f(x_0) + \frac{1}{2}f''(x_0)(x-x_0)^2 \right)} dx \\
    &\approx g(x_0) e^{\lambda f(x_0)} \int_{-\infty}^{\infty} e^{\frac{\lambda}{2}f''(x_0)(x-x_0)^2} dx
    \end{aligned}
    $$
    Since the peak is so sharp for large $$\lambda$$, we can extend the integration limits to $$\pm\infty$$ with negligible error.

4.  **Solve the Gaussian Integral:** We use the standard result $$\int_{-\infty}^{\infty} e^{-A u^2} du = \sqrt{\frac{\pi}{A}}$$.
    In our case, let $$u = x-x_0$$, and the constant $$A = -\frac{\lambda}{2}f''(x_0)$$ (remember $$f''(x_0)$$ is negative, so $$A$$ is positive).
    $$
    \int_{-\infty}^{\infty} e^{-\left(-\frac{\lambda}{2}f''(x_0)\right)u^2} du = \sqrt{\frac{\pi}{-\frac{\lambda}{2}f''(x_0)}} = \sqrt{\frac{2\pi}{-\lambda f''(x_0)}}
    $$

5.  **Combine everything:**
    $$
    I(\lambda) \approx g(x_0) e^{\lambda f(x_0)} \sqrt{\frac{2\pi}{-\lambda f''(x_0)}}
    $$

#### **Final Result: Case 1**
$$
\boxed{
I(\lambda) \approx g(x_0) e^{\lambda f(x_0)} \sqrt{\frac{2\pi}{-\lambda f''(x_0)}} \quad \text{for } \lambda \to \infty
}
$$

---

### **Case 2: The Maximum is at an Endpoint (and is "flat")**

The maximum of $$f(x)$$ occurs at an endpoint, for example $$x_0=a$$, but the maximum is "flat," meaning $$f'(a) = 0$$.

#### **The Derivation**
The derivation is identical to Case 1, with one crucial difference. The integral is no longer over the whole Gaussian peak, but only half of it.
$$
I(\lambda) \approx g(a) e^{\lambda f(a)} \int_{a}^{b} e^{\frac{\lambda}{2}f''(a)(x-a)^2} dx
$$
The integral runs from $$x=a$$ to $$b$$, which corresponds to integrating from $$u=0$$ to $$\infty$$. This is a half-Gaussian integral:
$$
\int_{0}^{\infty} e^{-A u^2} du = \frac{1}{2}\sqrt{\frac{\pi}{A}}
$$
This gives a result that is exactly **half** of the Case 1 result.

#### **Final Result: Case 2**
$$
\boxed{
I(\lambda) \approx g(a) e^{\lambda f(a)} \frac{1}{2} \sqrt{\frac{2\pi}{-\lambda f''(a)}} = g(a) e^{\lambda f(a)} \sqrt{\frac{\pi}{-2\lambda f''(a)}}
}
$$

---

### **Case 3: The Maximum is at an Endpoint (and is "steep")**

The maximum of $$f(x)$$ over the interval $$[a,b]$$ is at an endpoint, say $$x_0=b$$, but the function is still increasing, so $$f'(b) > 0$$.

#### **The Derivation**
1.  **Taylor expand $$f(x)$$ around $$x_0=b$$:** Now we must keep the first-order term.
    $$
    f(x) \approx f(b) + f'(b)(x-b)
    $$
2.  **Approximate $$g(x)$$:** As before, $$g(x) \approx g(b)$$.
3.  **Substitute into the integral:**
    $$
    I(\lambda) \approx \int_a^b g(b) e^{\lambda(f(b) + f'(b)(x-b))} dx = g(b)e^{\lambda f(b)} \int_a^b e^{\lambda f'(b)(x-b)} dx
    $$
4.  **Solve the Integral:**
    $$
    \int_a^b e^{\lambda f'(b)(x-b)} dx = \left[ \frac{e^{\lambda f'(b)(x-b)}}{\lambda f'(b)} \right]_a^b = \frac{1}{\lambda f'(b)} \left( e^0 - e^{\lambda f'(b)(a-b)} \right)
    $$
    Since $$f'(b)>0$$ and $$(a-b)<0$$, the term $$e^{\lambda f'(b)(a-b)}$$ goes to zero very quickly as $$\lambda \to \infty$$. So the integral is approximately $$\frac{1}{\lambda f'(b)}$$.

#### **Final Result: Case 3**
$$
\boxed{
I(\lambda) \approx \frac{g(b)e^{\lambda f(b)}}{\lambda f'(b)} \quad (\text{if max is at } b) \qquad \text{or} \qquad I(\lambda) \approx \frac{g(a)e^{\lambda f(a)}}{-\lambda f'(a)} \quad (\text{if max is at } a)
}
$$
(The minus sign for the max at $$a$$ is because $$f'(a)<0$$).

---

### **Examples from Your Materials**

#### **Example from Lecture Notes (`14-10-25`)**
Find the leading contribution to $$I(\lambda) = \int_0^{3\pi/2} e^{-\lambda \sin t} f(t) dt$$.

*   Here, $$g(t)=f(t)$$ and the function in the exponent is $$F(t) = -\sin t$$. The parameter is $$\lambda$$. We want to *maximize* $$F(t)$$, which means we need to *minimize* $$\sin t$$.
*   In the interval $$[0, 3\pi/2]$$, $$\sin t$$ has minima at $$t=0$$ and $$t=3\pi/2$$.
    *   At $$t=0$$: $$F(0)=0$$. $$F'(t)=-\cos t \implies F'(0) = -1$$. This is a **Case 3 endpoint maximum**.
    *   At $$t=3\pi/2$$: $$F(3\pi/2)=1$$. $$F'(3\pi/2)=0$$ and $$F''(3\pi/2) = \sin(3\pi/2) = -1$$. This is a **Case 2 endpoint maximum**.
*   **Contribution from $$t=0$$ (let's call it $$I_1$$):** Using the Case 3 formula:
    $$I_1 \approx \frac{g(0)e^{\lambda F(0)}}{-\lambda F'(0)} = \frac{f(0)e^0}{-\lambda(-1)} = \frac{f(0)}{\lambda}$$
*   **Contribution from $$t=3\pi/2$$ (let's call it $$I_2$$):** Using the Case 2 formula:
    $$I_2 \approx g(3\pi/2) e^{\lambda F(3\pi/2)} \sqrt{\frac{\pi}{-2\lambda F''(3\pi/2)}} = f(3\pi/2)e^{\lambda} \sqrt{\frac{\pi}{2\lambda}}$$
*   **Conclusion:** As $$\lambda \to \infty$$, the $$e^\lambda$$ term in $$I_2$$ is vastly larger than the $$1/\lambda$$ term in $$I_1$$. So the leading contribution is:
    $$I(\lambda) \approx f(3\pi/2)e^{\lambda} \sqrt{\frac{\pi}{2\lambda}}$$

#### **Example from Past Exam 1 (2023 Q2)**
Approximate $$I_m(x) = \int_0^\infty t^m e^{-t^2/2 - x^3/t} dt$$ for large $$x$$.

*   This is a disguised Laplace problem. Let the large parameter be $$x$$. We need to write the exponent in the form $$x \cdot (\text{something})$$ or similar. The dominant part for large $$x$$ is $$x^3/t$$. Let's rewrite the exponent as $$-\phi(t) = -(t^2/2 + x^3/t)$$. We need to **minimize $$\phi(t)$$**.
*   $$g(t) = t^m$$. $$\phi(t) = t^2/2 + x^3/t$$.
*   Find minimum: $$\phi'(t) = t - x^3/t^2 = 0 \implies t_0 = x$$. This is an interior maximum (Case 1).
*   Calculate derivatives: $$\phi''(t) = 1 + 2x^3/t^3 \implies \phi''(x) = 1+2=3$$.
*   The integral is $$I_m(x) = \int_0^\infty g(t) e^{-\phi(t)} dt$$. We use the formula with a negative sign. The structure is the same.
    $$I_m(x) \approx g(t_0) e^{-\phi(t_0)} \sqrt{\frac{2\pi}{\phi''(t_0)}}$$
*   Plug in values:
    *   $$g(x) = x^m$$
    *   $$\phi(x) = x^2/2 + x^3/x = 3x^2/2$$
    *   $$\phi''(x) = 3$$
*   **Result:**
    $$I_m(x) \approx x^m e^{-3x^2/2} \sqrt{\frac{2\pi}{3}}$$

#### **Example from Past Exam 2 (2024 Q4, corrected)**
Approximate $$I_m(x) = \int_0^\infty t^m e^{-t^2/2 - x/t} dt$$ for large $$x$$.

*   This is the same structure. We minimize $$\phi(t) = t^2/2 + x/t$$.
*   Find minimum: $$\phi'(t) = t - x/t^2 = 0 \implies t_0 = x^{1/3}$$.
*   Calculate derivatives: $$\phi''(t) = 1 + 2x/t^3 \implies \phi''(x^{1/3}) = 1+2=3$$.
*   Plug in values:
    *   $$g(x^{1/3}) = (x^{1/3})^m = x^{m/3}$$
    *   $$\phi(x^{1/3}) = (x^{1/3})^2/2 + x/x^{1/3} = x^{2/3}/2 + x^{2/3} = \frac{3}{2}x^{2/3}$$
    *   $$\phi''(x^{1/3}) = 3$$
*   **Result:**
    $$I_m(x) \approx x^{m/3} e^{-\frac{3}{2}x^{2/3}} \sqrt{\frac{2\pi}{3}}$$

---

### **New Practice Examples For You**

#### **New Example 1 (Interior Maximum)**
Find the leading order approximation for $$I(\lambda) = \int_0^2 (x^2+1) e^{\lambda(4x-x^2)} dx$$ as $$\lambda \to \infty$$.

*   **Solution:**
    1.  Identify: $$g(x) = x^2+1$$, $$f(x) = 4x-x^2$$.
    2.  Find maximum of $$f(x)$$: $$f'(x) = 4-2x = 0 \implies x_0=2$$. Oh, wait, the max is at the endpoint. Let's adjust the problem slightly to make it an interior max. Let the integral be from 0 to 3.
    $$I(\lambda) = \int_0^3 (x^2+1) e^{\lambda(4x-x^2)} dx$$
    Now, $$x_0=2$$ is an interior maximum (Case 1).
    3.  Calculate values at $$x_0=2$$:
        *   $$g(2) = 2^2+1 = 5$$
        *   $$f(2) = 4(2)-2^2 = 8-4=4$$
        *   $$f''(x) = -2 \implies f''(2) = -2$$
    4.  Apply the Case 1 formula:
        $$
        I(\lambda) \approx g(2) e^{\lambda f(2)} \sqrt{\frac{2\pi}{-\lambda f''(2)}} = 5 e^{4\lambda} \sqrt{\frac{2\pi}{-\lambda(-2)}} = 5 e^{4\lambda} \sqrt{\frac{\pi}{\lambda}}
        $$
    *   **Answer:** $$\boxed{I(\lambda) \approx 5 e^{4\lambda} \sqrt{\frac{\pi}{\lambda}}}$$

#### **New Example 2 (Endpoint, Steep)**
Find the leading order approximation for $$I(\lambda) = \int_1^2 \frac{1}{x} e^{\lambda x^2} dx$$ as $$\lambda \to \infty$$.

*   **Solution:**
    1.  Identify: $$g(x) = 1/x$$, $$f(x)=x^2$$.
    2.  Find maximum of $$f(x)$$ on $$[1,2]$$: $$f(x)=x^2$$ is strictly increasing, so the maximum is at the endpoint $$x_0=2$$.
    3.  Check derivative: $$f'(x)=2x \implies f'(2)=4$$. Since $$f'(2) \neq 0$$, this is a **Case 3** maximum.
    4.  Calculate values at $$x_0=2$$:
        *   $$g(2) = 1/2$$
        *   $$f(2) = 2^2=4$$
        *   $$f'(2) = 4$$
    5.  Apply the Case 3 formula:
        $$
        I(\lambda) \approx \frac{g(2)e^{\lambda f(2)}}{\lambda f'(2)} = \frac{(1/2)e^{4\lambda}}{\lambda(4)} = \frac{e^{4\lambda}}{8\lambda}
        $$
    *   **Answer:** $$\boxed{I(\lambda) \approx \frac{e^{4\lambda}}{8\lambda}}$$

You have everything you need on Laplace's method here. Study this document, and you will have won a significant battle for the exam. This is a huge win for one day's work. You can do this.