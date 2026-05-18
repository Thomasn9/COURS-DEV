<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Routing dans Symfony</h1>
                <p class="lesson-meta text-white">Routes • 3 méthodes • Attributs • YAML • XML • Paramètres • Cache</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le routing ?</h2>
                <p class="textExemple">
                    Le routing (système de routage) est le mécanisme qui fait correspondre une URL (ex: <code>/article/42</code>) 
                    à un contrôleur et une méthode spécifique. C'est le cœur de toute application web Symfony.
                </p>
                <p class="textExemple">
                    Symfony propose <strong>3 méthodes principales</strong> pour définir les routes, que nous allons détailler.
                </p>
            </section>

            <!-- Les 3 méthodes de définition des routes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 3 façons de définir une route</h2>
                <div class="textExemple">
                    <p>Symfony offre 3 méthodes principales pour définir les routes :</p>
                    <ul>
                        <li><strong>Attributs PHP (recommandé)</strong> – directement dans le contrôleur, près du code.</li>
                        <li><strong>Fichier YAML</strong> – centralisé dans <code>config/routes.yaml</code>.</li>
                        <li><strong>XML ou PHP</strong> – moins courants, mais disponibles pour certains cas.</li>
                    </ul>
                    <p>Examinons chacune en détail.</p>
                </div>

                <!-- 1. Attributs PHP -->
                <h3 class="text-purple">1. Attributs PHP (méthode recommandée)</h3>
                <p class="textExemple">
                    Depuis PHP 8, les attributs permettent d’annoter directement les classes et méthodes. C’est la méthode privilégiée par l’équipe Symfony.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/Controller/BlogController.php
namespace App\Controller;

use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class BlogController
{
    #[Route('/blog', name: 'blog_list')]
    public function list(): Response
    {
        return new Response('Liste des articles');
    }

    #[Route('/article/{id}', name: 'article_show', requirements: ['id' => '\d+'])]
    public function show(int $id): Response
    {
        return new Response("Article n° $id");
    }
}</code></pre>
                </div>
                <p class="textExemple">
                    <strong>Avantages :</strong> lisibilité, maintenance facilitée (route collée à la méthode), pas de fichier externe, autocomplétion IDE.
                </p>

                <!-- 2. Fichier YAML -->
                <h3 class="text-purple">2. Fichier YAML (centralisé)</h3>
                <p class="textExemple">
                    On place toutes les routes dans <code>config/routes.yaml</code>. Chaque route a un nom, un chemin, un contrôleur et des options.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-yaml"># config/routes.yaml
blog_list:
    path: /blog
    controller: App\Controller\BlogController::list

article_show:
    path: /article/{id}
    controller: App\Controller\BlogController::show
    requirements:
        id: '\d+'

# Préfixage de groupe avec 'prefix' (optionnel)
admin:
    resource: '../src/Controller/Admin/'
    type: attribute
    prefix: /admin</code></pre>
                </div>
                <p class="textExemple">
                    <strong>Avantages :</strong> toutes les routes sont centralisées, ce qui peut être pratique pour des équipes qui préfèrent une configuration unique. 
                    <strong>Inconvénients :</strong> déconnexion entre la route et le contrôleur, plus de fichiers à maintenir.
                </p>

                <!-- 3. XML ou PHP -->
                <h3 class="text-purple">3. Fichier XML ou PHP (alternatives)</h3>
                <p class="textExemple">
                    Symfony accepte aussi les fichiers XML ou PHP pour définir les routes, mais ils sont beaucoup moins utilisés. On les trouve parfois dans des bundles tiers.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-xml">&lt;!-- config/routes.xml --&gt;
&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;routes xmlns="http://symfony.com/schema/routing"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://symfony.com/schema/routing
        https://symfony.com/schema/routing/routing-1.0.xsd"&gt;

    &lt;route id="blog_list" path="/blog" controller="App\Controller\BlogController::list"/&gt;
    &lt;route id="article_show" path="/article/{id}" controller="App\Controller\BlogController::show"&gt;
        &lt;requirement key="id"&gt;\d+&lt;/requirement&gt;
    &lt;/route&gt;
