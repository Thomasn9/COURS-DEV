<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Intégration de Bootstrap dans Symfony</h1>
                <p class="lesson-meta text-white">Symfony • Bootstrap 4/5 • AssetMapper • Webpack Encore • Twig</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi intégrer Bootstrap dans Symfony ?</h2>
                <p class="textExemple">
                    Bootstrap est le framework CSS le plus populaire, offrant une grille responsive, des composants d'interface prêts à l'emploi et des styles cohérents.
                    Dans un projet Symfony, son intégration permet d'accélérer le développement front-end tout en garantissant une base solide et maintenable.
                </p>
                <p class="textExemple">
                    Symfony propose deux approches principales pour intégrer Bootstrap : via <strong>AssetMapper</strong> (recommandé à partir de Symfony 6.4) ou via <strong>Webpack Encore</strong>.
                    Le choix dépend de vos besoins en termes de personnalisation et de build front-end.
                </p>
            </section>

            <!-- NOUVELLE SECTION : Où trouver les liens CDN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Où trouver les liens CDN officiels ?</h2>
                <p class="textExemple">
                    Avant d'intégrer Bootstrap via CDN, vous devez récupérer les liens (balises <code>&lt;link&gt;</code> et <code>&lt;script&gt;</code>) sur le site officiel. 
                    Voici la procédure pour Bootstrap 4 et Bootstrap 5.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Pour Bootstrap 5 (recommandé, pas de dépendance jQuery)</h3>
                    <ul>
                        <li>Rendez-vous sur <a href="https://getbootstrap.com/docs/5.3/getting-started/introduction/" target="_blank" class="text-purple">getbootstrap.com/docs/5.3</a></li>
                        <li>Dans la section <strong>"Quick start"</strong>, copiez le <code>&lt;link&gt;</code> CSS et le <code>&lt;script&gt;</code> du bundle JavaScript (qui inclut déjà Popper).</li>
                        <li>Insérez-les dans votre template Twig comme montré plus bas.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;!-- Bootstrap 5 CSS (exemple avec integrity) --&gt;
&lt;link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous"&gt;

&lt;!-- Bootstrap 5 JS Bundle --&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"&gt;&lt;/script&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Pour Bootstrap 4 (nécessite jQuery et Popper.js)</h3>
                    <ul>
                        <li>Allez sur <a href="https://getbootstrap.com/docs/4.6/getting-started/introduction/" target="_blank" class="text-purple">getbootstrap.com/docs/4.6</a></li>
                        <li>Dans la section <strong>"Quick start"</strong>, copiez le CSS, puis les trois scripts dans l'ordre : <strong>jQuery (slim)</strong>, <strong>Popper.js</strong>, <strong>Bootstrap JS</strong>.</li>
                        <li>Respectez impérativement cet ordre.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;!-- Bootstrap 4 CSS --&gt;
&lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous"&gt;

