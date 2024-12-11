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

```{index} Force method; Class exercise statically indeterminate bending only
```

(lesson5.1)=
# Lesson Monday September 30th

During today's lesson it's demonstrated how you to use the force method for statically indeterminate problems which only involve bending

## Demonstration
Given a structure as shown below:

```{figure} ./intro_data/structure.svg
:align: center

Structure
```

We'll apply the force method, specifically, the 'hoekveranderingsvergelijkingen'.

### Define mechanism compatibility conditions

To apply the 'hoekveranderingsvergelijkingen', we apply hinges, with statically indeterminate moments $M_\text{B}$ and $M_\text{D}$ and compatibility conditions $\varphi _{\text{B}}^{{\text{AB}}} = \varphi _{\text{B}}^{{\text{BD}}} $ and $\varphi _{\text{D}}^{{\text{BD}}} = \varphi _{\text{D}}^{{\text{DC}}}$

```{figure} ./intro_data/statically_determinate.svg
:align: center

Mechanism with compatibility conditions
```

The structure has now become a mechanism, which will lead to rigid body rotations next to the bending. The deformation due to the rigid body rotations of the mechanism can be found as:

```{figure} ./intro_data/mechanism.svg
:align: center

Deformation mechanisms
```

The deformations due to bending can be sketched as follows

```{figure} ./intro_data/bending.svg
:align: center

Deformation due to bending
```

These rotations can be found using the forget-me-nots and the rotations of each of the elements due to the rigid body rotations:

- $ \varphi _{\text{B}}^{{\text{AB}}} = \cfrac{M_\text{B}\cdot 4}{3\cdot 20000} \to \varphi _{\text{B}}^{{\text{AB}}} = \cfrac{M_\text{B}\cdot 2}{30000} $
- $ \varphi _{\text{B}}^{{\text{BD}}} = -\cfrac{M_\text{B}\cdot 4}{3\cdot 20000} - \cfrac{M_\text{D}\cdot 4}{6\cdot 20000} - \cfrac{20 \cdot 4^3}{24 \cdot20000} - \theta \to \varphi _{\text{B}}^{{\text{BD}}} = -\cfrac{M_\text{B}\cdot 2}{30000} - \cfrac{M_\text{D}}{30000} - \cfrac{1}{375} - \theta$
- $ \varphi _{\text{D}}^{{\text{BD}}} = \cfrac{M_\text{B}\cdot 4}{6\cdot 20000} + \cfrac{M_\text{D}\cdot 4}{3\cdot 20000} + \cfrac{20 \cdot 4^3}{24 \cdot20000} - \theta \to \varphi _{\text{D}}^{{\text{BD}}} = \cfrac{M_\text{B}}{30000} + \cfrac{M_\text{D}\cdot 2}{30000} + \cfrac{1}{375} - \theta$
- $ \varphi _{\text{D}}^{{\text{DC}}} = - \cfrac{M_\text{D}\cdot 4 \sqrt{2}}{3\cdot 20000 \sqrt{2}} + \theta \to \varphi _{\text{D}}^{{\text{DC}}} = -\cfrac{M_\text{D}\cdot 2}{30000} + \theta$

### Solve statically indeterminate structure with compatibility conditions and equilibrium

The statically indeterminate forces and unknown rigid body rotation $\theta$ can now be solved. However, with only two compatibility conditions an additional equation is needed. This follows from equilibrium, in which the virtual work formulation is most efficient. Therefore, the mechanisms can be reused:

```{figure} ./intro_data/virtual_work.svg
:align: center

Mechanism for virtual work calculation
```

This leads to the virtual work equations: $\delta A = 0 \to {M_{\text{B}}} \cdot \delta \theta  + 20 \cdot 4 \cdot 2\delta \theta  - {M_{\text{D}}} \cdot \delta \theta  - {M_{\text{D}}} \cdot \delta \theta  = 0 \to {M_{\text{B}}} + 160 - 2{M_{\text{D}}} = 0$

