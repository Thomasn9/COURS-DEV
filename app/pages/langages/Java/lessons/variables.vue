<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Les Variables Primitives en Java</h1>
                <p class="lesson-meta text-white">Comprendre les types fondamentaux et leur utilisation en Java</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux types primitifs</h2>
                <p class="textExemple">
                    En Java, les types primitifs sont les types de données fondamentaux qui représentent 
                    des valeurs simples. Contrairement aux objets, ils sont stockés directement dans la 
                    mémoire stack et non dans le heap. Ils sont plus rapides et utilisent moins de mémoire.
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Caractéristiques des types primitifs</span>
Valeur directe → Pas d'objets → Stack mémoire → Performant → Types fixes</code></pre>
                </div>
            </div>

            <!-- Les 8 types primitifs -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 8 types primitifs de Java</h2>
                
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// 1. Types entiers (signés)</span>
<span class="java-keyword">byte</span>    <span class="java-comment">// 1 octet  : -128 à 127</span>
<span class="java-keyword">short</span>   <span class="java-comment">// 2 octets : -32,768 à 32,767</span>
<span class="java-keyword">int</span>     <span class="java-comment">// 4 octets : -2^31 à 2^31-1 (≈ ±2.1 milliards)</span>
<span class="java-keyword">long</span>    <span class="java-comment">// 8 octets : -2^63 à 2^63-1</span>

<span class="java-comment">// 2. Types à virgule flottante</span>
<span class="java-keyword">float</span>   <span class="java-comment">// 4 octets : simple précision (IEEE 754)</span>
<span class="java-keyword">double</span>  <span class="java-comment">// 8 octets : double précision (IEEE 754)</span>

<span class="java-comment">// 3. Type caractère</span>
<span class="java-keyword">char</span>    <span class="java-comment">// 2 octets : caractère Unicode (0 à 65,535)</span>

<span class="java-comment">// 4. Type booléen</span>
<span class="java-keyword">boolean</span> <span class="java-comment">// 1 bit (mais taille dépend de la JVM)</span></code></pre>
                </div>

                <h3 class="text-purple">Tableau récapitulatif</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Type       Taille    Plage de valeurs                   Valeur par défaut   Exemple
-----      ------    -----------------                   -----------------   -------
byte       1 octet   -128 à 127                          0                   byte b = 100;
short      2 octets  -32,768 à 32,767                    0                   short s = 1000;
int        4 octets  -2,147,483,648 à 2,147,483,647      0                   int i = 100000;
long       8 octets  -9.22×10¹⁸ à 9.22×10¹⁸              0L                  long l = 100000L;
float      4 octets  ≈ ±3.4×10³⁸ (7 chiffres significatifs) 0.0f             float f = 3.14f;
double     8 octets  ≈ ±1.8×10³⁰⁸ (15 chiffres significatifs) 0.0d          double d = 3.14159;
char       2 octets  '\u0000' à '\uffff' (0 à 65,535)    '\u0000' (null)    char c = 'A';
boolean    1 bit*    true ou false                       false               boolean bool = true;

*Note : La taille exacte de boolean dépend de la JVM (souvent 1 octet en pratique)</code></pre>
                </div>
            </div>

            <!-- Déclaration et initialisation -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Déclaration et initialisation</h2>

                <h3 class="text-purple">Déclaration de variables primitives</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-comment">// Déclaration sans initialisation</span>
<span class="java-keyword">int</span> <span class="java-variable">age</span>;
<span class="java-keyword">double</span> <span class="java-variable">price</span>;
<span class="java-keyword">boolean</span> <span class="java-variable">isActive</span>;

<span class="java-comment">// Déclaration avec initialisation</span>
<span class="java-keyword">int</span> <span class="java-variable">count</span> = <span class="java-number">10</span>;
<span class="java-keyword">double</span> <span class="java-variable">temperature</span> = <span class="java-number">23.5</span>;
<span class="java-keyword">char</span> <span class="java-variable">grade</span> = <span class="java-string">'A'</span>;
<span class="java-keyword">boolean</span> <span class="java-variable">isValid</span> = <span class="java-keyword">true</span>;

