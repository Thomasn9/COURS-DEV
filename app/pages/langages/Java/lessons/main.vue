<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">La Méthode main en Java</h1>
                <p class="lesson-meta text-white">Le point d'entrée de toute application Java</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à la méthode main</h2>
                <p class="textExemple">
                    La méthode <code>main</code> est le point d'entrée de toute application Java exécutable.
                    C'est la première méthode appelée par la JVM (Java Virtual Machine) lorsqu'un programme Java démarre.
                    Sans une méthode <code>main</code> correctement définie, une application Java ne peut pas être exécutée.
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Rôle de la méthode main</span>
Point d'entrée → Premier appel JVM → Lancement programme → Gestion arguments</code></pre>
                </div>
            </div>

            <!-- Syntaxe de base -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de base de la méthode main</h2>
                
                <h3 class="text-purple">La signature obligatoire</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">MaClasse</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Code de votre application</span>
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Analyse détaillée de chaque mot-clé</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// public - Modificateur d'accès</span>
<span class="java-comment">// • La JVM doit pouvoir appeler cette méthode de l'extérieur</span>
<span class="java-comment">// • Sans 'public', la JVM ne pourrait pas y accéder</span>

<span class="java-comment">// static - Méthode de classe</span>
<span class="java-comment">// • Appartient à la classe, pas à une instance</span>
<span class="java-comment">// • La JVM peut l'appeler sans créer d'objet</span>
<span class="java-comment">// • Exécutée avant toute instanciation</span>

<span class="java-comment">// void - Type de retour</span>
<span class="java-comment">// • Ne retourne aucune valeur</span>
<span class="java-comment">// • La JVM ne s'attend pas à un retour</span>
<span class="java-comment">// • Termine avec System.exit() si besoin</span>

<span class="java-comment">// main - Nom de la méthode</span>
<span class="java-comment">// • Nom conventionnel et obligatoire</span>
<span class="java-comment">// • La JVM recherche spécifiquement ce nom</span>
<span class="java-comment">// • Respecter la casse (minuscule)</span>

<span class="java-comment">// (String[] args) - Paramètres</span>
<span class="java-comment">// • Tableau de chaînes pour les arguments</span>
<span class="java-comment">// • 'args' est le nom conventionnel (peut être changé)</span>
<span class="java-comment">// • Contient les arguments passés en ligne de commande</span></code></pre>
                </div>
            </div>

            <!-- Exemples complets -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples complets de méthode main</h2>

                <h3 class="text-purple">Exemple 1 : Programme "Hello World" classique</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// HelloWorld.java</span>
<span class="java-keyword">public class</span> <span class="java-class">HelloWorld</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Hello, World!"</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Exemple 2 : Programme avec utilisation des arguments</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Welcome.java</span>
<span class="java-keyword">public class</span> <span class="java-class">Welcome</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> &gt; <span class="java-number">0</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Bonjour, "</span> + <span class="java-variable">args</span>[<span class="java-number">0</span>] + <span class="java-string">"!"</span>);
        } <span class="java-keyword">else</span> {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Bonjour, monde !"</span>);
        }
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Exemple 3 : Programme avec plusieurs arguments</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Calculator.java - Addition simple</span>
<span class="java-keyword">public class</span> <span class="java-class">Calculator</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> != <span class="java-number">2</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Usage: java Calculator &lt;nombre1&gt; &lt;nombre2&gt;"</span>);
            <span class="java-keyword">return</span>;
        }
        
        <span class="java-keyword">try</span> {
            <span class="java-keyword">double</span> <span class="java-variable">num1</span> = <span class="java-class">Double</span>.<span class="java-function">parseDouble</span>(<span class="java-variable">args</span>[<span class="java-number">0</span>]);
            <span class="java-keyword">double</span> <span class="java-variable">num2</span> = <span class="java-class">Double</span>.<span class="java-function">parseDouble</span>(<span class="java-variable">args</span>[<span class="java-number">1</span>]);
            <span class="java-keyword">double</span> <span class="java-variable">sum</span> = <span class="java-variable">num1</span> + <span class="java-variable">num2</span>;
            
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"%.2f + %.2f = %.2f%n"</span>, <span class="java-variable">num1</span>, <span class="java-variable">num2</span>, <span class="java-variable">sum</span>);
        } <span class="java-keyword">catch</span> (<span class="java-class">NumberFormatException</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : Veuillez entrer des nombres valides."</span>);
        }
    }
}</code></pre>
                </div>
            </div>

            <!-- Variantes de la méthode main -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Variantes syntaxiques de la méthode main</h2>

                <h3 class="text-purple">Variantes valides (Java 5 et +)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// 1. Syntaxe classique (la plus utilisée)</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) { }

