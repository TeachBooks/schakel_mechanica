---
jupytext:
  cell_markers: '"""'
  text_representation:
    extension: .md,py
    format_name: myst,percent
    format_version: 0.13
    jupytext_version: 1.16.1
kernelspec:
  display_name: base
  language: python
  name: python3
---

```{index} Transformations; Class exercise using analytical formulas
```

```{custom_download_link} intro.py
:text: ".py"
```

(lesson13.1)=
# Lesson November 25th

During today's lesson you'll work on a complex exercise on the topic of the Transforming tensors. Please ask your questions regarding the [homework](homework13.1) as well!

## Exercise Transforming tensors

Given is the following structure and cross-section:

```{figure} intro_data/structure.svg
:align: center
```

1. Find the relevant cross-sectional properties.
2. Find the normal and shear stresses just below $\text{G}$, in $\text{H}$, in $\text{I}$ and just right of $\text{C}$ in cross-section $\text{A}$.
3. Find the principal values of the stresses in the points just below $\text{G}$, in $\text{H}$, in $\text{I}$ and just right of $\text{C}$ in cross-section $\text{A}$.

````{admonition} Solution assignment 1
:class: tip, dropdown

Normal force centre is given by:
```{figure} intro_data/NC.svg
:align: center
```

- $A \approx  17500 \text{ mm}^2$
- $I_{zz} \approx 655 \cdot 10^6 \text{ mm}^4$

````

````{admonition} Solution assignment 2
:class: tip, dropdown

- $\sigma_\text{just below G} = +6.73 \text{ MPa}$
- $\tau_\text{just below G} = +0.164 \text{ MPa}$
- $\sigma_\text{H} = +6.73 \text{ MPa}$
- $\tau_\text{H} = 0 \text{ MPa}$
- $\sigma_\text{I} = -2 \text{ MPa}$
- $\tau_\text{I} = +0.35 \text{ MPa}$
- $\sigma_\text{just right of C} = -8.53 \text{ MPa}$
- $\tau_\text{just right of C} = -0.12 \text{ MPa}$

````

````{admonition} Solution assignment 3
:class: tip, dropdown

- $\sigma_\text{1, just below G} = +6.73 \text{ MPa}$
- $\sigma_\text{2, just below G} = -0.0040 \text{ MPa}$
- $\sigma_\text{1, H} = +6.73 \text{ MPa}$
- $\sigma_\text{2, H} = 0 \text{ MPa}$
- $\sigma_\text{1, I} = 0.59 \text{ MPa}$
- $\sigma_\text{2, I} = -2.06 \text{ MPa}$
- $\sigma_\text{1, just right of C} = 0.0018 \text{ MPa}$
- $\sigma_\text{2, just right of C} = -8.5 \text{ MPa}$

````

Test of adding more text

```{code-cell}
:tags: [remove-cell]

Izz = 655e6

tau_G = -3e3 * -250*10*286 / 20 / Izz
print(tau_G)

tau_C = -3e3 * -250*20*(286-500) / 40 / Izz
print(tau_C)

sigma_G = +6.73
tau_G = -tau_G
sigma_G_1 = 1/2 * (sigma_G + 0) + ((1/2 * (sigma_G + 0))**2 + tau_G**2)**0.5
sigma_G_2 = 1/2 * (sigma_G + 0) - ((1/2 * (sigma_G + 0))**2 + tau_G**2)**0.5
print(sigma_G_1, sigma_G_2)

sigma_H = +6.73
tau_G = 0
sigma_H_1 = 1/2 * (sigma_H + 0) + ((1/2 * (sigma_H + 0))**2 + tau_G**2)**0.5
sigma_H_2 = 1/2 * (sigma_H + 0) - ((1/2 * (sigma_H + 0))**2 + tau_G**2)**0.5
print(sigma_H_1, sigma_H_2)

sigma_I = -2
tau_I = +0.35
sigma_I_1 = 1/2 * (sigma_I + 0) + ((1/2 * (sigma_I + 0))**2 + tau_I**2)**0.5
sigma_I_2 = 1/2 * (sigma_I + 0) - ((1/2 * (sigma_I + 0))**2 + tau_I**2)**0.5
print(sigma_I_1, sigma_I_2)

sigma_C = -8.53
tau_C = -tau_C
sigma_C_1 = 1/2 * (sigma_C + 0) + ((1/2 * (sigma_C))**2 + tau_C**2)**0.5
sigma_C_2 = 1/2 * (sigma_C + 0) - ((1/2 * (sigma_C))**2 + tau_C**2)**0.5
print(sigma_C_1, sigma_C_2)
```
