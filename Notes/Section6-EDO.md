# Section 6: Equations Différentiels Ordinaires

## Partie 1 - Résolution numérique des EDO d'ordre 1.

### 1 Cadre théorique:

On considère le problème de Cauchy suivant:

$$
(P):\begin{cases}
y'(t)=f(t,y(t)),\ \forall t \in [0,T]\ (E)\\
y(t_ 0=0)=\alpha\ (CI) 
\end{cases}
$$

Où $[0,T]$ est l'intervalle de résolution, $f:\ \left[\mathbb R^2 \rightarrow \mathbb R\ |\ (t,y)\mapsto f(t,y)\right]$, $(E)$ est l'EDO et $(CI)$ la condition initiale.

**Existence et unicité de la solution du $(P)$ sur $[0,T]$**:  
*Théorème:* (Cauchy-Lipschitz)

Si $f$ est *lipschitzienne* par rapport à sa seconde variable (y), c'est à dire:

$$
\begin{aligned}
&\exists k>0,\ \forall t\in[0,T],\ \forall (y_ 1, y_ 2)\in\mathbb R^2,
\\
&|f(t,y_ 2)-f(t, y_1)|\leq k|y_ 2-y_ 1|
\end{aligned}
$$
 
Alors il existe une solution *unique* à $(P)$ sur $[0,T]$. 

### 2 Résolution numérique:
**2.a) Solution discrète:**  

On se donne un _maillage **uniforme**_ de l'intervalle de résolution $[0,T]$ en subdivisant $[0,T]$ en $N$ sous-intervalles de même largeur $h=\frac T N$ appelée *pas du maillage*.  
On introduit la solution *discrète* $(y_ n)_ {0\leq n \leq N}$:

$$
y_ n=y(t=t_ n),\ \forall n \in [0,N]
$$

Où $y=$ (vraie) solution de $(P)$.

**But:** calculer la solution discrète $(y_ n)_ {0\leq n \leq N}$ en les points $(t_ n)$ du maillage avec un pas $h$ suffisamment petit pour avoir une représentation la plus fidèle/précise possible de la solution exacte $y$ de $(P)$.

**2.b) Méthodologie générale de résolution numérique de $(P)$:**  

Soit l'équation différentielle suivante:

$$
y'(t)=f(t,y(t))\ (E)
$$

On intègre $(E)$ entre $t_ n$ et $t_ {n+1}$ (où $n\in[0,N - 1]$):

$$
\begin{aligned}
&\int^{t_ {n+1}}_ {t_ n}y'(t)dt=\int^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
\\
\iff & \left[y(t)\right]^{t_ {n+1}}_ {t_ n}=\int^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
\\
\iff & y(t_ {n+})-y(t_ n)=\int^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
\\
\iff & y_ {n+1}=y_ n+\int^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
\end{aligned}
$$

Chaque méthode de résolution numérique de $(P)$ (au moins celle que l'on verra) repose sur l'égalité précédente et une méthode particulière *d'intégration numérique* de $\int^{t_ {n+1}}_ {t_ n}f(t,y(t))dt$.

**2.c) Méthodes/schémas numériques:**  

**Méthode d'Euler explicite:**  
Elle repose sur la méthode des rectangles à gauche pour approcher $\int^{t_ {n+1}} _{t_ {n}}f(t,y(t))dt$:

$$
\int^{t_ {n+1}} _{t_ {n}}f(t,y(t))dt\approx \frac{t_ {n+1}-t_ {n}}{1} f(t_ {n},y(t_ {n}))\approx hf(t_ {n},y(t_ {n}))
$$

