## Which Systems Are We Analyzing?


We are analyzing wall-bounded shear flows in the transitional regime. examples are:

Pipe Flow (cylindrical pipe)
Plane Couette Flow (fluid sheared between two parallel plates moving in opposite directions)
Channel/Poiseuille Flow (pressure-driven flow between two stationary parallel plates)

The laminar state (the smooth, parabolic, or linear velocity profile) is linearly stable to infinitesimal perturbations at all Reynolds numbers ($Re$), but nonlinearly unstable to finite-amplitude perturbations.

turbulence does not arise from a smooth linear instability; it must be "triggered" by a sufficiently large disturbance.

### why study this?
Full Laminar Flow: Perfectly understood. The Navier-Stokes equations yield exact, stable, analytical solutions for these geometries (e.g., the parabolic Hagen-Poiseuille profile for pipe flow).

Fully Developed Turbulence: While still an open problem mathematically, it is largely understood statistically (e.g., Kolmogorov's 1941 theory of energy cascades). It is ubiquitous and robust at high Reynolds numbers.

We study transitions from a state that is completely stable to infinitesimal perturbations into chaos. understand the purely nonlinear mechanisms that create and sustain turbulence.


## Dynamical Systems

we project the infinite-dimensional Navier-Stokes velocity field onto a state space where each point represents an instantaneous 3D fluid velocity field


### How de we know that we get a chaotic saddle in our system?

#### Experiments show:
- sensitivity to initial conditions
- between the laminar and the turbulent states there exists no intermediate state
- and that turbulence is not persistent, i.e., it can decay again, if the observation time is long enough. 
=> chaotic saddle

#### ECS Exact Coherent Structures: exact, time-invariant, or periodic solution to the full, nonlinear Navier-Stokes equations that is unstable. These are 
- Exact Travelling Waves (fixed spacial shape that simply travels downstream)
- Relative Periodic Orbits (RPO) (moving oscillating structure that is periodic with time T while it shifts downstream). It satisfies $x(t + T) = g \cdot x(t)$, where $T$ is the period and $g$ is a symmetry operation (like a spatial shift). unstable periodic orbit (UPO). The lyapunov exponents in the




We find them using a mathematical technique called the Newton-Krylov method.
- You take a snapshot of a turbulent puff from a DNS simulation.
- You feed it into a Newton-Raphson solver adapted for massive, high-dimensional spaces (the Krylov subspace).
- The solver iteratively searches for a state where the flow field repeats itself exactly after some time $T$, or travels downstream at a constant wave speed $c$ without changing shape.

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


### Strong Mixing and Memorylessness

A turbulent patch is a self-sustaining cycle of streamwise vortices and streaks. The nonlinear advection term in the Navier-Stokes equations, $(u \cdot \nabla)u$, causes these vortices to constantly stretch, break down, and reform. This "eddy turnover" scrambles the fluid's kinetic energy distribution very rapidly. This turnover time is the mixing time ($\tau_{mix}$).For the puff to decay, these eddies must accidentally arrange themselves in a specific, rare configuration that fails to extract energy from the mean shear flow.

On the chaotic saddle, trajectories diverge exponentially along unstable directions (positive Lyapunov exponents) and are folded back by the system's boundaries. If you start with a tight cluster of initial conditions, the flow stretches and folds this cluster until it becomes a fine, fractal filament that permeates the entire saddle.

Mathematically, a system with invariant measure $\mu$ is strongly mixing if, for any two measurable regions $A$ and $B$ in the phase space:$$\lim_{t \to \infty} \mu(A \cap \Phi^{-t}(B)) = \mu(A)\mu(B)$$where $\Phi^{-t}(B)$ is the pre-image of $B$ under the flow at time $t$

If you start with a localized cluster of similar initial conditions (region $A$), the chaotic dynamics (stretching and folding via positive Lyapunov exponents) will smear this cluster across the entire chaotic saddle. After the mixing time ($\tau_{mix}$), the proportion of your initial cluster that finds itself inside any region $B$ is simply proportional to the overall volume of $B$. The system has completely "forgotten" that the trajectories started localized in $A$.

saddle is not fully trapping. It has stable manifolds (directions trajectories follow to approach it) and unstable manifolds (directions trajectories follow to leave it)



- The Mixing Time ($\tau_{mix}$): Characterized by the reciprocal of the positive Lyapunov exponents. This is the time it takes for the turbulent eddy dynamics to "scramble" the local phase space.
- The Observation/Decay Time ($\tau_{decay}$): The average lifetime of the turbulent patch before the trajectory escapes the saddle and falls into the laminar state.

Because $\tau_{mix} \ll \tau_{decay}$, the internal chaotic dynamics mix the system rapidly that the fluid effectively "forgets" its initial conditions long before it decays. Consequently, the probability of the trajectory finding the escape route to the laminar state is constant per unit time. exponential survival probability distribution ($P(t) \sim e^{-t/\tau_{decay}}$) = memoryless Poisson process.
=
The Timescale Separation: Because $\tau_{mix} \ll \tau_{decay}$, the trajectory is stretched and folded across the entire saddle much faster than it leaks out through $E$.The Loss of Memory: Because the system is strongly mixing, after a short time $t > \tau_{mix}$, the trajectory is smeared uniformly according to the natural measure of the saddle. Therefore, at any given moment, the probability of the trajectory wandering into the escape hole $E$ is purely a function of the geometric size (measure) of $E$ relative to the saddle, $\mu(E)$.

Since $\mu(E)$ is constant, the system has a constant probability $p$ of escaping per unit time, regardless of where it was $\Delta t$ ago.I

if the probability of surviving one time step is $(1-p)$, the probability of surviving $N$ time steps is $(1-p)^N$. In continuous time, this rigorously yields an exponential survival probability:
$$P(t) = e^{-\gamma t}$$
where $\gamma$ is the escape rate ($\gamma = 1/\tau_{decay}$). An exponential distribution is the unique continuous probability distribution that possesses the memoryless (Markov) property: $P(T > t + s \mid T > s) = P(T > t)$.

### Memorylessness => Stochastic Modelling

Navier-Stokes equations are fully deterministic. But because the internal chaotic dynamics of the subcritical turbulence are strongly mixing on a fast timescale, the macroscopic observable (the survival of the turbulent patch) behaves exactly like a stochastic, memoryless coin toss. 
=> stochatic model


## Directed Percolation 

The Grid/Nodes: The spatial domain is coarse-grained. A single "node" or "site" does not represent a fluid particle. It represents the minimal spatial footprint of a self-sustaining turbulent structure (e.g., a length of $\approx 20$ pipe diameters).

The Time Step: The temporal step $\Delta t$ is chosen to be larger than $\tau_{mix}$ but smaller than $\tau_{decay}$. This ensures that the state of a node at step $N+1$ is statistically independent of its internal configuration at step $N$, preserving the Markov property.

The Rules: At each time step, an active (turbulent) node can either:

- Decay into the absorbing (laminar) state.
- Survive.
- Split/Sprout by infecting a neighboring laminar node.
(you can't get an active node from nothing, because the system is linearly stable for laminar flow)


The dimensionality of the graph is not the same as the fluid domain. Dimension of the percolation graph  = Dimensions in real space where turbulence an spread
Pipe Flow: The flow is confined radially and azimuthally. Turbulence can only spread upstream or downstream. The DP graph is 1D space + 1D time (1+1D DP).

Couette / Channel Flow: The flow is confined between parallel plates but is infinitely wide in the spanwise and streamwise directions. Turbulence can spread in a 2D plane. The DP graph is 2D space + 1D time (2+1D DP).


## What can we predict?

- The Exact Critical Reynolds Number ($Re_c$): The point where the splitting rate exactly matches the decay rate.
- Universal Scaling Exponents: The DP universality class dictates how the "turbulent fraction" (the percentage of the fluid that is turbulent) grows above $Re_c$. For 1+1D DP, the fraction $\rho$ grows as $\rho \propto (Re - Re_c)^\beta$, where the universal constant $\beta \approx 0.276$. Fluids perfectly match this purely theoretical statistical number.
- Spatiotemporal Intermittency: The phase transition is continuous (second-order). At $Re_c$, the whole pipe doesn't instantly become turbulent. Instead, it becomes an intermittent, fluctuating equilibrium of turbulent bands and laminar gaps.











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
- 	Laminar flow: fixed point XXXXXXX
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





apparently, there is no phase space "phase transition" at Re_c. The phase transition is macroscopic and described by Percolation
also at Re > Re_c the chaotic saddles do not become chaotic attractors, rather, the turbulence patches just grow more than they die.
phase transition is macroscopic, not microscopic!
(this is true in large enough domains, in small domains you also get the transition in phase space

























### Timeline of Subcritical Turbulence (Pipe Flow)

#### 1. The Laminar Regime: $0 < Re < Re_{SN}$ ($Re \lesssim 1250$)
* **Fluid Mechanics:** Viscous dissipation completely dominates advection. The Hagen-Poiseuille profile is unconditionally stable. Any disturbance, no matter the amplitude, is damped out.
* **Dynamical Systems:** The phase space is effectively empty. The laminar state is a global attractor. Its basin of attraction is the entire infinite-dimensional space.
* **Percolation Theory:** N/A.

#### 2. The Birth of the Saddle: $Re = Re_{SN}$ ($Re \approx 1250$)
* **Fluid Mechanics:** Advection becomes just strong enough to balance viscosity in a highly specific, localized configuration. The "Self-Sustaining Process" becomes physically possible.
* **Dynamical Systems (What Changes):** A mathematical **Saddle-Node Bifurcation** occurs. Out of nowhere, pairs of Exact Coherent Structures (ECSs) materialize in the phase space. 
    * The "Lower Branch" ECS forms the **Edge of Chaos** (the basin boundary).
    * The "Upper Branch" ECS forms the foundation of the **Chaotic Saddle**.
* **Percolation Theory:** N/A.

#### 3. Subcritical Transient Chaos: $Re_{SN} < Re < Re_c$ ($1250 < Re < 2040$)
* **Fluid Mechanics (What Changes):** You can now trigger localized turbulent "puffs." However, they always eventually decay back to laminar. As $Re$ increases, their characteristic lifetime ($\tau_{decay}$) increases super-exponentially. 
* **Dynamical Systems (What Changes):** A cascade of secondary bifurcations occurs. More and more ECS pairs are born. The chaotic saddle grows incredibly dense and complex. Crucially, the **basin boundary moves closer to the laminar fixed point**, meaning smaller physical disturbances are required to trigger turbulence. 
* **Percolation Theory (What Stays):** We are in the subcritical regime of the graph. The decay probability of a turbulent node is higher than its splitting/infection probability. The macroscopic turbulent fraction $\rho$ is strictly $0$.

#### 4. The Macroscopic Phase Transition: $Re = Re_c$ ($Re \approx 2040$)
* **Fluid Mechanics (What Changes):** Turbulent puffs begin to split (replicate) at the exact same rate that they decay. The flow enters a state of sustained spatiotemporal intermittency.
* **Dynamical Systems (What Stays):** **Absolutely nothing qualitatively changes here.** The local phase space topology does not undergo a bifurcation. The chaotic saddle is still a "leaky" saddle. The Edge of Chaos still exists. 
* **Percolation Theory (What Changes):** This is the Directed Percolation critical point. The spatial spreading rate matches the local decay rate. This is where the statistical memorylessness of the local chaotic saddle perfectly feeds the macroscopic stochastic lattice.

#### 5. Spatiotemporal Intermittency: $Re_c < Re < \approx 2700$
* **Fluid Mechanics (What Changes):** Turbulent puffs begin to merge into expanding "slugs." The pipe is a dynamic mixture of turbulent and laminar bands.
* **Dynamical Systems (What Stays):** If you zoom in on any specific segment of the pipe, the trajectory is still wandering on a transient chaotic saddle. It only survives locally because turbulence is constantly invading from upstream/downstream.
* **Percolation Theory (What Changes):** We are in the supercritical regime. The turbulent fraction $\rho$ grows from $0$ following the universal DP scaling law: $\rho \propto (Re - Re_c)^\beta$ (where $\beta \approx 0.276$ for 1+1D).

#### 6. Fully Developed Turbulence: $Re \gg 2700$
* **Fluid Mechanics:** The intermittent gaps vanish. The flow is uniformly, features-lessly turbulent across the entire domain.
* **Dynamical Systems:** The basin boundary is squeezed microscopically close to the laminar fixed point. The chaotic saddle is so dense and the "escape hole" is so infinitely small that the trajectory effectively never finds it.









papers:

file:///home/grego/Documents/BME/probability/lemoult2016.pdf
Directed percolation phase transition to sustained turbulence in Couette flow



file:///home/grego/Documents/BME/probability/eckhardt2007.pdf



Traveling Waves in Pipe Flow
A family of three-dimensional traveling waves for flow through a pipe of circular cross section is identified. The traveling waves are dominated by pairs of downstream vortices and streaks. They originate in saddle-node bifurcations at Reynolds numbers as low as 1250. All states are immediately unstable. Their dynamical significance is that they provide a skeleton for the formation of a chaotic saddle that can explain the intermittent transition to turbulence and the sensitive dependence on initial
conditions in this shear flow.
(first mathematically proved the existence of the ECS in pipe flow using Newton-Krylov methods)






it's funny that "emergence of turbulence at critical Re" sounds like something that is super fine and you need to look at very microscopically, but a super coarse percolation graph does the trick

what sort of questions can the percolation model answer?
- expansion
- phase transitions
- decay? lifetime? survival? of the patches
-


is direct percolation like percolation on a tree?




















First, explain why this system is truly mixed. I understand that the turbulent part in phase space is a chaotic set, which is unstable. Why is there chaotic mixing or strong mixing? How does it come about? How can I explain it to other people, both in physics and math?
