<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <div class="lesson-header">
        <h1 class="text-white">♿ RGAA - Référentiel Général d'Amélioration de l'Accessibilité</h1>
        <p class="lesson-meta text-white">
          Comprendre et appliquer les standards d'accessibilité numérique en France
        </p>
      </div>

      <!-- Section d'introduction -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4">🎯 Qu'est-ce que le RGAA ?</h2>
        <p class="textExemple">
          Le RGAA est le référentiel officiel français qui définit les règles techniques pour rendre 
          les services numériques accessibles à tous les usagers, notamment les personnes en situation de handicap. 
          Il s'appuie sur les standards internationaux WCAG (Web Content Accessibility Guidelines).
        </p>
        
        <div class="code-comparison mt-4">
          <div class="bg-white p-3 rounded">
            <h4 class="text-purple">📊 Portée légale</h4>
            <ul>
              <li><strong>Obligatoire</strong> pour les services publics</li>
              <li><strong>Recommandé</strong> pour le secteur privé</li>
              <li>Applicable aux sites web, applications mobiles, intranets</li>
              <li>Contrôles réguliers par la DINUM</li>
            </ul>
          </div>
          
          <div class="bg-white p-3 rounded">
            <h4 class="text-purple">🎯 Objectifs</h4>
            <ul>
              <li>Permettre l'accès à l'information pour tous</li>
              <li>Garantir l'égalité des chances</li>
              <li>Améliorer l'expérience utilisateur globale</li>
              <li>Conformer à la législation française</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Section 1 : Les 4 principes fondamentaux -->
      <div class="lesson-section bg-light-purple border-purple">
        <div class="d-flex align-items-center mb-4">
          <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3" style="width: 50px; height: 50px;">
            <span style="font-size: 1.5rem;">1</span>
          </div>
          <h2 class="text-purple mb-0">📐 Les 4 Principes Fondamentaux (POUR)</h2>
        </div>
        
        <p class="textExemple mb-4">
          Le RGAA s'articule autour de 4 principes fondamentaux, résumés par l'acronyme POUR.
          Chaque principe contient des directives et des critères de succès testables.
        </p>
        
        <div class="code-comparison">
          <div class="p-3 bg-gradient-primary text-white rounded">
            <h4 class="text-white mb-3">P - Perceptible</h4>
            <p>L'information doit être présentable de façons différentes pour être perçue par tous les utilisateurs.</p>
            <ul class="mt-2">
              <li>Textes alternatifs pour les images</li>
              <li>Sous-titres pour les vidéos</li>
              <li>Contraste suffisant des couleurs</li>
              <li>Redimensionnable sans perte d'information</li>
            </ul>
          </div>
          
          <div class="p-3 bg-gradient-primary text-white rounded">
            <h4 class="text-white mb-3">O - Utilisable</h4>
            <p>Les composants d'interface doivent être utilisables par tous.</p>
            <ul class="mt-2">
              <li>Navigation au clavier complète</li>
              <li>Temps suffisant pour lire/interagir</li>
              <li>Pas de contenu clignotant dangereux</li>
              <li>Navigation et orientation faciles</li>
            </ul>
          </div>
        </div>
        
        <div class="code-comparison mt-3">
          <div class="p-3 bg-gradient-primary text-white rounded">
            <h4 class="text-white mb-3">U - Compréhensible</h4>
            <p>L'information et l'utilisation doivent être compréhensibles.</p>
            <ul class="mt-2">
              <li>Texte lisible et compréhensible</li>
              <li>Pages qui s'affichent de manière prévisible</li>
              <li>Aide à la saisie pour éviter les erreurs</li>
              <li>Instructions claires et simples</li>
            </ul>
          </div>
          
          <div class="p-3 bg-gradient-primary text-white rounded">
            <h4 class="text-white mb-3">R - Robuste</h4>
            <p>Le contenu doit être interprétable de manière fiable par différentes technologies.</p>
            <ul class="mt-2">
              <li>Compatibilité avec les aides techniques</li>
              <li>Code HTML valide et sémantique</li>
              <li>Support des technologies d'assistance</li>
              <li>Respect des standards du web</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Section 2 : Critères techniques -->
      <div class="lesson-section bg-light-purple border-purple">
        <div class="d-flex align-items-center mb-4">
          <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3" style="width: 50px; height: 50px;">
            <span style="font-size: 1.5rem;">2</span>
          </div>
          <h2 class="text-purple mb-0">🔧 Critères Techniques Essentiels</h2>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple mb-3">🎨 Contraste des couleurs (Critère 3.2)</h4>
          <p class="textExemple mb-3">Le rapport de contraste entre le texte et son arrière-plan doit être suffisant.</p>
          
          <div class="code-comparison">
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">✅ Conforme</h5>
              <div class="d-flex align-items-center justify-content-between p-2 mt-2">
                <div style="background: #2c3e50; color: #ecf0f1; padding: 10px; border-radius: 5px; width: 100%;">
                  <strong>Contraste 8.8:1</strong> - Excellente lisibilité
                </div>
              </div>
              <pre class="mt-2"><code><span class="comment">&lt;!-- Texte sombre sur fond clair --&gt;</span>
