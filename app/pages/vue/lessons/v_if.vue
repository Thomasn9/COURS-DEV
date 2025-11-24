<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">La directive v-if en Vue.js</h1>
        <p class="lesson-meta text-white">Conditionner l'affichage de vos éléments</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à v-if</h2>
        <p class="textExemple">
          La directive <code>v-if</code> est l'une des directives conditionnelles les plus importantes en Vue.js. 
          Elle permet de conditionner l'affichage d'un élément HTML en fonction de la valeur d'une expression JavaScript.
        </p>
        <p class="textExemple">
          Lorsque l'expression évaluée est <strong>truthy</strong> (vraie), l'élément est rendu dans le DOM. 
          Dans le cas contraire, il est complètement supprimé du DOM.
        </p>
      </section>

      <!-- Syntaxe de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de base</h2>
        <p class="textExemple">
          La syntaxe de base de <code>v-if</code> est simple : elle s'utilise comme un attribut sur l'élément que vous souhaitez conditionner.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Exemple de base :</h4>
          <pre v-pre><code>&lt;div <span class="variable">v-if</span>="<span class="variable">condition</span>"&gt;
  Ce contenu s'affiche uniquement si la condition est vraie
&lt;/div&gt;</code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Exemple avec une variable :</h4>
          <pre v-pre><code>&lt;template&gt;
  &lt;div&gt;
    &lt;p <span class="variable">v-if</span>="<span class="variable">isVisible</span>"&gt;Je suis visible !&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">data</span>() {
    <span class="keyword">return</span> {
      <span class="variable">isVisible</span>: <span class="keyword">true</span>
    }
  }
}
&lt;/script&gt;</code></pre>
        </div>
      </section>

      <!-- v-else et v-else-if -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">v-else et v-else-if</h2>
        <p class="textExemple">
          Vue.js fournit également les directives <code>v-else</code> et <code>v-else-if</code> pour créer des structures conditionnelles plus complexes.
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Avec v-else :</h4>
            <pre v-pre><code>&lt;div <span class="variable">v-if</span>="<span class="variable">isLoggedIn</span>"&gt;
  Bienvenue, utilisateur !
&lt;/div&gt;
&lt;div <span class="variable">v-else</span>&gt;
  Veuillez vous connecter.
&lt;/div&gt;</code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">Avec v-else-if :</h4>
            <pre v-pre><code>&lt;div <span class="variable">v-if</span>="<span class="variable">type</span> === <span class="string">'A'</span>"&gt;
  Type A
&lt;/div&gt;
&lt;div <span class="variable">v-else-if</span>="<span class="variable">type</span> === <span class="string">'B'</span>"&gt;
  Type B
&lt;/div&gt;
&lt;div <span class="variable">v-else-if</span>="<span class="variable">type</span> === <span class="string">'C'</span>"&gt;
  Type C
&lt;/div&gt;
&lt;div <span class="variable">v-else</span>&gt;
  Type inconnu
&lt;/div&gt;</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <p><strong>Important :</strong> Les éléments avec <code>v-else</code> ou <code>v-else-if</code> doivent immédiatement suivre un élément avec <code>v-if</code> ou <code>v-else-if</code>.</p>
        </div>
      </section>

      <!-- v-if vs v-show -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">v-if vs v-show</h2>
        <p class="textExemple">
          Il est important de comprendre la différence entre <code>v-if</code> et <code>v-show</code> :
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">v-if</h4>
            <ul>
              <li>Conditionnel au niveau du <strong>rendu</strong></li>
              <li>L'élément est complètement supprimé du DOM quand la condition est fausse</li>
              <li>Plus coûteux en performance lors du basculement</li>
              <li>Supporte <code>v-else</code> et <code>v-else-if</code></li>
            </ul>
          </div>

          <div class="code-example">
            <h4 class="text-purple">v-show</h4>
            <ul>
              <li>Conditionnel au niveau du <strong>style</strong></li>
              <li>L'élément est toujours dans le DOM, mais caché avec <code>display: none</code></li>
              <li>Moins coûteux en performance lors du basculement</li>
              <li>Ne supporte pas <code>v-else</code></li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Quand utiliser v-if vs v-show ?</h4>
          <pre v-pre><code><span class="comment">// Utilisez v-if quand :</span>
<span class="comment">// - La condition change rarement</span>
<span class="comment">// - L'élément est coûteux à rendre</span>
<span class="comment">// - Vous avez besoin de v-else ou v-else-if</span>

<span class="comment">// Utilisez v-show quand :</span>
<span class="comment">// - La condition change fréquemment</span>
<span class="comment">// - L'élément est simple et peu coûteux</span></code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques</h2>
        
        <div class="code-example">
          <h4 class="text-purple">1. Éviter v-if et v-for sur le même élément</h4>
          <pre v-pre><code><span class="comment">// ❌ À éviter</span>
&lt;div <span class="variable">v-for</span>="<span class="variable">item</span> <span class="keyword">in</span> <span class="variable">items</span>" <span class="variable">v-if</span>="<span class="variable">item</span>.<span class="variable">isActive</span>"&gt;
  {{ item.name }}
