<template>
    <div class="lesson-container">
        <article class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header bg-gradient-primary">
                <h1 class="text-white">Les includes en PHP</h1>
                <p class="lesson-meta text-white">
                    <span>Niveau : Débutant</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>
                    Les fonctions d'inclusion en PHP permettent d'insérer le contenu d'un fichier dans un autre.
                    C'est une technique essentielle pour créer des sites web modulaires et maintenables.
                </p>
            </section>

            <!-- Les différentes fonctions d'inclusion -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Les fonctions d'inclusion</h2>
                <p>
                    PHP propose quatre fonctions principales pour inclure des fichiers :
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">include</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Inclut un fichier, génère un warning si non trouvé</span>
<span class="function">include</span> <span class="string">'header.php'</span>;
<span class="function">include</span> <span class="string">'config.php'</span>;

<span class="comment">// Le script continue même si le fichier n'est pas trouvé</span>
<span class="function">echo</span> <span class="string">"Cette ligne s'exécute même si header.php n'existe pas"</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">require</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Inclut un fichier, génère une erreur fatale si non trouvé</span>
<span class="function">require</span> <span class="string">'database.php'</span>;
<span class="function">require</span> <span class="string">'functions.php'</span>;

<span class="comment">// Le script S'ARRÊTE si le fichier n'est pas trouvé</span>
<span class="function">echo</span> <span class="string">"Cette ligne ne s'exécute pas si database.php n'existe pas"</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">include_once</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Inclut le fichier une seule fois</span>
<span class="function">include_once</span> <span class="string">'config.php'</span>;
<span class="function">include_once</span> <span class="string">'config.php'</span>; <span class="comment">// Ne sera pas inclus une deuxième fois</span>

<span class="comment">// Utile pour éviter les redéfinitions de fonctions/classes</span>
<span class="function">include_once</span> <span class="string">'User.php'</span>;
<span class="function">include_once</span> <span class="string">'User.php'</span>; <span class="comment">// Évite l'erreur "class already defined"</span>
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">require_once</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Requiert le fichier une seule fois</span>
<span class="function">require_once</span> <span class="string">'database.php'</span>;
<span class="function">require_once</span> <span class="string">'database.php'</span>; <span class="comment">// Ne sera pas requis une deuxième fois</span>

<span class="comment">// Idéal pour les fichiers critiques qui ne doivent être inclus qu'une fois</span>
<span class="function">require_once</span> <span class="string">'autoload.php'</span>;
<span class="function">require_once</span> <span class="string">'constants.php'</span>;
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Variables et scope -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Variables et scope</h2>
                <p>
                    Les fichiers inclus ont accès à toutes les variables du scope dans lequel ils sont inclus.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Partage de variables</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Fichier principal</span>
<span class="variable">$titre</span> = <span class="string">"Mon Article"</span>;
<span class="variable">$auteur</span> = <span class="string">"Jean Dupont"</span>;
<span class="variable">$date</span> = <span class="string">"2023-10-15"</span>;

<span class="comment">// Inclure un fichier qui utilise ces variables</span>
<span class="function">include</span> <span class="string">'article_template.php'</span>;
<span class="php-tag">?&gt;</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">article_template.php</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Ce fichier a accès aux variables $titre, $auteur, $date</span>
<span class="html-tag">&lt;article class="article"&gt;</span>
    <span class="html-tag">&lt;h2&gt;</span><span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="function">htmlspecialchars</span>(<span class="variable">$titre</span>); <span class="php-tag">?&gt;</span><span class="html-tag">&lt;/h2&gt;</span>
    <span class="html-tag">&lt;p class="auteur"&gt;</span>Par <span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="function">htmlspecialchars</span>(<span class="variable">$auteur</span>); <span class="php-tag">?&gt;</span><span class="html-tag">&lt;/p&gt;</span>
    <span class="html-tag">&lt;p class="date"&gt;</span>Publié le <span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="variable">$date</span>; <span class="php-tag">?&gt;</span><span class="html-tag">&lt;/p&gt;</span>
    <span class="html-tag">&lt;div class="contenu"&gt;</span>
        <span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="variable">$contenu</span> ?? <span class="string">'Contenu non disponible'</span>; <span class="php-tag">?&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
