## Which Systems Are We Analyzing?


We are analyzing wall-bounded shear flows in the transitional regime. examples are:

Pipe Flow (cylindrical pipe)
Plane Couette Flow (fluid sheared between two parallel plates moving in opposite directions)
Channel/Poiseuille Flow (pressure-driven flow between two stationary parallel plates)

The laminar state (the smooth, parabolic, or linear velocity profile) is linearly stable to infinitesimal perturbations at all Reynolds numbers ($Re$), but nonlinearly unstable to finite-amplitude perturbations.

turbulence does not arise from a linear instability, it requires a sufficiently large disturbance.

### Why study this?
Full Laminar Flow: Perfectly understood. The Navier-Stokes equations have exact, stable, analytical solutions for these geometries (e.g., the parabolic Hagen-Poiseuille profile for pipe flow).

Fully Developed Turbulence: While still an open problem mathematically, it is largely understood statistically (e.g., Kolmogorov's 1941 theory of energy cascades) at high Reynolds numbers.

We study transitions from a state that is completely stable to infinitesimal perturbations into chaos to understand the purely nonlinear mechanisms that create and sustain turbulence.


## Dynamical Systems

We project the infinite-dimensional Navier-Stokes velocity field onto a state space where each point represents an instantaneous 3D fluid velocity field


### How de we know that we get a chaotic saddle in our system?

#### Experiments show:
- sensitivity to initial conditions
- between the laminar and the turbulent states there exists no intermediate state
- turbulence is not persistent, it decays if the observation time is long enough. 

This suggests a chaotic saddle

#### ECS Exact Coherent Structures: exact, time-invariant, or periodic solution to the full, nonlinear Navier-Stokes equations that is unstable. These are:
- Exact Travelling Waves (fixed spacial shape that simply travels downstream). In a co-moving frame it is an unstable fixed point (a saddle point). eigenvalues of the linearized Navier-Stokes operator around this fixed point positive real parts
- Relative Periodic Orbits (RPO) (moving oscillating structure that is periodic with time T while it shifts downstream). Unstable Periodic Orbit (UPO) /* It satisfies $x(t + T) = g \cdot x(t)$, where $T$ is the period and $g$ is a symmetry operation (like a spatial shift). but we work in the symmetry-reduced phase space. The lyapunov exponents in the direction of the flow is 0 (every periodic orbit (that is not a fixed point) has at least one Lyapunov exponent that is exactly zero, and this exponent corresponds to the perturbation tangent to the flow.) and the */



We find ECS using a mathematical technique called the Newton-Krylov method.

/*

1.  Initial Guess: Run a Direct Numerical Simulation (DNS). Monitor the chaotic phase space trajectory. When the phase space becomes recurrent (RPO) or reaches close to 0 speed (indicating closeness to ECS point), save that instantaneous 3D velocity field ($\mathbf{u}_0$) as your initial guess. (We need an initial guess because Krylov solver converges only for good guesses)
2.  Search for a Traveling Wave (TW) or Relative Periodic Orbit (RPO) as a nonlinear root-finding problem: $\mathbf{G}(\mathbf{u}) = \mathbf{0}$ (e.g., state at $t=0$ exactly equals state at $t=T$).
3.  Matrix-Free Solver (GMRES): Standard Newton-Raphson requires building and inverting an impossible $10^6 \times 10^6$ Jacobian matrix. Instead, use the Krylov subspace algorithm (GMRES). GMRES only requires the *effect* of the Jacobian on a vector, which is approximated using tiny, forward-time DNS finite differences. The matrix is never actually built.
4.  Convergence (Proof of Existence): Iterate the GMRES solver to update $\mathbf{u}_0$. When the residual error $\|\mathbf{G}(\mathbf{u})\|$ drops to machine precision (e.g., $10^{-10}$), the mathematical existence of the ECS is rigorously proven.
5.  Proof of Saddle: Feed the exact ECS into an Arnoldi iteration (another matrix-free algorithm) to calculate its leading eigenvalues. Finding eigenvalues with strictly positive real parts proves the ECS has unstable manifolds, classifying it as a topological saddle.
6.  Heteroclinic Tracking: Add an infinitesimal perturbation to the exact ECS along one of its positive eigenvectors. Run the DNS forward. The trajectory will ride the unstable manifold away from the current ECS and crash into the stable manifold of a different ECS, mapping the heteroclinic connections of the chaotic saddle. 

*/



#### Physics and meaning of ECS
ECS is governed by Waleffe's Self-Sustaining Process (SSP)


#### How does phase space look like?

Laminar Flow = Stable Fixed Point (single point). There is a Laminar basin of attraction. If a perturbation is small, it falls back to the origin.

Transient Turbulence (Below Critical $Re_c$) = Chaotic Saddle: When you trigger turbulence below $Re_c$, the trajectory is kicked far from the laminar fixed point onto a chaotic saddle. A saddle has both stable manifolds (directions trajectories follow to approach it) and unstable manifolds (directions they follow to leave it). The trajectory wanders chaotically on this saddle for a finite time, but because it is not an attractor, the trajectory eventually "falls off" along an unstable manifold and is sucked into the laminar fixed point.

dense, tangled web of thousands of different highly unstable ECSs (traveling waves and periodic orbits).
These ECSs are connected by heteroclinic orbits (paths connecting one unstable state to another).
When the fluid is turbulent, the state trajectory is bouncing around this web, visiting the neighborhood of one ECS, being violently repelled along its unstable manifold, and crashing into the neighborhood of another. until it accidentally follows a trajectory that points directly toward the laminar fixed point and escapes the chaptic part

chaotic saddle (like a chaotic attractor) is strictly defined in periodic orbit theory as the closure of the infinite set of Unstable Periodic Orbits (UPOs) embedded within it. A chaotic saddle is built from many (theoretically infinite) ECSs.
The chaotic saddle consists of:
- An infinite, dense set of unstable ECSs (TWs and RPOs).
- The heteroclinic connections between them (the infinite intersections of the unstable manifold of one ECS with the stable manifold of another).


Sustained Turbulence (Above $Re_c$) = Chaotic Attractor (or Expanding Saddle): Above the critical point, the geometry changes. The saddle either undergoes a crisis and becomes a true chaotic attractor, or the spatial spreading of the turbulence outweighs the local decay rate, meaning the "effective" saddle in the spatially extended system never fully empties.

#### Why do we get Saddles and Attractors?

Why infinite-dimensional fluid dynamics collapses onto lower-dimensional manifolds (saddles). Because the system is strictly dissipative. Let $V$ be a volume in the phase space. Liouville's theorem: the rate of change of this volume under the fluid flow equations $\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x})$ is determined by the divergence of the velocity field:

$$\frac{dV}{dt} = \int_V (\nabla \cdot \mathbf{f}) dV$$

For the incompressible Navier-Stokes equations, the kinetic energy is reduced by viscous dissipation ($\nu \nabla^2 \mathbf{u}$). The system is strictly dissipative globally, the trace of the Jacobian is negative ($\nabla \cdot \mathbf{f} < 0$). 
$\frac{dV}{dt} < 0$, all trajectories to contract onto sub-manifolds of zero volume (fixed points, periodic orbits, or chaotic saddles).

### Strong Mixing and Memorylessness

A turbulent patch is a self-sustaining cycle of streamwise vortices and streaks. The nonlinear advection term in the Navier-Stokes equations, $(u \cdot \nabla)u$, causes these vortices to constantly stretch, break down, and reform. This "eddy turnover" scrambles the fluid's kinetic energy distribution very rapidly. This turnover time is the mixing time ($\tau_{mix}$).For the puff to decay, these eddies must accidentally arrange themselves in a specific, rare configuration that fails to extract energy from the mean shear flow.

On the chaotic saddle, trajectories diverge exponentially along unstable directions (positive Lyapunov exponents) and are folded back by the system's boundaries. If you start with a tight cluster of initial conditions, the flow stretches and folds this cluster until it becomes a fine, fractal filament that permeates the entire saddle.

Mathematically, a system with invariant measure $\mu$ is strongly mixing if, for any two measurable regions $A$ and $B$ in the phase space:

$\lim_{t \to \infty} \mu(A \cap \Phi^{-t}(B)) = \mu(A)\mu(B)$

where $\Phi^{-t}(B)$ is the pre-image of $B$ under the flow at time $t$

/*
maybe easier to understand is: 

$\lim_{t \to \infty} \mu(\Phi^{t}(A) \cap  B) = \mu(A)\mu(B)$

which is true for invertible systems like flows generated by Navier-Stokes (but excludes the non-invertible discrete chaotic maps). The Pre-image definition is more common because in measure theory, the pre-image of a measurable set under any measurable function is always guaranteed to be measurable.

*/


If you start with a localized cluster of similar initial conditions (region $A$), the chaotic dynamics (stretching and folding via positive Lyapunov exponents) will smear this cluster across the entire chaotic saddle. After the mixing time ($\tau_{mix}$), the proportion of your initial cluster that finds itself inside any region $B$ is simply proportional to the overall volume of $B$. The system has completely "forgotten" that the trajectories started localized in $A$.

The chaotic saddle is not fully trapping. It has stable manifolds (directions trajectories follow to approach it) and unstable manifolds (directions trajectories follow to leave it)

- The Mixing Time ($\tau_{mix}$): Determined by the reciprocal of the positive Lyapunov exponents. This is the time it takes for the turbulent eddy dynamics to "scramble" the local phase space. A small cluster of initial conditions with diameter $\epsilon$ will diverge exponentially:

$$\delta(t) = \epsilon e^{\lambda_{max} t}$$

Complete mixing occurs when this perturbation stretches to the characteristic length scale of the entire saddle manifold, $L$. Setting $\delta(\tau_{mix}) = L$ gives:

$$\tau_{mix} = \frac{1}{\lambda_{max}} \ln\left(\frac{L}{\epsilon}\right)$$


- The Observation/Decay Time ($\tau_{decay}$): The average lifetime of the turbulent patch before the trajectory escapes the saddle and falls into the laminar state.

In the transitional regime to turbulence $\tau_{mix} \ll \tau_{decay}$ 

/*
$\tau_{mix}$ is roughly constant, while $\tau_{decay}$ grows super-exponentially or exponentially (there is conflicting evidence) fast (because the measure of the chaotic saddles in phase space grows rapidly, while the size of the escape route E remains roughly constant, so it's relative measure $\mu(E)$ shrinks to 0)
*/

The Timescale Separation: Because $\tau_{mix} \ll \tau_{decay}$, the trajectory is stretched and folded across the entire saddle much faster than it leaks out through the escape path E. Because the system is strongly mixing, after a short time $t > \tau_{mix}$, the trajectory is distributed uniformly according to the natural measure of the saddle. Therefore, at any given moment, the probability of the trajectory wandering into the escape hole $E$ is purely a function of the (measure) of $E$ relative to the saddle, $\mu(E)$.

Since $\mu(E)$ is constant, the system has a constant probability $p$ of escaping per unit time, regardless of where it was $\Delta t$ ago. If the probability of surviving one time step is $(1-p)$, the probability of surviving $N$ time steps is $(1-p)^N$. In continuous time, this is an exponential survival probability:
$$P(t) = e^{-\gamma t}$$
where $\gamma$ is the escape rate ($\gamma = 1/\tau_{decay}$). An exponential distribution is the unique continuous probability distribution that possesses the memoryless (Markov) property: 

$P(T > t + s \mid T > s) = P(T > t)$.

The only continuous, non-trivial solution is $P(t) = e^{-\gamma t}$.

### Memorylessness => Stochastic Modelling

Navier-Stokes equations are fully deterministic. But because the internal chaotic dynamics of the subcritical turbulence are strongly mixing on a fast timescale, the macroscopic observable (the survival of the turbulent patch) behaves exactly like a stochastic, memoryless coin toss. 
=> stochatic model


## Directed Percolation 

The Grid/Nodes: The spatial domain is coarse-grained. A single "node" or "site" does not represent a fluid particle. It represents the minimal size of a self-sustaining turbulent structure (a length of $\approx 20$ pipe diameters).

The Time Step: The temporal step $\Delta t$ is chosen to be larger than $\tau_{mix}$ but smaller than $\tau_{decay}$. This ensures that the state of a node at step $N+1$ is statistically independent of its internal configuration at step $N$, preserving the Markov property.

The Rules: At each time step, an active (turbulent) node can either:

- Decay into the absorbing (laminar) state.
- Survive.
- Split/Sprout by infecting a neighboring laminar node.
(you can't get an active node from nothing, because the system is linearly stable for laminar flow)

/*
The dimensionality of the graph is not the same as the fluid domain. Dimension of the percolation graph  = Dimensions in real space where turbulence an spread
Pipe Flow: The flow is confined radially and azimuthally. Turbulence can only spread upstream or downstream. The DP graph is 1D space + 1D time (1+1D DP).

Couette / Channel Flow: The flow is confined between parallel plates but is infinitely wide in the spanwise and streamwise directions. Turbulence can spread in a 2D plane. The DP graph is 2D space + 1D time (2+1D DP).
*/

/*
This is different from a tree, because in DP you can get merging, and space is correlated. In trees, offspring are non-interacting.
*/

## What can we predict?

- Universal Scaling Exponents: The DP universality class dictates how the "turbulent fraction" (the percentage of the fluid that is turbulent) grows above $Re_c$. For 1+1D DP, the fraction $\rho$ grows as $\rho \propto (Re - Re_c)^\beta$, where the universal constant $\beta \approx 0.276$. Fluids perfectly match this purely theoretical statistical number.
- Spatiotemporal Intermittency: The phase transition is continuous (second-order). At $Re_c$, the whole pipe doesn't instantly become turbulent. Instead, it becomes an intermittent, fluctuating equilibrium of turbulent bands and laminar gaps.
- Spatial Correlation Length ($\xi_\perp$): The typical size of a correlated turbulent cluster scales as $\xi_\perp \propto (Re - Re_c)^{-\nu_\perp}$. (For 1+1D DP, $\nu_\perp \approx 1.09$). (the characteristic spatial distance over which fluctuations in the system are statistically correlated.)
- Temporal Correlation Time ($\xi_\parallel$): The typical lifetime of these correlated fluctuations scales as $\xi_\parallel \propto (Re - Re_c)^{-\nu_\parallel}$. (For 1+1D DP, $\nu_\parallel \approx 1.73$). (the macroscopic characteristic "memory" or lifetime of a fluctuation.)
- Laminar Gap Distribution: DP predicts that the probability distribution of finding a laminar gap of length $L$ will follow a pure scale-free power law: $P(L) \propto L^{-\mu_\perp}$ where $\mu_\perp = 2 - \beta / \nu_\perp$.
- Universality and independence from boundary conditions. Plane Couette flow (sheared walls) and Channel flow (pressure-driven) have completely different Navier-Stokes base profiles. They are both 2D+1D DP, so they will have the same universal exponents.

/*
This model doesn't predict the Critical Reynolds Number ($Re_c$): The point where the splitting rate exactly matches the decay rate, but it does define it and help mesaure it experimentally.
*/

#### Universal Scaling Exponents $\beta$

I can't prove this. I can give you an intuition.

Assume no spatial correlations. Mean-Field theory. 
/* In reality, if position x is turbulent, the probability that $x+\delta x$ is also turbulent is extremely high. But we ignore this for now, we show that $\beta$ is 1, and then we re-introduce correlation and show that $\beta$ is less than 1.*/

Define $\rho(t)$ as the fraction of the domain that is turbulent. Let the creation rate of turbulence be $p_b$ (branching) and the decay rate be $p_d$. The macroscopic rate equation is:

$$\frac{d\rho}{dt} = p_b \rho (1 - \rho) - p_d \rho$$

The $(1-\rho)$ term ensures turbulence can only spread to non-turbulent space. Steady state $\frac{d\rho}{dt} = 0$, we find two solutions. Either $\rho = 0$ (the absorbing laminar state), or:

$$\rho = 1 - \frac{p_d}{p_b} \propto (p_b - p_d)^1$$

/* We ignore the 1/p_b term because we care about the behaviour at p_b \approx p_d, and there p_b is a constant. lol. */

This proves that above the critical point ($p_b > p_d$), the turbulent fraction grows continuously. The Mean-Field scaling exponent is strictly $\beta = 1$. 

In a 1-dimensional pipe, spatial fluctuations are severe, which lowers this exponent from the theoretical $1$ to the true $1+1$D DP value of $\beta \approx 0.276$. 

/*
The reason why $\beta$ is smaller when you have spatial correlation is that the Mean-Field assumes a turbulent site is surrounded by an infinite number of neighbors to infect. In 1D space, a turbulent cluster only has two boundaries (left and right) where it can expand into laminar space. The surface area of a 1D cluster is fixed at exactly two points regardless of how large the cluster gets, the cluster is highly vulnerable to local statistical fluctuations.
*/


### What each field gave us

#### Fluid Mechanics:
- foundational model of the system
- deterministic continuous
- The Reynolds number ($Re$)
- boundary conditions
- physical mechanism of energy transfer (the nonlinear advection term $(\mathbf{u} \cdot \nabla)\mathbf{u}$ against viscous dissipation $\nu \nabla^2 \mathbf{u}$).
- DNS

#### Dynamical Systems Theory
- topology of the flow in phase space
- 	Laminar flow: fixed point
- 	Transcient turbulence: chaotic saddle
- stability analysis
- ECS Exact Coherent Structures
- strong mixing and memorylessness
- chaos metrcis: lyapunov exponents and mixing time

Assumptions: finite dimensional manifold can describe infinite dimensional fluid PDE

#### Statistical Mechanics & Percolation Theory
- phase transition
- prediction of Re_c
- universal scaling exponents
- spaciotemporal intermittency exponents

Assumptions: markovian memorylessness & strictly absorbing state (Laminar)



### How does the turbulence profile depend on Re?

#### 1. The Laminar Regime: $0 < Re < Re_{SN}$ ($Re \lesssim 1250$)
* **Fluid Mechanics:** Viscous dissipation completely dominates advection. The Hagen-Poiseuille profile is unconditionally stable. Any disturbance, no matter the amplitude, is damped out.
* **Dynamical Systems:** The phase space is effectively empty. The laminar state is a global attractor. Its basin of attraction is the entire infinite-dimensional space.
* **Percolation Theory:** N/A.

#### 2. Appearance of Chaotic Saddles: $Re = Re_{SN}$ ($Re \approx 1250$)
* **Fluid Mechanics:** Advection becomes just strong enough to balance viscosity in a highly specific, localized configuration. The "Self-Sustaining Process" becomes physically possible.
* **Dynamical Systems (What Changes):** A mathematical **Saddle-Node Bifurcation** occurs. Out of nowhere, pairs of Exact Coherent Structures (ECSs) materialize in the phase space. 
    * The "Lower Branch" ECS forms the **Edge of Chaos** (the basin boundary).
    * The "Upper Branch" ECS forms the foundation of the **Chaotic Saddle**.
* **Percolation Theory:** N/A.

#### 3. Subcritical Transient Chaos: $Re_{SN} < Re < Re_c$ ($1250 < Re < 2040$)
* **Fluid Mechanics (What Changes):** You can now trigger localized turbulent "puffs." However, they always eventually decay back to laminar. As $Re$ increases, their characteristic lifetime ($\tau_{decay}$) increases super-exponentially or exponentially (there is conflicting evidence). 
* **Dynamical Systems (What Changes):** A cascade of secondary bifurcations occurs. More and more ECS pairs are born. The chaotic saddle grows incredibly dense and complex. Crucially, the **basin boundary moves closer to the laminar fixed point**, meaning smaller physical disturbances are required to trigger turbulence. 
* **Percolation Theory (What Stays):** We are in the subcritical regime of the graph. The decay probability of a turbulent node is higher than its splitting/infection probability. The macroscopic turbulent fraction $\rho$ is strictly $0$.

#### 4. The Macroscopic Phase Transition: $Re = Re_c$ ($Re \approx 2040$)
* **Fluid Mechanics (What Changes):** Turbulent puffs begin to split (replicate) at the exact same rate that they decay. The flow enters a state of sustained spatiotemporal intermittency.
* **Dynamical Systems (What Stays):** **nothing qualitatively changes here.**
* **Percolation Theory (What Changes):** This is the Directed Percolation critical point. The spatial spreading rate matches the local decay rate.

#### 5. Spatiotemporal Intermittency: $Re_c < Re < \approx 2700$
* **Fluid Mechanics (What Changes):** Turbulent puffs begin to merge into expanding "slugs." The pipe is a dynamic mixture of turbulent and laminar bands.
* **Dynamical Systems (What Stays):** **nothing qualitatively changes here.**   
* **Percolation Theory (What Changes):** We are in the supercritical regime. The turbulent fraction $\rho$ grows from $0$ following the universal DP scaling law: $\rho \propto (Re - Re_c)^\beta$ (where $\beta \approx 0.276$ for 1+1D).

#### 6. Fully Developed Turbulence: $Re \gg 2700$
* **Fluid Mechanics:** The intermittent gaps vanish. The flow is uniformly, features-lessly turbulent across the entire domain.
* **Dynamical Systems:** The basin boundary is squeezed microscopically close to the laminar fixed point. The chaotic saddle is so dense and the "escape hole" is so infinitely small that the trajectory effectively never finds it.




There is no phase space "phase transition" at Re_c. The phase transition is macroscopic and described by Percolation model. Also at Re > Re_c the chaotic saddles do not become chaotic attractors, rather, the turbulence patches just grow more than they die.
phase transition is macroscopic, not microscopic!
(this is true in large enough domains, in small domains you also get the transition in phase space

Above the $Re-c$ the macroscopic spatial spreading rate of the turbulence exceeds the local decay rate. The fluid sustains turbulence not by altering its local deterministic dynamics into an attractor, but through spatial replication. It is a purely macroscopic effect.





papers:

file:///home/grego/Documents/BME/probability/lemoult2016.pdf
Directed percolation phase transition to sustained turbulence in Couette flow



file:///home/grego/Documents/BME/probability/eckhardt2007.pdf



Traveling Waves in Pipe Flow
A family of three-dimensional traveling waves for flow through a pipe of circular cross section is identified. The traveling waves are dominated by pairs of downstream vortices and streaks. They originate in saddle-node bifurcations at Reynolds numbers as low as 1250. All states are immediately unstable. Their dynamical significance is that they provide a skeleton for the formation of a chaotic saddle that can explain the intermittent transition to turbulence and the sensitive dependence on initial
conditions in this shear flow.
(first mathematically proved the existence of the ECS in pipe flow using Newton-Krylov methods)




A universal transition to turbulence in channel flow

measuring four critical exponents, a universal scaling function and a scaling relation, all in agreement with the (2+1)-dimensional directed percolation universality class.

