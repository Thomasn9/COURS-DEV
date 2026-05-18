<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Routing dans Symfony</h1>
                <p class="lesson-meta text-white">Routes • Annotations • Attributs • Paramètres • Génération d'URL</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le routing ?</h2>
                <p class="textExemple">
                    Le routing (système de routage) est le mécanisme qui fait correspondre une URL (ex: <code>/article/42</code>) 
                    à un contrôleur et une méthode spécifique. C'est le cœur de toute application web Symfony.
                </p>
                <p class="textExemple">
                    Sans routage, pas de page, pas d'API. Symfony propose un système puissant et flexible, basé sur des 
                    <strong>annotations</strong> (attributs PHP) ou des fichiers YAML/XML.
                </p>
            </section>

            <!-- Les différentes façons de définir des routes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les différentes façons de définir une route</h2>
                <div class="textExemple">
                    <p>Symfony offre 3 méthodes principales pour définir les routes :</p>
                    <ul>
                        <li><strong>Attributs PHP (recommandé)</strong> – directement dans le contrôleur, près du code.</li>
                        <li><strong>Fichier YAML</strong> – centralisé dans <code>config/routes.yaml</code>.</li>
                        <li><strong>XML ou PHP</strong> – moins courants.</li>
                    </ul>
                    <p>Dans cette leçon, nous nous concentrerons sur les <strong>attributs PHP</strong>, la méthode moderne et privilégiée.</p>
                </div>

                <h3 class="text-purple">Exemple basique avec attribut</h3>
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
}</code></pre>
                </div>
                <p class="textExemple">
                    La route sera accessible à l'URL <code>/blog</code> et portera le nom interne <code>blog_list</code>.
                </p>
            </section>

            <!-- Types de routes et paramètres -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Paramètres dynamiques dans l'URL</h2>
                <p class="textExemple">
                    On peut capturer des parties variables de l'URL en utilisant des <strong>paramètres entre accolades</strong>.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">#[Route('/article/{id}', name: 'article_show')]
public function show(int $id): Response
{
    return new Response("Affichage de l'article n° $id");
}</code></pre>
                </div>
                <p class="textExemple">
                    Symfony injecte automatiquement la valeur dans l'argument de la méthode. Vous pouvez contraindre le paramètre avec des expressions régulières :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">#[Route('/article/{id}', name: 'article_show', requirements: ['id' => '\d+'])]
public function show(int $id): Response { ... }

// Plusieurs paramètres :
#[Route('/blog/{category}/{slug}', name: 'blog_show', requirements: ['category' => 'news|tutorial', 'slug' => '[a-z-]+'])]
public function show(string $category, string $slug): Response { ... }</code></pre>
                </div>
            </section>

            <!-- Paramètres optionnels et valeurs par défaut -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Paramètres optionnels</h2>
                <p class="textExemple">
                    On peut rendre un paramètre optionnel en ajoutant <code>?</code> après le nom et une valeur par défaut dans la méthode.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">#[Route('/page/{slug}', name: 'page_show', defaults: ['slug' => 'accueil'])]
public function show(string $slug): Response
{
    return new Response("Page : $slug");
}</code></pre>
                </div>
                <p class="textExemple">
                    Ainsi, <code>/page</code> affichera "accueil" et <code>/page/contact</code> affichera "contact".
                </p>
            </section>

            <!-- Méthodes HTTP -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Restreindre les méthodes HTTP</h2>
                <p class="textExemple">
                    On peut limiter une route à certaines méthodes (GET, POST, PUT, DELETE, etc.) via l'option <code>methods</code>.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">#[Route('/api/article', name: 'api_article_create', methods: ['POST'])]
public function create(Request $request): Response { ... }

