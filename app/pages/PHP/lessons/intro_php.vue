<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Introduction à PHP</h1>
                <p class="lesson-meta text-white">Découvrez les bases du langage PHP et son utilité dans le
                    développement web</p>
            </header>

            <!-- Section 1: Qu'est-ce que PHP -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que PHP ?</h2>
                <p class="textExemple">
                    PHP (Hypertext Preprocessor) est un langage de script côté serveur conçu spécifiquement pour le
                    développement web.
                    Créé en 1994 par Rasmus Lerdorf, PHP s'est imposé comme l'un des langages les plus populaires pour
                    créer des sites web dynamiques.
                </p>
                <p class="textExemple">
                    Contrairement aux langages côté client comme JavaScript, le code PHP est exécuté sur le serveur
                    avant que la page ne soit envoyée au navigateur.
                    Cela signifie que le visiteur ne voit jamais le code PHP, seulement le résultat HTML généré.
                </p>
            </section>

            <!-- Section 2: Utilité de PHP -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser PHP ?</h2>
                <p class="textExemple">
                    PHP est particulièrement utile pour :
                </p>
                <ul class="textExemple">
                    <li><strong>Créer des sites web dynamiques</strong> : Pages qui changent en fonction des données ou
                        des actions de l'utilisateur</li>
                    <li><strong>Gérer des bases de données</strong> : PHP interagit facilement avec MySQL, PostgreSQL,
                        etc.</li>
                    <li><strong>Gérer les formulaires</strong> : Traitement des données envoyées par les utilisateurs
                    </li>
                    <li><strong>Créer des sessions utilisateur</strong> : Gestion des connexions et des paniers d'achat
                    </li>
                    <li><strong>Générer du contenu personnalisé</strong> : Pages adaptées à chaque visiteur</li>
                </ul>
            </section>

            <!-- Section 3: Premier exemple de code -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Votre premier script PHP</h2>
                <p class="textExemple">
                    Voici un exemple simple de code PHP qui affiche un message :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
  <span class="comment">// Ceci est un commentaire en PHP</span>
  <span class="function">echo</span> <span class="string">"&lt;h1&gt;Bonjour le monde !&lt;/h1&gt;"</span>;
  <span class="function">echo</span> <span class="string">"&lt;p&gt;Aujourd'hui nous sommes le "</span> . <span class="function">date</span>(<span class="string">'d/m/Y'</span>) . <span class="string">"&lt;/p&gt;"</span>;
<span class="keyword">?&gt;</span></code></pre>
                </div>
                <p class="textExemple">
                    Ce code générera un titre "Bonjour le monde !" et affichera la date actuelle.
                </p>
            </section>

            <!-- Section 4: PHP vs HTML statique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">PHP vs HTML statique</h2>
                <p class="textExemple">
                    Comparons comment afficher la date avec HTML statique et PHP dynamique :
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">HTML Statique</h4>
                        <pre><code><span class="keyword">&lt;!DOCTYPE html&gt;</span>
<span class="keyword">&lt;html&gt;</span>
<span class="keyword">&lt;head&gt;</span>
  <span class="keyword">&lt;title&gt;</span>Page statique<span class="keyword">&lt;/title&gt;</span>
<span class="keyword">&lt;/head&gt;</span>
<span class="keyword">&lt;body&gt;</span>
  <span class="keyword">&lt;p&gt;</span>Aujourd'hui nous sommes le 15/03/2024<span class="keyword">&lt;/p&gt;</span>
<span class="keyword">&lt;/body&gt;</span>
<span class="keyword">&lt;/html&gt;</span></code></pre>
                        <p class="textExemple">La date reste fixe et doit être mise à jour manuellement.</p>
                    </div>
                    <div>
                        <h4 class="text-purple">PHP Dynamique</h4>
                        <pre><code><span class="keyword">&lt;!DOCTYPE html&gt;</span>
<span class="keyword">&lt;html&gt;</span>
<span class="keyword">&lt;head&gt;</span>
  <span class="keyword">&lt;title&gt;</span>Page dynamique<span class="keyword">&lt;/title&gt;</span>
