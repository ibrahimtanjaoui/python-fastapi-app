# SECURITY NOTES – TP7



**Q3.** `@main` pointe vers la dernière version de la branche, qui change à chaque
commit : si le dépôt est compromis ou si un changement casse le workflow, notre
pipeline exécute ce nouveau code sans que nous l'ayons relu. `@v4` fixe une version
connue et stable, donc le comportement est reproductible. (Encore plus sûr : épingler
sur le SHA complet du commit, car un tag peut aussi être déplacé.)

**Q4.** Non. Le badge indique seulement que l'identité de l'organisation a été vérifiée
par GitHub, pas que le code est exempt de bugs ou de failles. Un compte légitime peut
être compromis, ou publier du code mal écrit. Il reste nécessaire de relire le code
et de limiter les permissions.

**Q5.** 
1. Lire le code source de l'action (action.yml, dist/ ou Dockerfile) pour vérifier
   qu'elle ne fait pas d'appels réseau suspects ni n'exfiltre de secrets.
2. Vérifier la réputation : mainteneur identifiable, nombre d'étoiles, activité
   récente, issues ouvertes, et épingler l'action sur un SHA de commit précis.