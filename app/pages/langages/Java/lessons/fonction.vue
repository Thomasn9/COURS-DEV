<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Fonctions (Méthodes) en Java</h1>
                <p class="lesson-meta text-white">Java • Méthodes • Programmation Orientée Objet • JDK 8+</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux fonctions en Java</h2>
                <p class="textExemple">
                    En Java, une fonction est appelée <strong>méthode</strong>. C'est un bloc de code réutilisable qui exécute une tâche spécifique.
                    Les méthodes permettent d'organiser, de structurer et d'éviter la redondance dans un programme.
                </p>
                <p class="textExemple">
                    Une méthode peut recevoir des paramètres, effectuer des traitements et éventuellement retourner une valeur.
                    Toute méthode Java doit être déclarée à l'intérieur d'une classe.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe d'une méthode</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Structure générale</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">[modificateurs] typeRetour nomMéthode([paramètres]) {
    // Corps de la méthode
    // Instructions
    // Optionnel : return valeur;
}</code></pre>
                    </div>
                    <ul>
                        <li><strong>modificateurs</strong> : <code>public</code>, <code>private</code>, <code>static</code>, <code>abstract</code>, etc.</li>
                        <li><strong>typeRetour</strong> : type de la valeur retournée (<code>int</code>, <code>String</code>, <code>void</code> si rien).</li>
                        <li><strong>nomMéthode</strong> : en camelCase, verbe d'action (ex: <code>calculerSomme</code>).</li>
                        <li><strong>paramètres</strong> : liste de variables passées à la méthode, entre parenthèses.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Premier exemple concret</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Exemple {

    // Méthode qui additionne deux entiers et retourne le résultat
    public int additionner(int a, int b) {
        int somme = a + b;
        return somme;
    }

    // Méthode qui affiche un message (void = pas de retour)
    public void afficherBonjour() {
        System.out.println("Bonjour !");
    }

    // Appel des méthodes (dans main par exemple)
    public static void main(String[] args) {
        Exemple ex = new Exemple();
        int resultat = ex.additionner(5, 3);
        System.out.println("Somme : " + resultat); // Somme : 8

        ex.afficherBonjour(); // Bonjour !
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Passage de paramètres -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Passage de paramètres</h2>

                <div class="textExemple">
                    <p>Java utilise toujours le <strong>passage par valeur</strong> :</p>
                    <ul>
                        <li>Pour les types primitifs (<code>int</code>, <code>double</code>, <code>boolean</code>…), une <strong>copie</strong> de la valeur est passée.</li>
                        <li>Pour les objets, la <strong>référence</strong> est copiée, donc l'objet peut être modifié depuis la méthode.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class PassageParametres {

    // Ne modifie PAS la variable originale (primitif)
    public void incrementer(int n) {
        n++;
    }

    // Modifie l'objet (tableau, liste, etc.)
    public void remplirTableau(int[] tab, int valeur) {
        for (int i = 0; i < tab.length; i++) {
            tab[i] = valeur;
        }
    }

    public static void main(String[] args) {
        PassageParametres pp = new PassageParametres();

        int nombre = 10;
        pp.incrementer(nombre);
        System.out.println(nombre); // 10 (inchangé)

        int[] monTableau = new int[3];
        pp.remplirTableau(monTableau, 5);
        System.out.println(Arrays.toString(monTableau)); // [5, 5, 5]
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Surcharge de méthodes (Overloading) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Surcharge de méthodes (Overloading)</h2>

                <div class="textExemple">
                    <p>
                        La surcharge permet de définir plusieurs méthodes avec le <strong>même nom</strong> mais des <strong>paramètres différents</strong>
                        (type, nombre, ordre). Le compilateur choisit la bonne méthode selon les arguments passés.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Surcharge {

    // Version avec deux entiers
    public int multiplier(int a, int b) {
        return a * b;
    }

    // Version avec trois entiers
    public int multiplier(int a, int b, int c) {
        return a * b * c;
    }

    // Version avec deux doubles
    public double multiplier(double a, double b) {
        return a * b;
    }

    public static void main(String[] args) {
        Surcharge s = new Surcharge();
        System.out.println(s.multiplier(2, 3));       // 6
        System.out.println(s.multiplier(2, 3, 4));    // 24
        System.out.println(s.multiplier(2.5, 3.5));   // 8.75
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes statiques vs instance -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes statiques vs méthodes d'instance</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Méthode d'instance</strong> : appartient à une instance de la classe. Nécessite un objet pour être appelée.</li>
                        <li><strong>Méthode statique</strong> : appartient à la classe elle-même. Appelée directement via le nom de la classe.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Calculatrice {

    // Méthode d'instance
    public int carre(int x) {
        return x * x;
    }

    // Méthode statique
    public static int cube(int x) {
        return x * x * x;
    }

    public static void main(String[] args) {
        // Appel statique : pas besoin d'objet
        int resultatCube = Calculatrice.cube(3);
        System.out.println("Cube : " + resultatCube); // Cube : 27

        // Appel d'instance : créer un objet
        Calculatrice calc = new Calculatrice();
        int resultatCarre = calc.carre(5);
        System.out.println("Carré : " + resultatCarre); // Carré : 25
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Récursivité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récursivité</h2>

                <div class="textExemple">
                    <p>
                        Une méthode récursive s'appelle elle-même pour résoudre un problème en le décomposant en sous-problèmes similaires.
                        Il est impératif de définir une <strong>condition d'arrêt</strong> pour éviter une boucle infinie.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Recursivite {

    // Factorielle (n!) avec récursion
    public static long factorielle(int n) {
        if (n <= 1) return 1;        // Condition d'arrêt
        return n * factorielle(n - 1);
    }

    // Suite de Fibonacci
    public static int fibonacci(int n) {
        if (n <= 1) return n;
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    public static void main(String[] args) {
        System.out.println("5! = " + factorielle(5));     // 120
        System.out.println("fib(7) = " + fibonacci(7));   // 13
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Lambda expressions (Java 8+) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Expressions Lambda (Java 8+)</h2>

                <div class="textExemple">
                    <p>
                        Les expressions lambda permettent d'écrire des fonctions anonymes de manière concise.
                        Elles sont souvent utilisées avec les API fonctionnelles (<code>Stream</code>, <code>Comparator</code>, etc.).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">import java.util.*;

public class LambdaDemo {
    public static void main(String[] args) {
        List&lt;String&gt; noms = Arrays.asList("Alice", "Bob", "Charlie");

        // Sans lambda (classe anonyme)
        noms.sort(new Comparator&lt;String&gt;() {
            @Override
            public int compare(String s1, String s2) {
                return s1.length() - s2.length();
            }
        });

        // Avec lambda
        noms.sort((s1, s2) -> s1.length() - s2.length());

        // Parcours avec lambda
        noms.forEach(nom -> System.out.println(nom));

        // Utilisation avec Stream API
        int somme = noms.stream()
                        .mapToInt(String::length)
                        .sum();
        System.out.println("Somme des longueurs : " + somme);
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques pour nommer et concevoir ses méthodes</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Nom explicite</strong> : utilisez un verbe ou une action (ex: <code>calculerMoyenne</code>, <code>envoyerEmail</code>).</li>
                        <li><strong>Single Responsibility</strong> : une méthode doit faire une seule chose, et bien la faire.</li>
                        <li><strong>Longueur raisonnable</strong> : si une méthode dépasse 20-30 lignes, envisagez de la découper.</li>
                        <li><strong>Paramètres limités</strong> : idéalement moins de 4 paramètres. Utilisez un objet si nécessaire.</li>
                        <li><strong>Évitez les effets de bord</strong> : une méthode doit soit modifier un objet, soit retourner une valeur, rarement les deux.</li>
                    </ul>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Maximum de deux nombres</h3>
                    <p>Écrivez une méthode <code>max(int a, int b)</code> qui retourne le plus grand des deux entiers. Testez-la dans un <code>main</code>.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-java">public class Exercice1 {
    public static int max(int a, int b) {
        return (a > b) ? a : b;
    }

    public static void main(String[] args) {
        System.out.println(max(8, 12)); // 12
        System.out.println(max(-3, -7)); // -3
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Factorielle avec récursion</h3>
                    <p>Implémentez une méthode récursive <code>factorielle(int n)</code> et testez-la pour <code>n = 0, 1, 6, 10</code>.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-java">public class Exercice2 {
    public static long factorielle(int n) {
        if (n < 0) throw new IllegalArgumentException("n doit être >= 0");
        return (n == 0) ? 1 : n * factorielle(n - 1);
    }

    public static void main(String[] args) {
        System.out.println("0! = " + factorielle(0)); // 1
        System.out.println("1! = " + factorielle(1)); // 1
        System.out.println("6! = " + factorielle(6)); // 720
        System.out.println("10! = " + factorielle(10)); // 3628800
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Surcharge pour une surface</h3>
                    <p>Créez deux méthodes <code>surface()</code> : une pour un carré (un paramètre côté) et une pour un rectangle (deux paramètres). Calculez et retournez l'aire.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-java">public class Exercice3 {
    public static double surface(double cote) {
        return cote * cote;
    }

    public static double surface(double largeur, double hauteur) {
        return largeur * hauteur;
    }

    public static void main(String[] args) {
        System.out.println("Carré 5 : " + surface(5));          // 25.0
        System.out.println("Rectangle 4x7 : " + surface(4, 7)); // 28.0
    }
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Les méthodes sont le cœur de la programmation Java. Elles permettent de structurer le code,
                        de le rendre réutilisable et plus facile à maintenir. La maîtrise des différents concepts
                        (passage de paramètres, surcharge, récursivité, lambdas) est essentielle pour tout développeur Java.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous aborderons les classes abstraites, les interfaces,
                        les exceptions et la gestion des collections.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaFunctionLesson',

    mounted() {
        // Charger highlight.js + thème VS Code Dark via CDN
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel  = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    // Java est supporté nativement, pas besoin de langage supplémentaire
                    resolve();
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            // Appliquer la coloration sur tous les blocs de code
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
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
    top: 0; left: 0; right: 0; bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
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
    animation: fadeInUp 0.6s ease forwards;
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

.bg-light-purple { background-color: #f8f6ff; }

.border-purple {
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.text-purple { color: #6A3093 !important; }
.text-white  { color: white !important; }

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

.code-example {
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
    width: 100%;
    box-sizing: border-box;
    white-space: pre;
    margin: 0;
}

pre code {
    display: block;
    white-space: pre;
    width: 100%;
}

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
}

.warning-text {
    color: #d63031;
    font-weight: bold;
    margin-top: 0.5rem;
}

.success-text {
    color: #00b894;
    font-weight: bold;
    margin-top: 0.5rem;
}

.exercise { margin: 2rem 0; }
.solution { margin: 1rem 0; }

.solution-content {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #8B5FBF;
}

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

@media (max-width: 768px) {
    .lesson-container  { padding: 1rem; }
    .lesson-header     { padding: 2rem 1rem; }
    .lesson-header h1  { font-size: 2rem; }
    .lesson-section    { padding: 1.5rem; }
    .code-comparison   { grid-template-columns: 1fr; gap: 1rem; }
    pre                { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre               { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section   { padding: 1rem; }
    .lesson-header    { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}
</style>