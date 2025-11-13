<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Bootstrap</h1>
                <p class="lesson-meta text-white">Framework CSS populaire pour le développement front-end rapide</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Bootstrap ?</h2>
                <p class="textExemple">
                    Bootstrap est un framework CSS open-source développé par Twitter qui permet de créer des sites web
                    responsives
                    et mobiles-first rapidement. Il fournit une collection d'outils et de composants prédéfinis pour
                    faciliter
                    le développement front-end.
                </p>
                <div class="code-example">
                    <h3 class="text-purple">Exemple simple</h3>
                    <pre><code><span class="comment">&lt;!-- Avec Bootstrap --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="keyword">&gt;</span>
  Bouton stylisé
<span class="keyword">&lt;/button&gt;</span>

<span class="comment">&lt;!-- CSS traditionnel --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"custom-button"</span><span class="keyword">&gt;</span>Bouton stylisé<span class="keyword">&lt;/button&gt;</span>

<span class="keyword">&lt;style&gt;</span>
<span class="variable">.custom-button</span> {
  <span class="variable">background-color</span>: <span class="constant">#007bff</span>;
  <span class="variable">color</span>: <span class="variable">white</span>;
  <span class="variable">border</span>: <span class="number">1px</span> <span class="variable">solid</span> <span class="constant">#007bff</span>;
  <span class="variable">padding</span>: <span class="number">0.375</span><span class="variable">rem</span> <span class="number">0.75</span><span class="variable">rem</span>;
  <span class="variable">border-radius</span>: <span class="number">0.25</span><span class="variable">rem</span>;
  <span class="variable">font-size</span>: <span class="number">1</span><span class="variable">rem</span>;
}
<span class="keyword">&lt;/style&gt;</span></code></pre>
                </div>
            </section>

            <!-- Pourquoi utiliser Bootstrap -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser Bootstrap ?</h2>
                <div class="textExemple">
                    <h3 class="text-purple">Avantages principaux :</h3>
                    <ul>
                        <li><strong>Développement rapide</strong> : Composants prêts à l'emploi</li>
                        <li><strong>Design responsive</strong> : Système de grille mobile-first</li>
                        <li><strong>Consistance visuelle</strong> : Design cohérent sur tous les composants</li>
                        <li><strong>Documentation complète</strong> : Très bien documenté avec nombreux exemples</li>
                        <li><strong>Communauté active</strong> : Large communauté et nombreux templates</li>
                        <li><strong>Cross-browser</strong> : Compatible avec tous les navigateurs modernes</li>
                    </ul>
                </div>
                <div class="code-example">
                    <h3 class="text-purple">Exemple de design responsive</h3>
                    <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"row"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-12 col-md-6 col-lg-4"</span><span class="keyword">&gt;</span>
      Colonne 1
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-12 col-md-6 col-lg-4"</span><span class="keyword">&gt;</span>
      Colonne 2
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-12 col-md-12 col-lg-4"</span><span class="keyword">&gt;</span>
      Colonne 3
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation de Bootstrap</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Méthode 1 : Via CDN (recommandé pour débuter)</h3>
                    <p>Ajoutez ces lignes dans votre balise &lt;head&gt; :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">&lt;!-- CSS Bootstrap --&gt;</span>
<span class="keyword">&lt;link</span> 
  <span class="variable">href</span>=<span class="string">"https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"</span> 
  <span class="variable">rel</span>=<span class="string">"stylesheet"</span> 
  <span class="variable">integrity</span>=<span class="string">"sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN"</span> 
  <span class="variable">crossorigin</span>=<span class="string">"anonymous"</span>
<span class="keyword">&gt;</span>

<span class="comment">&lt;!-- JavaScript Bootstrap --&gt;</span>
<span class="keyword">&lt;script</span> 
  <span class="variable">src</span>=<span class="string">"https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"</span> 
  <span class="variable">integrity</span>=<span class="string">"sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL"</span> 
  <span class="variable">crossorigin</span>=<span class="string">"anonymous"</span>
<span class="keyword">&gt;&lt;/script&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Méthode 2 : Installation via npm</h3>
                    <p>Pour les projets plus complexes :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment"># Installer Bootstrap</span>
<span class="variable">npm install bootstrap@5.3.2</span>

<span class="comment"># Installer les dépendances (si nécessaire)</span>
<span class="variable">npm install @popperjs/core</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configuration pour Nuxt</h3>
                    <p>Dans Nuxt, vous pouvez utiliser Bootstrap via un module :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment"># Installer le module Bootstrap pour Nuxt</span>