<span class="java-comment">// 2. Varargs (Java 5+) - équivalent à String[] args</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>... <span class="java-variable">args</span>) { }

<span class="java-comment">// 3. Avec final sur les paramètres</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-keyword">final</span> <span class="java-class">String</span>[] <span class="java-variable">args</span>) { }

<span class="java-comment">// 4. Avec final et varargs</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-keyword">final</span> <span class="java-class">String</span>... <span class="java-variable">args</span>) { }

<span class="java-comment">// 5. Nom de paramètre différent (args est une convention)</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">arguments</span>) { }
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">argv</span>) { }  <span class="java-comment">// Style C</span></code></pre>
                </div>

                <h3 class="text-purple">Variantes invalides (ne fonctionneront pas)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// 1. Sans public - erreur de compilation</span>
<span class="java-keyword">static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) { }  <span class="java-comment">// Erreur : pas public</span>

<span class="java-comment">// 2. Sans static - erreur d'exécution</span>
<span class="java-keyword">public void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) { }    <span class="java-comment">// Erreur : pas static</span>

<span class="java-comment">// 3. Avec retour différent de void</span>
<span class="java-keyword">public static int</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) { <span class="java-keyword">return</span> <span class="java-number">0</span>; }  <span class="java-comment">// Erreur : doit être void</span>

<span class="java-comment">// 4. Paramètres incorrects</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>() { }                    <span class="java-comment">// Erreur : pas de paramètres</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-keyword">int</span>[] <span class="java-variable">args</span>) { }       <span class="java-comment">// Erreur : doit être String[]</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span> <span class="java-variable">args</span>) { }       <span class="java-comment">// Erreur : doit être tableau</span></code></pre>
                </div>
            </div>

            <!-- Utilisation des arguments -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation des arguments de la ligne de commande</h2>

                <h3 class="text-purple">Accès aux arguments</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">ArgumentDemo</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Nombre d'arguments</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Nombre d'arguments : "</span> + <span class="java-variable">args</span>.<span class="java-variable">length</span>);
        
        <span class="java-comment">// Afficher tous les arguments</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Arguments reçus :"</span>);
        <span class="java-keyword">for</span> (<span class="java-keyword">int</span> <span class="java-variable">i</span> = <span class="java-number">0</span>; <span class="java-variable">i</span> &lt; <span class="java-variable">args</span>.<span class="java-variable">length</span>; <span class="java-variable">i</span>++) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"  args[%d] = %s%n"</span>, <span class="java-variable">i</span>, <span class="java-variable">args</span>[<span class="java-variable">i</span>]);
        }
        
        <span class="java-comment">// Boucle for-each (Java 5+)</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"\nAvec for-each :"</span>);
        <span class="java-keyword">for</span> (<span class="java-class">String</span> <span class="java-variable">arg</span> : <span class="java-variable">args</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"  - "</span> + <span class="java-variable">arg</span>);
        }
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Exécution avec arguments</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Compilation</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac ArgumentDemo.java</span>

<span class="bash-comment"># Exécution sans arguments</span>
<span class="bash-prompt">$</span> <span class="bash-command">java ArgumentDemo</span>
Nombre d'arguments : 0
Arguments reçus :

<span class="bash-comment"># Exécution avec arguments</span>
<span class="bash-prompt">$</span> <span class="bash-command">java ArgumentDemo Java est super</span>
Nombre d'arguments : 3
Arguments reçus :
  args[0] = Java
  args[1] = est
  args[2] = super

