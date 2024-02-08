# Structure d'un projet Spring boot

Intellij IDEA - Spring boot 5

``` bash
.
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── monprojet
│   │   │           ├── config/
│   │   │           ├── controllers/
│   │   │           ├── models/
│   │   │           ├── repositories/
│   │   │           ├── services/
│   │   │           └── Application.java
│   │   └── resources
│   │       ├── application.properties
│   │       └── static/
│   └── test
│       ├── java
│       │   └── com
│       │       └── monprojet
│       │           └── ApplicationTests.java
│       └── resources/
│
└── pom.xml
```

Le dossier <span class="span-hightlight">resources</span> contient les ressources de l'application. Il contient généralement les fichiers suivants :

- <span class="span-hightlight">Application.java</span> : contient le point d'entrée de l'application. Il est utilisé pour démarrer l'application et configurer son environnement.
- <span class="span-hightlight">application.properties</span> : fichier de configuration de l'application. Le fichier des propriétes peut être aussi un fichier *.yml*
- <span class="span-hightlight">static</span> : dossier contenant les ressources statiques de l'application, telles que les images, les CSS et le JavaScript.
- <span class="span-hightlight">pom.xml</span> : Fichier de dépendances Maven

Les dossiers suivants peuvent être ajoutés pour structurer le projet:

- <span class="span-hightlight">controllers</span>: Les classes représentant les contrôleurs traitent les requêtes HTTP de l'utilisateur. Elles sont utilisées pour afficher les données à l'utilisateur et pour traiter les actions de l'utilisateur. Elles contiennent peu de règles métiers et sollicitent les services pour les règles métiers

- <span class="span-hightlight">services</span>: Les classes représentant les services fournissent des fonctionnalités métier à l'application. Elles sont utilisées pour abstraire la logique métier de l'application.

- <span class="span-hightlight">models</span>: Les classes repréentants les entités: POJO simple avec une collection de propriétés qui peuvent ou non être utilisées par la vue

- <span class="span-hightlight">repositories</span>:

- <span class="span-hightlight">config</span>:

