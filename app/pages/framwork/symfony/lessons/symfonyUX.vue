<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Symfony UX : Front-end moderne dans Symfony</h1>
                <p class="lesson-meta text-white">Stimulus • Turbo • LiveComponent • Webpack Encore • Hotwire</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Symfony UX ?</h2>
                <p class="textExemple">
                    Symfony UX est un ensemble de bibliothèques JavaScript officielles qui intègrent parfaitement les technologies front-end modernes (Stimulus, Turbo, LiveComponent, etc.) dans un projet Symfony. L'objectif est de construire des applications dynamiques et réactives sans écrire de JavaScript complexe, en restant dans l'écosystème Symfony.
                </p>
                <p class="textExemple">
                    Symfony UX repose sur <strong>Webpack Encore</strong> pour l'asset management, <strong>Stimulus</strong> pour les interactions légères, <strong>Turbo</strong> pour les mises à jour sans rechargement complet, et <strong>LiveComponent</strong> pour des composants dynamiques côté serveur avec mise à jour en temps réel.
                </p>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation de l'écosystème UX</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Installer Webpack Encore et les dépendances de base</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer Webpack Encore
composer require symfony/webpack-encore-bundle

# Installer les dépendances Node (yarn ou npm)
yarn install
yarn add @symfony/webpack-encore --dev</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Installer les packages UX désirés</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Stimulus (gestionnaire de contrôleurs)
composer require symfony/stimulus-bundle

# Turbo (navigation rapide et mises à jour)
composer require symfony/ux-turbo

# LiveComponent (composants réactifs)
composer require symfony/ux-live-component

# Chart.js (graphiques)
composer require symfony/ux-chartjs

# Dropzone (upload de fichiers)
composer require symfony/ux-dropzone

# Tous les packages UX sont disponibles via :
# composer require symfony/ux-nom-du-paquet</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Construire les assets</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Compiler les assets une fois
yarn build

# Ou lancer en mode développement avec watch
yarn watch</code></pre>
                    </div>
                </div>
            </section>

            <!-- Stimulus : Contrôleurs JavaScript -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Stimulus : des contrôleurs JavaScript légers</h2>

                <div class="textExemple">
                    <p>
                        Stimulus est un framework minimaliste qui attache des contrôleurs JavaScript à des éléments HTML via des attributs <code>data-controller</code>. Il permet d'ajouter de l'interactivité sans écrire de JavaScript complexe.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer un contrôleur Stimulus</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Générer un contrôleur avec le maker
php bin/console make:stimulus Hello</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// assets/controllers/hello_controller.js
import { Controller } from '@hotwired/stimulus';

export default class extends Controller {
    static targets = ['name', 'output'];

    greet() {
        const name = this.nameTarget.value;
        this.outputTarget.textContent = `Bonjour ${name} !`;
    }
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/hello/index.html.twig #}
<div data-controller="hello">
    <input type="text" data-hello-target="name" placeholder="Votre nom">
    <button data-action="click->hello#greet">Saluer</button>
    <div data-hello-target="output"></div>
</div></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Attributs Stimulus essentiels</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html"><div data-controller="nom-du-controleur">
    <!-- Cibles -->
    <span data-nom-du-controleur-target="maCible"></span>
    <!-- Actions -->
    <button data-action="click->nom-du-controleur#maMethode">Cliquez</button>
    <!-- Valeurs -->
    <div data-nom-du-controleur-texte-value="Bonjour"></div>
</div></code></pre>
                    </div>
                </div>
            </section>

            <!-- Turbo : Navigation instantanée -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Turbo : navigation rapide sans rechargement</h2>

