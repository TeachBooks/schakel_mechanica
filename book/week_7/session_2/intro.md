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

```{index} Displacement method; Class exercise
```

(lesson7.2)=
# Lesson October 16th

During today's lesson you'll work on a complex exercise on the topic of the Displacement method. Please ask your questions regarding the [homework](homework7.2) as well!

## Exercise Displacement method

Given the following structure. Use the horizontal displacement at $\text{D}$ as the degree of freedom (→).

```{figure} intro_data/structure.svg
:align: center
```

1. Find the relation of the normal force in $\text{CD}$ in terms of the degree of freedom $w_\text{D}$.
2. Solve the value of the degree of freedom.
3. Find the bending moment distribution.

````{admonition} Solution assignment 1
:class: tip, dropdown

In terms of the horizontal displacement at $\text{D}$:

- $N_\text{CD} = 45−1500 w_D$
- $N_\text{CD} = 3000 w_D - 11.25$

````

````{admonition} Solution assignment 2
:class: tip, dropdown

$w_D = 1.25 \text{ cm}$ (→)

````

````{admonition} Solution assignment 3
:class: tip, dropdown

```{figure} intro_data/M-line.svg
:align: center
```
````

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

EA, EI, F, L_BE, L_CF, L_EF = sym.symbols('EA EI F L_BE L_CF L_EF')
N_EF = sym.symbols('N_EF')
w_F = sym.symbols('w_F')

#L_BE = 6
#L_CF = 4
EI = 500000
EA = 20000
F = sym.nsimplify(45)
L_EF = sym.nsimplify(10)
L_BE = L_EF/2

Eq1 = sym.Eq(w_F, F * L_EF **3 / (EI) / 3 - N_EF * L_EF **3 / EI / 3)
N_EF_1 = sym.solve(Eq1, N_EF)[0]
display(N_EF_1)

Eq2 = sym.Eq(w_F - N_EF * L_BE / EA , N_EF * L_BE**3 / EI / 3 + L_BE **3 / EI / 3 * sym.nsimplify(45))
N_EF_2 = sym.solve(Eq2, N_EF)[0]
display(N_EF_2)

Eq3 = sym.Eq(N_EF_1, N_EF_2)
w_F_sol = sym.solve(Eq3, w_F)[0]
display(w_F_sol)
display(N_EF_1.subs(w_F, w_F_sol).evalf())
```
