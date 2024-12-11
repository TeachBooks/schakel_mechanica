---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.16.1
kernelspec:
  display_name: base
  language: python
  name: python3
---

```{index} Differential equations; demonstration for bending
```

(lesson2.1)=
# Lesson Monday September 9th

During today's lesson it's demonstrated how you to use differential equations to solve structural problems.

## Demonstration
Given a structure as shown below:

```{figure} intro_data/structure.svg
:align: center
```

We can calculate the force distribution and displacements of this structure using differential equations.

First, let's define the segments with continuous loads. This requires splitting the top element $\text{DB}$ into two because the distributed load causes a discontinuity. This leads to four segments:
- $\text{AC}$
- $\text{AD}$
- $\text{DE}$
- $\text{EB}$

Now, each segment can be drawn separately, indicating the loads, coordinate systems, dimensions and section forces at the edges of each segment.

### Element $\text{AC}$

As element is hinged at both ends and is only loaded at its end, it's a [zero-force member](two-force-member). The free-body diagram therefore only includes normal forces:

```{figure} intro_data/FBD_AC.svg
:align: center

Free body diagram element $\text{AC}$
```

As this element is unloaded, the loading equation for this element gives:

$$q_{x,\text{AC}} = 0$$

leading to the equations:

$$ N_\text{AC}\left( x \right) = C_1 $$

$$ u_\text{AC}\left( x \right) = \cfrac{C_1 \cdot x + C_2}{20000} $$

Because of the support at $\text{C}$ the first boundary condition is as follows:

```{math}
:label: BC_1
u_\text{AC} \left(10\right) = 0
```

At $\text{C}$ the normal force is unknown (equilibrium with support reactions).

At $\text{A}$ the extension is unknown as $\text{A}$ can move horizontally this leads to a potential displacement of $\text{A}$ in the longitudinal direction of the element.

The normal force at $\text{A}$ follows from the equilibrium of node $\text{A}$. It's free-body-diagram is:

```{figure} intro_data/FBD_A.svg
:name: FBDA
:align: center

Free body diagram node $\text{A}$
```

Horizontal equilibrium gives the second boundary condition:

```{math}
:label: BC_2
\sum {{{\left. {{F_{\text{h}}}} \right|}^{\text{A}}} = 0}  \to \frac{4}{5} \cdot {N_{{\text{AC}}}} + 150 = 0
```

This element could be solved independently as there are two unknowns (two integration constants) and two equations ({eq}`BC_1` and {eq}`BC_2`).

+++

### Element $\text{AD}$

Again, this element is a [zero-force member](two-force-member). The free-body diagram therefore only includes normal forces:

```{figure} intro_data/FBD_AD.svg
:align: center

Free body diagram element $\text{AD}$
```

As this element is unloaded too, the load equation for this element gives:

$$q_{x,\text{AD}}=0$$

leading to the equations:

$$ N_\text{AD}\left( x \right) = C_3 $$

$$ u_\text{AD}\left( x \right) = \cfrac{C_3 \cdot x + C_4}{20000} $$

Because of the support at $\text{A}$ the first boundary condition is as follows:

```{math}
:label: BC_3
u_\text{AD} \left(9\right) = 0
```

At $\text{D}$ another boundary condition can be identified from the consistency of displacements: the downwards displacement of the top of element $\text{AD}$ must be the same as the downwards displacement of the left of element $\text{DE}$:

```{math}
:label: BC_5
{u_{{\text{AD}}}}\left( 0 \right) = {w_{{\text{DE}}}}\left( 0 \right)
```

And finally, a boundary condition can be formulated as the normal force in $\text{D}$ is in equilibrium with the forces from element $\text{DE}$. The free-body-diagram of $\text{D}$ is:

```{figure} intro_data/FBD_D.svg
:align: center

Free body diagram node $\text{D}$
```

Vertical equilibrium gives:

```{math}
:label: BC_6
\sum {{{\left. {{F_{\text{v}}}} \right|}^{\text{D}}} = 0}  \to {N_{{\text{AD}}}} + V_{\text{D}}^{{\text{DE}}} = 0
```

+++

### Element $\text{DE}$

The free-body diagram of this element is:

```{figure} intro_data/FBD_ED.svg
:align: center

Free body diagram element $\text{ED}$
```

As this element is unloaded, the load equation for this element gives:

$$q_{z,\text{DE}}=0$$

leading to the equations:

$$ V_\text{DE} \left(x\right) = C_5$$

$$ M_\text{DE} \left(x\right) = C_5 \cdot x + C_6 $$

$$ \kappa_\text{DE} \left(x\right) = \cfrac{C_5 \cdot x + C_6}{5000}$$

$$ \varphi_\text{DE} \left(x\right) = \cfrac{\cfrac{1}{2}\cdot C_5 \cdot x^2 + C_6 \cdot x}{5000} + C_7$$

