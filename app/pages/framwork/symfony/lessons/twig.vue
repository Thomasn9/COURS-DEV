<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white" v-pre>Twig avec Symfony</h1>
                <p class="lesson-meta text-white" v-pre>Le moteur de template Twig dans l'écosystème Symfony</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Introduction à Twig</h2>
                <p class="textExemple" v-pre>
                    Twig est un moteur de template moderne et flexible pour PHP, créé par les développeurs de Symfony.
                    Il est conçu pour être rapide, sécurisé et facile à utiliser. Dans Symfony, Twig est le moteur
                    de template par défaut pour générer des vues HTML.
                </p>
                <p class="textExemple" v-pre>
                    Twig sépare clairement la logique métier de la présentation, ce qui rend le code plus maintenable
                    et facilite la collaboration entre développeurs et designers.
                </p>
            </section>

            <!-- Installation et configuration -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Installation et Configuration</h2>
                <p class="textExemple" v-pre>
                    Dans un projet Symfony, Twig est généralement installé par défaut. Si ce n'est pas le cas,
                    vous pouvez l'installer avec Composer :
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-bash"><span class="comment"># Installation de Twig</span>
<span class="function">composer</span> <span class="variable">require</span> twig</code></pre>
                </div>

                <p class="textExemple" v-pre>
                    La configuration de Twig se fait dans le fichier <code>config/packages/twig.yaml</code> :
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-yaml"><span class="variable">twig</span>:
    <span class="property">default_path</span>: <span class="string">'%kernel.project_dir%/templates'</span>
    <span class="property">debug</span>: <span class="string">'%kernel.debug%'</span>
    <span class="property">strict_variables</span>: <span class="string">'%kernel.debug%'</span></code></pre>
                </div>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Syntaxe de Base de Twig</h2>
                <p class="textExemple" v-pre>
                    Twig utilise une syntaxe simple et expressive. Voici les éléments fondamentaux :
                </p>

                <h3 class="text-purple" v-pre>Affichage de variables</h3>
                <div class="code-comparison" v-pre>
                    <div>
                        <h4>Code Twig</h4>
                        <pre><code class="language-twig"><span class="template-tag">{{</span> <span class="variable">variable</span> <span class="template-tag">}}</span>
<span class="template-tag">{{</span> <span class="variable">user</span><span class="operator">.</span><span class="property">name</span> <span class="template-tag">}}</span>
<span class="template-tag">{{</span> <span class="variable">products</span><span class="operator">|</span><span class="function">length</span> <span class="template-tag">}}</span></code></pre>
                    </div>
                    <div>
                        <h4>Résultat</h4>
                        <pre><code class="language-html"><span class="text">Valeur de la variable</span>