&lt;!-- jQuery d'abord, puis Popper, puis Bootstrap JS --&gt;
&lt;script src="https://code.jquery.com/jquery-3.6.0.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"&gt;&lt;/script&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"&gt;&lt;/script&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.min.js" integrity="sha384-+sLIOodYLS7CIrQpBjl+C7nPvqq+FbNUBDunl/OZv93DB7Ln/533i8e/mZXLi/P+" crossorigin="anonymous"&gt;&lt;/script&gt;</code></pre>
                    </div>
                    <div class="warning-section">
                        <strong>Important :</strong> Les attributs <code>integrity</code> et <code>crossorigin</code> sont fournis par le site officiel. Ils garantissent que le fichier n'a pas été altéré (SRI). <strong>Toujours utiliser les liens avec integrity</strong> pour la sécurité en production.
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Intégration dans un template Symfony (base.html.twig)</h3>
                    <p>Placez les liens dans l'en-tête et avant la fermeture du <code>&lt;body&gt;</code> comme suit :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/base.html.twig #}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;
        {# ... #}
        &lt;link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet"&gt;
        {% block stylesheets %}{% endblock %}
    &lt;/head&gt;
    &lt;body&gt;
        {% block body %}{% endblock %}
        &lt;script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"&gt;&lt;/script&gt;
        {% block javascripts %}{% endblock %}
    &lt;/body&gt;
&lt;/html&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthode 1 : CDN (rapide, sans personnalisation) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 1 : Intégration via CDN</h2>
                <p class="textExemple">
                    La méthode la plus rapide pour démarrer consiste à inclure les feuilles de style et le bundle JavaScript de Bootstrap via un CDN.
                    Elle convient aux prototypes ou aux projets sans besoin de personnalisation poussée.
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Ajouter les liens CDN dans base.html.twig (Bootstrap 5)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/base.html.twig #}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;meta charset=&quot;UTF-8&quot;&gt;
        &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1&quot;&gt;
        &lt;title&gt;{% block title %}Mon projet Symfony{% endblock %}&lt;/title&gt;
        
        {# Bootstrap 5 CSS #}
        &lt;link href=&quot;https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css&quot; rel=&quot;stylesheet&quot;&gt;
        
        {% block stylesheets %}{% endblock %}
    &lt;/head&gt;
    &lt;body&gt;
        {% block body %}{% endblock %}
        
        {# Bootstrap JavaScript Bundle (inclut Popper) #}
        &lt;script src=&quot;https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js&quot;&gt;&lt;/script&gt;
        {% block javascripts %}{% endblock %}
    &lt;/body&gt;
&lt;/html&gt;</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <p><strong>Avantages</strong> : zéro configuration, mise en cache CDN, démarrage instantané.<br>
                    <strong>Inconvénients</strong> : impossible de personnaliser les variables SASS de Bootstrap, dépendance externe.</p>
                </div>
            </section>

            <!-- Méthode 2 : AssetMapper (recommandée Symfony 6.4+) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 2 : AssetMapper (approche moderne sans Node)</h2>
                <p class="textExemple">
                    AssetMapper est la solution native de Symfony pour gérer les assets JavaScript et CSS, sans nécessiter Node.js.
                    Elle est parfaite pour intégrer Bootstrap rapidement tout en gardant la possibilité de mettre à jour les dépendances via Composer.
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Installation</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer le bundle AssetMapper (souvent déjà présent)
composer require symfony/asset-mapper

# Installer Bootstrap via npm (mais géré par AssetMapper)
npm install bootstrap @popperjs/core

# (Optionnel) Installer le package Stimulus pour une utilisation avancée
composer require symfony/stimulus-bundle</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Configuration d'AssetMapper (config/packages/asset_mapper.yaml)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">framework:
    asset_mapper:
        paths:
            - assets/
        missing_import_mode: strict</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Créer les fichiers d'entrypoint (assets/bootstrap.js et assets/styles/app.css)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// assets/bootstrap.js
import * as bootstrap from 'bootstrap';

// Rendre Bootstrap globalement disponible (pour les attributs data-bs-*)
window.bootstrap = bootstrap;</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-css">/* assets/styles/app.css */
@import 'bootstrap/dist/css/bootstrap.min.css';

/* Vos styles personnalisés */
body {
    background-color: #f8f9fa;
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Inclure les assets dans base.html.twig</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/base.html.twig #}
&lt;head&gt;
    {# ... #}
    {% block stylesheets %}
        {{ importmap('app.css') }}
    {% endblock %}
    {% block javascripts %}
        {{ importmap('app.js') }}
        {{ importmap('bootstrap.js') }}
    {% endblock %}
&lt;/head&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthode 3 : Webpack Encore (personnalisation SASS complète) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 3 : Webpack Encore (pour les projets exigeants)</h2>
                <p class="textExemple">
                    Webpack Encore est l'intégration officielle de Symfony avec Webpack. Elle permet de compiler du SASS, de personnaliser les variables Bootstrap,
                    de minifier les assets et d'utiliser des frameworks JavaScript modernes.
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Installation</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer Webpack Encore
composer require symfony/webpack-encore-bundle

# Installer les dépendances Node
npm install

# Installer Bootstrap, Popper, SASS et le chargeur SASS
npm install bootstrap @popperjs/core sass-loader sass --save-dev</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Configuration de webpack.config.js</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// webpack.config.js
const Encore = require('@symfony/webpack-encore');

Encore
    .setOutputPath('public/build/')
    .setPublicPath('/build')
    .addEntry('app', './assets/app.js')
    .enableSassLoader()
    .enableStimulusBridge('./assets/controllers.json')
    .enableVersioning(Encore.isProduction());

module.exports = Encore.getWebpackConfig();</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Créer un fichier SCSS personnalisé (assets/styles/app.scss)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-scss">// assets/styles/app.scss
// 1. Importer les variables Bootstrap
@import '~bootstrap/scss/functions';
@import '~bootstrap/scss/variables';
@import '~bootstrap/scss/mixins';

// 2. Surcharger les variables Bootstrap (ex: couleur primaire)
$primary: #8B5FBF;   // Notre violet
$enable-shadows: true;

// 3. Importer tout Bootstrap
@import '~bootstrap/scss/bootstrap';

// 4. Vos styles personnalisés
body {
    padding-top: 70px;
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Créer le point d'entrée JavaScript (assets/app.js)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// assets/app.js
import './styles/app.scss';
import * as bootstrap from 'bootstrap';

// Rendre Bootstrap global pour les comportements dynamiques
window.bootstrap = bootstrap;</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Compiler les assets et les inclure dans Twig</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">npm run watch   # développement
npm run build   # production</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{% block stylesheets %}
    {{ encore_entry_link_tags('app') }}
{% endblock %}

{% block javascripts %}
    {{ encore_entry_script_tags('app') }}
{% endblock %}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utilisation des composants Bootstrap dans Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utiliser les composants Bootstrap dans Twig</h2>
                <p class="textExemple">
                    Une fois Bootstrap intégré, vous pouvez utiliser toutes les classes CSS et les composants JavaScript directement dans vos templates Twig.
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Exemple : Barre de navigation responsive</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/_navbar.html.twig #}
&lt;nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top"&gt;
    &lt;div class="container"&gt;
        &lt;a class="navbar-brand" href="{{ path('home') }}"&gt;Mon App&lt;/a&gt;
        &lt;button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"&gt;
            &lt;span class="navbar-toggler-icon"&gt;&lt;/span&gt;
        &lt;/button&gt;
        &lt;div class="collapse navbar-collapse" id="navbarNav"&gt;
            &lt;ul class="navbar-nav ms-auto"&gt;
                &lt;li class="nav-item"&gt;&lt;a class="nav-link" href="{{ path('articles') }}"&gt;Articles&lt;/a&gt;&lt;/li&gt;
                &lt;li class="nav-item"&gt;&lt;a class="nav-link" href="{{ path('contact') }}"&gt;Contact&lt;/a&gt;&lt;/li&gt;
            &lt;/ul&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/nav&gt;</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Exemple : Alerte et Card</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;div class="alert alert-success alert-dismissible fade show" role="alert"&gt;
    Article publié avec succès !
    &lt;button type="button" class="btn-close" data-bs-dismiss="alert"&gt;&lt;/button&gt;
&lt;/div&gt;

&lt;div class="card" style="width: 18rem;"&gt;
    &lt;img src="..." class="card-img-top" alt="..."&gt;
    &lt;div class="card-body"&gt;
        &lt;h5 class="card-title"&gt;Titre de la carte&lt;/h5&gt;
        &lt;p class="card-text"&gt;Description rapide.&lt;/p&gt;
        &lt;a href="#" class="btn btn-primary"&gt;Aller quelque part&lt;/a&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Intégration avec les formulaires Symfony (Bootstrap theme) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Formulaires Symfony avec le thème Bootstrap 5</h2>
                <p class="textExemple">
                    Symfony fournit un thème officiel pour Bootstrap 5 qui génère automatiquement des formulaires bien structurés (classes `.form-label`, `.form-control`, `.form-check`, etc.).
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Activer le thème Bootstrap 5 globalement</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/twig.yaml
twig:
    form_themes:
        - 'bootstrap_5_layout.html.twig'</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Ou appliquer le thème à un seul formulaire</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{% form_theme form 'bootstrap_5_layout.html.twig' %}

{{ form_start(form) }}
    {{ form_row(form.titre, {attr: {placeholder: 'Titre...'}}) }}
    {{ form_row(form.contenu, {attr: {rows: 10}}) }}
    &lt;button class="btn btn-primary"&gt;Enregistrer&lt;/button&gt;
{{ form_end(form) }}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Rendu personnalisé mais compatible Bootstrap</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;div class="mb-3"&gt;
    {{ form_label(form.email, 'Adresse email', {label_attr: {class: 'form-label'}}) }}
    {{ form_widget(form.email, {attr: {class: 'form-control'}}) }}
    {{ form_errors(form.email) }}
    &lt;div class="form-text"&gt;Nous ne partagerons jamais votre email.&lt;/div&gt;
&lt;/div&gt;

&lt;div class="form-check mb-3"&gt;
    {{ form_widget(form.agreeTerms, {attr: {class: 'form-check-input'}}) }}
    {{ form_label(form.agreeTerms, 'Accepter les conditions', {label_attr: {class: 'form-check-label'}}) }}
&lt;/div&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Personnalisation avancée du thème Bootstrap -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Personnalisation avancée (SASS / Webpack Encore)</h2>
                <p class="textExemple">
                    Avec Webpack Encore, vous pouvez surcharger les variables Bootstrap avant l'import pour créer un thème unique.
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Créer un fichier `assets/styles/_custom-bootstrap.scss`</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-scss">// 1. Définir vos propres variables
$primary:       #8B5FBF;   // violet
$secondary:     #6c757d;
$success:       #198754;
$info:          #0dcaf0;
$warning:       #ffc107;
$danger:        #dc3545;

$font-family-base: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto;
$border-radius: 0.5rem;

// 2. Importer les fonctions et variables Bootstrap (obligatoire)
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";
@import "~bootstrap/scss/mixins";

// 3. Écraser les maps (ex: couleurs des boutons)
$custom-colors: (
  "primary": $primary
);
$theme-colors: map-merge($theme-colors, $custom-colors);

// 4. Importer le reste de Bootstrap
@import "~bootstrap/scss/root";
@import "~bootstrap/scss/reboot";
@import "~bootstrap/scss/type";
@import "~bootstrap/scss/images";
@import "~bootstrap/scss/containers";
@import "~bootstrap/scss/grid";
@import "~bootstrap/scss/tables";
@import "~bootstrap/scss/forms";
@import "~bootstrap/scss/buttons";
@import "~bootstrap/scss/transitions";
@import "~bootstrap/scss/dropdown";
@import "~bootstrap/scss/button-group";
@import "~bootstrap/scss/nav";
@import "~bootstrap/scss/navbar";
@import "~bootstrap/scss/card";
@import "~bootstrap/scss/accordion";
@import "~bootstrap/scss/breadcrumb";
@import "~bootstrap/scss/pagination";
@import "~bootstrap/scss/badge";
@import "~bootstrap/scss/alert";
@import "~bootstrap/scss/progress";
@import "~bootstrap/scss/list-group";
@import "~bootstrap/scss/close";
@import "~bootstrap/scss/toasts";
@import "~bootstrap/scss/modal";
@import "~bootstrap/scss/tooltip";
@import "~bootstrap/scss/popover";
@import "~bootstrap/scss/carousel";
@import "~bootstrap/scss/spinners";
@import "~bootstrap/scss/offcanvas";
@import "~bootstrap/scss/utilities";
@import "~bootstrap/scss/utilities/api";</code></pre>
                    </div>
                </div>
                <p class="textExemple">
                    Il suffit ensuite d'importer ce fichier dans `app.scss` à la place du Bootstrap standard, et de compiler avec Encore.
                </p>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Intégration d'une navbar et d'une grille responsive</h3>
                    <p>À partir d'un nouveau projet Symfony, intégrez Bootstrap via AssetMapper ou CDN, puis créez :</p>
                    <ul>
                        <li>Une barre de navigation avec le logo, des liens (Accueil, À propos, Contact) et un bouton de connexion</li>
                        <li>Une grille responsive avec 3 cartes (Bootstrap Cards) présentant des services</li>
                        <li>Un pied de page simple contenant les mentions légales</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir une solution partielle</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-twig">{# templates/home/index.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
&lt;div class="container mt-5"&gt;
    &lt;div class="row"&gt;
        &lt;div class="col-md-4"&gt;
            &lt;div class="card h-100"&gt;
                &lt;div class="card-body"&gt;
                    &lt;h5 class="card-title"&gt;Service 1&lt;/h5&gt;
                    &lt;p class="card-text"&gt;Description du service.&lt;/p&gt;
                    &lt;a href="#" class="btn btn-primary"&gt;En savoir plus&lt;/a&gt;
                &lt;/div&gt;
            &lt;/div&gt;
        &lt;/div&gt;
        {# Répéter pour col-md-4 ... #}
    &lt;/div&gt;
&lt;/div&gt;
{% endblock %}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Personnaliser les variables Bootstrap</h3>
                    <p>En utilisant Webpack Encore, créez un thème personnalisé :</p>
                    <ul>
                        <li>Changez la couleur primaire pour un orange (#F39C12)</li>
                        <li>Augmentez le rayon des bordures à 0.8rem</li>
                        <li>Personnalisez la police par défaut (ex : "Nunito", sans-serif)</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-scss">// assets/styles/app.scss
$primary: #F39C12;
$border-radius: 0.8rem;
$font-family-base: 'Nunito', sans-serif;

@import '~bootstrap/scss/bootstrap';</code></pre>
                            <p>Puis exécutez <code>npm run watch</code> pour compiler.</p>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques et conclusion</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Préférez AssetMapper</strong> pour les projets standards (pas de customisation lourde).</li>
                        <li><strong>Choisissez Webpack Encore</strong> si vous avez besoin de SASS, de variables Bootstrap surchargées ou d'un build front-end complexe.</li>
                        <li><strong>Évitez de mélanger CDN et build local</strong> pour ne pas créer de conflits de versions.</li>
                        <li><strong>Utilisez toujours le thème Bootstrap 5 de Symfony</strong> pour les formulaires – il gère automatiquement les classes d'erreur, les états valid/invalid, etc.</li>
                        <li><strong>Pensez à l'accessibilité</strong> : les composants Bootstrap sont plutôt accessibles, mais vérifiez les attributs ARIA.</li>
                    </ul>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        L'intégration de Bootstrap dans Symfony est simple et flexible, que vous passiez par un simple CDN, AssetMapper ou Webpack Encore.
                        Une fois en place, vous bénéficiez d'une interface moderne et responsive en un temps record. N'hésitez pas à explorer la
                        <a href="https://getbootstrap.com/docs/5.3" target="_blank" class="text-purple">documentation officielle de Bootstrap 5</a>
                        pour découvrir tous ses composants.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'BootstrapSymfonyLesson',

    mounted() {
        // Charger highlight.js + thème VS Code Dark via CDN
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
                    // Charger les langages PHP, Twig, Bash, YAML, SCSS et JavaScript
                    const languages = ['php', 'twig', 'bash', 'yaml', 'scss', 'javascript', 'css'];
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
/* Le style est identique à celui de votre leçon existante */
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