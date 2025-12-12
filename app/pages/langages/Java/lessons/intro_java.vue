<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Introduction au Langage Java</h1>
                <p class="lesson-meta text-white">Découvrez les fondamentaux, l'histoire et les caractéristiques du langage de programmation Java</p>
            </div>

            <!-- Introduction générale -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Java ?</h2>
                <p class="textExemple">
                    Java est un langage de programmation orienté objet, multiplateforme et polyvalent, 
                    créé par Sun Microsystems (aujourd'hui Oracle) en 1995. C'est l'un des langages les plus 
                    utilisés au monde, particulièrement pour le développement d'applications d'entreprise, 
                    web, mobiles (Android) et systèmes embarqués.
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Caractéristiques principales de Java</span>
Plateforme Indépendante → Orienté Objet → Robuste → Sécurisé → Performant</code></pre>
                </div>
            </div>

            <!-- Histoire et évolution -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Histoire et évolution de Java</h2>
                
                <h3 class="text-purple">Les origines</h3>
                <p class="textExemple">
                    Java a été créé par James Gosling et son équipe chez Sun Microsystems dans les années 1990. 
                    Initialement appelé "Oak" (en référence à un chêne devant le bureau de Gosling), 
                    le langage a été renommé Java (inspiré du café Java) avant sa sortie publique.
                </p>

                <h3 class="text-purple">Chronologie des versions majeures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">1996 : Java 1.0 - Première version publique
1998 : Java 1.2 (Java 2) - Introduction des collections
2004 : Java 5 (1.5) - Génériques, annotations, boucle for-each
2011 : Java 7 - Try-with-resources, NIO.2
2014 : Java 8 (LTS) - Lambda expressions, Stream API
2017 : Java 9 - Modules (Project Jigsaw)
2018 : Java 11 (LTS) - HTTP Client, var local
2021 : Java 17 (LTS) - Pattern matching, sealed classes
2023 : Java 21 (LTS) - Virtual Threads, Pattern matching records</code></pre>
                </div>
            </div>

            <!-- Les caractéristiques fondamentales -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Caractéristiques fondamentales de Java</h2>
                
                <h3 class="text-purple">1. Plateforme indépendante - "Write Once, Run Anywhere" (WORA)</h3>
                <p class="textExemple">
                    Le code source Java est compilé en bytecode qui s'exécute sur la Java Virtual Machine (JVM). 
                    Cela permet d'exécuter le même programme sur n'importe quel système d'exploitation 
                    (Windows, Linux, macOS) sans recompilation.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Architecture Java</span>
Code Source (.java) → Compilateur Java → Bytecode (.class) → JVM → Exécution</code></pre>
                </div>

                <h3 class="text-purple">2. Orienté objet</h3>
                <p class="textExemple">
                    Java est entièrement orienté objet (contrairement à C++ qui est hybride). Tout en Java 
                    est un objet (sauf les types primitifs). Cela implique les concepts de :
                </p>
                <ul class="textExemple">
                    <li><strong>Classes et objets</strong> : Modèle de programmation basé sur des objets</li>
                    <li><strong>Encapsulation</strong> : Masquage des détails d'implémentation</li>
                    <li><strong>Héritage</strong> : Réutilisation du code via l'héritage de classes</li>
                    <li><strong>Polymorphisme</strong> : Capacité d'un objet à prendre plusieurs formes</li>
                </ul>

                <h3 class="text-purple">3. Gestion automatique de la mémoire (Garbage Collection)</h3>
                <p class="textExemple">
                    Java gère automatiquement l'allocation et la libération de la mémoire via le 
                    ramasse-miettes (Garbage Collector). Le développeur n'a pas à libérer manuellement 
                    la mémoire comme en C ou C++.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Pas besoin de libérer la mémoire manuellement</span>
<span class="java-class">List</span>&lt;<span class="java-class">String</span>&gt; <span class="java-variable">list</span> = <span class="java-keyword">new</span> <span class="java-class">ArrayList</span>&lt;&gt;();
<span class="java-variable">list</span>.<span class="java-function">add</span>(<span class="java-string">"Java"</span>);
<span class="java-comment">// Le garbage collector libérera la mémoire automatiquement</span>
<span class="java-comment">// quand l'objet ne sera plus référencé</span></code></pre>
                </div>

                <h3 class="text-purple">4. Typage statique et fort</h3>
                <p class="textExemple">
                    Java est un langage à typage statique : les types des variables sont vérifiés à la 
                    compilation. C'est aussi un langage à typage fort : les conversions entre types doivent 
                    être explicites.
                </p>

                <h3 class="text-purple">5. Sécurité intégrée</h3>
                <p class="textExemple">
                    Java a été conçu avec la sécurité en tête :
                </p>
                <ul class="textExemple">
                    <li>Pas de pointeurs explicites (contrairement à C/C++)</li>
                    <li>Vérification du bytecode avant exécution</li>
                    <li>Système de sécurité par sandboxing pour les applets</li>
                    <li>Gestion des permissions d'accès</li>
                </ul>

                <h3 class="text-purple">6. Multithreading natif</h3>
                <p class="textExemple">
                    Java supporte nativement la programmation multithreadée, permettant d'exécuter 
                    plusieurs tâches simultanément.
                </p>
            </div>

            <!-- Architecture Java -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture de la plateforme Java</h2>
                
                <h3 class="text-purple">Les trois composants principaux</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">1. Java Development Kit (JDK)</h4>
                        <pre v-pre><code class="language-text">• Environnement de développement
• Compilateur (javac)
• Outils (debugger, profiler)
• Bibliothèques de développement
• Pour les développeurs</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">2. Java Runtime Environment (JRE)</h4>
                        <pre v-pre><code class="language-text">• Environnement d'exécution
• Java Virtual Machine (JVM)
• Bibliothèques d'exécution
• Pour exécuter des applications
• Inclus dans le JDK</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">3. Java Virtual Machine (JVM)</h4>
                    <pre v-pre><code class="language-text">• Machine virtuelle qui exécute le bytecode
• Gère la mémoire (heap, stack)
• Execute le garbage collector
• Fournit un environnement isolé
• Implémentations : HotSpot (Oracle), OpenJ9 (IBM)</code></pre>
                </div>

                <h3 class="text-purple">Cycle de vie d'un programme Java</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">Édition → Compilation → Chargement → Vérification → Exécution</code></pre>
                </div>
            </div>

            <!-- Premier programme Java -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Votre premier programme Java</h2>
                
                <h3 class="text-purple">Structure de base</h3>
                <div class="code-example">
                    <h4 class="text-purple">HelloWorld.java</h4>
                    <pre v-pre><code class="language-java"><span class="java-comment">// Déclaration de la classe</span>
<span class="java-keyword">public class</span> <span class="java-class">HelloWorld</span> {
    
    <span class="java-comment">// Méthode principale - point d'entrée du programme</span>
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        
        <span class="java-comment">// Instruction d'affichage</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Hello, World!"</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Explication ligne par ligne</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Commentaire sur une ligne - ignoré par le compilateur</span>

<span class="java-keyword">public</span> <span class="java-comment">// Modificateur d'accès - accessible de partout</span>
<span class="java-keyword">class</span> <span class="java-comment">// Mot-clé pour déclarer une classe</span>
<span class="java-class">HelloWorld</span> <span class="java-comment">// Nom de la classe (commence par majuscule)</span>
{ <span class="java-comment">// Début du bloc de la classe</span>

    <span class="java-keyword">public</span> <span class="java-comment">// Accessible de partout</span>
    <span class="java-keyword">static</span> <span class="java-comment">// Méthode de classe (pas besoin d'instance)</span>
    <span class="java-keyword">void</span> <span class="java-comment">// Type de retour (aucun)</span>
    <span class="java-function">main</span> <span class="java-comment">// Nom de la méthode principale</span>
    (<span class="java-class">String</span>[] <span class="java-variable">args</span>) <span class="java-comment">// Paramètres (tableau de chaînes)</span>
    { <span class="java-comment">// Début du bloc de la méthode</span>
        
        <span class="java-class">System</span> <span class="java-comment">// Classe système</span>
        .<span class="java-variable">out</span> <span class="java-comment">// Objet de sortie standard</span>
        .<span class="java-function">println</span> <span class="java-comment">// Méthode pour afficher avec retour à la ligne</span>
        (<span class="java-string">"Hello, World!"</span>); <span class="java-comment">// Chaîne à afficher</span>
        
    } <span class="java-comment">// Fin du bloc de la méthode</span>
    
} <span class="java-comment">// Fin du bloc de la classe</span></code></pre>
                </div>

                <h3 class="text-purple">Compilation et exécution</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># 1. Compilation du code source en bytecode</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac HelloWorld.java</span>

<span class="bash-comment"># 2. Résultat : fichier HelloWorld.class (bytecode)</span>
<span class="bash-prompt">$</span> <span class="bash-command">ls</span>
HelloWorld.java  HelloWorld.class

<span class="bash-comment"># 3. Exécution via la JVM</span>
<span class="bash-prompt">$</span> <span class="bash-command">java HelloWorld</span>
Hello, World!</code></pre>
                </div>
            </div>

            <!-- Syntaxe de base -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de base de Java</h2>

                <h3 class="text-purple">1. Variables et types de données</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Types primitifs (stockés par valeur)</span>
<span class="java-keyword">int</span> <span class="java-variable">age</span> = <span class="java-number">25</span>;               <span class="java-comment">// Entier (4 octets)</span>
<span class="java-keyword">double</span> <span class="java-variable">price</span> = <span class="java-number">19.99</span>;        <span class="java-comment">// Nombre à virgule (8 octets)</span>
<span class="java-keyword">boolean</span> <span class="java-variable">isActive</span> = <span class="java-keyword">true</span>;    <span class="java-comment">// Booléen (true/false)</span>
<span class="java-keyword">char</span> <span class="java-variable">grade</span> = <span class="java-string">'A'</span>;           <span class="java-comment">// Caractère (2 octets)</span>

<span class="java-comment">// Types objets (stockés par référence)</span>
<span class="java-class">String</span> <span class="java-variable">name</span> = <span class="java-string">"Java"</span>;       <span class="java-comment">// Chaîne de caractères</span>
<span class="java-class">Integer</span> <span class="java-variable">count</span> = <span class="java-number">100</span>;         <span class="java-comment">// Objet entier (wrapper)</span>
<span class="java-class">Date</span> <span class="java-variable">today</span> = <span class="java-keyword">new</span> <span class="java-class">Date</span>();   <span class="java-comment">// Objet Date</span></code></pre>
                </div>

                <h3 class="text-purple">2. Structures de contrôle</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Conditions</h4>
                        <pre v-pre><code class="language-java"><span class="java-keyword">if</span> (<span class="java-variable">age</span> &gt;= <span class="java-number">18</span>) {
    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Majeur"</span>);
} <span class="java-keyword">else</span> {
    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Mineur"</span>);
}

<span class="java-keyword">switch</span> (<span class="java-variable">day</span>) {
    <span class="java-keyword">case</span> <span class="java-number">1</span>: <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Lundi"</span>); <span class="java-keyword">break</span>;
    <span class="java-keyword">case</span> <span class="java-number">2</span>: <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Mardi"</span>); <span class="java-keyword">break</span>;
    <span class="java-keyword">default</span>: <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Autre jour"</span>);
}</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Boucles</h4>
                        <pre v-pre><code class="language-java"><span class="java-comment">// Boucle for</span>
<span class="java-keyword">for</span> (<span class="java-keyword">int</span> <span class="java-variable">i</span> = <span class="java-number">0</span>; <span class="java-variable">i</span> &lt; <span class="java-number">10</span>; <span class="java-variable">i</span>++) {
    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-variable">i</span>);
}

<span class="java-comment">// Boucle while</span>
<span class="java-keyword">while</span> (<span class="java-variable">count</span> &gt; <span class="java-number">0</span>) {
    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-variable">count</span>);
    <span class="java-variable">count</span>--;
}

<span class="java-comment">// Boucle do-while</span>
<span class="java-keyword">do</span> {
    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Au moins une fois"</span>);
} <span class="java-keyword">while</span> (<span class="java-keyword">false</span>);</code></pre>
                    </div>
                </div>

                <h3 class="text-purple">3. Tableaux</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Déclaration et initialisation</span>
<span class="java-keyword">int</span>[] <span class="java-variable">numbers</span> = <span class="java-keyword">new</span> <span class="java-keyword">int</span>[<span class="java-number">5</span>];  <span class="java-comment">// Tableau de 5 entiers</span>
<span class="java-class">String</span>[] <span class="java-variable">names</span> = {<span class="java-string">"Alice"</span>, <span class="java-string">"Bob"</span>, <span class="java-string">"Charlie"</span>};

<span class="java-comment">// Accès aux éléments</span>
<span class="java-variable">numbers</span>[<span class="java-number">0</span>] = <span class="java-number">10</span>;
<span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-variable">names</span>[<span class="java-number">1</span>]);  <span class="java-comment">// Affiche "Bob"</span>

<span class="java-comment">// Longueur du tableau</span>
<span class="java-keyword">int</span> <span class="java-variable">length</span> = <span class="java-variable">names</span>.<span class="java-variable">length</span>;  <span class="java-comment">// = 3</span></code></pre>
                </div>
            </div>

            <!-- Programmation orientée objet en Java -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Programmation orientée objet en Java</h2>

                <h3 class="text-purple">1. Classes et objets</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Définition d'une classe</span>
<span class="java-keyword">public class</span> <span class="java-class">Personne</span> {
    <span class="java-comment">// Attributs (variables d'instance)</span>
    <span class="java-keyword">private</span> <span class="java-class">String</span> <span class="java-variable">nom</span>;
    <span class="java-keyword">private</span> <span class="java-keyword">int</span> <span class="java-variable">age</span>;
    
    <span class="java-comment">// Constructeur</span>
    <span class="java-keyword">public</span> <span class="java-function">Personne</span>(<span class="java-class">String</span> <span class="java-variable">nom</span>, <span class="java-keyword">int</span> <span class="java-variable">age</span>) {
        <span class="java-keyword">this</span>.<span class="java-variable">nom</span> = <span class="java-variable">nom</span>;
        <span class="java-keyword">this</span>.<span class="java-variable">age</span> = <span class="java-variable">age</span>;
    }
    
    <span class="java-comment">// Méthodes (comportements)</span>
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">sePresenter</span>() {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Je m'appelle "</span> + <span class="java-variable">nom</span> + <span class="java-string">" et j'ai "</span> + <span class="java-variable">age</span> + <span class="java-string">" ans."</span>);
    }
    
    <span class="java-comment">// Getters et setters (encapsulation)</span>
    <span class="java-keyword">public</span> <span class="java-class">String</span> <span class="java-function">getNom</span>() { <span class="java-keyword">return</span> <span class="java-variable">nom</span>; }
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">setNom</span>(<span class="java-class">String</span> <span class="java-variable">nom</span>) { <span class="java-keyword">this</span>.<span class="java-variable">nom</span> = <span class="java-variable">nom</span>; }
}

