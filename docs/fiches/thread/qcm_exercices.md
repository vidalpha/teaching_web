Les QCM et les exercices sont à rendre suivant la programmation sur Webcampus et sont indispensables pour la suite des TP.

## QCM

Cliquez sur [#QCM](){:target="_blank"} pour accéder au questionnaire. Vous aurez besoin de vous connectez à Webcampus.

## Exercices

### 1- Vérou Mutex

Implémentez une classe qui joue le rôle d’un verrou mutex en Java. Vous aurez certainement besoin d’utiliser des méthodes synchronized, ainsi que les méthodes wait(), notify() et notifyAll().


### 2- Salle d'attente virtuelle

Écrire un programme multithread qui gère l'accès à un site web en limitant le nombre de connexions simultanées. Le programme doit permettre aux utilisateurs d'accéder à la plateforme tout en respectant les règles suivantes :

- Limiter le nombre maximal de connexions simultanées, ce nombre étant paramétrable. Si ce nombre est atteint, les nouveaux utilisateurs qui tentent d'accéder à la plateforme sont mis en attente dans une file d'attente *FIFO (First-In-First-Out)*.

- Si la file d'attente atteint sa capacité maximale, les requêtes des utilisateurs supplémentaires seront déboutées avec un retour timeout.

- Chaque utilisateur qui a accès à la plateforme dispose d'un temps maximal de navigation, défini de manière aléatoire. Si un utilisateur se déconnecte avant la fin de ce temps, la ressource est libérée, permettant au prochain utilisateur dans la file d'accéder à la plateforme.

- Les utilisateurs en attente sont informés du nombre de personnes dans la file d'attente et reçoivent une estimation du nombre de minutes avant leur accès. Cette information doit être mise à jour en temps réel.

Pour implémenter cela, vous devrez utiliser des mécanismes de synchronisation tels que des threads, des mutex (ou sémaphores) pour gérer l'accès concurrentiel aux ressources partagées, et un mécanisme de file d'attente pour organiser l'ordre d'arrivée des utilisateurs en attente. De plus, vous devrez générer des temps aléatoires pour le temps maximal de navigation de chaque utilisateur.