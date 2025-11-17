<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Vitest - Framework de Tests Ultra-Rapide</h1>
        <p class="lesson-meta text-white">Apprenez à installer et configurer Vitest dans différents environnements</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à Vitest</h2>
        <p class="textExemple">
          Vitest est un framework de tests unitaires ultra-rapide conçu spécifiquement pour les projets utilisant Vite. 
          Il offre une expérience de développement exceptionnelle avec un rechargement à chaud (HMR) pour vos tests.
        </p>
        <div class="code-example">
          <h3 class="text-purple">Avantages de Vitest</h3>
          <ul>
            <li>Compatibilité avec Jest (même API)</li>
            <li>Configuration quasi nulle</li>
            <li>Exécution extrêmement rapide</li>
            <li>Support natif de TypeScript, JSX et TSX</li>
            <li>Mode watch intelligent</li>
          </ul>
        </div>
      </section>

      <!-- Installation générale -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Installation de base</h2>
        <p class="textExemple">
          Commençons par l'installation de base de Vitest dans un nouveau projet.
        </p>
        
        <div class="code-block">
          <h3 class="text-purple">Installation avec npm</h3>
          <pre><code><span class="comment"># Installation de Vitest comme dépendance de développement</span>
<span class="keyword">npm</span> <span class="function">install</span> -D <span class="variable">vitest</span></code></pre>
        </div>

        <div class="code-block">
          <h3 class="text-purple">Installation avec yarn</h3>
          <pre><code><span class="comment"># Installation avec Yarn</span>
<span class="keyword">yarn</span> <span class="function">add</span> -D <span class="variable">vitest</span></code></pre>
        </div>

        <div class="code-block">
          <h3 class="text-purple">Installation avec pnpm</h3>
          <pre><code><span class="comment"># Installation avec pnpm</span>
<span class="keyword">pnpm</span> <span class="function">add</span> -D <span class="variable">vitest</span></code></pre>
        </div>
      </section>

      <!-- Configuration pour différents environnements -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Configuration selon l'environnement</h2>
        
        <!-- Projet Vanilla JavaScript -->
        <div class="code-example">
          <h3 class="text-purple">1. Projet Vanilla JavaScript</h3>
          <p class="textExemple">
            Pour un projet JavaScript simple sans framework.
          </p>
          <pre><code><span class="comment">// vitest.config.js</span>
<span class="keyword">import</span> { <span class="variable">defineConfig</span> } <span class="keyword">from</span> <span class="string">'vitest/config'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineConfig</span>({
  <span class="variable">test</span>: {
    <span class="variable">environment</span>: <span class="string">'jsdom'</span>, <span class="comment">// Pour tester le DOM</span>
    <span class="variable">globals</span>: <span class="constant">true</span>
  }
})</code></pre>
        </div>

        <!-- Projet Vue.js -->
        <div class="code-example">
          <h3 class="text-purple">2. Projet Vue.js</h3>
          <p class="textExemple">
            Configuration pour un projet Vue.js avec Vue Test Utils.
          </p>
          <pre><code><span class="comment">// vitest.config.js</span>
<span class="keyword">import</span> { <span class="variable">defineConfig</span> } <span class="keyword">from</span> <span class="string">'vitest/config'</span>
<span class="keyword">import</span> <span class="variable">Vue</span> <span class="keyword">from</span> <span class="string">'@vitejs/plugin-vue'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineConfig</span>({
  <span class="variable">plugins</span>: [<span class="function">Vue</span>()],
  <span class="variable">test</span>: {
    <span class="variable">globals</span>: <span class="constant">true</span>,
    <span class="variable">environment</span>: <span class="string">'jsdom'</span>
  }
})</code></pre>
          
          <p class="textExemple">Installation des dépendances supplémentaires :</p>
          <pre><code><span class="keyword">npm</span> <span class="function">install</span> -D <span class="variable">@vue/test-utils</span> <span class="variable">jsdom</span></code></pre>
        </div>

        <!-- Projet React -->
        <div class="code-example">
          <h3 class="text-purple">3. Projet React</h3>
          <p class="textExemple">
            Configuration pour un projet React avec Testing Library.
          </p>
          <pre><code><span class="comment">// vitest.config.js</span>
