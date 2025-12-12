<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Le SDK Java (Software Development Kit)</h1>
                <p class="lesson-meta text-white">Comprendre et maîtriser l'environnement de développement Java</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction au SDK Java</h2>
                <p class="textExemple">
                    Le SDK Java (Software Development Kit) est l'ensemble complet d'outils nécessaires 
                    pour développer, compiler, déboguer et exécuter des applications Java. 
                    C'est le kit de développement officiel fourni par Oracle et la communauté OpenJDK.
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Composition du SDK Java</span>
JDK = JRE + Outils de développement + Bibliothèques de développement</code></pre>
                </div>
            </div>

            <!-- Architecture du SDK -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture du SDK Java</h2>
                
                <h3 class="text-purple">Les trois composants fondamentaux</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">1. JDK (Java Development Kit)</h4>
                        <pre v-pre><code class="language-text">• Pour les développeurs
• Contient le JRE
• Outils de développement
• Compilateur (javac)
• Debugger (jdb)
• Documentation (javadoc)
• Bibliothèques de dev</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">2. JRE (Java Runtime Environment)</h4>
                        <pre v-pre><code class="language-text">• Pour exécuter des apps
• Contient la JVM
• Bibliothèques d'exécution
• Plugins Java
• Configuration
• Ne contient pas javac
• Pour les utilisateurs finaux</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">3. JVM (Java Virtual Machine)</h4>
                    <pre v-pre><code class="language-text">• Exécute le bytecode
• Gestion de la mémoire
• Garbage Collector
• JIT Compiler
• Gestion des threads
• Sécurité
• Multiplateforme</code></pre>
                </div>

                <h3 class="text-purple">Relation entre les composants</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">    +-----------------------+
    |      JDK              |
    |  +-----------------+  |
    |  |      JRE        |  |
    |  |  +-----------+  |  |
    |  |  |    JVM    |  |  |
    |  |  +-----------+  |  |
    |  +-----------------+  |
    |  +-----------------+  |
    |  | Outils de dev   |  |
    |  +-----------------+  |
    +-----------------------+</code></pre>
                </div>
            </div>

            <!-- Installation du SDK -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation du SDK Java</h2>

                <h3 class="text-purple">Choix de la distribution</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Oracle JDK</h4>
                        <pre v-pre><code class="language-text">• Distribution officielle
• Licence commerciale
• Support d'Oracle
• Performances optimisées
• Pour production
• Mises à jour régulières</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">OpenJDK</h4>
                        <pre v-pre><code class="language-text">• Open source (GPL)
• Communauté
• Multiple fournisseurs
• Gratuit
• Compatible Oracle JDK
• Builds communautaires</code></pre>
                    </div>
                </div>

                <h3 class="text-purple">Fournisseurs OpenJDK populaires</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Principaux fournisseurs JDK</span>
- <span class="bash-keyword">Adoptium (Eclipse Temurin)</span> : Recommandé, support long terme
- <span class="bash-keyword">Amazon Corretto</span> : Amazon, support long terme
- <span class="bash-keyword">Microsoft Build</span> : Microsoft, optimisé Windows
- <span class="bash-keyword">Azul Zulu</span> : Azul Systems, multiplateforme
- <span class="bash-keyword">Red Hat OpenJDK</span> : Pour RHEL/CentOS
- <span class="bash-keyword">SapMachine</span> : SAP, pour applications d'entreprise</code></pre>
                </div>
            </div>

            <!-- Structure des répertoires du SDK -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure des répertoires du SDK</h2>

                <h3 class="text-purple">Arborescence standard après installation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">jdk-21/                      # Racine du JDK
├── bin/                     # Exécutables (javac, java, jar, etc.)
│   ├── javac               # Compilateur Java
│   ├── java                # Lanceur d'applications
│   ├── javadoc             # Générateur de documentation
│   ├── jshell              REPL Java
│   ├── jdb                 # Debugger
│   ├── jar                 # Gestion d'archives
│   └── ... 30+ outils
├── conf/                   # Fichiers de configuration
│   ├── management/         # Configuration JMX
│   ├── security/           # Politiques de sécurité
│   └── net.properties      # Propriétés réseau
├── include/                # Fichiers header C/C++
│   └── jni.h              # Java Native Interface
├── jmods/                  # Modules Java (JPMS)
│   └── java.base.jmod     # Module de base
├── legal/                  # Licences et notices légales
│   ├── java.base/         # Licences du module base
│   └── ... autres modules
├── lib/                    # Bibliothèques natives et outils
│   ├── jli/               # Java Launcher Interface
│   ├── security/          # Certificats et sécurité
│   ├── server/            # Librairies serveur
│   └── tools.jar          # Outils de développement
├── man/                    # Pages man (Linux/macOS)
│   └── man1/              # Section 1
├── release                 # Fichier de version
└── ... autres fichiers</code></pre>
                </div>

                <h3 class="text-purple">Répertoires importants</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Dossier bin - Outils essentiels</span>
