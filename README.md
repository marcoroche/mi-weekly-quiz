# mi-weekly-quiz

Weekly quiz for MindInvest users.

## Principe

Chaque **dimanche**, un nouveau quiz narratif est publié au format JSON.
Il est **visible par les utilisateurs de l'app MindInvest dès le lundi**
(en réalité dès quelques secondes après le commit).

Le weekly quiz se différencie du quiz intégré de l'app (≈ 5 000 questions
statiques, difficulté 1–5) par :

- un **thème narratif hebdomadaire** (les questions forment une histoire) ;
- une **difficulté croissante** au fil du quiz (1 → 5) ;
- des **types de questions variés** : MCQ, TRUE_FALSE, NUMERIC_GUESS, BONUS ;
- un **score et des rangs** partageables ;
- un fil **actualité des marchés** possible chaque semaine.

## URL de lecture pour l'app MindInvest

```
https://raw.githubusercontent.com/marcoroche/mi-weekly-quiz/main/quizzes/current.json
```

L'app lit toujours cette URL fixe : `quizzes/current.json` est mis à jour
à chaque nouvelle semaine.

## Structure du repo

- `quizzes/current.json` — quiz de la semaine (URL fixe lue par l'app)
- `quizzes/<ANNEE>/W<SEMAINE>.json` — archives des semaines passées

## Format (schemaVersion 2)

- `id` : identifiant unique du quiz (`wq_<année>_W<semaine>`)
- `validFrom` / `validUntil` : fenêtre de visibilité (lundi → dimanche)
- `narrative` : intro racontée, traduite fr/en
- `questions[]` : `difficulty` (1–5), `type` (MCQ | TRUE_FALSE | NUMERIC_GUESS | BONUS),
  `points`, `translations` (fr/en) avec `options[] {id, text, isCorrect}`
- Pour `NUMERIC_GUESS` : `answer` (nombre) + `tolerance`, le plus proche gagne
- `scoring.rankLabels` : rangs selon le score obtenu

## Processus hebdomadaire

1. Dimanche : publication de `quizzes/current.json` + archive `quizzes/<ANNEE>/W<SS>.json`
2. Lundi : le quiz est visible dans l'app MindInvest
3. La semaine suivante : nouveau thème, l'ancien quiz reste en archive