<span class="bash-comment"># Exécution avec arguments contenant des espaces</span>
<span class="bash-prompt">$</span> <span class="bash-command">java ArgumentDemo "Hello World" "Java Programming"</span>
Nombre d'arguments : 2
Arguments reçus :
  args[0] = Hello World
  args[1] = Java Programming</code></pre>
                </div>

                <h3 class="text-purple">Programme avec gestion avancée des arguments</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">AdvancedArgs</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Vérifier le nombre d'arguments</span>
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> == <span class="java-number">0</span>) {
            <span class="java-function">afficherAide</span>();
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">1</span>);  <span class="java-comment">// Quitter avec code d'erreur</span>
        }
        
        <span class="java-comment">// Traiter les arguments</span>
        <span class="java-class">String</span> <span class="java-variable">commande</span> = <span class="java-variable">args</span>[<span class="java-number">0</span>];
        
        <span class="java-keyword">switch</span> (<span class="java-variable">commande</span>.<span class="java-function">toLowerCase</span>()) {
            <span class="java-keyword">case</span> <span class="java-string">"add"</span>:
                <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> != <span class="java-number">3</span>) {
                    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Usage: add &lt;num1&gt; &lt;num2&gt;"</span>);
                    <span class="java-keyword">break</span>;
                }
                <span class="java-keyword">try</span> {
                    <span class="java-keyword">double</span> <span class="java-variable">a</span> = <span class="java-class">Double</span>.<span class="java-function">parseDouble</span>(<span class="java-variable">args</span>[<span class="java-number">1</span>]);
                    <span class="java-keyword">double</span> <span class="java-variable">b</span> = <span class="java-class">Double</span>.<span class="java-function">parseDouble</span>(<span class="java-variable">args</span>[<span class="java-number">2</span>]);
                    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"%.2f + %.2f = %.2f%n"</span>, <span class="java-variable">a</span>, <span class="java-variable">b</span>, <span class="java-variable">a</span> + <span class="java-variable">b</span>);
                } <span class="java-keyword">catch</span> (<span class="java-class">NumberFormatException</span> <span class="java-variable">e</span>) {
                    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : arguments invalides"</span>);
                }
                <span class="java-keyword">break</span>;
                
            <span class="java-keyword">case</span> <span class="java-string">"help"</span>:
                <span class="java-function">afficherAide</span>();
                <span class="java-keyword">break</span>;
                
            <span class="java-keyword">default</span>:
                <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Commande inconnue: "</span> + <span class="java-variable">commande</span>);
                <span class="java-function">afficherAide</span>();
        }
    }
    
    <span class="java-keyword">private static void</span> <span class="java-function">afficherAide</span>() {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Usage: java AdvancedArgs &lt;commande&gt; [arguments]"</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Commandes disponibles:"</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"  add &lt;num1&gt; &lt;num2&gt;  - Additionne deux nombres"</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"  help              - Affiche cette aide"</span>);
    }
}</code></pre>
                </div>
            </div>

            <!-- Méthode main dans plusieurs classes -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode main dans plusieurs classes</h2>

                <h3 class="text-purple">Possibilité d'avoir plusieurs méthodes main</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Fichier 1 : App1.java</span>
<span class="java-keyword">public class</span> <span class="java-class">App1</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Application 1 démarrée"</span>);
    }
}

<span class="java-comment">// Fichier 2 : App2.java</span>
<span class="java-keyword">public class</span> <span class="java-class">App2</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Application 2 démarrée"</span>);
    }
}

<span class="java-comment">// Fichier 3 : ClasseAvecMainInterne.java</span>
<span class="java-keyword">public class</span> <span class="java-class">ClasseAvecMainInterne</span> {
    
    <span class="java-comment">// Méthode main principale</span>
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Main principale"</span>);
        
        <span class="java-comment">// Appeler une autre méthode main (comme méthode normale)</span>
        <span class="java-class">String</span>[] <span class="java-variable">testArgs</span> = {<span class="java-string">"test"</span>, <span class="java-string">"123"</span>};
        <span class="java-function">mainSecondaire</span>(<span class="java-variable">testArgs</span>);
    }
    
    <span class="java-comment">// Autre méthode avec la signature de main (mais pas le point d'entrée)</span>
    <span class="java-keyword">public static void</span> <span class="java-function">mainSecondaire</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Main secondaire appelée avec "</span> + <span class="java-variable">args</span>.<span class="java-variable">length</span> + <span class="java-string">" arguments"</span>);
    }
    
    <span class="java-comment">// Encore une autre méthode qui ressemble à main</span>
    <span class="java-keyword">static void</span> <span class="java-function">main</span>(<span class="java-keyword">int</span> <span class="java-variable">numero</span>) {  <span class="java-comment">// Surcharge - paramètres différents</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Méthode main surchargée : "</span> + <span class="java-variable">numero</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Comment choisir quelle méthode main exécuter</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Compilation</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac App1.java App2.java ClasseAvecMainInterne.java</span>

<span class="bash-comment"># Exécution - spécifier la classe contenant le main à exécuter</span>
<span class="bash-prompt">$</span> <span class="bash-command">java App1</span>
Application 1 démarrée

<span class="bash-prompt">$</span> <span class="bash-command">java App2</span>
Application 2 démarrée

<span class="bash-prompt">$</span> <span class="bash-command">java ClasseAvecMainInterne</span>
Main principale
Main secondaire appelée avec 2 arguments

<span class="bash-comment"># Erreur si on essaie d'exécuter une classe sans main valide</span>
<span class="bash-prompt">$</span> <span class="bash-command">java ClasseSansMain</span>
Erreur : méthode principale introuvable dans la classe ClasseSansMain</code></pre>
                </div>
            </div>

            <!-- Retour et codes de sortie -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Codes de sortie et terminaison du programme</h2>

                <h3 class="text-purple">Utilisation de System.exit()</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">ExitDemo</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Vérifier les arguments</span>
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> == <span class="java-number">0</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Aucun argument fourni."</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Code de sortie : 1 (erreur)"</span>);
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">1</span>);  <span class="java-comment">// Termine avec code d'erreur</span>
        }
        
        <span class="java-comment">// Traitement normal</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Argument reçu : "</span> + <span class="java-variable">args</span>[<span class="java-number">0</span>]);
        
        <span class="java-comment">// Essayer de convertir en nombre</span>
        <span class="java-keyword">try</span> {
            <span class="java-keyword">int</span> <span class="java-variable">nombre</span> = <span class="java-class">Integer</span>.<span class="java-function">parseInt</span>(<span class="java-variable">args</span>[<span class="java-number">0</span>]);
            
            <span class="java-keyword">if</span> (<span class="java-variable">nombre</span> &lt; <span class="java-number">0</span>) {
                <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Nombre négatif non accepté."</span>);
                <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">2</span>);  <span class="java-comment">// Code d'erreur personnalisé</span>
            }
            
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Traitement réussi."</span>);
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">0</span>);  <span class="java-comment">// Succès (optionnel - terminera automatiquement)</span>
            
        } <span class="java-keyword">catch</span> (<span class="java-class">NumberFormatException</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : argument non numérique."</span>);
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">3</span>);  <span class="java-comment">// Code d'erreur pour format invalide</span>
        }
        
        <span class="java-comment">// Ce code ne sera jamais exécuté à cause des System.exit()</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Ce message ne s'affichera jamais."</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Codes de sortie standards</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Code  Signification                   Convention
----  -----------------------------  -----------
0     Succès                         Programme terminé normalement
1     Erreur générale                Erreur non spécifiée
2     Mauvaise utilisation           Arguments incorrects
126   Commande invoquée impossible   Problème de permissions
127   Commande non trouvée           Programme non trouvé
130   Terminé par signal (Ctrl+C)    Interruption utilisateur
255   Code de sortie hors limites    > 255 ramené à 255 (mod 256)

Conventions courantes dans les scripts :
• 0 = succès
• 1-127 = erreurs définies par le programme
• 128-255 = erreurs système</code></pre>
                </div>

                <h3 class="text-purple">Vérification du code de sortie</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Compilation et exécution</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac ExitDemo.java</span>

<span class="bash-comment"># Tester différents cas</span>
<span class="bash-prompt">$</span> <span class="bash-command">java ExitDemo 42</span>
Argument reçu : 42
Traitement réussi.

<span class="bash-prompt">$</span> <span class="bash-command">echo $?</span>  <span class="bash-comment"># Affiche le code de sortie du dernier programme</span>
0

<span class="bash-prompt">$</span> <span class="bash-command">java ExitDemo -5</span>
Argument reçu : -5
Nombre négatif non accepté.

<span class="bash-prompt">$</span> <span class="bash-command">echo $?</span>
2

<span class="bash-prompt">$</span> <span class="bash-command">java ExitDemo abc</span>
Argument reçu : abc
Erreur : argument non numérique.

<span class="bash-prompt">$</span> <span class="bash-command">echo $?</span>
3

<span class="bash-prompt">$</span> <span class="bash-command">java ExitDemo</span>
Aucun argument fourni.
Code de sortie : 1 (erreur)

<span class="bash-prompt">$</span> <span class="bash-command">echo $?</span>
1</code></pre>
                </div>
            </div>

            <!-- Bonnes pratiques -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques pour la méthode main</h2>

                <h3 class="text-purple">Recommandations</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">1. Garder main() concise :
   • main() devrait principalement orchestrer le programme
   • Déléguer la logique à d'autres méthodes/classes
   • Éviter les méthodes main() trop longues (> 50 lignes)

2. Gestion des erreurs :
   • Toujours valider les arguments
   • Gérer les exceptions appropriées
   • Fournir des messages d'erreur clairs
   • Utiliser des codes de sortie significatifs

3. Structure recommandée :
   • Validation des arguments
   • Initialisation des ressources
   • Appel à la logique principale
   • Gestion des exceptions
   • Nettoyage des ressources
   • Code de sortie approprié

4. Documentation :
   • Documenter les arguments attendus
   • Indiquer les codes de sortie
   • Fournir des exemples d'utilisation
   • Utiliser des commentaires Javadoc

5. Testabilité :
   • Faciliter les tests unitaires
   • Séparer la logique de main()
   • Utiliser des méthodes statiques testables
   • Éviter les effets de bord globaux</code></pre>
                </div>

                <h3 class="text-purple">Exemple de bonne implémentation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">/**
 * Programme de calculatrice simple.
 * Usage: java Calculatrice &lt;opération&gt; &lt;nombre1&gt; &lt;nombre2&gt;
 * 
 * Opérations supportées : add, sub, mul, div
 * 
 * Codes de sortie :
 *   0 - Succès
 *   1 - Arguments incorrects
 *   2 - Division par zéro
 *   3 - Opération inconnue
 */</span>
<span class="java-keyword">public class</span> <span class="java-class">Calculatrice</span> {
    
    <span class="java-comment">/**
     * Point d'entrée du programme.
     * @param args Arguments de la ligne de commande
     */</span>
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">try</span> {
            <span class="java-comment">// Validation des arguments</span>
            <span class="java-keyword">if</span> (!<span class="java-function">validerArguments</span>(<span class="java-variable">args</span>)) {
                <span class="java-function">afficherAide</span>();
                <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">1</span>);
            }
            
            <span class="java-comment">// Extraction des arguments</span>
            <span class="java-class">String</span> <span class="java-variable">operation</span> = <span class="java-variable">args</span>[<span class="java-number">0</span>];
            <span class="java-keyword">double</span> <span class="java-variable">nombre1</span> = <span class="java-class">Double</span>.<span class="java-function">parseDouble</span>(<span class="java-variable">args</span>[<span class="java-number">1</span>]);
            <span class="java-keyword">double</span> <span class="java-variable">nombre2</span> = <span class="java-class">Double</span>.<span class="java-function">parseDouble</span>(<span class="java-variable">args</span>[<span class="java-number">2</span>]);
            
            <span class="java-comment">// Exécution du calcul</span>
            <span class="java-keyword">double</span> <span class="java-variable">resultat</span> = <span class="java-function">executerOperation</span>(<span class="java-variable">operation</span>, <span class="java-variable">nombre1</span>, <span class="java-variable">nombre2</span>);
            
            <span class="java-comment">// Affichage du résultat</span>
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"Résultat : %.2f%n"</span>, <span class="java-variable">resultat</span>);
            
        } <span class="java-keyword">catch</span> (<span class="java-class">ArithmeticException</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : "</span> + <span class="java-variable">e</span>.<span class="java-function">getMessage</span>());
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">2</span>);
        } <span class="java-keyword">catch</span> (<span class="java-class">IllegalArgumentException</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : "</span> + <span class="java-variable">e</span>.<span class="java-function">getMessage</span>());
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">3</span>);
        }
        <span class="java-comment">// Succès - pas besoin de System.exit(0) explicite</span>
    }
    
    <span class="java-keyword">private static boolean</span> <span class="java-function">validerArguments</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">return</span> <span class="java-variable">args</span>.<span class="java-variable">length</span> == <span class="java-number">3</span>;
    }
    
    <span class="java-keyword">private static void</span> <span class="java-function">afficherAide</span>() {
        <span class="java-comment">// ... affichage de l'aide ...</span>
    }
    
    <span class="java-keyword">private static double</span> <span class="java-function">executerOperation</span>(<span class="java-class">String</span> <span class="java-variable">operation</span>, <span class="java-keyword">double</span> <span class="java-variable">a</span>, <span class="java-keyword">double</span> <span class="java-variable">b</span>) {
        <span class="java-comment">// ... logique de calcul ...</span>
        <span class="java-keyword">return</span> <span class="java-number">0</span>;  <span class="java-comment">// simplifié pour l'exemple</span>
    }
}</code></pre>
                </div>
            </div>

            <!-- Cas spéciaux et pièges -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas spéciaux et pièges courants</h2>

                <h3 class="text-purple">Problèmes fréquents</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// 1. Oubli du mot-clé static</span>
<span class="java-keyword">public class</span> <span class="java-class">ErreurStatic</span> {
    <span class="java-keyword">public void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {  <span class="java-comment">// ERREUR : manque static</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Ceci ne fonctionnera pas"</span>);
    }
}

<span class="java-comment">// 2. Mauvais type de paramètre</span>
<span class="java-keyword">public class</span> <span class="java-class">ErreurParametre</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-keyword">int</span>[] <span class="java-variable">args</span>) {  <span class="java-comment">// ERREUR : doit être String[]</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Ceci ne fonctionnera pas"</span>);
    }
}

<span class="java-comment">// 3. Classe publique dans un fichier de nom différent</span>
<span class="java-comment">// Fichier : AutreNom.java</span>
<span class="java-keyword">public class</span> <span class="java-class">MonProgramme</span> {  <span class="java-comment">// ERREUR : nom de fichier doit être MonProgramme.java</span>
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Ceci compile mais pose problème"</span>);
    }
}

<span class="java-comment">// 4. Arguments passés comme un seul string</span>
<span class="java-keyword">public class</span> <span class="java-class">ProblemeArguments</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> &gt; <span class="java-number">0</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Premier argument : "</span> + <span class="java-variable">args</span>[<span class="java-number">0</span>]);
            <span class="java-comment">// Si appelé avec : java ProblemeArguments "a b c"</span>
            <span class="java-comment">// args[0] contiendra "a b c" (un seul argument)</span>
            <span class="java-comment">// Si appelé avec : java ProblemeArguments a b c</span>
            <span class="java-comment">// args[0] = "a", args[1] = "b", args[2] = "c"</span>
        }
    }
}

<span class="java-comment">// 5. Problème d'encodage des arguments</span>
<span class="java-keyword">public class</span> <span class="java-class">ProblemeEncodage</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">for</span> (<span class="java-class">String</span> <span class="java-variable">arg</span> : <span class="java-variable">args</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Argument: "</span> + <span class="java-variable">arg</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Longueur: "</span> + <span class="java-variable">arg</span>.<span class="java-function">length</span>());
            <span class="java-comment">// Les caractères spéciaux peuvent poser problème selon l'OS et le terminal</span>
        }
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Solutions aux problèmes courants</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// 1. Utiliser un constructeur si besoin d'instanciation</span>
<span class="java-keyword">public class</span> <span class="java-class">SolutionInstanciation</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Créer une instance si besoin</span>
        <span class="java-class">SolutionInstanciation</span> <span class="java-variable">programme</span> = <span class="java-keyword">new</span> <span class="java-class">SolutionInstanciation</span>();
        <span class="java-variable">programme</span>.<span class="java-function">demarrer</span>(<span class="java-variable">args</span>);
    }
    
    <span class="java-keyword">public void</span> <span class="java-function">demarrer</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Logique du programme ici</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Programme démarré"</span>);
    }
}

