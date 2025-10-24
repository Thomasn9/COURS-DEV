<template>
    <div class="lesson-container">
        <article class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1>Les structures switch en PHP</h1>
                <p class="lesson-meta">
                    <time datetime="2023-10-15">15 Octobre 2023</time> •
                    <span>Niveau : Débutant/Intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section">
                <h2>Introduction</h2>
                <p>
                    La structure <code>switch</code> en PHP est une alternative aux structures conditionnelles
                    <code>if...elseif...else</code> lorsqu'on a besoin de tester une même variable ou expression
                    contre plusieurs valeurs possibles.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section">
                <h2>Syntaxe de base</h2>
                <p>Voici la structure générale d'un <code>switch</code> :</p>

                <div class="code-example">
                    <h3>Structure générale</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="keyword">switch</span> (<span class="variable">$expression</span>) {
    <span class="keyword">case</span> <span class="string">valeur1</span>:
        <span class="comment">// Code à exécuter si expression == valeur1</span>
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">valeur2</span>:
        <span class="comment">// Code à exécuter si expression == valeur2</span>
        <span class="keyword">break</span>;
    <span class="keyword">default</span>:
        <span class="comment">// Code à exécuter si aucune case ne correspond</span>
}
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Exemple pratique -->
            <section class="lesson-section">
                <h2>Exemple pratique</h2>
                <p>Comparons un jour de la semaine en utilisant d'abord <code>if...elseif</code>, puis
                    <code>switch</code> :
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3>Avec if...elseif</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$jour</span> = <span class="string">"Lundi"</span>;

<span class="keyword">if</span> (<span class="variable">$jour</span> == <span class="string">"Lundi"</span>) {
    <span class="function">echo</span> <span class="string">"Début de semaine"</span>;
} <span class="keyword">elseif</span> (<span class="variable">$jour</span> == <span class="string">"Vendredi"</span>) {
    <span class="function">echo</span> <span class="string">"Bientôt le weekend!"</span>;
} <span class="keyword">elseif</span> (<span class="variable">$jour</span> == <span class="string">"Samedi"</span> <span class="operator">||</span> <span class="variable">$jour</span> == <span class="string">"Dimanche"</span>) {
    <span class="function">echo</span> <span class="string">"Weekend!"</span>;
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Jour de semaine normal"</span>;
}
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3>Avec switch</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$jour</span> = <span class="string">"Lundi"</span>;

<span class="keyword">switch</span> (<span class="variable">$jour</span>) {
    <span class="keyword">case</span> <span class="string">"Lundi"</span>:
        <span class="function">echo</span> <span class="string">"Début de semaine"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">"Vendredi"</span>:
        <span class="function">echo</span> <span class="string">"Bientôt le weekend!"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">"Samedi"</span>:
    <span class="keyword">case</span> <span class="string">"Dimanche"</span>:
        <span class="function">echo</span> <span class="string">"Weekend!"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">default</span>:
        <span class="function">echo</span> <span class="string">"Jour de semaine normal"</span>;
}
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- L'importance du break -->
            <section class="lesson-section">
                <h2>L'importance de l'instruction <code>break</code></h2>
                <p>
                    L'instruction <code>break</code> est cruciale dans un <code>switch</code>.
                    Sans elle, PHP continuera à exécuter les cas suivants même si une correspondance a été trouvée.
                </p>

                <div class="code-example">
                    <h3>Avec et sans break</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$note</span> = <span class="string">"B"</span>;

<span class="comment">// Sans break - COMPORTEMENT NON SOUHAITÉ</span>
<span class="keyword">switch</span> (<span class="variable">$note</span>) {
    <span class="keyword">case</span> <span class="string">"A"</span>:
        <span class="function">echo</span> <span class="string">"Excellent"</span>;
    <span class="keyword">case</span> <span class="string">"B"</span>:
        <span class="function">echo</span> <span class="string">"Très bien"</span>;
    <span class="keyword">case</span> <span class="string">"C"</span>:
        <span class="function">echo</span> <span class="string">"Bien"</span>;
    <span class="keyword">default</span>:
        <span class="function">echo</span> <span class="string">"Note non reconnue"</span>;
}
<span class="comment">// Affiche: "Très bienBienNote non reconnue"</span>

