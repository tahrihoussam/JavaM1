 Java Avancé - Projet de Master 1
Exercice 1 - JShellBook - Interactive Java Book
Le but de ce projet est d'implanter un système de livre interactif, dans le même principe que les ipython notebooks capable :

    de visualiser dans un browser Web des exercices écrit au format MarkDown.
    de permettre à un utilisateur de répondre aux questions d'un exercice dans le browser en écrivant du code Java avec une évaluation interactive en utilisant une interface simple AJAX/REST.


Le projet est composé de deux modules principaux, l'affichage d'un exercice et la gestion interactive de codes Java pour répondre à un exercice.

    Configuration
    Zéro configuration, on doit lancer l'executable sur un répertoire, celui-ci crée un serveur web sur le port 8989, et affiche dans le terminal une URL. On se connecte avec un browser à cette URL pour faire les exercices du répertoire.
    Sécurité
    IJavaBook ne propose pas par défaut de sécurité à part vérifier que le(s) browser(s) Web qui se connecte(nt) possède(nt) la même adresse IP que le serveur Web, c-a-d vérifier que le serveur et le browser web tournent sur la même machine.
    Affichage d'un exercice
    JShellBook permet d'afficher des exercices au format HTML des exercices écrit au format MarkDown.
    La récupération des exercices doit être asynchrone et se faire en tâche de fond dans une ou plusieurs threads dediées, de telle sorte à ce que lorsqu'un exercice est modifié dans le répertoire, le ou les browsers affichant cette exercice se mettent automatiquement à jour (sans perdre les données déjà rentré par l'utilisateur dans la mesure du possible).
    Stockage des exercices
    JShellBook n'utilise pas de base de donnée relationelle/NoSQL pour stocker les exercices, ceux-ci reste stockés sur le disque au format MarkDown. Bien sûr, pour des questions de performance, une partie des exercices peuvent être stockées en mémoire tant que cela reste raisonnable (1 Giga n'est pas raisonnable).
    Le programme doit donc avoir un algorithme spécifique permettant de garder en mémoire uniquement les exerices en cours.
    Edition interactive
    Un utilisateur doit pouvoir répondre aux questions directement au niveau de l'affichage d'une question d'un exercice. Pour cela, lorsque l'utilisateur écrit une ligne de code Java, le code est envoyé au serveur, évalué par JShell, et le résultat est retourné et affiché dans le browser.
    De plus, il doit être possible de spécifier du code de test (tests unitaires) qui ne seront visible que si l'utilisateur demande explicitement à voir ces tests. Le format des tests unitaires, JUnit ou autre, est laissé à votre convenance mais ceux-ci doivent être embarquable directement dans le fichier d'exercice et aussi spécifiable sous forme d'un fichier source (donc pas compilé) séparé.
    Cette partie est extrèmement importante et l'ergonomie doit être la plus simple possible pour l'utilisateur et la partie affichage doit être répondre le plus rapidement possible.

L'affichage se fait dans un browser Web sous forme d'une page unique par exercice. Les données sont exportées par le serveur sous forme de services Web respectant la technologie REST et affichées par le browser en utilisant des requêtes JavaScript asynchrone (AJAX) émises par une bibliothèque JavaScript. La page correspondant à un exercice est générée par le serveur une unique fois et modifiée dynamiquement par le browser en JavaScript.
Pour la partie JavasScript (affichage et requête) vous être libre d'utiliser la/les librairies JavaScript que vous voulez, bootstrap, jquery, backbonejs, react ou angularjs.
Le serveur Web est imposé, il s'agit de vertx dans sa version 3.0. Un petit exemple jouant le rôle de prototype est disponible.
Attention, ce n'est qu'un prototype qui ne montre en rien comment vous devez concevoir l'architecture de votre programme.
Pour gérer l'affichage en HTML de vos fichiers MarkDown, vous utiliser la librairie Parboiled.
Pour surveiller les modifications d'un répertoire, vous pouvez utiiser la classe WatchService.
Pour exécuter les snippets de code Java vous utiliserez l'API JShell présente dans le JDK 9. Il n'est pas nécessaire que votre projet compile avec Java 9, Java 8 avec la bibliothèque jdk.jshell.jar est suffisant. Mais par contre, il devra s'exécuter avec le jdk9b90 (oui, celui-là pas un autre).
Sur les machine de l'université, cette version est installée dans le répertoire /usr/local/apps/jdk9/.