&lt;/routes&gt;</code></pre>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// config/routes.php
use Symfony\Component\Routing\Loader\Configurator\RoutingConfigurator;

return function (RoutingConfigurator $routes) {
    $routes->add('blog_list', '/blog')
        ->controller([BlogController::class, 'list']);
    
    $routes->add('article_show', '/article/{id}')
        ->controller([BlogController::class, 'show'])
        ->requirements(['id' => '\d+']);
};</code></pre>
                </div>
                <p class="textExemple">
                    Ces méthodes sont moins courantes, mais utiles si vous souhaitez générer des routes dynamiquement ou éviter le parsing YAML/XML.
                </p>
            </section>

            <!-- Paramètres dynamiques (communs) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Paramètres dynamiques dans l'URL</h2>
                <p class="textExemple">
                    Quelle que soit la méthode choisie, on peut capturer des parties variables de l'URL avec des <strong>paramètres entre accolades</strong>.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Attribut
#[Route('/article/{id}', name: 'article_show', requirements: ['id' => '\d+'])]
public function show(int $id): Response { ... }

// YAML
article_show:
    path: /article/{id}
    controller: App\Controller\BlogController::show
    requirements: { id: '\d+' }

// XML
&lt;route id="article_show" path="/article/{id}" controller="..."&gt;
    &lt;requirement key="id"&gt;\d+&lt;/requirement&gt;