<span class="comment">// Avec break - COMPORTEMENT SOUHAITÉ</span>
<span class="keyword">switch</span> (<span class="variable">$note</span>) {
    <span class="keyword">case</span> <span class="string">"A"</span>:
        <span class="function">echo</span> <span class="string">"Excellent"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">"B"</span>:
        <span class="function">echo</span> <span class="string">"Très bien"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">"C"</span>:
        <span class="function">echo</span> <span class="string">"Bien"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">default</span>:
        <span class="function">echo</span> <span class="string">"Note non reconnue"</span>;
}
<span class="comment">// Affiche: "Très bien"</span>
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Utilisation avancée -->
            <section class="lesson-section">
                <h2>Utilisations avancées</h2>

                <div class="code-example">
                    <h3>Comparaison stricte avec ===</h3>
                    <p class="textExemple">Par défaut, <code>switch</code> utilise une comparaison lâche (==). Pour une comparaison stricte,
                        vous pouvez utiliser cette astuce :</p>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$valeur</span> = <span class="string">"1"</span>;

<span class="keyword">switch</span> (<span class="constant">true</span>) {
    <span class="keyword">case</span> <span class="variable">$valeur</span> <span class="operator">===</span> <span class="number">1</span>:
        <span class="function">echo</span> <span class="string">"Strictement égal à 1 (entier)"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="variable">$valeur</span> <span class="operator">===</span> <span class="string">"1"</span>:
        <span class="function">echo</span> <span class="string">"Strictement égal à '1' (chaîne)"</span>;
        <span class="keyword">break</span>;
    <span class="keyword">default</span>:
        <span class="function">echo</span> <span class="string">"Autre valeur"</span>;
}
<span class="comment">// Affiche: "Strictement égal à '1' (chaîne)"</span>
<span class="php-tag">?&gt;</span></code></pre>
                </div>

                <div class="code-example">
                    <h3>Retour de valeurs</h3>
                    <p class="textExemple">Vous pouvez utiliser <code>switch</code> pour retourner des valeurs :</p>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="keyword">function</span> <span class="function">obtenirStatutCommande</span>(<span class="variable">$code</span>) {
    <span class="keyword">switch</span> (<span class="variable">$code</span>) {
        <span class="keyword">case</span> <span class="number">1</span>:
            <span class="keyword">return</span> <span class="string">"En attente"</span>;
        <span class="keyword">case</span> <span class="number">2</span>:
            <span class="keyword">return</span> <span class="string">"Confirmée"</span>;
        <span class="keyword">case</span> <span class="number">3</span>:
            <span class="keyword">return</span> <span class="string">"Expédiée"</span>;
        <span class="keyword">case</span> <span class="number">4</span>:
            <span class="keyword">return</span> <span class="string">"Livrée"</span>;
        <span class="keyword">default</span>:
            <span class="keyword">return</span> <span class="string">"Statut inconnu"</span>;
    }
}

<span class="function">echo</span> <span class="function">obtenirStatutCommande</span>(<span class="number">2</span>); <span class="comment">// Affiche: "Confirmée"</span>
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section">
                <h2>Bonnes pratiques</h2>
                <ul>
                    <li>Toujours inclure un <code>break</code> sauf lorsque vous voulez explicitement un "fall-through"
                    </li>
                    <li>Utiliser <code>default</code> pour gérer les cas non prévus</li>
                    <li>Préférer <code>switch</code> aux multiples <code>if...elseif</code> quand vous testez la même
                        variable contre plusieurs valeurs</li>
                    <li>Documenter les cas où vous utilisez intentionnellement un "fall-through" (absence de break)</li>
                </ul>
            </section>

            <!-- Exercices -->
            <section class="lesson-section">
                <h2>Exercices pratiques</h2>

                <div class="exercise">
                    <h3>Exercice 1: Convertisseur de notes</h3>
                    <p>
                        Écrivez une fonction qui convertit une note numérique (0-20) en mention :
                    </p>
                    <ul>
                        <li>16-20: "Très bien"</li>
                        <li>14-15: "Bien"</li>
                        <li>12-13: "Assez bien"</li>
                        <li>10-11: "Passable"</li>
                        <li>0-9: "Insuffisant"</li>
                    </ul>

                    <details class="solution">
                        <summary>Voir la solution</summary>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="keyword">function</span> <span class="function">convertirNote</span>(<span class="variable">$note</span>) {
    <span class="keyword">switch</span> (<span class="constant">true</span>) {
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">16</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt;= <span class="number">20</span>:
            <span class="keyword">return</span> <span class="string">"Très bien"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">14</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">16</span>:
            <span class="keyword">return</span> <span class="string">"Bien"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">12</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">14</span>:
            <span class="keyword">return</span> <span class="string">"Assez bien"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">10</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">12</span>:
            <span class="keyword">return</span> <span class="string">"Passable"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">0</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">10</span>:
            <span class="keyword">return</span> <span class="string">"Insuffisant"</span>;
        <span class="keyword">default</span>:
            <span class="keyword">return</span> <span class="string">"Note invalide"</span>;
    }
}
<span class="php-tag">?&gt;</span></code></pre>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section">
                <h2>Conclusion</h2>
                <p>
                    La structure <code>switch</code> est un outil puissant pour simplifier le code lorsque vous
                    devez tester une variable contre plusieurs valeurs. Elle rend le code plus lisible et
                    plus facile à maintenir que des séries de conditions <code>if...elseif</code>.
                </p>
            </section>
        </article>
    </div>
</template>

<script>

</script>

<style scoped>

.textExemple{
    color: white;
}
.lesson-container {
    max-width: 900px;
    margin: 0 auto;
    padding: 2rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    line-height: 1.6;
}

.lesson-header {
    border-bottom: 2px solid #e1e1e1;
    padding-bottom: 1rem;
    margin-bottom: 2rem;
}

.lesson-header h1 {
    color: #2c3e50;
    margin-bottom: 0.5rem;
}

.lesson-meta {
    color: #7f8c8d;
    font-size: 0.9rem;
}

.lesson-section {
    margin-bottom: 3rem;
}

.lesson-section h2 {
    color: #3498db;
    border-bottom: 1px solid #e1e1e1;
    padding-bottom: 0.5rem;
    margin-bottom: 1rem;
}

.code-example,
.code-block {
    background: #1e1e1e;
    border: 1px solid #424242;
    border-radius: 6px;
    padding: 1rem;
    margin: 1rem 0;
    overflow-x: auto;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.code-example h3,
.code-block h3 {
    margin-top: 0;
    color: #d4d4d4;
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
}

.code-comparison {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
}

@media (max-width: 768px) {
    .code-comparison {
        grid-template-columns: 1fr;
    }
}

pre {
    margin: 0;
    white-space: pre-wrap;
    font-family: 'Cascadia Code', 'Fira Code', 'Consolas', 'Monaco', 'Courier New', monospace;
    font-size: 0.9rem;
    line-height: 1.5;
}

code {
    background: #1e1e1e;
    color: #d4d4d4;
    padding: 0.2rem 0.4rem;
    border-radius: 3px;
    font-family: 'Cascadia Code', 'Fira Code', 'Consolas', 'Monaco', 'Courier New', monospace;
}

pre code {
    background: none;
    color: inherit;
    padding: 0;
    display: block;
}

/* Coloration syntaxique VS Code pour PHP */
.language-php {
    color: #d4d4d4;
}

/* Balises PHP */
.language-php .php-tag {
    color: #569cd6;
}

/* Mots-clés PHP */
.language-php .keyword {
    color: #c586c0;
}

/* Fonctions */
.language-php .function {
    color: #dcdcaa;
}

/* Chaînes de caractères */
.language-php .string {
    color: #ce9178;
}

/* Commentaires */
.language-php .comment {
    color: #6a9955;
    font-style: italic;
}

/* Variables */
.language-php .variable {
    color: #9cdcfe;
}

/* Opérateurs */
.language-php .operator {
    color: #d4d4d4;
}

/* Nombres */
.language-php .number {
    color: #b5cea8;
}

/* Constantes et booléens */
.language-php .constant {
    color: #569cd6;
}

/* Ponctuation */
.language-php .punctuation {
    color: #d4d4d4;
}

.exercise {
    background: #e8f4fd;
    border-left: 4px solid #3498db;
    padding: 1rem;
    margin: 1.5rem 0;
    border-radius: 4px;
}

.solution {
    margin-top: 1rem;
}

.solution summary {
    cursor: pointer;
    font-weight: bold;
    color: #2980b9;
    padding: 0.5rem;
    background: #d6eaf8;
    border-radius: 4px;
    transition: background-color 0.2s;
}

.solution summary:hover {
    background: #aed6f1;
}

.solution pre {
    margin-top: 1rem;
}

ul {
    padding-left: 1.5rem;
}

li {
    margin-bottom: 0.5rem;
}

/* Amélioration pour la lisibilité */
.code-example:hover,
.code-block:hover {
    border-color: #569cd6;
    transition: border-color 0.3s ease;
}

/* Scrollbar personnalisée pour les blocs de code */
.code-example::-webkit-scrollbar,
.code-block::-webkit-scrollbar {
    height: 8px;
}

.code-example::-webkit-scrollbar-track,
.code-block::-webkit-scrollbar-track {
    background: #2d2d2d;
    border-radius: 0 0 6px 6px;
}

.code-example::-webkit-scrollbar-thumb,
.code-block::-webkit-scrollbar-thumb {
    background: #569cd6;
    border-radius: 4px;
}

.code-example::-webkit-scrollbar-thumb:hover,
.code-block::-webkit-scrollbar-thumb:hover {
    background: #4a86c6;
}

/* Style pour le code inline */
:not(pre)>code {
    background: #f1f1f1;
    color: #e74c3c;
    padding: 0.2rem 0.4rem;
    border-radius: 3px;
    font-size: 0.9em;
}
</style>