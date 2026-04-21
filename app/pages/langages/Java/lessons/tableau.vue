<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les tableaux en Java</h1>
                <p class="lesson-meta text-white">Java • Tableaux • Collections • Algorithmique</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux tableaux</h2>
                <p class="textExemple">
                    Un tableau est une structure de données qui permet de stocker plusieurs valeurs du même type dans une seule variable.
                    Chaque élément est accessible via un index (entier) commençant à <strong>0</strong>.
                </p>
                <p class="textExemple">
                    Les tableaux en Java sont des objets, ils ont une taille fixe définie à la création. Ils peuvent contenir des types primitifs
                    (int, double, boolean, etc.) ou des références vers des objets.
                </p>
            </section>

            <!-- Déclaration et création -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Déclaration et création</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxes de déclaration</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Déclaration d'un tableau d'entiers
int[] nombres;          // Style recommandé
int nombres2[];         // Style C (déconseillé)

// Déclaration d'un tableau de chaînes
String[] mots;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Création d'un tableau (allocation mémoire)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Tableau de 5 entiers (valeurs par défaut : 0)
int[] nombres = new int[5];

// Tableau de 10 chaînes (valeurs par défaut : null)
String[] mots = new String[10];

// Création + initialisation directe
int[] premiers = {2, 3, 5, 7, 11};
String[] couleurs = {"rouge", "vert", "bleu"};

// Avec new et initialisation
int[] valeurs = new int[]{10, 20, 30};</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Taille d'un tableau</h3>
                    <p>La propriété <code>length</code> donne la taille (nombre d'éléments) :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] tab = new int[8];
System.out.println(tab.length); // Affiche 8</code></pre>
                    </div>
                </div>
            </section>

            <!-- Accès et modification -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Accès et modification des éléments</h2>
                <div class="textExemple">
                    <p>On utilise l'index entre crochets :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] notes = {12, 15, 8, 19};
// Accès
int premiereNote = notes[0];     // 12
int derniereNote = notes[3];     // 19

// Modification
notes[1] = 16;   // le tableau devient {12, 16, 8, 19}</code></pre>
                    </div>
                    <div class="warning-section">
                        <p class="warning-text">
                            ⚠️ Attention : l'index doit être compris entre 0 et length-1. Un index hors limites provoque une <code>ArrayIndexOutOfBoundsException</code>.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Parcours d'un tableau -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Parcourir un tableau</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Boucle for classique</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] nombres = {10, 20, 30, 40};
for (int i = 0; i &lt; nombres.length; i++) {
    System.out.println(nombres[i]);
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Boucle for-each (améliorée)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] nombres = {10, 20, 30, 40};
for (int valeur : nombres) {
    System.out.println(valeur);
}
// Ne permet pas de modifier le tableau (car copie de la valeur)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Tableaux d'objets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Tableaux d'objets</h2>
                <div class="textExemple">
                    <p>Un tableau d'objets contient des <strong>références</strong>. Chaque élément doit être instancié individuellement.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Tableau de 3 objets Personne (classe hypothétique)
Personne[] annuaire = new Personne[3];
annuaire[0] = new Personne("Alice");
annuaire[1] = new Personne("Bob");
annuaire[2] = new Personne("Charlie");

// Accès aux méthodes
annuaire[0].afficher();</code></pre>
                    </div>
                </div>
            </section>

            <!-- Tableaux multidimensionnels -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Tableaux multidimensionnels</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Tableau 2D (matrice)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Déclaration et création
int[][] matrice = new int[3][4]; // 3 lignes, 4 colonnes

// Initialisation directe
int[][] grille = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accès
int valeur = grille[1][2]; // 6 (ligne 1, colonne 2)

// Parcours
for (int i = 0; i &lt; grille.length; i++) {
    for (int j = 0; j &lt; grille[i].length; j++) {
        System.out.print(grille[i][j] + " ");
    }
    System.out.println();
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Tableau irrégulier (jagged array)</h3>
                    <p>Chaque ligne peut avoir une longueur différente.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[][] triangle = new int[4][];
triangle[0] = new int[1];
triangle[1] = new int[2];
triangle[2] = new int[3];
triangle[3] = new int[4];

// Remplir le triangle de Pascal par exemple</code></pre>
                    </div>
                </div>
            </section>

            <!-- Opérations courantes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Opérations courantes sur les tableaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Copie de tableau</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] original = {1, 2, 3, 4, 5};

// Méthode 1 : boucle
int[] copie1 = new int[original.length];
for (int i = 0; i &lt; original.length; i++) {
    copie1[i] = original[i];
}

// Méthode 2 : System.arraycopy()
int[] copie2 = new int[original.length];
System.arraycopy(original, 0, copie2, 0, original.length);

// Méthode 3 : Arrays.copyOf()
int[] copie3 = Arrays.copyOf(original, original.length);

