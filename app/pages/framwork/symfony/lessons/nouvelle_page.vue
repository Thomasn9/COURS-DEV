<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Créer une Nouvelle Page dans Symfony</h1>
                <p class="lesson-meta text-white">Maîtrisez le routage, les contrôleurs et les templates pour créer vos propres pages</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à la création de pages</h2>
                <p class="textExemple">
                    Dans Symfony, une page web est le résultat de la collaboration entre trois composants principaux : 
                    la <strong>route</strong>, le <strong>contrôleur</strong> et le <strong>template</strong>.
                </p>
                <p class="textExemple">
                    Cette leçon vous guidera à travers les étapes nécessaires pour créer une page complète dans Symfony.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Architecture MVC d'une page Symfony</span>
Route (URL) → Contrôleur (Logique) → Template (Vue) → Page HTML</code></pre>
                </div>
            </div>

            <!-- Les 3 étapes fondamentales -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 3 étapes fondamentales</h2>
                <p class="textExemple">
                    Pour créer une nouvelle page dans Symfony, vous devez suivre ces trois étapes :
                </p>
                <ol class="textExemple">
                    <li><strong>Définir une route</strong> : Associer une URL à votre page</li>
                    <li><strong>Créer un contrôleur</strong> : Implémenter la logique métier</li>
                    <li><strong>Créer un template</strong> : Définir l'affichage HTML</li>
                </ol>
            </div>

            <!-- Étape 1 : Création du contrôleur avec symfony make:controller -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : Créer un contrôleur avec symfony make:controller</h2>
                <p class="textExemple">
                    La façon la plus simple et recommandée de créer un contrôleur dans Symfony est d'utiliser la commande <code>symfony make:controller</code>.
                    Cette commande vous guide pas à pas et crée automatiquement tous les fichiers nécessaires.
                </p>

                <h3 class="text-purple">1. Lancez la commande</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console make:controller</span></code></pre>
                </div>

                <h3 class="text-purple">2. Suivez les instructions interactives</h3>
                <p class="textExemple">
                    La commande est interactive et vous posera quelques questions pour configurer votre contrôleur :
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console make:controller</span>

<span class="bash-comment"># Symfony va vous demander plusieurs informations :</span>

<span class="bash-string">Quel nom souhaitez-vous donner à votre classe de contrôleur ?</span>
<span class="bash-parameter">[ex: VictoriousPenguinController]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">AboutController</span>

<span class="bash-string">Voulez-vous générer une méthode avec une route ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Quelle route souhaitez-vous ? (ex: /blog) [/about]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">/about</span>

<span class="bash-string">Quel nom souhaitez-vous donner à la route ? [about]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">about</span>

<span class="bash-comment"># Symfony va générer automatiquement :</span>
<span class="bash-success">✓ Création de src/Controller/AboutController.php</span>
<span class="bash-success">✓ Création de templates/about/index.html.twig</span>
<span class="bash-success">✓ Mise à jour de config/routes.yaml</span>

<span class="bash-success">Votre contrôleur a été généré avec succès !</span></code></pre>
                </div>

                <h3 class="text-purple">3. Vérifiez les fichiers générés</h3>
                <p class="textExemple">
                    Après avoir exécuté la commande, Symfony aura créé deux fichiers :
                </p>
                <ul class="textExemple">
                    <li><strong>src/Controller/AboutController.php</strong> : Votre contrôleur avec la logique PHP</li>
                    <li><strong>templates/about/index.html.twig</strong> : Le template Twig pour l'affichage</li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Structure du contrôleur généré</h4>
                    <pre v-pre><code class="language-php"><span class="php-comment">// src/Controller/AboutController.php</span>
<span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Controller</span>;

<span class="php-keyword">use</span> Symfony\<span class="php-class">Bundle</span>\<span class="php-class">FrameworkBundle</span>\<span class="php-class">Controller</span>\<span class="php-class">AbstractController</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">HttpFoundation</span>\<span class="php-class">Response</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">Routing</span>\<span class="php-class">Annotation</span>\<span class="php-class">Route</span>;

