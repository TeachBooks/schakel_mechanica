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

```{index} Support settlement; Class exercise
```
```{index} Stiffness influences; Class exercise
```


(lesson8.2)=
# Lesson October 23th

During today's lesson you'll work on a complex exercise on the topic of Stiffness discontinuities and Support settlement. Please ask your questions regarding the [homework](homework8.2) as well!

## Exercise Support settlement

Given the following structure.

```{figure} intro_data/structure.svg
:align: center
```

1. Find the moment distribution for $n=1$


````{admonition} Solution assignment 1
:class: tip, dropdown

```{figure} intro_data/M-line.svg
:align: center
```

````

## Exercise Stiffness discontinuities

2. Find the moment distribution for $n=0$
3. Find the moment distribution for $n \to \infty$

````{admonition} Solution assignment 2
:class: tip, dropdown

```{figure} intro_data/M-line-2.svg
:align: center
```

````

````{admonition} Solution assignment 3
:class: tip, dropdown

```{figure} intro_data/M-line-3.svg
:align: center
```
````

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

EI = sym.nsimplify(25e3)
w = sym.nsimplify(0.025)

M_B, M_C = sym.symbols('M_B M_C')

eq1 = sym.Eq(-M_B * 10 / 3 / EI + w / 10 ,0)
M_B_1 = sym.solve(eq1, M_B)[0]

eq2 = sym.Eq(M_B * 10 / 3 / EI - w / 10, w / 10)
eq3 = sym.Eq(w/10, M_C * 10 / 3 / EI)
M_B_2 = sym.solve(eq2, M_B)[0]
M_C_2 = sym.solve(eq3, M_C)[0]

display(M_B_1, M_B_2, M_C_2)
display(M_B_1 - M_B_2, M_C_2)
```
