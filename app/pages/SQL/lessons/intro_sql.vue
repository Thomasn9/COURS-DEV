<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Introduction à SQL</h1>
                <p class="lesson-meta text-white">Découvrez les bases du langage SQL et son utilité dans la gestion des
                    bases de données</p>
            </header>

            <!-- Section 1: Qu'est-ce que SQL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que SQL ?</h2>
                <p class="textExemple">
                    SQL (Structured Query Language) est un langage de programmation spécialement conçu pour gérer et
                    manipuler des bases de données relationnelles.
                    Développé dans les années 1970 par IBM, SQL est devenu le standard international pour interagir avec
                    les bases de données.
                </p>
                <p class="textExemple">
                    SQL permet de créer, modifier, interroger et administrer des bases de données. Contrairement aux
                    langages de programmation traditionnels,
                    SQL est un langage déclaratif : vous décrivez le résultat souhaité, et le système de base de données
                    détermine comment l'obtenir.
                </p>
            </section>

            <!-- Section 2: Utilité de SQL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi apprendre SQL ?</h2>
                <p class="textExemple">
                    SQL est essentiel pour :
                </p>
                <ul class="textExemple">
                    <li><strong>Extraire des données</strong> : Récupérer des informations spécifiques depuis une base
                        de données</li>
                    <li><strong>Analyser des données</strong> : Effectuer des calculs, des regroupements et des
                        statistiques</li>
                    <li><strong>Manipuler des données</strong> : Ajouter, modifier ou supprimer des enregistrements</li>
                    <li><strong>Créer et gérer des structures</strong> : Concevoir des tables, des index et des
                        relations</li>
                    <li><strong>Automatiser des processus</strong> : Développer des procédures stockées et des
                        déclencheurs</li>
                </ul>
            </section>

            <!-- Section 3: Concepts fondamentaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts fondamentaux</h2>
                <p class="textExemple">
                    Les bases de données relationnelles sont organisées autour de plusieurs concepts clés :
                </p>
                <div class="code-example">
                    <pre><code><span class="comment">-- Une base de données contient des TABLES</span>
<span class="comment">-- Chaque table a des COLONNES (champs)</span>
<span class="comment">-- Chaque enregistrement est une LIGNE dans la table</span>
<span class="comment">-- Les clés primaires identifient de manière unique chaque ligne</span>
<span class="comment">-- Les clés étrangères créent des relations entre les tables</span></code></pre>
                </div>
            </section>

            <!-- Section 4: Premier exemple de requête -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Votre première requête SQL</h2>
                <p class="textExemple">
                    Voici un exemple simple de requête SQL qui récupère des données :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">SELECT</span> <span class="variable">nom</span>, <span class="variable">email</span>
<span class="keyword">FROM</span> <span class="variable">utilisateurs</span>
<span class="keyword">WHERE</span> <span class="variable">ville</span> = <span class="string">'Paris'</span>
<span class="keyword">ORDER BY</span> <span class="variable">nom</span> <span class="keyword">ASC</span>;</code></pre>
                </div>
                <p class="textExemple">
                    Cette requête sélectionne le nom et l'email de tous les utilisateurs habitant Paris, triés par ordre
                    alphabétique.
                </p>
            </section>

            <!-- Section 5: Commandes SQL principales -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les commandes SQL essentielles</h2>
                <p class="textExemple">
                    SQL s'articule autour de 4 commandes principales (CRUD) :
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">SELECT - Lire</h4>
                        <pre><code><span class="keyword">SELECT</span> <span class="variable">*</span>
<span class="keyword">FROM</span> <span class="variable">produits</span>
<span class="keyword">WHERE</span> <span class="variable">prix</span> &gt; <span class="number">50</span>;</code></pre>
                        <p class="textExemple">Récupère tous les produits dont le prix dépasse 50€.</p>
                    </div>
                    <div>
                        <h4 class="text-purple">INSERT - Créer</h4>
                        <pre><code><span class="keyword">INSERT INTO</span> <span class="variable">clients</span> (<span class="variable">nom</span>, <span class="variable">email</span>)
<span class="keyword">VALUES</span> (<span class="string">'Dupont'</span>, <span class="string">'dupont@email.com'</span>);</code></pre>
                        <p class="textExemple">Ajoute un nouveau client dans la table.</p>
                    </div>
                    <div>
                        <h4 class="text-purple">UPDATE - Modifier</h4>
                        <pre><code><span class="keyword">UPDATE</span> <span class="variable">clients</span>
<span class="keyword">SET</span> <span class="variable">ville</span> = <span class="string">'Lyon'</span>
<span class="keyword">WHERE</span> <span class="variable">id</span> = <span class="number">123</span>;</code></pre>
                        <p class="textExemple">Met à jour la ville d'un client spécifique.</p>
                    </div>
                    <div>
                        <h4 class="text-purple">DELETE - Supprimer</h4>
                        <pre><code><span class="keyword">DELETE FROM</span> <span class="variable">commandes</span>