// Méthode 4 : clone()
int[] copie4 = original.clone();</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Tri d'un tableau</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] nombres = {5, 2, 8, 1, 9};
Arrays.sort(nombres);  // Tri croissant
// Résultat : {1, 2, 5, 8, 9}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Recherche dans un tableau trié</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] nombres = {1, 2, 5, 8, 9};
int index = Arrays.binarySearch(nombres, 5); // retourne 2
// Si non trouvé, retourne -(point d'insertion) - 1</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Remplir / comparer</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] tab = new int[10];
Arrays.fill(tab, 42);   // remplit tout le tableau avec 42

int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
boolean egal = Arrays.equals(a, b); // true</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Convertir en chaîne</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] tab = {1, 2, 3};
String str = Arrays.toString(tab);
System.out.println(str); // "[1, 2, 3]"</code></pre>
                    </div>
                </div>
            </section>

            <!-- La classe Arrays -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La classe utilitaire <code>java.util.Arrays</code></h2>
                <p class="textExemple">
                    La classe <code>Arrays</code> fournit de nombreuses méthodes statiques pour manipuler les tableaux :
                </p>
                <ul>
                    <li><code>sort()</code> : tri</li>
                    <li><code>binarySearch()</code> : recherche dichotomique</li>
                    <li><code>copyOf()</code>, <code>copyOfRange()</code> : copie</li>
                    <li><code>equals()</code> : comparaison profonde</li>
                    <li><code>fill()</code> : remplissage</li>
                    <li><code>toString()</code> : représentation textuelle</li>
                    <li><code>stream()</code> : conversion en stream (Java 8+)</li>
                </ul>
                <div class="code-example">
                    <pre v-pre><code class="language-java">import java.util.Arrays;

int[] tab = {3, 1, 4, 1, 5};
Arrays.sort(tab);
System.out.println(Arrays.toString(tab)); // [1, 1, 3, 4, 5]</code></pre>
                </div>
            </section>

            <!-- Limitations et alternatives -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Limitations et alternatives</h2>
                <div class="textExemple">
                    <p><strong>Limitations des tableaux :</strong></p>
                    <ul>
                        <li>Taille fixe : impossible d'ajouter ou supprimer des éléments dynamiquement.</li>
                        <li>Type homogène : tous les éléments doivent être du même type (ou sous-type).</li>
                        <li>Pas de méthodes intégrées pour l'insertion, la suppression, la recherche (sauf via Arrays).</li>
                    </ul>
                    <p><strong>Alternatives :</strong></p>
                    <ul>
                        <li><code>ArrayList&lt;E&gt;</code> : tableau dynamique de la bibliothèque de collections.</li>
                        <li><code>LinkedList&lt;E&gt;</code> : liste chaînée.</li>
                        <li><code>HashSet&lt;E&gt;</code>, <code>HashMap&lt;K,V&gt;</code> : structures non ordonnées.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Exemple avec ArrayList
ArrayList&lt;String&gt; liste = new ArrayList&lt;&gt;();
liste.add("Java");
liste.add("Python");
liste.remove(0);
String premier = liste.get(0);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul class="textExemple">
                    <li><strong>Préférer <code>ArrayList</code></strong> si la taille est dynamique.</li>
                    <li><strong>Toujours vérifier les indices</strong> pour éviter les exceptions.</li>
                    <li><strong>Utiliser la boucle for-each</strong> en lecture seule pour plus de clarté.</li>
                    <li><strong>Initialiser les tableaux d'objets</strong> avant de les utiliser (évite les NullPointerException).</li>
                    <li><strong>Utiliser <code>Arrays.copyOf()</code></strong> plutôt qu'une boucle manuelle pour la copie.</li>
                    <li><strong>Ne pas utiliser <code>==</code> pour comparer deux tableaux</strong> (compare les références). Utiliser <code>Arrays.equals()</code>.</li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Les tableaux sont une structure fondamentale en Java. Ils permettent de gérer efficacement des collections de taille fixe.
                    Bien que limités, ils sont très performants et restent utilisés dans de nombreux contextes (algorithmique, jeux, traitement de données).
                </p>
                <p class="textExemple">
                    Pour des besoins plus avancés, la bibliothèque de collections Java (ArrayList, HashMap, etc.) offre plus de flexibilité.
                    La maîtrise des tableaux est un prérequis indispensable avant d'aborder les structures de données plus complexes.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaArraysLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const languages = ['java'];
                    let loaded = 0;
                    languages.forEach(lang => {
                        const langScript = document.createElement('script');
                        langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`;
                        langScript.onload = () => {
                            loaded++;
                            if (loaded === languages.length) resolve();
                        };
                        document.head.appendChild(langScript);
                    });
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
/* === Styles identiques aux leçons précédentes === */
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
.border-purple { border: 2px solid #e0d6ff; transition: all 0.3s ease; }
.text-purple { color: #6A3093 !important; }
.text-white { color: white !important; }

.code-example {
    margin: 1.5rem 0;
    width: 100%;
    box-sizing: border-box;
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

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

@media (max-width: 768px) {
    .lesson-container  { padding: 1rem; }
    .lesson-header     { padding: 2rem 1rem; }
    .lesson-header h1  { font-size: 2rem; }
    .lesson-section    { padding: 1.5rem; }
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