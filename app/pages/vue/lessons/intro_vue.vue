<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Introduction à Vue.js</h1>
        <p class="lesson-meta text-white">Comprendre les bases du framework Vue.js</p>
      </header>

      <!-- Section 1: Qu'est-ce que Vue.js -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que Vue.js ?</h2>
        <p class="textExemple">
          Vue.js (souvent appelé simplement Vue) est un framework JavaScript progressif utilisé pour construire des interfaces utilisateur (UI) et des applications web monopage (SPA). Contrairement à d'autres frameworks monolithiques, Vue est conçu pour être adopté progressivement.
        </p>
        <p class="textExemple">
          Créé par <strong>Evan You</strong> en 2014, Vue combine les meilleures idées d'autres frameworks comme Angular et React, tout en restant simple et accessible.
        </p>
      </section>

      <!-- Section 2: À quoi sert Vue.js -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">À quoi sert Vue.js ?</h2>
        <p class="textExemple">
          Vue.js est principalement utilisé pour :
        </p>
        <ul class="textExemple">
          <li><strong>Créer des interfaces utilisateur interactives</strong> - Gérer efficacement les mises à jour du DOM</li>
          <li><strong>Développer des applications web monopage (SPA)</strong> - Applications qui chargent une seule page HTML et mettent à jour dynamiquement le contenu</li>
          <li><strong>Construire des composants réutilisables</strong> - Créer des éléments d'interface modulaires</li>
          <li><strong>Gérer l'état des applications</strong> - Suivre et synchroniser les données entre différents composants</li>
        </ul>
      </section>

      <!-- Section 3: Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Concepts fondamentaux de Vue.js</h2>
        
        <div class="code-example">
          <h3 class="text-purple">1. Instance Vue</h3>
          <p class="textExemple">Une application Vue commence par créer une instance Vue :</p>
          <pre><code class="language-javascript">
<span class="keyword">const</span> <span class="variable">app</span> = <span class="keyword">new</span> <span class="class-name">Vue</span>({
  <span class="variable">el</span>: <span class="string">'#app'</span>, <span class="comment">// Élément HTML cible</span>
  <span class="variable">data</span>: {
    <span class="variable">message</span>: <span class="string">'Bonjour Vue !'</span> <span class="comment">// Données réactives</span>
  }
})
          </code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">2. Liaison de données (Data Binding)</h3>
          <p class="textExemple">Vue utilise la syntaxe de double accolades pour lier les données :</p>
          <pre><code class="language-html">
<span class="comment">&lt;!-- Dans le HTML --&gt;</span>
&lt;div id=<span class="string">"app"</span>&gt;
  {{ message }}
&lt;/div&gt;
          </code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">3. Directives</h3>
          <p class="textExemple">Les directives sont des attributs spéciaux préfixés par <code>v-</code> :</p>
          <pre><code class="language-html">
<span class="comment">&lt;!-- v-bind : Liaison d'attributs --&gt;</span>
&lt;span v-bind:title=<span class="string">"message"</span>&gt;Passez la souris sur moi&lt;/span&gt;

<span class="comment">&lt;!-- v-if : Conditionnel --&gt;</span>
&lt;p v-if=<span class="string">"visible"</span>&gt;Ce texte est conditionnel&lt;/p&gt;

<span class="comment">&lt;!-- v-for : Boucles --&gt;</span>
&lt;li v-for=<span class="string">"item in items"</span>&gt;{{ item.name }}&lt;/li&gt;
          </code></pre>
        </div>
      </section>

      <!-- Section 4: Exemple complet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple complet simple</h2>
        <p class="textExemple">Voici un exemple complet qui montre les concepts de base :</p>
        
        <div class="code-example">
          <pre><code class="language-html">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;Mon app Vue&lt;/title&gt;
  &lt;script src=<span class="string">"https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"</span>&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div id=<span class="string">"app"</span>&gt;
    &lt;h1&gt;{{ title }}&lt;/h1&gt;
    &lt;input v-model=<span class="string">"name"</span> placeholder=<span class="string">"Entrez votre nom"</span>&gt;
    &lt;p&gt;Bonjour, {{ name }} !&lt;/p&gt;
    &lt;button v-on:click=<span class="string">"reverseMessage"</span>&gt;Inverser le message&lt;/button&gt;
    &lt;ul&gt;
      &lt;li v-for=<span class="string">"todo in todos"</span>&gt;{{ todo.text }}&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;

  &lt;script&gt;
