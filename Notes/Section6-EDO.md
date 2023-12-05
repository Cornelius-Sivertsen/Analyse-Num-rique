# Section 6: Equations Différentiels Ordinaires

## Partie 1 - Résolution numérique des EDO d'ordre 1.

### 1 Cadre théorique:

On considère le problème de Cauchy suivant:

$$
(P):\begin{cases}
y'(t)=f(t,y(t)),\ \forall t \in [0,T]\ (E)\\
y(t_ 0=0)=y_ 0\ (CI)
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

$$
y'(t)=f(t,y(t))\ (E)
$$

On intègre $(E)$ entre $t_ n$ et $t_ {n+1}$ (où $n\in[0,N - 1]$):

$$
\int\limits^{t_ {n+1}}_ {t_ n}y'(t)dt=\int\limits^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
$$

$$
\iff \left[y(t)\right]^{t_ {n+1}}_ {t_ n}=\int\limits^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
$$

$$
\iff y(t_ {n+})-y(t_ n)=\int\limits^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
$$

$$
\iff y_ {n+1}=y_ n+\int\limits^{t_ {n+1}}_ {t_ n}f(t,y(t))dt
$$

Test $x*x+x_n$

Chaque méthode de résolution numérique de $(P)$ (au moins celle que l'on verra) repose sur l'égalité précédente et une méthode particulière *d'intégration numérique* de $\int\limits^{t_ {n+1}}_ {t_ n}f(t,y(t))dt$.



