<template>
    <div class="lesson-container">
        <article class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header bg-gradient-primary">
                <h1 class="text-white">Les superglobales SESSION en PHP</h1>
                <p class="lesson-meta text-white">
                    <span>Niveau : Intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>
                    La superglobale <code>$_SESSION</code> en PHP permet de conserver des données d'une page à l'autre
                    pendant la durée de visite d'un utilisateur. C'est un mécanisme essentiel pour maintenir l'état
                    de l'utilisateur dans les applications web.
                </p>
            </section>

            <!-- Qu'est-ce qu'une session ? -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Qu'est-ce qu'une session ?</h2>
                <p>
                    Une session PHP est un moyen de stocker des informations sur l'utilisateur à travers plusieurs pages.
                    Contrairement aux cookies qui sont stockés côté client, les sessions sont stockées côté serveur.
                </p>
                
                <div class="code-example">
                    <h3 class="text-purple">Fonctionnement des sessions</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Le serveur génère un ID de session unique</span>
<span class="comment">// Cet ID est stocké dans un cookie côté client</span>
<span class="comment">// À chaque requête, le client envoie l'ID de session</span>
<span class="comment">// Le serveur récupère les données correspondantes</span>
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Démarrer une session -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Démarrer une session</h2>
                <p>
                    Avant d'utiliser <code>$_SESSION</code>, vous devez toujours démarrer la session avec
                    <code>session_start()</code>.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Initialisation de session</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Démarrer la session (doit être appelé avant tout output)</span>
<span class="function">session_start</span>();

<span class="comment">// Vérifier si la session est déjà active</span>
<span class="keyword">if</span> (<span class="function">session_status</span>() === PHP_SESSION_NONE) {
    <span class="function">session_start</span>();
}

<span class="comment">// Maintenant vous pouvez utiliser $_SESSION</span>
<span class="variable">$_SESSION</span>[<span class="string">'username'</span>] = <span class="string">'john_doe'</span>;
<span class="variable">$_SESSION</span>[<span class="string">'login_time'</span>] = <span class="function">time</span>();

<span class="function">echo</span> <span class="string">"Session démarrée avec succès!"</span>;
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Stocker et récupérer des données -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Stocker et récupérer des données</h2>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">Page de connexion</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();

<span class="comment">// Simulation d'une connexion utilisateur</span>
<span class="variable">$username</span> = <span class="string">"marie_dupont"</span>;
<span class="variable">$email</span> = <span class="string">"marie@example.com"</span>;
<span class="variable">$role</span> = <span class="string">"admin"</span>;

<span class="comment">// Stocker les données en session</span>
<span class="variable">$_SESSION</span>[<span class="string">'user'</span>] = [
    <span class="string">'username'</span> => <span class="variable">$username</span>,
    <span class="string">'email'</span> => <span class="variable">$email</span>,
    <span class="string">'role'</span> => <span class="variable">$role</span>,
    <span class="string">'login_time'</span> => <span class="function">date</span>(<span class="string">'Y-m-d H:i:s'</span>)
];

<span class="variable">$_SESSION</span>[<span class="string">'is_logged_in'</span>] = <span class="constant">true</span>;

<span class="function">echo</span> <span class="string">"Utilisateur connecté avec succès!"</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">Page de profil</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();

<span class="comment">// Vérifier si l'utilisateur est connecté</span>
<span class="keyword">if</span> (<span class="keyword">isset</span>(<span class="variable">$_SESSION</span>[<span class="string">'is_logged_in'</span>]) && <span class="variable">$_SESSION</span>[<span class="string">'is_logged_in'</span>]) {
    
    <span class="variable">$user</span> = <span class="variable">$_SESSION</span>[<span class="string">'user'</span>];
    
    <span class="function">echo</span> <span class="string">"Bienvenue "</span> . <span class="variable">$user</span>[<span class="string">'username'</span>] . <span class="string">"!"</span>;
    <span class="function">echo</span> <span class="string">"&lt;br&gt;Email: "</span> . <span class="variable">$user</span>[<span class="string">'email'</span>];
    <span class="function">echo</span> <span class="string">"&lt;br&gt;Rôle: "</span> . <span class="variable">$user</span>[<span class="string">'role'</span>];
    <span class="function">echo</span> <span class="string">"&lt;br&gt;Connecté depuis: "</span> . <span class="variable">$user</span>[<span class="string">'login_time'</span>];
    
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Veuillez vous connecter pour accéder à cette page."</span>;
}
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des erreurs et sécurité -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Gestion des erreurs et sécurité</h2>

                <div class="code-example">
                    <h3 class="text-purple">Vérifications de sécurité</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();

