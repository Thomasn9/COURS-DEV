<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Introduction à Vue.js</h1>
        <p class="lesson-meta text-white">Découvrez le framework JavaScript progressif qui révolutionne le développement web</p>
        <div class="lesson-duration">
          <span class="duration-badge">Durée : 30 min</span>
          <span class="level-badge">Niveau : Débutant</span>
        </div>
      </header>

      <!-- Section Objectifs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'apprentissage</h2>
        <div class="objectives-grid">
          <div class="objective-item">
            <h3 class="text-purple">Comprendre Vue.js</h3>
            <p class="textExemple">Savoir ce qu'est Vue.js et pourquoi l'utiliser</p>
          </div>
          <div class="objective-item">
            <h3 class="text-purple">Concepts de base</h3>
            <p class="textExemple">Maîtriser les concepts fondamentaux</p>
          </div>
          <div class="objective-item">
            <h3 class="text-purple">Première application</h3>
            <p class="textExemple">Créer votre première app Vue.js</p>
          </div>
          <div class="objective-item">
            <h3 class="text-purple">Écosystème</h3>
            <p class="textExemple">Découvrir l'écosystème Vue</p>
          </div>
        </div>
      </section>

      <!-- Section 1: Qu'est-ce que Vue.js -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que Vue.js ?</h2>
        
        <div class="definition-card">
          <div class="definition-content">
            <h3 class="text-purple">Définition</h3>
            <p class="textExemple">
              <strong>Vue.js</strong> est un framework JavaScript <strong>progressif</strong> utilisé pour construire des interfaces utilisateur et des applications web modernes.
            </p>
            <div class="key-points">
              <div class="key-point">
                <strong>Progressif</strong> : Adoptable progressivement
              </div>
              <div class="key-point">
                <strong>Performant</strong> : Léger et rapide
              </div>
              <div class="key-point">
                <strong>Accessible</strong> : Courbe d'apprentissage douce
              </div>
            </div>
          </div>
          <div class="definition-meta">
            <div class="meta-item">
              <strong>Créateur :</strong> Evan You
            </div>
            <div class="meta-item">
              <strong>Première version :</strong> 2014
            </div>
            <div class="meta-item">
              <strong>Version actuelle :</strong> Vue 3
            </div>
            <div class="meta-item">
              <strong>GitHub :</strong> 200k+ stars
            </div>
          </div>
        </div>

        <div class="philosophy-section">
          <h3 class="text-purple">La philosophie Vue.js</h3>
          <p class="textExemple">
            Vue.js a été conçu pour combiner le meilleur d'Angular et de React, tout en restant 
            <strong>simple à apprendre</strong> et <strong>agréable à utiliser</strong>.
          </p>
        </div>
      </section>

      <!-- Section 2: Pourquoi Vue.js -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi choisir Vue.js ?</h2>
        
        <div class="comparison-section">
          <div class="advantages">
            <h3 class="text-purple">Avantages de Vue.js</h3>
            <ul class="textExemple">
              <li><strong>Courbe d'apprentissage douce</strong> - Syntaxe intuitive basée sur HTML</li>
              <li><strong>Documentation excellente</strong> - Une des meilleures documentations</li>
              <li><strong>Flexibilité</strong> - Utilisable progressivement</li>
              <li><strong>Performance</strong> - Seulement ~20KB gzipped</li>
              <li><strong>Écosystème riche</strong> - Vue Router, Vuex, Vite, etc.</li>
              <li><strong>Communauté active</strong> - Support et ressources abondants</li>
            </ul>
          </div>
          
          <div class="use-cases">
            <h3 class="text-purple">Cas d'utilisation</h3>
            <ul class="textExemple">
              <li><strong>Applications monopages (SPA)</strong></li>
              <li><strong>Interfaces utilisateur complexes</strong></li>
              <li><strong>Prototypage rapide</strong></li>
              <li><strong>Intégration progressive</strong></li>
              <li><strong>Applications mobiles (avec NativeScript)</strong></li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Section 3: Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Concepts fondamentaux</h2>
        
        <div class="concepts-grid">
          <div class="concept-card">
            <h3 class="text-purple">Instance Vue</h3>
            <p class="textExemple">Point d'entrée de toute application Vue</p>
            <pre><code class="language-javascript">const app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})</code></pre>
          </div>

          <div class="concept-card">
            <h3 class="text-purple">Liaison de données</h3>
            <p class="textExemple">Synchronisation automatique entre JS et HTML</p>
            <pre><code class="language-html">&lt;div id="app"&gt;
  {{ message }}