<span class="java-comment">// Déclaration multiple</span>
<span class="java-keyword">int</span> <span class="java-variable">x</span> = <span class="java-number">1</span>, <span class="java-variable">y</span> = <span class="java-number">2</span>, <span class="java-variable">z</span> = <span class="java-number">3</span>;
<span class="java-keyword">double</span> <span class="java-variable">pi</span> = <span class="java-number">3.14159</span>, <span class="java-variable">e</span> = <span class="java-number">2.71828</span>;</code></pre>
                </div>

                <h3 class="text-purple">Valeurs par défaut (dans les classes)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">ExempleValeurs</span> {
    <span class="java-comment">// Variables d'instance - ont des valeurs par défaut</span>
    <span class="java-keyword">byte</span> <span class="java-variable">b</span>;      <span class="java-comment">// 0</span>
    <span class="java-keyword">short</span> <span class="java-variable">s</span>;     <span class="java-comment">// 0</span>
    <span class="java-keyword">int</span> <span class="java-variable">i</span>;       <span class="java-comment">// 0</span>
    <span class="java-keyword">long</span> <span class="java-variable">l</span>;      <span class="java-comment">// 0L</span>
    <span class="java-keyword">float</span> <span class="java-variable">f</span>;     <span class="java-comment">// 0.0f</span>
    <span class="java-keyword">double</span> <span class="java-variable">d</span>;    <span class="java-comment">// 0.0d</span>
    <span class="java-keyword">char</span> <span class="java-variable">c</span>;      <span class="java-comment">// '\u0000' (caractère null)</span>
    <span class="java-keyword">boolean</span> <span class="java-variable">bool</span>; <span class="java-comment">// false</span>
    
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Variables locales - DOIVENT être initialisées avant utilisation</span>
        <span class="java-keyword">int</span> <span class="java-variable">localVar</span>;  <span class="java-comment">// ERREUR si utilisé sans initialisation</span>
        <span class="java-comment">// System.out.println(localVar); // Erreur de compilation</span>
        
        <span class="java-variable">localVar</span> = <span class="java-number">10</span>;  <span class="java-comment">// OK après initialisation</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-variable">localVar</span>);
    }
}</code></pre>
                </div>
            </div>

            <!-- Les types entiers -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les types entiers (byte, short, int, long)</h2>

                <h3 class="text-purple">Utilisation et limites</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">TypesEntiers</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// byte - pour les petites valeurs</span>
        <span class="java-keyword">byte</span> <span class="java-variable">age</span> = <span class="java-number">25</span>;
        <span class="java-keyword">byte</span> <span class="java-variable">temperature</span> = -<span class="java-number">10</span>;
        <span class="java-comment">// byte erreur = 200; // ERREUR : dépasse 127</span>
        
        <span class="java-comment">// short - valeurs moyennes</span>
        <span class="java-keyword">short</span> <span class="java-variable">populationVillage</span> = <span class="java-number">1500</span>;
        <span class="java-keyword">short</span> <span class="java-variable">score</span> = <span class="java-number">32000</span>;
        
        <span class="java-comment">// int - le type entier par défaut</span>
        <span class="java-keyword">int</span> <span class="java-variable">populationFrance</span> = <span class="java-number">67_000_000</span>;  <span class="java-comment">// Underscores pour lisibilité</span>
        <span class="java-keyword">int</span> <span class="java-variable">distanceTerreLune</span> = <span class="java-number">384_400_000</span>; <span class="java-comment">// en mètres</span>
        
        <span class="java-comment">// long - pour les très grandes valeurs</span>
        <span class="java-keyword">long</span> <span class="java-variable">populationMondiale</span> = <span class="java-number">7_900_000_000L</span>;  <span class="java-comment">// Notez le 'L'</span>
        <span class="java-keyword">long</span> <span class="java-variable">distanceLightYear</span> = <span class="java-number">9_461_000_000_000_000L</span>; <span class="java-comment">// en mètres</span>
        
        <span class="java-comment">// Affichage des valeurs</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Age: "</span> + <span class="java-variable">age</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Population France: "</span> + <span class="java-variable">populationFrance</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Population Mondiale: "</span> + <span class="java-variable">populationMondiale</span>);
        
        <span class="java-comment">// Valeurs limites</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Byte MAX: "</span> + <span class="java-class">Byte</span>.<span class="java-variable">MAX_VALUE</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Byte MIN: "</span> + <span class="java-class">Byte</span>.<span class="java-variable">MIN_VALUE</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Integer MAX: "</span> + <span class="java-class">Integer</span>.<span class="java-variable">MAX_VALUE</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Long MAX: "</span> + <span class="java-class">Long</span>.<span class="java-variable">MAX_VALUE</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Notations littérales pour les entiers</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">int</span> <span class="java-variable">decimal</span> = <span class="java-number">100</span>;        <span class="java-comment">// Décimal (base 10)</span>
<span class="java-keyword">int</span> <span class="java-variable">hex</span> = <span class="java-number">0xFF</span>;           <span class="java-comment">// Hexadécimal (base 16) - 255 en décimal</span>
<span class="java-keyword">int</span> <span class="java-variable">binary</span> = <span class="java-number">0b1100100</span>;    <span class="java-comment">// Binaire (base 2) - 100 en décimal</span>
<span class="java-keyword">int</span> <span class="java-variable">octal</span> = <span class="java-number">0144</span>;          <span class="java-comment">// Octal (base 8) - 100 en décimal</span>

