<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">La fonction password_verify() en PHP</h1>
                <p class="lesson-meta text-white">Sécurité • Hachage de mots de passe • Validation</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    La fonction <code>password_verify()</code> est une fonction essentielle en PHP pour la sécurité des
                    applications web.
                    Elle permet de vérifier qu'un mot de passe en clair correspond à un hachage généré par la fonction
                    <code>password_hash()</code>.
                </p>
                <p class="textExemple">
                    Cette fonction est cruciale pour authentifier les utilisateurs de manière sécurisée, sans stocker
                    leurs mots de passe en clair dans la base de données.
                </p>
            </section>

            <!-- Syntaxe -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe</h2>
                <div class="code-block">
                    <pre><code class="language-php">bool password_verify ( string $password , string $hash )</code></pre>
                </div>
                <div class="textExemple">
                    <p><strong>Paramètres :</strong></p>
                    <ul>
                        <li><code>$password</code> : Le mot de passe en clair à vérifier</li>
                        <li><code>$hash</code> : Le hachage stocké (généré par <code>password_hash()</code>)</li>
                    </ul>
                    <p><strong>Valeur de retour :</strong></p>
                    <ul>
                        <li><code>true</code> si le mot de passe correspond au hachage</li>
                        <li><code>false</code> dans le cas contraire</li>
                    </ul>
                </div>
            </section>

            <!-- Exemple d'utilisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple d'utilisation</h2>
                <p class="textExemple">
                    Voici un exemple complet d'utilisation de <code>password_verify()</code> dans un contexte
                    d'authentification :
                </p>

                <div class="code-example">
                    <pre><code class="language-php">&lt;?php
// Exemple de hachage de mot de passe (généré avec password_hash())
<span class="variable">$hash_stocke</span> = <span class="string">'$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi'</span>;

// Mot de passe saisi par l'utilisateur
<span class="variable">$mot_de_passe_saisi</span> = <span class="string">'password123'</span>;

// Vérification du mot de passe
<span class="keyword">if</span> (<span class="function">password_verify</span>(<span class="variable">$mot_de_passe_saisi</span>, <span class="variable">$hash_stocke</span>)) {
    <span class="function">echo</span> <span class="string">'Mot de passe correct !'</span>;
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">'Mot de passe incorrect.'</span>;
}
?&gt;</code></pre>
                </div>
            </section>

            <!-- Comparaison avec l'ancienne méthode -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comparaison avec les anciennes méthodes</h2>
                <p class="textExemple">
                    Avant l'introduction des fonctions <code>password_hash()</code> et <code>password_verify()</code>,
                    les développeurs utilisaient souvent des fonctions comme <code>md5()</code> ou <code>sha1()</code>
                    pour hacher les mots de passe, ce qui était beaucoup moins sécurisé.
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Ancienne méthode (déconseillée)</h4>
                        <pre><code class="language-php">&lt;?php
// Hachage avec md5 (INSÉCURISÉ)
<span class="variable">$hash</span> = <span class="function">md5</span>(<span class="variable">$password</span>);

// Vérification
<span class="keyword">if</span> (<span class="function">md5</span>(<span class="variable">$password_saisi</span>) === <span class="variable">$hash</span>) {
    <span class="comment">// Authentification réussie</span>
}
?&gt;</code></pre>
                    </div>

                    <div>
                        <h4 class="text-purple">Nouvelle méthode (recommandée)</h4>
                        <pre><code class="language-php">&lt;?php
// Hachage sécurisé
<span class="variable">$hash</span> = <span class="function">password_hash</span>(<span class="variable">$password</span>, PASSWORD_DEFAULT);

// Vérification sécurisée
<span class="keyword">if</span> (<span class="function">password_verify</span>(<span class="variable">$password_saisi</span>, <span class="variable">$hash</span>)) {
    <span class="comment">// Authentification réussie</span>
}
?&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <div class="textExemple">
                    <p><strong>1. Utilisez toujours password_hash() avec password_verify()</strong></p>
                    <p>Ces deux fonctions sont conçues pour fonctionner ensemble.</p>

                    <p><strong>2. Ne stockez jamais les mots de passe en clair</strong></p>
                    <p>Même avec les fonctions de hachage, assurez-vous que votre base de données est sécurisée.</p>

                    <p><strong>3. Utilisez PASSWORD_DEFAULT comme algorithme</strong></p>
                    <p>Cet algorithme évoluera avec les nouvelles versions de PHP pour garantir la sécurité.</p>

                    <p><strong>4. Vérifiez si le hachage doit être réactualisé</strong></p>
                    <p>Utilisez <code>password_needs_rehash()</code> pour mettre à jour les anciens hachages.</p>
                </div>
            </section>

            <!-- Cas d'usage complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas d'usage complet</h2>
                <p class="textExemple">
                    Voici un exemple complet d'inscription et de connexion d'un utilisateur :
                </p>

                <div class="code-example">
                    <pre><code class="language-php">&lt;?php