<span class="keyword">&lt;/head&gt;</span>
<span class="keyword">&lt;body&gt;</span>
  <span class="keyword">&lt;?php</span>
    <span class="function">echo</span> <span class="string">"&lt;p&gt;Aujourd'hui nous sommes le "</span> . <span class="function">date</span>(<span class="string">'d/m/Y'</span>) . <span class="string">"&lt;/p&gt;"</span>;
  <span class="keyword">?&gt;</span>
<span class="keyword">&lt;/body&gt;</span>
<span class="keyword">&lt;/html&gt;</span></code></pre>
                        <p class="textExemple">La date s'actualise automatiquement chaque jour.</p>
                    </div>
                </div>
            </section>

            <!-- Section 5: Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Créez un script PHP qui affiche un message de bienvenue personnalisé en fonction de l'heure de
                        la journée.
                    </p>
                    <details>
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution :</h4>
                            <pre><code><span class="keyword">&lt;?php</span>
  <span class="comment">// Récupérer l'heure actuelle</span>
  <span class="variable">$heure</span> = <span class="function">date</span>(<span class="string">'H'</span>);
  
  <span class="comment">// Déterminer le message en fonction de l'heure</span>
  <span class="keyword">if</span> (<span class="variable">$heure</span> &lt; <span class="number">12</span>) {
    <span class="variable">$message</span> = <span class="string">"Bonjour !"</span>;
  } <span class="keyword">elseif</span> (<span class="variable">$heure</span> &lt; <span class="number">18</span>) {
    <span class="variable">$message</span> = <span class="string">"Bon après-midi !"</span>;
  } <span class="keyword">else</span> {
    <span class="variable">$message</span> = <span class="string">"Bonsoir !"</span>;
  }
  
  <span class="comment">// Afficher le message</span>
  <span class="function">echo</span> <span class="string">"&lt;h2&gt;$message&lt;/h2&gt;"</span>;
<span class="keyword">?&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Section 6: Conclusion et suite -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Prochaines étapes</h2>
                <p class="text-white">
                    Maintenant que vous comprenez ce qu'est PHP et son utilité, vous êtes prêt à explorer les concepts
                    fondamentaux
                    comme les variables, les structures de contrôle, les fonctions et l'interaction avec les bases de
                    données.
                </p>
            </section>
        </div>
    </div>
</template>

<script>
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
    width: 100%;
    overflow-x: hidden;
    box-sizing: border-box;
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

/* CORRECTION RESPONSIVE POUR LES BLOCS DE CODE */
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
    /* Permet le retour à la ligne */
    word-wrap: break-word;
    /* Casse les mots longs */
    word-break: break-word;
    /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe PHP */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (for, while, if, function, etc.) */
.variable {
    color: #9cdcfe !important;
}

/* Variables et noms de fonctions */
.string {
    color: #ce9178 !important;
}

/* Chaînes de caractères */
.comment {
    color: #6a9955 !important;
}

/* Commentaires */
.function {
    color: #dcdcaa !important;
}

/* Noms de fonctions */
.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs (+, -, =, =>, etc.) */
.constant {
    color: #4fc1ff !important;
}

/* Constantes */
.number {
    color: #b5cea8 !important;
}

/* Nombres */
.class-name {
    color: #4ec9b0 !important;
}

/* Noms de classes */

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

.solution-content h4 {
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
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

.text-center {
    text-align: center;
}

/* RESPONSIVE DESIGN AMÉLIORÉ */
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

/* POUR LES TRÈS PETITS ÉCRANS */
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

/* POUR LES TRÈS GRANDS ÉCRANS */
@media (min-width: 1400px) {
    .lesson-content {
        max-width: 1300px;
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

.lesson-section:nth-child(1) {
    animation-delay: 0.1s;
}

.lesson-section:nth-child(2) {
    animation-delay: 0.2s;
}

.lesson-section:nth-child(3) {
    animation-delay: 0.3s;
}

.lesson-section:nth-child(4) {
    animation-delay: 0.4s;
}

.lesson-section:nth-child(5) {
    animation-delay: 0.5s;
}
</style>