<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Générer des contrôleurs avec Symfony Console</h1>
                <p class="lesson-meta text-white">Symfony • Console • MakerBundle • Contrôleurs • Routes</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser make:controller ?</h2>
                <p class="textExemple">
                    La console Symfony, via le <strong>MakerBundle</strong>, permet de générer automatiquement des contrôleurs
                    prêts à l’emploi. Cela accélère le développement, garantit une structure cohérente et évite la duplication de code.
                </p>
                <p class="textExemple">
                    La commande <code>make:controller</code> crée une classe PHP dans <code>src/Controller/</code>
                    ainsi qu’un template Twig dans <code>templates/</code>, avec une route par défaut et une action.
                </p>
            </section>

            <!-- Installation du MakerBundle -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et prérequis</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Installer MakerBundle (si ce n’est pas déjà fait)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installation en environnement de développement
composer require symfony/maker-bundle --dev

# Vérifier que le bundle est bien enregistré
php bin/console list make</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <div class="warning-section">
                        <h4 class="text-purple">⚠️ Important</h4>
                        <p class="warning-text">
                            MakerBundle est conçu pour les environnements de <strong>développement</strong>.
                            Il ne doit pas être installé en production. Utilisez l’option <code>--dev</code>.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Utilisation de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation de base de make:controller</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe générale</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:controller [nom_du_contrôleur]</code></pre>
                    </div>
                    <p>
                        Le nom doit suivre la convention <strong>PascalCase</strong> (ex: <code>BlogController</code>).
                        Le suffixe <code>Controller</code> est automatiquement ajouté si vous l’omettez.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple : générer un contrôleur “Blog”</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:controller Blog</code></pre>
                    </div>
                    <p>Commande interactive : vous pouvez aussi répondre aux questions.</p>
                    <p>Fichiers générés :</p>
                    <ul>
                        <li><code>src/Controller/BlogController.php</code> – la classe du contrôleur</li>
                        <li><code>templates/blog/index.html.twig</code> – le template associé à l’action <code>index</code></li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contenu généré par défaut</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/BlogController.php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class BlogController extends AbstractController
{
    #[Route('/blog', name: 'app_blog')]
    public function index(): Response
    {
        return $this->render('blog/index.html.twig', [
            'controller_name' => 'BlogController',
        ]);
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Options avancées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Options avancées de make:controller</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Créer un contrôleur sans template (Action invocable)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:controller --invokable ApiHealthController</code></pre>
                    </div>
                    <p>
                        L’option <code>--invokable</code> génère une seule méthode <code>__invoke()</code>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/api/health', name: 'api_health')]
public function __invoke(): Response
{
    return $this->json(['status' => 'OK']);
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Forcer le suffixe “Controller”</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:controller Product --controller-suffix</code></pre>
                    </div>
                    <p>
                        Le nom sera <code>ProductController</code>. Utile pour homogénéiser le nommage.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation non interactive (CI / automatisation)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Fournir le nom directement
php bin/console make:controller Contact

# Avec les options
php bin/console make:controller Security/Login --invokable</code></pre>
                    </div>
                    <p>
                        Vous pouvez organiser vos contrôleurs dans des sous-dossiers en utilisant un slash (<code>/</code>).
                    </p>
                </div>
            </section>

            <!-- Personnalisation des routes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Personnaliser les routes générées</h2>

                <div class="textExemple">
                    <p>
                        Par défaut, la route utilise l’attribut PHP 8+ <code>#[Route]</code>. Vous pouvez la modifier après génération.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Exemple : route avec paramètre dynamique
#[Route('/blog/{slug}', name: 'blog_show')]
public function show(string $slug): Response
{
    return $this->render('blog/show.html.twig', [
        'slug' => $slug,
    ]);
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Groupe de routes (préfixe)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/admin')]  // Préfixe commun
class AdminController extends AbstractController
{
    #[Route('/dashboard', name: 'admin_dashboard')]
    public function dashboard(): Response { ... }

    #[Route('/users', name: 'admin_users')]
    public function users(): Response { ... }
}</code></pre>
                    </div>
                    <p>Les routes finales seront <code>/admin/dashboard</code> et <code>/admin/users</code>.</p>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec les contrôleurs Symfony</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Un contrôleur = une responsabilité</strong> : séparez les fonctionnalités métier distinctes.</li>
                        <li><strong>Utilisez l’injection de dépendances</strong> dans le constructeur ou les méthodes.</li>
                        <li><strong>Évitez la logique métier dans le contrôleur</strong> : déléguez aux services.</li>
                        <li><strong>Nommez vos routes clairement</strong> : <code>app_product_index</code>, <code>admin_user_edit</code>.</li>
                        <li><strong>Utilisez les attributs PHP (ou annotations)</strong> pour les routes – plus lisibles.</li>
                        <li><strong>Ne dépassez pas 20-30 lignes par action</strong> : refactorisez si besoin.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple de contrôleur bien structuré</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">namespace App\Controller;

use App\Service\ProductService;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class ProductController extends AbstractController
{
    public function __construct(
        private ProductService $productService
    ) {}

    #[Route('/products', name: 'app_product_list')]
    public function list(): Response
    {
        $products = $this->productService->getAllActive();

        return $this->render('product/list.html.twig', [
            'products' => $products,
        ]);
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices : maîtrisez make:controller</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Génération et modification</h3>
                    <p>Générez un contrôleur <code>ArticleController</code> avec la commande <code>make:controller</code>.</p>
                    <ul>
                        <li>Ajoutez une deuxième action <code>show($id)</code> avec sa route.</li>
                        <li>Faites en sorte que l’action <code>index</code> redirige vers <code>show</code> avec un article fictif (id=1).</li>
                        <li>Modifiez le template pour afficher un message.</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Controller/ArticleController.php
#[Route('/article', name: 'app_article_')]
class ArticleController extends AbstractController
{
    #[Route('', name: 'index')]
    public function index(): Response
    {
        return $this->redirectToRoute('app_article_show', ['id' => 1]);
    }

    #[Route('/{id}', name: 'show')]
    public function show(int $id): Response
    {
        return $this->render('article/show.html.twig', [
            'article_id' => $id,
        ]);
    }
}</code></pre>
                            <pre v-pre><code class="language-twig">{# templates/article/show.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    <h1>Article #{{ article_id }}</h1>
    <p>Contenu de l'article...</p>
{% endblock %}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : API JSON avec invocable</h3>
                    <p>Créez un contrôleur invocable <code>ApiStatusController</code> qui répond en JSON avec les informations :</p>
                    <ul>
                        <li>Version de l’API (ex: 1.0)</li>
                        <li>Statut du serveur (up / down)</li>
                        <li>Horodatage actuel</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:controller --invokable ApiStatus</code></pre>
                            <pre v-pre><code class="language-php">// src/Controller/ApiStatusController.php
#[Route('/api/status', name: 'api_status')]
public function __invoke(): Response
{
    return $this->json([
        'api_version' => '1.0',
        'status' => 'up',
        'timestamp' => (new \DateTime())->format(\DateTime::ATOM),
    ]);
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>

                <div class="textExemple">
                    <p>
                        La commande <code>make:controller</code> est un gain de temps considérable pour structurer votre application.
                        Elle génère un squelette propre, conforme aux bonnes pratiques Symfony, que vous pouvez ensuite personnaliser.
                    </p>
                    <p>
                        Combinez-la avec d’autres commandes <code>make:*</code> (entity, form, crud, etc.) pour un développement ultra-rapide.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Rappel des commandes utiles</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Lister toutes les commandes "make"
php bin/console list make

# Générer un contrôleur classique
php bin/console make:controller ProductController

# Générer un contrôleur invocable
php bin/console make:controller --invokable Home

# Générer un CRUD complet (contrôleur + formulaire + templates)
php bin/console make:crud Product</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <p>
                        <strong>À retenir</strong> : les contrôleurs sont le point d’entrée HTTP de votre application.
                        Symfony console vous permet de les créer en quelques secondes pour vous concentrer sur l’essentiel :
                        la logique métier.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyMakeControllerLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel  = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const twigScript = document.createElement('script');
                        twigScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/twig.min.js';
                        twigScript.onload = resolve;
                        document.head.appendChild(twigScript);
                    };
                    document.head.appendChild(phpScript);
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

.code-example {
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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
}

.warning-text {
    color: #d63031;
    font-weight: bold;
    margin-top: 0.5rem;
}

.success-text {
    color: #00b894;
    font-weight: bold;
    margin-top: 0.5rem;
}

.exercise { margin: 2rem 0; }
.solution { margin: 1rem 0; }

.solution-content {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #8B5FBF;
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
    .code-comparison   { grid-template-columns: 1fr; gap: 1rem; }
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