<span class="java-comment">// Utilisation de la classe</span>
<span class="java-class">Personne</span> <span class="java-variable">personne1</span> = <span class="java-keyword">new</span> <span class="java-class">Personne</span>(<span class="java-string">"Alice"</span>, <span class="java-number">30</span>);
<span class="java-variable">personne1</span>.<span class="java-function">sePresenter</span>();</code></pre>
                </div>

                <h3 class="text-purple">2. Héritage</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Classe parente</span>
<span class="java-keyword">class</span> <span class="java-class">Vehicule</span> {
    <span class="java-keyword">protected</span> <span class="java-class">String</span> <span class="java-variable">marque</span>;
    
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">demarrer</span>() {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Le véhicule démarre."</span>);
    }
}

<span class="java-comment">// Classe fille</span>
<span class="java-keyword">class</span> <span class="java-class">Voiture</span> <span class="java-keyword">extends</span> <span class="java-class">Vehicule</span> {
    <span class="java-keyword">private</span> <span class="java-keyword">int</span> <span class="java-variable">portes</span>;
    
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">klaxonner</span>() {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Tut tut!"</span>);
    }
    
    <span class="java-comment">// Redéfinition (override) de méthode</span>
    <span class="java-marker">@Override</span>
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">demarrer</span>() {
        <span class="java-keyword">super</span>.<span class="java-function">demarrer</span>();  <span class="java-comment">// Appel à la méthode parent</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"La voiture roule."</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">3. Interfaces et classes abstraites</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Interface (contrat)</span>