$$ w_\text{DE} \left(x\right) = \cfrac{-\cfrac{1}{6}\cdot C_5 \cdot x^3 - \cfrac{1}{2} C_6 \cdot x^2}{5000} - C_7 \cdot x + C_8$$

Because of the hinge at $\text{D}$, a boundary condition can be formulated as:

```{math}
:label: BC_7
M_\text{DE} \left(0\right) = 0
```

At $\text{E}$ another boundary condition can be identified from the consistency of displacements: both the downwards and rotational displacement of the right of element $\text{DE}$ must be the same as the downwards and rotational displacement of the left of element $\text{BE}$:

```{math}
:label: BC_8
w_\text{DE} \left(4\right) = w_\text{BE} \left(0\right)
```

```{math}
:label: BC_9
\varphi_\text{DE} \left(4\right) = \varphi_\text{EB} \left(0 \right)
```

Finally, there should be consistency with the section forces too, as shown in the free body diagram:

```{figure} intro_data/FBD_E.svg
:align: center

Free body diagram node $\text{E}$
```

Vertical equilibrium gives:

```{math}
:label: BC_10
\sum {{{\left. {{F_{\text{v}}}} \right|}^{\text{E}}} = 0}  \to -{V_{{\text{E}}^\text{DE}}} + V_{\text{E}}^{{\text{BE}}} = 0
```

Moment equilibrium gives:

```{math}
:label: BC_11
\sum {{{\left. {{T}} \right|}_\text{E}^{\text{E}}} = 0}  \to -{M_{{\text{E}}^\text{DE}}} + M_{\text{E}}^{{\text{BE}}} = 0
```

+++

### Element $\text{BE}$

The free-body diagram of this element is:

```{figure} intro_data/FBD_BE.svg
:align: center

Free body diagram element $\text{BE}$
```

As this element is loaded, the load equation for this element gives:

$$q_{z,\text{BE}}=10$$

leading to the equations:

$$ V_\text{BE} \left(x\right) = -10 \cdot x + C_9$$

$$ M_\text{BE} \left(x\right) = -5 \cdot x^2 + C_9 \cdot x + C_10 $$

$$ \kappa_\text{BE} \left(x\right) = \cfrac{-5 \cdot x^2 + C_9 \cdot x + C_10}{5000}$$

$$ \varphi_\text{BE} \left(x\right) = \cfrac{-\cfrac{5}{3} \cdot x^3 + \cfrac{1}{2}\cdot C_9 \cdot x^2 + C_10 \cdot x}{5000} + C_11$$

$$ w_\text{BE} \left(x\right) = \cfrac{\cfrac{5}{12} \cdot x^4 -\cfrac{1}{6}\cdot C_9 \cdot x^3 - \cfrac{1}{2} C_10 \cdot x^2}{5000} - C_11 \cdot x + C_12$$

Because of the support at D, two boundary conditions can be formulated directly:

```{math}
:label: BC_12
\varphi_\text{BE} \left(4\right) = 0
```

```{math}
:label: BC_13
w_\text{BE} \left(4\right) = 0
```

+++

### Solve system of equations

12 boundary conditions have been formulated with 12 integration constants. These can now be solved. You're advised to use your calculator or a symbolic programming tool to solve this.

Filling in the boundary conditions gives:



$$
\begin{align}
\frac{C_{1}}{2000} + C_{2} = 0 \\
\frac{4 C_{1}}{5} + 150 = 0 \\
\frac{9 C_{3}}{20000} + C_{4} = 0 \\
- C_{4} + C_{8} = 0 \\
C_{3} + C_{5} = 0 \\
C_{6} = 0 \\
C_{12} + \frac{4 C_{5}}{1875} + \frac{C_{6}}{625} + 4 C_{7} - C_{8} = 0 \\
C_{11} - \frac{C_{5}}{625} - \frac{C_{6}}{1250} - C_{7} = 0 \\
- C_{5} + C_{9} = 0 \\
C_{10} - 4 C_{5} - C_{6} = 0 \\
\frac{C_{10}}{1250} + C_{11} + \frac{C_{9}}{625} - \frac{8}{375} = 0 \\
- \frac{C_{10}}{625} - 4 C_{11} + C_{12} - \frac{4 C_{9}}{1875} + \frac{8}{375} = 0 \\
\end{align}
$$

Solving this gives:

$$
\begin{align}
C_{1} = - \frac{375}{2} \\ 
C_{2} = \frac{3}{32}\\
C_{3} = - \frac{1792}{415}\\
C_{4} = \frac{504}{259375}\\ 
C_{5} = \frac{1792}{415} \\
C_{6} = 0\\
C_{7} = - \frac{4904}{778125} \\
C_{8} = \frac{504}{259375}\\ 
C_{9} = \frac{1792}{415} \\
C_{10} = \frac{7168}{415}\\ 
C_{11} = \frac{472}{778125}\\ 
C_{12} = \frac{2792}{155625}\\
\end{align}
$$