<span class="java-comment">// 2. Gérer les arguments avec des guillemets</span>
<span class="java-keyword">public class</span> <span class="java-class">SolutionGuillemets</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Pour traiter "John Doe" comme un seul argument :</span>
        <span class="java-comment">// java SolutionGuillemets "John Doe"</span>
        <span class="java-comment">// args[0] = "John Doe"</span>
        
        <span class="java-comment">// Pour traiter John et Doe comme deux arguments séparés :</span>
        <span class="java-comment">// java SolutionGuillemets John Doe</span>
        <span class="java-comment">// args[0] = "John", args[1] = "Doe"</span>
        
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> &gt; <span class="java-number">0</span>) {
            <span class="java-class">String</span> <span class="java-variable">nomComplet</span> = <span class="java-class">String</span>.<span class="java-function">join</span>(<span class="java-string">" "</span>, <span class="java-variable">args</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Bonjour, "</span> + <span class="java-variable">nomComplet</span>);
        }
    }
}</code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique : Créer un gestionnaire de tâches en ligne de commande</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer une application Java complète avec une méthode main robuste qui gère des arguments complexes.
                    </p>
                    <ol class="textExemple">
                        <li>Créez un programme <code>TaskManager</code> qui supporte les commandes :
                            <ul>
                                <li><code>add "Description de la tâche"</code> - Ajoute une nouvelle tâche</li>
                                <li><code>list</code> - Affiche toutes les tâches</li>
                                <li><code>complete &lt;id&gt;</code> - Marque une tâche comme complétée</li>
                                <li><code>remove &lt;id&gt;</code> - Supprime une tâche</li>
                                <li><code>help</code> - Affiche l'aide</li>
                            </ul>
                        </li>
                        <li>Implémentez les fonctionnalités :
                            <ul>
                                <li>Validation des arguments</li>
                                <li>Gestion des erreurs avec codes de sortie appropriés</li>
                                <li>Messages d'erreur clairs en français</li>
                                <li>Documentation Javadoc pour la méthode main</li>
                                <li>Structure modulaire (séparation de la logique)</li>
                            </ul>
                        </li>
                        <li>Testez avec différents cas :
                            <ul>
                                <li>Arguments manquants ou incorrects</li>
                                <li>Commandes inconnues</li>
                                <li>IDs invalides</li>
                                <li>Chaînes vides ou avec espaces</li>
                            </ul>
                        </li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la structure de solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Structure de base :</h4>
                        
                        <h5 class="text-purple">TaskManager.java :</h5>
                        <div class="code-example">
                            <pre v-pre><code class="language-java"><span class="java-comment">/**
 * Gestionnaire de tâches en ligne de commande.
 * Usage: java TaskManager &lt;commande&gt; [arguments]
 * 
 * Commandes disponibles:
 *   add "description"  - Ajoute une nouvelle tâche
 *   list               - Liste toutes les tâches
 *   complete &lt;id&gt;      - Marque une tâche comme terminée
 *   remove &lt;id&gt;        - Supprime une tâche
 *   help               - Affiche cette aide
 * 
 * Codes de sortie:
 *   0 - Succès
 *   1 - Arguments invalides
 *   2 - Commande inconnue
 *   3 - ID de tâche invalide
 *   4 - Erreur d'E/S (fichier)
 */</span>
