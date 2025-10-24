<template>
    <div class="lesson-container">
        <article class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header bg-gradient-primary">
                <h1 class="text-white">Les structures switch en PHP</h1>
                <p class="lesson-meta text-white">
                    <time datetime="2023-10-15">15 Octobre 2023</time> •
                    <span>Niveau : Débutant/Intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>
                    La structure <code>switch</code> en PHP est une alternative aux structures conditionnelles
                    <code>if...elseif...else</code> lorsqu'on a besoin de tester une même variable ou expression
                    contre plusieurs valeurs possibles.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Syntaxe de base</h2>
                <p>Voici la structure générale d'un <code>switch</code> :</p>

                <div class="code-example">
                    <h3 class="text-purple">Structure générale</h3>
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
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exemple pratique</h2>
                <p>Comparons un jour de la semaine en utilisant d'abord <code>if...elseif</code>, puis
                    <code>switch</code> :
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">Avec if...elseif</h3>
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
                        <h3 class="text-purple">Avec switch</h3>
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
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">L'importance de l'instruction <code>break</code></h2>
                <p>
                    L'instruction <code>break</code> est cruciale dans un <code>switch</code>.
                    Sans elle, PHP continuera à exécuter les cas suivants même si une correspondance a été trouvée.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Avec et sans break</h3>
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
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Utilisations avancées</h2>

                <div class="code-example">
                    <h3 class="text-purple">Comparaison stricte avec ===</h3>
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
                    <h3 class="text-purple">Retour de valeurs</h3>
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
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
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
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1: Convertisseur de notes</h3>
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
                        <summary class="btn btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="keyword">function</span> <span class="function">convertirNote</span>(<span class="variable">$note</span>) {
    <span class="keyword">switch</span> (<span class="constant">true</span>) {
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">16</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt;= <span class="number">20</span>:
            <span class="keyword">return</span> <span class="string">"Très bien"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">14</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">16</span>:
            <span class="keyword">return</span> <span class="string">"Bien"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">12</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">14</span>:
            <span class="keyword">return</span> <span class="string">"Assez bien"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">10</span> <span class="operator">&&</span> <span class="variable">$note</span> <span class="operator">&lt;</span> <span class="number">12</span>:
            <span class="keyword">return</span> <span class="string">"Passable"</span>;
        <span class="keyword">case</span> <span class="variable">$note</span> &gt;= <span class="number">0</span> <span class="operator">&&</span> <span class="variable">$note</span> &lt; <span class="number">10</span>:
            <span class="keyword">return</span> <span class="string">"Insuffisant"</span>;
        <span class="keyword">default</span>:
            <span class="keyword">return</span> <span class="string">"Note invalide"</span>;
    }
}
<span class="php-tag">?&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p>
                    La structure <code>switch</code> est un outil puissant pour simplifier le code lorsque vous
                    devez tester une variable contre plusieurs valeurs. Elle rend le code plus lisible et
                    plus facile à maintenir que des séries de conditions <code>if...elseif</code>.
                </p>
            </section>
        </article>
    </div>
</template>

<style scoped>
.lesson-container {
    padding: 2rem;
    background: #f8f9fa;
    min-height: 100vh;
}

.lesson-content {
    max-width: 1200px;
    margin: 0 auto;
}

/* Header avec le style gradient */
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

/* Sections de leçon */
.lesson-section {
    padding: 2rem;
    margin-bottom: 2rem;
    border-radius: 15px;
    transition: all 0.3s ease;
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

/* Classes CSS de l'autre page */
.bg-gradient-primary {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
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

/* Boutons */
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

/* Styles pour le code - CONSERVATION DES COULEURS VS CODE */
.code-example, .code-block {
    margin: 1.5rem 0;
}

.code-comparison {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin: 1.5rem 0;
}

@media (max-width: 768px) {
    .code-comparison {
        grid-template-columns: 1fr;
    }
}

pre {
    background: #1e1e1e !important; /* Fond sombre comme VS Code */
    color: #d4d4d4 !important;
    padding: 1.5rem !important;
    border-radius: 8px;
    overflow-x: auto;
    border: 1px solid #333;
    font-family: 'Consolas', 'Monaco', 'Courier New', monospace;
    font-size: 0.9rem;
    line-height: 1.5;
}

/* Couleurs VS Code pour la syntaxe PHP */
.php-tag { color: #569cd6 !important; }
.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }

/* Exercices et solutions */
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

details summary {
    cursor: pointer;
    outline: none;
}

/* Texte des exemples */
.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* Responsive */
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
}

/* Animations */
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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>