<span class="html-tag">&lt;/article&gt;</span></code></pre>
                </div>
            </section>

            <!-- Retour de valeurs -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Retour de valeurs</h2>
                <p>
                    Les fichiers inclus peuvent retourner des valeurs comme des fonctions.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Inclusion avec retour de valeur</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Fichier principal</span>
<span class="variable">$config</span> = <span class="function">include</span> <span class="string">'config.php'</span>;
<span class="function">var_dump</span>(<span class="variable">$config</span>);

<span class="comment">// Inclure un fichier qui retourne un résultat de calcul</span>
<span class="variable">$resultat</span> = <span class="function">include</span> <span class="string">'calcul.php'</span>;
<span class="function">echo</span> <span class="string">"Résultat: "</span> . <span class="variable">$resultat</span>;
<span class="php-tag">?&gt;</span></code></pre>
                </div>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">config.php</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Retourner un tableau de configuration</span>
<span class="keyword">return</span> [
    <span class="string">'db_host'</span> => <span class="string">'localhost'</span>,
    <span class="string">'db_name'</span> => <span class="string">'mon_site'</span>,
    <span class="string">'db_user'</span> => <span class="string">'root'</span>,
    <span class="string">'db_pass'</span> => <span class="string">''</span>,
    <span class="string">'site_name'</span> => <span class="string">'Mon Site Web'</span>
];
<span class="php-tag">?&gt;</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">calcul.php</h3>
                        <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Effectuer un calcul et retourner le résultat</span>
<span class="variable">$nombre1</span> = <span class="number">10</span>;
<span class="variable">$nombre2</span> = <span class="number">5</span>;
<span class="variable">$resultat</span> = <span class="variable">$nombre1</span> * <span class="variable">$nombre2</span>;

<span class="keyword">return</span> <span class="variable">$resultat</span>; <span class="comment">// Retourne 50</span>
<span class="php-tag">?&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des erreurs -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Gestion des erreurs</h2>

                <div class="code-example">
                    <h3 class="text-purple">Vérification avant inclusion</h3>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$fichier</span> = <span class="string">'mon_fichier.php'</span>;

<span class="comment">// Vérifier si le fichier existe avant de l'inclure</span>
<span class="keyword">if</span> (<span class="function">file_exists</span>(<span class="variable">$fichier</span>)) {
    <span class="function">include</span> <span class="variable">$fichier</span>;
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Le fichier </span><span class="variable">$fichier</span><span class="string"> n'existe pas."</span>;
}

<span class="comment">// Avec require, on peut utiliser un bloc try-catch</span>
<span class="keyword">try</span> {
    <span class="function">require</span> <span class="string">'fichier_important.php'</span>;
} <span class="keyword">catch</span> (<span class="class-name">Throwable</span> <span class="variable">$e</span>) {
    <span class="function">error_log</span>(<span class="string">"Erreur d'inclusion: "</span> . <span class="variable">$e</span>-><span class="function">getMessage</span>());
    <span class="function">echo</span> <span class="string">"Une erreur est survenue lors du chargement."</span>;
}

<span class="comment">// Inclusion conditionnelle avec opérateur ternaire</span>
<span class="variable">$template</span> = <span class="function">file_exists</span>(<span class="string">'template_personnalise.php'</span>) 
    ? <span class="string">'template_personnalise.php'</span> 
    : <span class="string">'template_defaut.php'</span>;
    
<span class="function">include</span> <span class="variable">$template</span>;
<span class="php-tag">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li>Utilisez <code>require_once</code> pour les fichiers critiques (configuration, classes)</li>
                    <li>Utilisez <code>include</code> pour les templates et parties réutilisables</li>
                    <li>Organisez vos fichiers dans des dossiers logiques (includes, templates, classes)</li>
                    <li>Vérifiez l'existence des fichiers avant inclusion quand c'est nécessaire</li>
                    <li>Utilisez des chemins relatifs ou absolus cohérents</li>
                    <li>Évitez les inclusions dynamiques non contrôlées (risque de sécurité)</li>
                    <li>Utilisez <code>return</code> pour les fichiers de configuration</li>
                    <li>Protégez les fichiers sensibles avec <code>.php</code> extension</li>
                </ul>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1: Création d'un site modulaire</h3>
                    <p>
                        Créez une structure de site modulaire avec :
                    </p>
                    <ul>
                        <li>Un header commun avec navigation</li>
                        <li>Un footer commun</li>
                        <li>Une page d'accueil</li>
                        <li>Une page "À propos"</li>
                        <li>Un fichier de configuration</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">config.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// Configuration du site</span>