<span class="bash-prompt">$</span> <span class="bash-command">ls /usr/lib/jvm/jdk-21/bin/ | head -10</span>
appletviewer  idlj    jaotc   jarsigner  java    javac   javadoc  javap    jcmd    jconsole
jdb           jdeprscan  jdeps  jfr        jhsdb   jimage  jinfo    jjs      jlink   jmap
jmod          jpackage   jps    jrunscript jshell  jstack  jstat    jstatd   keytool pack200
rmic          rmid       rmiregistry  serialver  unpack200

<span class="bash-comment"># Dossier lib - Bibliothèques système</span>
<span class="bash-prompt">$</span> <span class="bash-command">ls /usr/lib/jvm/jdk-21/lib/</span>
classlist     jexec       jspawnhelper  missioncontrol  security     tools.jar
ct.sym        jli         jvm.cfg       modules         server
jawt.lib      jrt-fs.jar  lib           psfont.properties.ja  src.zip</code></pre>
                </div>
            </div>

            <!-- Outils principaux du SDK -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils principaux du SDK Java</h2>

                <h3 class="text-purple">1. javac - Le compilateur Java</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Compilation basique</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac MonProgramme.java</span>

<span class="bash-comment"># Compilation avec options courantes</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -d ./classes -cp lib/*.jar -encoding UTF-8 -Xlint:unchecked *.java</span>

<span class="bash-comment"># Options importantes :</span>
-d <span class="bash-string">répertoire</span>      <span class="bash-comment"># Répertoire de sortie pour les .class</span>
-cp <span class="bash-string">chemin</span>        <span class="bash-comment"># Classpath (chemins de recherche)</span>
-encoding <span class="bash-string">enc</span>      <span class="bash-comment"># Encodage des fichiers source</span>
-source <span class="bash-string">version</span>    <span class="bash-comment"># Version source (ex: 11, 17, 21)</span>
-target <span class="bash-string">version</span>    <span class="bash-comment"># Version bytecode cible</span>
-parameters       <span class="bash-comment"># Génère les métadonnées des paramètres</span>
-Xlint            <span class="bash-comment"># Active les warnings avancés</span></code></pre>
                </div>

                <h3 class="text-purple">2. java - Le lanceur d'applications</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Execution basique</span>
<span class="bash-prompt">$</span> <span class="bash-command">java MaClasse</span>

<span class="bash-comment"># Avec classpath personnalisé</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -cp "classes:lib/*" com.monapp.Main</span>

<span class="bash-comment"># Options de la JVM</span>
-Xmx512m         <span class="bash-comment"># Mémoire heap maximum (512 MB)</span>
-Xms256m         <span class="bash-comment"># Mémoire heap initiale (256 MB)</span>
-XX:+UseG1GC     <span class="bash-comment"># Utilise le Garbage Collector G1</span>
-Dprop=valeur    <span class="bash-comment"># Définit une propriété système</span>
-verbose:gc      <span class="bash-comment"># Affiche les logs du garbage collector</span>
-server          <span class="bash-comment"># Mode serveur (optimisations)</span>
-client          <span class="bash-comment"># Mode client (démarrage rapide)</span></code></pre>
                </div>

                <h3 class="text-purple">3. jar - Gestion des archives Java</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer un JAR</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar cf monapp.jar -C classes .</span>

<span class="bash-comment"># Créer un JAR exécutable avec manifest</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar cfe monapp.jar com.monapp.Main -C classes .</span>

<span class="bash-comment"># Lister le contenu</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar tf monapp.jar</span>

<span class="bash-comment"># Extraire un JAR</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar xf monapp.jar</span>

<span class="bash-comment"># Mettre à jour un JAR existant</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar uf monapp.jar nouveau.class</span></code></pre>
                </div>
            </div>

            <!-- Outils de développement avancés -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils de développement avancés</h2>

                <h3 class="text-purple">4. jshell - REPL Java (Java 9+)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lancer jshell</span>
<span class="bash-prompt">$</span> <span class="bash-command">jshell</span>

<span class="bash-comment"># Exemples dans jshell :</span>
jshell&gt; <span class="bash-string">String message = "Hello JShell";</span>
message ==&gt; <span class="bash-string">"Hello JShell"</span>

jshell&gt; <span class="bash-string">System.out.println(message);</span>
Hello JShell

jshell&gt; <span class="bash-string">int x = 10, y = 20;</span>
x ==&gt; 10
y ==&gt; 20

