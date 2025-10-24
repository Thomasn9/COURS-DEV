<template>
    <div class="lesson-container">
        <article class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header bg-gradient-primary">
                <h1 class="text-white">La constante magique __DIR__ en PHP</h1>
                <p class="lesson-meta text-white">
                    <span>Niveau : Intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>
                    <code>__DIR__</code> est une constante magique en PHP qui retourne le chemin du dossier 
                    contenant le fichier en cours d'exécution. C'est un outil essentiel pour la gestion 
                    des chemins de fichiers dans vos applications PHP.
                </p>
            </section>

            <!-- Qu'est-ce que __DIR__ ? -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Qu'est-ce que __DIR__ ?</h2>
                <p>
                    <code>__DIR__</code> est une constante prédéfinie qui existe depuis PHP 5.3.0.
                    Elle retourne le chemin absolu du dossier parent du fichier où elle est utilisée,
                    sans le slash final (sauf à la racine du système).
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Utilisation basique</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Affiche le chemin du dossier contenant ce fichier</span>
<span class="function">echo</span> <span class="constant">__DIR__</span>;
<span class="comment">// Exemple: /var/www/html/mon-site/includes</span>

<span class="comment">// Comparaison avec __FILE__</span>
<span class="function">echo</span> <span class="constant">__FILE__</span>;
<span class="comment">// Exemple: /var/www/html/mon-site/includes/config.php</span>

<span class="comment">// __DIR__ équivaut à dirname(__FILE__)</span>
<span class="function">echo</span> <span class="function">dirname</span>(<span class="constant">__FILE__</span>);
<span class="comment">// Donne le même résultat que __DIR__</span>
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Différences entre constantes magiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Constantes magiques comparées</h2>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">__DIR__ vs __FILE__</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Fichier: /home/user/projet/index.php</span>

<span class="function">echo</span> <span class="string">"__DIR__: "</span> . <span class="constant">__DIR__</span>;
<span class="comment">// Affiche: /home/user/projet</span>

<span class="function">echo</span> <span class="string">"__FILE__: "</span> . <span class="constant">__FILE__</span>;
<span class="comment">// Affiche: /home/user/projet/index.php</span>

<span class="function">echo</span> <span class="string">"dirname(__FILE__): "</span> . <span class="function">dirname</span>(<span class="constant">__FILE__</span>);
<span class="comment">// Affiche: /home/user/projet (identique à __DIR__)</span>
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">Autres constantes magiques</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// __LINE__ - Ligne courante dans le fichier</span>
<span class="function">echo</span> <span class="string">"Ligne: "</span> . <span class="constant">__LINE__</span>;

<span class="comment">// __FUNCTION__ - Nom de la fonction courante</span>
<span class="keyword">function</span> <span class="function">maFonction</span>() {
    <span class="function">echo</span> <span class="string">"Fonction: "</span> . <span class="constant">__FUNCTION__</span>;
}

<span class="comment">// __CLASS__ - Nom de la classe courante</span>
<span class="keyword">class</span> <span class="class-name">MaClasse</span> {
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">getClass</span>() {
        <span class="function">echo</span> <span class="string">"Classe: "</span> . <span class="constant">__CLASS__</span>;
    }
}

<span class="comment">// __NAMESPACE__ - Nom du namespace courant</span>
<span class="function">echo</span> <span class="string">"Namespace: "</span> . <span class="constant">__NAMESPACE__</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Cas d'utilisation pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Cas d'utilisation pratiques</h2>

                <div class="code-example">
                    <h3 class="text-purple">Inclusion de fichiers</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Méthode RISQUÉE - chemins relatifs</span>
<span class="function">include</span> <span class="string">'../config/database.php'</span>;
<span class="function">include</span> <span class="string">'../../lib/functions.php'</span>;

<span class="comment">// Méthode SÉCURISÉE - avec __DIR__</span>
<span class="function">include</span> <span class="constant">__DIR__</span> . <span class="string">'/../config/database.php'</span>;
<span class="function">include</span> <span class="constant">__DIR__</span> . <span class="string">'/../../lib/functions.php'</span>;

