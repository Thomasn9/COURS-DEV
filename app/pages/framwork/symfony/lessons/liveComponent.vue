<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Symfony UX & Live Component : Le dynamisme sans JavaScript</h1>
                <p class="lesson-meta text-white">Symfony • UX • Live Component • Twig • Stimulus • MVC • AJAX</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Symfony UX ?</h2>
                <p class="textExemple">
                    Symfony UX rassemble des outils officiels qui créent un pont entre Symfony et l'écosystème JavaScript moderne, s'appuyant sur npm, Webpack Encore et Stimulus[reference:0]. Son objectif est de permettre aux développeurs spécialistes back-end de construire des interfaces utilisateur dynamiques et interactives, sans avoir à maîtriser des frameworks SPA complexes[reference:1].
                </p>
                <div class="textExemple">
                    <p><strong>Principaux composants de Symfony UX :</strong></p>
                    <ul>
                        <li><strong>TwigComponent :</strong> Pour créer des composants Twig réutilisables et paramétrables.</li>
                        <li><strong>Live Component :</strong> La pièce maîtresse pour l'interactivité. Il permet à un composant Twig de se re-rendre dynamiquement en AJAX, sans rechargement de page.</li>
                        <li><strong>Turbo :</strong> Pour accélérer la navigation et mettre à jour des parties de page, donnant un effet "Single Page Application".</li>
                        <li><strong>Stimulus :</strong> Un framework JavaScript modeste qui permet d'"augmenter" un HTML statique avec des interactions ciblées.</li>
                    </ul>
                </div>
            </section>

            <!-- Focus sur les Live Component -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Focus sur les Live Component</h2>
                <p class="textExemple">
                    Un <strong>Live Component</strong> (composant "vivant") transforme un composant Twig classique en une interface dynamique et interactive. Lorsqu'un utilisateur interagit avec lui (saisie dans un champ, clic sur un bouton), le composant communique avec le serveur en arrière-plan (via AJAX) et se met à jour automatiquement[reference:2]. C'est un peu comme si votre PHP et votre Twig devenaient soudainement "réactifs", à la manière de Livewire (pour Laravel) ou de Phoenix LiveView[reference:3].
                </p>
                <div class="textExemple">
                    <p>Ils reposent sur trois briques fondamentales :</p>
                    <ul>
                        <li><strong>#[AsLiveComponent] :</strong> L'attribut qui transforme une classe PHP en Live Component[reference:4].</li>
                        <li><strong>#[LiveProp] :</strong> Attribut pour déclarer les propriétés persistantes et réactives du composant, dont l'état est conservé, même entre les re-rendus[reference:5].</li>
                        <li><strong>#[LiveAction] :</strong> Attribut pour déclarer des méthodes PHP qui peuvent être déclenchées directement depuis le front-end[reference:6].</li>
                    </ul>
                </div>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation dans un projet Symfony + Webpack Encore / AssetMapper</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Prérequis : Webpack Encore configuré</h3>
                    <p>Assurez-vous d'avoir Webpack Encore installé et fonctionnel.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Assurez-vous d'avoir un fichier webpack.config.js
composer require symfony/webpack-encore-bundle
npm install</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Étape 1 : Installer le bundle Symfony UX</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installation de la bibliothèque Live Component
composer require symfony/ux-live-component</code></pre>
                    </div>
                    <p>Cette commande utilise Symfony Flex pour automatiquement :</p>
                    <ul>
                        <li>Ajouter `symfony/ux-live-component` à vos dépendances.[reference:7]</li>
                        <li>Mettre à jour votre `package.json` avec les packages JavaScript spécifiques nécessaires.[reference:8]</li>
                        <li>Déclencher et configurer le bundle automatiquement.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Étape 2 : Installer les assets JavaScript via NPM</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">npm install --force