&lt;/div&gt;</code></pre>
          </div>

          <div class="concept-card">
            <h3 class="text-purple">Directives</h3>
            <p class="textExemple">Attributs spéciaux préfixés par v-</p>
            <pre><code class="language-html">&lt;div v-if="visible"&gt;Conditionnel&lt;/div&gt;
&lt;li v-for="item in items"&gt;{{ item }}&lt;/li&gt;
&lt;button v-on:click="method"&gt;Click&lt;/button&gt;</code></pre>
          </div>

          <div class="concept-card">
            <h3 class="text-purple">Réactivité</h3>
            <p class="textExemple">Mise à jour automatique de l'interface</p>
            <pre><code class="language-javascript">data: {
  count: 0  // Modifiable réactivement
},
methods: {
  increment() {
    this.count++ // L'interface se met à jour automatiquement
  }
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Section 4: Première application -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Votre première application Vue</h2>
        
        <div class="live-demo">
          <h3 class="text-purple">Application de liste de tâches</h3>
          <p class="textExemple">Créez une application de liste de tâches complète :</p>
          
          <div class="demo-container">
            <div class="code-editor">
              <h4 class="text-purple">HTML</h4>
              <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;Ma Todo List Vue.js&lt;/title&gt;
  &lt;script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div id="app"&gt;
    &lt;h3&gt;Ma Liste de Tâches&lt;/h3&gt;
    &lt;div class="input-group"&gt;
      &lt;input v-model="newTask" 
             placeholder="Nouvelle tâche"
             @keyup.enter="addTask"&gt;
      &lt;button @click="addTask"&gt;Ajouter&lt;/button&gt;
    &lt;/div&gt;
    
    &lt;ul class="task-list"&gt;
      &lt;li v-for="(task, index) in tasks" 
          :key="index"
          class="task-item"&gt;
        &lt;span&gt;{{ task }}&lt;/span&gt;
        &lt;button @click="removeTask(index)"&gt;
          Supprimer
        &lt;/button&gt;
      &lt;/li&gt;
    &lt;/ul&gt;
    
    &lt;div v-if="tasks.length === 0" class="empty-state"&gt;
      Aucune tâche pour le moment
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
            </div>
            
            <div class="code-editor">
              <h4 class="text-purple">JavaScript</h4>
              <pre><code class="language-javascript">new Vue({
  el: '#app',
  data: {
    newTask: '',
    tasks: ['Apprendre Vue.js', 'Créer une application']
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push(this.newTask.trim());
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  },
  mounted() {
    console.log('Application Vue.js démarrée !');
  }
});</code></pre>
            </div>
          </div>
        </div>
      </section>

      <!-- Section 5: Écosystème Vue -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">L'écosystème Vue.js</h2>
        
        <div class="ecosystem-grid">
          <div class="tool-card">
            <h3 class="text-purple">Vue Router</h3>
            <p class="textExemple">Gestion de la navigation et des routes pour applications monopages</p>
          </div>
          
          <div class="tool-card">
            <h3 class="text-purple">Vuex / Pinia</h3>
            <p class="textExemple">Gestion d'état centralisée pour les applications complexes</p>
          </div>
          
          <div class="tool-card">
            <h3 class="text-purple">Vite</h3>
            <p class="textExemple">Outil de build ultra-rapide pour le développement moderne</p>
          </div>
          
          <div class="tool-card">
            <h3 class="text-purple">Vue DevTools</h3>
            <p class="textExemple">Extension navigateur pour déboguer les applications Vue</p>
          </div>
          
          <div class="tool-card">
            <h3 class="text-purple">Nuxt.js</h3>
            <p class="textExemple">Framework full-stack basé sur Vue.js pour le rendu universel</p>
          </div>
          
          <div class="tool-card">
            <h3 class="text-purple">Vue CLI</h3>
            <p class="textExemple">Outil en ligne de commande pour scaffoldiser des projets Vue</p>
          </div>
        </div>
      </section>

      <!-- Section 6: Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        
        <div class="conclusion-content">
          <div class="conclusion-summary">
            <h3 class="text-white">Récapitulatif des points clés</h3>
            <ul class="text-white">
              <li><strong>Framework progressif</strong> - Vue.js peut être intégré progressivement dans les projets existants</li>
              <li><strong>Syntaxe intuitive</strong> - Basée sur le HTML standard avec des directives simples</li>
              <li><strong>Système réactif</strong> - Mise à jour automatique de l'interface utilisateur</li>
              <li><strong>Écosystème mature</strong> - Outils, bibliothèques et communauté active</li>
              <li><strong>Performance optimisée</strong> - Poids léger et mécanismes de rendu efficaces</li>
            </ul>
          </div>

          <div class="conclusion-perspective">
            <h3 class="text-white">Vue.js dans le paysage des frameworks</h3>
            <p class="text-white">
              Vue.js s'est imposé comme une alternative sérieuse aux autres frameworks JavaScript grâce à son approche pragmatique. 
              Son adoption par des entreprises comme <strong>GitLab, Alibaba, BMW et Nintendo</strong> témoigne de sa robustesse 
              en environnement de production.
            </p>
          </div>

          <div class="conclusion-benefits">
            <h3 class="text-white">Pourquoi Vue.js continue de gagner en popularité</h3>
            <div class="benefits-grid">
              <div class="benefit-item">
                <h4 class="text-white">Productivité accrue</h4>
                <p class="text-white">Syntaxe claire et outils de développement excellents</p>
              </div>
              <div class="benefit-item">
                <h4 class="text-white">Performance remarquable</h4>
                <p class="text-white">Bundle léger et système de rendu virtuel optimisé</p>
              </div>
              <div class="benefit-item">
                <h4 class="text-white">Polyvalence exceptionnelle</h4>
                <p class="text-white">Du petit widget aux grandes applications enterprise</p>
              </div>
              <div class="benefit-item">
                <h4 class="text-white">Communauté solide</h4>
                <p class="text-white">Support actif et documentation complète en multiples langues</p>
              </div>
            </div>
          </div>

          <div class="conclusion-final">
            <div class="final-thoughts">
              <p class="text-white">
                <strong>Vous avez maintenant les bases fondamentales pour démarrer avec Vue.js.</strong> 
                Ce framework combine élégamment simplicité et puissance, ce qui en fait un excellent choix 
                autant pour les débutants que pour les développeurs expérimentés.
              </p>
              <p class="text-white">
                La courbe d'apprentissage douce de Vue.js vous permettra de créer des applications 
                interactives rapidement, tout en vous préparant à aborder des concepts plus avancés 
                au fur et à mesure que vos besoins évoluent.
              </p>
            </div>
            
            <div class="action-call">
              <p class="text-white" style="text-align: center; font-weight: 600;">
                Le voyage ne fait que commencer ! Continuez à explorer, expérimenter et construire 
                avec Vue.js pour maîtriser ce framework remarquable.
              </p>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueJsIntroductionLesson',
  data() {
    return {
      lessonTitle: 'Introduction à Vue.js'
    }
  }
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

/* Header amélioré */
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
    margin-bottom: 1.5rem;
}