&lt;p <span class="variable">style</span>=<span class="string">"color: #2c3e50; background: #ecf0f1;"</span>&gt;
  Texte accessible
&lt;/p&gt;</code></pre>
            </div>
            
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">❌ Non conforme</h5>
              <div class="d-flex align-items-center justify-content-between p-2 mt-2">
                <div style="background: #f39c12; color: #f1c40f; padding: 10px; border-radius: 5px; width: 100%;">
                  <strong>Contraste 1.3:1</strong> - Difficile à lire
                </div>
              </div>
              <pre class="mt-2"><code><span class="comment">&lt;!-- Contraste insuffisant --&gt;</span>
&lt;p <span class="variable">style</span>=<span class="string">"color: #f39c12; background: #f1c40f;"</span>&gt;
  Texte peu lisible
&lt;/p&gt;</code></pre>
            </div>
          </div>
        </div>
        
        <div class="code-example mt-4">
          <h4 class="text-purple mb-3">🏷️ Alternatives textuelles (Critère 1.1)</h4>
          <div class="code-comparison">
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">✅ Bonne pratique</h5>
              <pre><code><span class="comment">&lt;!-- Image informative avec alt descriptif --&gt;</span>
&lt;img <span class="variable">src</span>=<span class="string">"graphique-evolution.png"</span>
     <span class="variable">alt</span>=<span class="string">"Graphique montrant une augmentation de 25% des ventes au premier trimestre 2024"</span>
     <span class="variable">width</span>=<span class="string">"600"</span> <span class="variable">height</span>=<span class="string">"400"</span>&gt;</code></pre>
            </div>
            
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">❌ À éviter</h5>
              <pre><code><span class="comment">&lt;!-- Alternative textuelle insuffisante --&gt;</span>
&lt;img <span class="variable">src</span>=<span class="string">"graphique.png"</span> <span class="variable">alt</span>=<span class="string">"graphique"</span>&gt;
<span class="comment">&lt;!-- Ou pire : --&gt;</span>
&lt;img <span class="variable">src</span>=<span class="string">"photo.jpg"</span> <span class="variable">alt</span>=<span class="string">"image"</span>&gt;</code></pre>
            </div>
          </div>
        </div>
        
        <div class="code-example mt-4">
          <h4 class="text-purple mb-3">⌨️ Navigation au clavier (Critère 7.1)</h4>
          <pre><code><span class="comment">&lt;!-- Structure HTML sémantique --&gt;</span>
&lt;nav <span class="variable">aria-label</span>=<span class="string">"Menu principal"</span>&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a <span class="variable">href</span>=<span class="string">"/"</span> <span class="variable">tabindex</span>=<span class="string">"0"</span>&gt;Accueil&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a <span class="variable">href</span>=<span class="string">"/services"</span>&gt;Services&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/nav&gt;

<span class="comment">&lt;!-- Indicateur de focus visible --&gt;</span>
&lt;style&gt;
  <span class="keyword">a</span>:focus, <span class="keyword">button</span>:focus {
    <span class="variable">outline</span>: <span class="number">3</span>px solid #8B5FBF;
    <span class="variable">outline-offset</span>: <span class="number">2</span>px;
  }