npm run watch</code></pre>
                    </div>
                    <p>Ces commandes installent les dépendances front-end (StimulusBundle, etc.) et lancent Webpack Encore en mode "watch".</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Étape 3 : Vérification de la configuration</h3>
                    <p>Après l'installation, assurez-vous que vos fichiers sont corrects.</p>
                    <ul>
                        <li>Assurez-vous que votre `package.json` contient désormais `@symfony/ux-live-component`[reference:9].</li>
                        <li>Votre `assets/bootstrap.js` initialise correctement les contrôleurs Live Component et Stimulus.</li>
                        <li>Votre `config/bundles.php` liste `Symfony\UX\TwigComponent\TwigComponentBundle::class`, `Symfony\UX\LiveComponent\LiveComponentBundle::class` et `Symfony\UX\StimulusBundle\StimulusBundle::class`.</li>
                    </ul>
                </div>
            </section>

            <!-- Avantages et Pourquoi c'est super -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi c'est génial ? (Avantages)</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Productivité maximale :</strong> Construisez des fonctionnalités complexes en vous concentrant uniquement sur PHP/Twig. Symfony UX dédie les développeurs back-end à créer des interactions front-end avancées, sans être des experts JavaScript.</li>
                        <li><strong>Sécurité native :</strong> Les composants Live sont intrinsèquement sécurisés car toute logique métier restent côté serveur. Moins d'appels API exposés signifie une surface d'attaque réduite.</li>
                        <li><strong>Performances :</strong> Le système de mise à jour est léger et optimisé (AJAX). Les Live Component ne chargent que le strict nécessaire[reference:10].</li>
                        <li><strong>Migration progressive :</strong> Intégrez Live Component où vous en avez besoin, sans réécrire toute votre application.</li>
                        <li><strong>Facilité de maintenance :</strong> Le code reste basé sur la structure MVC et les standards Symfony， ce qui est plus maintenable qu'une application SPA séparée.</li>
                    </ul>
                </div>
            </section>

            <!-- Live Component Minimal (Exemple Compteur) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple concret : Un compteur interactif (Counter)</h2>
                <p class="textExemple">
                    Rien de mieux qu'un exemple simple pour prendre en main les Live Component. Créons un compteur qui s'incrémente sans recharger la page.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">1. Création de la classe PHP (src/Twig/Components/Counter.php)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Twig/Components/Counter.php
namespace App\Twig\Components;

use Symfony\UX\LiveComponent\Attribute\AsLiveComponent;
use Symfony\UX\LiveComponent\Attribute\LiveProp;
use Symfony\UX\LiveComponent\DefaultActionTrait;

#[AsLiveComponent('counter')]
class Counter
{
    use DefaultActionTrait; // Nécessaire pour le rendu par défaut

    // Propriété 'count' dont l'état sera conservé et qui peut être modifiée depuis le frontend
    #[LiveProp(writable: true)]
    public int $count = 0;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Création du template Twig (templates/components/Counter.html.twig)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/components/Counter.html.twig #}
&lt;div {{ attributes }} class="p-4 border rounded-lg shadow-sm text-center max-w-sm mx-auto"&gt;
    &lt;p class="text-purple-600 font-bold text-2xl mb-4"&gt;Compteur : {{ this.count }}&lt;/p&gt;

    &lt;div class="flex justify-center gap-3"&gt;
        &lt;button
            type="button"
            data-action="live#$render"
            class="bg-purple-500 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded transition"
        &gt;
            Incrémenter [+]
        &lt;/button&gt;

        &lt;button
            type="button"
            data-action="live#$render"
            class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded transition"
        &gt;
            Décrémenter [-]
        &lt;/button&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>
                    </div>
                    <p class="textExemple">
                        <strong>Explications :</strong> Ici, la div parent possède l'attribut spécial `{{ attributes }}`, indispensable au bon fonctionnement. Le bouton utilise `data-action="live#$render"` grâce auquel le nom du composant est automatiquement inféré du nom de l'action. Cliquer sur ce bouton déclenche le re-rendu (équivalent à invoquer la méthode `__invoke()` du contrôleur).
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Intégration dans une page existante</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# Exemple : templates/home/index.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    &lt;h1&gt;Ma page d'accueil dynamique&lt;/h1&gt;
    {{ component('counter') }}
{% endblock %}</code></pre>
                    </div>
                    <p>Résultat : Sans une seule ligne de JavaScript manuelle, le composant "Counter" est auto-suffisant, réactif, et s'incrémente instantanément.</p>
                </div>
            </section>