jshell&gt; <span class="bash-string">x + y</span>
$4 ==&gt; 30

jshell&gt; <span class="bash-string">/list</span>    <span class="bash-comment"># Lister les commandes</span>
jshell&gt; <span class="bash-string">/save monfichier.java</span>  <span class="bash-comment"># Sauvegarder la session</span>
jshell&gt; <span class="bash-string">/exit</span>   <span class="bash-comment"># Quitter</span></code></pre>
                </div>

                <h3 class="text-purple">5. jdeps - Analyse des dépendances</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Analyser les dépendances d'un JAR</span>
<span class="bash-prompt">$</span> <span class="bash-command">jdeps monapp.jar</span>

<span class="bash-comment"># Analyse détaillée</span>
<span class="bash-prompt">$</span> <span class="bash-command">jdeps -v -cp "lib/*" monapp.jar</span>

<span class="bash-comment"># Vérifier les dépendances vers des modules internes</span>
<span class="bash-prompt">$</span> <span class="bash-command">jdeps --jdk-internals monapp.jar</span>

<span class="bash-comment"># Générer un graphe de dépendances (dot)</span>
<span class="bash-prompt">$</span> <span class="bash-command">jdeps -dotoutput deps monapp.jar</span></code></pre>
                </div>

                <h3 class="text-purple">6. jlink - Création d'images runtime (Java 9+)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer une image runtime minimale</span>
<span class="bash-prompt">$</span> <span class="bash-command">jlink --module-path $JAVA_HOME/jmods:mods --add-modules com.monapp --output monapp-runtime</span>

<span class="bash-comment"># Inclure des services</span>
<span class="bash-prompt">$</span> <span class="bash-command">jlink --add-modules java.base,java.logging --output minimal-jre</span>

<span class="bash-comment"># Compression</span>
<span class="bash-prompt">$</span> <span class="bash-command">jlink --compress=2 --module-path mods --add-modules com.monapp --output monapp-compressed</span>

<span class="bash-comment"># Lancer l'application depuis l'image</span>
<span class="bash-prompt">$</span> <span class="bash-command">./monapp-runtime/bin/java -m com.monapp/com.monapp.Main</span></code></pre>
                </div>
            </div>

            <!-- Outils de monitoring et profiling -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils de monitoring et profiling</h2>

                <h3 class="text-purple">7. jconsole - Monitoring JMX</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lancer jconsole (interface graphique)</span>
<span class="bash-prompt">$</span> <span class="bash-command">jconsole</span>

<span class="bash-comment"># Se connecter à un processus local</span>
<span class="bash-prompt">$</span> <span class="bash-command">jconsole &lt;pid&gt;</span>

<span class="bash-comment"># Se connecter à distance</span>
<span class="bash-prompt">$</span> <span class="bash-command">jconsole hostname:port</span>

<span class="bash-comment"># Informations disponibles :</span>
- Utilisation mémoire (heap, non-heap)
- Threads (nombre, états)
- Classes chargées
- GC activity
- MBeans (opérations de gestion)</code></pre>
                </div>

                <h3 class="text-purple">8. jvisualvm - Profiler avancé</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lancer VisualVM (plus puissant que jconsole)</span>
<span class="bash-prompt">$</span> <span class="bash-command">jvisualvm</span>