(On a appliqué la méthode des rectangles avec "1 seule subdivision" de l'intervalle). On construit donc la solution discrète *approchée* $(y_ {n})_ {0\leq n\leq N}$. Avec la relation de récurrence:

$$
y_ {n+1}=y_ {n}+hf(t_ {n},y_ {n})
$$

En initialisant avec $y_ {0}=\alpha$ qui vient de la CI: $y(t=0)=\alpha$.  
On calcule donc dans l'ordre une approximation de $y(t_ {1}=h)$ puis $y(t_ {2}=2h)$ puis $\dots$ jusqu'à $y(t_ {n}=Nh=T)$.

**Méthode d'Euler implicite:**  
On va utiliser la méthode des rectangles à droite:

$$
\int^{t_ {n+1}} _{t_ {n}}f(t,y(t))dt\approx \frac{t_ {n+1}-t_ {n}}{1} f(t_ {n+1},y(t_ {n+1}))\approx hf(t_ {n+1},y(t_ {n+1}))
$$

Schéma d'Euler implicite:

$$
y_ {n+1}=y_ {n}+hf(t_ {n+1},y_ {n+1})
$$

On obtient donc une équation à résoudre pour trouver $y_ {n+1}$ en connaissant $y _ {n}$:

$$
y_ {n+1}-hf(t_ {n+1},y_ {n+1})=0
$$

-> Équation du type $g(x)=0$.  
En générale, il y a 2 inquiètes de faire:

- Si $f$ est simple, on peut espérer pouvoir résoudre l'équation manuellement (sur papier).
- Sinon on utilise une méthode du chapitre 3 (Newton, point fixe, sécante...).

**Schéma de Crank-Nicholson (ou méthode des trapèzes implicite):**  
On utilise la méthode des trapèzes pour approcher l'intégrale:

$$
\begin{aligned}
\int^{t_ {n+1}} _{t_ {n}}f(t,y(t))dt & \approx h\left[\frac{f(t_ {n},y(t_ {n}))+f(t_ {n+1},y(t_ {n+1}))}{2}\right]
\\
& \approx \frac{h}{2} \left[f(t_ {n},y(t_ {n}))+f(t_ {n+1},y(t_ {n+1}))\right]
\end{aligned}
$$

Méthode de Crank-Nicholson:

$$
y_ {n+1}=y_ {n}+\frac{h}{2} \left[f(t_ {n},y(t_ {n}))+f(t_ {n+1},y(t_ {n+1}))\right]
$$

A chaque itération, on doit résoudre l'équation:

$$
y_ {n+1}-f(t_ {n+1},y_ {n+1})-y_ {n}-f(t_ {n},y_ {n})=0
$$

Idem on résout soit manuellement, soit avec Newton.

## Partie 2 - Ordre et stabilité:
### 1 Ordre d'un méthode
**1.a) Déf:** 

Soit $(y_ {n})_ {o\leq N\leq N}$ la solution numérique (discrète) fournie par l'application d'une méthode de résolution numérique $M$ du problème $(P)$, alors on dit $M$ est d'ordre $p\ (\in \mathbb N^\ast$ si il existe $C\in \mathbb R^{\ast}_ {+}$ telle que:

$$
E(h)=|y^{h}_ {N}-y(T)|\lessapprox Ch^{p}
$$

Ou $y^{h}_ {N}$ est la solution numérique à $t=t_ {n}=T$ et $y(T)$ est la solution exacte (ou vraie) à $t=T$.

Pour déterminer l'ordre d'une méthode $M$, on trace $log(E(h))$ en fonction de $log(h)$ et on determine la pente de la quasi-droite obtenue, qui nous donne $p$.  
Si on prend $log(N)$ en abscisses alors la pente est égale à $-p$.

**1.b) Ordre des méthodes classiques:**

- Méthodes d'Euler (implicite *et* explicite): ordre 1
- Méthodes des trapèzes (implicite [ou Crank-Nicholson] et explicite [Runge-Kutta d'ordre 2]): ordre 2

### 2 Stabilité d'une méthode
**2.a) Déf:**

On dit qu'une méthode numérique $M$ est stable si la solution numérique $(y_ {n})_ {0\leq n\leq N}$ correspondante reste *bornée* pour tout $h>0$, c'est à dire: $\exists K>0$ tel que:

$$
\sup_ {h\in \mathbb R^{\ast}_ {+}}\{||(y_ {n}^{h})||_ {\infty}\}\leq K
$$

Où $||(y_ {n}^{h})||_ {\infty}=\max_ {\{0\leq n\leq N\}}|y_ {n}^{h}|$.  
On dit que la solution numérique *explose* lorsque $||(y_ {n}^{h})||_ {\infty}\nearrow$ fortement lorsque $h\nearrow\implies$ instabilité.

**2.b) Exemple:**

On considère le problème de Cauchy:

$$
\begin{cases}
y'(t)=-ay(t),\ \forall t\in[0,T]
\\
y(0)=y_ {0}
\end{cases}
$$

Où $a>0$ et la solution exacte est: $y(t)=y_ {0}e^{-at}$.

- Euler explicite:

$$
\begin{aligned}
& y_ {n+1}=y_ {n}+hf(t_ {n},y_ {n}).
\\
\textrm{Ici}: & y_ {n+1}=y_ {n}+h(-ay_ {n})
\\
\iff & y_ {n+1}=(a-ah)y_ {n}
\end{aligned}
$$

Donc $y_ {n}=(1-ah)^{n}y_ {0}$, D'où $||(y_ {n})||_ {\infty}=\max|y_ {n}|$ dépend de la valeur de $r=1-ah$.

**Première cas**: $r=|1-ah|<1$,  
alors $||(y_ {n})||_ {\infty}=y_ {0}$ 

**Deuxième cas:** $r=1$,  
alors $||(y_ {n})||_ {\infty}=|y_ {0}|$

**Troisième cas:** $r>1$,  
alors $||(y_ {n})||_ {\infty}=|y_ {N}|$ 

Donc dans le première cas:

$$
sup_ {h\in]o,T]}\{||y_ {n})||_ {\infty}\}=|y_ {0}|\rightarrow \ \textrm{borné}\ \implies \ \textrm{stable}
$$