                <div class="textExemple">
                    <p>
                        Turbo transforme les clics sur les liens en requêtes AJAX et remplace uniquement le contenu de la balise <code>&lt;body&gt;</code> (ou la partie ciblée). Cela rend la navigation quasi instantanée.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Activer Turbo</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/base.html.twig #}
{% block javascripts %}
    {{ importmap('app') }}
    {{ ux_turbo() }} {# Active Turbo automatiquement #}
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser Turbo Frames pour rafraîchir une partie</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/article/list.html.twig #}
<turbo-frame id="article-list">
    {% for article in articles %}
        <div>{{ article.titre }}</div>
    {% endfor %}

    <a href="{{ path('article_next_page', {page: page+1}) }}" turbo-frame="article-list">
        Charger plus
    </a>
</turbo-frame></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Turbo Streams : mises à jour en temps réel</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un contrôleur
use Symfony\UX\Turbo\TurboBundle;

#[Route('/article/{id}/comment', name: 'article_comment')]
public function comment(Article $article, Request $request): Response
{
    // ... traitement du commentaire

    if (TurboBundle::STREAM_FORMAT === $request->getPreferredFormat()) {
        // Réponse Turbo Stream
        return $this->render('article/comment.stream.html.twig', [
            'comment' => $comment,
        ]);
    }

    // Réponse normale
    return $this->redirectToRoute('article_show', ['id' => $article->getId()]);
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/article/comment.stream.html.twig #}
<turbo-stream action="append" target="comments-list">
    <template>
        <div>{{ comment.content }}</div>
    </template>
</turbo-stream></code></pre>
                    </div>
                </div>
            </section>

            <!-- LiveComponent : Composants réactifs côté serveur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">LiveComponent : dynamique sans JavaScript</h2>

                <div class="textExemple">
                    <p>
                        LiveComponent permet de créer des composants réactifs dont l'état est géré côté serveur. Les interactions utilisateur (clic, saisie) déclenchent des requêtes AJAX qui mettent à jour uniquement le composant. C'est idéal pour les formulaires, les recherches en direct, etc.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer un composant Live</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:live-component SearchForm</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Twig/Components/SearchForm.php
namespace App\Twig\Components;

use Symfony\UX\LiveComponent\Attribute\AsLiveComponent;
use Symfony\UX\LiveComponent\Attribute\LiveProp;
use Symfony\UX\LiveComponent\DefaultActionTrait;

#[AsLiveComponent('search_form')]
class SearchForm
{
    use DefaultActionTrait;

    #[LiveProp(writable: true)]
    public string $query = '';

    public function getResults(): array
    {
        // Recherche en base en fonction de $query
        return $this->searchService->search($this->query);
    }
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/components/search_form.html.twig #}
<div {{ attributes }}>
    <input
        type="search"
        data-model="query"
        placeholder="Rechercher..."
    >

    <div>
        {% for result in this.results %}
            <div>{{ result }}</div>
        {% else %}
            <div>Aucun résultat</div>
        {% endfor %}
    </div>
</div></code></pre>
                    </div>
                    <p>L'attribut <code>data-model</code> synchronise automatiquement le champ avec la propriété <code>$query</code> du composant.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser un LiveComponent dans un template</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{{ component('search_form') }}

{# Ou avec des paramètres #}
{{ component('search_form', { initialQuery: 'Symfony' }) }}</code></pre>
                    </div>
                </div>
            </section>

            <!-- UX Chart.js : graphiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">UX Chart.js : intégration de graphiques</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require symfony/ux-chartjs</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un contrôleur
use Symfony\UX\Chartjs\Builder\ChartBuilderInterface;
use Symfony\UX\Chartjs\Model\Chart;

public function stats(ChartBuilderInterface $chartBuilder): Response
{
    $chart = $chartBuilder->createChart(Chart::TYPE_LINE);

    $chart->setData([
        'labels' => ['Jan', 'Fév', 'Mar', 'Avr'],
        'datasets' => [
            [
                'label' => 'Ventes',
                'data' => [65, 59, 80, 81],
            ],
        ],
    ]);

    $chart->setOptions([
        'scales' => [
            'y' => ['beginAtZero' => true],
        ],
    ]);

    return $this->render('stats/index.html.twig', [
        'chart' => $chart,
    ]);
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{{ render_chart(chart) }}</code></pre>
                    </div>
                </div>
            </section>

            <!-- UX Dropzone : upload de fichiers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">UX Dropzone : upload de fichiers glisser-déposer</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require symfony/ux-dropzone</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{{ form_start(form) }}
    {{ form_row(form.image, { attr: { 'data-controller': 'dropzone' } }) }}
{{ form_end(form) }}</code></pre>
                    </div>
                    <p>Le bundle ajoute automatiquement l'interface Dropzone sur le champ de type FileType.</p>
                </div>
            </section>

            <!-- UX Autocomplete : recherche avec sélection -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">UX Autocomplete : champs de sélection avancés</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require symfony/ux-autocomplete</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un FormType
use Symfony\UX\Autocomplete\Form\AsEntityAutocompleteField;
use Symfony\UX\Autocomplete\Form\ParentEntityAutocompleteType;

#[AsEntityAutocompleteField]
class ProductAutocompleteField extends AbstractType
{
    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'class' => Product::class,
            'choice_label' => 'name',
            'multiple' => true,
        ]);
    }

    public function getParent(): string
    {
        return ParentEntityAutocompleteType::class;
    }
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Utilisation dans un formulaire
$builder->add('product', ProductAutocompleteField::class);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Formulaire de recherche en direct avec LiveComponent</h3>
                    <p>Créez un composant Live qui permet de filtrer une liste de produits en temps réel via une barre de recherche.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Twig/Components/ProductSearch.php
#[AsLiveComponent('product_search')]
class ProductSearch
{
    use DefaultActionTrait;

    #[LiveProp(writable: true)]
    public string $search = '';

    public function __construct(private ProductRepository $productRepository) {}

    public function getProducts(): array
    {
        return $this->productRepository->findBySearch($this->search);
    }
}</code></pre>
                            <pre v-pre><code class="language-twig">{# templates/components/product_search.html.twig #}
<div {{ attributes }}>
    <input
        type="text"
        data-model="search"
        placeholder="Rechercher un produit..."
        class="form-control mb-3"
    >

    <div class="list-group">
        {% for product in this.products %}
            <div class="list-group-item">{{ product.name }} - {{ product.price }} €</div>
        {% else %}
            <div class="alert alert-info">Aucun produit trouvé</div>
        {% endfor %}
    </div>
</div></code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Turbo Stream pour ajouter des commentaires</h3>
                    <p>Créez un système de commentaires où l'ajout d'un nouveau commentaire se fait via un formulaire et s'affiche sans rechargement grâce à Turbo Stream.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// CommentController.php
#[Route('/article/{id}/comment', name: 'add_comment')]
public function addComment(Article $article, Request $request, EntityManagerInterface $em): Response
{
    $comment = new Comment();
    $form = $this->createForm(CommentType::class, $comment);
    $form->handleRequest($request);

    if ($form->isSubmitted() && $form->isValid()) {
        $comment->setArticle($article);
        $em->persist($comment);
        $em->flush();

        if (TurboBundle::STREAM_FORMAT === $request->getPreferredFormat()) {
            return $this->render('comment/_stream.html.twig', ['comment' => $comment]);
        }

        return $this->redirectToRoute('article_show', ['id' => $article->getId()]);
    }

    return $this->render('comment/form.html.twig', ['form' => $form]);
}</code></pre>
                            <pre v-pre><code class="language-twig">{# comment/_stream.html.twig #}
<turbo-stream action="append" target="comments-list">
    <template>
        <div class="comment">
            <strong>{{ comment.author }}</strong> : {{ comment.content }}
        </div>
    </template>
</turbo-stream></code></pre>
                            <pre v-pre><code class="language-twig">{# templates/article/show.html.twig #}
<turbo-frame id="comments-list">
    {% for comment in article.comments %}
        <div class="comment">
            <strong>{{ comment.author }}</strong> : {{ comment.content }}
        </div>
    {% endfor %}
</turbo-frame>

{{ form_start(form, { attr: { 'data-turbo-frame': '_top' } }) }}
    {# Le formulaire sera soumis avec Turbo #}
{{ form_end(form) }}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques et conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Architecture et organisation</h3>
                    <ul>
                        <li><strong>Utilisez Stimulus pour les interactions simples</strong> : animations, toggles, petits formulaires.</li>
                        <li><strong>Préférez LiveComponent pour les composants avec état</strong> : recherches en direct, formulaires avec validation instantanée.</li>
                        <li><strong>Turbo est idéal pour la navigation globale</strong> : activez-le par défaut pour toute l'application.</li>
                        <li><strong>Découpez vos composants Live en petits morceaux</strong> pour faciliter la maintenance.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance</h3>
                    <ul>
                        <li>Les LiveComponent envoient des requêtes AJAX à chaque interaction ; utilisez <code>debounce</code> sur les champs de recherche.</li>
                        <li>Chargez uniquement les contrôleurs Stimulus nécessaires via le système d'importmap.</li>
                        <li>Utilisez la mise en cache des assets avec Webpack Encore en production.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurité</h3>
                    <ul>
                        <li>Les LiveComponent incluent automatiquement un token CSRF lors des mises à jour.</li>
                        <li>Vérifiez toujours les droits d'accès côté serveur, même si le composant est dynamique.</li>
                        <li>Évitez d'exposer des propriétés sensibles via <code>#[LiveProp]</code>.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Symfony UX offre un écosystème cohérent pour construire des applications modernes et réactives sans avoir à maîtriser un framework front-end complet. En combinant Turbo, Stimulus et LiveComponent, vous pouvez créer des interfaces riches tout en restant dans le confort de Symfony.
                    </p>
                    <p>
                        Pour aller plus loin, explorez les autres packages UX comme <strong>UX Twig Component</strong> (composants réutilisables Twig), <strong>UX Icons</strong> (gestion d'icônes SVG) ou <strong>UX Toggle</strong> (boutons à bascule).
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyUxLesson',

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
                    const langs = ['php', 'twig', 'javascript', 'bash', 'html'];
                    let loaded = 0;
                    langs.forEach(lang => {
                        const langScript = document.createElement('script');
                        langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`;
                        langScript.onload = () => {
                            loaded++;
                            if (loaded === langs.length) resolve();
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
/* Les styles restent identiques à ceux utilisés précédemment */
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