Le projet (un seul fichier par binôme) doit être déposé par le binome dont le nom est le premier dans l'ordre alphabétique sur la plateforme elearning avant le 31 décembre à 23h55.
Le livrable est un fichier au format ZIP (avec un encodage en UTF8 si vous utilisez Windows ou MacOS) et devra contenir dans un répertoire principal à vos deux noms

    un répertoire src contenant les sources du projet et les éventuelles ressources à recopier à côté des classes;
    un répertoire docs contenant le manuel de l'utilisateur (user.pdf) et le rapport qui explique votre architecture (dev.pdf) au format PDF;
    un répertoire classes vide dans l'archive et qui contiendra les classes une fois compilées
    un répertoire libs qui contiendra le ou les jars nécéessaire pour Parboiled et JShell.
    un jar exécutable nommé jshellbook.jar qui fonctionne avec java -jar jshellbook.jar et donc qui possède un fichier manifest adéquat;
    un build.xml (écrit à la main, pas illisible car généré par un outil) qui permet de
        compiler les sources (target compile)
        créer le jar exécutable (target jar)
        générer la javadoc dans docs/api (target javadoc)
        nettoyer le projet pour qu'il ne reste plus que les éléments demandés (target clean)
        les répertoires vertx et webroot.


Ce projet est évalué par les enseignants de Java Avancé et Design Pattern, et donnera donc lieu à 2 notes différentes qui seront chacune intégrée de le calcul de la moyenne de la matière concernée.
Voici les critères d'évaluation :

    Design Pattern
    Le programme doit être architecturé en utilisant les principes de la POO et utilisant quand cela est nécessaire les design patterns (vu ou non en cours).
    Il vous est demandé de fournir un rapport de design (dev.pdf) indiquant comment vous avez architecturé votre pogramme avec des diagrammes de classes UML ainsi que la responsabilité de chaque classe. Mais aussi pourquoi vous avez architecturé votre programme de cette façon plutôt que d'une autre et ce pour chaque décision de design que vous avez prise.
    Pour chaque classe mutable, il vous faut justifier pourquoi cette classe est mutable.
    Il vous est de plus demandé une javadoc complète pour toute les méthodes publiques, écrite en anglais (il vous sera retiré 2 points pour chaque manquement).
    Concurrence
    Le programme doit être permettre à plusieurs clients WEB (browsers) de se connecter en même temps, dans ce cas, le réponses aux questions sont spécifiques à un client. La mise à jour des exercices doit se faire de façon asynchrone et treadsafe indépendamment du fait qu'un client fasse ou non une requête.
    Le code doit clairement séparer la gestions des threads du reste du programme, utiliser les principes de la programmation objet pour encapsuler la gestion de la concurrence en utilisant les principes et techniques vus en cours.
    La présence de classes qui devraient être thread safe mais qui permettent une utilisation non-thread safe de ses méthodes sera sévèrement sanctionnée.
    Java Avancé
    Le programme doit être écrit en utilisant correctement les différents concepts vus lors du cours de Java Avancé (sous-typage, polymorphisme, lambda, classes internes, exceptions, types paramétrés, collections, entrées/sorties et reflection).
    Pour vous aider, si vous ne respectez pas les indications de "mort imminente" suivantes, il vous sera retiré la moitié des points (10 points, puis 5 points, puis 2 points, puis 1 points) pour chaque non respect des indications.
        Il ne doit pas y avoir de warnings lorsque l'on passe findbugs.
        Il ne doit pas y avoir de warnings lorsque l'on charge le code dans Eclipse.
        Il ne doit pas y avoir de warnings lorsque l'on compile avec javac.
        Il ne doit pas y avoir de raw types, de @SuppressWarning non justifié, de cast non justifié.
        Il ne doit pas y avoir d'instanceof/switch/if...else sur des types là où il est possible d'utiliser le polymorphisme.
        Chaque interface devra être nécessaire.
        Chaque classe abstraite doit être non publique et pas utilisé comme un type.
        Chaque méthode devra être appelée (pas de code mort).
        Chaque méthode ne doit pas faire plus de 8 lignes sans une vraie justification.
        Il est interdit d'utiliser des champs static typés par un objet (pas de globale), seule les constantes (static final) de type primitif sont autorisées.