<span class="keyword">const</span> <span class="variable">app</span> = <span class="keyword">new</span> <span class="class-name">Vue</span>({
  <span class="variable">el</span>: <span class="string">'#app'</span>,
  <span class="variable">data</span>: {
    <span class="variable">title</span>: <span class="string">'Ma première app Vue'</span>,
    <span class="variable">name</span>: <span class="string">''</span>,
    <span class="variable">todos</span>: [
      { <span class="variable">text</span>: <span class="string">'Apprendre Vue.js'</span> },
      { <span class="variable">text</span>: <span class="string">'Créer une app cool'</span> },
      { <span class="variable">text</span>: <span class="string">'Partager mes connaissances'</span> }
    ]
  },
  <span class="variable">methods</span>: {
    <span class="function">reverseMessage</span>: <span class="keyword">function</span> () {
      <span class="keyword">this</span>.<span class="variable">title</span> = <span class="keyword">this</span>.<span class="variable">title</span>.<span class="function">split</span>(<span class="string">''</span>).<span class="function">reverse</span>().<span class="function">join</span>(<span class="string">''</span>)
    }
  }
})
  &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
          </code></pre>
        </div>
      </section>

      <!-- Section 5: Avantages de Vue.js -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi choisir Vue.js ?</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">✅ Avantages</h3>
            <ul class="textExemple">
              <li><strong>Courbe d'apprentissage douce</strong> - Facile à apprendre pour les débutants</li>
              <li><strong>Documentation excellente</strong> - Une des meilleures documentations</li>
              <li><strong>Flexibilité</strong> - Peut être utilisé progressivement</li>
              <li><strong>Performance</strong> - Très léger et rapide</li>
              <li><strong>Écosystème riche</strong> - Beaucoup de plugins et outils</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">🔄 Comparaison</h3>
            <ul class="textExemple">
              <li><strong>Vue vs React</strong> - Syntaxe plus simple, moins de boilerplate</li>
              <li><strong>Vue vs Angular</strong> - Plus léger, moins d'opinions</li>
              <li><strong>Vue vs Svelte</strong> - Plus mature, écosystème plus large</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Section 6: Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <p class="textExemple">
            <strong>Objectif :</strong> Créez une petite application Vue qui affiche une liste de courses et permet d'ajouter de nouveaux éléments.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code class="language-html">
&lt;div id=<span class="string">"app"</span>&gt;
  &lt;h2&gt;Ma liste de courses&lt;/h2&gt;
  &lt;ul&gt;
    &lt;li v-for=<span class="string">"(item, index) in shoppingList"</span>&gt;
      {{ item }}
      &lt;button v-on:click=<span class="string">"removeItem(index)"</span>&gt;Supprimer&lt;/button&gt;
    &lt;/li&gt;
  &lt;/ul&gt;
  &lt;input v-model=<span class="string">"newItem"</span> placeholder=<span class="string">"Nouvel article"</span>&gt;
  &lt;button v-on:click=<span class="string">"addItem"</span>&gt;Ajouter&lt;/button&gt;
&lt;/div&gt;

&lt;script&gt;
<span class="keyword">new</span> <span class="class-name">Vue</span>({
  <span class="variable">el</span>: <span class="string">'#app'</span>,
  <span class="variable">data</span>: {
    <span class="variable">shoppingList</span>: [<span class="string">'Pommes'</span>, <span class="string">'Pain'</span>, <span class="string">'Lait'</span>],
    <span class="variable">newItem</span>: <span class="string">''</span>
  },
  <span class="variable">methods</span>: {
    <span class="function">addItem</span>: <span class="keyword">function</span>() {
      <span class="keyword">if</span> (<span class="keyword">this</span>.<span class="variable">newItem</span>) {
        <span class="keyword">this</span>.<span class="variable">shoppingList</span>.<span class="function">push</span>(<span class="keyword">this</span>.<span class="variable">newItem</span>);
        <span class="keyword">this</span>.<span class="variable">newItem</span> = <span class="string">''</span>;
      }
    },
    <span class="function">removeItem</span>: <span class="keyword">function</span>(<span class="variable">index</span>) {
      <span class="keyword">this</span>.<span class="variable">shoppingList</span>.<span class="function">splice</span>(<span class="variable">index</span>, <span class="number">1</span>);
    }
  }
})
&lt;/script&gt;
              </code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Section 7: Prochaines étapes -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Prochaines étapes</h2>
        <p class="text-white">
          Maintenant que vous comprenez les bases de Vue.js, voici ce que vous devriez apprendre ensuite :
        </p>
        <ul class="text-white">
          <li>Composants Vue (syntaxe single-file .vue)</li>
          <li>Vue Router pour la navigation</li>
          <li>Vuex pour la gestion d'état</li>
          <li>Composition API (Vue 3)</li>
          <li>Intégration avec Nuxt.js</li>
        </ul>
        <a href="#" class="btn-purple btn-hover" style="margin-top: 1rem;">Leçon suivante : Les Composants Vue</a>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueIntroductionLesson',
  // Vous pouvez ajouter des données ou méthodes si nécessaire
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