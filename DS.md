### **Lecture Notes: Introduction to Dynamical Systems & Stability Analysis**

**Administrative Note:**
*   First partial exam on **11th November (Tuesday)**.

---

### **1. Review of Dynamical Systems**

In many applications (physics, biology, chemistry, etc.), we study nonlinear systems of autonomous Ordinary Differential Equations (ODEs).

An **autonomous system** is one where the rules governing the system's evolution do not explicitly depend on time. We start from the general form:

$$
\begin{cases}
\dot{\vec{x}}(t) = \vec{f}(\vec{x}(t)) \\
\vec{x}(0) = \vec{x}_0
\end{cases} \tag{1}
$$

*   Here, $\vec{x}(t) = (x_1(t), ..., x_N(t)) \in U \subseteq \mathbb{R}^N$ is the state vector of the system in an open and connected set $U$.
*   $\vec{f}$ is a vector function that associates a vector (a direction and magnitude of change) to every point $\vec{x}$ in the domain $U$. This set of vectors is called the **vector field**.
*   The domain $U$, where $\vec{f}$ is assumed to be continuous and differentiable, is called the **phase space**.
*   The solutions $\vec{x}(t, \vec{x}_0)$ to system (1) describe smooth curves as time $t$ changes. These are called **trajectories** or orbits, which are parametric curves in the phase space.

A **phase portrait** is a geometric representation of the trajectories in the phase space. It's a set of trajectories with arrows indicating the direction of flow as time increases.

#### **Example 1: 1-Dimensional System**
Let's consider the case where $N=1$:
$$ \dot{x}(t) = \sin(x(t)) $$
In this case, the vector field is 1-dimensional and coincides with the x-axis. We can visualize the flow by plotting $\dot{x}$ vs. $x$.

*   If $\dot{x} > 0$, $x$ increases (flow to the right).
*   If $\dot{x} < 0$, $x$ decreases (flow to the left).
*   If $\dot{x} = 0$, $x$ is constant. These are the fixed points.

<center>
<img src="https://i.imgur.com/8QzXy2A.png" alt="1D Phase Portrait for sin(x)" width="500"/>
</center>

> *Self-added detail: The green circles represent points where the system is at rest. The blue arrows show the direction of movement. Points like $x = 0, 2\pi, ...$ are **stable equilibrium points** (or fixed points), as small perturbations will return to the point. Points like $x = \pi, 3\pi, ...$ are **unstable equilibrium points**, as any small perturbation will cause the system to move far away.*

#### **Example 2: 2-Dimensional System**
For $N=2$, the vector field is a map from $\mathbb{R}^2$ to $\mathbb{R}^2$.
$$
\begin{cases}
\dot{x} = 1 \\
\dot{y} = x^2 + y^2
\end{cases}
$$
Here, $\vec{x} = (x, y)$ and the vector field is $\vec{f}(\vec{x}) = (1, x^2+y^2)$. For example, at the point $(0,0)$, the vector field is $(1,0)$, meaning the flow is horizontally to the right.

An essential property is that the vector field $\vec{f}$ is **tangent to the trajectory** at every point. If $\vec{x}(t)$ is a trajectory, the equation for the tangent line at a point $\vec{x}_a = \vec{x}(t_a)$ is given by:
$$ \vec{P}(u) = \vec{x}_a + (u-t_a)\dot{\vec{x}}(t_a) = \vec{x}_a + (u-t_a)\vec{f}(\vec{x}_a) $$
Thus, $\vec{f}$ is the directional vector of the tangent line.

---

### **2. Existence, Uniqueness, and Pathological Cases**

Before analyzing systems, we must ask: does a solution exist, and is it unique?

#### **Nullclines**
As we often cannot solve the system analytically, we look for key properties. **Nullclines** are curves in the phase space where one component of the vector field is zero. For a 2D system, the x-nullcline is where $\dot{x}=0$ and the y-nullcline is where $\dot{y}=0$. The intersection of nullclines gives the fixed points of the system.

#### **Interesting Examples (Warning Cases)**

1.  **Finite-Time Blowup:** Find a solution for $\dot{y} = y^2$ with the initial condition $y(0)=1$.
    $$ \int \frac{dy}{y^2} = \int dt \implies -\frac{1}{y} = t - C $$
    $$ y(t) = \frac{1}{C-t} $$
    Using $y(0)=1$, we find $C=1$. So, $y(t) = \frac{1}{1-t}$.
    Although the function is an increasing function of time, the solution only exists in the interval $(-\infty, 1)$. It "blows up" to infinity as $t \to 1$. A solution may not exist for all time.