<span class="php-keyword">class</span> <span class="php-class">AboutController</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractController</span>
{
    #[<span class="php-function">Route</span>(<span class="php-string">'/about'</span>, <span class="php-variable">name</span>: <span class="php-string">'about'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">index</span>(): <span class="php-class">Response</span>
    {
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'about/index.html.twig'</span>, [
            <span class="php-string">'controller_name'</span> =&gt; <span class="php-string">'AboutController'</span>,
        ]);
    }
}</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Structure du template généré</h4>
                    <pre v-pre><code class="language-twig"><span class="bash-comment">{# templates/about/index.html.twig #}</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">extends</span> <span class="twig-string">'base.html.twig'</span> <span class="twig-keyword">%}</span>

<span class="twig-keyword">{%</span> <span class="twig-tag">block</span> title <span class="twig-keyword">%}</span>Hello AboutController!<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span>

<span class="twig-keyword">{%</span> <span class="twig-tag">block</span> body <span class="twig-keyword">%}</span>
<span class="twig-template">&lt;div class="example-wrapper"&gt;
    &lt;h1&gt;Hello {{ controller_name }}! &lt;/h1&gt;
    
    &lt;p&gt;Votre page about fonctionne correctement.&lt;/p&gt;
&lt;/div&gt;</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span></code></pre>
                </div>

                <h3 class="text-purple">Options avancées de la commande</h3>
                <p class="textExemple">
                    Vous pouvez également utiliser la commande avec des options pour gagner du temps :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Créer un contrôleur avec tous les paramètres en une ligne</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer un contrôleur avec un nom spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller AboutController</span>

<span class="bash-comment"># Créer un contrôleur avec une route personnalisée</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller --route=/a-propos --template=about/index AboutController</span>

<span class="bash-comment"># Créer un contrôleur sans route (pour l'ajouter manuellement)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller --no-route DashboardController</span>

<span class="bash-comment"># Voir toutes les options disponibles</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller --help</span></code></pre>
                </div>

                <h3 class="text-purple">Avantages de symfony make:controller</h3>
                <ul class="textExemple">
                    <li><strong>Génération automatique</strong> : Crée à la fois le contrôleur et le template</li>
                    <li><strong>Configuration des routes</strong> : Ajoute automatiquement la route dans le bon fichier</li>
                    <li><strong>Structure standardisée</strong> : Respecte les conventions Symfony</li>
                    <li><strong>Économie de temps</strong> : Pas besoin de créer les fichiers manuellement</li>
                    <li><strong>Interactif</strong> : Vous guide à travers le processus</li>
                </ul>

                <div class="code-example tip">
                    <h4 class="text-purple">Astuce pratique</h4>
                    <p class="textExemple">
                        Si vous voulez créer rapidement plusieurs contrôleurs pour différentes sections de votre site :
                    </p>
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller HomeController</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller BlogController</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller ContactController</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller Admin/DashboardController</span></code></pre>
                    <p class="textExemple">
                        Pour les contrôleurs dans un sous-dossier, utilisez la notation avec <code>/</code>.
                    </p>
                </div>
            </div>

            <!-- Étape 2 : Personnaliser la route -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Personnaliser la route</h2>
                <p class="textExemple">
                    Par défaut, Symfony crée une route simple. Vous pouvez la personnaliser selon vos besoins :
                </p>

                <h3 class="text-purple">Routes de base</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Route simple</span>
#[<span class="php-function">Route</span>(<span class="php-string">'/a-propos'</span>, <span class="php-variable">name</span>: <span class="php-string">'about'</span>)]

<span class="php-comment">// Route avec plusieurs URLs</span>
#[<span class="php-function">Route</span>([<span class="php-string">'/a-propos'</span>, <span class="php-string">'/about'</span>, <span class="php-string">'/qui-sommes-nous'</span>], <span class="php-variable">name</span>: <span class="php-string">'about'</span>)]

<span class="php-comment">// Route avec paramètre</span>
#[<span class="php-function">Route</span>(<span class="php-string">'/article/{id}'</span>, <span class="php-variable">name</span>: <span class="php-string">'article_show'</span>)]
<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">show</span>(<span class="php-variable">$id</span>): <span class="php-class">Response</span>
{
    <span class="php-comment">// $id contiendra la valeur de l'URL</span>
}</code></pre>
                </div>

                <h3 class="text-purple">Routes avec méthodes HTTP spécifiques</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Route accessible seulement en GET</span>
#[<span class="php-function">Route</span>(<span class="php-string">'/contact'</span>, <span class="php-variable">name</span>: <span class="php-string">'contact'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'GET'</span>])]

<span class="php-comment">// Route pour un formulaire (GET pour afficher, POST pour soumettre)</span>
#[<span class="php-function">Route</span>(<span class="php-string">'/contact'</span>, <span class="php-variable">name</span>: <span class="php-string">'contact'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'GET'</span>, <span class="php-string">'POST'</span>])]</code></pre>
                </div>

                <h3 class="text-purple">Routes avec paramètres optionnels</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Paramètre optionnel avec valeur par défaut</span>
#[<span class="php-function">Route</span>(<span class="php-string">'/blog/{page}'</span>, <span class="php-variable">name</span>: <span class="php-string">'blog_list'</span>, <span class="php-variable">defaults</span>: [<span class="php-string">'page'</span> =&gt; <span class="php-number">1</span>])]
<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">list</span>(<span class="php-variable">$page</span> = <span class="php-number">1</span>): <span class="php-class">Response</span>
{
    <span class="php-comment">// $page vaudra 1 si non spécifié dans l'URL</span>
}</code></pre>
                </div>
            </div>

            <!-- Étape 3 : Créer le template -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Créer et personnaliser le template</h2>
                <p class="textExemple">
                    Symfony utilise le moteur de template <strong>Twig</strong>. Le template généré automatiquement se trouve dans <code>templates/about/index.html.twig</code>
                </p>

                <h3 class="text-purple">Template de base généré</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-twig"><span class="bash-comment">{# templates/about/index.html.twig #}</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">extends</span> <span class="twig-string">'base.html.twig'</span> <span class="twig-keyword">%}</span>