&lt;/style&gt;</code></pre>
        </div>
      </div>

      <!-- Section 3 : Mise en œuvre pratique -->
      <div class="lesson-section bg-light-purple border-purple">
        <div class="d-flex align-items-center mb-4">
          <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3" style="width: 50px; height: 50px;">
            <span style="font-size: 1.5rem;">3</span>
          </div>
          <h2 class="text-purple mb-0">🚀 Mise en Œuvre dans un Projet Web</h2>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple mb-3">📋 Checklist de Démarrage</h4>
          <div class="p-3 bg-white rounded">
            <ul class="mb-3">
              <li><input type="checkbox" checked> Utiliser des balises HTML sémantiques</li>
              <li><input type="checkbox" checked> Ajouter des attributs ARIA quand nécessaire</li>
              <li><input type="checkbox" checked> Vérifier le contraste des couleurs</li>
              <li><input type="checkbox"> Tester la navigation au clavier</li>
              <li><input type="checkbox"> Fournir des alternatives aux médias</li>
              <li><input type="checkbox"> Assurer la compatibilité avec les lecteurs d'écran</li>
            </ul>
          </div>
        </div>
        
        <div class="code-example mt-4">
          <h4 class="text-purple mb-3">🛠️ Outils de Vérification</h4>
          <div class="code-comparison">
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">🔍 Extensions navigateur</h5>
              <ul>
                <li><strong>axe DevTools</strong> - Google Chrome</li>
                <li><strong>Wave Evaluation Tool</strong> - Firefox/Chrome</li>
                <li><strong>ARC Toolkit</strong> - Chrome</li>
                <li><strong>Color Contrast Analyzer</strong> - Chrome</li>
              </ul>
            </div>
            
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">⚡ Outils en ligne</h5>
              <ul>
                <li><strong>ASQ</strong> - outil officiel français</li>
                <li><strong>AChecker</strong> - validation automatique</li>
                <li><strong>WebAIM Color Contrast</strong></li>
                <li><strong>Lighthouse</strong> - Google Chrome</li>
              </ul>
            </div>
          </div>
        </div>
        
        <div class="code-example mt-4">
          <h4 class="text-purple mb-3">💻 Exemple de Composant Accessible (Vue/Nuxt)</h4>
          <pre><code><span class="comment">&lt;!-- Composant de bouton accessible --&gt;</span>
&lt;template&gt;
  &lt;button
    <span class="variable">:class</span>=<span class="string">"['btn-purple', { 'btn-loading': loading }]"</span>
    <span class="variable">:disabled</span>=<span class="string">"disabled || loading"</span>
    <span class="variable">:aria-busy</span>=<span class="string">"loading ? 'true' : 'false'"</span>
    <span class="variable">:aria-label</span>=<span class="string">"ariaLabel || label"</span>
    <span class="variable">@click</span>=<span class="string">"handleClick"</span>
    <span class="variable">@keydown.enter</span>=<span class="string">"handleClick"</span>
    <span class="variable">@keydown.space</span>=<span class="string">"handleClick"</span>
  &gt;
    &lt;span <span class="variable">v-if</span>=<span class="string">"loading"</span> <span class="variable">aria-hidden</span>=<span class="string">"true"</span>&gt;
      &lt;span <span class="variable">class</span>=<span class="string">"spinner"</span>&gt;&lt;/span&gt;
    &lt;/span&gt;
    &lt;span <span class="variable">v-else</span>&gt;
      {{ label }}
    &lt;/span&gt;
  &lt;/button&gt;
&lt;/template&gt;

&lt;script setup&gt;
<span class="keyword">const</span> props = <span class="variable">defineProps</span>({
  label: <span class="keyword">String</span>,
  ariaLabel: <span class="keyword">String</span>,
  disabled: <span class="keyword">Boolean</span>,
  loading: <span class="keyword">Boolean</span>
});

<span class="keyword">const</span> emit = <span class="variable">defineEmits</span>([<span class="string">'click'</span>]);