<span class="bash-comment"># Fonctionnalités :</span>
- Profiling CPU (méthodes les plus utilisées)
- Profiling mémoire (objets créés)
- Analyse de threads (détection de deadlocks)
- Analyse de heap (objets en mémoire)
- Snapshots (captures d'état)
- Plugins additionnels</code></pre>
                </div>

                <h3 class="text-purple">9. jcmd - Commandes de diagnostic</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lister les processus Java</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd -l</span>

<span class="bash-comment"># Envoyer des commandes à un processus</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd &lt;pid&gt; VM.version</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd &lt;pid&gt; VM.flags</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd &lt;pid&gt; Thread.print</span>      <span class="bash-comment"># Dump des threads</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd &lt;pid&gt; GC.heap_dump fichier.hprof</span>  <span class="bash-comment"># Dump du heap</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd &lt;pid&gt; VM.native_memory</span>   <span class="bash-comment"># Mémoire native</span>
<span class="bash-prompt">$</span> <span class="bash-command">jcmd &lt;pid&gt; help</span>              <span class="bash-comment"># Liste des commandes</span></code></pre>
                </div>
            </div>

            <!-- Outils de debugging -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils de debugging</h2>

                <h3 class="text-purple">10. jdb - Debugger Java</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Déboguer une application</span>
<span class="bash-prompt">$</span> <span class="bash-command">jdb -sourcepath src -classpath classes com.monapp.Main</span>

<span class="bash-comment"># Commandes jdb courantes :</span>
stop at com.monapp.Main:22      <span class="bash-comment"># Point d'arrêt à la ligne 22</span>
run                             <span class="bash-comment"># Démarrer l'execution</span>
cont                            <span class="bash-comment"># Continuer après un breakpoint</span>
step                            <span class="bash-comment"># Step into</span>
next                            <span class="bash-comment"># Step over</span>
print variable                  <span class="bash-comment"># Afficher une variable</span>
locals                          <span class="bash-comment"># Afficher les variables locales</span>
threads                         <span class="bash-comment"># Lister les threads</span>
where                           <span class="bash-comment"># Stack trace du thread courant</span>
quit                            <span class="bash-comment"># Quitter</span></code></pre>
                </div>

                <h3 class="text-purple">11. jstack - Analyse des threads</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Dump de la stack trace des threads</span>
<span class="bash-prompt">$</span> <span class="bash-command">jstack &lt;pid&gt;</span>

<span class="bash-comment"># Dump dans un fichier</span>
<span class="bash-prompt">$</span> <span class="bash-command">jstack &lt;pid&gt; &gt; thread-dump.txt</span>

<span class="bash-comment"># Dump avec informations de verrous</span>
<span class="bash-prompt">$</span> <span class="bash-command">jstack -l &lt;pid&gt;</span>

<span class="bash-comment"># Analyser un deadlock</span>
<span class="bash-prompt">$</span> <span class="bash-command">jstack &lt;pid&gt; | grep -A 10 "deadlock"</span>

<span class="bash-comment"># Surveiller régulièrement</span>
<span class="bash-prompt">$</span> <span class="bash-command">while true; do jstack &lt;pid&gt; &gt;&gt; threads.log; sleep 5; done</span></code></pre>
                </div>

                <h3 class="text-purple">12. jmap - Analyse de la mémoire heap</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Dump du heap (format hprof)</span>
<span class="bash-prompt">$</span> <span class="bash-command">jmap -dump:live,format=b,file=heap.hprof &lt;pid&gt;</span>

<span class="bash-comment"># Statistiques du heap</span>
<span class="bash-prompt">$</span> <span class="bash-command">jmap -heap &lt;pid&gt;</span>

<span class="bash-comment"># Histogramme des objets en mémoire</span>
<span class="bash-prompt">$</span> <span class="bash-command">jmap -histo &lt;pid&gt;</span>

<span class="bash-comment"># Histogramme des objets live seulement</span>
<span class="bash-prompt">$</span> <span class="bash-command">jmap -histo:live &lt;pid&gt;</span>

<span class="bash-comment"># Analyser avec jhat (Java Heap Analysis Tool)</span>
<span class="bash-prompt">$</span> <span class="bash-command">jhat heap.hprof</span>
<span class="bash-comment"># Puis ouvrir http://localhost:7000</span></code></pre>
                </div>
            </div>

            <!-- Gestion des modules (JPMS) -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des modules avec JPMS (Java 9+)</h2>

                <h3 class="text-purple">Modules système</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lister les modules disponibles</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --list-modules</span>

<span class="bash-comment"># Afficher les détails d'un module</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --describe-module java.base</span>

<span class="bash-comment"># Modules essentiels :</span>
java.base        <span class="java-comment">// Classes fondamentales (obligatoire)</span>
java.desktop     <span class="java-comment">// AWT, Swing, applets</span>
java.sql         <span class="java-comment">// API JDBC</span>
java.xml         <span class="java-comment">// XML processing</span>
java.logging     <span class="java-comment">// Logging API</span>
java.net         <span class="java-comment">// Networking</span>
java.nio         <span class="java-comment">// NIO (New I/O)</span></code></pre>
                </div>

                <h3 class="text-purple">Création et utilisation de modules</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Structure d'un module</span>
monmodule/
├── src/
│   └── com.monmodule/
│       ├── module-info.java     <span class="bash-comment"># Déclaration du module</span>
│       └── com/
│           └── monmodule/
│               └── MaClasse.java
└── classes/                     <span class="bash-comment"># Répertoire de sortie</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">module-info.java</h4>
                    <pre v-pre><code class="language-java"><span class="java-keyword">module</span> <span class="java-class">com.monmodule</span> {
    <span class="java-comment">// Dépendances</span>
    <span class="java-keyword">requires</span> java.base;           <span class="java-comment">// Implicite</span>
    <span class="java-keyword">requires</span> java.logging;
    <span class="java-keyword">requires transitive</span> java.sql; <span class="java-comment">// Ré-exporté</span>
    
    <span class="java-comment">// Exports (API publique)</span>
    <span class="java-keyword">exports</span> com.monmodule.api;
    <span class="java-keyword">exports</span> com.monmodule.internal <span class="java-keyword">to</span> com.autremodule;
    
    <span class="java-comment">// Ouverture (pour reflection)</span>
    <span class="java-keyword">opens</span> com.monmodule.reflect;
    
    <span class="java-comment">// Services</span>
    <span class="java-keyword">provides</span> com.monmodule.Service
        <span class="java-keyword">with</span> com.monmodule.ServiceImpl;
    
    <span class="java-keyword">uses</span> com.monmodule.spi.ServiceProvider;
}</code></pre>
                </div>

                <h3 class="text-purple">Compilation et exécution avec modules</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Compilation avec module path</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -d classes --module-source-path src --module com.monmodule</span>

<span class="bash-comment"># Création d'un module JAR</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar --create --file=monmodule.jar -C classes .</span>

<span class="bash-comment"># Execution avec module path</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --module-path "monmodule.jar:lib/*" --module com.monmodule/com.monmodule.Main</span></code></pre>
                </div>
            </div>

            <!-- Configuration et personnalisation -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Configuration et personnalisation du SDK</h2>

                <h3 class="text-purple">Variables d'environnement</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># JAVA_HOME - Répertoire d'installation du JDK</span>
<span class="bash-keyword">export</span> JAVA_HOME=/usr/lib/jvm/jdk-21
<span class="bash-keyword">export</span> PATH=<span class="bash-variable">$JAVA_HOME</span>/bin:<span class="bash-variable">$PATH</span>

<span class="bash-comment"># CLASSPATH - Chemin de recherche des classes (obsolète)</span>
<span class="bash-keyword">export</span> CLASSPATH=.:<span class="bash-variable">$HOME</span>/lib/*.jar

<span class="bash-comment"># Options par défaut de la JVM</span>
<span class="bash-keyword">export</span> JAVA_OPTS=<span class="bash-string">"-Xmx2g -Xms512m -XX:+UseG1GC"</span>

<span class="bash-comment"># Pour les applications GUI (AWT/Swing)</span>
<span class="bash-keyword">export</span> _JAVA_OPTIONS=<span class="bash-string">"-Dawt.useSystemAAFontSettings=on"</span>

<span class="bash-comment"># Proxy settings</span>
<span class="bash-keyword">export</span> JAVA_PROXY_OPTS=<span class="bash-string">"-Dhttp.proxyHost=proxy -Dhttp.proxyPort=8080"</span></code></pre>
                </div>

                <h3 class="text-purple">Fichiers de configuration</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># java.security - Politiques de sécurité</span>
<span class="bash-prompt">$</span> <span class="bash-command">nano $JAVA_HOME/conf/security/java.security</span>

<span class="bash-comment"># logging.properties - Configuration des logs</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -Djava.util.logging.config.file=logging.properties MonApp</span>

<span class="bash-comment"># net.properties - Propriétés réseau</span>
<span class="bash-prompt">$</span> <span class="bash-command">cat $JAVA_HOME/conf/net.properties</span>

<span class="bash-comment"># management.properties - JMX monitoring</span>
<span class="bash-prompt">$</span> <span class="bash-command">cat $JAVA_HOME/conf/management/management.properties</span></code></pre>
                </div>

                <h3 class="text-purple">Fichiers de policy de sécurité</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Exemple de fichier policy.policy</span>
<span class="java-comment">// Donne tous les droits</span>
grant {
    permission java.security.AllPermission;
};

<span class="java-comment">// Politique restrictive</span>
grant codeBase <span class="java-string">"file:${java.home}/lib/-"</span> {
    permission java.security.AllPermission;
};

grant codeBase <span class="java-string">"file:${java.home}/jre/lib/-"</span> {
    permission java.security.AllPermission;
};

<span class="java-comment">// Exécution avec politique de sécurité</span>
<span class="java-comment">// java -Djava.security.manager -Djava.security.policy=policy.policy MonApp</span></code></pre>
                </div>
            </div>

            <!-- Bonnes pratiques et optimisation -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques et optimisation</h2>

                <h3 class="text-purple">Optimisation de la compilation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Compilation incrémentale (IDE)</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -d build/classes -sourcepath src -cp libs/*.jar @sources.txt</span>

<span class="bash-comment"># Utiliser le compilateur du serveur (plus rapide)</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -J-server *.java</span>

<span class="bash-comment"># Générer les métadonnées de débogage</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -g:lines,vars,source *.java</span>

<span class="bash-comment"># Désactiver les assertions en production</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -da *.java</span>  <span class="bash-comment"># Disable assertions</span></code></pre>
                </div>

                <h3 class="text-purple">Optimisation de l'exécution</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Choisir le bon garbage collector</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XX:+UseG1GC -Xmx4g -Xms4g MonApp</span>       <span class="bash-comment"># G1GC (par défaut depuis Java 9)</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XX:+UseParallelGC MonApp</span>               <span class="bash-comment"># Throughput</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XX:+UseZGC -Xmx16g MonApp</span>               <span class="bash-comment"># ZGC (low latency, Java 11+)</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XX:+UseShenandoahGC MonApp</span>             <span class="bash-comment"># Shenandoah (low latency)</span>

<span class="bash-comment"># Ajuster la taille du heap</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -Xmx4096m -Xms4096m -Xmn2048m MonApp</span>   <span class="bash-comment"># Heap max/min, young generation</span>

<span class="bash-comment"># Tuning du GC</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XX:MaxGCPauseMillis=200 -XX:G1HeapRegionSize=16m MonApp</span>

<span class="bash-comment"># Native memory tracking</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XX:NativeMemoryTracking=detail -XX:+UnlockDiagnosticVMOptions MonApp</span></code></pre>
                </div>

                <h3 class="text-purple">Sécurité et performance</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Désactiver les fonctionnalités dangereuses</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -Djava.security.manager -Djava.security.policy==policy.policy MonApp</span>

<span class="bash-comment"># Limiter la reflection</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --illegal-access=deny MonApp</span>  <span class="bash-comment"># Java 9+</span>

<span class="bash-comment"># TLS/SSL security</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -Dhttps.protocols=TLSv1.2,TLSv1.3 -Djdk.tls.client.protocols=TLSv1.2 MonApp</span>

<span class="bash-comment"># Cryptographic strength</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -Djava.security.properties=java.security MonApp</span></code></pre>
                </div>
            </div>

            <!-- Dépannage commun -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Dépannage commun du SDK</h2>

                <h3 class="text-purple">Problèmes d'installation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Vérifier l'installation</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -version</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -version</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo $JAVA_HOME</span>
<span class="bash-prompt">$</span> <span class="bash-command">which java</span>
<span class="bash-prompt">$</span> <span class="bash-command">which javac</span>

<span class="bash-comment"># Problème : java et javac versions différentes</span>
<span class="bash-comment"># Solution : Vérifier $PATH, JAVA_HOME, alternatives (Linux)</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo update-alternatives --config java</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo update-alternatives --config javac</span></code></pre>
                </div>

                <h3 class="text-purple">Problèmes de classpath</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Erreur : ClassNotFoundException ou NoClassDefFoundError</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -cp ".:lib/*:conf" MonApp</span>  <span class="bash-comment"># Sous Unix/Linux/macOS</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -cp ".;lib/*;conf" MonApp</span>  <span class="bash-comment"># Sous Windows</span>

<span class="bash-comment"># Afficher le classpath effectif</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -XshowSettings:properties -version 2>&1 | grep java.class.path</span>

<span class="bash-comment"># Vérifier le contenu d'un JAR</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar tf monapp.jar | grep MaClasse</span></code></pre>
                </div>

                <h3 class="text-purple">Problèmes de mémoire</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Erreur : OutOfMemoryError</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -Xmx4g -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./heap.hprof MonApp</span>

<span class="bash-comment"># Analyser le dump mémoire</span>
<span class="bash-prompt">$</span> <span class="bash-command">jhat heap.hprof</span>
<span class="bash-prompt">$</span> <span class="bash-command">jvisualvm</span>  <span class="bash-comment"># Charger le fichier .hprof</span>

<span class="bash-comment"># Monitoring en temps réel</span>
<span class="bash-prompt">$</span> <span class="bash-command">jstat -gcutil &lt;pid&gt; 1000 10</span>  <span class="bash-comment"># Toutes les secondes, 10 fois</span></code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique : Maîtriser les outils du SDK</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Utiliser les outils du SDK Java pour développer, déboguer et optimiser une application.
                    </p>
                    <ol class="textExemple">
                        <li>Créez une application simple avec plusieurs classes</li>
                        <li>Utilisez javac avec différentes options de compilation</li>
                        <li>Créez un JAR exécutable avec manifest</li>
                        <li>Testez jshell pour explorer des expressions Java</li>
                        <li>Utilisez jdeps pour analyser les dépendances de votre JAR</li>
                        <li>Créez un dump mémoire avec jmap et analysez-le avec jvisualvm</li>
                        <li>Générez la documentation avec javadoc</li>
                        <li>Expérimentez avec différentes options de la JVM (-Xmx, -XX:+UseG1GC, etc.)</li>
                        <li>Créez une image runtime minimale avec jlink</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir des exemples de commandes</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Commandes pratiques :</h4>
                        
                        <h5 class="text-purple">Création et compilation :</h5>
                        <div class="code-example">
                            <pre v-pre><code class="language-bash"><span class="bash-comment"># 1. Créer la structure</span>
<span class="bash-prompt">$</span> <span class="bash-command">mkdir -p src/com/monapp && mkdir classes lib</span>

<span class="bash-comment"># 2. Créer une classe simple</span>
<span class="bash-prompt">$</span> <span class="bash-command">cat &gt; src/com/monapp/Main.java &lt;&lt; 'EOF'</span>
package com.monapp;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello SDK!");
        Calculator calc = new Calculator();
        System.out.println("5 + 3 = " + calc.add(5, 3));
    }
}
EOF

<span class="bash-prompt">$</span> <span class="bash-command">cat &gt; src/com/monapp/Calculator.java &lt;&lt; 'EOF'</span>
package com.monapp;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int multiply(int a, int b) {
        int result = 0;
        for (int i = 0; i < b; i++) {
            result = add(result, a);  <span class="bash-comment"># Utilisation intentionnelle pour l'exercice</span>
        }
        return result;
    }
}
EOF

<span class="bash-comment"># 3. Compiler</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac -d classes -sourcepath src src/com/monapp/*.java</span>

<span class="bash-comment"># 4. Créer un JAR</span>
<span class="bash-prompt">$</span> <span class="bash-command">jar cfe monapp.jar com.monapp.Main -C classes .</span>

<span class="bash-comment"># 5. Analyser avec jdeps</span>
<span class="bash-prompt">$</span> <span class="bash-command">jdeps monapp.jar</span>

<span class="bash-comment"># 6. Générer la documentation</span>
<span class="bash-prompt">$</span> <span class="bash-command">javadoc -d docs -sourcepath src -subpackages com.monapp</span></code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources avancées</h2>
                <p class="textExemple">
                    Le SDK Java est un ensemble d'outils puissants et complets qui va bien au-delà 
                    de la simple compilation et exécution de code. Maîtriser ces outils est essentiel 
                    pour développer des applications Java performantes, maintenables et sécurisées.
                </p>

                <h3 class="text-purple">Points clés à retenir :</h3>
                <ul class="textExemple">
                    <li>Le JDK inclut le JRE plus les outils de développement</li>
                    <li>Chaque outil a un rôle spécifique (compilation, debugging, monitoring, etc.)</li>
                    <li>Les options de la JVM permettent d'optimiser les performances</li>
                    <li>Les modules (JPMS) offrent une meilleure encapsulation depuis Java 9</li>
                    <li>La sécurité doit être configurée selon les besoins de l'application</li>
                </ul>

                <h3 class="text-purple">Ressources avancées :</h3>
                <ul class="textExemple">
                    <li><a href="https://docs.oracle.com/javase/8/docs/technotes/tools/" target="_blank" class="btn-purple btn-hover">Documentation officielle des outils Java</a></li>
                    <li><a href="https://openjdk.org/groups/hotspot/docs/RuntimeOverview.html" target="_blank" class="btn-purple btn-hover">Architecture de la JVM HotSpot</a></li>
                    <li><a href="https://docs.oracle.com/javase/9/tools/jshell.htm" target="_blank" class="btn-purple btn-hover">Guide complet de jshell</a></li>
                    <li><a href="https://docs.oracle.com/javase/9/jpms/toc.htm" target="_blank" class="btn-purple btn-hover">Java Platform Module System</a></li>
                    <li><a href="https://visualvm.github.io/" target="_blank" class="btn-purple btn-hover">VisualVM Documentation</a></li>
                    <li><a href="https://github.com/openjdk/jmh" target="_blank" class="btn-purple btn-hover">JMH - Java Microbenchmark Harness</a></li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Commande pour explorer tous les outils</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lister tous les outils disponibles dans le bin/</span>
<span class="bash-prompt">$</span> <span class="bash-command">ls $JAVA_HOME/bin/ | xargs -I {} sh -c 'echo "=== {} ===" && $JAVA_HOME/bin/{} --help 2>&1 | head -5'</span>

<span class="bash-comment"># Pour chaque outil, lire la documentation :</span>
<span class="bash-prompt">$</span> <span class="bash-command">man java</span>      <span class="bash-comment"># Sur Linux/macOS</span>
<span class="bash-prompt">$</span> <span class="bash-command">java -help</span>    <span class="bash-comment"># Aide en ligne</span></code></pre>
                </div>

                <p class="textExemple">
                    Le SDK Java évolue constamment avec de nouveaux outils et améliorations. 
                    Rester à jour avec les dernières versions et fonctionnalités est crucial 
                    pour tirer le meilleur parti de la plateforme Java.
                </p>
            </div>
        </div>
    </div>
</template>

<script>

</script>

<style scoped>
/* Styles en violet pour correspondre à votre projet */
.lesson-container {
    padding: 2rem;
    background: #f8f9fa;
    min-height: 100vh;
}

.lesson-content {
    max-width: 1200px;
    margin: 0 auto;
    width: 100%;
    overflow-x: hidden;
}

.lesson-header {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
    padding: 3rem 2rem;
    border-radius: 15px;
    margin-bottom: 2rem;
    text-align: center;
    position: relative;
    overflow: hidden;
}

.lesson-header::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
}

