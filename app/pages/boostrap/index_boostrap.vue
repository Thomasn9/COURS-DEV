<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Bootstrap - Framework CSS</h1>
                <p class="lesson-meta text-white">Apprenez à utiliser Bootstrap pour créer des interfaces web modernes
                    et responsives</p>
            </header>

            <!-- Introduction à Bootstrap -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Bootstrap ?</h2>
                <p class="textExemple">
                    Bootstrap est un framework CSS open-source développé par Twitter. Il permet de créer des sites web
                    responsives
                    et mobiles-first rapidement grâce à son système de grille et ses composants prédéfinis.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Principales fonctionnalités :</h3>
                    <ul>
                        <li><strong>Système de grille responsive</strong> - 12 colonnes qui s'adaptent à tous les écrans
                        </li>
                        <li><strong>Composants prêts à l'emploi</strong> - Boutons, formulaires, navigation, etc.</li>
                        <li><strong>Classes utilitaires</strong> - Pour le spacing, les couleurs, la typographie</li>
                        <li><strong>Compatibilité cross-browser</strong> - Fonctionne sur tous les navigateurs modernes
                        </li>
                    </ul>
                </div>
            </section>

            <!-- Installation de Bootstrap -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation de Bootstrap</h2>
                <p class="textExemple">
                    Il existe plusieurs méthodes pour installer Bootstrap selon votre type de projet.
                </p>

                <!-- Méthode 1 : CDN -->
                <div class="code-example">
                    <h3 class="text-purple">1. Via CDN (méthode la plus simple)</h3>
                    <p>Ajoutez ces liens dans le <code>&lt;head&gt;</code> de votre HTML :</p>
                    <pre><code><span class="comment">&lt;!-- CSS Bootstrap --&gt;</span>
<span class="tag">&lt;link</span> <span class="variable">href</span>=<span class="string">"https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"</span> <span class="variable">rel</span>=<span class="string">"stylesheet"</span><span class="tag">&gt;</span>

<span class="comment">&lt;!-- JavaScript Bootstrap (optionnel) --&gt;</span>
<span class="tag">&lt;script</span> <span class="variable">src</span>=<span class="string">"https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"</span><span class="tag">&gt;</span><span class="tag">&lt;/script&gt;</span></code></pre>
                </div>

                <!-- Méthode 2 : NPM -->
                <div class="code-example">
                    <h3 class="text-purple">2. Via NPM (pour les projets modernes)</h3>
                    <p>Dans votre terminal, exécutez :</p>
                    <pre><code><span class="function">npm install</span> bootstrap@5.3.2</code></pre>

                    <p>Puis importez dans votre fichier principal :</p>
                    <pre><code><span class="comment">// Dans main.js ou app.js</span>
<span class="keyword">import</span> <span class="string">'bootstrap/dist/css/bootstrap.min.css'</span>
<span class="keyword">import</span> <span class="string">'bootstrap/dist/js/bootstrap.bundle.min.js'</span></code></pre>
                </div>

                <!-- Méthode 3 : Téléchargement -->
                <div class="code-example">
                    <h3 class="text-purple">3. Téléchargement direct</h3>
                    <p>Téléchargez les fichiers depuis le site officiel et incluez-les dans votre projet :</p>
                    <pre><code><span class="tag">&lt;link</span> <span class="variable">href</span>=<span class="string">"chemin/vers/bootstrap.min.css"</span> <span class="variable">rel</span>=<span class="string">"stylesheet"</span><span class="tag">&gt;</span>
