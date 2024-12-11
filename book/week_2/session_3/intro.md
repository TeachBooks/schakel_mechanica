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

```{index} Cables; Class exercise using differential equations and  equilibrium in a specific cross-section
```

(lesson2.3)=
# Lesson Friday September 13th

+++

During today's lesson you'll work on a complex exercise on the topic of Equilibrium relations and cables. Please ask your questions regarding the [homework](homework2.3) as well!

## Exercise Equilibrium relations and cables

Given is the following structure:

```{figure} ./intro_data/cable.svg
:align: center
```

1. Find the displacement halfway using equilibrium in a specific cross-section
2. Find the displacement halfway using the differential equations

Given is the following structure:

```{figure} ./intro_data/beam.svg
:align: center
```

3. Find the moment distribution for the beam.

+++

````{admonition} Solution assignment 1 and 2
:class: tip, dropdown

${w_{\text{C}}} =\cfrac {1}{18} \approx {\text{0}}{\text{.0556}}{\text{ m}}$ ↓
````

````{admonition} Solution assignment 3
:class: tip, dropdown

```{figure} ./intro_data/ans.svg
:align: center
```

$M_\text{BC}\left(x_\text{BC}\right) = - 30 x_\text{BC} \text{  } \left( \text{kNm} \right)$

$M_\text{CA}\left(x_\text{CA}\right) = - \cfrac{5}{12} x_\text{CA}^{3} - 60.0 x_\text{CA} - 120 \text{  }  \left( \text{kNm} \right)$
````

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

x, C_1, C_2, C_3, C_4 = sym.symbols('x C_1 C_2 C_3 C_4')

L, F, q, = sym.symbols('L F q')

L = 4
F = 30
q = 10

q_1 = 0
V_1 = -sym.integrate(q_1, x) + C_1
M_1 = sym.integrate(V_1, x) + C_2

q_2 = sym.nsimplify(q/L*x)
V_2 = -sym.integrate(q_2, x) + C_3
M_2 = sym.integrate(V_2, x) + C_4

eq1 = sym.Eq(V_1.subs(x,0),-F)
eq2 = sym.Eq(M_1.subs(x,0),0)
eq3 = sym.Eq(V_1.subs(x,L),V_2.subs(x,0)+F)
eq4 = sym.Eq(M_1.subs(x,L),M_2.subs(x,0))

sol = sym.solve([eq1,eq2,eq3,eq4],(C_1,C_2,C_3,C_4))
display(sol)

display(M_2.subs(sol).simplify().subs(x,L*3/2))
display(sym.latex(M_1.subs(sol)))
display(sym.latex(M_2.subs(sol)))
```