.lesson-header h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    position: relative;
}

.lesson-meta {
    font-size: 1.1rem;
    opacity: 0.9;
    position: relative;
}

.lesson-section {
    padding: 2rem;
    margin-bottom: 2rem;
    border-radius: 15px;
    transition: all 0.3s ease;
    width: 100%;
    overflow-x: hidden;
    box-sizing: border-box;
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

.bg-light-purple {
    background-color: #f8f6ff;
    border-radius: 12px;
}

.border-purple {
    border: 2px solid #e0d6ff;
    border-radius: 15px;
    transition: all 0.3s ease;
}

.text-purple {
    color: #6A3093 !important;
}

.text-white {
    color: white !important;
}

.btn-purple {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
    border: none;
    color: white;
    font-weight: 600;
    padding: 12px 24px;
    border-radius: 8px;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(106, 48, 147, 0.2);
    text-decoration: none;
    display: inline-block;
    cursor: pointer;
    margin: 0.5rem 0;
}

.btn-purple:hover {
    background: linear-gradient(135deg, #7a4fa8 0%, #5a287a 100%);
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(106, 48, 147, 0.3);
    color: white;
}

.btn-hover {
    position: relative;
    overflow: hidden;
}

.btn-hover::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 50%;
    transition: all 0.5s ease;
    transform: translate(-50%, -50%);
}

.btn-hover:hover::after {
    width: 300px;
    height: 300px;
}

.code-example,
.code-block {
    margin: 1.5rem 0;
    width: 100%;
    box-sizing: border-box;
}

.code-comparison {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin: 1.5rem 0;
    width: 100%;
}

pre {
    background: #1e1e1e !important;
    color: #d4d4d4 !important;
    padding: 1.5rem !important;
    border-radius: 8px;
    overflow-x: auto;
    border: 1px solid #333;
    font-family: 'Consolas', 'Monaco', 'Courier New', monospace;
    font-size: 0.9rem;
    line-height: 1.5;
    max-width: 100%;
    width: 100%;
    box-sizing: border-box;
    white-space: pre-wrap;
    word-wrap: break-word;
    word-break: break-word;
}

pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs Bash */
.bash-prompt {
    color: #2ECC71 !important;
    font-weight: bold;
}

.bash-command {
    color: #F1C40F !important;
}

.bash-comment {
    color: #7F8C8D !important;
    font-style: italic;
}

.bash-string {
    color: #E74C3C !important;
}

.bash-keyword {
    color: #3498DB !important;
}

.bash-parameter {
    color: #9B59B6 !important;
}

.bash-number {
    color: #1ABC9C !important;
}

.bash-variable {
    color: #9CDCFE !important;
}

/* Couleurs Java */
.java-keyword {
    color: #569CD6 !important;
}

.java-function {
    color: #DCDCAA !important;
}

.java-class {
    color: #4EC9B0 !important;
}

.java-variable {
    color: #9CDCFE !important;
}

.java-string {
    color: #CE9178 !important;
}

.java-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.java-number {
    color: #B5CEA8 !important;
}

.exercise {
    margin: 2rem 0;
}

.solution {
    margin: 1rem 0;
}

.solution-content {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #8B5FBF;
}

.solution-content h4 {
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
}

details summary {
    cursor: pointer;
    outline: none;
}

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

@media (max-width: 768px) {
    .lesson-container {
        padding: 1rem;
    }

    .lesson-header {
        padding: 2rem 1rem;
    }

    .lesson-header h1 {
        font-size: 2rem;
    }

    .lesson-section {
        padding: 1.5rem;
    }

    .code-comparison {
        grid-template-columns: 1fr;
        gap: 1rem;
    }

    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
    }
}

@media (max-width: 480px) {
    pre {
        padding: 0.75rem !important;
        font-size: 0.8rem;
    }

    .lesson-container {
        padding: 0.5rem;
    }

    .lesson-section {
        padding: 1rem;
    }

    .lesson-header {
        padding: 1.5rem 1rem;
    }

    .lesson-header h1 {
        font-size: 1.75rem;
    }
}

@media (min-width: 1400px) {
    .lesson-content {
        max-width: 1300px;
    }
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.lesson-section {
    animation: fadeInUp 0.6s ease forwards;
}
</style>