<span class="comment">// Vérifier sécurité avec isset() et !empty()</span>
<span class="keyword">if</span> (<span class="keyword">isset</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>]) && !<span class="function">empty</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>])) {
    
    <span class="comment">// Validation des données de session</span>
    <span class="keyword">if</span> (<span class="function">is_array</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>])) {
        <span class="variable">$username</span> = <span class="function">htmlspecialchars</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>][<span class="string">'username'</span>]);
        <span class="variable">$email</span> = <span class="function">filter_var</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>][<span class="string">'email'</span>], FILTER_VALIDATE_EMAIL);
        
        <span class="keyword">if</span> (<span class="variable">$email</span>) {
            <span class="function">echo</span> <span class="string">"Utilisateur valide: "</span> . <span class="variable">$username</span>;
        } <span class="keyword">else</span> {
            <span class="function">echo</span> <span class="string">"Email invalide dans la session"</span>;
        }
    }
    
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Aucun utilisateur en session"</span>;
}

<span class="comment">// Régénération de l'ID de session pour la sécurité</span>
<span class="function">session_regenerate_id</span>(<span class="constant">true</span>);
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Détruire une session -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Détruire une session</h2>
                <p>
                    Il est important de bien détruire les sessions pour des raisons de sécurité,
                    notamment lors de la déconnexion d'un utilisateur.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Déconnexion complète</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();

<span class="comment">// Méthode 1: Supprimer toutes les variables de session</span>
<span class="variable">$_SESSION</span> = [];

<span class="comment">// Méthode 2: Supprimer le cookie de session</span>
<span class="keyword">if</span> (<span class="keyword">isset</span>(<span class="variable">$_COOKIE</span>[<span class="function">session_name</span>()])) {
    <span class="function">setcookie</span>(<span class="function">session_name</span>(), <span class="string">''</span>, <span class="function">time</span>() - <span class="number">3600</span>, <span class="string">'/'</span>);
}

<span class="comment">// Méthode 3: Détruire la session complètement</span>
<span class="function">session_destroy</span>();

<span class="function">echo</span> <span class="string">"Déconnexion réussie!"</span>;
<span class="function">header</span>(<span class="string">'Location: login.php'</span>); <span class="comment">// Redirection</span>
<span class="keyword">exit</span>;
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Configuration des sessions -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Configuration des sessions</h2>

                <div class="code-example">
                    <h3 class="text-purple">Paramètres de session dans php.ini</h3>
                    <pre><code class="language-ini"><span class="comment">; Durée de vie du cookie de session (en secondes)</span>
<span class="ini-keyword">session.cookie_lifetime</span> = <span class="ini-number">0</span> <span class="comment">; 0 = jusqu'à la fermeture du navigateur</span>

<span class="comment">; Durée de vie de la session côté serveur (en secondes)</span>
<span class="ini-keyword">session.gc_maxlifetime</span> = <span class="ini-number">1440</span> <span class="comment">; 24 minutes par défaut</span>

<span class="comment">; Utiliser uniquement des cookies pour les sessions</span>
<span class="ini-keyword">session.use_only_cookies</span> = <span class="ini-number">1</span>

<span class="comment">; Protection contre les attaques de fixation de session</span>
<span class="ini-keyword">session.use_strict_mode</span> = <span class="ini-number">1</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Configuration programmatique</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Configurer les paramètres de session avant session_start()</span>
<span class="function">ini_set</span>(<span class="string">'session.cookie_lifetime'</span>, <span class="number">86400</span>); <span class="comment">// 24 heures</span>
<span class="function">ini_set</span>(<span class="string">'session.gc_maxlifetime'</span>, <span class="number">86400</span>); <span class="comment">// 24 heures</span>

<span class="comment">// Paramètres de sécurité</span>
<span class="function">ini_set</span>(<span class="string">'session.use_only_cookies'</span>, <span class="number">1</span>);
<span class="function">ini_set</span>(<span class="string">'session.use_strict_mode'</span>, <span class="number">1</span>);
<span class="function">ini_set</span>(<span class="string">'session.cookie_httponly'</span>, <span class="number">1</span>);
<span class="function">ini_set</span>(<span class="string">'session.cookie_secure'</span>, <span class="number">1</span>); <span class="comment">// Uniquement en HTTPS</span>