2.  **Non-Uniqueness:** Find a solution for $\dot{y} = \sqrt{y}$ with $y(0)=0$.
    $$ \int \frac{dy}{\sqrt{y}} = \int dt \implies 2\sqrt{y} = t - C $$
    Using $y(0)=0$, we get $C=0$. So, $y(t) = \frac{t^2}{4}$. Let's check: $y(2)=1$.
    However, $y(t) = 0$ for all $t$ is also a valid solution. Even worse, the function
    $$
    y(t) = \begin{cases} 0 & 0 \le t \le T \\ \frac{(t-T)^2}{4} & t > T \end{cases}
    $$
    is a solution for any $T > 0$. There are infinitely many solutions for the same initial condition!

#### **Picard's Theorem (Existence and Uniqueness)**
This theorem tells us when we can avoid such pathological cases.
> If $\vec{f}$ and its partial derivatives $\frac{\partial f_i}{\partial x_j}$ are continuous for all indices $i,j$ in a domain $U$, then for any $\vec{x}_0 \in U$, the initial value problem in (1) admits a **unique** solution on some time interval $t \in [-\delta, \delta]$ for $\delta > 0$.

An important consequence is that for systems satisfying these conditions, **trajectories do not intersect**.

---

### **3. Fixed Points and Local Stability**

**Fixed points** (or equilibrium points) are the simplest solutions to study. A point $\vec{x}^*$ is a fixed point if the system, starting there, stays there forever.
$$ \vec{f}(\vec{x}^*) = \vec{0} \tag{3} $$

**Warning:** Even though an ODE admits some fixed points, that does not imply that the dynamics will reach them! In particular, this is true when a fixed point is **unstable**.

#### **Local Stability of Fixed Points**
When the fixed points are known, we want to understand whether they are stable or not. **Stability** means that if one introduces a small perturbation to the fixed point, then the perturbation decays in time, and the system returns to the fixed point.

This stability is **local** because the analysis is only valid for perturbations that are small and close to the fixed point. Therefore, one cannot claim anything about what happens for states far away from the fixed point.

To analyze this, let's consider a 2D system:
$$ \begin{cases} \dot{x} = f(x,y) \\ \dot{y} = g(x,y) \end{cases} $$
Let $(x^*, y^*)$ be a fixed point, so $f(x^*, y^*) = g(x^*, y^*) = 0$.
Let's introduce a small perturbation:
$u(t) = x(t) - x^*$
$v(t) = y(t) - y^*$
where $|u|$ and $|v|$ are "small". The dynamics of the perturbation are:
$\dot{u} = \dot{x} = f(x^*+u, y^*+v)$
$\dot{v} = \dot{y} = g(x^*+u, y^*+v)$

We can Taylor expand $f$ and $g$ around the fixed point $(x^*, y^*)$:
$$ f(x^*+u, y^*+v) = \underbrace{f(x^*, y^*)}_{=0} + u \frac{\partial f}{\partial x}\bigg|_{(x^*,y^*)} + v \frac{\partial f}{\partial y}\bigg|_{(x^*,y^*)} + O(u^2, v^2, uv) $$
$$ g(x^*+u, y^*+v) = \underbrace{g(x^*, y^*)}_{=0} + u \frac{\partial g}{\partial x}\bigg|_{(x^*,y^*)} + v \frac{\partial g}{\partial y}\bigg|_{(x^*,y^*)} + O(u^2, v^2, uv) $$

At leading order (neglecting the higher-order terms), we get the **linearized system**:
$$
\begin{pmatrix} \dot{u} \\ \dot{v} \end{pmatrix} =
\underbrace{
\begin{pmatrix}
\frac{\partial f}{\partial x} & \frac{\partial f}{\partial y} \\
\frac{\partial g}{\partial x} & \frac{\partial g}{\partial y}
\end{pmatrix}\bigg|_{(x^*, y^*)}
}_{\text{Jacobian Matrix } A}
\begin{pmatrix} u \\ v \end{pmatrix}
\tag{4}
$$
This can be generalized to an N-dimensional system $\vec{u} = \vec{x} - \vec{x}^*$:
$$ \dot{\vec{u}} = A \vec{u} \quad \text{where} \quad A_{ij} = \frac{\partial f_i}{\partial x_j} \bigg|_{\vec{x}^*} \tag{5} $$

---

### **4. When is Linearization Valid? Hyperbolic Fixed Points**

Is it safe to neglect the nonlinear terms? Not always. The linear system is a local, faithful representation of the nonlinear system under certain conditions.