<span class="comment">// Ou mieux encore, avec realpath()</span>
<span class="function">include</span> <span class="function">realpath</span>(<span class="constant">__DIR__</span> . <span class="string">'/../config/database.php'</span>);
<span class="php-tag">?&gt;</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Configuration d'application</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Définition des chemins de l'application</span>
<span class="function">define</span>(<span class="string">'APP_ROOT'</span>, <span class="constant">__DIR__</span>);
<span class="function">define</span>(<span class="string">'CONFIG_DIR'</span>, <span class="constant">__DIR__</span> . <span class="string">'/config'</span>);
<span class="function">define</span>(<span class="string">'UPLOAD_DIR'</span>, <span class="constant">__DIR__</span> . <span class="string">'/uploads'</span>);
<span class="function">define</span>(<span class="string">'LOG_DIR'</span>, <span class="constant">__DIR__</span> . <span class="string">'/logs'</span>);

<span class="comment">// Utilisation dans tout le projet</span>
<span class="function">include</span> <span class="constant">CONFIG_DIR</span> . <span class="string">'/database.php'</span>;
<span class="function">include</span> <span class="constant">CONFIG_DIR</span> . <span class="string">'/settings.php'</span>;

<span class="variable">$log_file</span> = <span class="constant">LOG_DIR</span> . <span class="string">'/app.log'</span>;
<span class="variable">$upload_path</span> = <span class="constant">UPLOAD_DIR</span> . <span class="string">'/images'</span>;
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Structure de projet avec __DIR__ -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Structure de projet organisée</h2>

                <div class="code-example">
                    <h3 class="text-purple">Structure de fichiers</h3>
                    <pre><code class="language-php">mon-projet/
├── index.php
├── admin/
│   └── dashboard.php
├── includes/
│   ├── config.php
│   ├── functions.php
│   └── header.php
├── assets/
│   ├── css/
│   └── js/
└── uploads/</code></pre>
                </div>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">index.php</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Définition de la racine du projet</span>
<span class="function">define</span>(<span class="string">'PROJECT_ROOT'</span>, <span class="constant">__DIR__</span>);

<span class="comment">// Inclusion sécurisée des fichiers</span>
<span class="function">require_once</span> <span class="constant">PROJECT_ROOT</span> . <span class="string">'/includes/config.php'</span>;
<span class="function">require_once</span> <span class="constant">PROJECT_ROOT</span> . <span class="string">'/includes/functions.php'</span>;

<span class="function">echo</span> <span class="string">"Racine du projet: "</span> . <span class="constant">PROJECT_ROOT</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">admin/dashboard.php</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Remonter d'un niveau pour atteindre la racine</span>
<span class="function">define</span>(<span class="string">'PROJECT_ROOT'</span>, <span class="function">dirname</span>(<span class="constant">__DIR__</span>));

<span class="comment">// Inclusions fonctionnent depuis n'importe quel dossier</span>
<span class="function">require_once</span> <span class="constant">PROJECT_ROOT</span> . <span class="string">'/includes/config.php'</span>;
<span class="function">require_once</span> <span class="constant">PROJECT_ROOT</span> . <span class="string">'/includes/functions.php'</span>;

<span class="function">echo</span> <span class="string">"Dashboard chargé depuis: "</span> . <span class="constant">__DIR__</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Bonnes pratiques avec __DIR__</h2>

                <div class="code-example">
                    <h3 class="text-purple">Validation et sécurisation</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// 1. Toujours utiliser realpath() pour la validation</span>
<span class="variable">$config_path</span> = <span class="function">realpath</span>(<span class="constant">__DIR__</span> . <span class="string">'/../config/app.php'</span>);
<span class="keyword">if</span> (<span class="variable">$config_path</span> !== <span class="constant">false</span> && <span class="function">file_exists</span>(<span class="variable">$config_path</span>)) {
    <span class="function">require_once</span> <span class="variable">$config_path</span>;
} <span class="keyword">else</span> {
    <span class="keyword">throw</span> <span class="keyword">new</span> <span class="class-name">Exception</span>(<span class="string">'Fichier de configuration non trouvé'</span>);
}

