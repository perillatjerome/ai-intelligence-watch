# Méthode de notation et de sélection

## Objectif

Sur un flux quotidien potentiellement large d'actualités et de résultats de recherche, ce document définit comment sont sélectionnés les 5 éléments retenus par catégorie (actualités IA / découvertes assistées par IA).

## Critères de score

Chaque élément candidat est évalué selon les critères suivants (score qualitatif, pas de calcul automatique dissimulé) :

| Critère | Description |
|---|---|
| Portée | Nombre d'acteurs, de personnes ou de domaines concernés par l'information |
| Nouveauté | Caractère inédit de l'information par rapport à ce qui a déjà été publié |
| Vérifiabilité | Disponibilité d'une source primaire et, si nécessaire, d'une confirmation croisée |
| Solidité | Pour une recherche : méthodologie, revue par les pairs ou non, reproductibilité annoncée |
| Pertinence temporelle | Lien avec l'actualité récente, urgence ou fenêtre de validité de l'information |

## Processus de sélection

1. Recensement des candidats du jour dans les deux catégories.
2. Élimination des doublons par recoupement avec [`data/news-index.csv`](../data/news-index.csv) et [`data/topic-index.csv`](../data/topic-index.csv).
3. Évaluation qualitative de chaque candidat restant selon les critères ci-dessus.
4. Retenue des 5 éléments les plus significatifs par catégorie.
5. Si moins de 5 éléments de qualité suffisante sont disponibles dans une catégorie un jour donné, le rapport le mentionne explicitement plutôt que de compléter avec un élément secondaire présenté comme équivalent.

## Catégories thématiques surveillées

- Modèles et systèmes d'IA (nouveaux modèles, mises à jour majeures, benchmarks)
- Entreprises et acteurs industriels (produits, levées de fonds, partenariats)
- Recherche fondamentale en IA (nouvelles architectures, méthodes d'entraînement)
- Réglementation et politiques publiques
- Applications sectorielles de l'IA (santé, éducation, industrie, etc.)
- Sciences assistées par l'IA (biologie, physique, mathématiques, climat, médecine, matériaux, etc.)

Le détail de ces catégories est également suivi dans [`data/topic-index.csv`](../data/topic-index.csv).

## Non-automatisation du jugement final

Ce score qualitatif encadre la sélection mais ne la remplace pas : la décision finale de retenir un élément reste une évaluation éditoriale documentée dans le rapport, pas un calcul opaque.