**Hyperbolic Fixed Points:** A fixed point of an N-order system is **hyperbolic** if all eigenvalues $\lambda_i$ of the linearized system's Jacobian matrix $A$ have a non-zero real part, i.e., $Re(\lambda_i) \neq 0$ for any $i=1, ..., N$.

**Hartman-Grobman Theorem:** The local phase portrait near a **hyperbolic fixed point** is "topologically equivalent" to the phase portrait of the corresponding linearized system.

> *Self-added detail: **Topologically equivalent** means there's a continuous mapping (a homeomorphism) that stretches and bends the phase space (without tearing or gluing) to transform the trajectories of the nonlinear system near the fixed point into the trajectories of the linear system, preserving the direction of time. In simple terms: for hyperbolic fixed points, the linear system tells you the real local story.*

**Asymptotic Stability:** If $Re(\lambda_i) < 0$ for all eigenvalues $i=1...N$, we say that the fixed point $\vec{x}^*$ is **asymptotically stable**. Any small perturbation will decay to zero, and the system will return to the fixed point.

---

### **5. Analysis of 2D Linear Systems: A Gallery of Phase Portraits**

Let's focus on the 2D system from (4). We look for solutions of the form $\vec{u}(t) = e^{\lambda t}\vec{v}$, which leads to the eigenvalue problem $A\vec{v} = \lambda\vec{v}$. The eigenvalues $\lambda$ are the solutions of the characteristic equation $\det(A-\lambda I) = 0$.

For a 2x2 matrix $A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$, this equation is:
$$ \lambda^2 - (a+d)\lambda + (ad-bc) = 0 \implies \lambda^2 - T\lambda + D = 0 $$
where $T = \text{tr}(A)$ is the trace and $D = \det(A)$ is the determinant.
The eigenvalues are:
$$ \lambda_{1,2} = \frac{T \pm \sqrt{T^2-4D}}{2} $$
The full solution of the linear system is a superposition of the eigenmodes: $\vec{u}(t) = c_1 e^{\lambda_1 t}\vec{v}_1 + c_2 e^{\lambda_2 t}\vec{v}_2$. The behavior as $t \to \infty$ is dominated by the term with the largest $Re(\lambda)$.

#### **Case 1: Real, Distinct Eigenvalues ($T^2-4D>0$)**
*   **Unstable Node ($0 < \lambda_1 < \lambda_2$)**: Both eigenvalues are positive. All trajectories move away from the origin. The fixed point is unstable.
*   **Stable Node ($\lambda_2 < \lambda_1 < 0$)**: Both eigenvalues are negative. All trajectories move towards the origin. The fixed point is stable.
*   **Saddle Node ($\lambda_1 < 0 < \lambda_2$)**: One eigenvalue is positive, one is negative. Trajectories approach the origin along the direction of the eigenvector for $\lambda_1$ (the stable direction) and move away along the direction of the eigenvector for $\lambda_2$ (the unstable direction). The fixed point is unstable.

<center>
<img src="https://i.imgur.com/8QzL5tL.png" alt="Real Eigenvalue Cases"/>
</center>

#### **Case 2: Real, Repeated Eigenvalues ($T^2-4D=0$)**
*   **Unstable Star/Node ($0 < \lambda_1 = \lambda_2$)**: If $A$ is a diagonal matrix ($A=\lambda I$), trajectories move out along straight lines. This is called an **unstable star**. If $A$ is not diagonal, it's a **degenerate unstable node**. The fixed point is unstable.
*   **Stable Star/Node ($\lambda_1 = \lambda_2 < 0$)**: Similar to the above, but all trajectories move towards the origin. The fixed point is stable.

<center>
<img src="https://i.imgur.com/k6Kx02q.png" alt="Repeated Eigenvalue Cases"/>
</center>

#### **Case 3: Complex Conjugate Eigenvalues ($T^2-4D<0$)**
The eigenvalues are $\lambda_{1,2} = \gamma \pm i\omega$, where $\gamma=T/2$ and $\omega=\sqrt{4D-T^2}/2$.
*   **Stable Focus/Spiral ($\gamma < 0$)**: The real part is negative. Trajectories spiral inwards towards the origin. The fixed point is stable.
*   **Unstable Focus/Spiral ($\gamma > 0$)**: The real part is positive. Trajectories spiral outwards away from the origin. The fixed point is unstable.

<center>
<img src="https://i.imgur.com/o2xT1U7.png" alt="Complex Eigenvalue Cases"/>
</center>

