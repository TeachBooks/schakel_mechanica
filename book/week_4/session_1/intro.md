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

```{index} Displacements truss structures; Class exercise using constitutive equation
```

(lesson4.1)=
# Lesson Monday September 23th

During today's lesson you'll work on a complex exercise on the topic of Extension. Please ask your questions regarding the [homework](homework4.1) as well!

## Exercise Extension

Given the following structure.

```{figure} intro_data/structure.svg
:align: center
```

1. Find the displacement of $\text{R}$

2. Draw the displaced structure


````{admonition} Solution assignment 1
:class: tip, dropdown

$96.7 \text{ mm}$ ↓

```{admonition} Solution elongations cables
:class: tip, dropdown

| Cable   | Elongation (mm) |
|---------|-----------------|
| BK      | 24           |
| CK      | 24           |
| DH      | 13           |
| GJ      | 52           |
| IM      | 5           |
| JP      | 15           |
| KQ      | 48           |
| OR      | 40            |

```

````

````{admonition} Solution assignment 2
:class: tip, dropdown

```{figure} intro_data/ans.svg
:align: center
```

````

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

F_1, F_2 = sym.symbols('F_1 F_2')

F_2 = 11 * 16
F_1 = 5 * 36

display(F_1, F_2)

N_OR = F_2 / 11 * 5
N_KQ = F_2 - N_OR
N_JP = N_OR / 8 * 6
N_IM = N_OR - N_JP
N_GJ = (N_IM*2 + N_JP*10 + F_1 * 8) / 10
N_DH = F_1 + N_IM + N_JP - N_GJ
N_BK = N_KQ / 2
N_CK = N_BK

#display(N_OR, N_KQ, N_JP, N_IM, N_GJ, N_DH, N_BK, N_CK)

L_BK = 4
L_CK = 4
L_DH = 2
L_GJ = 2
L_IM = 2
L_JP = 2
L_KQ = 4
L_OR = 4

EA = sym.symbols('EA')

EA = 8000

deltaL_BK = N_BK * L_BK / EA
deltaL_CK = N_CK * L_CK / EA
deltaL_DH = N_DH * L_DH / EA
deltaL_GJ = N_GJ * L_GJ / EA
deltaL_IM = N_IM * L_IM / EA
deltaL_JP = N_JP * L_JP / EA
deltaL_KQ = N_KQ * L_KQ / EA
deltaL_OR = N_OR * L_OR / EA

display(deltaL_BK, deltaL_CK, deltaL_DH, deltaL_GJ, deltaL_IM, deltaL_JP, deltaL_KQ, deltaL_OR)

u_H = deltaL_DH
u_J = deltaL_GJ
phi_HJ = (u_J - u_H) / 10
u_I = u_H + phi_HJ * 2
u_M = u_I + deltaL_IM
u_P = u_J + deltaL_JP
phi_MP = (u_P- u_M)/8
u_O = u_M + phi_MP * 6
U_R = u_O + deltaL_OR
u_K = deltaL_BK
u_Q = u_K + deltaL_KQ

display(u_H, u_J, phi_HJ, u_I, u_M, u_P, phi_MP, u_O, U_R, u_K, u_Q)
```