<span class="java-keyword">interface</span> <span class="java-class">Transport</span> {
    <span class="java-keyword">void</span> <span class="java-function">transporter</span>(<span class="java-class">String</span> <span class="java-variable">destination</span>);
    <span class="java-keyword">int</span> <span class="java-function">getCapacite</span>();
}

<span class="java-comment">// Classe abstraite</span>
<span class="java-keyword">abstract class</span> <span class="java-class">Animal</span> {
    <span class="java-keyword">protected</span> <span class="java-class">String</span> <span class="java-variable">nom</span>;
    
    <span class="java-keyword">public</span> <span class="java-keyword">abstract</span> <span class="java-keyword">void</span> <span class="java-function">faireDuBruit</span>();  <span class="java-comment">// Méthode abstraite</span>
    
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">dormir</span>() {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Zzz..."</span>);
    }
}

<span class="java-comment">// Implémentation</span>
<span class="java-keyword">class</span> <span class="java-class">Chien</span> <span class="java-keyword">extends</span> <span class="java-class">Animal</span> <span class="java-keyword">implements</span> <span class="java-class">Transport</span> {
    <span class="java-marker">@Override</span>
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">faireDuBruit</span>() {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Woof!"</span>);
    }
    
    <span class="java-marker">@Override</span>
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">transporter</span>(<span class="java-class">String</span> <span class="java-variable">destination</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Transport vers: "</span> + <span class="java-variable">destination</span>);
    }
    
    <span class="java-marker">@Override</span>
    <span class="java-keyword">public</span> <span class="java-keyword">int</span> <span class="java-function">getCapacite</span>() {
        <span class="java-keyword">return</span> <span class="java-number">1</span>;
    }
}</code></pre>
                </div>
            </div>

            <!-- Écosystème Java -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">L'écosystème Java</h2>

                <h3 class="text-purple">1. Éditions Java</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Java SE (Standard Edition)</h4>
                        <pre v-pre><code class="language-text">• Noyau de la plateforme Java