<span class="comment">// 2. Normalisation des chemins</span>
<span class="variable">$upload_dir</span> = <span class="function">rtrim</span>(<span class="constant">__DIR__</span>, <span class="string">'/'</span>) . <span class="string">'/uploads'</span>;
<span class="variable">$log_file</span> = <span class="function">rtrim</span>(<span class="constant">__DIR__</span>, <span class="string">'/'</span>) . <span class="string">'/logs/app.log'</span>;

<span class="comment">// 3. Utilisation avec dirname() pour les niveaux supérieurs</span>
<span class="variable">$project_root</span> = <span class="function">dirname</span>(<span class="constant">__DIR__</span>); <span class="comment">// Remonte d'un niveau</span>
<span class="variable">$parent_dir</span> = <span class="function">dirname</span>(<span class="constant">__DIR__</span>, <span class="number">2</span>); <span class="comment">// Remonte de deux niveaux (PHP 7.0+)</span>

<span class="comment">// 4. Stockage en constante pour performance</span>
<span class="function">define</span>(<span class="string">'CURRENT_DIR'</span>, <span class="constant">__DIR__</span>);
<span class="function">define</span>(<span class="string">'PARENT_DIR'</span>, <span class="function">dirname</span>(<span class="constant">__DIR__</span>));
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Exemples avancés -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exemples avancés</h2>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">Autoloader personnalisé</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="function">spl_autoload_register</span>(<span class="keyword">function</span> (<span class="variable">$class_name</span>) {
    <span class="comment">// Convertir le namespace en chemin de fichier</span>
    <span class="variable">$file</span> = <span class="constant">__DIR__</span> . <span class="string">'/src/'</span> . <span class="function">str_replace</span>(<span class="string">'\\'</span>, <span class="string">'/'</span>, <span class="variable">$class_name</span>) . <span class="string">'.php'</span>;
    
    <span class="keyword">if</span> (<span class="function">file_exists</span>(<span class="variable">$file</span>)) {
        <span class="function">require_once</span> <span class="variable">$file</span>;
    }
});

<span class="comment">// Utilisation</span>
<span class="variable">$user</span> = <span class="keyword">new</span> <span class="class-name">App\Models\User</span>(); <span class="comment">// Charge /src/App/Models/User.php</span>
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">Gestionnaire de logs</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">Logger</span> {
    <span class="keyword">private</span> <span class="variable">$log_file</span>;
    
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">__construct</span>(<span class="variable">$filename</span> = <span class="string">'app.log'</span>) {
        <span class="variable">$log_dir</span> = <span class="constant">__DIR__</span> . <span class="string">'/logs'</span>;
        
        <span class="comment">// Créer le dossier logs s'il n'existe pas</span>
        <span class="keyword">if</span> (!<span class="function">is_dir</span>(<span class="variable">$log_dir</span>)) {
            <span class="function">mkdir</span>(<span class="variable">$log_dir</span>, <span class="number">0755</span>, <span class="constant">true</span>);
        }
        
        <span class="variable">$this</span>-><span class="property">log_file</span> = <span class="variable">$log_dir</span> . <span class="string">'/'</span> . <span class="variable">$filename</span>;
    }
    
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">log</span>(<span class="variable">$message</span>) {
        <span class="variable">$timestamp</span> = <span class="function">date</span>(<span class="string">'Y-m-d H:i:s'</span>);
        <span class="variable">$log_entry</span> = <span class="string">"[<span class="variable">$timestamp</span>] <span class="variable">$message</span>"</span> . PHP_EOL;
        <span class="function">file_put_contents</span>(<span class="variable">$this</span>-><span class="property">log_file</span>, <span class="variable">$log_entry</span>, FILE_APPEND);
    }
}

<span class="variable">$logger</span> = <span class="keyword">new</span> <span class="class-name">Logger</span>();
<span class="variable">$logger</span>-><span class="function">log</span>(<span class="string">"Application démarrée"</span>);
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Pièges et erreurs courantes -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Pièges et erreurs courantes</h2>

                <div class="code-example">
                    <h3 class="text-purple">À éviter</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// 1. Oublier le slash lors de la concaténation</span>
