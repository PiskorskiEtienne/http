# Projet CI/CD ENSG
 Mise en place de l'intégration continue et du déploiement continu, sur le projet [http-server](https://github.com/http-party/http-server) pour nodejs.

 * Dépôt github : [https://github.com/PiskorskiEtienne/http](https://github.com/PiskorskiEtienne/http)

 * Système d'intégration continue utilisé : github action disponible sur [https://github.com/PiskorskiEtienne/http/actions](https://github.com/PiskorskiEtienne/http/actions)

 ### Etapes mise en place dans la chaîne d'intégration

 * Etape build qui, sur une machine ubuntu, installe les dépendances avec `npm install`. Ensuite démarre le serveur avec `npm start`, on attend 20 secondes que le serveur ait le temps de démarrer avec `sleep 20`, on test ensuite le serveur avec `curl http://localhost:8080`

 * Les test sont effectués avec `npm test`

 * L'étape build va également construire la documentation grâce à jsdoc [https://github.com/jsdoc/jsdoc](https://github.com/jsdoc/jsdoc)

 * L'étape deploy ne va s'effectuer que lorsque l'étape build sera validée. cette étape va mettre la documentation en ligne sur le site [https://piskorskietienne.github.io/http/](https://piskorskietienne.github.io/http/)

 * Les Etapes de build, run et test sont effectuées en parallèle sur les versions 8, 10 et 12 de nodejs


 ### Lors d'un pull request sur master

 Lorsqu'un utilisateur effectue un pull request la chaîne d'intégration est également appelée, si une des étapes n'est pas passé la pull request sera refusé, sinon la branche sera fusionnée automatiquement avec master.

Cette fonctionnalité n'apparaît pas sur le fichier yml de l'intégration, il apparaît en fait sur les paramètre du dépôt dans branches>branches protection. J'ai protégé la branche master pour que les pull requests ne soient acceptés quand les étapes de build sont validés.

le fichier d'intégration continue nodejs.yml pour github action se trouve dans `.github/workflows/nodejs.yml`
