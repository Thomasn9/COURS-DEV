<template>
  <div class="lesson-container">
    <div class="lesson-content">

      <!-- En-tête -->
      <header class="lesson-header">
        <h1 class="text-white">Polices Google Fonts dans Symfony</h1>
        <p class="lesson-meta text-white">Google Fonts • Typographie • Intégration • Bonnes pratiques</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi utiliser Google Fonts ?</h2>
        <p class="text-example">
          Google Fonts est une bibliothèque gratuite de plus de 1 500 polices, optimisées pour le web.
          L'intégration est simple, rapide et ne nécessite aucun téléchargement ni hébergement local.
          Elle permet d'améliorer l'identité visuelle d'un projet Symfony sans alourdir le code.
        </p>
        <p class="text-example">
          Dans cette leçon, nous allons voir comment importer une police Google Fonts, l'appliquer
          globalement ou sur des éléments spécifiques, et respecter les bonnes pratiques de performance.
        </p>
      </section>

      <!-- Étape 1 : Choisir la police -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">1. Choisir une police sur Google Fonts</h2>
        <p class="text-example">
          Rendez-vous sur <a href="https://fonts.google.com" target="_blank" class="text-purple">fonts.google.com</a>.
          Parcourez les polices, filtrez par catégorie (sans-serif, serif, etc.) ou par langue.
        </p>
        <div class="text-example">
          <h3 class="text-purple">Sélectionner les styles et graisses</h3>
          <p>
            Cliquez sur une police qui vous plaît, puis sur <strong>"Get font"</strong>. Une fenêtre s'ouvre :
            vous pouvez choisir les graisses (weights) et les styles (italique) dont vous avez besoin.
          </p>
          <ul>
            <li><strong>Recommandation</strong> : limitez-vous à 3-4 graisses (ex: 400, 500, 700) pour ne pas ralentir le chargement.</li>
            <li><strong>Style italique</strong> : ne le prenez que si vous en avez vraiment besoin.</li>
          </ul>
        </div>
        <div class="text-example">
          <h3 class="text-purple">Exemple : la police "Inter"</h3>
          <p>Nous allons utiliser la police <strong>Inter</strong> avec les graisses 400, 500 et 700.</p>
        </div>
      </section>

      <!-- Étape 2 : Obtenir le code d'intégration -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">2. Obtenir le code d'intégration</h2>
        <p class="text-example">
          Après avoir sélectionné les graisses, Google Fonts génère un code à insérer dans le &lt;head&gt; de vos pages.
          Deux méthodes sont proposées : la balise &lt;link&gt; et la règle CSS <code>@import</code>.
        </p>

        <div class="text-example">
          <h3 class="text-purple">Méthode recommandée : la balise link</h3>
          <div class="code-example">
            <pre v-pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&amp;display=swap" rel="stylesheet"&gt;</code></pre>
          </div>
          <p>
            Cette méthode est préférable car elle permet au navigateur de découvrir la ressource plus tôt
            et de la charger en parallèle d'autres feuilles de style.
          </p>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Méthode alternative : @import dans le CSS</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&amp;display=swap');</code></pre>
          </div>
          <p>
            Cette méthode est déconseillée car elle bloque le rendu : le navigateur doit télécharger le CSS,
            puis l'importer avant d'afficher la page.
          </p>
        </div>
      </section>

      <!-- Étape 3 : Intégration dans Symfony (Twig) -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">3. Intégration dans un projet Symfony (Twig)</h2>
        <p class="text-example">
          Dans Symfony, on utilise le template <code>base.html.twig</code> pour définir le code commun à toutes les pages.
          Placez la balise &lt;link&gt; dans la section &lt;head&gt;.
        </p>
        <div class="code-example">
          <pre v-pre><code class="language-twig">{# templates/base.html.twig #}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;{% block title %}Mon Projet Symfony{% endblock %}&lt;/title&gt;
    
    &lt;link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&amp;display=swap" rel="stylesheet"&gt;

    {% block stylesheets %}
        {{ parent() }}
    {% endblock %}
&lt;/head&gt;
&lt;body&gt;
    {% block body %}{% endblock %}
&lt;/body&gt;
&lt;/html&gt;</code></pre>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Optimisation avec preconnect</h3>
          <p>
            Pour accélérer le chargement, ajoutez les balises <code>preconnect</code> juste avant le lien Google Fonts.
            Elles établissent une connexion anticipée avec les serveurs Google.
          </p>
          <div class="code-example">
            <pre v-pre><code class="language-twig">&lt;link rel="preconnect" href="https://fonts.googleapis.com"&gt;
&lt;link rel="preconnect" href="https://fonts.gstatic.com" crossorigin&gt;
&lt;link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&amp;display=swap" rel="stylesheet"&gt;</code></pre>
          </div>
        </div>
      </section>

      <!-- Étape 4 : Appliquer la police en CSS -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">4. Appliquer la police aux éléments HTML</h2>
        <p class="text-example">
          Une fois la police importée, il faut l'utiliser dans vos feuilles de style CSS (ou SCSS).
        </p>

        <div class="text-example">
          <h3 class="text-purple">Application globale (toute la page)</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">/* assets/styles/app.css */
body {
    font-family: 'Inter', sans-serif;
}</code></pre>
          </div>
          <p>
            La propriété <code>font-family</code> accepte une liste de polices. La première disponible sera utilisée.
            On ajoute <code>sans-serif</code> comme police de secours système.
          </p>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Application spécifique à certaines balises</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">/* Titres avec une graisse plus forte */
h1, h2, h3 {
    font-family: 'Inter', sans-serif;
    font-weight: 700;
}

/* Paragraphes avec graisse normale */
p {
    font-family: 'Inter', sans-serif;
    font-weight: 400;
}

/* Éléments de navigation */
nav a {
    font-family: 'Inter', sans-serif;
    font-weight: 500;
}</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Utilisation de classes utilitaires</h3>
          <p>Vous pouvez créer des classes réutilisables pour ne pas répéter la propriété <code>font-family</code>.</p>
          <div class="code-example">
            <pre v-pre><code class="language-css">.font-inter {
    font-family: 'Inter', sans-serif;
}
.font-light {
    font-weight: 400;
}
.font-regular {
    font-weight: 500;
}
.font-bold {
    font-weight: 700;
}</code></pre>
          </div>
          <div class="code-example">
            <pre v-pre><code class="language-html">&lt;h1 class="font-inter font-bold"&gt;Titre important&lt;/h1&gt;
&lt;p class="font-inter font-light"&gt;Un paragraphe normal.&lt;/p&gt;</code></pre>
          </div>
        </div>
      </section>

      <!-- Étape 5 : Cas des balises spécifiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">5. Exemples par type d'élément</h2>

        <div class="text-example">
          <h3 class="text-purple">En-têtes (h1 à h6)</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">h1 { font-size: 2.5rem; font-weight: 700; letter-spacing: -0.02em; }
h2 { font-size: 2rem; font-weight: 600; }
h3 { font-size: 1.5rem; font-weight: 500; }</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Paragraphes et texte courant</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">p {
    font-size: 1rem;
    line-height: 1.6;
    font-weight: 400;
}</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Liens et boutons</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">a, button {
    font-family: 'Inter', sans-serif;
    font-weight: 500;
    text-decoration: none;
}
a:hover {
    text-decoration: underline;
}</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">Navigation et menus</h3>
          <div class="code-example">
            <pre v-pre><code class="language-css">.nav-item {
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.05em;
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Bonnes pratiques avancées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques et optimisation</h2>

        <div class="text-example">
          <h3 class="text-purple">A. Utiliser la propriété <code>font-display: swap</code></h3>
          <p>
            Le paramètre <code>display=swap</code> dans l'URL Google Fonts garantit que le texte s'affiche immédiatement
            avec une police de secours, puis est remplacé lorsque la police personnalisée est chargée.
            Cela évite le "Flash of Invisible Text" (FOIT).
          </p>
          <div class="code-example">
            <pre v-pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css2?family=Inter:wght@400&amp;display=swap" rel="stylesheet"&gt;</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">B. Limiter les jeux de caractères (subset)</h3>
          <p>
            Par défaut, Google Fonts inclut tous les caractères. Vous pouvez limiter au jeu <code>latin</code> pour réduire le poids.
          </p>
          <div class="code-example">
            <pre v-pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css2?family=Inter:wght@400&amp;display=swap&amp;subset=latin" rel="stylesheet"&gt;</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">C. Police de secours (fallback) système</h3>
          <p>
            Toujours spécifier une ou plusieurs polices de secours pour les navigateurs qui ne chargent pas
            la police distante (ex: <code>sans-serif</code>, <code>Arial</code>, <code>Helvetica</code>).
          </p>
          <div class="code-example">
            <pre v-pre><code class="language-css">body {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}</code></pre>
          </div>
        </div>

        <div class="text-example">
          <h3 class="text-purple">D. Éviter le CLS (Cumulative Layout Shift)</h3>
          <p>
            L'utilisation de <code>font-display: swap</code> peut causer un léger décalage lors du remplacement de la police.
            Pour minimiser ce phénomène, réservez l'espace nécessaire avec <code>size-adjust</code> ou utilisez
            des polices de secours aux dimensions similaires (ex: <code>Arial</code> pour <code>Inter</code>).
          </p>
        </div>
      </section>

      <!-- Intégration avec AssetMapper (optionnel) -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Intégration via AssetMapper (approche moderne)</h2>
        <p class="text-example">
          Si vous utilisez AssetMapper (recommandé pour Symfony 6.3+), vous pouvez importer la police directement
          dans votre fichier CSS principal.
        </p>
        <div class="code-example">
          <pre v-pre><code class="language-css">/* assets/styles/app.css */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&amp;display=swap');

body {
    font-family: 'Inter', sans-serif;
}</code></pre>
        </div>
        <p class="text-example">
          Puis dans <code>base.html.twig</code>, il suffit d'inclure la feuille de style via AssetMapper :
        </p>
        <div class="code-example">
          <pre v-pre><code class="language-twig">{% block stylesheets %}
    {{ importmap('app') }}
{% endblock %}</code></pre>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="text-example">
          L'intégration de Google Fonts dans Symfony est un jeu d'enfant. Les étapes clés à retenir :
        </p>
        <ul>
          <li>Choisir la police et ses graisses sur Google Fonts.</li>
          <li>Insérer la balise <code>&lt;link&gt;</code> (avec <code>preconnect</code>) dans <code>head</code> de <code>base.html.twig</code>.</li>
          <li>Appliquer la police en CSS via <code>font-family</code> sur les sélecteurs souhaités.</li>
          <li>Respecter les bonnes pratiques : <code>display=swap</code>, fallback système, sous-ensembles.</li>
        </ul>
        <p class="text-example">
          Vous pouvez maintenant personnaliser la typographie de votre projet Symfony pour lui donner une identité unique.
          Dans les prochaines leçons, nous verrons comment héberger vos propres polices localement pour le RGPD
          et comment optimiser les performances avec le préchargement.
        </p>
      </section>

    </div>
  </div>
</template>

<script>
export default {
  name: 'GoogleFontsLesson',

  mounted() {
    this.$nextTick(() => {
      this.loadHighlightJS().then(() => {
        this.highlightCodeBlocks()
      }).catch(err => {
        console.warn('Highlight.js loading failed:', err)
      })
    })
  },

  methods: {
    loadHighlightJS() {
      return new Promise((resolve, reject) => {
        if (window.hljs && window.hljs.getLanguage) {
          resolve()
          return
        }

        if (document.querySelector('script[data-highlight-loader]')) {
          const checkInterval = setInterval(() => {
            if (window.hljs && window.hljs.getLanguage) {
              clearInterval(checkInterval)
              resolve()
            }
          }, 50)
          return
        }

        if (!document.querySelector('link[href*="highlight.js/11.9.0/styles/vs2015"]')) {
          const link = document.createElement('link')
          link.rel = 'stylesheet'
          link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css'
          document.head.appendChild(link)
        }

        const mainScript = document.createElement('script')
        mainScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js'
        mainScript.setAttribute('data-highlight-loader', 'true')

        mainScript.onload = () => {
          const languages = ['css', 'twig', 'html', 'bash', 'javascript', 'plaintext']
          let loaded = 0
          let hasError = false

          if (languages.length === 0) {
            resolve()
            return
          }

          languages.forEach(lang => {
            const langScript = document.createElement('script')
            langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`
            langScript.onload = () => {
              loaded++
              if (loaded === languages.length && !hasError) resolve()
            }
            langScript.onerror = () => {
              hasError = true
              reject(new Error(`Failed to load language: ${lang}`))
            }
            document.head.appendChild(langScript)
          })
        }

        mainScript.onerror = () => reject(new Error('Failed to load highlight.js core'))
        document.head.appendChild(mainScript)
      })
    },

    highlightCodeBlocks() {
      if (!window.hljs) return
      const blocks = this.$el.querySelectorAll('pre code')
      blocks.forEach((block) => {
        if (!block.dataset.highlighted) {
          window.hljs.highlightElement(block)
          block.dataset.highlighted = 'true'
        }
      })
    },
  },
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

.bg-light-purple {
  background-color: #f8f6ff;
}

.border-purple {
  border: 2px solid #e0d6ff;
  transition: all 0.3s ease;
}

.text-purple {
  color: #6A3093 !important;
}

.text-white {
  color: white !important;
}

.text-example {
  margin-bottom: 1rem;
  line-height: 1.6;
}

.code-example {
  margin: 1.5rem 0;
  width: 100%;
  box-sizing: border-box;
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
  pre {
    padding: 1rem !important;
    font-size: 0.85rem;
  }
}

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
</style>