<span class="tag">&lt;script</span> <span class="variable">src</span>=<span class="string">"chemin/vers/bootstrap.bundle.min.js"</span><span class="tag">&gt;</span><span class="tag">&lt;/script&gt;</span></code></pre>
                </div>
            </section>

            <!-- Installation spécifique à Nuxt -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation dans Nuxt</h2>
                <p class="textExemple">
                    Pour intégrer Bootstrap dans un projet Nuxt, voici la méthode recommandée :
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Étape 1 : Installation</h4>
                        <pre><code><span class="function">npm install</span> bootstrap @popperjs/core</code></pre>
                    </div>

                    <div>
                        <h4 class="text-purple">Étape 2 : Configuration</h4>
                        <pre><code><span class="comment">// Dans nuxt.config.js</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="variable">css</span>: [
    <span class="string">'bootstrap/dist/css/bootstrap.min.css'</span>
  ]
}</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Étape 3 : Plugin (pour JavaScript)</h4>
                    <p>Créez un fichier <code>plugins/bootstrap.client.js</code> :</p>
                    <pre><code><span class="keyword">import</span> bootstrap <span class="keyword">from</span> <span class="string">'bootstrap/dist/js/bootstrap.bundle.min.js'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineNuxtPlugin</span>(() <span class="operator">=></span> {
  <span class="keyword">return</span> {
    <span class="function">provide</span>: {
      <span class="variable">bootstrap</span>: bootstrap
    }
  }
})</code></pre>
                </div>
            </section>

            <!-- Exemples pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples pratiques avec Bootstrap</h2>

                <div class="code-example">
                    <h3 class="text-purple">Système de grille</h3>
                    <pre><code><span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"container"</span><span class="tag">&gt;</span>
  <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"row"</span><span class="tag">&gt;</span>
    <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4"</span><span class="tag">&gt;</span>Colonne 1<span class="tag">&lt;/div&gt;</span>
    <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4"</span><span class="tag">&gt;</span>Colonne 2<span class="tag">&lt;/div&gt;</span>
    <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"col-md-4"</span><span class="tag">&gt;</span>Colonne 3<span class="tag">&lt;/div&gt;</span>
  <span class="tag">&lt;/div&gt;</span>
<span class="tag">&lt;/div&gt;</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Boutons avec différentes couleurs</h3>
                    <pre><code><span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="tag">&gt;</span>Primary<span class="tag">&lt;/button&gt;</span>
<span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-secondary"</span><span class="tag">&gt;</span>Secondary<span class="tag">&lt;/button&gt;</span>
<span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-success"</span><span class="tag">&gt;</span>Success<span class="tag">&lt;/button&gt;</span>
<span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-danger"</span><span class="tag">&gt;</span>Danger<span class="tag">&lt;/button&gt;</span>
<span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-warning"</span><span class="tag">&gt;</span>Warning<span class="tag">&lt;/button&gt;</span>
<span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"btn btn-info"</span><span class="tag">&gt;</span>Info<span class="tag">&lt;/button&gt;</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Navigation responsive</h3>
                    <pre><code><span class="tag">&lt;nav</span> <span class="variable">class</span>=<span class="string">"navbar navbar-expand-lg navbar-light bg-light"</span><span class="tag">&gt;</span>
  <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"container-fluid"</span><span class="tag">&gt;</span>
    <span class="tag">&lt;a</span> <span class="variable">class</span>=<span class="string">"navbar-brand"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="tag">&gt;</span>MonSite<span class="tag">&lt;/a&gt;</span>
    <span class="tag">&lt;button</span> <span class="variable">class</span>=<span class="string">"navbar-toggler"</span> <span class="variable">type</span>=<span class="string">"button"</span> <span class="variable">data-bs-toggle</span>=<span class="string">"collapse"</span> <span class="variable">data-bs-target</span>=<span class="string">"#navbarNav"</span><span class="tag">&gt;</span>
      <span class="tag">&lt;span</span> <span class="variable">class</span>=<span class="string">"navbar-toggler-icon"</span><span class="tag">&gt;</span><span class="tag">&lt;/span&gt;</span>
    <span class="tag">&lt;/button&gt;</span>
    <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"collapse navbar-collapse"</span> <span class="variable">id</span>=<span class="string">"navbarNav"</span><span class="tag">&gt;</span>
      <span class="tag">&lt;ul</span> <span class="variable">class</span>=<span class="string">"navbar-nav"</span><span class="tag">&gt;</span>
        <span class="tag">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="tag">&gt;</span><span class="tag">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link active"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="tag">&gt;</span>Accueil<span class="tag">&lt;/a&gt;</span><span class="tag">&lt;/li&gt;</span>
        <span class="tag">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="tag">&gt;</span><span class="tag">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="tag">&gt;</span>Services<span class="tag">&lt;/a&gt;</span><span class="tag">&lt;/li&gt;</span>
        <span class="tag">&lt;li</span> <span class="variable">class</span>=<span class="string">"nav-item"</span><span class="tag">&gt;</span><span class="tag">&lt;a</span> <span class="variable">class</span>=<span class="string">"nav-link"</span> <span class="variable">href</span>=<span class="string">"#"</span><span class="tag">&gt;</span>Contact<span class="tag">&lt;/a&gt;</span><span class="tag">&lt;/li&gt;</span>
      <span class="tag">&lt;/ul&gt;</span>
    <span class="tag">&lt;/div&gt;</span>
  <span class="tag">&lt;/div&gt;</span>