<span class="comment">// INSCRIPTION - Création du compte</span>
<span class="keyword">function</span> <span class="function">creerUtilisateur</span>(<span class="variable">$nom_utilisateur</span>, <span class="variable">$mot_de_passe</span>) {
    <span class="comment">// Hachage du mot de passe</span>
    <span class="variable">$hash_mot_de_passe</span> = <span class="function">password_hash</span>(<span class="variable">$mot_de_passe</span>, PASSWORD_DEFAULT);
    
    <span class="comment">// Stockage dans la base de données</span>
    <span class="comment">// (pseudo-code pour l'exemple)</span>
    <span class="variable">$requete</span> = <span class="string">"INSERT INTO utilisateurs (nom_utilisateur, mot_de_passe) VALUES (?, ?)"</span>;
    <span class="comment">// Exécuter la requête avec $nom_utilisateur et $hash_mot_de_passe</span>
}

<span class="comment">// CONNEXION - Authentification</span>
<span class="keyword">function</span> <span class="function">authentifierUtilisateur</span>(<span class="variable">$nom_utilisateur</span>, <span class="variable">$mot_de_passe_saisi</span>) {
    <span class="comment">// Récupération de l'utilisateur depuis la base de données</span>
    <span class="comment">// (pseudo-code pour l'exemple)</span>
    <span class="variable">$requete</span> = <span class="string">"SELECT mot_de_passe FROM utilisateurs WHERE nom_utilisateur = ?"</span>;
    <span class="variable">$utilisateur</span> = <span class="comment">/* résultat de la requête */</span>;
    
    <span class="keyword">if</span> (<span class="variable">$utilisateur</span>) {
        <span class="comment">// Vérification du mot de passe</span>
        <span class="keyword">if</span> (<span class="function">password_verify</span>(<span class="variable">$mot_de_passe_saisi</span>, <span class="variable">$utilisateur</span>[<span class="string">'mot_de_passe'</span>])) {
            <span class="comment">// Authentification réussie</span>
            <span class="function">echo</span> <span class="string">'Connexion réussie !'</span>;
            <span class="keyword">return</span> <span class="constant">true</span>;
        }
    }
    
    <span class="comment">// Échec de l'authentification</span>
    <span class="function">echo</span> <span class="string">'Nom d\\'utilisateur ou mot de passe incorrect.'</span>;
    <span class="keyword">return</span> <span class="constant">false</span>;
}

<span class="comment">// Exemple d'utilisation</span>
<span class="function">creerUtilisateur</span>(<span class="string">'john_doe'</span>, <span class="string">'mon_mot_de_passe_secret'</span>);
<span class="function">authentifierUtilisateur</span>(<span class="string">'john_doe'</span>, <span class="string">'mon_mot_de_passe_secret'</span>); <span class="comment">// true</span>
<span class="function">authentifierUtilisateur</span>(<span class="string">'john_doe'</span>, <span class="string">'mauvais_mot_de_passe'</span>); <span class="comment">// false</span>
?&gt;</code></pre>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer un système d'authentification simple utilisant
                        <code>password_hash()</code> et <code>password_verify()</code>.
                    </p>

                    <p class="textExemple">
                        <strong>Instructions :</strong>
                    </p>
                    <ol>
                        <li>Créez une fonction <code>inscrireUtilisateur()</code> qui prend un nom d'utilisateur et un
                            mot de passe, hache le mot de passe et le stocke (simulez le stockage avec un tableau)</li>
                        <li>Créez une fonction <code>connecterUtilisateur()</code> qui vérifie si le nom d'utilisateur
                            existe et si le mot de passe correspond</li>
                        <li>Testez votre système avec plusieurs utilisateurs</li>
                    </ol>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-php">&lt;?php
