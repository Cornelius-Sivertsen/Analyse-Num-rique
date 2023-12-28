# Section 4-A: Résolution directe des systèmes linéaires

# Rappel sur l’elimination de Gauss

### Exemple 1:

Soit le système d’equations:

$$
\begin{cases}
2x_1+x_2+x_3=1
\\
6x_1+2x_2+x_3=-1
\\
-2x_1+2x_2+x_3=7
\end{cases}
$$

Objectif: obtenir un système **triangulaire** équivalent qu'on résolut par remontée

Méthode: mettre des zéros dans la première colonne (sauf à la première ligne) et réitérer

- $L_2$ devient $L_2-3L_3$
- $L_3$ devient $L_3+L_1$

Alors on a:

$$
\begin{cases}
2x_1+x_2+x_3=1
\\
-x_2-2x_3=-4
\\
3x_2+2x_3=8
\end{cases}
$$

On réitère le procédé sur le système formé des deux dernières lignes.

### Exemple 2:

$$
\begin{cases}
x_1+x_2+x_3+x_4=1
\\
x_1+x_2+3x_3+3x_4=3
\\
x_1+x_2+2x_3+3x_4=3
\\
x_1+3x_2+x_3+3x_4=4
\end{cases}
$$

→ $L_i - L_1$ pour $i=\  2,3,4$

On a donc:

$$
\begin{cases}
x_1+x_2+x_3+x_4=1
\\
2x_3+2x_4=2
\\
x_3+2x_4=2
\\
2x_2+2x_3+2x_4=3
\end{cases}
$$

**Pivot nul:** on ne peut itérer directement le procédé. On permute $L_4$ et $L_2$.

**Résolution machine:** problème (et solution!) similaire si le pivot est très petit. 

- On prend le plus grand coéf. de la    colonne come pivot

# Interprétation matricielle de la méthode d’elimination de Gauss

Soit $\mathcal{L}_ {ij}(\lambda)\in\mathcal{M}_ n(\mathbb{R})$, un matrice de transvection, définie par:

$$
\mathcal{L}_ {ij}(\lambda) = I_ {\mathbb{R}^n}+\lambda E_ {ij}
$$

Avec $(E_{ij})_ {kl}=\delta_ {ik}\delta_ {jl}$

$E_{ij}$ est donc un matrice avec un seul coef non nul, à la ligne i et colonne j, qui est egal à 1.

**Propriété:** Si $i>j$, alors $\mathcal{L}_ {ij}(\lambda)$ est triangulaire inférieure, inversible et $\mathcal{L}_ {ij}(\lambda)^{-1}=\mathcal{L}_{ij}(-\lambda)$

**Opérations lignes:** Soit $A\in\mathcal{M}_ n (\mathbb{R})$, la matrice: $\tilde{A}=\mathcal{L}_ {ij}(\lambda)A$, est la matrice résultant de l’opération $L_ i \rightarrow L_ i+\lambda L_ j$ 

Exemple: Elimination de Gauss vu matriciellement sur l’exemple 1:

$$
A=
\begin{pmatrix}
2&1&1\\
6&2&1\\
-2&2&1\\
\end{pmatrix}
\rightarrow \mathcal{L}_ {32}(3)\mathcal{L}_ {31}(1)\mathcal{L}_ {21}(-3)A=
\begin{pmatrix}
2&1&1\\
0&-1&-2\\
0&0&-4
\end{pmatrix}
=U
$$

$$
\mathrm{Posons:}\  L=(\mathcal{L}_ {32}(3)\mathcal{L}_ {31}(1)\mathcal{L}_ {21}(-3))^{-1}=\mathcal{L}_ {21}(3)\mathcal{L}_ {32}(-1)\mathcal{L}_ {32}(-3)
$$

La matrice $A$ admet la **factorisation** $A=LU$

Résoudre $Ax=b$ revient à résoudre $Ly=b$ et $Ux=y$

Théorème:

Soit $A=(a_ {ij})_ {1\leq i,j\leq n}\in\mathcal{M}_ n(\mathbb{R})$ Si pour tout $k=1,\dots,n$, la sous matrice $A_ k=(a_ {ij})_ {1\leq i,j\leq k} \in \mathcal{M}_ k(R)$ est inversible (c.a.d. $det(A_ k)\neq 0$ alors la matrice $A$ admet une factorisation $A=LU$ où la matrice $L$ est triangulaire inférieure, et la matrice U est diagonale supérieure. De plus, si L contient que des 1 sur la diagonale, la décomposition est unique.

**Attention:** cette factorisation correspond à l’algorithme de Gauss SANS permutations.

## Décompte d’opérations:

A l’étape k (compris entre $1$ et $n-1$) (n est la taille de la matrice), on doit faire $n-k$ divisions par le pivot pour le calcul de la $k$-ième colonne de la matrice $L$ puis, pour la mise à jour de la matrice $A$, on doit faire $(n-k)^2$ multiplications et $(n-k)^2$ soustractions.

**Coût total:**

$$
C(n)=\sum_{k=1}^{n-1}(n-k)+(n-k)^2=n(n-1)\frac{4n-1}{6}~_ {n\rightarrow\infty}\frac{2n^3}{3}
$$

**Applications de la décomposition LU:**

Calcul de déterminant: $det(A)=det(L)det(U)=\prod_{i=1}^nU_{ii}$

- Coût: $C(n)+n-1~\frac{2n^3}{3}$

Calcul de l’inverse de A: on résout $Av_j=e_j,\  j=1,\dots,n$

- Coût: Décomposition $LU$ et résolution de $2n$ systèmes triangulaires $~\frac{2n^3}{3}+\frac{4n^3}{3}=2n^3$

On ne calcule jamais l’inverse d’une matrice pour résoudre un système linéaire.

# Décomposition de Cholesky

**Définition:** une matrice $A$ est symétrique définie positive ssi:

1. $A=A^T$
2. $x^TAx>0,\ \forall x\in \mathbb{R}^n$

Théorème: Si $A$ est une matrice symétrique définie positive, il existe une matrice $L$ triangulaire inférieure telle que $A=LL^T$. La décomposition est unique si on impose les termes diagonaux strictement positifs.

**Attention:** cette décomposition (dite de CHOLESKY) n’est pas la décomposition LU

Calcul de L: on fait le produit de L et de sa transposée et on identifie avec les coefficients de A. On obtient un système sur les coefficients de L qu'on résout par remonté.

- Coût de calcul divisé par deux par rapport à la décomposition LU
