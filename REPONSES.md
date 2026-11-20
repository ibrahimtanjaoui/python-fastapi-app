TP6 – Réponses

1/ Le runner lit le fichier GITHUB_ENV seulement une fois la step terminée, puis
injecte les variables dans les steps suivantes. La step qui écrit a déjà démarré avec
son environnement figé, donc elle ne voit pas la variable.

2/ `$APP_NAME` s'affiche vide dans verify-env. Chaque job tourne sur un runner
distinct (une VM neuve) : la portée de GITHUB_ENV est limitée au job courant.

3/ `>` écrase le fichier au lieu d'ajouter à la fin : seul le dernier output écrit
survit, le premier est perdu. Il faut utiliser `>>`.

4/ GITHUB_ENV ne vit que dans un job (une VM). GITHUB_OUTPUT, couplé à `outputs:`
au niveau du job et à `needs`, est transmis par GitHub aux autres jobs.

5/ Sans `needs: build`, deploy démarre en parallèle (pas d'ordre garanti) et
`needs.build.outputs.full_version` est vide, car deploy n'a pas de dépendance déclarée
sur build.