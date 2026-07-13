# Prompt — Synthèse hebdomadaire

## Contexte

Ce prompt sert de base pour produire la synthèse hebdomadaire, qui met en perspective les rapports quotidiens de la semaine écoulée.

## Instructions

1. Relis l'ensemble des rapports quotidiens publiés dans `reports/daily/` pour la semaine concernée.
2. Identifie les fils conducteurs : sujets récurrents, évolutions d'une actualité couverte en début de semaine, tendances qui se dégagent de plusieurs éléments distincts.
3. Ne reformule pas simplement chaque rapport quotidien : dégage une mise en perspective qui apporte une valeur ajoutée par rapport à la simple juxtaposition des jours.
4. Vérifie via [`data/topic-index.csv`](../data/topic-index.csv) qu'aucun sujet n'est présenté comme nouveau alors qu'il a déjà été traité dans un rapport hebdomadaire précédent.
5. Rédige la synthèse en suivant [`templates/weekly-report-template.md`](../templates/weekly-report-template.md).
6. Enregistre le rapport dans `reports/weekly/AAAA/AAAA-Www.md` (numéro de semaine ISO).
7. Crée une branche `claude/synthese-hebdo-AAAA-Www` et prépare une Pull Request vers la branche principale, sans la fusionner.

## Rappels impératifs

- Applique les mêmes exigences de sourcing que pour la veille quotidienne (voir [`CLAUDE.md`](../CLAUDE.md)).
- Ne modifie ni ne supprime aucun rapport déjà publié.