<span class="twig-keyword">{%</span> <span class="twig-tag">block</span> title <span class="twig-keyword">%}</span>Hello AboutController!<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span>

<span class="twig-keyword">{%</span> <span class="twig-tag">block</span> body <span class="twig-keyword">%}</span>
<span class="twig-template">&lt;style&gt;
    .example-wrapper { margin: 1em auto; max-width: 800px; width: 95%; font: 18px/1.5 sans-serif; }
    .example-wrapper code { background: #F5F5F5; padding: 2px 6px; }
&lt;/style&gt;

&lt;div class="example-wrapper"&gt;
    &lt;h1&gt;Hello {{ controller_name }}! &lt;/h1&gt;

    This friendly message is coming from:
    &lt;ul&gt;
        &lt;li&gt;Your controller at &lt;code&gt;&lt;a href="{{ '<span class="twig-variable">src</span>/<span class="twig-variable">Controller</span>/<span class="twig-variable">AboutController</span>.<span class="twig-variable">php</span>'|file_link(0) }}"&gt;src/Controller/AboutController.php&lt;/a&gt;&lt;/code&gt;&lt;/li&gt;
        &lt;li&gt;Your template at &lt;code&gt;&lt;a href="{{ '<span class="twig-variable">templates</span>/<span class="twig-variable">about</span>/<span class="twig-variable">index</span>.<span class="twig-variable">html</span>.<span class="twig-variable">twig</span>'|file_link(0) }}"&gt;templates/about/index.html.twig&lt;/a&gt;&lt;/code&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span></code></pre>
                </div>

                <h3 class="text-purple">Personnalisation du template</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-twig"><span class="bash-comment">{# templates/about/index.html.twig - Version personnalisée #}</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">extends</span> <span class="twig-string">'base.html.twig'</span> <span class="twig-keyword">%}</span>

<span class="twig-keyword">{%</span> <span class="twig-tag">block</span> title <span class="twig-keyword">%}</span>À propos de nous<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span>