<span class="function">session_start</span>();
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li>Toujours appeler <code>session_start()</code> au début du script, avant tout output</li>
                    <li>Utiliser <code>session_regenerate_id(true)</code> après une connexion pour prévenir les attaques de fixation</li>
                    <li>Ne stockez jamais d'informations sensibles comme des mots de passe en session</li>
                    <li>Valider et filtrer les données stockées en session</li>
                    <li>Détruire proprement les sessions lors de la déconnexion</li>
                    <li>Utiliser <code>session.use_strict_mode</code> pour la sécurité</li>
                    <li>Limiter la quantité de données stockées en session</li>
                </ul>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1: Système de connexion simple</h3>
                    <p>
                        Créez un système de connexion avec trois pages :
                    </p>
                    <ul>
                        <li><strong>login.php</strong> : Formulaire de connexion</li>
                        <li><strong>dashboard.php</strong> : Page sécurisée après connexion</li>
                        <li><strong>logout.php</strong> : Page de déconnexion</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">login.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();
<span class="keyword">if</span> (<span class="keyword">isset</span>(<span class="variable">$_POST</span>[<span class="string">'login'</span>])) {
    <span class="variable">$username</span> = <span class="function">trim</span>(<span class="variable">$_POST</span>[<span class="string">'username'</span>]);
    <span class="variable">$password</span> = <span class="function">trim</span>(<span class="variable">$_POST</span>[<span class="string">'password'</span>]);
    
    <span class="comment">// Validation simple</span>
    <span class="keyword">if</span> (<span class="variable">$username</span> === <span class="string">'admin'</span> && <span class="variable">$password</span> === <span class="string">'password123'</span>) {
        <span class="variable">$_SESSION</span>[<span class="string">'user'</span>] = <span class="variable">$username</span>;
        <span class="variable">$_SESSION</span>[<span class="string">'login_time'</span>] = <span class="function">time</span>();
        <span class="function">session_regenerate_id</span>(<span class="constant">true</span>);
        <span class="function">header</span>(<span class="string">'Location: dashboard.php'</span>);
        <span class="keyword">exit</span>;
    } <span class="keyword">else</span> {
        <span class="variable">$error</span> = <span class="string">"Identifiants incorrects"</span>;
    }
}
<span class="php-tag">?&gt;</span>
<span class="comment">&lt;!-- Formulaire HTML --&gt;</span></code></pre>

                            <h4 class="text-purple">dashboard.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();
<span class="keyword">if</span> (!<span class="keyword">isset</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>])) {
    <span class="function">header</span>(<span class="string">'Location: login.php'</span>);
    <span class="keyword">exit</span>;
}

<span class="function">echo</span> <span class="string">"Bienvenue "</span> . <span class="function">htmlspecialchars</span>(<span class="variable">$_SESSION</span>[<span class="string">'user'</span>]) . <span class="string">"!"</span>;
<span class="function">echo</span> <span class="string">"&lt;br&gt;Connecté depuis: "</span> . <span class="function">date</span>(<span class="string">'Y-m-d H:i:s'</span>, <span class="variable">$_SESSION</span>[<span class="string">'login_time'</span>]);
<span class="function">echo</span> <span class="string">'&lt;br&gt;&lt;a href="logout.php"&gt;Déconnexion&lt;/a&gt;'</span>;
<span class="php-tag">?&gt;</span></code></pre>

                            <h4 class="text-purple">logout.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">session_start</span>();
<span class="variable">$_SESSION</span> = [];
<span class="function">session_destroy</span>();
<span class="function">header</span>(<span class="string">'Location: login.php'</span>);
<span class="keyword">exit</span>;
<span class="php-tag">?&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p>
                    Les sessions PHP sont un outil puissant pour maintenir l'état des utilisateurs dans vos applications web.
                    Elles permettent de créer des expériences personnalisées et sécurisées. Cependant, une bonne
                    compréhension de leur fonctionnement et des mesures de sécurité associées est essentielle
                    pour développer des applications robustes.
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
.code-example, .code-block {
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
    white-space: pre-wrap; /* Permet le retour à la ligne */
    word-wrap: break-word; /* Casse les mots longs */
    word-break: break-word; /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap; /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
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
.html-tag { color: #808080 !important; }
.class-name { color: #4ec9b0 !important; }
.ini-keyword { color: #9cdcfe !important; }
.ini-number { color: #b5cea8 !important; }

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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>