• API de base (collections, I/O, réseau)
• Pour applications desktop
• Développement général
• La plus utilisée</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Java EE (Enterprise Edition)</h4>
                        <pre v-pre><code class="language-text">• Jakarta EE (nouveau nom)
• Extensions pour entreprises
• Servlets, JSP, EJB, JPA
• Développement web/services
• Frameworks : Spring</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Java ME (Micro Edition)</h4>
                    <pre v-pre><code class="language-text">• Pour appareils embarqués
• Téléphones mobiles (anciens)
• Appareils IoT
• Ressources limitées
• Moins utilisé aujourd'hui</code></pre>
                </div>

                <h3 class="text-purple">2. Frameworks populaires</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">• Spring/Spring Boot : Framework d'entreprise
• Hibernate : ORM (Object-Relational Mapping)
• Maven/Gradle : Outils de build
• JUnit : Tests unitaires
• Lombok : Réduction du code boilerplate
• Apache Commons : Bibliothèques utilitaires</code></pre>
                </div>

                <h3 class="text-purple">3. Domaines d'application</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">• Applications d'entreprise (ERP, CRM)
• Développement web (backend)
• Applications Android
• Systèmes bancaires/financiers
• Big Data (Hadoop, Spark)
• Jeux vidéo (Minecraft)
• IoT et systèmes embarqués
• Recherche scientifique</code></pre>
                </div>
            </div>

            <!-- Avantages et inconvénients -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages et inconvénients de Java</h2>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Avantages</h4>
                        <pre v-pre><code class="language-text">• Multiplateforme (WORA)