.lesson-duration {
    display: flex;
    gap: 1rem;
    justify-content: center;
    position: relative;
}

.duration-badge, .level-badge {
    background: rgba(255, 255, 255, 0.2);
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.9rem;
}

/* Grille des objectifs */
.objectives-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.objective-item {
    text-align: center;
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
    transition: transform 0.3s ease;
}

.objective-item:hover {
    transform: translateY(-5px);
}

/* Cartes de définition */
.definition-card {
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 2rem;
    margin: 1.5rem 0;
}

.key-points {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-top: 1rem;
}

.key-point {
    padding: 0.5rem;
    background: #f8f6ff;
    border-radius: 5px;
    border-left: 3px solid #8B5FBF;
}

.definition-meta {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

.meta-item {
    margin-bottom: 0.5rem;
    padding: 0.5rem 0;
    border-bottom: 1px solid #f0f0f0;
}

.meta-item:last-child {
    border-bottom: none;
    margin-bottom: 0;
}

/* Comparaison */
.comparison-section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin-top: 1.5rem;
}

/* Grille des concepts */
.concepts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.concept-card {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
    transition: transform 0.3s ease;
}

.concept-card:hover {
    transform: translateY(-5px);
}

/* Démo interactive */
.demo-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.code-editor {
    background: #1e1e1e;
    border-radius: 8px;
    overflow: hidden;
}