Dans le deuxième cas, idem mais la solution numérique ne converge pas vers la solution exacte:

$$
y_ {n}=y_ {0},\ \forall n\in [0,N]\rightarrow \ \textrm{solution numérique constante}\ 
$$

Alors que $y(t)=y_ {0}e^{-at}$ 

$$
\implies \lim_ {T\rightarrow +\infty}|y_ {N}-g(T)|=y_ {0}\neq 0
$$

-> Pas d'instabilité mais la solution numérique n'approche plus la solution exacte.

Dans le troisième cas, $||(y_ {n})||_ {\infty}$ non borné suivant $h$ $\implies$ *instabilité*.

Donc la méthode sera stable si et seulement si on est dans le cas 1 (ou 2), autrement dit, $|1-ah|\leq 1$, $\iff h\leq\frac{2}{a}$. On dit que $\frac{2}{a}$ est le seuil de stabilité de la méthode d'Euler explicite *pour l'EDO considérée*.  
**Si on change l'EDO, on change le seuil de stabilité!**

Par contre, c'est un résultat général: la méthode d'Euler explicite est *stable sous condition* de type $h<\ \textrm{seuil}\ $. 

- Euler implicite:

$$
y_ {n+1}=y_ {n}+f(t_ {n+1},y_ {n+1})
$$

Ici, cela donne:

$$
\begin{aligned}
&y_ {n+1}=y_ {n}-ahy_ {n+1}
&\iff y_ {n+1}=\frac{1}{1+ah}y_ {n}
\end{aligned}
$$

-> Suite géométrique de raison $r=\frac{1}{1+ah}$. Où $a$ et $h$ sont tous $>0$, $\implies 1+ah>1$.

Donc $o<r<1$  
D'où $||(y_ {n})||_ {\infty}=y_ {0}$ et donc la méthode sera *toujours stable*! C'est un résultat général, la méthode d'Euler implicite est **inconditionnellement stable**.

**À retenir:** Les méthodes explicites sont toutes stables sous condition de type $h<\ \textrm{seuil}\ $ et les méthodes implicites sont toutes inconditionnellement stables.

## Partie 3 - Systèmes d'EDO
Système à $p$ équations à $p$ inconnues $y _ {1}(t),\dots,y_ {p}(t)$:

$$
\begin{cases}
Y'(t)=F(t,Y(t)),\ \forall t\in [o,T]
\\
Y(0)=Y_ {0}\in\mathbb R^p
\end{cases}
$$

Où:

$$
Y(t)=
\begin{pmatrix}
y_ {1}(t)\\
\vline\\
y_ {p}(t)
\end{pmatrix}
\in\mathbb R^p
$$

$$
F:
\begin{pmatrix}
\mathbb R\times \mathbb R^p\rightarrow \mathbb R^p
\\
(t,y_ {1},\dots,y_ {p})\mapsto
\begin{pmatrix}
f_ {1}(t,y_ {1},\dots,y_ {p})
\\
f_ {p}(t,y_ {1},\dots,y_ {p})
\end{pmatrix}
\end{pmatrix}
$$

On note $F(t,Y)=F(t,y_ {1},\dots,y_ {p})$.

**Théorème:** Cauchy, idem avec F lipschitzienne par rapport à sa seconde variable (vectorielle) Y:

$$
\begin{aligned}
\exists k>0&,\forall t\in[0,1],\ \forall(Y_ {1},Y_ {2})\in\mathbb R^p\times\mathbb R^p:
\\
||F(t,&Y_ {2})-F(t,Y_ {1})||\leq k||(Y_ {2}-Y_ {1}||
\\
\implies &\exists \ \textrm{solution unique}\ Y \ \textrm{sur}\ [o,T]
\end{aligned}
$$

->Les méthodes ne changent pas.

Euler explicite:

$$
Y_ {n+1}=Y_ {n}+F(t_ {n},Y_ {n})
$$

Euler implicite:

$$
Y_ {n+1}=Y_ {n}+F(t_ {n+1},Y_ {n+1})
$$

**Exemple:**

$$
\begin{cases}
y'_ {1}(t)=y_ {2}(t)+t
\\
y'_ {2}(t)=y_ {1}(t)+2t
\end{cases}
$$

Euler explicite donne:

$$
\begin{cases}
y_ {1,n+1}=y_ {1,n}+h(y_ {2,n}+t_ {n})
\\
y_ {2,n+1}=y_ {2,n}+h(y_ {1,n}+2t_ {n})
\end{cases}
$$

-> Ordre et stabilité restent inchangés à ceci près qu'on utilisera des normes à la place des valeurs absolues.

-> On peut transformer toute EDO d'ordre $k\ge 2$ en un système $Y'(t)=F(t,Y(T))$ où:

$$
Y(t)=
\begin{pmatrix}
y(t)\\
y'(t)\\
\vdots \\
y^{(k-1)}(t)
\end{pmatrix}
$$