• Grande communauté
• Documentation exhaustive
• Riches bibliothèques
• Performances élevées
• Sécurité robuste
• Évolutivité prouvée
• Support à long terme</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Inconvénients</h4>
                        <pre v-pre><code class="language-text">• Verbosité (beaucoup de code)
• Consommation mémoire
• Temps de démarrage
• Syntaxe complexe
• Courbe d'apprentissage
• Updates fréquentes
• Licensing Oracle</code></pre>
                    </div>
                </div>
            </div>

            <!-- Comparaison avec d'autres langages -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Java vs autres langages</h2>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Java vs Python</h4>
                        <pre v-pre><code class="language-text">Java :
• Typage statique
• Plus rapide
• Plus verbeux
• Meilleur pour les grandes apps

Python :
• Typage dynamique
• Plus lent
• Plus concis
• Meilleur pour le scripting</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Java vs C#</h4>
                        <pre v-pre><code class="language-text">Java :
• Multiplateforme
• Oracle/JVM
• Plus ancien
• Communauté immense

C# :
• Principalement Windows
• Microsoft/.NET
• Syntaxe similaire
• Intégration Windows</code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Java vs JavaScript</h4>
                        <pre v-pre><code class="language-text">Java :
• Langage compilé
• Backend/serveur
• Orienté objet classique
• Fortement typé