<span class="keyword">import</span> { <span class="variable">defineConfig</span> } <span class="keyword">from</span> <span class="string">'vitest/config'</span>
<span class="keyword">import</span> <span class="variable">React</span> <span class="keyword">from</span> <span class="string">'@vitejs/plugin-react'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineConfig</span>({
  <span class="variable">plugins</span>: [<span class="function">React</span>()],
  <span class="variable">test</span>: {
    <span class="variable">globals</span>: <span class="constant">true</span>,
    <span class="variable">environment</span>: <span class="string">'jsdom'</span>,
    <span class="variable">setupFiles</span>: <span class="string">'./src/test-setup.js'</span>
  }
})</code></pre>
          
          <p class="textExemple">Installation des dépendances supplémentaires :</p>
          <pre><code><span class="keyword">npm</span> <span class="function">install</span> -D <span class="variable">@testing-library/react</span> <span class="variable">@testing-library/jest-dom</span> <span class="variable">jsdom</span></code></pre>
        </div>

        <!-- Projet Nuxt -->
        <div class="code-example">
          <h3 class="text-purple">4. Projet Nuxt</h3>
          <p class="textExemple">
            Configuration spécifique pour un projet Nuxt.
          </p>
          <pre><code><span class="comment">// vitest.config.js</span>
<span class="keyword">import</span> { <span class="variable">defineConfig</span> } <span class="keyword">from</span> <span class="string">'vitest/config'</span>
<span class="keyword">import</span> <span class="variable">Vue</span> <span class="keyword">from</span> <span class="string">'@vitejs/plugin-vue'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineConfig</span>({
  <span class="variable">plugins</span>: [<span class="function">Vue</span>()],
  <span class="variable">test</span>: {
    <span class="variable">globals</span>: <span class="constant">true</span>,
    <span class="variable">environment</span>: <span class="string">'jsdom'</span>,
    <span class="comment">// Configuration spécifique Nuxt</span>
    <span class="variable">setupFiles</span>: [<span class="string">'~/test-setup.js'</span>]
  }
})</code></pre>
        </div>

        <!-- Projet TypeScript -->
        <div class="code-example">
          <h3 class="text-purple">5. Projet TypeScript</h3>
          <p class="textExemple">
            Configuration pour un projet TypeScript.
          </p>
          <pre><code><span class="comment">// vitest.config.ts</span>
<span class="keyword">import</span> { <span class="variable">defineConfig</span> } <span class="keyword">from</span> <span class="string">'vitest/config'</span>

<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineConfig</span>({
  <span class="variable">test</span>: {
    <span class="variable">globals</span>: <span class="constant">true</span>,
    <span class="variable">environment</span>: <span class="string">'node'</span>,
    <span class="comment">// Pour les projets TypeScript</span>
    <span class="variable">typecheck</span>: {
      <span class="variable">checker</span>: <span class="string">'tsc'</span>
    }
  }
})</code></pre>
        </div>
      </section>

      <!-- Scripts de test -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Scripts npm pour les tests</h2>
        <p class="textExemple">
          Ajoutez ces scripts à votre fichier <code>package.json</code> pour exécuter facilement vos tests.
        </p>
        
        <div class="code-block">
          <pre><code>{
  <span class="string">"scripts"</span>: {
    <span class="string">"test"</span>: <span class="string">"vitest"</span>,
    <span class="string">"test:run"</span>: <span class="string">"vitest run"</span>,
    <span class="string">"test:ui"</span>: <span class="string">"vitest --ui"</span>,
    <span class="string">"test:coverage"</span>: <span class="string">"vitest run --coverage"</span>
  }
}</code></pre>
        </div>
      </section>

      <!-- Exemple de test -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple de test avec Vitest</h2>
        <p class="textExemple">
          Voici un exemple simple de test unitaire avec Vitest.
        </p>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Fonction à tester</h3>
            <pre><code><span class="comment">// math.js</span>
<span class="keyword">export</span> <span class="keyword">function</span> <span class="function">add</span>(<span class="variable">a</span>, <span class="variable">b</span>) {
  <span class="keyword">return</span> <span class="variable">a</span> <span class="operator">+</span> <span class="variable">b</span>
}

<span class="keyword">export</span> <span class="keyword">function</span> <span class="function">multiply</span>(<span class="variable">a</span>, <span class="variable">b</span>) {
  <span class="keyword">return</span> <span class="variable">a</span> <span class="operator">*</span> <span class="variable">b</span>
}</code></pre>
          </div>
          
          <div>
            <h3 class="text-purple">Fichier de test</h3>
            <pre><code><span class="comment">// math.test.js</span>
