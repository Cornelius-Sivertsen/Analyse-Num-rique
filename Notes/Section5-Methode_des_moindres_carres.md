# Partie 5: Méthode des moindres carrées 
## Méthode de moindres carrées linéaire 
Soient $m$ données $\{d_i\}_{1\leq i\leq m}$

**Objectif:** représenter ces données par un *modelé*.

Ex classique: Modelé dit de régression linéaire: une droite, 2 paramètres.

En générale, on a une modelé linéaire à n paramètres $(x_i)_{1\leq i\leq n}$ pour $m$ données:

$$
\begin{cases}
a_{11}x_1+\dots+a_{1n}x_n=d_1\\
\dots=\dots\\
a_{m1}x_1+\dots+a_{mm}x_n=d_m
\end{cases} 
$$

A rectangulaire $m\times n$; $d\in\mathbb R^m$ vecteur d'observations; $x\in \mathbb R^n$ vecteur d'inconnues.

**Étant donnée $d\in\mathbb R^m$, trouver $x\in \mathbb R^n$ tel que: $Ax=d$**

-> Problème de calibration de modelé. On cherche alors à calibrer la modèle par rapport aux données.

- Dans le cas (improbable) où $n=m$ le problème est _bien posé_ ssi $A$ est de rang maximal,c.a.d. $r=rank(A)=dim(Im(A))=n$.
  - Alors il existe un unique jeu de paramètres $x$ décrivant exactement les données.

- Cas $n=m$ mais $r=rank(A)=dim(Im(A))< n$. Alors $Ker(A)\neq\emptyset$ : $\exists z\in \mathbb R^n$ t.q. $Az=0$ dans $\mathbb R^m$.

- Cas $n>m$: système sous-détermine, infinité de solutions.

- Cas $n< m$: Système sur-déterminé: cas qui nous intéresse. A-priori le systeme n'admet pas de solution (au sens usuel...)

### Solution au sens des moindres carrés:
On cherche une solution qui représente _au mieux_ les observations, i.e. _minimisant la norme_ $||Ax-d||$.
Bon choix de norme: $||.||_ 2$ car associée à un produit scalaire.

Le problème devient: **Trouver $x^ * \in \mathbb R^n$ tel que:**

$$
j(x^ * )=\min_{x\in\mathbb R^n} j(x) \space\mathrm{avec}\space j(x)=||Ax-d||^2_{2,m}
$$

Problème d'optimisation (dans l'espace entier $\mathbb R^n$).

La solution ici est _la solution au sens des Moindres Carrés._

On a: $j\space : \mathbb R^n \rightarrow \mathbb R$,

$$
j(x)=||Ax-d||^2_{2,m}=\left< A^TAx,x\right>-2\left< Ax,d\right>+\left< d,d\right>
$$

La matrice carrée $A^TA$ est positive, $j$ est quadratique donc convexe $\implies j$ admet, _au moins_, un minimum dans $\mathbb R^n$.

-> Si de plus la matrice $A^TA$ est définie alors la solution est unique.

**Rappels:**
- Une matrice carrée $M$ positive est également définie si $\left< M x, x \right>=0$ est équivalent à $x=0$
- On peut montrer que $A^TA$ est définie ssi $A$ de rang maximal.

C.N. d'optimum local: $\nabla j(x)=0$ <br/>
puis C.S. de minimum (local): $D^2j(x)=H_j(x)$ est positive définie.

**Lemme:**<br/>
Le gradient de j s'écrit: $\nabla j(x)=A^TAx-A^Td$ (vecteur de $\mathbb R^n$)<br/>
Sa _matrice Hessienne_ (carrée $n\times n$) s'écrit: $H_j (x)=A^TA,\space\forall x$.

**Théorème centrale:**<br/>
Toute solution du problème de M.C. au cas sur-détermine ($n< m$) est également solution du système linéaire $n\times n$: 

$$
A^TAx=A^Td\quad\rightarrow\quad\textrm{équations normales}
$$

De plus, la solution est unique ssi $A$ de rang maximal ($rang(A)=n$)

### Modèle de régression linéaire:
- Faire passer une droite (linéaire) "au mieux" dans un "nuage" des points.
- Fonctions de base des solutions: $\{1,x\}$
- Pour $m$ points $(x_i,y_i)$ de $\mathbb R^2$, $A$ s'écrit:

$$
\begin{pmatrix}
1&x_1\\
\vdots&\vdots\\
1&x_m
\end{pmatrix}
$$
- Equations normales:

$$
\begin{pmatrix}
m&\sum\limits^m_{i=1}x_i\\
\sum\limits^m_{i=1}x_i&\sum^m_{i=1}x_i^2
\end{pmatrix}
\cdot \begin{pmatrix}
a_0\\
a_1
\end{pmatrix}
=\begin{pmatrix}
\sum\limits^m_{i=1}y_i\\
\sum\limits^m_{i=1}x_iy_i
\end{pmatrix}
$$ 

- Paramètres = coefficients de la droite: $(a_0,a_1)$

### Interprétation géométrique:
-> Une solution aux M.C. minimise la distance euclidienne entre $d\in\mathbb R^m$ et $Im(A)$ (qui est un sous-espace vectoriel de $\mathbb R^m$.<br/>

**Autrement formulé:**<br/>
$x^\ast$ est t.q. $Ax^\ast$ projeté $\perp$ de $d\in\mathbb R^m$ sur $Im(A)$

**Lemme**<br/>
$||Ax-d||_ {2,m}$ minimal ssi $(Ax-d)\perp Im(A)$