#[Route('/api/article/{id}', name: 'api_article_delete', methods: ['DELETE'])]
public function delete(int $id): Response { ... }</code></pre>
                </div>
                <p class="textExemple">
                    Symfony déclenchera une erreur 405 (Méthode non autorisée) si la requête utilise une autre méthode.
                </p>
            </section>

            <!-- Nom des routes et génération d'URL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Nom des routes et génération d'URL</h2>
                <p class="textExemple">
                    Chaque route possède un nom unique (ex: <code>article_show</code>). Ce nom permet de générer des URLs dans les templates ou dans le code, sans les écrire en dur.
                </p>
                <h3 class="text-purple">Dans un template Twig :</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-twig">{{ path('article_show', {id: 42}) }}
{# Génère : /article/42 #}

{{ url('article_show', {id: 42}) }}
{# Génère l'URL absolue : http://localhost/article/42 #}</code></pre>
                </div>
                <h3 class="text-purple">Dans un contrôleur :</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php">use Symfony\Component\Routing\Generator\UrlGeneratorInterface;

// Depuis un contrôleur qui étend AbstractController
$this->generateUrl('article_show', ['id' => 42]);

// Avec injection du service
public function index(UrlGeneratorInterface $urlGenerator): Response
{
    $url = $urlGenerator->generate('article_show', ['id' => 42]);
}</code></pre>
                </div>
            </section>

            <!-- Groupe de routes (préfixes) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Grouper des routes avec un préfixe</h2>
                <p class="textExemple">
                    Lorsque plusieurs routes partagent le même préfixe, on peut utiliser l'attribut <code>#[Route]</code> au niveau de la classe.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">#[Route('/admin')]
class AdminController extends AbstractController
{
    #[Route('/dashboard', name: 'admin_dashboard')]
    public function dashboard(): Response { ... }
    // URL finale : /admin/dashboard

    #[Route('/users', name: 'admin_users')]
    public function listUsers(): Response { ... }
    // URL finale : /admin/users
}</code></pre>
                </div>
            </section>

            <!-- Redirections -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Redirections entre routes</h2>
                <p class="textExemple">
                    On peut rediriger une route vers une autre en utilisant le nom de la route cible.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">use Symfony\Component\HttpFoundation\RedirectResponse;

#[Route('/ancienne-page', name: 'old_page')]
public function oldPage(): RedirectResponse
{
    return $this->redirectToRoute('new_page', [], 301); // redirection permanente
}</code></pre>
                </div>
                <p class="textExemple">
                    Il est aussi possible de définir une redirection directement dans le fichier <code>config/routes.yaml</code> sans contrôleur.
                </p>
            </section>

            <!-- Debug des routes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Debugger les routes</h2>
                <p class="textExemple">
                    Symfony fournit des commandes pour lister toutes les routes et déboguer.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">php bin/console debug:router</span>
<span class="bash-comment"># Affiche toutes les routes avec leur nom, chemin, méthodes et contrôleur</span>

<span class="bash-prompt">$</span> <span class="bash-command">php bin/console debug:router article_show</span>
<span class="bash-comment"># Détail d'une route spécifique</span>

<span class="bash-prompt">$</span> <span class="bash-command">php bin/console router:match /article/42</span>
<span class="bash-comment"># Teste quelle route correspond à une URL donnée</span></code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li><strong>Toujours nommer ses routes</strong> – cela permet de générer des URLs sans les coder en dur.</li>
                    <li><strong>Utiliser des noms de routes explicites</strong> : <code>article_show</code> plutôt que <code>show</code>.</li>
                    <li><strong>Préférer les attributs PHP aux fichiers YAML</strong> – la logique reste proche du contrôleur.</li>
                    <li><strong>Restreindre les méthodes HTTP</strong> pour plus de sécurité (GET pour afficher, POST pour créer, etc.).</li>
                    <li><strong>Éviter les paramètres optionnels complexes</strong> – préférez plusieurs routes si nécessaire.</li>
                    <li><strong>Versionner ses routes d'API</strong> : <code>/api/v1/articles</code>, <code>/api/v2/articles</code>.</li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Le routing de Symfony est flexible, puissant et sécurisé. En maîtrisant les attributs <code>#[Route]</code>,
                        les paramètres dynamiques et la génération d'URL, vous pouvez construire des applications propres,
                        maintenables et faciles à faire évoluer.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous approfondirons les <strong>paramètres convertis</strong> (ex: <code>Article $article</code>)
                        et les <strong>conditions avancées</strong> (ex: expressions, sous-domaines).
                    </p>
                </div>
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
                    const languages = ['php', 'twig', 'bash'];
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
/* Styles identiques aux leçons précédentes – copie exacte */
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