Now, the full force distribution and displacements of the structure has been solved. For example the moment distribution in $\text{BE}$ is $- 5 \cdot x^{2} + \cfrac{1792}{415} \cdot x + \cfrac{7168}{415}$ which can be plotted as:

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym
import numpy as np
import matplotlib.pyplot as plt

%config InlineBackend.figure_formats = ['svg']
sym.init_printing()

x = sym.symbols('x')

q = 10 
EI = 5000 
EA = 20000 
F = 150

q_AC = 0
q_AD = 0
q_CD = 0
q_DE = 0
q_EB = q

C_1, C_2 = sym.symbols('C_1 C_2')
C_3, C_4 = sym.symbols('C_3 C_4')
C_5, C_6, C_7, C_8 = sym.symbols('C_5 C_6 C_7 C_8')
C_9, C_10, C_11, C_12 = sym.symbols('C_9 C_10 C_11 C_12')

N_AC = -sym.integrate(q_AC, x) + C_1
eps_AC = N_AC/EA
u_AC = sym.integrate(eps_AC, x) + C_2

N_AD = -sym.integrate(q_AD, x) + C_3
eps_AD  = N_AD/EA
u_AD = sym.integrate(eps_AD, x) + C_4

V_DE = -sym.integrate(q_DE, x) + C_5
M_DE = sym.integrate(V_DE, x) + C_6
kappa_DE = M_DE/EI
phi_DE = sym.integrate(kappa_DE, x) + C_7
w_DE = -sym.integrate(phi_DE, x) + C_8

V_EB = -sym.integrate(q_EB, x) + C_9
M_EB = sym.integrate(V_EB, x) + C_10
kappa_EB = M_EB/EI
phi_EB = sym.integrate(kappa_EB, x) + C_11
w_EB = -sym.integrate(phi_EB, x) + C_12

eq1 = sym.Eq(w_EB.subs(x,4),0)
eq2 = sym.Eq(phi_EB.subs(x,4),0)
eq3 = sym.Eq(w_EB.subs(x,0)-w_DE.subs(x,4),0)
eq4 = sym.Eq(phi_EB.subs(x,0)-phi_DE.subs(x,4),0)
eq5 = sym.Eq(M_EB.subs(x,0) - M_DE.subs(x,4),0)
eq6 = sym.Eq(V_EB.subs(x,0) - V_DE.subs(x,4),0)
eq7 = sym.Eq(V_DE.subs(x,0) + N_AD.subs(x,0),0)
eq8 = sym.Eq(M_DE.subs(x,0),0)
eq9 = sym.Eq(w_DE.subs(x,0)-u_AD.subs(x,0),0)
eq10 = sym.Eq(F + N_AC.subs(x,0)/5*4,0)
eq11 = sym.Eq(u_AD.subs(x,9),0)
eq12 = sym.Eq(u_AC.subs(x,10),0)

display(eq1,eq2,eq3,eq4,eq5,eq6,eq7,eq8,eq9,eq10,eq11,eq12)
print(sym.latex(eq11))
print(sym.latex(eq12))
print(sym.latex(eq10))
print(sym.latex(eq9))
print(sym.latex(eq7))
print(sym.latex(eq8))
print(sym.latex(eq3))
print(sym.latex(eq4))
print(sym.latex(eq6))
print(sym.latex(eq5))
print(sym.latex(eq2))
print(sym.latex(eq1))
```

```{code-cell} ipython3
:tags: [remove-cell]

sol = sym.solve([eq1,eq2,eq3,eq4,eq5,eq6,eq7,eq8,eq9,eq10,eq11,eq12],(C_1,C_2,C_3,C_4,C_5,C_6,C_7,C_8,C_9,C_10,C_11,C_12))
display(sol)
sym.latex(sol)
```

```{code-cell} ipython3
:tags: [remove-input]