<span class="tag">&lt;/nav&gt;</span></code></pre>
                </div>
            </section>

            <!-- Avantages et inconvénients -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages et inconvénients</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Avantages</h3>
                        <ul>
                            <li>Développement rapide</li>
                            <li>Design responsive intégré</li>
                            <li>Grande communauté</li>
                            <li>Documentation complète</li>
                            <li>Compatibilité cross-browser</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Inconvénients</h3>
                        <ul>
                            <li>Taille du fichier CSS</li>
                            <li>Design générique (sans personnalisation)</li>
                            <li>Courbe d'apprentissage pour la personnalisation</li>
                            <li>Peut ralentir les performances si mal utilisé</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Créer une carte produit responsive</h3>
                    <p>Utilisez Bootstrap pour créer une carte de produit avec :</p>
                    <ul>
                        <li>Une image</li>
                        <li>Un titre</li>
                        <li>Une description</li>
                        <li>Un prix</li>
                        <li>Un bouton "Ajouter au panier"</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"card"</span> <span class="variable">style</span>=<span class="string">"width: 18rem;"</span><span class="tag">&gt;</span>
  <span class="tag">&lt;img</span> <span class="variable">src</span>=<span class="string">"produit.jpg"</span> <span class="variable">class</span>=<span class="string">"card-img-top"</span> <span class="variable">alt</span>=<span class="string">"Nom du produit"</span><span class="tag">&gt;</span>
  <span class="tag">&lt;div</span> <span class="variable">class</span>=<span class="string">"card-body"</span><span class="tag">&gt;</span>
    <span class="tag">&lt;h5</span> <span class="variable">class</span>=<span class="string">"card-title"</span><span class="tag">&gt;</span>Nom du produit<span class="tag">&lt;/h5&gt;</span>
    <span class="tag">&lt;p</span> <span class="variable">class</span>=<span class="string">"card-text"</span><span class="tag">&gt;</span>Description courte du produit.<span class="tag">&lt;/p&gt;</span>
    <span class="tag">&lt;p</span> <span class="variable">class</span>=<span class="string">"h4 text-primary"</span><span class="tag">&gt;</span>29,99 €<span class="tag">&lt;/p&gt;</span>
    <span class="tag">&lt;a</span> <span class="variable">href</span>=<span class="string">"#"</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="tag">&gt;</span>Ajouter au panier<span class="tag">&lt;/a&gt;</span>
  <span class="tag">&lt;/div&gt;</span>
<span class="tag">&lt;/div&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Ressources supplémentaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Ressources supplémentaires</h2>

                <div class="code-example">
                    <ul>
                        <li><a href="https://getbootstrap.com/docs/" target="_blank"
                                class="btn-purple btn-hover">Documentation officielle</a></li>
                        <li><a href="https://getbootstrap.com/docs/5.3/examples/" target="_blank"
                                class="btn-purple btn-hover">Exemples et templates</a></li>
                        <li><a href="https://icons.getbootstrap.com/" target="_blank"
                                class="btn-purple btn-hover">Bootstrap Icons</a></li>
                        <li><a href="https://themes.getbootstrap.com/" target="_blank"
                                class="btn-purple btn-hover">Thèmes premium</a></li>
                    </ul>
                </div>
            </section>
        </div>
    </div>
</template>

<script setup>

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

/* COULEURS VS CODE AMÉLIORÉES */
.comment {
    color: #6a9955 !important;
    font-style: italic;
}

.tag {
    color: #569cd6 !important;
}

.variable {
    color: #9cdcfe !important;
}

.string {
    color: #ce9178 !important;
}

.keyword {
    color: #c586c0 !important;
}

.function {
    color: #dcdcaa !important;
}

.operator {
    color: #d4d4d4 !important;
}

.constant {
    color: #4fc1ff !important;
}

.number {
    color: #b5cea8 !important;
}

.class-name {
    color: #4ec9b0 !important;
}

.attribute {
    color: #9cdcfe !important;
}

.property {
    color: #9cdcfe !important;
}

.punctuation {
    color: #d4d4d4 !important;
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