<span class="twig-keyword">{%</span> <span class="twig-tag">block</span> body <span class="twig-keyword">%}</span>
<span class="twig-template">&lt;div class="container my-5"&gt;
    &lt;div class="row"&gt;
        &lt;div class="col-12"&gt;
            &lt;h1 class="text-center mb-4"&gt;À propos de notre entreprise&lt;/h1&gt;
            
            &lt;div class="card shadow-lg"&gt;
                &lt;div class="card-body"&gt;
                    &lt;h2 class="card-title"&gt;Notre mission&lt;/h2&gt;
                    &lt;p class="card-text"&gt;
                        Nous nous engageons à fournir les meilleurs services à nos clients
                        avec innovation et qualité.
                    &lt;/p&gt;
                    
                    &lt;h3 class="mt-4"&gt;Nos valeurs&lt;/h3&gt;
                    &lt;ul class="list-group list-group-flush"&gt;
                        &lt;li class="list-group-item"&gt;Intégrité et transparence&lt;/li&gt;
                        &lt;li class="list-group-item"&gt;Innovation constante&lt;/li&gt;
                        &lt;li class="list-group-item"&gt;Satisfaction client&lt;/li&gt;
                        &lt;li class="list-group-item"&gt;Travail d'équipe&lt;/li&gt;
                    &lt;/ul&gt;
                    
                    &lt;div class="mt-4"&gt;
                        &lt;a href="{{ path('contact') }}" class="btn btn-primary"&gt;
                            Nous contacter
                        &lt;/a&gt;
                    &lt;/div&gt;
                &lt;/div&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span></code></pre>
                </div>
            </div>

            <!-- Passer des données au template -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Passer des données du contrôleur au template</h2>
                <p class="textExemple">
                    Vous pouvez passer n'importe quelle donnée du contrôleur au template via un tableau associatif :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Contrôleur avec données</h4>
                    <pre v-pre><code class="language-php"><span class="php-keyword">class</span> <span class="php-class">AboutController</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractController</span>
{
    #[<span class="php-function">Route</span>(<span class="php-string">'/about'</span>, <span class="php-variable">name</span>: <span class="php-string">'about'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">index</span>(): <span class="php-class">Response</span>
    {
        <span class="php-variable">$teamMembers</span> = [
            [
                <span class="php-string">'name'</span> =&gt; <span class="php-string">'Jean Dupont'</span>,
                <span class="php-string">'role'</span> =&gt; <span class="php-string">'CEO'</span>,
                <span class="php-string">'email'</span> =&gt; <span class="php-string">'jean@example.com'</span>
            ],
            [
                <span class="php-string">'name'</span> =&gt; <span class="php-string">'Marie Curie'</span>,
                <span class="php-string">'role'</span> =&gt; <span class="php-string">'CTO'</span>,
                <span class="php-string">'email'</span> =&gt; <span class="php-string">'marie@example.com'</span>
            ]
        ];

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'about/index.html.twig'</span>, [
            <span class="php-string">'team'</span> =&gt; <span class="php-variable">$teamMembers</span>,
            <span class="php-string">'company_name'</span> =&gt; <span class="php-string">'Symfony Corp'</span>,
            <span class="php-string">'founded_year'</span> =&gt; <span class="php-number">2024</span>,
            <span class="php-string">'is_active'</span> =&gt; <span class="php-keyword">true</span>
        ]);
    }
}</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Template utilisant les données</h4>
                    <pre v-pre><code class="language-twig"><span class="twig-keyword">{%</span> <span class="twig-tag">block</span> body <span class="twig-keyword">%}</span>
<span class="twig-template">&lt;div class="container"&gt;
    &lt;h1&gt;À propos de {{ company_name }}&lt;/h1&gt;
    &lt;p&gt;Fondée en {{ founded_year }}&lt;/p&gt;
    
    {% if is_active %}
        &lt;div class="alert alert-success"&gt;Entreprise active&lt;/div&gt;
    {% endif %}
    
    &lt;h2&gt;Notre équipe&lt;/h2&gt;
    &lt;div class="row"&gt;
        {% for member in team %}
            &lt;div class="col-md-4 mb-3"&gt;
                &lt;div class="card"&gt;
                    &lt;div class="card-body"&gt;
                        &lt;h5 class="card-title"&gt;{{ member.name }}&lt;/h5&gt;
                        &lt;h6 class="card-subtitle mb-2 text-muted"&gt;{{ member.role }}&lt;/h6&gt;
                        &lt;a href="mailto:{{ member.email }}" class="card-link"&gt;{{ member.email }}&lt;/a&gt;
                    &lt;/div&gt;
                &lt;/div&gt;
            &lt;/div&gt;
        {% endfor %}
    &lt;/div&gt;