            <!-- Exemple Plus Complexe : Recherche en direct -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Application avancée : Barre de recherche en direct (Live Search)</h2>
                <p class="textExemple">
                    Créons une barre de recherche de produits qui filtre les résultats au fur et à mesure que l'utilisateur tape, sans cliquer sur un bouton "Rechercher"[reference:11]. On utilisera ici le `data-model` intégré aux Live Component.
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">1. Classe PHP (src/Twig/Components/ProductSearch.php)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Twig/Components/ProductSearch.php
namespace App\Twig\Components;

use App\Repository\ProductRepository;
use Symfony\UX\LiveComponent\Attribute\AsLiveComponent;
use Symfony\UX\LiveComponent\Attribute\LiveProp;
use Symfony\UX\LiveComponent\DefaultActionTrait;

#[AsLiveComponent('product_search')]
class ProductSearch
{
    use DefaultActionTrait;

    public function __construct(private ProductRepository $productRepository)
    {}

    // 'writable: true' permet au front de modifier cette propriété.
    #[LiveProp(writable: true)]
    public string $query = '';

    public function getProducts(): array
    {
        // Retourne les résultats de recherche basés sur la propriété '$query'.
        return $this->productRepository->search($this->query);
    }
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">2. Template Twig (templates/components/ProductSearch.html.twig)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;div {{ attributes }} class="search-container p-4 bg-gray-100 rounded-lg"&gt;
    &lt;input
        type="search"
        placeholder="Rechercher un produit..."
        class="w-full p-2 mb-4 border border-gray-300 rounded"
        data-model="query"
    &gt;

    &lt;ul class="list-disc pl-5"&gt;
        {% for product in this.products %}
            &lt;li class="mb-1"&gt;{{ product.name }} - {{ product.price }} €&lt;/li&gt;
        {% else %}
            &lt;li class="text-gray-500 italic"&gt;Aucun produit trouvé.&lt;/li&gt;
        {% endfor %}
    &lt;/ul&gt;
&lt;/div&gt;</code></pre>
                    </div>
                    <p>
                        L'attribut magique `data-model="query"` lie le champ de saisie à la propriété PHP `$query` de notre composant. À chaque frappe, une requête AJAX est envoyée au serveur pour re-rendre le composant avec les nouveaux résultats, offrant une expérience ultra-réactive quasi instantanée.
                    </p>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-twig">{{ component('product_search') }}</code></pre>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Symfony UX et les Live Component comblent le fossé entre les applications traditionnelles Symfony et les interfaces dynamiques modernes. Ils permettent de construire des expériences utilisateur riches et interactives de manière incrémentale et sécurisée, en restant dans l'environnement familier de Symfony.
                    </p>
                    <p>
                        Leurs points forts sont redoutables :
                    </p>
                    <ul>
                        <li>Réduction drastique de la quantité de JavaScript à écrire ou gérer manuellement.</li>
                        <li>Meilleure maintenabilité et productivité grâce à une logique centralisée côté serveur.</li>
                        <li>Performances optimisées pour le réseau interne d'une entreprise.</li>
                    </ul>
                    <p>
                        Dans les prochaines leçons, nous étudierons des sujets plus avancés, tels que l'utilisation des `LiveAction` (déclencher des méthodes PHP arbitraires depuis le clavier) et l'intégration des formulaires Symfony avec les Live Component pour une validation en temps réel.
                    </p>
                    <p class="mt-4 font-bold text-purple">
                        À retenir : Les Live Component redonnent à Symfony sa superpuissance Front-End, sans avoir à apprendre React ou Vue depuis le début.
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
                link.rel = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const languages = ['php', 'twig', 'bash', 'plaintext'];
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
/* Styles identiques – inchangés par rapport à vos leçons existantes */
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