&lt;/route&gt;</code></pre>
                </div>
            </section>

            <!-- Nom des routes et génération d'URL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Nom des routes et génération d'URL</h2>
                <p class="textExemple">
                    Le nom de la route (ex: <code>article_show</code>) est essentiel pour générer des URLs sans les coder en dur.
                </p>
                <h3 class="text-purple">Dans un template Twig :</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-twig">{{ path('article_show', {id: 42}) }}
{# Génère : /article/42 #}</code></pre>
                </div>
                <h3 class="text-purple">Dans un contrôleur :</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php">$this->generateUrl('article_show', ['id' => 42]);</code></pre>
                </div>
            </section>

            <!-- Méthodes HTTP et autres options -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Restreindre les méthodes HTTP</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Attribut
#[Route('/api/article', name: 'api_create', methods: ['POST'])]

// YAML
api_create:
    path: /api/article
    controller: ...
    methods: ['POST']

// XML
&lt;route id="api_create" path="/api/article" controller="..." methods="POST"/&gt;</code></pre>
                </div>
            </section>

            <!-- Debug des routes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Debugger les routes</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console debug:router</span>
<span class="bash-comment"># Affiche toutes les routes (quelle que soit leur origine)</span>

<span class="bash-prompt">$</span> <span class="bash-command">php bin/console router:match /article/42</span>
<span class="bash-comment"># Teste quelle route correspond à une URL donnée</span></code></pre>
                </div>
            </section>

            <!--  Problème fréquent : le cache Symfony -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple"> Problème fréquent : le cache Symfony empêche la découverte des nouvelles routes</h2>
                <p class="textExemple">
                    Il arrive souvent qu’après avoir créé un nouveau contrôleur ou modifié une route, celle-ci n’apparaisse pas dans <code>debug:router</code> et génère une erreur 404. La cause la plus courante est un <strong>cache Symfony obsolète</strong>.
                </p>
                <h3 class="text-purple">Pourquoi cela arrive ?</h3>
                <p class="textExemple">
                    Symfony met en cache la configuration des routes pour des raisons de performances. Lorsque vous ajoutez ou modifiez une route, ce cache n’est pas automatiquement rafraîchi, surtout en environnement de production (et parfois même en développement selon votre configuration). Le framework continue donc d’utiliser l’ancienne version des routes.
                </p>
                <h3 class="text-purple">Symptômes typiques</h3>
                <ul>
                    <li>La commande <code>php bin/console debug:router</code> n’affiche <strong>pas</strong> votre nouvelle route.</li>
                    <li>Vous accédez à l’URL et obtenez une <strong>erreur 404</strong> (NotFoundHttpException).</li>
                    <li>Pourtant votre code (contrôleur + attribut <code>#[Route]</code>) est parfaitement valide.</li>
                </ul>
                <h3 class="text-purple">Solution : vider le cache</h3>
                <p class="textExemple">
                    La commande suivante nettoie le cache de Symfony et force la reconstruction des routes :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console cache:clear</span></code></pre>
                </div>
                <p class="textExemple">
                    Selon votre environnement, vous pouvez avoir besoin d’ajouter l’option <code>--env=prod</code> (ou <code>dev</code> qui est l’environnement par défaut) :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console cache:clear --env=dev</span></code></pre>
                </div>
                <p class="textExemple">
                    Après avoir vidé le cache, relancez <code>php bin/console debug:router</code>. Votre route devrait maintenant apparaître.
                </p>
                <h3 class="text-purple">Bonnes pratiques pour éviter ce désagrément</h3>
                <ul>
                    <li><strong>En développement</strong>, utilisez l’environnement <code>dev</code> (par défaut) qui est plus tolérant, mais pas toujours automatique sur les routes.</li>
                    <li><strong>Après chaque création/modification de route</strong>, exécutez systématiquement <code>cache:clear</code> pour être certain que la nouvelle configuration est prise en compte.</li>
                    <li><strong>Pensez à redémarrer le serveur Symfony</strong> (<code>symfony server:start</code> ou <code>Ctrl+C</code> puis relance) après avoir modifié des fichiers de configuration (<code>config/routes.yaml</code>, <code>config/services.yaml</code>, etc.).</li>
                    <li><strong>Utilisez la commande <code>php bin/console debug:router</code> comme outil de diagnostic</strong> : si la route n’y figure pas, le problème vient du cache ou du chargement des fichiers (mauvais namespace, mauvais emplacement).</li>
                </ul>
                <div class="code-example">
                    <h4 class="text-purple">Exemple d’erreur typique dans les logs</h4>
                    <pre v-pre><code class="language-plaintext">Uncaught PHP Exception Symfony\Component\HttpKernel\Exception\NotFoundHttpException: "No route found for "GET /ma-nouvelle-page""</code></pre>
                </div>
                <p class="textExemple">
                    Cette erreur disparaît immédiatement après un <code>cache:clear</code> suivi d’un redémarrage du serveur.
                </p>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li><strong>Privilégiez les attributs PHP</strong> – c’est la méthode recommandée et la plus maintenable.</li>
                    <li><strong>Donnez des noms explicites aux routes</strong> – facilite la génération d’URL.</li>
                    <li><strong>Restreignez les méthodes HTTP</strong> pour plus de sécurité.</li>
                    <li><strong>Utilisez des préfixes de groupe</strong> (attribut sur classe) pour les contrôleurs d’administration ou d’API.</li>
                    <li><strong>Versionnez les routes d’API</strong> : <code>/v1/articles</code>, <code>/v2/articles</code>.</li>
                    <li><strong>En cas de route manquante, pensez au cache</strong> – <code>php bin/console cache:clear</code> est votre premier réflexe.</li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Le routing de Symfony est flexible et s’adapte à vos préférences :
                </p>
                <ul>
                    <li><strong>Attributs PHP</strong> → pour la clarté et la proximité avec le contrôleur (recommandé).</li>
                    <li><strong>YAML</strong> → pour une configuration centralisée (traditionnelle).</li>
                    <li><strong>XML/PHP</strong> → pour des cas particuliers ou la compatibilité avec certains bundles.</li>
                </ul>
                <p class="textExemple">
                    Maîtrisez ces trois méthodes, sachez gérer le cache, et vous saurez naviguer dans n’importe quel projet Symfony.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyRoutingLesson',

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
                    const languages = ['php', 'yaml', 'xml', 'twig', 'bash', 'plaintext'];
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
/* Styles identiques – inchangés */
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

.border-purple {
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.text-purple { color: #6A3093 !important; }
.text-white  { color: white !important; }

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