The compatibility conditions are as follows:

- $\varphi _{\text{B}}^{{\text{AB}}} = \varphi _{\text{B}}^{{\text{BD}}} \to \cfrac{M_\text{B}\cdot 2}{30000} = -\cfrac{M_\text{B}\cdot 2}{30000} - \cfrac{M_\text{D}}{30000} - \cfrac{1}{375} - \theta \to \cfrac{M_\text{B}\cdot 4}{30000} + \cfrac{M_\text{D}}{30000} + \cfrac{1}{375} + \theta = 0$
- $\varphi _{\text{D}}^{{\text{BD}}} = \varphi _{\text{D}}^{{\text{DC}}} \to \cfrac{M_\text{B}}{30000} + \cfrac{M_\text{D}\cdot 2}{30000} + \cfrac{1}{375} - \theta = -\cfrac{M_\text{D}\cdot 2}{30000} + \theta \to \cfrac{M_\text{B}}{30000} + \cfrac{M_\text{D}\cdot 4}{30000} + \cfrac{1}{375} - 2\theta = 0$

Solving these 3 equations gives:

- $M_\text{B} = -60 \text{ kNm}$
- $M_\text{D} = 50 \text{ kNm}$
- $\theta = \cfrac{11}{3000} \approx 0.0036667 \text{ rad}$

#### Section force diagrams

Given the solved moments, and $\cfrac{1}{8}\cdot20\cdot4^2 = 40 \text{ kNm}$, the full moment diagram can be drawn:

```{figure} ./intro_data/Mlijn.svg
:align: center
```

The deformation signs for the shear forces follow from the M-line

```{figure} ./intro_data/Mlijn2.svg
:align: center
```

And the sloped give the shear forces themselves:

- $V_\text{AB} = \cfrac{60}{4}= 15 \text{ kN}$
- $V_{\text{B}}^{\text{BD}} = \cfrac{60+75}{2} = 67.5 \text{ kN}$
- $V_\text{D} = \cfrac{75-50}{2} = 12.5 \text{ kN}$
- $V_\text{DC} = \cfrac{50}{4\sqrt{2}} = 6.25\sqrt{2} \text{ kN}$

The intersection of the V-line with $0$, which coincides with the maximum moment can be found with $\cfrac{7.5}{20} = 0.375 \text{ m}$.

This leads to the following shear line:

```{figure} ./intro_data/Vlijn.svg
:align: center
```

#### Displacements

The nodal displacement can be found using the rigid body deformations:

- $u_{x,\text{A}} = \cfrac{11}{3000} \cdot 4 = \cfrac{11}{750} \approx 0.01467 \text{ m}$
- $u_{x,\text{B}} = \cfrac{11}{3000} \cdot 4 = \cfrac{11}{750} \approx 0.01467 \text{ m}$
- $u_{x,\text{D}} = \cfrac{11}{3000} \cdot 4 = \cfrac{11}{750} \approx 0.01467 \text{ m}$
- $u_{z,\text{D}} = \cfrac{11}{3000} \cdot 4 = \cfrac{11}{750} \approx 0.01467 \text{ m}$

This, together with the given direction of curvatures from the M-line gives the following displaced structure:

```{figure} ./intro_data/displacements.svg
:align: center
```

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

M_B, M_D, theta = sym.symbols('M_B M_D theta')

eq1 = sym.nsimplify(sym.Eq(M_B + 160 - 2 * M_D ,0))
eq2 = sym.nsimplify(sym.Eq(M_B * 4 / 30000 + M_D / 30000 + 1 / 375 + theta, 0))
eq3 = sym.nsimplify(sym.Eq(M_B / 30000 + M_D * 4 / 30000 + 1 / 375 - 2*theta, 0))

sol = sym.solve([eq1, eq2, eq3], (M_B, M_D, theta))
display(sol)
sol[theta].evalf()

print(1/8*20*4**2)

(sol[theta] * 4).evalf()
```
