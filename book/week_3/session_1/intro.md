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

```{index} Displacements frame structures; Class exercise using euler-bernoulli
```

(lesson3.1)=
# Lesson Monday September 16th

During today's lesson you'll work on a complex exercise on the topic of 'Euler-Bernoulli'. Please ask your questions regarding the [homework](homework3.1) as well!

## Exercise Euler-Bernoulli

Given the following structure.

```{figure} intro_data/figure1.svg
:align: center
```

1. Use the Euler-Bernoulli equations to find the displacement halfway.

Given the following structure.

```{figure} intro_data/figure2.svg
:align: center
```

2. Use the Euler-Bernoulli equations to find the rotation at the left support

Given the following structure.

```{figure} intro_data/figure3.svg
:align: center
```

3. Use the Euler-Bernoulli equations to find the displacement of the top of the structure.

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

x, C_1, C_2, C_3, C_4 = sym.symbols('x C_1 C_2 C_3 C_4')

L, F, T, EI = sym.symbols('L F T EI')

L = 6
F = 20
T = 40
EI = 21000

q = 0
V = -sym.integrate(q, x) + C_1
M = sym.integrate(V, x) + C_2
kappa = M/EI
phi = sym.integrate(kappa, x) + C_3
w = -sym.integrate(phi, x) + C_4

eq1 = sym.Eq(w.subs(x,0),0)
eq2 = sym.Eq(phi.subs(x,0),0)
eq3 = sym.Eq(V.subs(x,L),F)
eq4 = sym.Eq(M.subs(x,L),-T)

sol = sym.solve([eq1,eq2,eq3,eq4],(C_1,C_2,C_3,C_4))
display(sol)

display(w.subs(sol).simplify().subs(x,L/2))
```

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

x, C_1, C_2, C_3, C_4 = sym.symbols('x C_1 C_2 C_3 C_4')

L, q, EI = sym.symbols('L q EI')

L = sym.S(8)
q = sym.S(96)
EI = 6400

q = -q/L*x
display(q)
V = -sym.integrate(q, x) + C_1
M = sym.integrate(V, x) + C_2
kappa = M/EI
phi = sym.integrate(kappa, x) + C_3
w = -sym.integrate(phi, x) + C_4

eq1 = sym.Eq(w.subs(x,0),0)
eq2 = sym.Eq(M.subs(x,0),0)
eq3 = sym.Eq(w.subs(x,L),0)
eq4 = sym.Eq(phi.subs(x,L),0)

sol = sym.solve([eq1,eq2,eq3,eq4],(C_1,C_2,C_3,C_4))
display(sol)

display(phi.subs(sol).simplify().subs(x,0).evalf())
display(w.subs(sol).simplify().subs(x,L/2).evalf())
```

```{code-cell} ipython3
:tags: [remove-cell]

import sympy as sym

x, C_1, C_2, C_3, C_4 = sym.symbols('x C_1 C_2 C_3 C_4')

EA, L1, L2, q, EI, F = sym.symbols('EA L1 L2 q EI F')

L1 = sym.S(4)
L2 = sym.S(5)
#q = sym.S(96)
EA = 20000

q_1 = -8
N_1 = -sym.integrate(q_1, x) + C_1
eps_1  = N_1/EA
u_1 = sym.integrate(eps_1, x) + C_2

q_2 = 0
N_2 = -sym.integrate(q_2, x) + C_3
eps_2  = N_2/EA
u_2 = sym.integrate(eps_2, x) + C_4

eq1 = sym.Eq(u_1.subs(x,0),0)
eq2 = sym.Eq(u_1.subs(x,L1),0)
eq3 = sym.Eq(u_2.subs(x,L1),0)
eq4 = sym.Eq(N_2.subs(x,L1+L2),20)

sol = sym.solve([eq1,eq2,eq3,eq4],(C_1,C_2,C_3,C_4))
display(sol)

display(u_2.subs(sol).simplify().subs(x,L1+L2).evalf())
```

````{admonition} Solution assignment 1
:class: tip, dropdown

$0.03 \text{ m}$ ↓
````

````{admonition} Solution assignment 2
:class: tip, dropdown
$0.064 \text{ rad}$ ⟲

````

````{admonition} Solution assignment 3
:class: tip, dropdown

$0.005 \text{ m}$ ↑
````
