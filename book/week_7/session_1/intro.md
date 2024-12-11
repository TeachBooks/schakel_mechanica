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

```{index} Displacement method; demonstration
```

(lesson7.1)=
# Lesson October 14th

During today's lesson it's demonstrated how you to use the displacement method.

## Demonstration extension
Given a structure as shown below:

```{figure} ./intro_data/structure.svg
:align: center

Structure
```

For the displacement method, it's needed to choose one or multiple degrees of freedom which describe the displacement of the full structure. Then, using equilibrium, this displacement can be solved for. In this case, that can be the horizontal and vertical displacement of $\text{S}$. A positive displacement is arbitrarily chosen for both of them:

```{figure} ./intro_data/displaced.svg
:align: center

Displaced structure with assumed $u_\text{B,h}$ and $u_\text{b,v}$
```

This leads to extension of the elements:

- $\Delta L_{\text{AS}} = + u_\text{S,h}$
- $\Delta L_{\text{SB}} = - u_\text{S,h}$

And for element $\text{SC}$ in detail:

```{figure} ./intro_data/displaced_SC.svg
:align: center

Displaced $\text{SC}$
```

- $\Delta L_{\text{SC}} = - \frac{4}{5} u_\text{S,v} - \frac{3}{5} u_\text{S,h}$

Applying the constitutive and kinematic relation $ N = EA \cfrac{\Delta L}{L}$ gives:

- $N_{\text{AS}} = 1000 u_\text{S,h}$
- $N_{\text{SB}} = - 2500 u_\text{S,h}$
- $N_{\text{SC}} = - 800 u_\text{S,h} - 600 u_\text{S,v} $

Now, the equilibrium of node $\text{S}$ can be analysed:

```{figure} ./intro_data/equilibrium_S.svg
:align: center

Free-body-diagram node $\text{S}$
```

- $\Sigma F_\text{h}^\text{S} = 0 \to -N_\text{AS} + N_\text{SB} + \frac{3}{5} N_\text{SC} = 0$
- $\Sigma F_\text{v}^\text{S} = 0 \to 40 + \frac{4}{5} N_\text{SC} = 0$

This gives:

- $u_\text{S,h} = -\cfrac{3}{350} \text{ m} \approx -8.57 \text{ mm}$
- $u_\text{S,v} = \cfrac{193}{2800}  \text{ m} \approx 68.9 \text{ mm}$

```{figure} ./intro_data/displaced_sol.svg
:align: center

Final displaced structure
```

Evaluating our previous expressions for the nodal forces gives:
- $N_{\text{AS}} \approx -8.57 \text{ kN}$
- $N_{\text{SB}} \approx 21.4 \text{ kN}$
- $N_{\text{SC}} = -50 \text{ kN} $

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

EA = sym.nsimplify(5e3)

u_bh, u_bv = sym.symbols('u_bh u_bv')

deltaL_AS = + u_bh
deltaL_SB = - u_bh
deltaL_SC = - u_bv * 4 / 5 - u_bh / 5 * 3

N_AS = EA  * deltaL_AS / 5
N_SB = EA  * deltaL_SB / 2
N_SC = EA  * deltaL_SC / 5

display(N_AS, N_SB, N_SC)

eq1 = sym.Eq(-N_AS + N_SB + N_SC / 5 * 3 , 0)
eq2 = sym.Eq(40 + N_SC / 5 * 4, 0)

sol = sym.solve([eq1, eq2], (u_bh, u_bv))
display(sol)

for k, v in sol.items():
    display(k, v.evalf())   

display('N_AS =', N_AS.subs(sol).evalf())
display('N_SB =', N_SB.subs(sol).evalf())
display('N_SC =', N_SC.subs(sol).evalf())
```

## Demonstration bending
Given a structure as shown below:

```{figure} ./intro_data/structure2.svg
:align: center

Structure
```

Again, it's needed to choose one or multiple degrees of freedom which describe the displacement of the full structure. In this case, that can be the rotation of $\text{D}$. A positive displacement is arbitrarily chosen:

```{figure} ./intro_data/displaced_2.svg
:align: center

Displaced structure with assumed $\varphi_\text{D}$
```

As the nodes will not displace, each element can be analysed using forget-me-nots. The directions of the bending moments are arbitrarily chosen:

```{figure} ./intro_data/elem_AD.svg
:align: center

Isolated element $\text{AD}$
```

The rotation $\varphi$ can be calculated using forget-me-nots as: $\varphi_\text{D} = \cfrac{5M_\text{D}^\text{AD}}{3 EI} + \cfrac{ 15 \cdot 5}{6 EI}$
This can be rewritten as $M_\text{D}^\text{AD} = 72000 \varphi_\text{D} - 7.5 $

Similarly, for the other elements:

```{figure} ./intro_data/DB.svg
:align: center

Isolated element $\text{DB}$
```

$M_\text{D}^\text{DB} = 180000 \varphi_\text{D} - 6 $

```{figure} ./intro_data/DC.svg
:align: center

Isolated element $\text{DC}$
```

$M_\text{D}^\text{DC} = -72000 \varphi_\text{D}$

Now, the equilibrium of node $\text{D}$ can be analysed:

```{figure} ./intro_data/FBD_S.svg
:align: center

Free-body-diagram node $\text{D}$ only showing bending moments
```

$\Sigma T = 0 \to -M_\text{D}^\text{AD} + M_\text{D}^\text{DB} + M_\text{D}^\text{DC} = 0$

This gives $\varphi = \cfrac{5}{9EI} = \cfrac{1}{216000} = 4.63 \cdot 10^{-6} \text{ rad}$

Evaluating our previous expressions for the moments gives:
- $M_\text{D}^{\text{AD}} = -\cfrac{43}{6} \approx -7.17 \text{ kNm}$
- $M_\text{D}^{\text{DB}} = -\cfrac{41}{6} \approx -6.83 \text{ kNm}$
- $M_\text{D}^{\text{DC}} = -\cfrac{1}{3} \approx - 0.333 \text{ kNm} $

This gives the following M-line:

```{figure} ./intro_data/M-line.svg
:align: center

Moment distribution
```

```{code-cell} ipython3
:tags: [remove-cell]

phi = sym.nsimplify(5/9/120e3)
display('phi =', phi)
M_DB = - phi * 180000 - 6
display('M_DB =', M_DB)	
display('M_DB =', M_DB.evalf())
M_DC = -72000 * phi
display('M_DC =', M_DC)
display('M_DC =', M_DC.evalf())
M_AD = 72000 * phi - sym.nsimplify(15/2)
display('M_AD =', M_AD)
display('M_AD =', M_AD.evalf())
```
