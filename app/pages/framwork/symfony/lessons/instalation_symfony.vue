<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Installation et Création d'un Projet Symfony</h1>
                <p class="lesson-meta text-white">Maîtrisez les bases de Symfony en créant votre premier projet</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Symfony</h2>
                <p class="textExemple">
                    Symfony est un framework PHP complet qui facilite le développement d'applications web.
                    Il suit les bonnes pratiques du développement web et propose une architecture modulaire.
                </p>
                <p class="textExemple">
                    Dans cette leçon, nous allons voir comment installer Symfony et créer votre premier projet.
                </p>
            </div>

            <!-- Prérequis -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis</h2>
                <p class="textExemple">
                    Avant de commencer, assurez-vous d'avoir les éléments suivants installés sur votre machine :
                </p>
                <ul class="textExemple">
                    <li>PHP 8.2 ou supérieur</li>
                    <li>Composer (gestionnaire de dépendances PHP)</li>
                    <li>Une base de données (MySQL, PostgreSQL, SQLite)</li>
                    <li>Git (pour le contrôle de version)</li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Vérifier l'installation de PHP :</h4>
                    <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php --version</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Vérifier l'installation de Composer :</h4>
                    <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">composer --version</span></code></pre>
                </div>
            </div>

            <!-- Installation de Symfony CLI -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation de Symfony CLI</h2>
                <p class="textExemple">
                    Symfony CLI est un outil en ligne de commande qui facilite la création et la gestion des projets
                    Symfony.
                </p>

                <h3 class="text-purple">Installation sur Windows</h3>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Télécharger et installer Symfony CLI depuis le site officiel</span>
<span class="bash-comment"># Ou utiliser scoop</span>
<span class="bash-prompt">$</span> <span class="bash-command">scoop install symfony-cli</span></code></pre>
                </div>

                <h3 class="text-purple">Installation sur macOS</h3>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Installation avec Homebrew</span>
<span class="bash-prompt">$</span> <span class="bash-command">brew install symfony-cli/tap/symfony-cli</span></code></pre>
                </div>

                <h3 class="text-purple">Installation sur Linux</h3>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Installation avec curl</span>
<span class="bash-prompt">$</span> <span class="bash-command">curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo apt install symfony-cli</span></code></pre>
                </div>

                <p class="textExemple">
                    Après installation, vérifiez que Symfony CLI fonctionne correctement :
                </p>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony --version</span></code></pre>
                </div>
            </div>

            <!-- Création d'un nouveau projet Symfony -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Création d'un nouveau projet Symfony</h2>
                <p class="textExemple">
                    Il existe plusieurs façons de créer un nouveau projet Symfony. Voici les méthodes les plus courantes
                    :
                </p>

                <h3 class="text-purple">Méthode 1 : Utilisation de Symfony CLI (recommandée)</h3>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Créer un nouveau projet Symfony</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony new mon-projet-symfony --webapp</span></code></pre>
                </div>
                <p class="textExemple">
                    L'option <code>--webapp</code> installe une structure de projet complète avec des fonctionnalités
                    web prêtes à l'emploi.
                </p>

                <h3 class="text-purple">Méthode 2 : Utilisation de Composer</h3>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Créer un nouveau projet avec Composer</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer create-project symfony/skeleton:"6.4.*" mon-projet-symfony</span></code></pre>
                </div>

                <h3 class="text-purple">Méthode 3 : Utilisation du Symfony Demo</h3>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Pour un projet avec des exemples de code</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony new mon-projet-symfony --demo</span></code></pre>
                </div>
            </div>

            <!-- Structure du projet -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure du projet Symfony</h2>
                <p class="textExemple">
                    Après la création, votre projet aura la structure suivante :
                </p>
                <div class="code-example">
                    <pre><code class="language-bash">mon-projet-symfony/
├── bin/
│   └── console          <span class="bash-comment"># Console Symfony pour les commandes</span>
├── config/              <span class="bash-comment"># Fichiers de configuration</span>
├── public/
│   └── index.php        <span class="bash-comment"># Point d'entrée de l'application</span>
├── src/                 <span class="bash-comment"># Code source de votre application</span>
├── templates/           <span class="bash-comment"># Templates Twig</span>
├── translations/        <span class="bash-comment"># Fichiers de traduction</span>
├── var/                 
│   └── cache/           <span class="bash-comment"># Cache de l'application</span>
├── vendor/              <span class="bash-comment"># Dépendances Composer</span>
└── .env                 <span class="bash-comment"># Variables d'environnement</span></code></pre>
                </div>
            </div>

            <!-- Démarrage du serveur de développement -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Démarrage du serveur de développement</h2>
                <p class="textExemple">
                    Symfony inclut un serveur web de développement. Pour le démarrer :
                </p>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Se déplacer dans le répertoire du projet</span>
