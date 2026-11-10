# Rapport de synthèse — Étude et expérimentation de 29 algorithmes de Machine Learning

*\[Prénom NOM\] — ENCG Settat, Sciences de Gestion (Finance et Audit), S7 — \[date de remise\]*

> **Mode d'emploi (à supprimer avant de rendre).** Ce squelette suit la consigne (5 à 8 pages). Chaque section indique sa longueur cible et ce qu'elle doit contenir. Tout ce qui est entre crochets **\[À COMPLÉTER\]** doit être remplacé par vos propres résultats, lus dans les sorties de votre notebook. Ne recopiez aucun chiffre qui ne figure pas dans vos tableaux, et n'écrivez pas qu'un modèle est « meilleur » si l'écart est dans la marge de variation.

## 1. Introduction *(½ page)*

**Objectif.** Comprendre le principe, les contextes d'usage et les performances de 29 algorithmes de Machine Learning, répartis en six familles : régression, classification, clustering, réduction de dimension, détection d'anomalies et renforcement.

**Démarche en deux temps.** (1) Partie A : pour chaque algorithme, une présentation, un schéma, des contextes d'utilisation et l'analyse d'une expérience de démonstration sur données synthétiques. (2) Partie B : tests sur des jeux de données publics et réels, avec une méthode de référence et au moins une méthode avancée par famille.

**Annonce du plan.** \[1 à 2 phrases : ce que le lecteur trouvera dans chaque section.\]

## 2. Données et préparation *(1 page)*

### 2.1 Jeux de données utilisés

| Jeu de données | Source | Licence | Taille | Cible | Utilisé pour |
| --- | --- | --- | --- | --- | --- |
| Default of Credit Card Clients | UCI Machine Learning Repository (I-C. Yeh, 2009) | CC BY 4.0 | 30 000 lignes, 23 variables explicatives | défaut de paiement le mois suivant (0/1) | classification (algorithmes 8 à 16) |
| California Housing | StatLib / scikit-learn (Pace & Barry, 1997) | **\[À COMPLÉTER\]** | 20 640 lignes, 8 variables explicatives | valeur médiane des logements | régression (algorithmes 1 à 7) |
| Online Retail | UCI Machine Learning Repository (D. Chen, 2015) | CC BY 4.0 | 541 909 lignes, 8 colonnes | aucune (non supervisé) | clustering, réduction de dimension, anomalies (algorithmes 17 à 24) |
| Blackjack-v1, FrozenLake-v1 | Gymnasium (Farama Foundation) | **\[À COMPLÉTER\]** | environnements simulés | récompense, taux de réussite | bandits, Q-learning, SARSA (algorithmes 25 à 28) |

**Dates de consultation et d'exécution :** \[À COMPLÉTER\].

**Précision à écrire clairement :** les environnements Gymnasium ne sont pas des données réelles ; les trajectoires sont produites par simulation. Le DQN (algorithme 29) reste conceptuel et n'a pas fait l'objet d'une expérience complète (choix facultatif prévu par la consigne).

### 2.2 Qualité des données et décisions de nettoyage

À résumer en un court paragraphe ou un tableau par jeu de données (valeurs manquantes, doublons, valeurs extrêmes, déséquilibre) :

- **Crédit :** aucune valeur manquante ; 22,1 % de clients en défaut (classes déséquilibrées) ; 35 doublons hors identifiant, conservés car deux clients peuvent avoir le même profil ; modalités non documentées par UCI (`EDUCATION` = 0, 5, 6 ; `MARRIAGE` = 0) regroupées dans « autres » par une règle fixe ; factures négatives (soldes créditeurs) conservées.
- **California Housing :** \[À COMPLÉTER : manquants, plafonnement de la cible à 5,0, extrêmes\].
- **Online Retail :** \[À COMPLÉTER : part de lignes sans identifiant client, annulations, doublons, quantités ou prix non positifs ; construction des profils clients RFM ; ce que ces choix font perdre\].

### 2.3 Protocole d'évaluation