<span class="variable">npm install bootstrap-vue@next</span></code></pre>
                </div>
                <div class="textExemple">
                    <p>Ajoutez ensuite le module dans votre fichier <code>nuxt.config.js</code> :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">// nuxt.config.js</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="variable">css</span>: [
    <span class="string">'bootstrap/dist/css/bootstrap.min.css'</span>
  ],
  <span class="variable">plugins</span>: [
    { <span class="variable">src</span>: <span class="string">'~/plugins/bootstrap.js'</span>, <span class="variable">mode</span>: <span class="string">'client'</span> }
  ]
}</code></pre>
                </div>

                <div class="textExemple">
                    <p>Créez le fichier plugin <code>plugins/bootstrap.js</code> :</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">// plugins/bootstrap.js</span>
<span class="keyword">import</span> <span class="variable">bootstrap</span> <span class="keyword">from</span> <span class="string">'bootstrap/dist/js/bootstrap.bundle.min.js'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="keyword">function</span>(<span class="variable">context</span>) {
  <span class="variable">context</span>.<span class="variable">app</span>.<span class="variable">config</span>.<span class="variable">globalProperties</span>.<span class="variable">$bootstrap</span> = <span class="variable">bootstrap</span>
}</code></pre>
                </div>
            </section>

            <!-- Concepts de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts de base de Bootstrap</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Système de grille</h3>
                    <p>Bootstrap utilise un système de grille responsive à 12 colonnes.</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"row"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-sm-6 col-md-4 col-lg-3"</span><span class="keyword">&gt;</span>
      Colonne 1
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-sm-6 col-md-4 col-lg-3"</span><span class="keyword">&gt;</span>
      Colonne 2
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-sm-6 col-md-4 col-lg-3"</span><span class="keyword">&gt;</span>
      Colonne 3
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-sm-6 col-md-4 col-lg-3"</span><span class="keyword">&gt;</span>
      Colonne 4
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Composants prédéfinis</h3>
                    <p>Bootstrap fournit de nombreux composants réutilisables.</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">&lt;!-- Navigation --&gt;</span>
<span class="keyword">&lt;nav</span> <span class="variable">class</span>=<span class="string">"navbar navbar-expand-lg navbar-light bg-light"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container-fluid"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"navbar-brand"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Mon Site<span class="keyword">&lt;/a&gt;</span>
    <span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"navbar-toggler"</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">data-bs-toggle</span>=<span class="string">"collapse"</span> <span class="variable">data-bs-target</span>=<span class="string">"#navbarNav"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;span</span> <span class="variable">class</span>=<span class="string">"navbar-toggler-icon"</span><span class="keyword">&gt;&lt;/span&gt;</span>
    <span class="keyword">&lt;/button&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"collapse navbar-collapse"</span> <span class="variable">id</span>=<span class="string">"navbarNav"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;ul</span> <span class="variable">class</span>=<span class="string">"navbar-nav"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link active"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Accueil<span class="keyword">&lt;/a&gt;</span>
        <span class="keyword">&lt;/li&gt;</span>
        <span class="keyword">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Services<span class="keyword">&lt;/a&gt;</span>
        <span class="keyword">&lt;/li&gt;</span>
      <span class="keyword">&lt;/ul&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/nav&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Classes utilitaires</h3>
                    <p>Bootstrap inclut de nombreuses classes utilitaires pour le style rapide.</p>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">&lt;!-- Couleurs de texte --&gt;</span>
<span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"text-primary"</span><span class="keyword">&gt;</span>Texte primaire<span class="keyword">&lt;/p&gt;</span>
<span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"text-success"</span><span class="keyword">&gt;</span>Texte succès<span class="keyword">&lt;/p&gt;</span>
<span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"text-danger"</span><span class="keyword">&gt;</span>Texte danger<span class="keyword">&lt;/p&gt;</span>

<span class="comment">&lt;!-- Backgrounds --&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"bg-primary text-white p-3"</span><span class="keyword">&gt;</span>Background primaire<span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"bg-light p-3"</span><span class="keyword">&gt;</span>Background light<span class="keyword">&lt;/div&gt;</span>

<span class="comment">&lt;!-- Espacement --&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"m-3 p-4"</span><span class="keyword">&gt;</span>Margin 3, Padding 4<span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"mt-2 mb-4 ms-1 me-3"</span><span class="keyword">&gt;</span>Margins directionnels<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>
            </section>

            <!-- Composants principaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Composants principaux de Bootstrap</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Boutons</h3>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">&lt;!-- Types de boutons --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="keyword">&gt;</span>Primaire<span class="keyword">&lt;/button&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-secondary"</span><span class="keyword">&gt;</span>Secondaire<span class="keyword">&lt;/button&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-success"</span><span class="keyword">&gt;</span>Succès<span class="keyword">&lt;/button&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-danger"</span><span class="keyword">&gt;</span>Danger<span class="keyword">&lt;/button&gt;</span>