<span class="function">include</span> <span class="constant">__DIR__</span> . <span class="string">'config.php'</span>; <span class="comment">// ERREUR: /pathconfig.php</span>
<span class="function">include</span> <span class="constant">__DIR__</span> . <span class="string">'/config.php'</span>; <span class="comment">// CORRECT: /path/config.php</span>

<span class="comment">// 2. Utiliser __DIR__ dans des fonctions incluses</span>
<span class="keyword">function</span> <span class="function">chargerConfig</span>() {
    <span class="comment">// __DIR__ réfère au fichier où cette fonction est DÉFINIE</span>
    <span class="function">include</span> <span class="constant">__DIR__</span> . <span class="string">'/config.php'</span>;
}

<span class="comment">// 3. Ne pas valider l'existence des fichiers</span>
<span class="function">include</span> <span class="constant">__DIR__</span> . <span class="string">'/fichier_inexistant.php'</span>; <span class="comment">// Warning/Error</span>

<span class="comment">// 4. Confusion entre __DIR__ et getcwd()</span>
<span class="function">echo</span> <span class="constant">__DIR__</span>; <span class="comment">// Dossier du fichier courant</span>
<span class="function">echo</span> <span class="function">getcwd</span>(); <span class="comment">// Dossier de travail courant (peut être différent)</span>
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1: Configuration d'application</h3>
                    <p>
                        Créez un système de configuration qui définit automatiquement les chemins 
                        principaux de votre application en utilisant <code>__DIR__</code>.
                    </p>

                    <details class="solution">
                        <summary class="btn btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// config/paths.php</span>
<span class="function">define</span>(<span class="string">'ROOT_PATH'</span>, <span class="function">dirname</span>(<span class="constant">__DIR__</span>));
<span class="function">define</span>(<span class="string">'APP_PATH'</span>, <span class="constant">ROOT_PATH</span> . <span class="string">'/app'</span>);
<span class="function">define</span>(<span class="string">'CONFIG_PATH'</span>, <span class="constant">ROOT_PATH</span> . <span class="string">'/config'</span>);
<span class="function">define</span>(<span class="string">'PUBLIC_PATH'</span>, <span class="constant">ROOT_PATH</span> . <span class="string">'/public'</span>);
<span class="function">define</span>(<span class="string">'STORAGE_PATH'</span>, <span class="constant">ROOT_PATH</span> . <span class="string">'/storage'</span>);
<span class="function">define</span>(<span class="string">'VENDOR_PATH'</span>, <span class="constant">ROOT_PATH</span> . <span class="string">'/vendor'</span>);

<span class="comment">// Validation des dossiers requis</span>
<span class="variable">$required_dirs</span> = [<span class="constant">APP_PATH</span>, <span class="constant">CONFIG_PATH</span>, <span class="constant">PUBLIC_PATH</span>, <span class="constant">STORAGE_PATH</span>];
<span class="keyword">foreach</span> (<span class="variable">$required_dirs</span> <span class="keyword">as</span> <span class="variable">$dir</span>) {
    <span class="keyword">if</span> (!<span class="function">is_dir</span>(<span class="variable">$dir</span>)) {
        <span class="function">mkdir</span>(<span class="variable">$dir</span>, <span class="number">0755</span>, <span class="constant">true</span>);
    }
}

<span class="function">echo</span> <span class="string">"Application configurée avec succès!"</span>;
<span class="function">echo</span> <span class="string">"Racine: "</span> . <span class="constant">ROOT_PATH</span>;
<span class="php-tag">?&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p>
                    La constante magique <code>__DIR__</code> est un outil indispensable pour la gestion 
                    des chemins de fichiers en PHP. Elle offre une manière fiable et portable de référencer 
                    des fichiers et dossiers, rendant votre code plus robuste et maintenable.
                </p>
                <p>
                    En combinant <code>__DIR__</code> avec des fonctions comme <code>realpath()</code>, 
                    <code>dirname()</code> et des validations appropriées, vous pouvez créer des applications 
                    PHP solides qui fonctionnent correctement quel que soit l'environnement de déploiement.
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
.property { color: #9cdcfe !important; }
.class-name { color: #4ec9b0 !important; }

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