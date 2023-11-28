# Section I : Erreurs numériques

# Introduction

**Analyse Numérique:** concevoir et comprendre la résolution numérique de problèmes mathématiques issus du monde réel

*****Erreur = différence entre solution exacte et résultat numérique*****

Sources d’erreur:

- Erreurs de modélisation
- Erreurs de données
- Erreurs de discrétisation
- Erreurs d’arrondi

**But:** estimer, comprendre et anticiper les erreurs

# Calcul de l’erreur

### Erreur absolue et erreur relative:

Soit un problème P avec un solution théorique (réel/vrai) $x$ et solution numérique (approximé) $\tilde{x}$

Erreur absolue:  $\vert x-\tilde{x}\vert$ → possède un unité (celle de x)

Erreur relative:  $\vert \frac{x-\tilde{x}}{x}\vert$

# Représentation des réels en machine

Rappel: Dans la vie normale on utilise la _“base décimale”_ pour représenter des réels.

**Notion importante:** Représentation machine = *approximation* (mémoire finie).


Le représentation machine que l'on utilise c’est la ***virgule flottante normalisée:***

$$
fl(x)=\pm m\cdot b^e
$$

- b: base (b=2 en général)
- m: mantisse avec $1\le m < b $, avec p chiffres maximum en base b
- e: exposant avec $e_{min}\le e\le e_{max}$
- p: un entier positif fixé par l’architecture que l’on utilise

Deux types de précision: simple (32 bits), et double (64 bits)

| Précision | taille | mantisse | exposant | e_min | e_max |
| --- | --- | --- | --- | --- | --- |
| simple | 32 bits | 23+1 bits | 8 bits | -126 | +127 |
| double | 64 bits | 52+1 bits | 11 bits | -1022 | +1023 |

# Erreurs d’arrondi

On fait l’arrondissement de la mantisse réel d’un nombre vers la plus proche mantisse en p chiffres.

**Erreurs d’arrondi:**  $\vert \frac{fl(x)-x}{fl(x)}\vert \le u$  où $u$: unité d’arrondi

Simple précision: $u \approx 10^{-10}$ et double précision: $u\approx 10^{-16}$

**Précision machine:** la plus grand $\epsilon >0, \space tq \space fl(1+\epsilon)=1$

L’arrondissement nous donne quelques problèmes:

- Absorption: l’addition des deux nombres d’ordre de grandeur très différentes (ex. 1+$\epsilon$)
- Élimination: soustraction des deux nombres très proches en valeur
- Accumulation des erreurs
    - Exemple: $0.1+0.2 = fl[fl(0.1)+fl(0.2)]$
    - → 3 erreurs d’arrondi pour une simple addition!

# Conditionnement et stabilité

**But: quantifier la sensibilité de la solution aux erreurs**

Conditionnement d’un problème:

Mesure de l’influence des erreurs de données sur la précision de la solution final. 

- Intrinsèque au problème réel, en dehors de tout contexte numérique.

Stabilité d’un algorithme:

S’applique à un algorithme de résolution numérique où on quantifie le susceptibilité de l’ensemble des opération aux erreurs d’arrondissement.