<span class="keyword">return</span> [
    <span class="string">'site_name'</span> => <span class="string">'Mon Site Modulaire'</span>,
    <span class="string">'author'</span> => <span class="string">'Votre Nom'</span>,
    <span class="string">'year'</span> => <span class="function">date</span>(<span class="string">'Y'</span>)
];
<span class="php-tag">?&gt;</span></code></pre>

                            <h4 class="text-purple">header.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$config</span> = <span class="function">include</span> <span class="string">'config.php'</span>;
<span class="php-tag">?&gt;</span>
<span class="html-tag">&lt;!DOCTYPE html&gt;</span>
<span class="html-tag">&lt;html lang="fr"&gt;</span>
<span class="html-tag">&lt;head&gt;</span>
    <span class="html-tag">&lt;meta charset="UTF-8"&gt;</span>
    <span class="html-tag">&lt;title&gt;</span><span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="variable">$page_title</span> ?? <span class="variable">$config</span>[<span class="string">'site_name'</span>]; <span class="php-tag">?&gt;</span><span class="html-tag">&lt;/title&gt;</span>
<span class="html-tag">&lt;/head&gt;</span>
<span class="html-tag">&lt;body&gt;</span>
    <span class="html-tag">&lt;header&gt;</span>
        <span class="html-tag">&lt;h1&gt;</span><span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="variable">$config</span>[<span class="string">'site_name'</span>]; <span class="php-tag">?&gt;</span><span class="html-tag">&lt;/h1&gt;</span>
        <span class="html-tag">&lt;nav&gt;</span>
            <span class="html-tag">&lt;a href="index.php"&gt;</span>Accueil<span class="html-tag">&lt;/a&gt;</span>
            <span class="html-tag">&lt;a href="about.php"&gt;</span>À propos<span class="html-tag">&lt;/a&gt;</span>
        <span class="html-tag">&lt;/nav&gt;</span>
    <span class="html-tag">&lt;/header&gt;</span>
    <span class="html-tag">&lt;main&gt;</span></code></pre>

                            <h4 class="text-purple">index.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$page_title</span> = <span class="string">'Accueil - Mon Site Modulaire'</span>;
<span class="function">include</span> <span class="string">'header.php'</span>;
<span class="php-tag">?&gt;</span>

<span class="html-tag">&lt;h2&gt;</span>Bienvenue<span class="html-tag">&lt;/h2&gt;</span>
<span class="html-tag">&lt;p&gt;</span>Ceci est la page d'accueil de mon site modulaire.<span class="html-tag">&lt;/p&gt;</span>

<span class="php-tag">&lt;?php</span> <span class="function">include</span> <span class="string">'footer.php'</span>; <span class="php-tag">?&gt;</span></code></pre>

                            <h4 class="text-purple">footer.php</h4>
                            <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="variable">$config</span> = <span class="function">include</span> <span class="string">'config.php'</span>;
<span class="php-tag">?&gt;</span>
    <span class="html-tag">&lt;/main&gt;</span>
    <span class="html-tag">&lt;footer&gt;</span>
        <span class="html-tag">&lt;p&gt;</span>&copy; <span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="variable">$config</span>[<span class="string">'year'</span>]; <span class="php-tag">?&gt;</span> <span class="php-tag">&lt;?php</span> <span class="function">echo</span> <span class="variable">$config</span>[<span class="string">'site_name'</span>]; <span class="php-tag">?&gt;</span><span class="html-tag">&lt;/p&gt;</span>
    <span class="html-tag">&lt;/footer&gt;</span>
<span class="html-tag">&lt;/body&gt;</span>
<span class="html-tag">&lt;/html&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p>
                    Les fonctions d'inclusion en PHP sont fondamentales pour créer des applications web modulaires,
                    maintenables et organisées. En maîtrisant <code>include</code>, <code>require</code>,
                    <code>include_once</code> et <code>require_once</code>, vous pouvez structurer votre code
                    de manière professionnelle et éviter les répétitions.
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
    word-break: break-all; /* Assure la césure des mots */
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