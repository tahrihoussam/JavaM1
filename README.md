# JavaM1
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:xhtml="http://www.w3.org/1999/xhtml" xmlns:umlv="http://www.umlv.fr/2005/tipi" lang="fr" xml:lang="fr"><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>
  Java Avancé - Projet de Master 1
 </title><link rel="stylesheet" type="text/css" href="http://igm.univ-mlv.fr/ens/resources/stylesheet.css" media="screen"></link><link rel="stylesheet" type="text/css" href="http://igm.univ-mlv.fr/ens/resources/printstylesheet.css" media="print"></link><link rel="stylesheet" type="text/css" href="http://igm.univ-mlv.fr/ens/resources/sh_ide-eclipse.css"></link><SCRIPT type="text/javascript">
	      if(document.location.href.indexOf('http://igm/',0)!=-1){
	              document.location.href=document.location.href.replace(/.univ-mlv.fr/,'').replace(/http:\/\/(igm|www-igm)/,'http://igm.univ-mlv.fr');
		      }
	      if(document.location.href.indexOf('http://www-igm/',0)!=-1){
		                            document.location.href=document.location.href.replace(/.univ-mlv.fr/,'').replace(/http:\/\/(igm|www-igm)/,'http://igm.univ-mlv.fr');
					                          }
		function viewPDF(){
			window.print();
		}
			
		function myswitch(){
		if(document.location.href.indexOf('index')>-1){
			document.location.href= document.location.href.replace(/ens/,'ens/private').replace('http://','https://');
		}else{
		document.location.href= document.location.href.replace(/ens/,'ens/private').replace(/.php/,'_cor.php').replace('http://','https://');
		}	
		}
	</SCRIPT></head><body><div class="conteneur"><div class="contenu"><span style="float:right;" class="noprint"><div class="noprint"><table><tr><td><a href="javascript:myswitch();" style="text-decoration:none"><img src="http://igm.univ-mlv.fr/ens/resources/lock_icon.gif" class="noprint" align="middle"></img></a></td></tr></table></div></span><span style="text-align:left;"><a>::</a><a href="./../../../../index.php"> Enseignements </a>::<a href="./../../../index.php"> Master </a>::<a href="./../../index.php"> M1 </a>::<a href="./../index.php"> 2015-2016 </a>::<a href="./index.php"> Java Avancé </a>::</span><hr noshade size="1"></hr><table><tr><td valign="middle"><img class="print" src="http://igm.univ-mlv.fr/ens/resources/mlv.png" alt="[LOGO]"></img></td><td style="vertical-align : middle;"><h1>
  Java Avancé - Projet de Master 1
 </h1></td></tr></table><hr></hr>
 

 <h3 xmlns="">Exercice 1 - JShellBook - Interactive Java Book</h3>
  <div xmlns="">
   Le but de ce projet est d'implanter un système de livre interactif, dans le même principe
   que les <a href="https://ipython.org/notebook.html">ipython notebooks</a> capable :
   <ul>
    <li>
     de visualiser dans un browser Web des exercices écrit au format
     <a href="http://daringfireball.net/projects/markdown/">MarkDown</a>.
    </li>
<li>
     de permettre à un utilisateur de répondre aux questions d'un exercice dans le browser
     en écrivant du code Java avec une évaluation interactive en utilisant une interface simple AJAX/REST.
    </li>
   </ul>
  </div>
<br xmlns="">
  <div xmlns="">
   Le projet est composé de deux modules principaux, l'affichage d'un exercice et
   la gestion interactive de codes Java pour répondre à un exercice. 
  </div>
<br xmlns="">
  
  <ol xmlns="">
   <li>
    Configuration
   <br>
    Zéro configuration, on doit lancer l'executable sur un répertoire, celui-ci crée un serveur web sur le port 8989,
    et affiche dans le terminal une URL.
    On se connecte avec un browser à cette URL pour faire les exercices du répertoire.
   </li>
<li>
    Sécurité
   <br>
    IJavaBook ne propose pas par défaut de sécurité à part vérifier que le(s) browser(s) Web
    qui se connecte(nt) possède(nt) la même adresse IP que le serveur Web, c-a-d vérifier que le serveur et le browser
    web tournent sur la même machine.
   </li>
