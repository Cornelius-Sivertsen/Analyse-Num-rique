# Section 2: Intégration Numérique

# Introduction

But: Calcul de manière générale $I=\int_a^b f(x)dx$ pour toute fonction f continue.

Idée: Trouver des méthodes numériques *****rapides***** permettant de calculer un valeur **********approchée********** de cette intégrale

Le principe se divise en etapes:

1. On subdivise $[a,b]$ en n sous-intervalles $[x_{k-1},x_k],\space k=1,\dots,n$
    1. Remarque: On a donc n+1 points
2. On écrit $I$ sous la forme $\int_a^bf(x)dx=\sum\limits_{k=1}^n(\int_{x_{k-1}}^{x_k}f(x)dx)=\sum\limits_{k=1}^nI_k$
3. On approche $f(x)$ par $f_k(x)$ sur chaque sous-intervalle $[x_{k-1},x_k]$
4. on calcule $\tilde{I_k}=\int_{x_{k-1}}^{x_k}f_k(x)dx$ qui approxime $I_k = \int_{x_{k-1}}^{x_k}f(x)dx$
5. On obtient une valeur approchée $\tilde{I}$ de $I$ par la somme $\tilde{I}=\sum\limits_{k=1}^n\tilde{I_k}$

# Les différentes méthodes d’approximation de f(x)

## Les deux méthodes des rectangles:

Principe: On approche $f$ par un fonction constante par morceaux:

**Cas de rectangles à gauche:**

$$
f_k(x) = f(x_{k-1}), \space\forall x\in [x_{k-1},x_k]
$$

On a donc:

$$
\tilde{I_k}=\int_{x_{k-1}}^{x_k}f_k(x)dx=(x_k-x_{k-1})*f(x_{k-1})
\newline
\implies I\approx\tilde{I}=\sum\limits^n_{k=1}(x_k-x_{k-1})*f(x_{k-1})
$$

On utilise normalement un subdivision *uniforme* de $[a,b]$:  $x_k=a+k\frac{b-a}{n}$

$$
\implies I\approx\tilde{I}=\frac{b-a}{n}\sum\limits^n_{k=1}f(x_{k-1})
$$

<aside>
💡 On aura donc un valeur approximé qui est < que la valeur vraie

</aside>

**Cas de rectangles à droite:**

On change $x_{k-1}$ par $x_k$

Avec un subdivision uniforme on a donc:

$$
I\approx\tilde{I}=\frac{b-a}{n}\sum\limits_{k=1}^nf(x_k)
$$

<aside>
💡 Ici, on aura un valeur approximé > que la valeur vraie

</aside>

## Méthode des trapèzes

Principe: On approche f par une fonction affine par morceaux qui relie sur chaque intervalle $[x_{k-1},x_k]$ les points $(x_{k-1},f(x_{k-1}))$ et $(x_k,f(x_k))$. 

Rappel: $\textrm{Une fonction F est affine}\space\iff\space F(x)=ax+b\space,\space (a,b)\in\mathbb R$


On a donc:

$$
\tilde{I_k}=\int_{x_{k-1}}^{x_k}f_k(x)dx=(x_k-x_{k-1})(\frac{f(x_{k-1})+f(x_k)}{2})
\newline
\implies I\approx\tilde{I}=\sum\limits^n_{k=1}(x_k-x_{k-1})(\frac{f(x_{k-1})+f(x_k)}{2})
$$

Avec un subdivision uniforme de $[a,b]$ on a donc:

$$
I\approx\tilde{I}=\frac{b-a}{n}\sum\limits^n_{k=1}\frac{f(x_{k-1})+f(x_k)}{2}
$$

## Autres méthodes:

### Méthode du point milieu:

Comme méthode des rectangles, mais on prend le valeur au milieu de l'intervalle: 


On a donc:

$$
f_k(x)=f(\frac{x_{k-1}+x_k}{2})\space, \space\forall x\in[x_{k-1},x_k]
\newline
\implies I\approx\tilde{I}=\sum\limits^n_{k=1}(x_k-x_{k-1})f(\frac{x_{k-1}+x_k}{2})
$$

Avec subdivision uniforme:

$$
I\approx\tilde{I}=\frac{b-a} n\sum\limits^n_{k=1}(f(\frac{x_{k-1}+x_k}{2})
$$

### ********************Méthode de Simpson:********************

On approche f par le polynôme de degré 2 coïncidant avec f à gauche, à droite et au milieu de chaque intervalle:

$$
I\approx\tilde{I}=\sum\limits^n_{k=1}\frac{x_k-x_{k-1}}{6}(f(x_{k-1})+4f(\frac{x_k+x_{k-1}}{2})+f(x_k))
$$

Avec subdivision uniforme:

$$
I\approx\tilde{I}=\frac{b-a} n\sum\limits^n_{k=1}\frac{1}{6}(f(x_{k-1})+4f(\frac{x_k+x_{k-1}}{2})+f(x_k))
$$

<aside>
💡 On note que le calcul de $\tilde{I}$ necesite ici le calcul de $2(n+1)$ points. Par contre les rectangles necesite $n$ points et les trapèzes $n+1$ points.

</aside>

## Ordre des méthodes

L’ordre de méthode d’un méthode d’intégration numérique est un indicateur de son précision.

**Définition:** Une méthode d’intégration numérique est d’ordre $p$ si pour toute fonction $f$ de classe $C^p$ sur $[a,b]$ il existe une constante $C(f,a,b)$ positive telle que:

$$
|I-\tilde{I}|\leq C(f,a,b)(\frac{b-a}{n})^p
$$

Ou $n$ est le nombre de sous-intervalles de $[a,b]$ utilisées pour l'approximation.

**Quelques remarques:**

1. Toute méthode d’ordre $p\geq1$  est convergente, c.a.d. que $\tilde{I}\rightarrow I$ quand $n\rightarrow +\infty$.
2. On voit que, pour un $n$ donné, un méthode d’ordre $p$ sera **moins précis** q’un méthode d’ordre $p+1$.
3. Cette équation peut nous donner, pour un certain méthode, le nombre minimal des sous-divisions nécessaire pour attendre un certain précision.
4. Un méthode d’ordre $p$ ne s’applique que aux fonctions de classe $C^p$

 

Ordre des méthodes vues:

- Rectangles: ordre 1
- Trapèzes *et du point milieu* ordre 2
- Simpson: ordre 4

<aside>
💡 De manière générale: des que l'on augmente en ordre de précision, on augmente aussi en coût de calcul, donc en temps de calcul.

</aside>
