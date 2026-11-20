# TP7 – Réponses

**Q1.** actions/checkout a des valeurs par défaut pour tous ses paramètres (dépôt
courant, ref qui a déclenché le workflow, token automatique), donc `with` est
optionnel. setup-node doit savoir quelle version de Node installer : sans
`node-version`, on obtient la version préinstallée sur le runner, non contrôlée.

**Q2.** Chaque job s'exécute sur un runner distinct (VM neuve), et le dépôt n'y est
pas partagé en direct. De plus, report.txt est généré pendant l'exécution du job build
et n'est jamais commité : il n'existe que sur le runner de build. Un artefact permet
de transférer ce fichier d'un job à l'autre.

**Q6.** Le runner démarre sur une machine vide. L'action locale est un dossier du
dépôt (`./.github/actions/build-info`) : tant que checkout n'a pas récupéré le code,
ce dossier n'existe pas et GitHub ne trouve pas action.yml.

**Q7.** Dans une action composite, les steps `run` n'héritent d'aucun shell par
défaut (contrairement à un workflow classique). Il faut le préciser explicitement
avec `shell: bash`, sinon GitHub signale une erreur de validation.

**Partie 4 (comparaison).** Action composite : ~0s. Action Docker : ~XXs, car l'image
est construite à chaque exécution. (Remplacez par vos durées réelles.)