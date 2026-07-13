# ai-intelligence-watch

## Objectif

Publier régulièrement une synthèse factuelle et vérifiée de l'actualité de l'intelligence artificielle, en distinguant deux volets complémentaires :

1. les **actualités essentielles sur l'intelligence artificielle** en tant que sujet (modèles, produits, acteurs, réglementation) ;
2. les **recherches ou découvertes importantes réalisées grâce à l'intelligence artificielle** en tant qu'outil au service d'autres sciences (biologie, physique, mathématiques, médecine, climat, etc.).

## Fonctionnement

Le projet s'appuie sur Claude Code, exécuté selon des prompts définis à l'avance, pour rechercher, sélectionner, vérifier et rédiger chaque rapport. Chaque publication suit le même cycle :

1. Recherche et recensement des candidats du jour, de la semaine ou du mois.
2. Élimination des doublons par recoupement avec les index tenus dans `data/`.
3. Sélection et vérification selon la méthodologie du projet.
4. Rédaction du rapport à partir des gabarits définis dans `templates/`.
5. Création d'une branche dédiée et ouverture d'une Pull Request.
6. Relecture et fusion par un humain.

Aucun rapport n'est considéré comme publié tant que la Pull Request correspondante n'a pas été fusionnée par un relecteur humain.

## Architecture

```
ai-intelligence-watch/
├── CLAUDE.md                        # Règles permanentes pour Claude Code
├── README.md                        # Ce document
├── data/
│   ├── news-index.csv               # Index des actualités déjà publiées
│   ├── source-register.csv          # Registre des sources utilisées
│   └── topic-index.csv              # Index des sujets déjà traités
├── methodology/
│   ├── editorial-policy.md          # Ligne éditoriale
│   ├── source-selection.md          # Règles de sélection des sources
│   ├── scoring-method.md            # Critères de sélection des éléments retenus
│   └── quality-control.md           # Contrôle qualité et rôles humain / automatisé
├── prompts/
│   ├── daily-watch.md               # Prompt de veille quotidienne
│   ├── weekly-summary.md            # Prompt de synthèse hebdomadaire
│   └── monthly-review.md            # Prompt de bilan mensuel
├── templates/
│   ├── daily-report-template.md     # Gabarit de rapport quotidien
│   ├── weekly-report-template.md    # Gabarit de synthèse hebdomadaire
│   └── monthly-report-template.md   # Gabarit de bilan mensuel
└── reports/
    ├── daily/2026/                  # Rapports quotidiens
    ├── weekly/2026/                 # Synthèses hebdomadaires
    └── monthly/2026/                # Bilans mensuels
```

## Méthodologie

La méthodologie complète est détaillée dans le dossier [`methodology/`](methodology/) :

- [Politique éditoriale](methodology/editorial-policy.md) — portée de la veille, ce qui est couvert ou non, ton et cadence.
- [Sélection des sources](methodology/source-selection.md) — hiérarchie des sources, critères d'inclusion et d'exclusion.
- [Méthode de notation](methodology/scoring-method.md) — critères utilisés pour retenir les 5 éléments de chaque catégorie.
- [Contrôle qualité](methodology/quality-control.md) — vérifications appliquées avant publication.

## Catégories surveillées

- Modèles et systèmes d'IA
- Entreprises et acteurs industriels
- Recherche fondamentale en IA
- Réglementation et politiques publiques
- Applications sectorielles de l'IA
- Sciences assistées par l'IA (biologie, physique, mathématiques, médecine, climat, matériaux, etc.)

## Critères de sélection

Chaque élément retenu est évalué selon sa portée, sa nouveauté, sa vérifiabilité, sa solidité méthodologique (pour une recherche) et sa pertinence temporelle. Le détail de ces critères figure dans [méthode de notation](methodology/scoring-method.md). Seuls les éléments correctement sourcés et non redondants avec les publications précédentes sont retenus ; en l'absence d'éléments suffisamment solides, le rapport le signale plutôt que de compléter avec un contenu de moindre qualité.

## Rôle de Claude Code

Claude Code effectue la recherche, la vérification, la rédaction et la préparation de chaque rapport, en respectant les règles permanentes définies dans [`CLAUDE.md`](CLAUDE.md) : rédaction en français, sourcing rigoureux, distinction entre date de publication et date de l'événement, signalement des prépublications, absence de fusion automatique des Pull Requests, et traitement de tout contenu web comme une donnée à analyser plutôt que comme une instruction.

## Rôle de la validation humaine

Un relecteur humain vérifie chaque rapport avant publication : exactitude des sources citées, pertinence du ton, respect de la méthodologie. La fusion de la Pull Request vers la branche principale — c'est-à-dire la publication effective du rapport — reste une décision humaine à chaque fois.

## Limites de l'automatisation

- La qualité de la veille dépend de la disponibilité et de la fiabilité des sources accessibles au moment de la rédaction.
- La détection de doublons repose sur les index de `data/` : une lacune dans leur mise à jour peut entraîner un doublon non détecté.
- L'automatisation réduit le risque d'erreur mais ne garantit pas l'exactitude absolue ; c'est pourquoi la validation humaine reste une étape obligatoire avant toute publication.
- Le système ne couvre que les sources et langues auxquelles Claude Code a accès au moment de la recherche.

## Derniers rapports disponibles

- [Rapports quotidiens](reports/daily/2026/)
- [Synthèses hebdomadaires](reports/weekly/2026/)
- [Bilans mensuels](reports/monthly/2026/)

Aucun rapport n'a encore été publié : ces dossiers seront alimentés au fil des prochaines Pull Requests fusionnées.