Séparation entraînement / validation / test (60 / 20 / 20) ; hyperparamètres choisis sur la validation uniquement ; test utilisé une seule fois par modèle ; prétraitements ajustés sur l'entraînement dans un `Pipeline` (pas de fuite d'information) ; graine fixée à 42 ; versions des bibliothèques : \[À COMPLÉTER, recopier l'affichage du notebook\]. Aucune validation chronologique n'était applicable : aucun des 29 algorithmes n'est un modèle de série temporelle et aucune tâche n'est une prévision dans le temps.

## 3. Résultats par famille *(3 pages)*

Pour chaque famille : un tableau comparatif et une phrase de lecture. Les noms de colonnes ci-dessous sont ceux de votre notebook.

### 3.1 Classification : défaut de paiement

Méthode de référence : régression logistique. Méthodes avancées : forêt aléatoire, gradient boosting, AdaBoost, XGBoost.

| Modèle | Rôle | Précision | Rappel | F1 | ROC-AUC | PR-AUC | Temps d'ajustement (s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| \[À COMPLÉTER\] |  |  |  |  |  |  |  |

*Figure \[n\] : courbes précision–rappel sur le jeu de test.* **Lecture (2 à 4 phrases) :** \[la référence est-elle dépassée, de combien, l'écart est-il significatif pour \~6 000 clients de test ? quel compromis précision/rappel pour un risque de crédit ?\] Rappeler que le SVM est entraîné sur un sous-échantillon de 8 000 lignes.

### 3.2 Régression : valeur des logements

Méthode de référence : régression linéaire. Méthodes avancées : forêt aléatoire, gradient boosting.

| Modèle | Rôle | MAE | RMSE | R² | Temps d'ajustement (s) |
| --- | --- | --- | --- | --- | --- |
| \[À COMPLÉTER\] |  |  |  |  |  |

*Figure \[n\] : valeurs prédites en fonction des valeurs observées.* **Lecture :** \[gain des modèles avancés ; apport du polynôme de degré 2 ; effet de Ridge/Lasso ; limites : plafonnement de la cible, corrélation spatiale entre secteurs voisins\].

### 3.3 Clustering

K-means (référence), classification hiérarchique, mélanges gaussiens, DBSCAN.

| Méthode | Groupes | Part de bruit | Silhouette | Davies–Bouldin | Stabilité (ARI moyen) | Temps (s) |
| --- | --- | --- | --- | --- | --- | --- |
| \[À COMPLÉTER\] |  |  |  |  |  |  |

**Lecture :** \[nombre de groupes retenu et critère ; stabilité ; **nom métier de chaque groupe, justifié par le tableau des profils** ; précision que DBSCAN rejette une part des clients, donc la comparaison de silhouette n'est pas à armes égales ; aucune évaluation externe car aucune étiquette réelle\].

### 3.4 Réduction de dimension

| Méthode | Trustworthiness (10 voisins) | Variance expliquée (2 comp.) | Temps (s) |
| --- | --- | --- | --- |
| \[À COMPLÉTER\] |  |  |  |

**Lecture :** \[composantes nécessaires pour environ 80 % de variance ; méthode qui conserve le mieux les voisinages et son coût ; rappel que les distances entre îlots de t-SNE et d'UMAP ne s'interprètent pas\].

### 3.5 Détection d'anomalies

Référence : z-score robuste. Avancée : Isolation Forest. Comparaison : LOF. Taux d'alertes fixé à 2 % par construction.

| Élément | Résultat |
| --- | --- |
| Accord entre méthodes (Jaccard) | \[À COMPLÉTER\] |
| Stabilité d'Isolation Forest selon la graine | \[À COMPLÉTER\] |
| Description des alertes (médianes des variables) | \[À COMPLÉTER\] |

**Lecture :** \[que sont réellement les clients signalés ; ne pas parler de fraude ; pas de précision/rappel car aucune étiquette fiable\].

### 3.6 Renforcement (simulation)

| Expérience | Algorithme | Résultat principal | Variation entre graines |
| --- | --- | --- | --- |
| Bandits (Blackjack) | aléatoire / ε-greedy / UCB1 | \[récompense cumulée, regret, part sur le meilleur bras\] | \[À COMPLÉTER\] |
| FrozenLake glissant | Q-learning / SARSA / aléatoire | \[taux de réussite de la politique finale\] | \[À COMPLÉTER\] |

**Lecture :** \[écart par rapport à la politique aléatoire ; différence entre Q-learning et SARSA visible ou non sur cet environnement, en comparant l'écart à la variation entre graines\].

## 4. Tableau comparatif final *(½ page)*

| Famille | Méthode de référence | Méthode avancée | Métrique | Valeur référence | Valeur avancée | Coût de calcul | Interprétabilité |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Classification | Régression logistique | \[À COMPLÉTER\] | PR-AUC | \[ \] | \[ \] | \[ \] | \[ \] |
| Régression | Régression linéaire | \[À COMPLÉTER\] | RMSE | \[ \] | \[ \] | \[ \] | \[ \] |
| Clustering | K-means | \[À COMPLÉTER\] | silhouette | \[ \] | \[ \] | \[ \] | \[ \] |
| Réduction de dimension | ACP | \[À COMPLÉTER\] | trustworthiness | \[ \] | \[ \] | \[ \] | \[ \] |
| Anomalies | z robuste | Isolation Forest | accord / stabilité | \[ \] | \[ \] | \[ \] | \[ \] |
| Renforcement | politique aléatoire | \[À COMPLÉTER\] | taux de réussite | \[ \] | \[ \] | \[ \] | \[ \] |

## 5. Discussion *(1 page)*

- **Performance :** les méthodes avancées battent-elles les références, et l'écart justifie-t-il leur complexité ? \[À COMPLÉTER\]
- **Coût de calcul :** \[temps relevés dans vos tableaux\].
- **Interprétabilité :** modèles lisibles (régression, arbre peu profond) contre ensembles et méthodes de projection.
- **Choix de la métrique :** pourquoi PR-AUC et rappel sur un jeu déséquilibré ; pourquoi RMSE et MAE ensemble en régression.
- **Leçon transversale :** \[une idée que vous retenez, par exemple l'importance de la préparation des données ou du choix de la référence\].

## 6. Limites *(½ page)*

- un seul découpage entraînement / validation / test par jeu de données, et de petites grilles d'hyperparamètres ;
- pas de test statistique pour comparer les modèles entre eux ;
- jeux de données propres à un contexte (clients de cartes à Taïwan en 2005, logements californiens de 1990, un commerçant britannique de 2010-2011) : les résultats ne se généralisent pas tels quels ;
- clients sans identifiant exclus du clustering ; pas d'étiquettes réelles pour évaluer clustering et anomalies ;
- renforcement : environnements simplifiés, hyperparamètres non réglés, peu de graines ;
- DQN non expérimenté ;
- &#91;autres limites rencontrées lors de votre exécution\].

## 7. Conclusion *(¼ page)*

&#91;3 à 5 phrases : réponse à l'objectif de départ, principal enseignement, piste d'amélioration réaliste.\]

## 8. Usage d'une IA et reproductibilité *(¼ page)*

**Usage d'une IA (exigé par la consigne).** \[Indiquez honnêtement pour quelles tâches vous avez utilisé un assistant IA, et ce que vous avez vérifié, modifié et compris vous-même.\]

**Reproductibilité.** Notebook Google Colab joint ; graine 42 ; versions des bibliothèques en section 2.3 ; tableaux exportés en CSV dans le dossier `resultats_partieB`.

## Références

- Yeh, I.-C. (2009). *Default of Credit Card Clients* \[jeu de données\]. UCI Machine Learning Repository. https://doi.org/10.24432/C55S3H
- Chen, D. (2015). *Online Retail* \[jeu de données\]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
- Pace, R. K. et Barry, R. (1997). Sparse spatial autoregressions. *Statistics & Probability Letters*, 33(3). (California Housing, distribué par scikit-learn)
- Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12.
- Chen, T. et Guestrin, C. (2016). XGBoost: A Scalable Tree Boosting System. *KDD 2016*.
- McInnes, L., Healy, J. et Melville, J. (2018). UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction. *arXiv:1802.03426*.
- Gymnasium (Farama Foundation). https://gymnasium.farama.org/
- &#91;Ajoutez ici toute autre source réellement consultée.\]
