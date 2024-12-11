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

```{index} Force method; Class exercise for frame structures
```

(lesson6.1)=
# Lesson October 7th

During today's lesson you'll work on a complex exercise on the topic of Force method for frame structures. Please ask your questions regarding the [homework](homework6.1) as well!

## Exercise Force method for frame structures

Given the following structure.

```{figure} intro_data/structure.svg
:align: center
```

1. Find the bending moment distribution
2. Find the normal force distribution


````{admonition} Solution assignment 1
:class: tip, dropdown

```{figure} ./intro_data/M-line.svg
:align: center
```
````


````{admonition} Solution assignment 2
:class: tip, dropdown

```{figure} ./intro_data/N-line.svg
:align: center
```

````

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

q = sym.symbols('q')

q = 11
EI = sym.symbols('EI')
M_D, M_B_BD, M_B_AB, M_B_BC = sym.symbols('M_D M_B_BD M_B_AB M_B_BC')

eq1 = sym.Eq(M_D * 6 / 3 / EI, - M_D * 8 / 3 / EI - M_B_BD * 8 / 6 / EI)
eq2 = sym.Eq(M_B_AB * 10 / 3 / EI, M_B_BD * 8 / 3 / EI + M_D * 8 / 6 / EI)
eq3 = sym.Eq(M_B_AB * 10 / 3 / EI, M_B_BC * 6 / 3 / EI + q * 6 ** 3 / EI / 24)
eq4 = sym.Eq(M_B_BD + M_B_AB + M_B_BC,0)
display(eq1, eq2, eq3)

sol = sym.solve([eq1, eq2, eq3, eq4], (M_D, M_B_BD, M_B_AB, M_B_BC))
display(sol)

print(1/8 * 11 * 6**2)
print(-59/2/2+1/8*11*6**2)
print(-59/2/2+1/8*11*6**2*2)
```