<span class="keyword">const</span> handleClick = () => {
  <span class="keyword">if</span> (!props.disabled && !props.loading) {
    emit(<span class="string">'click'</span>);
  }
};
&lt;/script&gt;</code></pre>
        </div>
      </div>

      <!-- Section 4 : Conformité et déclaration -->
      <div class="lesson-section bg-light-purple border-purple">
        <div class="d-flex align-items-center mb-4">
          <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3" style="width: 50px; height: 50px;">
            <span style="font-size: 1.5rem;">4</span>
          </div>
          <h2 class="text-purple mb-0">📄 Conformité et Déclaration d'Accessibilité</h2>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple mb-3">📊 Niveaux de Conformité</h4>
          <div class="code-comparison">
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">🥉 Niveau A</h5>
              <p><strong>Obligatoire</strong> - Critères essentiels</p>
              <ul>
                <li>Alternatives textuelles</li>
                <li>Contrôle du temps</li>
                <li>Clavier accessible</li>
                <li>Pas de piège au clavier</li>
              </ul>
            </div>
            
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">🥈 Niveau AA</h5>
              <p><strong>Recommandé</strong> - Amélioration significative</p>
              <ul>
                <li>Contraste 4.5:1 (texte normal)</li>
                <li>Navigation cohérente</li>
                <li>Identification des erreurs</li>
                <li>Sous-titres (vidéos pré-enregistrées)</li>
              </ul>
            </div>
            
            <div class="p-3 bg-white rounded">
              <h5 class="text-purple">🥇 Niveau AAA</h5>
              <p><strong>Excellence</strong> - Accessibilité optimale</p>
              <ul>
                <li>Contraste 7:1 (texte normal)</li>
                <li>Langue des passages complexes</li>
                <li>Pas d'interruption</li>
                <li>Signification par la forme uniquement</li>
              </ul>
            </div>
          </div>
        </div>
        
        <div class="code-example mt-4">
          <h4 class="text-purple mb-3">📝 Déclaration d'Accessibilité Obligatoire</h4>
          <div class="p-3 bg-white rounded">
            <pre><code><span class="comment">&lt;!-- Modèle de déclaration --&gt;</span>