&lt;/div&gt;</span>
<span class="twig-keyword">{%</span> <span class="twig-tag">endblock</span> <span class="twig-keyword">%}</span></code></pre>
                </div>
            </div>

            <!-- Exemple complet : Page de blog -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple complet : Page d'article de blog</h2>
                <p class="textExemple">
                    Créons une page d'article de blog complète avec paramètre d'URL :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Création du contrôleur Blog</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créons d'abord le contrôleur</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller BlogController</span>

<span class="bash-string">Quelle route souhaitez-vous ? (ex: /blog) [/blog]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">/blog</span>

<span class="bash-string">Quel nom souhaitez-vous donner à la route ? [blog]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">blog_index</span>

<span class="bash-success">✓ Création de src/Controller/BlogController.php</span>
<span class="bash-success">✓ Création de templates/blog/index.html.twig</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">BlogController.php</h4>
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Controller</span>;

<span class="php-keyword">use</span> Symfony\<span class="php-class">Bundle</span>\<span class="php-class">FrameworkBundle</span>\<span class="php-class">Controller</span>\<span class="php-class">AbstractController</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">HttpFoundation</span>\<span class="php-class">Response</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">Routing</span>\<span class="php-class">Annotation</span>\<span class="php-class">Route</span>;

<span class="php-keyword">class</span> <span class="php-class">BlogController</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractController</span>
{
    #[<span class="php-function">Route</span>(<span class="php-string">'/blog'</span>, <span class="php-variable">name</span>: <span class="php-string">'blog_index'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">index</span>(): <span class="php-class">Response</span>
    {
        <span class="php-variable">$articles</span> = [
            [
                <span class="php-string">'id'</span> =&gt; <span class="php-number">1</span>,
                <span class="php-string">'title'</span> =&gt; <span class="php-string">'Mon premier article Symfony'</span>,
                <span class="php-string">'content'</span> =&gt; <span class="php-string">'Contenu de mon premier article...'</span>,
                <span class="php-string">'published_at'</span> =&gt; <span class="php-keyword">new</span> \<span class="php-class">DateTime</span>(<span class="php-string">'2024-01-15'</span>)
            ],
            [
                <span class="php-string">'id'</span> =&gt; <span class="php-number">2</span>,
                <span class="php-string">'title'</span> =&gt; <span class="php-string">'Les contrôleurs Symfony'</span>,
                <span class="php-string">'content'</span> =&gt; <span class="php-string">'Tout sur les contrôleurs...'</span>,
                <span class="php-string">'published_at'</span> =&gt; <span class="php-keyword">new</span> \<span class="php-class">DateTime</span>(<span class="php-string">'2024-01-20'</span>)
            ]
        ];

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'blog/index.html.twig'</span>, [
            <span class="php-string">'articles'</span> =&gt; <span class="php-variable">$articles</span>,
        ]);
    }

    #[<span class="php-function">Route</span>(<span class="php-string">'/blog/{id}'</span>, <span class="php-variable">name</span>: <span class="php-string">'blog_show'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">show</span>(<span class="php-variable">$id</span>): <span class="php-class">Response</span>
    {
        <span class="php-comment">// En réalité, vous iriez chercher l'article en base de données</span>
        <span class="php-variable">$article</span> = [
            <span class="php-string">'id'</span> =&gt; <span class="php-variable">$id</span>,
            <span class="php-string">'title'</span> =&gt; <span class="php-string">'Article ' . $id</span>,
            <span class="php-string">'content'</span> =&gt; <span class="php-string">'Contenu détaillé de l\'article ' . $id</span>,
            <span class="php-string">'author'</span> =&gt; <span class="php-string">'Auteur ' . $id</span>,
            <span class="php-string">'published_at'</span> =&gt; <span class="php-keyword">new</span> \<span class="php-class">DateTime</span>()
        ];

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'blog/show.html.twig'</span>, [
            <span class="php-string">'article'</span> =&gt; <span class="php-variable">$article</span>,
        ]);
    }
}</code></pre>
                </div>
            </div>

            <!-- Vérifier et tester les routes -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Vérifier et tester vos routes</h2>
                <p class="textExemple">
                    Symfony fournit des outils pour vérifier et tester vos routes :
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Lister toutes les routes</h4>
                        <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console debug:router</span></code></pre>
                    </div>a sémentique des bloc twig dans symfony

                    <div class="code-example">
                        <h4 class="text-purple">Voir les détails d'une route</h4>
                        <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console debug:router about</span></code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Exemple de sortie de debug:router</h4>
                    <pre v-pre><code class="language-bash"> <span class="bash-comment"># Liste des routes disponibles</span>
 -------------------------- -------- -------- ------ ----------------------------------- 
  <span class="bash-string">Name</span>                       <span class="bash-string">Method</span>   <span class="bash-string">Scheme</span>   <span class="bash-string">Host</span>   <span class="bash-string">Path</span>                                  
 -------------------------- -------- -------- ------ ----------------------------------- 
  <span class="bash-command">about</span>                     <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>    <span class="bash-string">/about</span>                               
  <span class="bash-command">blog_index</span>               <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>    <span class="bash-string">/blog</span>                                
  <span class="bash-command">blog_show</span>                <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>    <span class="bash-string">/blog/{id}</span>                           
  <span class="bash-command">app_home</span>                 <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>      <span class="bash-keyword">ANY</span>    <span class="bash-string">/</span>                                     
 -------------------------- -------- -------- ------ -----------------------------------</code></pre>
                </div>

                <h3 class="text-purple">Tester vos pages</h3>
                <p class="textExemple">
                    Après avoir créé vos contrôleurs et templates, démarrez le serveur et testez vos pages :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony server:start</span>