<span class="keyword">WHERE</span> <span class="variable">statut</span> = <span class="string">'annulée'</span>;</code></pre>
                        <p class="textExemple">Supprime les commandes annulées.</p>
                    </div>
                </div>
            </section>

            <!-- Section 6: Exemple de structure de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Création d'une table</h2>
                <p class="textExemple">
                    Voici comment créer une table utilisateurs avec SQL :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">CREATE TABLE</span> <span class="variable">utilisateurs</span> (
    <span class="variable">id</span> <span class="class-name">INT</span> <span class="keyword">PRIMARY KEY AUTO_INCREMENT</span>,
    <span class="variable">nom</span> <span class="class-name">VARCHAR</span>(<span class="number">50</span>) <span class="keyword">NOT NULL</span>,
    <span class="variable">email</span> <span class="class-name">VARCHAR</span>(<span class="number">100</span>) <span class="keyword">UNIQUE</span>,
    <span class="variable">date_inscription</span> <span class="class-name">DATE DEFAULT</span> <span class="function">CURRENT_DATE</span>,
    <span class="variable">actif</span> <span class="class-name">BOOLEAN DEFAULT</span> <span class="keyword">TRUE</span>
);</code></pre>
                </div>
            </section>

            <!-- Section 7: Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        En partant d'une table "produits" avec les colonnes : id, nom, catégorie, prix, stock.<br>
                        Écrivez une requête qui :
                    </p>
                    <ul class="textExemple">
                        <li>Sélectionne tous les produits de la catégorie "Électronique"</li>
                        <li>Affiche seulement le nom et le prix</li>
                        <li>Les trie par prix décroissant</li>
                    </ul>
                    <details>
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution :</h4>
                            <pre><code><span class="keyword">SELECT</span> <span class="variable">nom</span>, <span class="variable">prix</span>
<span class="keyword">FROM</span> <span class="variable">produits</span>
<span class="keyword">WHERE</span> <span class="variable">categorie</span> = <span class="string">'Électronique'</span>
<span class="keyword">ORDER BY</span> <span class="variable">prix</span> <span class="keyword">DESC</span>;</code></pre>

                            <h4 class="text-purple">Explication :</h4>
                            <ul class="textExemple">
                                <li><span class="keyword">SELECT</span> spécifie les colonnes à afficher</li>
                                <li><span class="keyword">FROM</span> indique la table source</li>
                                <li><span class="keyword">WHERE</span> filtre les résultats</li>
                                <li><span class="keyword">ORDER BY</span> trie les résultats (DESC = décroissant)</li>
                            </ul>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Section 8: SQL et PHP -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">SQL et PHP : Une combinaison puissante</h2>
                <p class="textExemple">
                    PHP et SQL fonctionnent parfaitement ensemble pour créer des applications web dynamiques :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Connexion à la base de données</span>
<span class="variable">$pdo</span> = <span class="keyword">new</span> <span class="class-name">PDO</span>(<span class="string">'mysql:host=localhost;dbname=ma_base'</span>, <span class="string">'user'</span>, <span class="string">'password'</span>);

<span class="comment">// Exécution d'une requête SQL</span>
<span class="variable">$requete</span> = <span class="variable">$pdo</span>-&gt;<span class="function">prepare</span>(<span class="string">"SELECT nom, email FROM utilisateurs WHERE ville = ?"</span>);
<span class="variable">$requete</span>-&gt;<span class="function">execute</span>([<span class="string">'Paris'</span>]);
<span class="variable">$utilisateurs</span> = <span class="variable">$requete</span>-&gt;<span class="function">fetchAll</span>();

<span class="comment">// Affichage des résultats</span>
<span class="keyword">foreach</span> (<span class="variable">$utilisateurs</span> <span class="keyword">as</span> <span class="variable">$user</span>) {
    <span class="function">echo</span> <span class="string">"&lt;p&gt;"</span> . <span class="variable">$user</span>[<span class="string">'nom'</span>] . <span class="string">" - "</span> . <span class="variable">$user</span>[<span class="string">'email'</span>] . <span class="string">"&lt;/p&gt;"</span>;
}
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 9: Conclusion et suite -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Prochaines étapes</h2>
                <p class="text-white">
                    Maintenant que vous comprenez les bases de SQL, vous êtes prêt à explorer des concepts plus avancés
                    comme les jointures, les sous-requêtes, les agrégations et l'optimisation des performances.
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

/* Couleurs VS Code pour la syntaxe SQL */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés SQL (SELECT, FROM, WHERE, etc.) */
.variable {
    color: #9cdcfe !important;
}

/* Noms de tables et colonnes */
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

/* Fonctions SQL */
.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs (=, >, <, etc.) */
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

/* Types de données (INT, VARCHAR, etc.) */

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