<span class="java-keyword">long</span> <span class="java-variable">bigNumber</span> = <span class="java-number">1_000_000_000L</span>;      <span class="java-comment">// Avec underscore</span>
<span class="java-keyword">long</span> <span class="java-variable">creditCard</span> = <span class="java-number">1234_5678_9012_3456L</span>;</code></pre>
                </div>
            </div>

            <!-- Les types à virgule flottante -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les types à virgule flottante (float, double)</h2>

                <h3 class="text-purple">Précision et utilisation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">TypesFlottants</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// float - simple précision (suffixe 'f' ou 'F' obligatoire)</span>
        <span class="java-keyword">float</span> <span class="java-variable">piFloat</span> = <span class="java-number">3.14159f</span>;
        <span class="java-keyword">float</span> <span class="java-variable">temperatureFloat</span> = <span class="java-number">23.5f</span>;
        <span class="java-keyword">float</span> <span class="java-variable">grandNombreFloat</span> = <span class="java-number">1.23456789f</span>; <span class="java-comment">// Perte de précision</span>
        
        <span class="java-comment">// double - double précision (type par défaut pour les littéraux)</span>
        <span class="java-keyword">double</span> <span class="java-variable">piDouble</span> = <span class="java-number">3.141592653589793</span>;
        <span class="java-keyword">double</span> <span class="java-variable">temperatureDouble</span> = <span class="java-number">23.5</span>; <span class="java-comment">// Pas besoin de suffixe</span>
        <span class="java-keyword">double</span> <span class="java-variable">grandNombreDouble</span> = <span class="java-number">1.234567890123456</span>;
        
        <span class="java-comment">// Notation scientifique</span>
        <span class="java-keyword">double</span> <span class="java-variable">vitesseLumiere</span> = <span class="java-number">2.99792458e8</span>;  <span class="java-comment">// 299,792,458 m/s</span>
        <span class="java-keyword">double</span> <span class="java-variable">chargeElectron</span> = <span class="java-number">1.602176634e-19</span>; <span class="java-comment">// Coulomb</span>
        
        <span class="java-comment">// Affichage - problème de précision avec float</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Float: "</span> + <span class="java-variable">grandNombreFloat</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Double: "</span> + <span class="java-variable">grandNombreDouble</span>);
        
        <span class="java-comment">// Comparaison de précision</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"Float pi: %.15f%n"</span>, <span class="java-variable">piFloat</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"Double pi: %.15f%n"</span>, <span class="java-variable">piDouble</span>);
        
        <span class="java-comment">// Valeurs spéciales</span>
        <span class="java-keyword">double</span> <span class="java-variable">infiniPositif</span> = <span class="java-class">Double</span>.<span class="java-variable">POSITIVE_INFINITY</span>;
        <span class="java-keyword">double</span> <span class="java-variable">infiniNegatif</span> = <span class="java-class">Double</span>.<span class="java-variable">NEGATIVE_INFINITY</span>;
        <span class="java-keyword">double</span> <span class="java-variable">nan</span> = <span class="java-class">Double</span>.<span class="java-variable">NaN</span>;  <span class="java-comment">// Not a Number</span>
        
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Infini positif: "</span> + <span class="java-variable">infiniPositif</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"NaN: "</span> + <span class="java-variable">nan</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Problèmes de précision des nombres flottants</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">ProblemePrecision</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Problème classique avec les nombres à virgule flottante</span>
        <span class="java-keyword">double</span> <span class="java-variable">resultat</span> = <span class="java-number">0.1</span> + <span class="java-number">0.2</span>;
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"0.1 + 0.2 = "</span> + <span class="java-variable">resultat</span>); <span class="java-comment">// 0.30000000000000004</span>
        
        <span class="java-comment">// Comparaison problématique</span>
        <span class="java-keyword">if</span> (<span class="java-variable">resultat</span> == <span class="java-number">0.3</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Égal !"</span>);
        } <span class="java-keyword">else</span> {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Pas égal !"</span>);  <span class="java-comment">// Ceci s'affiche</span>
        }
        
        <span class="java-comment">// Solution : utiliser une marge d'erreur (epsilon)</span>
        <span class="java-keyword">double</span> <span class="java-variable">epsilon</span> = <span class="java-number">0.000001</span>;
        <span class="java-keyword">if</span> (<span class="java-class">Math</span>.<span class="java-function">abs</span>(<span class="java-variable">resultat</span> - <span class="java-number">0.3</span>) &lt; <span class="java-variable">epsilon</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Assez proche !"</span>);
        }
        
        <span class="java-comment">// Pour les calculs financiers, utiliser BigDecimal</span>
        <span class="java-comment">// java.math.BigDecimal prix = new BigDecimal("0.1");</span>
    }
}</code></pre>
                </div>
            </div>

            <!-- Le type char -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le type char</h2>

                <h3 class="text-purple">Caractères Unicode</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">TypeChar</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Différentes façons de déclarer des caractères</span>
        <span class="java-keyword">char</span> <span class="java-variable">lettre</span> = <span class="java-string">'A'</span>;          <span class="java-comment">// Caractère simple</span>
        <span class="java-keyword">char</span> <span class="java-variable">chiffre</span> = <span class="java-string">'7'</span>;         <span class="java-comment">// Chiffre comme caractère</span>
        <span class="java-keyword">char</span> <span class="java-variable">symbole</span> = <span class="java-string">'$'</span>;         <span class="java-comment">// Symbole</span>
        <span class="java-keyword">char</span> <span class="java-variable">espace</span> = <span class="java-string">' '</span>;          <span class="java-comment">// Espace</span>
        <span class="java-keyword">char</span> <span class="java-variable">tabulation</span> = <span class="java-string">'\t'</span>;      <span class="java-comment">// Caractère d'échappement</span>
        <span class="java-keyword">char</span> <span class="java-variable">nouvelleLigne</span> = <span class="java-string">'\n'</span>;   <span class="java-comment">// Nouvelle ligne</span>
        
        <span class="java-comment">// Caractères Unicode</span>
        <span class="java-keyword">char</span> <span class="java-variable">alpha</span> = <span class="java-string">'\u03B1'</span>;      <span class="java-comment">// Lettre grecque alpha</span>
        <span class="java-keyword">char</span> <span class="java-variable">coeur</span> = <span class="java-string">'\u2764'</span>;       <span class="java-comment">// Symbole cœur</span>
        <span class="java-keyword">char</span> <span class="java-variable">euro</span> = <span class="java-string">'\u20AC'</span>;       <span class="java-comment">// Symbole euro</span>
        
        <span class="java-comment">// Code numérique d'un caractère</span>
        <span class="java-keyword">char</span> <span class="java-variable">b</span> = <span class="java-string">'B'</span>;
        <span class="java-keyword">int</span> <span class="java-variable">codeB</span> = (<span class="java-keyword">int</span>) <span class="java-variable">b</span>;        <span class="java-comment">// Cast en int - donne 66</span>
        <span class="java-keyword">char</span> <span class="java-variable">cFromCode</span> = (<span class="java-keyword">char</span>) <span class="java-number">67</span>;  <span class="java-comment">// Cast d'int vers char - donne 'C'</span>
        
        <span class="java-comment">// Affichage</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Lettre: "</span> + <span class="java-variable">lettre</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Alpha grec: "</span> + <span class="java-variable">alpha</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Cœur: "</span> + <span class="java-variable">coeur</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Code de B: "</span> + <span class="java-variable">codeB</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Caractère du code 67: "</span> + <span class="java-variable">cFromCode</span>);
        
        <span class="java-comment">// Caractères d'échappement courants</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Backslash: \\"</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Guillemet double: \""</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Guillemet simple: '"</span>);  <span class="java-comment">// Pas besoin d'échappement ici</span>
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Caractères d'échappement</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Séquence  Description           Valeur Unicode
--------  -------------------   --------------
\n        Nouvelle ligne        \u000A
\t        Tabulation            \u0009
\b        Backspace             \u0008
\r        Retour chariot        \u000D
\f        Saut de page          \u000C
\\        Backslash             \u005C
\'        Guillemet simple      \u0027
\"        Guillemet double      \u0022
\ddd      Caractère octal       (ddd)
\uxxxx    Caractère Unicode     (xxxx en hex)</code></pre>
                </div>
            </div>

            <!-- Le type boolean -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le type boolean</h2>

                <h3 class="text-purple">Valeurs booléennes</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">TypeBoolean</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Déclaration de variables booléennes</span>
        <span class="java-keyword">boolean</span> <span class="java-variable">estVrai</span> = <span class="java-keyword">true</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">estFaux</span> = <span class="java-keyword">false</span>;
        
        <span class="java-comment">// Expressions booléennes</span>
        <span class="java-keyword">int</span> <span class="java-variable">age</span> = <span class="java-number">25</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">estMajeur</span> = <span class="java-variable">age</span> &gt;= <span class="java-number">18</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">estJeune</span> = <span class="java-variable">age</span> &lt; <span class="java-number">30</span>;
        
        <span class="java-keyword">double</span> <span class="java-variable">temperature</span> = <span class="java-number">22.5</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">estAgreable</span> = <span class="java-variable">temperature</span> &gt; <span class="java-number">20.0</span> &amp;&amp; <span class="java-variable">temperature</span> &lt; <span class="java-number">25.0</span>;
        
        <span class="java-comment">// Opérateurs logiques</span>
        <span class="java-keyword">boolean</span> <span class="java-variable">resultat1</span> = <span class="java-keyword">true</span> &amp;&amp; <span class="java-keyword">false</span>;   <span class="java-comment">// ET logique → false</span>
        <span class="java-keyword">boolean</span> <span class="java-variable">resultat2</span> = <span class="java-keyword">true</span> || <span class="java-keyword">false</span>;   <span class="java-comment">// OU logique → true</span>
        <span class="java-keyword">boolean</span> <span class="java-variable">resultat3</span> = !<span class="java-keyword">true</span>;           <span class="java-comment">// NON logique → false</span>
        
        <span class="java-comment">// Affichage</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Est majeur: "</span> + <span class="java-variable">estMajeur</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Est jeune: "</span> + <span class="java-variable">estJeune</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Température agréable: "</span> + <span class="java-variable">estAgreable</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"true && false: "</span> + <span class="java-variable">resultat1</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"!true: "</span> + <span class="java-variable">resultat3</span>);
        
        <span class="java-comment">// Utilisation dans les conditions</span>
        <span class="java-keyword">if</span> (<span class="java-variable">estMajeur</span> &amp;&amp; <span class="java-variable">estJeune</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Personne majeure et jeune"</span>);
        }
        
        <span class="java-comment">// IMPORTANT : Java est strictement typé pour les booléens</span>
        <span class="java-comment">// boolean erreur = 0; // ERREUR : pas de conversion automatique int → boolean</span>
        <span class="java-comment">// boolean erreur = "true"; // ERREUR : pas de conversion String → boolean</span>
        
        <span class="java-comment">// Comparaison de booléens</span>
        <span class="java-keyword">boolean</span> <span class="java-variable">a</span> = <span class="java-keyword">true</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">b</span> = <span class="java-keyword">false</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">c</span> = <span class="java-keyword">true</span>;
        
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"a == b: "</span> + (<span class="java-variable">a</span> == <span class="java-variable">b</span>));      <span class="java-comment">// false</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"a == c: "</span> + (<span class="java-variable">a</span> == <span class="java-variable">c</span>));      <span class="java-comment">// true</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"a != b: "</span> + (<span class="java-variable">a</span> != <span class="java-variable">b</span>));      <span class="java-comment">// true</span>
    }
}</code></pre>
                </div>
            </div>

            <!-- Conversions et casting -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conversions et casting de types</h2>

                <h3 class="text-purple">Casting explicite</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">CastingTypes</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Casting de types numériques</span>
        
        <span class="java-comment">// 1. Casting rétrécissant (narrowing) - nécessite un cast explicite</span>
        <span class="java-keyword">int</span> <span class="java-variable">grandNombre</span> = <span class="java-number">1000</span>;
        <span class="java-keyword">byte</span> <span class="java-variable">petitNombre</span> = (<span class="java-keyword">byte</span>) <span class="java-variable">grandNombre</span>;  <span class="java-comment">// Cast explicite</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"int 1000 → byte: "</span> + <span class="java-variable">petitNombre</span>); <span class="java-comment">// Perte d'information !</span>
        
        <span class="java-keyword">double</span> <span class="java-variable">d</span> = <span class="java-number">3.14159</span>;
        <span class="java-keyword">int</span> <span class="java-variable">i</span> = (<span class="java-keyword">int</span>) <span class="java-variable">d</span>;  <span class="java-comment">// Cast double → int (troncature)</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"double 3.14159 → int: "</span> + <span class="java-variable">i</span>); <span class="java-comment">// 3</span>
        
        <span class="java-comment">// 2. Casting élargissant (widening) - automatique</span>
        <span class="java-keyword">byte</span> <span class="java-variable">b</span> = <span class="java-number">100</span>;
        <span class="java-keyword">int</span> <span class="java-variable">i2</span> = <span class="java-variable">b</span>;  <span class="java-comment">// Pas besoin de cast</span>
        <span class="java-keyword">float</span> <span class="java-variable">f</span> = <span class="java-variable">i2</span>; <span class="java-comment">// Pas besoin de cast</span>
        
        <span class="java-comment">// 3. Casting entre char et int</span>
        <span class="java-keyword">char</span> <span class="java-variable">c</span> = <span class="java-string">'A'</span>;
        <span class="java-keyword">int</span> <span class="java-variable">codeAscii</span> = <span class="java-variable">c</span>;  <span class="java-comment">// Automatique (widening)</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Code ASCII de A: "</span> + <span class="java-variable">codeAscii</span>);
        
        <span class="java-keyword">int</span> <span class="java-variable">code</span> = <span class="java-number">66</span>;
        <span class="java-keyword">char</span> <span class="java-variable">c2</span> = (<span class="java-keyword">char</span>) <span class="java-variable">code</span>;  <span class="java-comment">// Nécessite un cast (narrowing)</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Caractère du code 66: "</span> + <span class="java-variable">c2</span>);
        
        <span class="java-comment">// 4. Attention aux overflow/underflow</span>
        <span class="java-keyword">int</span> <span class="java-variable">maxInt</span> = <span class="java-class">Integer</span>.<span class="java-variable">MAX_VALUE</span>;
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Max int: "</span> + <span class="java-variable">maxInt</span>);
        
        <span class="java-keyword">long</span> <span class="java-variable">l</span> = <span class="java-variable">maxInt</span> + <span class="java-number">1L</span>;  <span class="java-comment">// OK avec promotion</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"maxInt + 1 (en long): "</span> + <span class="java-variable">l</span>);
        
        <span class="java-keyword">int</span> <span class="java-variable">overflow</span> = <span class="java-variable">maxInt</span> + <span class="java-number">1</span>;  <span class="java-comment">// Overflow !</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"maxInt + 1 (en int): "</span> + <span class="java-variable">overflow</span>); <span class="java-comment">// Valeur négative</span>
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Hiérarchie des conversions automatiques</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">byte → short → int → long → float → double
                      ↑
                     char