<span class="bash-comment"># Dans votre navigateur, visitez :</span>
http://localhost:8000/about
http://localhost:8000/blog
http://localhost:8000/blog/1</code></pre>
                </div>
            </div>

            <!-- Bonnes pratiques -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul class="textExemple">
                    <li><strong>Nommage des routes</strong> : Utilisez des noms descriptifs (ex: <code>about</code>, <code>blog_show</code>, <code>user_profile</code>)</li>
                    <li><strong>Structure des contrôleurs</strong> : Gardez vos contrôleurs légers, déplacez la logique métier dans des services</li>
                    <li><strong>Organisation des templates</strong> : Créez un répertoire par contrôleur dans <code>templates/</code></li>
                    <li><strong>Validation des paramètres</strong> : Utilisez les <code>requirements</code> pour valider les paramètres d'URL</li>
                    <li><strong>Sécurité</strong> : Restreignez l'accès aux routes sensibles avec les annotations de sécurité</li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Exemple de route sécurisée</h4>
                    <pre v-pre><code class="language-php"><span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">Security</span>\<span class="php-class">Http</span>\<span class="php-class">Attribute</span>\<span class="php-class">IsGranted</span>;

#[<span class="php-function">Route</span>(<span class="php-string">'/admin/dashboard'</span>, <span class="php-variable">name</span>: <span class="php-string">'admin_dashboard'</span>)]
#[<span class="php-function">IsGranted</span>(<span class="php-string">'ROLE_ADMIN'</span>)]
<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">dashboard</span>(): <span class="php-class">Response</span>
{
    <span class="php-comment">// Seuls les utilisateurs avec ROLE_ADMIN peuvent accéder</span>
}</code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer une application de portfolio avec plusieurs pages.
                    </p>
                    <ol class="textExemple">
                        <li>Créez un contrôleur <code>PortfolioController</code> avec <code>symfony make:controller</code></li>
                        <li>Ajoutez trois routes :
                            <ul>
                                <li><code>/portfolio</code> - Page d'accueil du portfolio</li>
                                <li><code>/portfolio/projets</code> - Liste des projets</li>
                                <li><code>/portfolio/projet/{slug}</code> - Détail d'un projet (avec paramètre slug)</li>
                            </ul>
                        </li>
                        <li>Créez les templates correspondants</li>
                        <li>Passez des données fictives (projets, informations personnelles) aux templates</li>
                        <li>Ajoutez une navigation entre les pages</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Étapes de la solution :</h4>
                        <div class="code-example">
                            <pre v-pre><code class="language-bash"><span class="bash-comment"># 1. Créer le contrôleur principal</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller PortfolioController</span>

