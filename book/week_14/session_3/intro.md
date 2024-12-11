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

```{index} Failure models; Class exercise
```

(lesson14.3)=
# Lesson December 6th

During today's lesson you'll work on a complex exercise on the topic of the Failure models. Please ask your questions regarding the [homework](homework14.3) as well!

## Exercise Failure models

Given is the following structure. It represents the Prinses Amaliabrug, a bicycle bridge near Dordrecht.

```{figure} intro_data/structure.svg
:align: center
```

1. Find the relevant cross-sectional properties.
2. Find the bending- en torsional moment distribution.
3. Find the shear- and normal forces in cross-section just right of $\text{D}$ at point $\text{E}$
4. Draw the stress state in cross-section just right of $\text{D}$ at point $\text{E}$ in the principal stress plane including Tresca's failure criterium for unknown yield stress.
5. What should be the minimum yield stress according to Tresca?

````{admonition} Solution assignment 1
:class: tip, dropdown

$A_m = 3.23 \text{ m}^2$

````

````{admonition} Solution assignment 2
:class: tip, dropdown

```{figure} intro_data/Mline.svg
:align: center
```

```{figure} intro_data/Mtline.svg
:align: center
```

````


````{admonition} Solution assignment 3
:class: tip, dropdown

- $\sigma_\text{E} = -0.0174 \text{ MPa}$
- $\tau_\text{E} = 12.53 \text{ MPa}$

```{figure} intro_data/stress.svg
:align: center
```

````

````{admonition} Solution assignment 4
:class: tip, dropdown

```{figure} intro_data/s1s2.svg
:align: center
```

````

````{admonition} Solution assignment 5
:class: tip, dropdown

- $f_y > 25.06 \text{ MPa}$

````

```{code-cell}
:tags: [remove-cell]

import numpy as np

t = 10e-3
r_outer = 2.8+t/2
r_inner =  2.80 - t/2
A_outer = np.pi*r_outer**2/2
A_inner = np.pi*r_inner**2/2
A_circle = A_outer-A_inner
c_outer = (4*r_outer/(3*np.pi))
c_inner = (4*r_inner/(3*np.pi))
c_1 = (A_outer * c_outer - A_inner * c_inner) / (A_outer - A_inner)
print(c_outer,c_inner,c_1)

Ix_1 = np.pi*r_outer**4/16+A_outer*(c_outer-c_1)**2-(np.pi*r_inner**4/16+A_inner*(c_inner-c_1)**2)
Iy_1 = Ix_1
Ixy_1 = 1/8*r_outer**4+A_outer*(c_outer-c_1)**2-(1/8*r_inner**4+A_inner*(c_inner-c_1)**2)
print(Ix_1,Ixy_1)

Iyy = (Ix_1+Iy_1)/2+(Ix_1-Iy_1)/2*np.cos(2*np.pi/4)+Ixy_1*np.sin(2*np.pi/4)
print(Iyy)
c_2 = 2.8 - c_1*np.sqrt(2)
print('c_2=',c_2)
d = 2.8-2.8/np.sqrt(2)
print('d=',d)
c_4 = 0.25+d-c_2
print('c_4=',c_4)

A_rechthoek = 4*t
A_klein = 0.25*t*2
c_3 = (A_klein*0.125+A_circle*c_4)/(A_rechthoek+A_klein+A_circle)
print('c_3=',c_3)

Iyy_totaal = 1/12*(4*t**3)+A_rechthoek*c_3**2+1/12*(2*t*0.25**3)+A_klein*(c_3-0.125)**2+Iyy+A_circle*(c_4-c_3)**2
print('Iyy_totaal=',Iyy_totaal)

Bv = (12.5*40*20-14.32*15)/25
print('Bv=',Bv)
Mb = 12.5*15*7.5
print('Mb=',Mb)
print('MCA=',12.5*7.5**2/2)
Mc = 12.5*25*12.5-Bv*10
print('Mc=',Mc)
print('MAC=',12.5*20*10-Bv*5)
print('MDB=',Mc/2-1/8*12.5*15**2)

Mtb = Bv*2
Mtc = Mtb+14.32*2
print(Mtb,Mtc)

Am = np.pi*2.8**2 / 4 - 2.8*2.8*0.5+0.25*4
tau = Mtc / (2*Am*t*1000)
print('Am=',Am,', tau=',tau)

sigma = Mc * (250+280)/Iyy_totaal / 1e6
print('sigma=',sigma)

sigma1 = sigma/2+np.sqrt((sigma/2)**2+tau**2)
sigma2 = sigma/2-np.sqrt((sigma/2)**2+tau**2)
print(sigma1,sigma2)

b = sigma2 - 1 * sigma1
print(b)
```