Règles :
1. Conversion automatique vers un type plus large (widening)
2. Conversion vers un type plus étroit nécessite un cast explicite (narrowing)
3. Les conversions peuvent causer une perte de précision
4. boolean ne peut pas être converti vers/depuis d'autres types</code></pre>
                </div>
            </div>

            <!-- Les Wrapper Classes -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les Wrapper Classes (classes enveloppes)</h2>

                <h3 class="text-purple">Autoboxing et unboxing</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">WrapperClasses</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Correspondance primitif → wrapper</span>
        <span class="java-comment">// byte    → Byte</span>
        <span class="java-comment">// short   → Short</span>
        <span class="java-comment">// int     → Integer</span>
        <span class="java-comment">// long    → Long</span>
        <span class="java-comment">// float   → Float</span>
        <span class="java-comment">// double  → Double</span>
        <span class="java-comment">// char    → Character</span>
        <span class="java-comment">// boolean → Boolean</span>
        
        <span class="java-comment">// Avant Java 5 - conversion manuelle</span>
        <span class="java-keyword">int</span> <span class="java-variable">primitive</span> = <span class="java-number">42</span>;
        <span class="java-class">Integer</span> <span class="java-variable">wrapper</span> = <span class="java-class">Integer</span>.<span class="java-function">valueOf</span>(<span class="java-variable">primitive</span>); <span class="java-comment">// Boxing</span>
        <span class="java-keyword">int</span> <span class="java-variable">unboxed</span> = <span class="java-variable">wrapper</span>.<span class="java-function">intValue</span>();           <span class="java-comment">// Unboxing</span>
        
        <span class="java-comment">// Depuis Java 5 - autoboxing/autounboxing automatique</span>
        <span class="java-class">Integer</span> <span class="java-variable">autoBoxed</span> = <span class="java-number">42</span>;        <span class="java-comment">// Autoboxing</span>
        <span class="java-keyword">int</span> <span class="java-variable">autoUnboxed</span> = <span class="java-variable">autoBoxed</span>;  <span class="java-comment">// Autounboxing</span>
        
        <span class="java-comment">// Méthodes utilitaires des wrappers</span>
        <span class="java-class">String</span> <span class="java-variable">nombreStr</span> = <span class="java-string">"123"</span>;
        <span class="java-keyword">int</span> <span class="java-variable">nombre</span> = <span class="java-class">Integer</span>.<span class="java-function">parseInt</span>(<span class="java-variable">nombreStr</span>);
        <span class="java-class">String</span> <span class="java-variable">resultatStr</span> = <span class="java-class">Integer</span>.<span class="java-function">toString</span>(<span class="java-variable">nombre</span>);
        
        <span class="java-comment">// Valeurs limites et constantes</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Max int: "</span> + <span class="java-class">Integer</span>.<span class="java-variable">MAX_VALUE</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Taille d'un int (bits): "</span> + <span class="java-class">Integer</span>.<span class="java-variable">SIZE</span>);
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Taille d'un int (octets): "</span> + <span class="java-class">Integer</span>.<span class="java-variable">BYTES</span>);
        
        <span class="java-comment">// Comparaison des wrappers</span>
        <span class="java-class">Integer</span> <span class="java-variable">a</span> = <span class="java-number">100</span>;
        <span class="java-class">Integer</span> <span class="java-variable">b</span> = <span class="java-number">100</span>;
        <span class="java-class">Integer</span> <span class="java-variable">c</span> = <span class="java-number">200</span>;
        <span class="java-class">Integer</span> <span class="java-variable">d</span> = <span class="java-number">200</span>;
        
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"a == b (100): "</span> + (<span class="java-variable">a</span> == <span class="java-variable">b</span>));      <span class="java-comment">// true (cache -128 à 127)</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"c == d (200): "</span> + (<span class="java-variable">c</span> == <span class="java-variable">d</span>));      <span class="java-comment">// false (pas dans le cache)</span>
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"c.equals(d): "</span> + <span class="java-variable">c</span>.<span class="java-function">equals</span>(<span class="java-variable">d</span>)); <span class="java-comment">// true</span>
        
        <span class="java-comment">// Utiliser equals() pour comparer des wrappers !</span>
    }
}</code></pre>
                </div>
            </div>

            <!-- Bonnes pratiques -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec les types primitifs</h2>

                <h3 class="text-purple">Recommandations</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">1. Choix du type approprié :
   • Utiliser int pour la plupart des entiers
   • Utiliser double pour la plupart des nombres à virgule
   • Utiliser long pour les très grands entiers
   • Éviter float sauf pour économiser de la mémoire (graphiques, gros tableaux)