<li>
    Affichage d'un exercice
   <br>
    JShellBook permet d'afficher des exercices au format HTML des exercices écrit au format MarkDown.
   <br>
    La récupération des exercices doit être asynchrone et se faire en tâche de fond dans une ou plusieurs threads dediées,
    de telle sorte à ce que lorsqu'un exercice est modifié dans le répertoire, le ou les browsers affichant cette exercice
    se mettent automatiquement à jour (sans perdre les données déjà rentré par l'utilisateur dans la mesure du possible).
   </li>
<li>
    Stockage des exercices
   <br>
    JShellBook n'utilise pas de base de donnée relationelle/NoSQL pour stocker les exercices, ceux-ci reste stockés
    sur le disque au format MarkDown. Bien sûr, pour des questions de performance, une partie des exercices peuvent
    être stockées en mémoire tant que cela reste raisonnable (1 Giga n'est pas raisonnable).
   <br>
    Le programme doit donc avoir un algorithme spécifique permettant de garder en mémoire uniquement
    les exerices en cours.
   </li>
<li>
    Edition interactive
   <br>
    Un utilisateur doit pouvoir répondre aux questions directement au niveau de l'affichage d'une question
    d'un exercice. Pour cela, lorsque l'utilisateur écrit une ligne de code Java,
    le code est envoyé au serveur, évalué par JShell, et le résultat est retourné et affiché dans le browser.
   <br>
    De plus, il doit être possible de spécifier du code de test (tests unitaires) qui ne seront visible que
    si l'utilisateur demande explicitement à voir ces tests. Le format des tests unitaires, JUnit ou autre,
    est laissé à votre convenance mais ceux-ci doivent être embarquable directement dans le fichier d'exercice
    et aussi spécifiable sous forme d'un fichier source (donc pas compilé) séparé.
   <br>
    Cette partie est extrèmement importante et l'ergonomie doit être la plus simple possible pour l'utilisateur
    et la partie affichage doit être répondre le plus rapidement possible.
   </li>
  </ol>
  
  <div xmlns="">
   L'affichage se fait dans un browser Web sous forme d'une page unique par exercice.
   Les données sont exportées par le serveur sous forme de services Web respectant la technologie REST
   et affichées par le browser en utilisant des requêtes JavaScript asynchrone (AJAX) émises par une bibliothèque JavaScript.
   La page correspondant à un exercice est générée par le serveur une unique fois et
   modifiée dynamiquement par le browser en JavaScript.
  <br>
   Pour la partie JavasScript (affichage et requête) vous être libre d'utiliser la/les librairies JavaScript que vous voulez,
   <a href="http://getbootstrap.com/javascript/">bootstrap</a>,
   <a href="http://jquery.com/">jquery</a>,
   <a href="http://backbonejs.org/">backbonejs</a>,
   <a href="http://facebook.github.io/react/">react</a> 
   ou <a href="https://angularjs.org/">angularjs</a>.
  <br>
   Le serveur Web est imposé, il s'agit de <a href="http://vertx.io/">vertx</a> dans sa version 3.0.
   Un petit exemple jouant le rôle de <a href="src/project/jshellbook.zip">prototype</a> est disponible.
  <br>
   Attention, ce n'est qu'un prototype qui ne montre en rien comment vous devez concevoir
   l'architecture de votre programme.
  <br>
   Pour gérer l'affichage en HTML de vos fichiers MarkDown, vous utiliser la librairie
   <a href="https://github.com/sirthias/parboiled/wiki">Parboiled</a>.
  <br>
   Pour surveiller les modifications d'un répertoire, vous pouvez utiiser la classe
   <a href="https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html">WatchService</a>.
  <br>
   Pour exécuter les snippets de code Java vous utiliserez l'API JShell présente dans le JDK 9.
   Il n'est pas nécessaire que votre projet compile avec Java 9, Java 8 avec la bibliothèque jdk.jshell.jar
   est suffisant. Mais par contre, il devra s'exécuter avec le
   <a href="http://www-igm.univ-mlv.fr/~forax/tmp/jdk9b90/">jdk9b90</a> (oui, celui-là pas un autre).
  <br>
   Sur les machine de l'université, cette version est installée dans le répertoire <tt>/usr/local/apps/jdk9/</tt>.
  </div>
<br xmlns="">
  <div xmlns="">
   Le projet (un seul fichier par binôme) doit être déposé par le binome
   dont le nom est le premier dans l'ordre alphabétique sur la plateforme
   <a href="https://elearning.u-pem.fr/mod/assign/view.php?id=15888">elearning</a>
   avant le 31 décembre à 23h55.
  <br>
   Le livrable est un fichier au format ZIP (avec un encodage en UTF8 si vous utilisez Windows ou MacOS)
   et devra contenir dans un répertoire principal à vos deux noms
   <ul>
    <li>
     un répertoire <tt>src</tt> contenant les sources du projet et les éventuelles ressources à recopier à côté des classes;
    </li>
<li>
     un répertoire <tt>docs</tt> contenant le manuel de l'utilisateur (user.pdf) et
     le rapport qui explique votre architecture (dev.pdf) au format PDF;
    </li>
<li>
     un répertoire <tt>classes</tt> vide dans l'archive et qui contiendra les classes une fois compilées
    </li>
<li>
     un répertoire <tt>libs</tt> qui contiendra le ou les jars nécéessaire pour Parboiled et JShell.
    </li>
<li>
     un jar exécutable nommé <tt>jshellbook.jar</tt> qui fonctionne avec java -jar jshellbook.jar et
     donc qui possède un fichier manifest adéquat;
    </li>
<li>
     un build.xml (écrit à la main, pas illisible car généré par un outil) qui permet de
     <ul>
      <li>compiler les sources (target compile)</li>
      <li>créer le jar exécutable (target jar)</li>
      <li>générer la javadoc dans <tt>docs/api</tt> (target javadoc)</li>
      <li>nettoyer le projet pour qu'il ne reste plus que les éléments demandés (target clean)</li>
      <li>les répertoires <tt>vertx</tt> et <tt>webroot</tt>.</li>
     </ul>
    </li>
   </ul>
  </div>
<br xmlns="">
  <div xmlns="">
   Ce projet est évalué par les enseignants de Java Avancé et Design Pattern,
   et donnera donc lieu à 2 notes différentes qui seront chacune intégrée de le calcul
   de la moyenne de la matière concernée.
  <br>
   Voici les critères d'évaluation :
  </div>
<br xmlns="">
  <ul xmlns="">
   <li>
    Design Pattern
   <br>
    Le programme doit être architecturé en utilisant les principes de la POO
    et utilisant quand cela est nécessaire les design patterns (vu ou non en cours).
   <br>
    Il vous est demandé de fournir un rapport de design (<tt>dev.pdf</tt>) indiquant comment vous
    avez architecturé votre pogramme avec des diagrammes de classes UML ainsi
    que la responsabilité de chaque classe. Mais aussi pourquoi vous avez
    architecturé votre programme de cette façon plutôt que d'une autre et
    ce pour chaque décision de design que vous avez prise.
   <br>
    Pour chaque classe mutable, il vous faut justifier pourquoi cette classe est mutable.
   <br>
    Il vous est de plus demandé une javadoc complète pour toute les méthodes publiques, écrite en anglais
    (il vous sera retiré 2 points pour chaque manquement).
   </li>
<li>
    Concurrence
   <br>
    Le programme doit être permettre à plusieurs clients WEB (browsers) de se connecter
    en même temps, dans ce cas, le réponses aux questions sont spécifiques à un client.
    La mise à jour des exercices doit se faire de façon asynchrone et treadsafe
    indépendamment du fait qu'un client fasse ou non une requête.
   <br>
    Le code doit clairement séparer la gestions des threads du reste du programme,
    utiliser les principes de la programmation objet pour encapsuler la gestion
    de la concurrence en utilisant les principes et techniques vus en cours.
   <br>
    La présence de classes qui devraient être thread safe mais qui permettent une utilisation
    non-thread safe de ses méthodes sera sévèrement sanctionnée.
   </li>
<li>
    Java Avancé
   <br>
    Le programme doit être écrit en utilisant correctement les différents concepts
    vus lors du cours de Java Avancé (sous-typage, polymorphisme, lambda, classes internes,
    exceptions, types paramétrés, collections, entrées/sorties et reflection).
   <br>
    Pour vous aider, si vous ne respectez pas les indications de "mort imminente" suivantes,
    il vous sera retiré la moitié des points (10 points, puis 5 points, puis 2 points, puis 1 points)
    pour chaque non respect des indications.
    <ul>
     <li>
       Il ne doit pas y avoir de warnings lorsque l'on passe findbugs.
     </li>
<li>
       Il ne doit pas y avoir de warnings lorsque l'on charge le code dans Eclipse.
     </li>
<li>
       Il ne doit pas y avoir de warnings lorsque l'on compile avec javac.
     </li>
<li>
      Il ne doit pas y avoir de raw types, de @SuppressWarning non justifié, de cast non justifié.
     </li>
<li>
      Il ne doit pas y avoir d'instanceof/switch/if...else sur des types là où il est possible
      d'utiliser le polymorphisme.
     </li>
<li>
      Chaque interface devra être nécessaire.
     </li>
<li>
      Chaque classe abstraite doit être non publique et pas utilisé comme un type.
     </li>
<li>
      Chaque méthode devra être appelée (pas de code mort).
     </li>
<li>
      Chaque méthode ne doit pas faire plus de 8 lignes sans une vraie justification.
     </li>
<li>
      Il est interdit d'utiliser des champs static typés par un objet (pas de globale),
      seule les constantes (static final) de type primitif sont autorisées.
     </li>
    </ul>
   </li>
  </ul>
 
<hr noshade size="1"></hr><span style="float:right;" class="noprint"><div class="noprint"></div></span><div align="center" class="copyright">© Université de Marne-la-Vallée</div></div></div></body></html>