<span class="bash-string">Quelle route souhaitez-vous ? (ex: /blog) [/portfolio]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">/portfolio</span>

<span class="bash-string">Quel nom souhaitez-vous donner à la route ? [portfolio]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">portfolio_home</span>

<span class="bash-comment"># 2. Modifier le contrôleur pour ajouter les autres méthodes</span>
<span class="bash-comment"># 3. Créer les templates dans templates/portfolio/</span>
<span class="bash-comment"># 4. Ajouter la navigation dans base.html.twig</span></code></pre>
                        </div>
                        
                        <h5 class="text-purple">PortfolioController.php :</h5>
                        <div class="code-example">
                            <pre v-pre><code class="language-php"><span class="php-keyword">class</span> <span class="php-class">PortfolioController</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractController</span>
{
    #[<span class="php-function">Route</span>(<span class="php-string">'/portfolio'</span>, <span class="php-variable">name</span>: <span class="php-string">'portfolio_home'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">home</span>(): <span class="php-class">Response</span>
    {
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'portfolio/home.html.twig'</span>, [
            <span class="php-string">'name'</span> =&gt; <span class="php-string">'John Doe'</span>,
            <span class="php-string">'title'</span> =&gt; <span class="php-string">'Développeur Web'</span>
        ]);
    }

    #[<span class="php-function">Route</span>(<span class="php-string">'/portfolio/projets'</span>, <span class="php-variable">name</span>: <span class="php-string">'portfolio_projects'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">projects</span>(): <span class="php-class">Response</span>
    {
        <span class="php-variable">$projects</span> = [
            [<span class="php-string">'name'</span> =&gt; <span class="php-string">'Site E-commerce'</span>, <span class="php-string">'description'</span> =&gt; <span class="php-string">'Boutique en ligne complète'</span>],
            [<span class="php-string">'name'</span> =&gt; <span class="php-string">'Application Mobile'</span>, <span class="php-string">'description'</span> =&gt; <span class="php-string">'App iOS et Android'</span>],
            [<span class="php-string">'name'</span> =&gt; <span class="php-string">'Dashboard Admin'</span>, <span class="php-string">'description'</span> =&gt; <span class="php-string">'Interface d\'administration'</span>]
        ];
        
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'portfolio/projects.html.twig'</span>, [
            <span class="php-string">'projects'</span> =&gt; <span class="php-variable">$projects</span>
        ]);
    }

    #[<span class="php-function">Route</span>(<span class="php-string">'/portfolio/projet/{slug}'</span>, <span class="php-variable">name</span>: <span class="php-string">'portfolio_project_show'</span>)]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">projectShow</span>(<span class="php-variable">$slug</span>): <span class="php-class">Response</span>
    {
        <span class="php-variable">$project</span> = [
            <span class="php-string">'slug'</span> =&gt; <span class="php-variable">$slug</span>,
            <span class="php-string">'name'</span> =&gt; <span class="php-string">'Projet ' . ucfirst($slug)</span>,
            <span class="php-string">'description'</span> =&gt; <span class="php-string">'Description détaillée du projet ' . $slug</span>
        ];
        
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'portfolio/project_show.html.twig'</span>, [
            <span class="php-string">'project'</span> =&gt; <span class="php-variable">$project</span>
        ]);
    }
}</code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>
                <p class="textExemple">
                    Félicitations ! Vous maîtrisez maintenant les bases de la création de pages dans Symfony.
                    Vous avez appris à utiliser <code>symfony make:controller</code> pour générer rapidement des contrôleurs,
                    à personnaliser les routes et à créer des templates dynamiques avec Twig.
                </p>

                <h3 class="text-purple">Résumé des commandes importantes</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer un contrôleur (interactif)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller</span>

<span class="bash-comment"># Créer un contrôleur avec un nom spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller AboutController</span>

<span class="bash-comment"># Lister toutes les routes</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console debug:router</span>