2. Performance et mémoire :
   • byte/short pour économiser la mémoire dans les grands tableaux
   • Privilégier les primitifs aux wrappers pour la performance
   • Attention à l'autoboxing dans les boucles

3. Précision numérique :
   • Utiliser BigDecimal pour les calculs financiers
   • Comparer les doubles avec une marge d'erreur (epsilon)
   • Attention aux overflow/underflow

4. Lisibilité :
   • Utiliser les underscores dans les grands nombres (1_000_000)
   • Nommer les variables de manière explicite
   • Initialiser les variables locales avant utilisation

5. Sécurité :
   • Vérifier les limites avant les conversions (narrowing)
   • Valider les entrées utilisateur avant conversion
   • Utiliser les méthodes parseXxx() avec gestion d'exceptions</code></pre>
                </div>

                <h3 class="text-purple">Exemple de code robuste</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">BonnesPratiques</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// 1. Initialisation explicite</span>
        <span class="java-keyword">int</span> <span class="java-variable">compteur</span> = <span class="java-number">0</span>;
        <span class="java-keyword">double</span> <span class="java-variable">total</span> = <span class="java-number">0.0</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">estTermine</span> = <span class="java-keyword">false</span>;
        
        <span class="java-comment">// 2. Noms explicites</span>
        <span class="java-keyword">int</span> <span class="java-variable">nombreArticles</span> = <span class="java-number">10</span>;
        <span class="java-keyword">double</span> <span class="java-variable">prixUnitaire</span> = <span class="java-number">19.99</span>;
        <span class="java-keyword">boolean</span> <span class="java-variable">estEnStock</span> = <span class="java-keyword">true</span>;
        
        <span class="java-comment">// 3. Conversions sécurisées</span>
        <span class="java-class">String</span> <span class="java-variable">input</span> = <span class="java-string">"123"</span>;
        <span class="java-keyword">try</span> {
            <span class="java-keyword">int</span> <span class="java-variable">valeur</span> = <span class="java-class">Integer</span>.<span class="java-function">parseInt</span>(<span class="java-variable">input</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Valeur convertie: "</span> + <span class="java-variable">valeur</span>);
        } <span class="java-keyword">catch</span> (<span class="java-class">NumberFormatException</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur de conversion"</span>);
        }
        
        <span class="java-comment">// 4. Comparaison de doubles avec epsilon</span>
        <span class="java-keyword">double</span> <span class="java-variable">a</span> = <span class="java-number">0.1</span> + <span class="java-number">0.2</span>;
        <span class="java-keyword">double</span> <span class="java-variable">b</span> = <span class="java-number">0.3</span>;
        <span class="java-keyword">double</span> <span class="java-variable">epsilon</span> = <span class="java-number">0.000001</span>;
        
        <span class="java-keyword">if</span> (<span class="java-class">Math</span>.<span class="java-function">abs</span>(<span class="java-variable">a</span> - <span class="java-variable">b</span>) &lt; <span class="java-variable">epsilon</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Les nombres sont égaux avec la marge d'erreur"</span>);
        }
        
        <span class="java-comment">// 5. Gestion des overflow</span>
        <span class="java-keyword">int</span> <span class="java-variable">max</span> = <span class="java-class">Integer</span>.<span class="java-variable">MAX_VALUE</span>;
        <span class="java-keyword">try</span> {
            <span class="java-keyword">int</span> <span class="java-variable">result</span> = <span class="java-class">Math</span>.<span class="java-function">addExact</span>(<span class="java-variable">max</span>, <span class="java-number">1</span>);
        } <span class="java-keyword">catch</span> (<span class="java-class">ArithmeticException</span> <span class="java-variable">e</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Overflow détecté !"</span>);
        }
    }
}</code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique : Gestionnaire de conversions</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer un programme qui démontre la maîtrise des types primitifs Java.
                    </p>
                    <ol class="textExemple">
                        <li>Créez un programme qui :
                            <ul>
                                <li>Déclare et initialise un exemple de chaque type primitif</li>
                                <li>Effectue des conversions entre différents types (avec et sans casting)</li>
                                <li>Montre les problèmes de précision avec les nombres flottants</li>
                                <li>Démontre l'autoboxing et l'unboxing</li>
                                <li>Calcule et affiche les valeurs limites de chaque type</li>
                            </ul>
                        </li>
                        <li>Implémentez des fonctions utilitaires :
                            <ul>
                                <li>Une fonction qui convertit Celsius en Fahrenheit (double)</li>
                                <li>Une fonction qui calcule l'IMC (Indice de Masse Corporelle)</li>
                                <li>Une fonction qui convertit un caractère en son code ASCII et vice versa</li>
                                <li>Une fonction qui vérifie si un nombre est pair (boolean)</li>
                            </ul>
                        </li>
                        <li>Testez les cas limites et les erreurs potentielles</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Exemple de solution :</h4>
                        
                        <h5 class="text-purple">PrimitiveManager.java :</h5>
                        <div class="code-example">
                            <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">PrimitiveManager</span> {
    
    <span class="java-comment">// Conversion Celsius → Fahrenheit</span>
    <span class="java-keyword">public static double</span> <span class="java-function">celsiusToFahrenheit</span>(<span class="java-keyword">double</span> <span class="java-variable">celsius</span>) {
        <span class="java-keyword">return</span> (<span class="java-variable">celsius</span> * <span class="java-number">9</span>/<span class="java-number">5</span>) + <span class="java-number">32</span>;
    }
    
    <span class="java-comment">// Calcul IMC</span>
    <span class="java-keyword">public static double</span> <span class="java-function">calculerIMC</span>(<span class="java-keyword">double</span> <span class="java-variable">poids</span>, <span class="java-keyword">double</span> <span class="java-variable">taille</span>) {
        <span class="java-keyword">return</span> <span class="java-variable">poids</span> / (<span class="java-variable">taille</span> * <span class="java-variable">taille</span>);
    }
    
    <span class="java-comment">// Caractère → Code ASCII</span>
    <span class="java-keyword">public static int</span> <span class="java-function">charToAscii</span>(<span class="java-keyword">char</span> <span class="java-variable">c</span>) {
        <span class="java-keyword">return</span> (<span class="java-keyword">int</span>) <span class="java-variable">c</span>;
    }
    
    <span class="java-comment">// Code ASCII → Caractère</span>
    <span class="java-keyword">public static char</span> <span class="java-function">asciiToChar</span>(<span class="java-keyword">int</span> <span class="java-variable">code</span>) {
        <span class="java-comment">// Vérification des limites</span>
        <span class="java-keyword">if</span> (<span class="java-variable">code</span> &lt; <span class="java-number">0</span> || <span class="java-variable">code</span> &gt; <span class="java-number">65535</span>) {
            <span class="java-keyword">throw new</span> <span class="java-class">IllegalArgumentException</span>(<span class="java-string">"Code ASCII invalide"</span>);
        }
        <span class="java-keyword">return</span> (<span class="java-keyword">char</span>) <span class="java-variable">code</span>;
    }
    
    <span class="java-comment">// Vérifier si un nombre est pair</span>
    <span class="java-keyword">public static boolean</span> <span class="java-function">estPair</span>(<span class="java-keyword">int</span> <span class="java-variable">nombre</span>) {
        <span class="java-keyword">return</span> <span class="java-variable">nombre</span> % <span class="java-number">2</span> == <span class="java-number">0</span>;
    }
    
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-comment">// Exemples de démonstration...</span>
    }
}</code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>
                <p class="textExemple">
                    Les types primitifs sont les briques fondamentales de Java. Leur compréhension 
                    est essentielle pour écrire du code efficace, performant et correct. 
                    Chaque type a ses spécificités, ses limites et ses cas d'utilisation optimaux.
                </p>

                <h3 class="text-purple">Points clés à retenir :</h3>
                <ul class="textExemple">
                    <li>Java a 8 types primitifs : byte, short, int, long, float, double, char, boolean</li>
                    <li>Les primitifs sont stockés dans la stack, pas dans le heap (performance)</li>
                    <li>int et double sont les types par défaut pour les entiers et nombres à virgule</li>
                    <li>Les conversions élargissantes sont automatiques, les conversions rétrécissantes nécessitent un cast</li>
                    <li>Les nombres flottants ont des problèmes de précision (utiliser BigDecimal pour la finance)</li>
                    <li>Les wrapper classes permettent d'utiliser les primitifs comme des objets</li>
                </ul>

                <h3 class="text-purple">Ressources pour aller plus loin :</h3>
                <ul class="textExemple">
                    <li><a href="https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html" target="_blank" class="btn-purple btn-hover">Documentation officielle Oracle sur les types de données</a></li>
                    <li><a href="https://docs.oracle.com/javase/specs/jls/se17/html/jls-4.html" target="_blank" class="btn-purple btn-hover">Java Language Specification - Types, Values, and Variables</a></li>
                    <li><a href="https://www.baeldung.com/java-primitives" target="_blank" class="btn-purple btn-hover">Baeldung - Guide des primitifs Java</a></li>
                    <li><a href="https://javarevisited.blogspot.com/2012/01/difference-between-type-casting-and.html" target="_blank" class="btn-purple btn-hover">Différence entre casting et conversion</a></li>
                    <li><a href="https://www.geeksforgeeks.org/data-types-in-java/" target="_blank" class="btn-purple btn-hover">GeeksforGeeks - Types de données en Java</a></li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Résumé final</h4>
                    <pre v-pre><code class="language-java"><span class="java-comment">// Les primitifs en un coup d'œil :</span>
<span class="java-comment">// Pour les performances et la mémoire : utiliser les primitifs</span>
<span class="java-comment">// Pour la flexibilité et les collections : utiliser les wrappers</span>
<span class="java-comment">// Toujours choisir le type le plus approprié au contexte</span>
<span class="java-comment">// Valider les conversions et gérer les exceptions</span>
<span class="java-comment">// Tester les cas limites et les problèmes de précision</span></code></pre>
                </div>

                <p class="textExemple">
                    La maîtrise des types primitifs est une compétence fondamentale en Java. 
                    Elle permet d'écrire du code plus performant, plus sûr et plus lisible. 
                    Prenez le temps de comprendre les nuances de chaque type et leurs implications 
                    sur la performance et la précision de vos programmes.
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'PrimitiveVariablesLesson'
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