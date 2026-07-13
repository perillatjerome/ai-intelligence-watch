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
├── reports/
│   ├── daily/2026/                  # Rapports quotidiens
│   ├── weekly/2026/                 # Synthèses hebdomadaires
│   └── monthly/2026/                # Bilans mensuels
├── scripts/
│   └── generate_daily_report.py     # Script d'automatisation (appelé par le workflow)
├── requirements.txt                  # Dépendances Python du script d'automatisation
└── .github/workflows/
    └── daily-ai-watch.yml           # Workflow GitHub Actions (exécution quotidienne)
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

## Automatisation quotidienne (GitHub Actions)

En plus de l'exécution manuelle via Claude Code, le projet peut générer son rapport quotidien **tout seul, chaque jour**, grâce à un workflow GitHub Actions qui appelle l'API OpenAI. Cette section explique, pas à pas et sans prérequis technique, comment cette automatisation fonctionne et comment la configurer.

### Comment fonctionne l'automatisation

- Le fichier [`.github/workflows/daily-ai-watch.yml`](.github/workflows/daily-ai-watch.yml) s'exécute automatiquement **chaque jour vers 08:15, heure de Paris**, et peut aussi être lancé manuellement à tout moment.
- Il exécute le script [`scripts/generate_daily_report.py`](scripts/generate_daily_report.py), qui, dans l'ordre :
  1. vérifie qu'aucun rapport n'existe déjà pour la date du jour (si oui, il s'arrête sans rien casser) ;
  2. lit `CLAUDE.md`, `methodology/`, `templates/daily-report-template.md`, `prompts/daily-watch.md` et les index de `data/` pour connaître les règles du projet et les sujets déjà traités ;
  3. interroge un modèle **OpenAI**, avec sa fonction de **recherche web**, pour proposer jusqu'à 5 actualités IA et 5 découvertes scientifiques assistées par IA, sourcées et datées ;
  4. écarte automatiquement les éléments dont l'URL est déjà présente dans `data/news-index.csv` (anti-doublon) ;
  5. écrit `reports/daily/AAAA/AAAA-MM-JJ.md` et met à jour `data/news-index.csv`, `data/topic-index.csv` et `data/source-register.csv`.
- Le workflow crée ensuite une branche `claude/veille-ia-AAAA-MM-JJ`, y committe les fichiers générés, la pousse sur GitHub, puis ouvre une Pull Request vers `main`.
- **Comme pour un rapport généré manuellement, cette Pull Request n'est jamais fusionnée automatiquement.** Un humain doit la relire et cliquer sur « Merge ».
- Un mini test intégré (`--self-test`) s'exécute avant chaque appel à l'API OpenAI, pour vérifier que le script lui-même fonctionne correctement (sans consommer de quota) avant de dépenser un appel API.

### Où ajouter la clé API OpenAI dans GitHub

L'automatisation a besoin d'une clé API OpenAI, stockée sous forme de **secret GitHub** nommé `OPENAI_API_KEY` (jamais écrite en clair dans le code).

1. Ouvrez le dépôt sur **github.com**.
2. Cliquez sur l'onglet **Settings** (Paramètres), tout en haut du dépôt.
3. Dans le menu de gauche, cliquez sur **Secrets and variables**, puis sur **Actions**.
4. Restez sur l'onglet **Secrets**, puis cliquez sur le bouton vert **New repository secret**.
5. Dans **Name**, saisissez exactement : `OPENAI_API_KEY`.
6. Dans **Secret**, collez votre clé API OpenAI (elle commence par `sk-...`).
7. Cliquez sur **Add secret**.

Optionnel : dans le même écran, onglet **Variables** (à côté de *Secrets*), vous pouvez ajouter une variable nommée `OPENAI_MODEL` si vous voulez utiliser un autre modèle que celui par défaut (`gpt-4.1`) — sans avoir à modifier le workflow.

### Lancer le workflow manuellement

1. Ouvrez l'onglet **Actions** du dépôt sur GitHub.
2. Dans la liste de gauche, cliquez sur **Veille IA quotidienne**.
3. Cliquez sur le bouton **Run workflow** (en haut à droite de la liste des exécutions).
4. Laissez la branche proposée (`main`) telle quelle, puis cliquez sur le bouton vert **Run workflow**.
5. Une nouvelle exécution apparaît en haut de la liste après quelques secondes.

### Vérifier si l'exécution a réussi

1. Dans l'onglet **Actions**, cliquez sur l'exécution la plus récente de **Veille IA quotidienne**.
2. Une coche verte ✅ à côté du nom signifie que tout s'est bien passé ; une croix rouge ❌ signifie qu'une étape a échoué.
3. En haut de la page de l'exécution, un résumé en langage clair (« Résultat du workflow « Veille IA quotidienne » ») indique si un nouveau rapport a été généré, s'il n'y avait rien à faire aujourd'hui, ou où regarder en cas d'échec.
4. En cas de croix rouge, cliquez sur l'étape concernée (par exemple « Générer le rapport quotidien ») pour lire le message d'erreur détaillé — il est rédigé pour être compréhensible sans connaissances techniques.

### Relire et fusionner la Pull Request générée

1. Ouvrez l'onglet **Pull requests** du dépôt.
2. Ouvrez la Pull Request intitulée **« Veille IA quotidienne — AAAA-MM-JJ »**.
3. Relisez le rapport généré (fichier `reports/daily/AAAA/AAAA-MM-JJ.md` listé dans l'onglet **Files changed**) : vérifiez que les sources citées existent réellement et disent bien ce que le rapport leur attribue, que le ton est correct, et complétez si vous le souhaitez la section « Regard critique personnel à compléter ».
4. Si tout est correct, cliquez sur **Merge pull request** puis **Confirm merge** pour publier le rapport. Si quelque chose ne va pas, laissez un commentaire ou fermez la Pull Request (**Close pull request**) sans la fusionner.

### En cas de problème

- **« La variable d'environnement OPENAI_API_KEY est absente »** : le secret n'a pas été créé, ou son nom est mal orthographié — revoir la section ci-dessus.
- **Erreur lors de l'appel à l'API OpenAI** : vérifiez que la clé API est valide, que le compte OpenAI associé dispose de crédit/quota disponible, et que le modèle configuré (variable `OPENAI_MODEL`) est bien accessible à ce compte.
- **Le workflow réussit (✅) mais n'ouvre aucune Pull Request** : c'est normal si un rapport existe déjà pour la date du jour. Si aucune actualité ou découverte suffisamment fiable n'a été trouvée, le workflow échoue explicitement (❌) plutôt que de publier un rapport vide ou de faible qualité — voir les logs de l'étape de génération pour le détail.
- **Aucune exécution ne s'est lancée à 08:15 pile** : les tâches planifiées (`schedule`) de GitHub Actions peuvent être retardées de quelques minutes selon la charge de la plateforme ; ce n'est pas une anomalie du projet. Il est toujours possible de lancer le workflow manuellement en attendant.

## Limites de l'automatisation

- La qualité de la veille dépend de la disponibilité et de la fiabilité des sources accessibles au moment de la rédaction.
- La détection de doublons repose sur les index de `data/` : une lacune dans leur mise à jour peut entraîner un doublon non détecté.
- L'automatisation réduit le risque d'erreur mais ne garantit pas l'exactitude absolue ; c'est pourquoi la validation humaine reste une étape obligatoire avant toute publication.
- Le système ne couvre que les sources et langues auxquelles Claude Code a accès au moment de la recherche.
- Le workflow GitHub Actions quotidien (`daily-ai-watch.yml`) dépend de la disponibilité et de la qualité de la recherche web du modèle OpenAI configuré ; ses résultats sont soumis exactement aux mêmes exigences de sourcing et de relecture humaine que les rapports générés manuellement.

## Derniers rapports disponibles

- [Rapports quotidiens](reports/daily/2026/)
- [Synthèses hebdomadaires](reports/weekly/2026/)
- [Bilans mensuels](reports/monthly/2026/)

Aucun rapport n'a encore été publié : ces dossiers seront alimentés au fil des prochaines Pull Requests fusionnées.