JavaScript :
• Langage interprété
• Frontend/navigateur
• Prototypal inheritance
• Faiblement typé</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Java vs C++</h4>
                        <pre v-pre><code class="language-text">Java :
• Garbage collection
• Pas de pointeurs
• Plus sécurisé
• Plus lent (JVM)

C++ :
• Gestion mémoire manuelle
• Pointeurs explicites
• Plus risqué
• Plus rapide (natif)</code></pre>
                    </div>
                </div>
            </div>

            <!-- Bonnes pratiques et conventions -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conventions et bonnes pratiques Java</h2>

                <h3 class="text-purple">Conventions de nommage</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Classes : PascalCase</span>
<span class="java-keyword">public class</span> <span class="java-class">MaClasse</span> {}

<span class="java-comment">// Méthodes/variables : camelCase</span>
<span class="java-keyword">public void</span> <span class="java-function">maMethode</span>() {
    <span class="java-keyword">int</span> <span class="java-variable">maVariable</span> = <span class="java-number">10</span>;
}

<span class="java-comment">// Constantes : UPPER_CASE</span>
<span class="java-keyword">public static final</span> <span class="java-class">String</span> <span class="java-variable">MA_CONSTANTE</span> = <span class="java-string">"VALEUR"</span>;

<span class="java-comment">// Packages : lowercase</span>
<span class="java-keyword">package</span> com.monentreprise.monprojet;</code></pre>
                </div>

                <h3 class="text-purple">Bonnes pratiques</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">• Utiliser l'encapsulation (private + getters/setters)
• Préférer l'héritage aux interfaces
• Éviter les classes trop grandes
• Documenter avec Javadoc
• Gérer les exceptions proprement
• Utiliser les collections génériques
• Éviter les valeurs magiques
• Tester avec JUnit
• Suivre les principes SOLID</code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique : Créer un système de gestion d'étudiants</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Mettre en pratique les concepts Java en créant un système simple de gestion d'étudiants.
                    </p>
                    <ol class="textExemple">
                        <li>Créez une classe <code>Etudiant</code> avec :
                            <ul>
                                <li>Attributs : nom, prénom, numéro étudiant, liste de notes</li>
                                <li>Constructeur avec paramètres</li>
                                <li>Getters et setters</li>
                                <li>Méthode pour ajouter une note</li>
                                <li>Méthode pour calculer la moyenne</li>
                            </ul>
                        </li>
                        <li>Créez une classe <code>Promotion</code> pour gérer plusieurs étudiants</li>
                        <li>Implémentez les fonctionnalités :
                            <ul>
                                <li>Ajouter/supprimer un étudiant</li>
                                <li>Afficher tous les étudiants</li>
                                <li>Trouver l'étudiant avec la meilleure moyenne</li>
                                <li>Calculer la moyenne générale de la promotion</li>
                            </ul>
                        </li>
                        <li>Créez une classe principale avec un menu interactif</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Structure de la solution :</h4>
                        
                        <h5 class="text-purple">Etudiant.java :</h5>
                        <div class="code-example">
                            <pre v-pre><code class="language-java"><span class="java-keyword">import</span> <span class="java-class">java.util.ArrayList</span>;
<span class="java-keyword">import</span> <span class="java-class">java.util.List</span>;