.code-editor h4 {
    background: #2d2d2d;
    padding: 0.75rem 1rem;
    margin: 0;
    color: #8B5FBF !important;
}

/* Écosystème */
.ecosystem-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-top: 1.5rem;
}

.tool-card {
    background: white;
    padding: 1.5rem 1rem;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.tool-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 25px rgba(106, 48, 147, 0.15);
}

/* Conclusion */
.conclusion-content {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.conclusion-summary,
.conclusion-perspective,
.conclusion-benefits,
.conclusion-final {
    padding: 1.5rem;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    border-left: 4px solid rgba(255, 255, 255, 0.3);
    backdrop-filter: blur(10px);
}

.benefits-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
}

.benefit-item {
    padding: 1rem;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 8px;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.action-call {
    background: rgba(255, 255, 255, 0.1);
    padding: 2rem;
    border-radius: 15px;
    text-align: center;
    margin-top: 2rem;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

/* Styles existants conservés */
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

/* Styles pour les blocs de code */
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
    margin: 1rem 0;
}

/* Coloration syntaxique VS Code améliorée */
pre code {
    display: block;
    background: none !important;
}

.language-javascript .keyword { color: #c586c0 !important; }
.language-javascript .variable { color: #9cdcfe !important; }
.language-javascript .string { color: #ce9178 !important; }
.language-javascript .comment { color: #6a9955 !important; }
.language-javascript .function { color: #dcdcaa !important; }
.language-javascript .number { color: #b5cea8 !important; }
.language-javascript .operator { color: #d4d4d4 !important; }
.language-javascript .class-name { color: #4ec9b0 !important; }

.language-html .tag { color: #569cd6 !important; }
.language-html .attribute { color: #9cdcfe !important; }
.language-html .string { color: #ce9178 !important; }
.language-html .comment { color: #6a9955 !important; }

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* Responsive */
@media (max-width: 768px) {
    .lesson-container {
        padding: 1rem;
    }
    
    .definition-card,
    .comparison-section,
    .demo-container {
        grid-template-columns: 1fr;
    }
    
    .objectives-grid,
    .concepts-grid,
    .benefits-grid {
        grid-template-columns: 1fr;
    }
    
    .lesson-header {
        padding: 2rem 1rem;
    }
    
    .lesson-header h1 {
        font-size: 2rem;
    }
    
    .lesson-duration {
        flex-direction: column;
        align-items: center;
    }
    
    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
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
.lesson-section:nth-child(6) { animation-delay: 0.6s; }
</style>