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

**Existence et unicité de la solution du $(P)$**:  
*Théorème:* (Cauchy-Lipschitz)

Si $f$ est *lipschitzienne* par rapport à sa seconde variable (y), c'est à dire:

\begin{align*}
&\exists k>0,\ \forall t\in[0,T],\ \forall (y_ 1, y_ 2)\in\mathbb R^2,
\\
&|f(t,y_ 2)-f(t, y_1)|\leq k|y_ 2-y_ 1|
\end{align*}

 
