<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Tailwind CSS</h1>
                <p class="lesson-meta text-white">Framework CSS utilitaire pour un développement rapide et personnalisé
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Tailwind CSS ?</h2>
                <p class="textExemple">
                    Tailwind CSS est un framework CSS utilitaire qui permet de créer des interfaces utilisateur modernes
                    et responsives directement dans votre HTML.
                    Contrairement aux frameworks traditionnels comme Bootstrap, Tailwind ne fournit pas de composants
                    prédéfinis mais plutôt des classes utilitaires
                    qui peuvent être combinées pour construire n'importe quel design.
                </p>
                <div class="code-example">
                    <h3 class="text-purple">Exemple simple</h3>
                    <pre><code><span class="comment">&lt;!-- Avec Tailwind CSS --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"</span><span class="keyword">&gt;</span>
  Bouton stylisé
<span class="keyword">&lt;/button&gt;</span>

<span class="comment">&lt;!-- CSS traditionnel --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"custom-button"</span><span class="keyword">&gt;</span>Bouton stylisé<span class="keyword">&lt;/button&gt;</span>

<span class="keyword">&lt;style&gt;</span>
<span class="variable">.custom-button</span> {
  <span class="variable">background-color</span>: <span class="constant">#3b82f6</span>;
  <span class="variable">color</span>: <span class="variable">white</span>;
  <span class="variable">font-weight</span>: <span class="variable">bold</span>;
  <span class="variable">padding</span>: <span class="number">0.5</span><span class="variable">rem</span> <span class="number">1</span><span class="variable">rem</span>;
  <span class="variable">border-radius</span>: <span class="number">0.25</span><span class="variable">rem</span>;
}
<span class="variable">.custom-button</span><span class="keyword">:hover</span> {
  <span class="variable">background-color</span>: <span class="constant">#1d4ed8</span>;
}
<span class="keyword">&lt;/style&gt;</span></code></pre>
                </div>
            </section>

            <!-- Pourquoi utiliser Tailwind CSS -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser Tailwind CSS ?</h2>
                <div class="textExemple">
                    <h3 class="text-purple">Avantages principaux :</h3>
                    <ul>
                        <li><strong>Développement rapide</strong> : Écrire moins de CSS personnalisé</li>
                        <li><strong>Design cohérent</strong> : Système de design uniforme grâce aux contraintes</li>
                        <li><strong>Personnalisation facile</strong> : Configuration simple via le fichier
                            tailwind.config.js</li>
                        <li><strong>Performance</strong> : Purge CSS automatique pour supprimer les classes inutilisées
                        </li>
                        <li><strong>Responsive design</strong> : Classes intégrées pour tous les points de rupture</li>
                        <li><strong>Maintenance simplifiée</strong> : Pas de CSS personnalisé à maintenir</li>
                    </ul>
                </div>
                <div class="code-example">
                    <h3 class="text-purple">Exemple de design responsive</h3>
                    <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"flex flex-col md:flex-row"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"w-full md:w-1/2 p-4 bg-gray-100"</span><span class="keyword">&gt;</span>
    Colonne 1
  <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"w-full md:w-1/2 p-4 bg-gray-200"</span><span class="keyword">&gt;</span>
    Colonne 2
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation de Tailwind CSS</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Méthode 1 : Via CDN (pour tests rapides)</h3>
                    <p>Ajoutez simplement cette ligne dans votre balise &lt;head&gt; :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;script</span> <span class="variable">src</span>=<span class="string">"https://cdn.tailwindcss.com"</span><span class="keyword">&gt;&lt;/script&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Méthode 2 : Installation via npm (recommandée)</h3>
                    <p>Pour les projets sérieux, l'installation via npm est préférable :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment"># Installer Tailwind CSS</span>
<span class="variable">npm install -D tailwindcss</span>

<span class="comment"># Créer le fichier de configuration</span>
<span class="variable">npx tailwindcss init</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configuration pour Nuxt</h3>
                    <p>Dans Nuxt, vous pouvez installer Tailwind CSS comme module :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment"># Installer le module Tailwind pour Nuxt</span>
<span class="variable">npm install --save-dev @nuxtjs/tailwindcss</span></code></pre>
                </div>
                <div class="textExemple">
                    <p>Ajoutez ensuite le module dans votre fichier <code>nuxt.config.js</code> :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">// nuxt.config.js</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="variable">buildModules</span>: [
    <span class="string">'@nuxtjs/tailwindcss'</span>
  ]
}</code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configuration du fichier tailwind.config.js</h3>
                    <p>Créez ou modifiez votre fichier de configuration :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">// tailwind.config.js</span>
