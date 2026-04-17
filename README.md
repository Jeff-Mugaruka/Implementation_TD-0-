# Implémentation de TD(0) dans un environnement Grid World

## 1. Présentation générale

Ce projet met en œuvre l’algorithme **Temporal Difference Learning TD(0)** dans un environnement discret de type **Grid World**.  
L’objectif principal est d’estimer la **fonction de valeur d’état** \(V(s)\) à partir des interactions d’un agent avec son environnement.

L’approche retenue n’est pas une approche de contrôle optimal.  
L’agent **n’apprend pas une nouvelle politique** au cours de l’exécution. Il suit une **politique fixe stochastique**, orientée vers le terminal de plus forte récompense, et l’algorithme TD(0) sert à **évaluer cette politique** en apprenant progressivement la valeur des états de la grille.

Le projet a été développé dans un cadre pédagogique pour illustrer concrètement :
- la modélisation d’un environnement de renforcement simple ;
- la représentation tabulaire de \(V(s)\) ;
- le mécanisme de mise à jour de TD(0) ;
- l’effet des hyperparamètres sur l’apprentissage ;
- l’interprétation graphique et numérique des résultats obtenus.

---

## 2. Objectifs du projet

Le projet poursuit les objectifs suivants :

- reproduire en Python un environnement **Grid World 5 × 5** comportant un état initial, des obstacles et des états terminaux ;
- implémenter la logique de transition de l’agent dans la grille ;
- représenter la fonction de valeur \(V(s)\) sous forme tabulaire ;
- implémenter la règle de mise à jour de **TD(0)** ;
- entraîner l’agent sur plusieurs épisodes ;
- visualiser l’apprentissage en temps réel grâce à une **interface Tkinter animée** ;
- produire un résumé global des performances ;
- générer des figures et tableaux exploitables dans un rapport académique.

---

## 3. Principe théorique utilisé

Le cœur du projet repose sur la règle de mise à jour suivante :

<img width="992" height="332" alt="image" src="https://github.com/user-attachments/assets/852be78f-3ee6-4beb-8fa0-3d333f6a8091" />


Le terme :

\[
\delta_t = r_{t+1} + \gamma V(s_{t+1}) - V(s_t)
\]

correspond à l’**erreur temporelle**.  
Cette quantité mesure l’écart entre ce que l’agent pensait obtenir et ce que l’expérience lui apprend effectivement.

---

## 4. Description de l’environnement

L’environnement utilisé est une grille de taille **5 lignes × 5 colonnes**.

### 4.1 États particuliers

- **État initial** : position de départ de l’agent
- **État terminal +5** : terminal de récompense positive intermédiaire
- **État terminal +10** : terminal de récompense positive maximale
- **Obstacles** : cases inaccessibles

### 4.2 Actions disponibles

L’agent dispose de quatre actions :

- `UP`
- `DOWN`
- `LEFT`
- `RIGHT`

### 4.3 Règle de transition

À chaque étape :
- si l’action demandée mène à une case valide, l’agent se déplace ;
- si l’action mène hors de la grille, l’agent reste sur place ;
- si l’action mène à un obstacle, l’agent reste aussi sur place ;
- si l’état atteint est terminal, l’épisode s’arrête.

---

## 5. Politique utilisée

L’agent suit une **politique fixe stochastique** inspirée du schéma du rapport de travail.

### 5.1 Idée générale

Dans chaque état non terminal accessible :
- une **action préférée** est définie ;
- cette action possède la probabilité la plus forte ;
- les autres actions conservent une faible probabilité.

### 5.2 Conséquence

Cette politique :
- oriente globalement l’agent vers le terminal `+10` ;
- conserve une petite part d’aléa ;
- permet de rester dans une logique d’**évaluation de politique** plutôt que d’optimisation de politique.

Autrement dit, le projet estime :

\[
V^\pi(s)
\]

où \(\pi\) désigne la politique fixe choisie.

---

## 6. Architecture technique du projet

Le projet est organisé de manière modulaire afin de séparer clairement :
- l’environnement ;
- la politique ;
- l’apprentissage ;
- l’interface ;
- l’analyse ;
- le résumé des performances.

### Arborescence

```text
td0_gridworld/
│
├── main.py
├── config.py
├── gridworld.py
├── policy.py
├── agent.py
├── ui.py
├── performance.py
├── analysis.py
├── requirements.txt
├── README.md
│
├── outputs/
│   ├── figures/
│   ├── tables/
│   └── summaries/
│
└── report/
    └── rapport.md