<span class="comment">&lt;!-- Tailles --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-primary btn-sm"</span><span class="keyword">&gt;</span>Petit<span class="keyword">&lt;/button&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-primary btn-lg"</span><span class="keyword">&gt;</span>Large<span class="keyword">&lt;/button&gt;</span>

<span class="comment">&lt;!-- Boutons outline --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-outline-primary"</span><span class="keyword">&gt;</span>Outline<span class="keyword">&lt;/button&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Cartes (Cards)</h3>
                </div>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card"</span> <span class="variable">style</span>=<span class="string">"width: 18rem;"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;img</span> <span class="variable">src</span>=<span class="string">"..."</span> <span class="variable">class</span>=<span class="string">"card-img-top"</span> <span class="variable">alt</span>=<span class="string">"..."</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card-body"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;h5</span> <span class="variable">class</span>=<span class="string">"card-title"</span><span class="keyword">&gt;</span>Titre de la carte<span class="keyword">&lt;/h5&gt;</span>
    <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"card-text"</span><span class="keyword">&gt;</span>
      Exemple de texte dans la carte.
    <span class="keyword">&lt;/p&gt;</span>
    <span class="keyword">&lt;a</span> <span class="variable">href</span>=<span class="string">"#"</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="keyword">&gt;</span>Aller quelque part<span class="keyword">&lt;/a&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Modals</h3>
                </div>
                <div class="code-example">
                    <pre><code><span class="comment">&lt;!-- Bouton pour ouvrir le modal --&gt;</span>
<span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span> <span class="variable">data-bs-toggle</span>=<span class="string">"modal"</span> <span class="variable">data-bs-target</span>=<span class="string">"#exampleModal"</span><span class="keyword">&gt;</span>
  Ouvrir le modal
<span class="keyword">&lt;/button&gt;</span>

<span class="comment">&lt;!-- Modal --&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"modal fade"</span> <span class="variable">id</span>=<span class="string">"exampleModal"</span> <span class="variable">tabindex</span>=<span class="string">"-1"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"modal-dialog"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"modal-content"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"modal-header"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;h5</span> <span class="variable">class</span>=<span class="string">"modal-title"</span><span class="keyword">&gt;</span>Titre du modal<span class="keyword">&lt;/h5&gt;</span>
        <span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn-close"</span> <span class="variable">data-bs-dismiss</span>=<span class="string">"modal"</span><span class="keyword">&gt;&lt;/button&gt;</span>
      <span class="keyword">&lt;/div&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"modal-body"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;p</span><span class="keyword">&gt;</span>Contenu du modal...<span class="keyword">&lt;/p&gt;</span>
      <span class="keyword">&lt;/div&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"modal-footer"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-secondary"</span> <span class="variable">data-bs-dismiss</span>=<span class="string">"modal"</span><span class="keyword">&gt;</span>Fermer<span class="keyword">&lt;/button&gt;</span>
        <span class="keyword">&lt;button</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="keyword">&gt;</span>Sauvegarder<span class="keyword">&lt;/button&gt;</span>
      <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span></code></pre>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Objectif</h3>
                    <p>
                        Créez une page de profil utilisateur responsive avec Bootstrap contenant :
                    </p>
                    <ul>
                        <li>Une navbar responsive</li>
                        <li>Une section de profil avec avatar</li>
                        <li>Une grille de cartes pour les compétences</li>
                        <li>Un formulaire de contact</li>
                        <li>Un footer</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution avec Bootstrap</h4>
                            <pre><code><span class="comment">&lt;!-- Navbar --&gt;</span>
<span class="keyword">&lt;nav</span> <span class="variable">class</span>=<span class="string">"navbar navbar-expand-lg navbar-dark bg-dark"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"navbar-brand"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Mon Portfolio<span class="keyword">&lt;/a&gt;</span>
    <span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"navbar-toggler"</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">data-bs-toggle</span>=<span class="string">"collapse"</span> <span class="variable">data-bs-target</span>=<span class="string">"#navbarNav"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;span</span> <span class="variable">class</span>=<span class="string">"navbar-toggler-icon"</span><span class="keyword">&gt;&lt;/span&gt;</span>
    <span class="keyword">&lt;/button&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"collapse navbar-collapse"</span> <span class="variable">id</span>=<span class="string">"navbarNav"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;ul</span> <span class="variable">class</span>=<span class="string">"navbar-nav ms-auto"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link active"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Profil<span class="keyword">&lt;/a&gt;</span>
        <span class="keyword">&lt;/li&gt;</span>
        <span class="keyword">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Compétences<span class="keyword">&lt;/a&gt;</span>
        <span class="keyword">&lt;/li&gt;</span>
        <span class="keyword">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="keyword">&gt;</span>Contact<span class="keyword">&lt;/a&gt;</span>
        <span class="keyword">&lt;/li&gt;</span>
      <span class="keyword">&lt;/ul&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/nav&gt;</span>

