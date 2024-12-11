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

```{index} Static indeterminate structures; Exam assignment
```
```{index} Transformations; Class exercise using Mohr's circle and analytical formulas
```


(lesson11.1)=
# Lesson November 11th

Today we'll discuss the results of the first [exam assignment on Statically indeterminate structures](exam1).

## Results first exam assignment on Statically indeterminate structures

Approaches taken during the [exam assignment](../../week_10/session/intro.md):
- Mostly applied displacement method with displacements at $\text{D}$
- One person applied force method for horizontal support reactions at $\text{C}$, another person for $N_\text{BD}$. Both of them abandoned that a
- Not explicitly clear which statically determinate structure is solved for
- Displacement of $30 \text{ mm}$ used incorrectly as full total elongation of bar $\text{BD}$

## Demonstration transforming stresses and Circle of Mohr

Given the following structure and cross section.

```{figure} intro_data/structure.svg
:align: center
```

We'll find the maximum stresses in point $\text{E}$ in cross-section $\text{A}$ and its direction.

### Internal forces
First, let's find the internal forces:

```{figure} intro_data/Mline.svg
:align: center
```

```{figure} intro_data/Vline.svg
:align: center
```

At cross-section $\text{A}$ this gives a moment of $-14.6 \text{ kNm}$ and shear force of $+16 \text{ kN}$.

### Cross-sectional properties

For this thin-walled cross-section, the second moment of area of the cross-section can be calculated with:

$$ I_\text{zz} = 2 \cdot \cfrac{1}{12} \cdot 4 \cdot 300 ^3 + 2 \cdot \left(\cfrac{1}{12} \cdot 100 \cdot 12^3 + 12 \cdot 100 \cdot 150^2 \right) = 72.0288 \cdot 10^6 \text{ mm}^4$$

### Normal and shear stresses

The normal stresses can be calculated as:

$$\sigma_\text{E} = \cfrac{-14600 \cdot -0.075}{72.0288 \cdot 10^{-6}} \approx +15 \cdot 10^6 \text{ Pa}$$

$$\sigma_\text{max} = \cfrac{-14600 \cdot -0.150}{72.0288 \cdot 10^{-6}} \approx +30 \cdot 10^6 \text{ Pa}$$

Leading to the following diagram:

```{figure} intro_data/normall_stress.svg
:align: center
```

The shear forces can be calculated as:

$$\sigma_\text{xm,max flange} = - \cfrac{16000 \cdot 12 \cdot 100 \cdot 150}{2 \cdot 12 \cdot 72.0288 \cdot 10^{-6}} \approx 1.7 \cdot 10^6 \text{ Pa}$$

$$\sigma_\text{xm,min web} = - \cfrac{16000 \cdot 12 \cdot 100 \cdot 150}{2 \cdot 4 \cdot 72.0288 \cdot 10^{-6}} \approx 5.0 \cdot 10^6 \text{ Pa}$$

$$\sigma_\text{xm,E} = - \cfrac{16000 \cdot \left(12 \cdot 100 \cdot 150 + 2\cdot 4\cdot 75 \cdot 112.5 \right)}{2 \cdot 4 \cdot 72.0288 \cdot 10^{-6}} \approx 6.9 \cdot 10^6 \text{ Pa}$$

$$\sigma_\text{xm,max web} = - \cfrac{16000 \cdot \left(12 \cdot 100 \cdot 150 + 2\cdot 4\cdot 150 \cdot 75 \right)}{2 \cdot 4 \cdot 72.0288 \cdot 10^{-6}} \approx 7.5 \cdot 10^6 \text{ Pa}$$

Leading to the following diagram:

```{figure} intro_data/shear_stresses.svg
:align: center
```

The stress state for a rectangular element at point $\text{E}$ is therefore:

```{figure} intro_data/element.svg
:align: center
```

#### Find maximum stress

As the stress can be represented as a tensor. Therefore, a $x,y$-coordinate system is introduced:

```{figure} intro_data/element2.svg
:align: center
```

Leading to the tensor $\sigma$:

$$\sigma  = \left[ \begin{array}{}
{15}&{-6.9}\\
{-6.9}&{0}
\end{array} \right]{\text{ MPa}}$$

The maximum stress can be found by applying the transformation rules:

$$\sigma_1 = \frac{1}{2} \left(15 + 0\right) + \sqrt{\left(\frac{1}{2}\left(15-0\right)\right)^2 + \left(-6.9\right)^2} \approx 17 \text{ MPa}$$

With a corresponding angle $\alpha$:

$$\alpha = \frac{1}{2} \arctan\left(\cfrac{-6.9}{\frac{1}{2}\left(15-0\right)}\right) \approx 21^\text{o}$$

This can also be found using a circle of Mohr:

First, the two points $\left(15,-6.9\right)$ and $\left(0,-6/9\right)$ are added:

```{figure} intro_data/mohr1.svg
:align: center
```

Then, Mohr's circle can be drawn

```{figure} intro_data/mohr2.svg
:align: center
```