&lt;/div&gt;

<span class="comment">// ✅ Préférez cette approche</span>
&lt;div <span class="variable">v-for</span>="<span class="variable">item</span> <span class="keyword">in</span> <span class="variable">activeItems</span>"&gt;
  {{ item.name }}
&lt;/div&gt;

&lt;script&gt;
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">computed</span>: {
    <span class="function">activeItems</span>() {
      <span class="keyword">return</span> <span class="keyword">this</span>.<span class="variable">items</span>.<span class="function">filter</span>(<span class="variable">item</span> <span class="operator">=></span> <span class="variable">item</span>.<span class="variable">isActive</span>)
    }
  }
}
&lt;/script&gt;</code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple">2. Utiliser &lt;template&gt; pour grouper plusieurs éléments</h4>
          <pre v-pre><code><span class="comment">// ✅ Bonne pratique</span>
&lt;template <span class="variable">v-if</span>="<span class="variable">isVisible</span>"&gt;
  &lt;h2&gt;Titre&lt;/h2&gt;
  &lt;p&gt;Paragraphe&lt;/p&gt;
  &lt;button&gt;Action&lt;/button&gt;
&lt;/template&gt;</code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h4 class="text-purple">Exercice 1 : Afficher un message conditionnel</h4>
          <p>Créez un composant qui affiche un message différent selon l'heure de la journée (matin, après-midi, soir).</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre v-pre><code>&lt;template&gt;
  &lt;div&gt;
    &lt;p <span class="variable">v-if</span>="<span class="variable">hour</span> &lt; <span class="number">12</span>"&gt;Bonjour !&lt;/p&gt;
    &lt;p <span class="variable">v-else-if</span>="<span class="variable">hour</span> &lt; <span class="number">18</span>"&gt;Bon après-midi !&lt;/p&gt;
    &lt;p <span class="variable">v-else</span>&gt;Bonsoir !&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">data</span>() {
    <span class="keyword">return</span> {
      <span class="variable">hour</span>: <span class="keyword">new</span> <span class="class-name">Date</span>().<span class="function">getHours</span>()
    }
  }
}
&lt;/script&gt;</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h4 class="text-purple">Exercice 2 : Système de notation</h4>
          <p>Créez un composant qui affiche une note sous forme d'étoiles selon une valeur numérique.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre v-pre><code>&lt;template&gt;
  &lt;div&gt;
    &lt;span <span class="variable">v-if</span>="<span class="variable">rating</span> >= <span class="number">1</span>"&gt;⭐&lt;/span&gt;
    &lt;span <span class="variable">v-if</span>="<span class="variable">rating</span> >= <span class="number">2</span>"&gt;⭐&lt;/span&gt;
    &lt;span <span class="variable">v-if</span>="<span class="variable">rating</span> >= <span class="number">3</span>"&gt;⭐&lt;/span&gt;
    &lt;span <span class="variable">v-if</span>="<span class="variable">rating</span> >= <span class="number">4</span>"&gt;⭐&lt;/span&gt;
    &lt;span <span class="variable">v-if</span>="<span class="variable">rating</span> >= <span class="number">5</span>"&gt;⭐&lt;/span&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">props</span>: {
    <span class="variable">rating</span>: {
      <span class="keyword">type</span>: <span class="class-name">Number</span>,
      <span class="variable">required</span>: <span class="keyword">true</span>,
      <span class="function">validator</span>(<span class="variable">value</span>) {
        <span class="keyword">return</span> <span class="variable">value</span> >= <span class="number">0</span> && <span class="variable">value</span> <= <span class="number">5</span>
      }
    }
  }
}
&lt;/script&gt;</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <div class="text-white">
          <p class="textExemple">
            La directive <code>v-if</code> est un outil fondamental dans Vue.js pour gérer l'affichage conditionnel de vos composants. 
            Au cours de cette leçon, nous avons exploré ses différentes facettes et bonnes pratiques d'utilisation.
          </p>
          
          <h4 class="text-white" style="margin-top: 1.5rem;">Points clés à retenir :</h4>
          <ul>
            <li><strong>v-if</strong> est idéal pour les conditions qui changent rarement et pour les éléments coûteux à rendre</li>
            <li><strong>v-show</strong> est plus adapté aux basculements fréquents grâce à son coût de performance réduit</li>
            <li>Les directives <strong>v-else</strong> et <strong>v-else-if</strong> permettent de créer des logiques conditionnelles complexes</li>
            <li>Évitez toujours la combinaison <strong>v-if</strong> et <strong>v-for</strong> sur le même élément</li>
            <li>Utilisez la balise <strong>&lt;template&gt;</strong> pour grouper plusieurs éléments conditionnels</li>
          </ul>

          <p class="textExemple" style="margin-top: 1.5rem;">
            Maîtriser <code>v-if</code> et ses directives associées vous permettra de créer des interfaces utilisateur dynamiques 
            et performantes. N'hésitez pas à pratiquer avec les exercices pour solidifier vos connaissances !
          </p>
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