&lt;section <span class="variable">aria-labelledby</span>=<span class="string">"accessibility-statement"</span>&gt;
  &lt;h2 <span class="variable">id</span>=<span class="string">"accessibility-statement"</span>&gt;
    Déclaration d'accessibilité
  &lt;/h2&gt;
  
  &lt;p&gt;
    [Nom de l'organisme] s'engage à rendre son service accessible...
  &lt;/p&gt;
  
  &lt;h3&gt;État de conformité&lt;/h3&gt;
  &lt;p&gt;
    Le site [nom du site] est <strong>partiellement conforme</strong>
    au RGAA 4.1.1 en raison des non-conformités listées ci-dessous.
  &lt;/p&gt;
  
  &lt;h3&gt;Résultats des tests&lt;/h3&gt;
  &lt;ul&gt;
    &lt;li&gt;Date : [JJ/MM/AAAA]&lt;/li&gt;
    &lt;li&gt;Technologie utilisée : [ASQ, etc.]&lt;/li&gt;
    &lt;li&gt;Échantillon testé : [description]&lt;/li&gt;
  &lt;/ul&gt;
&lt;/section&gt;</code></pre>
          </div>
        </div>
        
        <div class="exercise mt-4">
          <h4 class="text-purple">🧪 Exercice pratique : Audit RGAA</h4>
          <p>Analysez une page web existante et identifiez 5 problèmes d'accessibilité.</p>
          <details class="solution">
            <summary class="btn-purple btn-hover">Grille d'analyse suggérée</summary>
            <div class="solution-content">
              <h5>Points à vérifier :</h5>
              <ol>
                <li><strong>Images</strong> : Présence d'attributs alt significatifs</li>
                <li><strong>Liens</strong> : Texte descriptif hors contexte</li>
                <li><strong>Formulaires</strong> : Labels associés aux champs</li>
                <li><strong>Contraste</strong> : Ratio suffisant texte/fond</li>
                <li><strong>Structure</strong> : Hiérarchie des titres (h1-h6)</li>
                <li><strong>Clavier</strong> : Navigation complète sans souris</li>
                <li><strong>Multimédia</strong> : Sous-titres et transcriptions</li>
              </ol>
              <h5>Outils recommandés :</h5>
              <ul>
                <li>Extension Wave pour analyse rapide</li>
                <li>NVDA ou VoiceOver pour test lecteur d'écran</li>
                <li>Tabulation pour navigation clavier</li>
              </ul>
            </div>
          </details>
        </div>
      </div>

      <!-- Section résumé -->
      <div class="lesson-section bg-gradient-primary text-white">
        <h2 class="mb-4">📊 Bénéfices de l'Accessibilité</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-white">👥 Pour les utilisateurs</h4>
            <ul class="mt-3">
              <li>Autonomie des personnes handicapées</li>
              <li>Meilleure expérience sur mobile</li>
              <li>Lisibilité améliorée pour tous</li>
              <li>Navigation simplifiée</li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-white">🏢 Pour les organisations</h4>
            <ul class="mt-3">
              <li>Conformité légale</li>
              <li>Public élargi</li>
              <li>SEO amélioré</li>
              <li>Code de meilleure qualité</li>
              <li>Réduction des coûts de support</li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-white">💻 Pour les développeurs</h4>
            <ul class="mt-3">
              <li>Code plus maintenable</li>
              <li>Meilleure structure HTML</li>
              <li>Compatibilité améliorée</li>
              <li>Compétences valorisées</li>
            </ul>
          </div>
        </div>
        
        <div class="mt-4">
          <h4 class="text-white">🚀 Ressources Utiles</h4>
          <div class="d-flex flex-wrap gap-2 mt-3">
            <a href="https://www.numerique.gouv.fr/publications/rgaa-accessibilite/" target="_blank" class="btn-purple btn-hover">RGAA Officiel</a>
            <a href="https://www.w3.org/Translations/WCAG21-fr/" target="_blank" class="btn-purple btn-hover">WCAG FR</a>
            <a href="https://developer.mozilla.org/fr/docs/Web/Accessibility" target="_blank" class="btn-purple btn-hover">MDN Accessibilité</a>
            <a href="https://www.accede-web.com/" target="_blank" class="btn-purple btn-hover">Accede-Web</a>
          </div>
        </div>
      </div>

      <!-- Navigation -->
      <div class="d-flex justify-content-between mt-4">
        <a href="#" class="btn-purple btn-hover">← Leçon précédente</a>
        <a href="#" class="btn-purple btn-hover">Leçon suivante →</a>
      </div>
    </div>
  </div>
</template>

<script setup>
// Vous pouvez ajouter ici des variables réactives si nécessaire
const pageTitle = "RGAA - Référentiel Général d'Amélioration de l'Accessibilité";

// Met à jour le titre de la page
useHead({
  title: pageTitle
});
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

/* Styles additionnels pour cette page spécifique */
.mb-0 { margin-bottom: 0 !important; }
.mb-2 { margin-bottom: 0.5rem !important; }
.mb-3 { margin-bottom: 1rem !important; }
.mb-4 { margin-bottom: 1.5rem !important; }
.mt-2 { margin-top: 0.5rem !important; }
.mt-3 { margin-top: 1rem !important; }
.mt-4 { margin-top: 1.5rem !important; }
.me-3 { margin-right: 1rem !important; }
.d-flex { display: flex !important; }
.align-items-center { align-items: center !important; }
.justify-content-center { justify-content: center !important; }
.justify-content-between { justify-content: space-between !important; }
.justify-content-between { justify-content: space-between !important; }
.rounded-circle { border-radius: 50% !important; }
.rounded { border-radius: 8px !important; }
.flex-wrap { flex-wrap: wrap !important; }
.gap-2 { gap: 0.5rem !important; }
.p-3 { padding: 1rem !important; }
.bg-white { background-color: white !important; }

/* Style pour les listes dans les sections colorées */
.text-white ul, .text-white ol {
  color: white;
}

.text-white li {
  margin-bottom: 0.5rem;
}

/* Style pour les checkboxes dans la checklist */
input[type="checkbox"] {
  margin-right: 10px;
  transform: scale(1.2);
}

/* Style pour les démos de contraste */
.contrast-demo {
  padding: 15px;
  border-radius: 5px;
  margin: 10px 0;
}

/* Animation pour le spinner */
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.spinner {
  display: inline-block;
  width: 16px;
  height: 16px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: white;
  animation: spin 1s ease-in-out infinite;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .code-comparison {
    grid-template-columns: 1fr;
  }
  
  .d-flex.flex-wrap {
    justify-content: center;
  }
}
</style>