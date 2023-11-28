# Partie 5: Méthode des moindres carrées 
## Méthode de moindres carrées linéaire 
Soient $m$ données $\{d_i\}_{1\leq i\leq m}$

**Objectif:** représenter ces données par un *modelé*.

Ex. Modelé dit de régression linéaire: une droite, 2 paramètres.

En générale, on a une modelé linéaire à n paramètres $`(x_i)_{1\leq i\leq n}`$ pour $`m`$ données:
```math
\begin{cases}
a_{11}x_1+\dots+a_{1n}x_n=d_1\\
\dots=\dots\\
a_{m1}x_1+\dots+a_{mm}x_n=d_m
\end{cases} 
```math
A rectangulaire $`m\times n`$; $`d\in\mathbb R^m`$ observations; $`x\in \mathbb R^n`$ inconnues.

**Étant donnée $`d\in\mathbb R^m`$, trouver $`x\in \mathbb R^n`$ tel que: $`Ax=d`$**

-> Problème de calibration de modelé. 