<span class="java-keyword">public class</span> <span class="java-class">TaskManager</span> {
    
    <span class="java-keyword">private static final</span> <span class="java-class">List</span>&lt;<span class="java-class">String</span>&gt; <span class="java-variable">taches</span> = <span class="java-keyword">new</span> <span class="java-class">ArrayList</span>&lt;&gt;();
    
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-keyword">if</span> (<span class="java-variable">args</span>.<span class="java-variable">length</span> == <span class="java-number">0</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : aucune commande spécifiée."</span>);
            <span class="java-function">afficherAide</span>();
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">1</span>);
        }
        
        <span class="java-class">String</span> <span class="java-variable">commande</span> = <span class="java-variable">args</span>[<span class="java-number">0</span>];
        
        <span class="java-keyword">try</span> {
            <span class="java-keyword">switch</span> (<span class="java-variable">commande</span>) {
                <span class="java-keyword">case</span> <span class="java-string">"add"</span>:
                    <span class="java-function">gererAjout</span>(<span class="java-variable">args</span>);
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-string">"list"</span>:
                    <span class="java-function">afficherTaches</span>();
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-string">"complete"</span>:
                    <span class="java-function">gererCompletion</span>(<span class="java-variable">args</span>);
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-string">"remove"</span>:
                    <span class="java-function">gererSuppression</span>(<span class="java-variable">args</span>);
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-string">"help"</span>:
                    <span class="java-function">afficherAide</span>();
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">default</span>:
                    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : commande inconnue '"</span> + <span class="java-variable">commande</span> + <span class="java-string">"'"</span>);
                    <span class="java-function">afficherAide</span>();
                    <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">2</span>);
            }
        } <span class="java-keyword">catch</span> (<span class="java-class">Exception</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : "</span> + <span class="java-variable">e</span>.<span class="java-function">getMessage</span>());
            <span class="java-class">System</span>.<span class="java-variable">exit</span>(<span class="java-number">3</span>);
        }
    }
    
    <span class="java-comment">// Méthodes auxiliaires...</span>
}</code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>
                <p class="textExemple">
                    La méthode <code>main</code> est le cœur de toute application Java autonome. 
                    Sa compréhension est essentielle pour créer des programmes robustes, 
                    bien structurés et faciles à utiliser en ligne de commande.
                </p>

                <h3 class="text-purple">Points clés à retenir :</h3>
                <ul class="textExemple">
                    <li>Signature obligatoire : <code>public static void main(String[] args)</code></li>
                    <li>C'est le point d'entrée unique de la JVM</li>
                    <li>Les arguments sont passés via le tableau <code>args</code></li>
                    <li>Plusieurs classes peuvent avoir une méthode <code>main</code>, mais une seule est exécutée</li>
                    <li>Utiliser <code>System.exit(code)</code> pour contrôler le code de sortie</li>
                    <li>Toujours valider et documenter les arguments attendus</li>
                </ul>

                <h3 class="text-purple">Ressources pour aller plus loin :</h3>
                <ul class="textExemple">
                    <li><a href="https://docs.oracle.com/javase/tutorial/getStarted/application/index.html" target="_blank" class="btn-purple btn-hover">Documentation officielle Oracle sur les applications Java</a></li>
                    <li><a href="https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html" target="_blank" class="btn-purple btn-hover">Options de la ligne de commande java</a></li>
                    <li><a href="https://www.baeldung.com/java-main-method" target="_blank" class="btn-purple btn-hover">Baeldung - Guide complet de la méthode main</a></li>
                    <li><a href="https://www.javatpoint.com/main-method-in-java" target="_blank" class="btn-purple btn-hover">JavaTpoint - Méthode main en Java</a></li>
                    <li><a href="https://github.com/jline/jline3" target="_blank" class="btn-purple btn-hover">JLine - Bibliothèque pour interfaces ligne de commande avancées</a></li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Résumé en une ligne</h4>
                    <pre v-pre><code class="language-java"><span class="java-comment">// Sans cette méthode, point de salut pour votre application Java autonome !</span>
<span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) { }</code></pre>
                </div>

                <p class="textExemple">
                    La méthode <code>main</code> peut sembler simple, mais une bonne maîtrise 
                    de ses subtilités fait la différence entre un programme amateur et 
                    une application professionnelle. Prenez le temps de bien structurer 
                    votre méthode <code>main</code> et de gérer proprement les arguments 
                    et les erreurs.
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaMainMethodLesson'
}
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