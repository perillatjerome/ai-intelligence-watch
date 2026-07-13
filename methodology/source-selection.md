# Sélection des sources

## Principe général

La qualité de la veille dépend directement de la qualité des sources utilisées. Ce document fixe les règles de sélection, de hiérarchisation et de traçabilité des sources.

## Hiérarchie des sources

Par ordre de préférence décroissant :

1. **Sources primaires** : article de recherche original, dépôt de préprint (arXiv, bioRxiv, etc.), communiqué officiel d'un laboratoire ou d'une entreprise, dépôt de code, documentation technique publiée par l'auteur du travail.
2. **Presse spécialisée reconnue** : médias avec une expertise technique établie et des pratiques de vérification documentées.
3. **Presse généraliste** : utilisée en complément, notamment pour l'impact sociétal ou réglementaire d'une annonce, jamais comme unique source d'un fait technique.
4. **Réseaux sociaux et blogs personnels** : utilisés uniquement comme point de départ pour identifier un sujet, jamais comme source finale. Le fait doit être retracé jusqu'à une source primaire avant publication.

## Registre des sources

Toutes les sources effectivement utilisées sont consignées dans [`data/source-register.csv`](../data/source-register.csv), avec leur catégorie et leur niveau de fiabilité tel qu'évalué au moment de l'ajout.

## Critères d'inclusion d'une source

Une source est retenue si elle satisfait au moins les critères suivants :

- Elle identifie clairement son auteur ou son organisation.
- Elle date explicitement sa publication.
- Elle permet de remonter à l'origine de l'information (lien, référence, DOI).

## Critères d'exclusion

Une source est écartée si :

- Elle ne peut pas être attribuée à un auteur ou une organisation identifiable.
- Elle a été identifiée comme diffusant de manière récurrente des informations non vérifiées.
- Elle constitue du contenu généré automatiquement sans supervision éditoriale déclarée.

## Cas des prépublications

Les prépublications (preprints) sont des sources légitimes mais doivent systématiquement être signalées comme non évaluées par les pairs dans le rapport final, conformément à [`CLAUDE.md`](../CLAUDE.md).

## Vérification croisée

Pour toute annonce qualifiée d'importante (voir [scoring-method.md](scoring-method.md)), une deuxième source indépendante est recherchée avant publication. L'absence de confirmation croisée est mentionnée explicitement dans le rapport plutôt que passée sous silence.