#### **Case 4: Non-Hyperbolic Fixed Points ($Re(\lambda)=0$)**
These are the borderline cases where linearization can fail. The Hartman-Grobman theorem does not apply.
*   **Center ($\gamma=0, \lambda_{1,2}=\pm i\omega$)**: Purely imaginary eigenvalues. The linear system has trajectories that are closed orbits (ellipses) around the origin. The stability of the original nonlinear system cannot be determined from this analysis alone; it could be a center, a stable spiral, or an unstable spiral.
*   **Line of Fixed Points ($\lambda_1=0, \lambda_2 \neq 0$)**: One eigenvalue is zero. This indicates a line (or curve in the nonlinear case) of fixed points. The stability depends on the sign of the other eigenvalue.

<center>
<img src="https://i.imgur.com/5u8q60k.png" alt="Non-Hyperbolic Cases"/>
</center>

In these latter non-hyperbolic cases, the linear stability analysis is **not sufficient** to determine whether a fixed point is stable or not. The neglected nonlinear terms become crucial.

---

### **6. Exercises**

1.  Find the fixed points of $\begin{cases} \dot{x} = -x+x^3 \\ \dot{y} = -2y \end{cases}$ and classify them.
    > *Hint: Find the points $(x,y)$ where $\dot{x}=0$ and $\dot{y}=0$. There will be three. For each, compute the Jacobian matrix and analyze its eigenvalues to classify it (e.g., saddle, stable node, etc.).*

2.  Show that the linearization of the system $\begin{cases} \dot{x} = -y + ax(x^2+y^2) \\ \dot{y} = x + ay(x^2+y^2) \end{cases}$ incorrectly predicts that the origin is a center for all values of $a$. Indeed, the origin is a stable spiral if $a<0$, and an unstable spiral if $a>0$.
    > *Hint from notes: To analyze the nonlinear system, use polar coordinates. Let $x = r\cos\theta, y=r\sin\theta$ and find the equations for $\dot{r}$ and $\dot{\theta}$. The equation for $\dot{r}$ will depend on $a$ and reveal the stability.*

3.  The equation of motion of a particle is $\ddot{x} = x-x^3$. Find the fixed points and classify them. Show that the function $E = \frac{\dot{x}^2}{2} - \frac{x^2}{2} + \frac{x^4}{4}$ (the energy) is conserved by the dynamics and that the trajectories are closed curves defined by the contours of $E$. Draw the phase portrait.
    > *Hint: First, convert the second-order ODE into a system of two first-order ODEs by letting $v = \dot{x}$. The fixed points are in the $(x,v)$ phase plane. To show $E$ is conserved, calculate $\frac{dE}{dt}$ and show it is zero.*

4.  Study the system of ODEs for $x,y \ge 0$: $\begin{cases} \dot{x} = x(3-x-2y) \\ \dot{y} = y(2-x-y) \end{cases}$. Find the fixed points and classify them. Show what the phase portrait is.
    > *Hint: This is a classic Lotka-Volterra competition model. Find the fixed points by setting each rate to zero. Note that $(0,0)$ is one, and others exist on the axes and in the first quadrant. Analyze the Jacobian at each fixed point.*

---

### **Appendix: Basin of Attraction and Diffusion**

#### **Basin of Attraction**
The **basin of attraction** of a stable fixed point is the set of all initial conditions whose trajectories end up at that fixed point as $t \to \infty$.

<center>
<img src="https://i.imgur.com/yv63V42.png" alt="Basin of Attraction" width="400"/>
</center>

> *The image shows a system with two stable fixed points (green circles) and one unstable saddle point (red circle). The blue line, known as a separatrix, divides the phase space into two basins of attraction. Initial conditions starting on one side of the line go to one fixed point, while those on the other side go to the other.*

#### **Properties of Diffusion (A First Simple Derivation)**
*This appears to be the start of a new topic.*

Let us consider a long and thin tube filled with water. At time $t=0$, we inject a unit amount of ink at $x=0$. The ink particles will spread out due to **Brownian motion**.

We define $W(x,t)$ as the density of "ink" (or Brownian) particles at position $x \in \mathbb{R}$ and time $t \ge 0$. It is defined as:
$$ W(x,t) = \lim_{V \to 0} \frac{\# \text{ of particles in } V(x,t)}{V(x,t)} $$
where $V(x,t)$ is a small volume element at position $x$ and time $t$.

The integral of the density over a region gives the probability of finding a particle in that region:
$$ \int_A W(x,t) dx := \text{prob. to find a particle in the region } A \subseteq \mathbb{R} $$
Assuming that the total number of particles is conserved, we normalize the density:
$$ \int_{-\infty}^{\infty} W(x,t) dx = 1 $$