<span class="text">Nom de l'utilisateur</span>
<span class="text">Nombre de produits</span></code></pre>
                    </div>
                </div>

                <h3 class="text-purple" v-pre>Structures de contrôle</h3>
                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{%</span> <span class="keyword">if</span> <span class="variable">user</span><span class="operator">.</span><span class="property">isActive</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p&gt;</span>Bienvenue <span class="template-tag">{{</span> <span class="variable">user</span><span class="operator">.</span><span class="property">name</span> <span class="template-tag">}}</span>!<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">elseif</span> <span class="variable">user</span><span class="operator">.</span><span class="property">isPending</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p&gt;</span>Votre compte est en attente de validation.<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">else</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p&gt;</span>Veuillez vous connecter.<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">endif</span> <span class="template-tag">%}</span>

<span class="template-tag">{%</span> <span class="keyword">for</span> <span class="variable">product</span> <span class="keyword">in</span> <span class="variable">products</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;li&gt;</span><span class="template-tag">{{</span> <span class="variable">product</span><span class="operator">.</span><span class="property">name</span> <span class="template-tag">}}</span> - <span class="template-tag">{{</span> <span class="variable">product</span><span class="operator">.</span><span class="property">price</span> <span class="template-tag">}}</span>€<span class="html-tag">&lt;/li&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">endfor</span> <span class="template-tag">%}</span></code></pre>
                </div>
            </section>

            <!-- Filtres et fonctions -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Filtres et Fonctions</h2>
                <p class="textExemple" v-pre>
                    Twig propose de nombreux filtres et fonctions pour manipuler les données. Voici quelques exemples
                    courants :
                </p>

                <h3 class="text-purple" v-pre>Filtres utiles</h3>
                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{{</span> <span class="string">"hello world"</span><span class="operator">|</span><span class="function">upper</span> <span class="template-tag">}}</span> <span class="comment">{# HELLO WORLD #}</span>
<span class="template-tag">{{</span> <span class="string">"HELLO WORLD"</span><span class="operator">|</span><span class="function">lower</span> <span class="template-tag">}}</span> <span class="comment">{# hello world #}</span>
<span class="template-tag">{{</span> <span class="string">"hello world"</span><span class="operator">|</span><span class="function">capitalize</span> <span class="template-tag">}}</span> <span class="comment">{# Hello world #}</span>
<span class="template-tag">{{</span> <span class="string">"hello world"</span><span class="operator">|</span><span class="function">title</span> <span class="template-tag">}}</span> <span class="comment">{# Hello World #}</span>
<span class="template-tag">{{</span> <span class="string">"  hello  "</span><span class="operator">|</span><span class="function">trim</span> <span class="template-tag">}}</span> <span class="comment">{# hello #}</span>
<span class="template-tag">{{</span> <span class="string">"hello world"</span><span class="operator">|</span><span class="function">replace</span>({<span class="string">"hello"</span>: <span class="string">"hi"</span>}) <span class="template-tag">}}</span> <span class="comment">{# hi world #}</span>
<span class="template-tag">{{</span> <span class="variable">date</span><span class="operator">|</span><span class="function">date</span>(<span class="string">'d/m/Y'</span>) <span class="template-tag">}}</span> <span class="comment">{# 15/03/2023 #}</span>
<span class="template-tag">{{</span> <span class="variable">price</span><span class="operator">|</span><span class="function">number_format</span>(<span class="number">2</span>, <span class="string">','</span>, <span class="string">' '</span>) <span class="template-tag">}}</span> <span class="comment">{# 1 234,56 #}</span></code></pre>
                </div>

                <h3 class="text-purple" v-pre>Fonctions utiles</h3>
                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{{</span> <span class="function">path</span>(<span class="string">'route_name'</span>) <span class="template-tag">}}</span> <span class="comment">{# Génère une URL #}</span>
<span class="template-tag">{{</span> <span class="function">url</span>(<span class="string">'route_name'</span>) <span class="template-tag">}}</span> <span class="comment">{# Génère une URL absolue #}</span>
<span class="template-tag">{{</span> <span class="function">asset</span>(<span class="string">'images/logo.png'</span>) <span class="template-tag">}}</span> <span class="comment">{# Chemin vers un asset #}</span>
<span class="template-tag">{{</span> <span class="function">include</span>(<span class="string">'template.html.twig'</span>) <span class="template-tag">}}</span> <span class="comment">{# Inclut un autre template #}</span></code></pre>
                </div>
            </section>

            <!-- Héritage de templates -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Héritage de Templates</h2>
                <p class="textExemple" v-pre>
                    L'une des fonctionnalités les plus puissantes de Twig est l'héritage de templates,
                    qui permet de créer une structure de base et de la surcharger dans les templates enfants.
                </p>

                <h3 class="text-purple" v-pre>Template de base (base.html.twig)</h3>
                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="html-tag">&lt;!DOCTYPE html&gt;</span>
<span class="html-tag">&lt;html&gt;</span>
    <span class="html-tag">&lt;head&gt;</span>
        <span class="html-tag">&lt;title&gt;</span><span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">title</span> <span class="template-tag">%}</span>Mon Site<span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span><span class="html-tag">&lt;/title&gt;</span>
    <span class="html-tag">&lt;/head&gt;</span>
    <span class="html-tag">&lt;body&gt;</span>
        <span class="html-tag">&lt;header&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">header</span> <span class="template-tag">%}</span>
                <span class="html-tag">&lt;h1&gt;</span>Mon Site Web<span class="html-tag">&lt;/h1&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
        <span class="html-tag">&lt;/header&gt;</span>
        
        <span class="html-tag">&lt;main&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">content</span> <span class="template-tag">%}{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
        <span class="html-tag">&lt;/main&gt;</span>
        
        <span class="html-tag">&lt;footer&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">footer</span> <span class="template-tag">%}</span>
                <span class="html-tag">&lt;p&gt;</span>© <span class="template-tag">{{</span> <span class="string">"now"</span><span class="operator">|</span><span class="function">date</span>(<span class="string">"Y"</span>) <span class="template-tag">}}</span> Mon Site<span class="html-tag">&lt;/p&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
        <span class="html-tag">&lt;/footer&gt;</span>
    <span class="html-tag">&lt;/body&gt;</span>
<span class="html-tag">&lt;/html&gt;</span></code></pre>
                </div>

                <h3 class="text-purple" v-pre>Template enfant (page.html.twig)</h3>
                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{%</span> <span class="keyword">extends</span> <span class="string">"base.html.twig"</span> <span class="template-tag">%}</span>

<span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">title</span> <span class="template-tag">%}</span>Ma Page - <span class="template-tag">{{</span> <span class="function">parent</span>() <span class="template-tag">}}</span><span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>

<span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">header</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;h1&gt;</span>Ma Page Spéciale<span class="html-tag">&lt;/h1&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>

<span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">content</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p&gt;</span>Contenu spécifique à cette page.<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span></code></pre>
                </div>
            </section>

            <!-- Intégration avec Symfony -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Intégration avec Symfony</h2>
                <p class="textExemple" v-pre>
                    Symfony et Twig sont étroitement intégrés. Voici comment utiliser Twig dans un contrôleur Symfony :
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-php"><span class="php-tag">&lt;?php</span>
<span class="comment">// src/Controller/ProductController.php</span>

<span class="keyword">namespace</span> <span class="namespace">App\Controller</span>;

<span class="keyword">use</span> <span class="namespace">Symfony\Bundle\FrameworkBundle\Controller\AbstractController</span>;
<span class="keyword">use</span> <span class="namespace">Symfony\Component\HttpFoundation\Response</span>;
<span class="keyword">use</span> <span class="namespace">Symfony\Component\Routing\Annotation\Route</span>;

<span class="keyword">class</span> <span class="class-name">ProductController</span> <span class="keyword">extends</span> <span class="class-name">AbstractController</span>
{
    <span class="attribute">#[Route(<span class="string">'/products'</span>, <span class="property">name</span>: <span class="string">'product_list'</span>)]</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">list</span>(): <span class="class-name">Response</span>
    {
        <span class="variable">$products</span> = [
            [<span class="string">'name'</span> =&gt; <span class="string">'Laptop'</span>, <span class="string">'price'</span> =&gt; <span class="number">999.99</span>],
            [<span class="string">'name'</span> =&gt; <span class="string">'Mouse'</span>, <span class="string">'price'</span> =&gt; <span class="number">29.99</span>],
            [<span class="string">'name'</span> =&gt; <span class="string">'Keyboard'</span>, <span class="string">'price'</span> =&gt; <span class="number">79.99</span>],
        ];
        
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;<span class="function">render</span>(<span class="string">'product/list.html.twig'</span>, [
            <span class="string">'products'</span> =&gt; <span class="variable">$products</span>,
            <span class="string">'page_title'</span> =&gt; <span class="string">'Nos Produits'</span>
        ]);
    }
}</code></pre>
                </div>

                <p class="textExemple" v-pre>
                    Et le template correspondant (templates/product/list.html.twig) :
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{%</span> <span class="keyword">extends</span> <span class="string">"base.html.twig"</span> <span class="template-tag">%}</span>

<span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">title</span> <span class="template-tag">%}</span><span class="template-tag">{{</span> <span class="variable">page_title</span> <span class="template-tag">}}</span><span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>

<span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">content</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;h2&gt;</span><span class="template-tag">{{</span> <span class="variable">page_title</span> <span class="template-tag">}}</span><span class="html-tag">&lt;/h2&gt;</span>
    
    <span class="html-tag">&lt;ul&gt;</span>
        <span class="template-tag">{%</span> <span class="keyword">for</span> <span class="variable">product</span> <span class="keyword">in</span> <span class="variable">products</span> <span class="template-tag">%}</span>
            <span class="html-tag">&lt;li&gt;</span>
                <span class="template-tag">{{</span> <span class="variable">product</span><span class="operator">.</span><span class="property">name</span> <span class="template-tag">}}</span> - <span class="template-tag">{{</span> <span class="variable">product</span><span class="operator">.</span><span class="property">price</span><span class="operator">|</span><span class="function">number_format</span>(<span class="number">2</span>, <span class="string">','</span>, <span class="string">' '</span>) <span class="template-tag">}}</span>€
            <span class="html-tag">&lt;/li&gt;</span>
        <span class="template-tag">{%</span> <span class="keyword">endfor</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;/ul&gt;</span>
    
    <span class="html-tag">&lt;p&gt;</span>Total: <span class="template-tag">{{</span> <span class="variable">products</span><span class="operator">|</span><span class="function">length</span> <span class="template-tag">}}</span> produit(s)<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span></code></pre>
                </div>
            </section>

            <!-- Formulaires avec Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Formulaires avec Twig</h2>
                <p class="textExemple" v-pre>
                    Twig facilite grandement l'affichage des formulaires Symfony grâce à ses fonctions dédiées :
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{{</span> <span class="function">form_start</span>(<span class="variable">productForm</span>) <span class="template-tag">}}</span>
    <span class="template-tag">{{</span> <span class="function">form_errors</span>(<span class="variable">productForm</span>) <span class="template-tag">}}</span>
    
    <span class="html-tag">&lt;div</span> <span class="html-attr">class</span>=<span class="html-string">"form-group"</span><span class="html-tag">&gt;</span>
        <span class="template-tag">{{</span> <span class="function">form_label</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">name</span>) <span class="template-tag">}}</span>
        <span class="template-tag">{{</span> <span class="function">form_widget</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">name</span>, {<span class="string">'attr'</span>: {<span class="string">'class'</span>: <span class="string">'form-control'</span>}}) <span class="template-tag">}}</span>
        <span class="template-tag">{{</span> <span class="function">form_help</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">name</span>) <span class="template-tag">}}</span>
        <span class="template-tag">{{</span> <span class="function">form_errors</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">name</span>) <span class="template-tag">}}</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="html-tag">&lt;div</span> <span class="html-attr">class</span>=<span class="html-string">"form-group"</span><span class="html-tag">&gt;</span>
        <span class="template-tag">{{</span> <span class="function">form_label</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">price</span>) <span class="template-tag">}}</span>
        <span class="template-tag">{{</span> <span class="function">form_widget</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">price</span>, {<span class="string">'attr'</span>: {<span class="string">'class'</span>: <span class="string">'form-control'</span>}}) <span class="template-tag">}}</span>
        <span class="template-tag">{{</span> <span class="function">form_errors</span>(<span class="variable">productForm</span><span class="operator">.</span><span class="property">price</span>) <span class="template-tag">}}</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="html-tag">&lt;button</span> <span class="html-attr">type</span>=<span class="html-string">"submit"</span> <span class="html-attr">class</span>=<span class="html-string">"btn btn-primary"</span><span class="html-tag">&gt;</span>Ajouter<span class="html-tag">&lt;/button&gt;</span>
<span class="template-tag">{{</span> <span class="function">form_end</span>(<span class="variable">productForm</span>) <span class="template-tag">}}</span></code></pre>
                </div>

                <p class="textExemple" v-pre>
                    Ou plus simplement avec le rendu automatique :
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-twig"><span class="template-tag">{{</span> <span class="function">form</span>(<span class="variable">productForm</span>) <span class="template-tag">}}</span></code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple" v-pre>Exercice 1: Création d'un template de base</h3>
                    <p class="textExemple" v-pre>
                        Créez un template de base pour votre application Symfony avec les blocs suivants :
                        <code>title</code>, <code>stylesheets</code>, <code>header</code>, <code>content</code>,
                        <code>footer</code>.
                    </p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content" v-pre>
                            <pre><code class="language-twig"><span class="html-tag">&lt;!DOCTYPE html&gt;</span>
<span class="html-tag">&lt;html&gt;</span>
    <span class="html-tag">&lt;head&gt;</span>
        <span class="html-tag">&lt;meta</span> <span class="html-attr">charset</span>=<span class="html-string">"UTF-8"</span><span class="html-tag">&gt;</span>
        <span class="html-tag">&lt;title&gt;</span><span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">title</span> <span class="template-tag">%}</span>Mon Application<span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span><span class="html-tag">&lt;/title&gt;</span>
        <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">stylesheets</span> <span class="template-tag">%}{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;/head&gt;</span>
    <span class="html-tag">&lt;body&gt;</span>
        <span class="html-tag">&lt;header&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">header</span> <span class="template-tag">%}</span>
                <span class="html-tag">&lt;nav&gt;</span>
                    <span class="html-tag">&lt;ul&gt;</span>
                        <span class="html-tag">&lt;li&gt;</span><span class="html-tag">&lt;a</span> <span class="html-attr">href</span>=<span class="html-string">"</span><span class="template-tag">{{</span> <span class="function">path</span>(<span class="string">'home'</span>) <span class="template-tag">}}</span><span class="html-string">"</span><span class="html-tag">&gt;</span>Accueil<span class="html-tag">&lt;/a&gt;</span><span class="html-tag">&lt;/li&gt;</span>
                        <span class="html-tag">&lt;li&gt;</span><span class="html-tag">&lt;a</span> <span class="html-attr">href</span>=<span class="html-string">"</span><span class="template-tag">{{</span> <span class="function">path</span>(<span class="string">'about'</span>) <span class="template-tag">}}</span><span class="html-string">"</span><span class="html-tag">&gt;</span>À propos<span class="html-tag">&lt;/a&gt;</span><span class="html-tag">&lt;/li&gt;</span>
                    <span class="html-tag">&lt;/ul&gt;</span>
                <span class="html-tag">&lt;/nav&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
        <span class="html-tag">&lt;/header&gt;</span>
        
        <span class="html-tag">&lt;main&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">content</span> <span class="template-tag">%}{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
        <span class="html-tag">&lt;/main&gt;</span>
        
        <span class="html-tag">&lt;footer&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">footer</span> <span class="template-tag">%}</span>
                <span class="html-tag">&lt;p&gt;</span>© <span class="template-tag">{{</span> <span class="string">"now"</span><span class="operator">|</span><span class="function">date</span>(<span class="string">"Y"</span>) <span class="template-tag">}}</span> Mon Application<span class="html-tag">&lt;/p&gt;</span>
            <span class="template-tag">{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
        <span class="html-tag">&lt;/footer&gt;</span>
        
        <span class="template-tag">{%</span> <span class="keyword">block</span> <span class="variable">javascripts</span> <span class="template-tag">%}{%</span> <span class="keyword">endblock</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;/body&gt;</span>
<span class="html-tag">&lt;/html&gt;</span></code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple" v-pre>Exercice 2: Affichage conditionnel</h3>
                    <p class="textExemple" v-pre>
                        Créez un template qui affiche un message différent selon le rôle de l'utilisateur :
                        "Administrateur" pour ROLE_ADMIN, "Modérateur" pour ROLE_MODERATOR, et "Utilisateur" pour les
                        autres rôles.
                    </p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content" v-pre>
                            <pre><code class="language-twig"><span class="template-tag">{%</span> <span class="keyword">if</span> <span class="function">is_granted</span>(<span class="string">'ROLE_ADMIN'</span>) <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p</span> <span class="html-attr">class</span>=<span class="html-string">"admin-role"</span><span class="html-tag">&gt;</span>Administrateur<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">elseif</span> <span class="function">is_granted</span>(<span class="string">'ROLE_MODERATOR'</span>) <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p</span> <span class="html-attr">class</span>=<span class="html-string">"moderator-role"</span><span class="html-tag">&gt;</span>Modérateur<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">else</span> <span class="template-tag">%}</span>
    <span class="html-tag">&lt;p</span> <span class="html-attr">class</span>=<span class="html-string">"user-role"</span><span class="html-tag">&gt;</span>Utilisateur<span class="html-tag">&lt;/p&gt;</span>
<span class="template-tag">{%</span> <span class="keyword">endif</span> <span class="template-tag">%}</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Ressources supplémentaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple" v-pre>Ressources Supplémentaires</h2>
                <p class="textExemple" v-pre>
                    Pour approfondir vos connaissances sur Twig avec Symfony :
                </p>

                <ul class="textExemple">
                    <li><a href="https://twig.symfony.com/doc/3.x/" class="btn-purple btn-hover"
                            target="_blank">Documentation officielle de Twig</a></li>
                    <li><a href="https://symfony.com/doc/current/templates.html" class="btn-purple btn-hover"
                            target="_blank">Documentation Symfony sur les templates</a></li>
                    <li><a href="https://symfonycasts.com/screencast/twig" class="btn-purple btn-hover"
                            target="_blank">Tutoriel vidéo SymfonyCasts</a></li>
                </ul>
            </section>
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

/* COULEURS VS CODE COMPLÈTES */
.comment {
    color: #6A9955 !important;
    font-style: italic !important;
}

.keyword {
    color: #C586C0 !important;
}

.string {
    color: #CE9178 !important;
}

.function {
    color: #DCDCAA !important;
}

.variable {
    color: #9CDCFE !important;
}

.property {
    color: #9CDCFE !important;
}

.number {
    color: #B5CEA8 !important;
}

.operator {
    color: #D4D4D4 !important;
}

.constant {
    color: #4FC1FF !important;
}

.class-name {
    color: #4EC9B0 !important;
}

.namespace {
    color: #4EC9B0 !important;
}

.html-tag {
    color: #569CD6 !important;
}

.html-attr {
    color: #9CDCFE !important;
}

.html-string {
    color: #CE9178 !important;
}

.template-tag {
    color: #569CD6 !important;
}

.php-tag {
    color: #569CD6 !important;
}

.attribute {
    color: #D7BA7D !important;
}

.text {
    color: #D4D4D4 !important;
}

/* Styles spécifiques pour chaque langage */
.language-twig .template-tag {
    color: #569CD6 !important;
}

.language-twig .keyword {
    color: #C586C0 !important;
}

.language-twig .function {
    color: #DCDCAA !important;
}

.language-twig .variable {
    color: #9CDCFE !important;
}

.language-twig .string {
    color: #CE9178 !important;
}

.language-twig .comment {
    color: #6A9955 !important;
}

.language-php .php-tag {
    color: #569CD6 !important;
}

.language-php .keyword {
    color: #C586C0 !important;
}

.language-php .function {
    color: #DCDCAA !important;
}

.language-php .variable {
    color: #9CDCFE !important;
}

.language-php .string {
    color: #CE9178 !important;
}

.language-php .comment {
    color: #6A9955 !important;
}

.language-yaml .property {
    color: #9CDCFE !important;
}

.language-yaml .string {
    color: #CE9178 !important;
}

.language-yaml .number {
    color: #B5CEA8 !important;
}

.language-bash .function {
    color: #DCDCAA !important;
}

.language-bash .variable {
    color: #9CDCFE !important;
}

.language-bash .comment {
    color: #6A9955 !important;
}

.language-html .html-tag {
    color: #569CD6 !important;
}

.language-html .html-attr {
    color: #9CDCFE !important;
}

.language-html .html-string {
    color: #CE9178 !important;
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