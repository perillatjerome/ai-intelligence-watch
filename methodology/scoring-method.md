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

### Actualités sur l'intelligence artificielle

- Nouveaux modèles d'intelligence artificielle
- Multimodalité
- Agents IA
- Automatisation
- API et outils de développement
- Claude Code, GitHub et programmation assistée
- Adoption de l'IA en entreprise
- Transformation numérique
- Gestion de projet IA
- Réglementation et AI Act
- Sécurité, gouvernance et conformité
- Open source
- Robotique
- Infrastructures, centres de données et semi-conducteurs
- Investissements, partenariats et acquisitions importantes

### Recherches et découvertes réalisées grâce à l'IA

- Santé et médecine
- Biologie
- Génomique
- Découverte de médicaments
- Matériaux
- Énergie
- Climat et environnement
- Agriculture
- Mathématiques
- Physique
- Chimie
- Astronomie et spatial
- Archéologie
- Robotique scientifique

Le détail de ces catégories est également suivi dans [`data/topic-index.csv`](../data/topic-index.csv). Voir aussi [editorial-policy.md](editorial-policy.md) pour la présentation éditoriale de ces catégories.

## Règles de diversité

Au-delà du score qualitatif par élément, la sélection des 5 éléments par catégorie respecte les règles de diversité suivantes :

- Ne pas sélectionner cinq informations provenant toutes de la même entreprise.
- Ne pas sélectionner cinq informations appartenant toutes à la même catégorie thématique.
- Privilégier une diversité de secteurs, d'acteurs et de zones géographiques.
- Une recherche ne doit pas être sélectionnée simplement parce qu'elle mentionne l'intelligence artificielle : l'IA doit jouer un rôle substantiel dans la méthode ou le résultat, pas une mention accessoire.
- Ne retenir une information que si elle apporte une nouveauté réelle par rapport à ce qui a déjà été publié ou à ce qui est déjà connu du domaine.

## Non-automatisation du jugement final

Ce score qualitatif encadre la sélection mais ne la remplace pas : la décision finale de retenir un élément reste une évaluation éditoriale documentée dans le rapport, pas un calcul opaque.
