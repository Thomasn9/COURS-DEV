<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les boucles en Java</h1>
                <p class="lesson-meta text-white">Java • Itérations • for • while • do-while • for-each</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux boucles</h2>
                <p class="textExemple">
                    Les boucles permettent d’exécuter un bloc de code de manière répétitive tant qu’une condition est vraie.
                    Java propose plusieurs types de boucles : <code>for</code>, <code>while</code>, <code>do-while</code>,
                    et la boucle <code>for-each</code> (version améliorée de <code>for</code> pour les tableaux et collections).
                </p>
                <p class="textExemple">
                    Le choix de la boucle dépend du contexte : nombre d’itérations connu à l’avance, exécution au moins une fois,
                    parcours d’une collection, etc.
                </p>
            </section>

            <!-- La boucle for classique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La boucle for classique</h2>
                <div class="textExemple">
                    <p>La boucle <code>for</code> est idéale quand on connaît le nombre d’itérations à l’avance.</p>
                    <p><strong>Syntaxe :</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (initialisation; condition; incrément) {
    // instructions à répéter
}</code></pre>
                    </div>
                    <p><strong>Exemple :</strong> afficher les nombres de 0 à 9</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (int i = 0; i &lt; 10; i++) {
    System.out.println(i);
}</code></pre>
                    </div>
                    <p><strong>Exemple :</strong> parcourir un tableau</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] notes = {12, 15, 8, 19};
for (int i = 0; i &lt; notes.length; i++) {
    System.out.println("Note " + i + " : " + notes[i]);
}</code></pre>
                    </div>
                    <p><strong>Variantes :</strong> plusieurs variables, incrément complexe</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (int i = 0, j = 10; i &lt; j; i++, j--) {
    System.out.println("i=" + i + ", j=" + j);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- La boucle for-each (améliorée) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La boucle for-each (enhanced for)</h2>
                <div class="textExemple">
                    <p>Introduite en Java 5, elle simplifie le parcours des tableaux et des collections (Iterable).</p>
                    <p><strong>Syntaxe :</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (Type élément : tableauOuCollection) {
    // instructions
}</code></pre>
                    </div>
                    <p><strong>Exemple avec un tableau :</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[] nombres = {10, 20, 30, 40};
for (int val : nombres) {
    System.out.println(val);
}</code></pre>
                    </div>
                    <p><strong>Exemple avec une ArrayList :</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">List&lt;String&gt; noms = Arrays.asList("Alice", "Bob", "Charlie");
for (String nom : noms) {
    System.out.println("Bonjour " + nom);
}</code></pre>
                    </div>
                    <div class="warning-section">
                        <p class="warning-text">
                            ⚠️ La boucle for-each ne permet pas de modifier la structure de la collection
                            (ajout/suppression d’éléments) ni d’accéder à l’index courant.
                            Pour cela, utilisez la boucle for classique.
                        </p>
                    </div>
                </div>
            </section>

            <!-- La boucle while -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La boucle while</h2>
                <div class="textExemple">
                    <p>La boucle <code>while</code> répète un bloc tant que la condition est vraie.
                    Elle est adaptée quand le nombre d’itérations est inconnu à l’avance.</p>
                    <p><strong>Syntaxe :</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">while (condition) {
    // instructions
}</code></pre>
                    </div>
                    <p><strong>Exemple :</strong> afficher la table de multiplication de 7 jusqu’à 10</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int i = 1;
while (i &lt;= 10) {
    System.out.println("7 x " + i + " = " + (7 * i));
    i++;
}</code></pre>
                    </div>
                    <p><strong>Exemple :</strong> lire des entiers jusqu’à ce que l’utilisateur entre -1</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">Scanner sc = new Scanner(System.in);
int valeur;
while ((valeur = sc.nextInt()) != -1) {
    System.out.println("Vous avez saisi : " + valeur);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- La boucle do-while -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La boucle do-while</h2>
                <div class="textExemple">
                    <p>Similaire à <code>while</code>, mais la condition est testée <strong>après</strong> l’exécution du bloc.
                    Ainsi, le bloc est exécuté au moins une fois.</p>
                    <p><strong>Syntaxe :</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">do {
    // instructions
} while (condition);</code></pre>
                    </div>
                    <p><strong>Exemple :</strong> demander un nombre entre 1 et 10 (redemander tant qu’il n’est pas valide)</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int nombre;
do {
    System.out.print("Entrez un nombre entre 1 et 10 : ");
    nombre = sc.nextInt();
} while (nombre &lt; 1 || nombre &gt; 10);
System.out.println("Merci, vous avez saisi " + nombre);</code></pre>
                    </div>
                    <p>Ici, la saisie est effectuée au moins une fois, ce qui est naturel.</p>
                </div>
            </section>

            <!-- Instructions break et continue -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Instructions break et continue</h2>
                <div class="textExemple">
                    <h3 class="text-purple">break</h3>
                    <p>Interrompt immédiatement la boucle (on sort de la boucle).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (int i = 0; i &lt; 10; i++) {
    if (i == 5) {
        break;  // sort de la boucle quand i vaut 5
    }
    System.out.println(i);
}
// Affiche 0 1 2 3 4</code></pre>
                    </div>

                    <h3 class="text-purple">continue</h3>
                    <p>Passe à l’itération suivante (saute le reste du bloc).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (int i = 0; i &lt; 10; i++) {
    if (i % 2 == 0) {
        continue;  // saute les nombres pairs
    }
    System.out.println(i);
}
// Affiche 1 3 5 7 9</code></pre>
                    </div>

                    <h3 class="text-purple">break étiqueté (labeled break)</h3>
                    <p>Permet de sortir d’une boucle extérieure depuis une boucle imbriquée.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">recherche:
for (int i = 0; i &lt; 3; i++) {
    for (int j = 0; j &lt; 3; j++) {
        if (i == 1 &amp;&amp; j == 1) {
            break recherche;  // sort des deux boucles
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
// Affiche (0,0) (0,1) (0,2) (1,0)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Boucles imbriquées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Boucles imbriquées</h2>
                <div class="textExemple">
                    <p>On peut placer une boucle à l’intérieur d’une autre. Utile pour les tableaux multidimensionnels ou les combinaisons.</p>
                    <p><strong>Exemple :</strong> afficher une table de multiplication 5x5</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (int i = 1; i &lt;= 5; i++) {
    for (int j = 1; j &lt;= 5; j++) {
        System.out.print(i * j + "\t");
    }
    System.out.println();
}</code></pre>
                    </div>
                    <p><strong>Exemple :</strong> parcourir une matrice (tableau 2D)</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int[][] matrice = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
for (int i = 0; i &lt; matrice.length; i++) {
    for (int j = 0; j &lt; matrice[i].length; j++) {
        System.out.print(matrice[i][j] + " ");
    }
    System.out.println();
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Boucle infinie -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Boucle infinie et comment l’éviter</h2>
                <div class="textExemple">
                    <p>Une boucle infinie se produit quand la condition de sortie n’est jamais vraie.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Boucle infinie volontaire (à éviter sauf cas particulier)
while (true) {
    // ... avec un break à l’intérieur
}

// Boucle infinie accidentelle (oubli d’incrément)
int i = 0;
while (i &lt; 10) {
    System.out.println(i);
    // i++ manquant -> i reste à 0
}</code></pre>
                    </div>
                    <p>Pour interrompre une boucle infinie dans un programme en cours d’exécution, utilisez <kbd>Ctrl+C</kbd> (dans la console) ou stoppez le processus.</p>
                    <p><strong>Bonnes pratiques :</strong></p>
                    <ul>
                        <li>Vérifiez que l’incrément modifie bien la variable de condition.</li>
                        <li>Évitez les conditions toujours vraies (<code>true</code>) sauf si vous avez un <code>break</code> interne explicite.</li>
                        <li>Testez vos boucles avec des cas limites (0 itération, 1 itération).</li>
                    </ul>
                </div>
            </section>

            <!-- Performances et conseils -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conseils de performance</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Calculer la taille une seule fois</strong> dans la condition (si la taille ne change pas) :</li>
                        <div class="code-example">
                            <pre v-pre><code class="language-java">// Moins performant (recalcule length à chaque itération)
for (int i = 0; i &lt; tableau.length; i++) { ... }

// Mieux
for (int i = 0, len = tableau.length; i &lt; len; i++) { ... }</code></pre>
                        </div>
                        <li><strong>Préférer la boucle for-each</strong> pour la lecture seule de collections : plus lisible et moins d’erreurs d’indice.</li>
                        <li><strong>Éviter les opérations coûteuses dans la condition</strong> (appels de méthodes lourdes).</li>
                        <li><strong>Pour les grands tableaux</strong>, l’accès séquentiel est plus rapide que l’accès aléatoire (principe de localité).</li>
                    </ul>
                </div>
            </section>

            <!-- Erreurs courantes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Erreurs fréquentes</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Off-by-one (décalage d’indice)</strong> : utiliser <code>&lt;=</code> au lieu de <code>&lt;</code> ou inversement.</li>
                        <li><strong>Oublier l’incrément</strong> dans <code>while</code> → boucle infinie.</li>
                        <li><strong>Comparer des objets avec <code>==</code></strong> dans une condition de boucle (utiliser <code>.equals()</code>).</li>
                        <li><strong>Modifier la collection pendant un for-each</strong> (cause <code>ConcurrentModificationException</code>).</li>
                        <li><strong>Ne pas initialiser les variables utilisées dans la condition</strong>.</li>
                    </ul>
                </div>
            </section>

            <!-- Comparaison des types de boucles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Quand utiliser quelle boucle ?</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>for classique</strong> : nombre d’itérations connu (tableau, plage d’entiers).</li>
                        <li><strong>for-each</strong> : parcours complet d’un tableau ou d’une collection, sans besoin d’index.</li>
                        <li><strong>while</strong> : nombre inconnu, condition basée sur une entrée utilisateur ou une ressource.</li>
                        <li><strong>do-while</strong> : au moins une exécution obligatoire (ex: menu, saisie utilisateur).</li>
                    </ul>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Les boucles sont des structures fondamentales en programmation. Java offre plusieurs variantes
                    adaptées à différents contextes. Maîtriser <code>for</code>, <code>while</code>, <code>do-while</code>
                    et <code>for-each</code> permet d’écrire du code concis, efficace et sans erreur.
                </p>
                <p class="textExemple">
                    N’oubliez pas d’utiliser <code>break</code> et <code>continue</code> avec parcimonie,
                    et préférez toujours la boucle la plus expressive pour l’intention que vous voulez communiquer.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaLoopsLesson',

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