<span class="bash-comment"># Démarrer le serveur de développement</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony server:start</span>

<span class="bash-comment"># Afficher l'aide pour une commande</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller --help</span></code></pre>
                </div>

                <h3 class="text-purple">Prochaines étapes :</h3>
                <ul class="textExemple">
                    <li>Apprendre à utiliser les formulaires Symfony avec <code>symfony make:form</code></li>
                    <li>Découvrir l'intégration avec des bases de données via Doctrine et <code>symfony make:entity</code></li>
                    <li>Explorer les services et l'injection de dépendances</li>
                    <li>Mettre en place l'authentification avec <code>symfony make:user</code> et <code>symfony make:auth</code></li>
                </ul>

                <h3 class="text-purple">Ressources supplémentaires :</h3>
                <ul class="textExemple">
                    <li><a href="https://symfony.com/doc/current/controller.html" target="_blank"
                            class="btn-purple btn-hover">Documentation officielle des contrôleurs</a></li>
                    <li><a href="https://symfony.com/doc/current/routing.html" target="_blank"
                            class="btn-purple btn-hover">Documentation officielle du routage</a></li>
                    <li><a href="https://twig.symfony.com/doc/3.x/" target="_blank" class="btn-purple btn-hover">Documentation de Twig</a></li>
                    <li><a href="https://symfonycasts.com/screencast/symfony" target="_blank" class="btn-purple btn-hover">Tutoriels vidéo SymfonyCasts</a></li>
                    <li><a href="https://symfony.com/doc/current/the-fast-track/fr/" target="_blank" class="btn-purple btn-hover">Le Fast Track (Symfony en français)</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyLessonPage',
    
    mounted() {
        // Optionnel : Ajouter la coloration syntaxique si vous utilisez Prism.js ou similaire
        if (typeof Prism !== 'undefined') {
            Prism.highlightAll();
        }
    }
}
</script>

<style scoped>
/* Votre CSS reste inchangé */
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
    word-wrap: break-word;
    word-break: break-word;
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* COULEURS GIT BASH */
.bash-prompt {
    color: #2ECC71 !important;
    font-weight: bold;
}

.bash-command {
    color: #F1C40F !important;
}

.bash-comment {
    color: #7F8C8D !important;
    font-style: italic;
}

.bash-string {
    color: #E74C3C !important;
}

.bash-keyword {
    color: #3498DB !important;
}

.bash-parameter {
    color: #9B59B6 !important;
}

.bash-number {
    color: #1ABC9C !important;
}

/* NOUVELLE CLASSE POUR LE TEXTE EN SURBRILLANCE */
.bash-highlight {
    color: #FF9800 !important;
    font-weight: bold;
    background-color: rgba(255, 152, 0, 0.1);
    padding: 2px 4px;
    border-radius: 3px;
}

/* COULEURS POUR PHP */
.php-keyword {
    color: #569CD6 !important;
}

.php-function {
    color: #DCDCAA !important;
}

.php-class {
    color: #4EC9B0 !important;
}

.php-variable {
    color: #9CDCFE !important;
}

.php-string {
    color: #CE9178 !important;
}

.php-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.php-number {
    color: #B5CEA8 !important;
}

/* COULEURS POUR TWIG */
.twig-keyword {
    color: #C586C0 !important;
}

.twig-tag {
    color: #569CD6 !important;
}

.twig-string {
    color: #CE9178 !important;
}

.twig-variable {
    color: #9CDCFE !important;
}

.twig-template {
    color: #D4D4D4 !important;
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

/* Styles pour les conseils et astuces */
.tip {
    background: linear-gradient(135deg, rgba(139, 95, 191, 0.1) 0%, rgba(106, 48, 147, 0.1) 100%);
    border-left: 4px solid #8B5FBF;
    padding: 1.5rem;
    border-radius: 8px;
    margin: 1.5rem 0;
}

.tip h4 {
    color: #6A3093;
    margin-top: 0;
    display: flex;
    align-items: center;
    gap: 10px;
}

.tip h4::before {
    content: '💡';
    font-size: 1.2rem;
}

/* Styles pour les messages de succès */
.bash-success {
    color: #2ECC71 !important;
    font-weight: bold;
}
</style>