Given the same maximum of $\sigma_1 \approx 17 \text{ MPa}$. Finally, the corresponding rotation can also be found:

```{figure} intro_data/mohr3.svg
:align: center
```

Which gives the same $\alpha \approx 31^\text{o}$.

```{code-cell} ipython3
:tags: [remove-cell]

import numpy as np
import matplotlib.pyplot as plt
import matplotlib.patches as patches
%config InlineBackend.figure_format = 'svg'

x_CD = 1.8
x_BC = 2.6
x_AB = 2.2
F = 10
q = 10
h = 0.300
b = 0.100
tl = 0.004
tf = 0.012

Ar = h* tl * 2 + b * tf * 2
print('Oppervlakte=',Ar)

Izz = 1/12 * tl * h **3 * 2 + 1/12 * b * tf **3 * 2 + 2 * b * tf * (h/2) **2

print("Buigtraagheidsmoment=",Izz)

M_B = -F*x_AB
M_C = -F*(x_AB+x_BC)+q*x_BC*0.5*x_BC
M_D = -F*(x_AB+x_BC+x_CD)+q*x_BC*(0.5*x_BC+x_CD)
V_B = -F
V_C = -F+q*x_BC

print("M_B=",M_B," , M_C=",M_C,',M_D = ',M_D,', V_B=',V_B,', V_C=',V_C)

#hoekpunt, midden

S_A = b * tf * h / 2
S_B = b * tf * h / 2 + 2 * tl * h/2 * h/4
S_E = b * tf * h / 2 + 2 * tl * h/4 * h/8*3
print('Statisch moment A',S_A,', B=',S_B)
tau_Ab = (V_C*1e3 * S_A )/ (2*tf*Izz)
tau_Ao = (V_C*1e3 * S_A )/ (2*tl*Izz)
tau_B = (V_C*1e3 * S_B )/ (2*tl*Izz)
tau_E = (V_C*1e3 * S_E )/ (2*tl*Izz)

print('Schuifspanning buiging tau_Ab=',tau_Ab,', tau_A0 =',tau_Ao,', tau_B =',tau_B,', tau_E =',tau_E)

sigma_buiging = - M_C*1e3 * (h/4) / Izz
print('sigma_buiging=',sigma_buiging)

tau = tau_E / 1e6
sigma_x = sigma_buiging / 1e6
sigma_y = 0

sigma_min = (sigma_y+sigma_x)/2-np.sqrt(((sigma_x-sigma_y)/2)**2+tau**2)
sigma_max = (sigma_y+sigma_x)/2+np.sqrt(((sigma_x-sigma_y)/2)**2+tau**2)
alpha = np.arctan(2*tau/(sigma_x-sigma_y))/2
tau_max = np.sqrt(((sigma_y-sigma_x)/2)**2+tau**2)
print('sigma_min=',sigma_min)
print('sigma_max=', sigma_max)
print(np.rad2deg(alpha))


plt.figure()
ax = plt.gca()
ax.set_aspect('equal')
ax.spines['right'].set_color('none')
ax.spines['bottom'].set_position('zero')
ax.spines['left'].set_position('zero')
ax.spines['top'].set_color('none')
plt.grid()
if sigma_min<0:
    plt.xlim([1.1*sigma_min,1.4*sigma_max])
else:
    plt.xlim([0.7*sigma_min,1.1*sigma_max])
plt.ylim([-1.1*tau_max,1.1*tau_max])
plt.xlabel('xx, yy')
ax.xaxis.set_label_coords(0.95, 0.55)
ax.yaxis.set_label_coords(0,0.95)
#plt.ylabel(r'$\tau$')
plt.plot(sigma_x,-tau,marker='o')
plt.plot(sigma_y,tau,marker='o')
#plt.show()
plt.plot([sigma_x,sigma_y],[-tau,tau])
plt.plot((sigma_x+sigma_y)/2,0,marker='o')
circle1 = plt.Circle([(sigma_x+sigma_y)/2,0],np.sqrt(((sigma_x-sigma_y)/2)**2+tau**2),fill=False)
ax.add_artist(circle1)
plt.plot(sigma_max,0,marker='o')
plt.plot(sigma_min,0,marker='o')
#plt.show()
plt.plot([sigma_y,sigma_x],[-tau,-tau],color='black')
plt.plot([sigma_y,sigma_y],[-tau,tau],color='black')
plt.plot(sigma_y,-tau,marker='o',color='black')
plt.plot([sigma_y,sigma_max],[-tau,0],color='black')


# Add curved arrow from sigma_y/2, -tau to the last line shown
arrow = patches.FancyArrowPatch((sigma_x/2, -tau), (sigma_x/2*np.cos(alpha), -tau+np.sin(alpha)*sigma_x/2), connectionstyle="arc3,rad=.3", color="black", arrowstyle='simple',mutation_scale=15)
ax.add_patch(arrow)
plt.show()



s_v = np.sqrt(sigma_min**2-sigma_min*sigma_max+sigma_max**2)
print('vloeispanning =',s_v)
#plt.show()
```