<span class="variable">$utilisateurs</span> = []; <span class="comment">// Simule une base de données</span>

<span class="keyword">function</span> <span class="function">inscrireUtilisateur</span>(<span class="variable">$nom_utilisateur</span>, <span class="variable">$mot_de_passe</span>) {
    <span class="keyword">global</span> <span class="variable">$utilisateurs</span>;
    
    <span class="comment">// Vérifier si l'utilisateur existe déjà</span>
    <span class="keyword">if</span> (<span class="function">isset</span>(<span class="variable">$utilisateurs</span>[<span class="variable">$nom_utilisateur</span>])) {
        <span class="function">echo</span> <span class="string">"L'utilisateur existe déjà.\\n"</span>;
        <span class="keyword">return</span> <span class="constant">false</span>;
    }
    
    <span class="comment">// Hacher le mot de passe</span>
    <span class="variable">$hash</span> = <span class="function">password_hash</span>(<span class="variable">$mot_de_passe</span>, PASSWORD_DEFAULT);
    
    <span class="comment">// Stocker l'utilisateur</span>
    <span class="variable">$utilisateurs</span>[<span class="variable">$nom_utilisateur</span>] = <span class="variable">$hash</span>;
    <span class="function">echo</span> <span class="string">"Utilisateur '$nom_utilisateur' inscrit avec succès.\\n"</span>;
    <span class="keyword">return</span> <span class="constant">true</span>;
}

<span class="keyword">function</span> <span class="function">connecterUtilisateur</span>(<span class="variable">$nom_utilisateur</span>, <span class="variable">$mot_de_passe</span>) {
    <span class="keyword">global</span> <span class="variable">$utilisateurs</span>;
    
    <span class="comment">// Vérifier si l'utilisateur existe</span>
    <span class="keyword">if</span> (!<span class="function">isset</span>(<span class="variable">$utilisateurs</span>[<span class="variable">$nom_utilisateur</span>])) {
        <span class="function">echo</span> <span class="string">"Utilisateur non trouvé.\\n"</span>;
        <span class="keyword">return</span> <span class="constant">false</span>;
    }
    
    <span class="comment">// Vérifier le mot de passe</span>
    <span class="keyword">if</span> (<span class="function">password_verify</span>(<span class="variable">$mot_de_passe</span>, <span class="variable">$utilisateurs</span>[<span class="variable">$nom_utilisateur</span>])) {
        <span class="function">echo</span> <span class="string">"Connexion réussie pour '$nom_utilisateur'!\\n"</span>;
        <span class="keyword">return</span> <span class="constant">true</span>;
    } <span class="keyword">else</span> {
        <span class="function">echo</span> <span class="string">"Mot de passe incorrect.\\n"</span>;
        <span class="keyword">return</span> <span class="constant">false</span>;
    }
}

<span class="comment">// Tests</span>
<span class="function">inscrireUtilisateur</span>(<span class="string">'alice'</span>, <span class="string">'secret123'</span>);
<span class="function">inscrireUtilisateur</span>(<span class="string">'bob'</span>, <span class="string">'password456'</span>);

<span class="function">connecterUtilisateur</span>(<span class="string">'alice'</span>, <span class="string">'secret123'</span>); <span class="comment">// Réussite</span>
<span class="function">connecterUtilisateur</span>(<span class="string">'alice'</span>, <span class="string">'mauvais'</span>); <span class="comment">// Échec</span>
<span class="function">connecterUtilisateur</span>(<span class="string">'charlie'</span>, <span class="string">'test'</span>); <span class="comment">// Échec (utilisateur inexistant)</span>
?&gt;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Points clés à retenir -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Points clés à retenir</h2>
                <div class="textExemple text-white">
                    <ul>
                        <li><code>password_verify()</code> est la méthode recommandée pour vérifier les mots de passe en
                            PHP</li>
                        <li>Elle fonctionne avec les hachages générés par <code>password_hash()</code></li>
                        <li>Elle gère automatiquement le sel et les différents algorithmes de hachage</li>
                        <li>Elle est résistante aux attaques par timing</li>
                        <li>Ne stockez jamais les mots de passe en clair dans votre base de données</li>
                    </ul>
                </div>
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

/* Couleurs VS Code pour la syntaxe JavaScript */
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
