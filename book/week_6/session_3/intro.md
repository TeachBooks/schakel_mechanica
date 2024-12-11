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

```{index} Force method; Class exercise for frame structures with moveable nodes
```

(lesson6.3)=
# Lesson October 11th

During today's lesson you'll work on a complex exercise on the topic of Force method for frames, or more specifically 'hoekveranderingsvergelijkingen' with moveable nodes. Please ask your questions regarding the [homework](homework6.3) as well!

## Exercise 'Hoekveranderingsvergelijkingen' with moveable nodes

Given the following structure.

```{figure} intro_data/structure.svg
:align: center
```

1. Find the bending moment distribution
2. Find the displacement of $\text{E}$

````{admonition} Solution assignment 1
:class: tip, dropdown

```{figure} intro_data/mline.svg
:align: center
```

````

````{admonition} Solution assignment 2
:class: tip, dropdown

- $u_\text{E,v} \approx 74.4391 \text{ mm} $ (↓)
- $u_\text{E,h} \approx 40 \text{ mm} $ (→)

````

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym
sym.init_printing()

a, M_b, M_c, EI, theta, F = sym.symbols('a, M_b, M_c, EI, theta, F')

F = sym.nsimplify(616)
EI = 36100
print(EI)
a = 1

eq1 = sym.Eq(M_b * a * sym.sqrt(13) / 3 / EI / sym.sqrt(13) - theta * 2, -M_b * 6 * a / EI / 3 + M_c * 6 * a / EI / 6 - F * (6 * a)**2 / EI / 16 + theta)
eq2 = sym.Eq(M_b * 6 * a / EI / 6 - M_c * 6 * a / EI / 3 + F * (6 * a)**2 / EI / 16 + theta, M_c * 4 * a / EI / 3 - theta)
eq3 = sym.Eq(-M_b * 2 - M_b - M_c - M_c + F * 3 * a, 0)

display(eq1, eq2, eq3)

sol = sym.solve([eq1, eq2, eq3], (M_b, M_c, theta))
display(sol)
display({key: value.evalf() for key, value in sol.items()})
```