<span class="bash-prompt">$</span> <span class="bash-command">cd mon-projet-symfony</span>

<span class="bash-comment"># Démarrer le serveur de développement</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony server:start</span></code></pre>
                </div>
                <p class="textExemple">
                    Votre application sera accessible à l'adresse : <code>http://localhost:8000</code>
                </p>
            </div>

            <!-- Configuration de la base de données -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Configuration de la base de données</h2>
                <p class="textExemple">
                    Configurez votre base de données dans le fichier <code>.env</code> :
                </p>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># MySQL</span>
DATABASE_URL="mysql://username:password@127.0.0.1:3306/database_name?serverVersion=8.0"

<span class="bash-comment"># PostgreSQL</span>
DATABASE_URL="postgresql://username:password@127.0.0.1:5432/database_name?serverVersion=13&charset=utf8"

<span class="bash-comment"># SQLite</span>
DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"</code></pre>
                </div>

                <p class="textExemple">
                    Créez ensuite la base de données :
                </p>
                <div class="code-example">
                    <pre><code class="language-bash"><span class="bash-comment"># Créer la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">php bin/console doctrine:database:create</span>

<span class="bash-comment"># Créer les tables (si vous avez des entités)</span>
<span class="bash-prompt">$</span> <span class="bash-command">php bin/console doctrine:schema:update --force</span></code></pre>
                </div>
            </div>

            <!-- Commandes Symfony utiles -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Commandes Symfony utiles</h2>
                <p class="textExemple">
                    Voici quelques commandes essentielles pour travailler avec Symfony :
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Lister toutes les commandes</h4>
                        <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console list</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Vérifier les prérequis système</h4>
                        <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony check:requirements</span></code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Créer une entité</h4>
                        <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console make:entity</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Créer un contrôleur</h4>
                        <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console make:controller</span></code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Effacer le cache</h4>
                        <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console cache:clear</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Voir les routes</h4>
                        <pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console debug:router</span></code></pre>
                    </div>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer votre premier projet Symfony et le configurer avec une base de
                        données SQLite.
                    </p>
                    <ol class="textExemple">
                        <li>Installez Symfony CLI sur votre machine</li>
                        <li>Créez un nouveau projet Symfony nommé "mon-blog"</li>
                        <li>Configurez une base de données SQLite</li>
                        <li>Démarrez le serveur de développement</li>
                        <li>Accédez à l'application dans votre navigateur</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Étapes de la solution :</h4>
                        <div class="code-example">
                            <pre><code class="language-bash"><span class="bash-comment"># 1. Créer le projet</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony new mon-blog --webapp</span>

<span class="bash-comment"># 2. Se déplacer dans le répertoire</span>
<span class="bash-prompt">$</span> <span class="bash-command">cd mon-blog</span>

<span class="bash-comment"># 3. Configurer SQLite dans .env</span>
<span class="bash-comment"># Modifier DATABASE_URL pour :</span>
DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"

<span class="bash-comment"># 4. Créer la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">php bin/console doctrine:database:create</span>

<span class="bash-comment"># 5. Démarrer le serveur</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony server:start</span></code></pre>
                        </div>
                        <p class="textExemple">
                            Votre application sera accessible à <code>http://localhost:8000</code>
                        </p>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>
                <p class="textExemple">
                    Félicitations ! Vous avez maintenant installé Symfony et créé votre premier projet.
                    Vous pouvez commencer à développer votre application web.
                </p>

                <h3 class="text-purple">Ressources supplémentaires :</h3>
                <ul class="textExemple">
                    <li><a href="https://symfony.com/doc/current/setup.html" target="_blank"
                            class="btn-purple btn-hover">Documentation officielle de Symfony</a></li>
                    <li><a href="https://symfony.com/doc/current/the-fast-track/index.html" target="_blank"
                            class="btn-purple btn-hover">The Fast Track (tutoriel accéléré)</a></li>
                    <li><a href="https://github.com/symfony/symfony" target="_blank" class="btn-purple btn-hover">Code
                            source sur GitHub</a></li>
                </ul>
            </div>
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

/* COULEURS GIT BASH */
.bash-prompt {
    color: #2ECC71 !important; /* Vert pour le prompt $ */
    font-weight: bold;
}

.bash-command {
    color: #F1C40F !important; /* Jaune pour les commandes */
}

.bash-comment {
    color: #7F8C8D !important; /* Gris pour les commentaires */
    font-style: italic;
}

.bash-string {
    color: #E74C3C !important; /* Rouge pour les chaînes */
}

.bash-keyword {
    color: #3498DB !important; /* Bleu pour les mots-clés */
}

.bash-parameter {
    color: #9B59B6 !important; /* Violet pour les paramètres */
}

.bash-number {
    color: #1ABC9C !important; /* Turquoise pour les nombres */
}

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