M_numpy = sym.lambdify(x, M_EB.subs(sol))
x_numpy = np.linspace(0,4,100)
plt.figure()
plt.plot(x_numpy,M_numpy(x_numpy))
plt.xlabel('$x$')
plt.ylabel('$M_{EB}$');
ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
ax.spines['bottom'].set_position('zero')
ax.spines['left'].set_position('zero')
ax.invert_yaxis()
```

### Solve using digital tools
To solve the system of equations using numerical tools, you can write down the equations as a matrix formulation $Ax=b$ which can easily be solved by ie. your graphical calculator or python.

$$\left[\begin{array}{ccccccccccccc}0 & 0 & \frac{1}{2000} & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\0 & 0 & \frac{4}{5} & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\\frac{9}{20000} & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\1 & 0 & \frac{3}{5} & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1\\0 & -1 & 0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0\\1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\0 & 0 & 0 & 0 & \frac{4}{1875} & \frac{1}{625} & 4 & -1 & 0 & 0 & 0 & 1 & 0\\0 & 0 & 0 & 0 & - \frac{1}{625} & - \frac{1}{1250} & -1 & 0 & 0 & 0 & 1 & 0 & 0\\0 & 0 & 0 & 0 & -1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0\\0 & 0 & 0 & 0 & -4 & -1 & 0 & 0 & 0 & 1 & 0 & 0 & 0\\0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & \frac{1}{625} & \frac{1}{1250} & 1 & 0 & 0\end{array}\right] \left[ \begin{array} {ccccccccccccc}C_1\\C_2\\C_3\\C_4\\C_5\\C_6\\C_7\\C_8\\C_{10}\\C_{11}\\C_{12}\end{array}\right] = \left[\begin{matrix}0\\-150\\0\\0\\0\\0\\0\\0\\0\\0\\0\\\frac{8}{375}\end{matrix}\right]$$

```{code-cell} ipython3
:tags: [remove-cell]

A,b = sym.linear_eq_to_matrix((eq11,eq12,eq10,eq9,eq7,eq8,eq3,eq4,eq6,eq5,eq2,eq1),(C_1,C_2,C_3,C_4,C_5,C_6,C_7,C_8,C_9,C_10,C_11,C_12))
print(sym.latex(A))
print(sym.latex(b))
A = np.array(A).astype(np.float64)
b = np.array(b).astype(np.float64)
```

```{code-cell} ipython3
np.linalg.solve(A,b)
```

Alternatively, a symbolic programming language can be used to solve the equations exactly. As an example the [`sympy`](https://docs.sympy.org/latest/index.html) package in `Python` is used:

```{code-cell} ipython3
import sympy as sym
sym.init_printing()

x = sym.symbols('x')

q = 10 
EI = 5000 
EA = 20000 
F = 150

q_AC = 0
q_AD = 0
q_CD = 0
q_DE = 0
q_EB = q

C_1, C_2 = sym.symbols('C_1 C_2')
C_3, C_4 = sym.symbols('C_3 C_4')
C_5, C_6, C_7, C_8 = sym.symbols('C_5 C_6 C_7 C_8')
C_9, C_10, C_11, C_12 = sym.symbols('C_9 C_10 C_11 C_12')

N_AC = -sym.integrate(q_AC, x) + C_1
eps_AC = N_AC/EA
u_AC = sym.integrate(eps_AC, x) + C_2

N_AD = -sym.integrate(q_AD, x) + C_3
eps_AD  = N_AD/EA
u_AD = sym.integrate(eps_AD, x) + C_4

V_DE = -sym.integrate(q_DE, x) + C_5
M_DE = sym.integrate(V_DE, x) + C_6
kappa_DE = M_DE/EI
phi_DE = sym.integrate(kappa_DE, x) + C_7
w_DE = -sym.integrate(phi_DE, x) + C_8

V_EB = -sym.integrate(q_EB, x) + C_9
M_EB = sym.integrate(V_EB, x) + C_10
kappa_EB = M_EB/EI
phi_EB = sym.integrate(kappa_EB, x) + C_11
w_EB = -sym.integrate(phi_EB, x) + C_12

eq1 = sym.Eq(u_AC.subs(x,10),0)
eq2 = sym.Eq(F + N_AC.subs(x,0)/5*4,0)
eq3 = sym.Eq(u_AD.subs(x,9),0)
eq4 = sym.Eq(w_DE.subs(x,0)-u_AD.subs(x,0),0)
eq5 = sym.Eq(V_DE.subs(x,0) + N_AD.subs(x,0),0)
eq6 = sym.Eq(M_DE.subs(x,0),0)
eq7 = sym.Eq(w_EB.subs(x,0)-w_DE.subs(x,4),0)
eq8 = sym.Eq(phi_EB.subs(x,0)-phi_DE.subs(x,4),0)
eq9 = sym.Eq(V_EB.subs(x,0) - V_DE.subs(x,4),0)
eq10 = sym.Eq(M_EB.subs(x,0) - M_DE.subs(x,4),0)
eq11 = sym.Eq(phi_EB.subs(x,4),0)
eq12 = sym.Eq(w_EB.subs(x,4),0)

sol = sym.solve([eq1,eq2,eq3,eq4,eq5,eq6,eq7,eq8,eq9,eq10,eq11,eq12],(C_1,C_2,C_3,C_4,C_5,C_6,C_7,C_8,C_9,C_10,C_11,C_12))
display(sol)
```