<span class="keyword">import</span> { <span class="variable">describe</span>, <span class="variable">it</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">'vitest'</span>
<span class="keyword">import</span> { <span class="variable">add</span>, <span class="variable">multiply</span> } <span class="keyword">from</span> <span class="string">'./math'</span>

<span class="function">describe</span>(<span class="string">'Fonctions mathématiques'</span>, () => {
  <span class="function">it</span>(<span class="string">'devrait additionner deux nombres'</span>, () => {
    <span class="function">expect</span>(<span class="function">add</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">5</span>)
  })
  
  <span class="function">it</span>(<span class="string">'devrait multiplier deux nombres'</span>, () => {
    <span class="function">expect</span>(<span class="function">multiply</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">6</span>)
  })
})</code></pre>
          </div>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Créer une fonction de validation d'email</h3>
          <p class="textExemple">
            Créez une fonction <code>isValidEmail(email)</code> qui retourne <code>true</code> si l'email est valide, <code>false</code> sinon.
            Puis écrivez les tests unitaires pour cette fonction.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Fonction de validation</h4>
              <pre><code><span class="comment">// emailValidator.js</span>
<span class="keyword">export</span> <span class="keyword">function</span> <span class="function">isValidEmail</span>(<span class="variable">email</span>) {
  <span class="keyword">const</span> <span class="variable">emailRegex</span> = <span class="regex">/^[^\s@]+@[^\s@]+\.[^\s@]+$/</span>
  <span class="keyword">return</span> <span class="variable">emailRegex</span>.<span class="function">test</span>(<span class="variable">email</span>)
}</code></pre>
              
              <h4 class="text-purple">Tests unitaires</h4>
              <pre><code><span class="comment">// emailValidator.test.js</span>
<span class="keyword">import</span> { <span class="variable">describe</span>, <span class="variable">it</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">'vitest'</span>
<span class="keyword">import</span> { <span class="variable">isValidEmail</span> } <span class="keyword">from</span> <span class="string">'./emailValidator'</span>

<span class="function">describe</span>(<span class="string">'Validation d\'email'</span>, () => {
  <span class="function">it</span>(<span class="string">'devrait retourner true pour un email valide'</span>, () => {
    <span class="function">expect</span>(<span class="function">isValidEmail</span>(<span class="string">'test@example.com'</span>)).<span class="function">toBe</span>(<span class="constant">true</span>)
    <span class="function">expect</span>(<span class="function">isValidEmail</span>(<span class="string">'user.name@domain.co.uk'</span>)).<span class="function">toBe</span>(<span class="constant">true</span>)
  })
  
  <span class="function">it</span>(<span class="string">'devrait retourner false pour un email invalide'</span>, () => {
    <span class="function">expect</span>(<span class="function">isValidEmail</span>(<span class="string">'invalid-email'</span>)).<span class="function">toBe</span>(<span class="constant">false</span>)
    <span class="function">expect</span>(<span class="function">isValidEmail</span>(<span class="string">'test@'</span>)).<span class="function">toBe</span>(<span class="constant">false</span>)
    <span class="function">expect</span>(<span class="function">isValidEmail</span>(<span class="string">'@domain.com'</span>)).<span class="function">toBe</span>(<span class="constant">false</span>)
    <span class="function">expect</span>(<span class="function">isValidEmail</span>(<span class="string">''</span>)).<span class="function">toBe</span>(<span class="constant">false</span>)
  })
})</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Ressources supplémentaires -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        <p class="textExemple">
          Pour approfondir vos connaissances sur Vitest, consultez ces ressources :
        </p>
        
        <div class="code-example">
          <a href="https://vitest.dev/" class="btn-purple btn-hover" target="_blank">Documentation officielle</a>
          <a href="https://github.com/vitest-dev/vitest" class="btn-purple btn-hover" target="_blank">GitHub</a>
          <a href="https://vitest.dev/guide/migration.html" class="btn-purple btn-hover" target="_blank">Migration depuis Jest</a>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
// Le code JavaScript pour cette page irait ici
// Par exemple, pour gérer l'interactivité des composants
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
.code-example, .code-block {
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
    white-space: pre-wrap; /* Permet le retour à la ligne */
    word-wrap: break-word; /* Casse les mots longs */
    word-break: break-word; /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap; /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword { color: #c586c0 !important; } /* Mots-clés (for, while, if, function, etc.) */
.variable { color: #9cdcfe !important; } /* Variables et noms de fonctions */
.string { color: #ce9178 !important; } /* Chaînes de caractères */
.comment { color: #6a9955 !important; } /* Commentaires */
.function { color: #dcdcaa !important; } /* Noms de fonctions */
.operator { color: #d4d4d4 !important; } /* Opérateurs (+, -, =, =>, etc.) */
.constant { color: #4fc1ff !important; } /* Constantes */
.number { color: #b5cea8 !important; } /* Nombres */
.class-name { color: #4ec9b0 !important; } /* Noms de classes */
.regex { color: #d16969 !important; } /* Expressions régulières */

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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>