<span class="comment">&lt;!-- Section Profil --&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container my-5"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"row align-items-center"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4 text-center"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;img</span> <span class="variable">src</span>=<span class="string">"avatar.jpg"</span> <span class="variable">class</span>=<span class="string">"rounded-circle img-fluid"</span> <span class="variable">width</span>=<span class="string">"200"</span> <span class="variable">alt</span>=<span class="string">"Avatar"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-8"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;h1</span> <span class="variable">class</span>=<span class="string">"display-4"</span><span class="keyword">&gt;</span>John Doe<span class="keyword">&lt;/h1&gt;</span>
      <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"lead text-muted"</span><span class="keyword">&gt;</span>Développeur Full Stack<span class="keyword">&lt;/p&gt;</span>
      <span class="keyword">&lt;p</span><span class="keyword">&gt;</span>Passionné par le développement web et les nouvelles technologies.<span class="keyword">&lt;/p&gt;</span>
      <span class="keyword">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-primary btn-lg"</span><span class="keyword">&gt;</span>Me contacter<span class="keyword">&lt;/button&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
  <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/div&gt;</span>

<span class="comment">&lt;!-- Section Compétences --&gt;</span>
<span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container my-5"</span><span class="keyword">&gt;</span>
  <span class="keyword">&lt;h2</span> <span class="variable">class</span>=<span class="string">"text-center mb-4"</span><span class="keyword">&gt;</span>Mes Compétences<span class="keyword">&lt;/h2&gt;</span>
  <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"row"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4 mb-3"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card h-100"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card-body text-center"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;h5</span> <span class="variable">class</span>=<span class="string">"card-title"</span><span class="keyword">&gt;</span>Frontend<span class="keyword">&lt;/h5&gt;</span>
          <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"card-text"</span><span class="keyword">&gt;</span>HTML, CSS, JavaScript, React, Vue.js<span class="keyword">&lt;/p&gt;</span>
        <span class="keyword">&lt;/div&gt;</span>
      <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4 mb-3"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card h-100"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card-body text-center"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;h5</span> <span class="variable">class</span>=<span class="string">"card-title"</span><span class="keyword">&gt;</span>Backend<span class="keyword">&lt;/h5&gt;</span>
          <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"card-text"</span><span class="keyword">&gt;</span>Node.js, Express, MongoDB, MySQL<span class="keyword">&lt;/p&gt;</span>
        <span class="keyword">&lt;/div&gt;</span>
      <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4 mb-3"</span><span class="keyword">&gt;</span>
      <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card h-100"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"card-body text-center"</span><span class="keyword">&gt;</span>
          <span class="keyword">&lt;h5</span> <span class="variable">class</span>=<span class="string">"card-title"</span><span class="keyword">&gt;</span>Outils<span class="keyword">&lt;/h5&gt;</span>
          <span class="keyword">&lt;p</span> <span class="variable">class</span>=<span class="string">"card-text"</span><span class="keyword">&gt;</span>Git, Docker, Webpack, Figma<span class="keyword">&lt;/p&gt;</span>
        <span class="keyword">&lt;/div&gt;</span>
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
                        Bootstrap reste l'un des frameworks CSS les plus populaires et les plus utilisés dans le monde
                        du développement web.
                        Sa simplicité d'utilisation, sa documentation complète et sa large communauté en font un
                        excellent choix pour
                        démarrer rapidement un projet ou pour des applications nécessitant une interface utilisateur
                        cohérente et professionnelle.
                    </p>
                    <p>
                        Bien que des frameworks comme Tailwind CSS gagnent en popularité pour leur flexibilité,
                        Bootstrap continue d'évoluer
                        et reste une solution solide pour de nombreux projets.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ressources supplémentaires</h3>
                    <ul>
                        <li><a href="https://getbootstrap.com/docs/5.3/getting-started/introduction/"
                                class="btn-purple btn-hover" target="_blank">Documentation officielle</a></li>
                        <li><a href="https://getbootstrap.com/docs/5.3/examples/" class="btn-purple btn-hover"
                                target="_blank">Exemples et templates</a></li>
                        <li><a href="https://github.com/twbs/bootstrap" class="btn-purple btn-hover"
                                target="_blank">Code source sur GitHub</a></li>
                        <li><a href="https://bootswatch.com/" class="btn-purple btn-hover" target="_blank">Bootswatch -
                                Thèmes gratuits</a></li>
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