<span class="java-keyword">public class</span> <span class="java-class">Etudiant</span> {
    <span class="java-keyword">private</span> <span class="java-class">String</span> <span class="java-variable">nom</span>;
    <span class="java-keyword">private</span> <span class="java-class">String</span> <span class="java-variable">prenom</span>;
    <span class="java-keyword">private</span> <span class="java-class">String</span> <span class="java-variable">numero</span>;
    <span class="java-keyword">private</span> <span class="java-class">List</span>&lt;<span class="java-class">Double</span>&gt; <span class="java-variable">notes</span>;
    
    <span class="java-keyword">public</span> <span class="java-function">Etudiant</span>(<span class="java-class">String</span> <span class="java-variable">nom</span>, <span class="java-class">String</span> <span class="java-variable">prenom</span>, <span class="java-class">String</span> <span class="java-variable">numero</span>) {
        <span class="java-keyword">this</span>.<span class="java-variable">nom</span> = <span class="java-variable">nom</span>;
        <span class="java-keyword">this</span>.<span class="java-variable">prenom</span> = <span class="java-variable">prenom</span>;
        <span class="java-keyword">this</span>.<span class="java-variable">numero</span> = <span class="java-variable">numero</span>;
        <span class="java-keyword">this</span>.<span class="java-variable">notes</span> = <span class="java-keyword">new</span> <span class="java-class">ArrayList</span>&lt;&gt;();
    }
    
    <span class="java-keyword">public</span> <span class="java-keyword">void</span> <span class="java-function">ajouterNote</span>(<span class="java-keyword">double</span> <span class="java-variable">note</span>) {
        <span class="java-keyword">if</span> (<span class="java-variable">note</span> &gt;= <span class="java-number">0</span> &amp;&amp; <span class="java-variable">note</span> &lt;= <span class="java-number">20</span>) {
            <span class="java-variable">notes</span>.<span class="java-function">add</span>(<span class="java-variable">note</span>);
        }
    }
    
    <span class="java-keyword">public</span> <span class="java-keyword">double</span> <span class="java-function">calculerMoyenne</span>() {
        <span class="java-keyword">if</span> (<span class="java-variable">notes</span>.<span class="java-function">isEmpty</span>()) <span class="java-keyword">return</span> <span class="java-number">0</span>;
        
        <span class="java-keyword">double</span> <span class="java-variable">somme</span> = <span class="java-number">0</span>;
        <span class="java-keyword">for</span> (<span class="java-keyword">double</span> <span class="java-variable">note</span> : <span class="java-variable">notes</span>) {
            <span class="java-variable">somme</span> += <span class="java-variable">note</span>;
        }
        <span class="java-keyword">return</span> <span class="java-variable">somme</span> / <span class="java-variable">notes</span>.<span class="java-function">size</span>();
    }
    
    <span class="java-comment">// Getters et setters...</span>
}</code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources pour apprendre Java</h2>
                <p class="textExemple">
                    Java reste un langage incontournable dans le monde du développement logiciel. 
                    Sa stabilité, sa performance et son vaste écosystème en font un choix judicieux 
                    pour de nombreux types de projets, des applications mobiles aux systèmes d'entreprise complexes.
                </p>

                <h3 class="text-purple">Prochaines étapes dans l'apprentissage :</h3>
                <ul class="textExemple">
                    <li>Maîtriser les collections Java (List, Set, Map)</li>
                    <li>Apprendre les flux (Streams) et expressions lambda</li>
                    <li>Découvrir la programmation concurrente</li>
                    <li>Explorer les frameworks comme Spring</li>
                    <li>Apprendre les tests unitaires avec JUnit</li>
                    <li>Découvrir les design patterns en Java</li>
                </ul>

                <h3 class="text-purple">Ressources recommandées :</h3>
                <ul class="textExemple">
                    <li><a href="https://docs.oracle.com/javase/tutorial/" target="_blank" class="btn-purple btn-hover">Tutoriel officiel Java (Oracle)</a></li>
                    <li><a href="https://www.java.com/fr/" target="_blank" class="btn-purple btn-hover">Site officiel Java</a></li>
                    <li><a href="https://openjdk.org/" target="_blank" class="btn-purple btn-hover">OpenJDK (implémentation open source)</a></li>
                    <li><a href="https://stackoverflow.com/questions/tagged/java" target="_blank" class="btn-purple btn-hover">Stack Overflow - Java</a></li>
                    <li><a href="https://github.com/TheAlgorithms/Java" target="_blank" class="btn-purple btn-hover">Algorithmes en Java (GitHub)</a></li>
                    <li><a href="https://www.baeldung.com/" target="_blank" class="btn-purple btn-hover">Baeldung - Tutoriels Java</a></li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Citation célèbre sur Java</h4>
                    <pre v-pre><code class="language-text">"Java est à C++ ce que C++ est à l'assembleur."
                        - James Gosling, créateur de Java</code></pre>
                </div>

                <p class="textExemple">
                    Avec plus de 25 ans d'existence, Java continue d'évoluer et de s'adapter aux 
                    nouvelles tendances du développement logiciel. Son adoption massive dans 
                    l'industrie garantit qu'il restera un langage pertinent pour les années à venir.
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

.java-marker {
    color: #C586C0 !important; 
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