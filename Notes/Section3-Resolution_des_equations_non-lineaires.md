# Section 3: Résolution d’équations non-linéaires

# Position du problème

Soit $F:\space I\subset\mathbb R\rightarrow\mathbb R$ avec $F$ non-linéaire

Exemple: $F(x)=sin(x)$ ou $\sqrt x$

Rappel: $F \space\textrm{linéaire} \rightarrow F(x)=ax$ et $F\space\textrm{affine}\rightarrow F(x) = ax+b$

**Objectif:** Résoudre l’équation **non-linéaire** $F(x)=0$. En effet on cherche toujours à réécrire l’equation tel qu'on cherche à trouver le(s) zero(s)/racine(s) d’un fonction.

On va donc construire un suite $(x_k)_ {k\in\mathbb N}$ qui converge vers *une* solution du problème.

💡 Il peut être plusieurs solutions.


**Proposition** (Existence et unicité du zéro de F):

$$
\textrm{Soit}\space F:\space[a,b]\rightarrow R, \textrm{continue sur}\space [a,b].\space \textrm{Si}\space F(a)F(b)<0,\space\textrm{alors:}
\newline
\exists x^\ast \in\space]b,a[\space\textrm{tel que}\space F(x^\ast)=0
\\
\newline
\textrm{De plus si F est strictement monotone (soit croissant, soit décroissante),}\space x^\ast \space\textrm{est unique.}
$$

$x^\ast$, étant un (voir ***le***) zero de notre fonction, est alors le vraie solution qu'on cherche.

# Méthode de dichotomie

**Principe:** Localiser une solution “pas à pas” → Dichotomie.

- On considère $F:\space[a,b]\rightarrow \mathbb R$ **strictement croissante et continue** sur $[a,b]$ et tq: $F(a)F(b) <0 \implies$ F admet (au moins) un zéro.
- On note: $a_0=a,\space b_0=b,\space\textrm{et}\space c=\frac{a_0+b_0}{2}$
    - Si $F(a_0)F(c)<0$ alors forcement $x^*\in[a_0,c]$
    On pose: $a_1=a_0,\space b_1=c$ et on itère
    - Sinon, on a forcement $x^*\in[c,b_0]$
    On pose: $a_1=c$ et $b_1=b_0$.

Algorithme:
Soient $a_n,\space b_n$ tq $x^*\in[a_n,b_n]$. On pose $c=\frac{a_n+b_n}{2}$.

- Si $F(a_n)(F(c)<0$, on pose: $a_{n+1}=a_n$ et $b_{n+1}=c$,
- Sinon, on pose: $a_{n+1}=c$ et $b_{n+1}=b_n$

On itère jusqu'à convergence…

On montre par récurrence que:

- $(a_n)_{n\in\mathbb N}$ est croissante, $(b_n)_{n\in\mathbb N}$ est décroissante,
- $|b_n - a_n|=\frac{b - a}{2^n},\space \forall n\in\mathbb N$, (où $n$ est le $n$ “courante”, pas le nombre totale des itérations.
- $x^*\in[a_n,b_n],\space\forall n\in\mathbb N$.

→Les suites $(a_n)_{n\in\mathbb N}$ et $(b_n)_{n\in\mathbb N}$ sont adjacentes

$\implies$ Elles convergent toutes deux vers $x^*$.

De plus:

$$
|a_n - x^*|\leq\frac{b - a}{2^n},\space \forall n\in\mathbb N
$$

💡 Cette algorithme est robuste, mais elle converge très lentement: de manière logarithmique


# Méthode de point fixe

On va reformuler $F(x)=0$:

$$
\textrm{Soit}\space G_\lambda(x)=x+\lambda F(x),\space \lambda\in\mathbb R^*,\space\textrm{alors:}
\\
F(x)=0\iff x=G_\lambda(x)
$$

Rappel: Théorème de point fixe:

Soit $G$ une application de $I$ dans $\mathbb R$ tq:

- $G(I)\subset I$,
- $\exists k\in\space [0,1[$ tq $G$ k-contractante, c.a.d.:

$$
\forall(x,y)\in I^2,\space|G(x)-G(y)|\leq k|x-y|
$$

→ Alors G admet un unique poin fixe $x^*\in I$ tq: $G(x^*)=x^*$

→De plus pour $x_0\in I,\space x_{n+1}=G(x_n),n\in\mathbb N$, CV vers $x^*$.

********************************************************L’algorithme de point fixe******************************************************** appliqué à $G_\lambda$ donne:

$$
x_0\space\textrm{donné:}\space x_{n+1} = x_n+\lambda F(x_n),n\ge 0
$$

![Untitled](Section%203%20Re%CC%81solution%20d%E2%80%99e%CC%81quations%20non-line%CC%81aires%20c3c72abaf7f442cebe9d80cd5c485964/Untitled.png)

- On choisit $\lambda$ tq $G(x,\lambda)$ strictement contractante.
- On montre que:

$$
|x_n-x^*|\leq\frac{k(\lambda)^n}{1-k(\lambda)}|x_1-x^*|
$$

→Vitesse de CV d’ordre 1.

💡 La vitesse de convergence est plus rapide quand $k$ est pétit.


# Méthode de Newton

********************Principe:******************** on résout l’équation linéarisée. Soit:

- D.L. de Taylor à l’ordre 1 au point $x_n$:

$$
F(x_n+h)=F(x_n)+hF'(x_n)+h\epsilon(h)
$$

et on néglige le reste.

- On cherche “l’incrément” $h$ tq: $F(x_n+h)=0$

$\implies$A chaque itération, on résout: $F(x_n)+hF’(x_n)=0$

En posant $x_{n+n}=x_n+h$, cela donne l’algorithme de Newton:

$$
x_{n+1}=x_n-\frac{F(x_n)}{F'(x_n)},\space n\geq0,\space x_0\space\textrm{donné.}
$$

**********************Pour $F’(x_n)\neq 0$**

- Avantage: Convergence rapide (si CV)
- Désavantage: Convergence locale → Faut bien choisir le point initial $x_0$

→L’itéré de Newton se ré-écrit:

$$
F(x_n)+F'(x_n)(x_{n+1}-x_n)=0
$$

→ $x_{n+1}$ est le point d’intersection entre l’axe des $x$ et la droite $y=F(x_n)+F’(x_n)(x-x_n)$ qui est la tangente à la courbe $y=f(x)$ au point $x_n$

![Untitled](Section%203%20Re%CC%81solution%20d%E2%80%99e%CC%81quations%20non-line%CC%81aires%20c3c72abaf7f442cebe9d80cd5c485964/Untitled%201.png)

### Convergence de la méthode de newton:

******************Théorème:******************

Si $F$ de classe $C^2$ et $x^*$ racine simple de $F(x)$=0, c.a.d. que $F(x^*)=0\space\textrm{et}\space F’(x^*)\neq 0$

Alors l’alrogithme de Newton CV localement, à l’ordre 2.

CV locale:

$$
\exists \eta>0 \space \textrm{tq. si}\space |x-x_0|<\eta\space \textrm{la suite}\space (x_n)_n\space\textrm{converge vers }\space x^*.
$$

- Vitesse de CV d’ordre 2: $\exists C>0$ tel que:

$$
|x_n-x^*|\leq C|x_{n-1}-x^*|^2
$$

- En pratique: A chaque itération le nombre de digits exact est doublé car: $|x_{n-1}-x^*|=10^{-p}\implies |x_n-x^*|\approx 10^{-2p}$.

# Variante de Newton: Méthode de la sécante

- Le calcul de $F’(x_n)$, $DF(x_n)$ dans le cas de systèmes, peut être délicat à mener…
    - Alternative: *********approcher********* la dérivée par différence divisée.
- Algorithme de la sécante:

$$
x_{n+1}=x_n-F(x_n)\frac{x_n-x_{n-1}}{F(x_n)-F(x_n-1)}\space ,\space n\geq 0,\space x_0\space\textrm{donné}
$$

- CV locale uniquement (idem Newton)
- CV à l’ordre $\frac{1+\sqrt 5}2$ qui est $\in ]1,2[$
