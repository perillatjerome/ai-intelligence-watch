# Prompt — Bilan mensuel

## Contexte

Ce prompt sert de base pour produire le bilan mensuel, qui prend du recul sur l'ensemble des rapports quotidiens et hebdomadaires du mois écoulé.

## Instructions

1. Relis les rapports hebdomadaires du mois dans `reports/weekly/` ainsi que, si nécessaire, les rapports quotidiens dans `reports/daily/`.
2. Dégage les tendances structurantes du mois : évolutions majeures, ruptures, sujets qui se sont installés dans la durée plutôt qu'être restés ponctuels.
3. Distingue clairement les faits établis des tendances encore incertaines ou des signaux faibles.
4. Vérifie via [`data/topic-index.csv`](../data/topic-index.csv) la fréquence et la durée de vie des sujets abordés sur le mois.
5. Rédige le bilan en suivant [`templates/monthly-report-template.md`](../templates/monthly-report-template.md).
6. Enregistre le rapport dans `reports/monthly/AAAA/AAAA-MM.md`.
7. Crée une branche `claude/bilan-mensuel-AAAA-MM` et prépare une Pull Request vers la branche principale, sans la fusionner.

## Rappels impératifs

- Applique les mêmes exigences de sourcing que pour la veille quotidienne (voir [`CLAUDE.md`](../CLAUDE.md)).
- Ne modifie ni ne supprime aucun rapport déjà publié.