<span class="keyword">module</span>.<span class="variable">exports</span> = {
  <span class="variable">content</span>: [
    <span class="string">'./components/**/*.{vue,js}'</span>,
    <span class="string">'./layouts/**/*.vue'</span>,
    <span class="string">'./pages/**/*.vue'</span>,
    <span class="string">'./plugins/**/*.{js,ts}'</span>,
    <span class="string">'./nuxt.config.{js,ts}'</span>,
  ],
  <span class="variable">theme</span>: {
    <span class="variable">extend</span>: {
      <span class="variable">colors</span>: {
        <span class="string">'primary'</span>: <span class="string">'#8B5FBF'</span>,
        <span class="string">'secondary'</span>: <span class="string">'#6A3093'</span>,
      }
    },
  },
  <span class="variable">plugins</span>: [],
}</code></pre>
                </div>
            </section>

            <!-- Concepts de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts de base de Tailwind CSS</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Classes utilitaires</h3>
                    <p>Tailwind fonctionne avec des classes utilitaires qui correspondent à une propriété CSS
                        spécifique.</p>
                </div>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">CSS traditionnel</h4>
                        <pre><code><span class="comment">/* CSS */</span>
<span class="variable">.card</span> {
  <span class="variable">padding</span>: <span class="number">1rem</span>;
  <span class="variable">background-color</span>: <span class="variable">white</span>;
  <span class="variable">border-radius</span>: <span class="number">0.5rem</span>;
  <span class="variable">box-shadow</span>: <span class="number">0 4px 6px rgba(0, 0, 0, 0.1)</span>;
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Tailwind CSS</h4>
                        <pre><code><span class="comment">&lt;!-- HTML avec classes Tailwind --&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"p-4 bg-white rounded-lg shadow-md"</span><span class="keyword">&gt;</span>
  Contenu de la carte
<span class="keyword">&lt;/div&gt;</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Design responsive</h3>
                    <p>Tailwind utilise des préfixes pour les breakpoints :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"text-sm md:text-base lg:text-lg"</span><span class="keyword">&gt;</span>
  Ce texte change de taille selon l'écran
<span class="keyword">&lt;/div&gt;</span>

<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"w-full md:w-1/2 lg:w-1/3"</span><span class="keyword">&gt;</span>
  Cette div occupe 100% sur mobile, 50% sur tablette, 33% sur desktop
<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. États et interactions</h3>
                    <p>Gérez facilement les états comme hover, focus, etc.</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"bg-blue-500 hover:bg-blue-700 focus:bg-blue-900 text-white font-bold py-2 px-4 rounded"</span><span class="keyword">&gt;</span>
  Bouton interactif
<span class="keyword">&lt;/button&gt;</span></code></pre>
                </div>
            </section>

            <!-- Comparaison avec CSS traditionnel -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comparaison avec CSS traditionnel</h2>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">CSS traditionnel</h4>
                        <pre><code><span class="comment">/* HTML */</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;h2</span> <span class="variable">class</span>=<span class="string">"card-title"</span><span class="keyword">&gt;</span>Titre<span class="keyword">&lt;/h2&gt;</span>
  <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"card-content"</span><span class="keyword">&gt;</span>Contenu<span class="keyword">&lt;/p&gt;</span>
<span class="keyword">&lt;/div&gt;</span>

<span class="comment">/* CSS */</span>
<span class="variable">.card</span> {
  <span class="variable">background</span>: <span class="variable">white</span>;
  <span class="variable">border-radius</span>: <span class="number">8px</span>;
  <span class="variable">padding</span>: <span class="number">16px</span>;
  <span class="variable">box-shadow</span>: <span class="number">0 2px 4px rgba(0,0,0,0.1)</span>;
  <span class="variable">margin-bottom</span>: <span class="number">16px</span>;
}

<span class="variable">.card-title</span> {
  <span class="variable">font-size</span>: <span class="number">1.25</span><span class="variable">rem</span>;
  <span class="variable">font-weight</span>: <span class="variable">bold</span>;
  <span class="variable">margin-bottom</span>: <span class="number">8px</span>;
}

<span class="variable">.card-content</span> {
  <span class="variable">color</span>: <span class="constant">#666</span>;
  <span class="variable">line-height</span>: <span class="number">1.5</span>;
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Tailwind CSS</h4>
                        <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"bg-white rounded-lg p-4 shadow-sm mb-4"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;h2</span> <span class="variable">class</span>=<span class="string">"text-xl font-bold mb-2"</span><span class="keyword">&gt;</span>Titre<span class="keyword">&lt;/h2&gt;</span>
  <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"text-gray-600 leading-relaxed"</span><span class="keyword">&gt;</span>Contenu<span class="keyword">&lt;/p&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <p>
                        Avec Tailwind, vous n'avez pas besoin de créer des classes CSS personnalisées pour chaque
                        élément.
                        Vous utilisez directement les classes utilitaires dans votre HTML, ce qui accélère le
                        développement
                        et garantit une cohérence visuelle.
                    </p>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Objectif</h3>
                    <p>
                        Créez une carte de produit responsive avec les caractéristiques suivantes :
                    </p>
                    <ul>
                        <li>Image en haut</li>
                        <li>Titre du produit</li>
                        <li>Description</li>
                        <li>Prix</li>
                        <li>Bouton "Ajouter au panier"</li>
                        <li>Design qui s'adapte aux mobiles et desktop</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution avec Tailwind CSS</h4>
                            <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"max-w-sm mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"md:flex"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"md:shrink-0"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;img</span> <span class="variable">class</span>=<span class="string">"h-48 w-full object-cover md:h-full md:w-48"</span> <span class="variable">src</span>=<span class="string">"/img/product.jpg"</span> <span class="variable">alt</span>=<span class="string">"Produit"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"p-8"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"uppercase tracking-wide text-sm text-indigo-500 font-semibold"</span><span class="keyword">&gt;</span>Catégorie<span class="keyword">&lt;/div&gt;</span>
      <span class="keyword">&lt;h3</span> <span class="variable">class</span>=<span class="string">"block mt-1 text-lg leading-tight font-medium text-black"</span><span class="keyword">&gt;</span>Nom du produit<span class="keyword">&lt;/h3&gt;</span>
      <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"mt-2 text-gray-500"</span><span class="keyword">&gt;</span>Description du produit avec quelques détails intéressants.<span class="keyword">&lt;/p&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"mt-4 flex items-center justify-between"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;span</span> <span class="variable">class</span>=<span class="string">"text-2xl font-bold text-gray-900"</span><span class="keyword">&gt;</span>29,99€<span class="keyword">&lt;/span&gt;</span>
        <span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"bg-indigo-500 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded"</span><span class="keyword">&gt;</span>
          Ajouter au panier
        <span class="keyword">&lt;/button&gt;</span>
      <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Tailwind CSS est un outil puissant qui change la façon dont nous concevons les interfaces web.
                        En utilisant des classes utilitaires, nous pouvons développer plus rapidement, maintenir une
                        cohérence
                        visuelle et créer des designs entièrement personnalisés sans écrire beaucoup de CSS.
                    </p>
                    <p>
                        Pour les projets Nuxt, l'intégration est simple grâce au module officiel, et la configuration
                        permet d'adapter parfaitement Tailwind à vos besoins spécifiques.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ressources supplémentaires</h3>
                    <ul>
                        <li><a href="https://tailwindcss.com/docs" class="btn-purple btn-hover"
                                target="_blank">Documentation officielle</a></li>
                        <li><a href="https://tailwindui.com/" class="btn-purple btn-hover" target="_blank">Tailwind UI -
                                Composants premium</a></li>
                        <li><a href="https://github.com/tailwindlabs/tailwindcss" class="btn-purple btn-hover"
                                target="_blank">Code source sur GitHub</a></li>
                    </ul>
                </div>
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

/* Couleurs VS Code pour la syntaxe */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés HTML/JS (div, export, function, etc.) */
.variable {
    color: #9cdcfe !important;
}

/* Variables, attributs, noms de classes */
.string {
    color: #ce9178 !important;
}

/* Chaînes de caractères */
.comment {
    color: #6a9955 !important;
}

/* Commentaires */
.function {
    color: #dcdcaa !important;
}

/* Noms de fonctions */
.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs (+, -, =, =>, etc.) */
.constant {
    color: #4fc1ff !important;
}

/* Constantes, couleurs */
.number {
    color: #b5cea8 !important;
}

/* Nombres */
.class-name {
    color: #4ec9b0 !important;
}

/* Noms de classes CSS */
.selector {
    color: #d7ba7d !important;
}

/* Sélecteurs CSS */

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