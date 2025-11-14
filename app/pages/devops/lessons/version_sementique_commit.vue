<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Versions Sémantiques des Commits</h1>
        <p class="lesson-meta text-white">Apprenez à structurer vos messages de commit pour un historique clair et professionnel</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p>Les commits sémantiques sont une convention de nommage qui permet de donner plus de sens et de structure à vos messages de commit. Cette pratique améliore la lisibilité de l'historique Git et facilite la génération automatique des notes de version.</p>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de commit sémantique</h3>
          <pre><code>feat: ajouter la fonctionnalité de recherche avancée</code></pre>
        </div>
      </section>

      <!-- Pourquoi utiliser les commits sémantiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi utiliser les commits sémantiques ?</h2>
        <ul>
          <li><strong>Historique clair :</strong> Comprendre rapidement l'évolution du projet</li>
          <li><strong>Automatisation :</strong> Génération automatique des changelogs</li>
          <li><strong>Collaboration :</strong> Meilleure communication entre développeurs</li>
          <li><strong>Versioning :</strong> Détermination plus facile du versioning sémantique</li>
        </ul>
      </section>

      <!-- Structure d'un commit sémantique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Structure d'un commit sémantique</h2>
        <p>Un commit sémantique suit généralement ce format :</p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;type&gt;</span>[<span class="variable">scope optionnel</span>]: <span class="string">&lt;description&gt;</span>

[<span class="comment">corps optionnel</span>]

[<span class="comment">pied de page optionnel</span>]</code></pre>
        </div>
        
        <h3 class="text-purple">Composants principaux</h3>
        <ul>
          <li><strong>Type :</strong> Indique la nature du changement (feat, fix, docs, etc.)</li>
          <li><strong>Scope (optionnel) :</strong> Précise la partie de l'application concernée</li>
          <li><strong>Description :</strong> Brève description du changement</li>
          <li><strong>Corps (optionnel) :</strong> Explications détaillées si nécessaire</li>
          <li><strong>Pied de page (optionnel) :</strong> Références aux issues, breaking changes</li>
        </ul>
      </section>

      <!-- Types de commits -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de commits conventionnels</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Types principaux</h3>
            <ul>
              <li><strong>feat :</strong> Nouvelle fonctionnalité</li>
              <li><strong>fix :</strong> Correction de bug</li>
              <li><strong>docs :</strong> Modification de la documentation</li>
              <li><strong>style :</strong> Changements qui n'affectent pas le sens du code</li>
              <li><strong>refactor :</strong> Restructuration du code sans changer le comportement</li>
              <li><strong>perf :</strong> Amélioration des performances</li>
              <li><strong>test :</strong> Ajout ou modification de tests</li>
              <li><strong>build :</strong> Changements liés au système de build</li>
              <li><strong>ci :</strong> Changements liés à l'intégration continue</li>
              <li><strong>chore :</strong> Tâches de maintenance diverses</li>
              <li><strong>revert :</strong> Annulation d'un commit précédent</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Exemples</h3>
            <div class="code-example">
              <pre><code><span class="function">feat</span>(auth): ajouter l'authentification OAuth2</code></pre>
              <pre><code><span class="function">fix</span>(api): corriger la fuite mémoire dans l'endpoint users</code></pre>
              <pre><code><span class="function">docs</span>: mettre à jour le README avec les nouvelles instructions</code></pre>
              <pre><code><span class="function">style</span>: formater le code avec Prettier</code></pre>
              <pre><code><span class="function">refactor</span>(database): optimiser les requêtes SQL</code></pre>
            </div>
          </div>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques</h2>
        
        <h3 class="text-purple">Règles de rédaction</h3>
        <ul>
          <li>Utilisez l'impératif ("ajouter" pas "ajouté")</li>
          <li>Ne mettez pas de majuscule en début de phrase</li>
          <li>Ne terminez pas par un point</li>
          <li>Limitez la ligne de sujet à 50 caractères</li>
          <li>Séparez le corps du sujet par une ligne vide</li>
          <li>Limitez les lignes du corps à 72 caractères</li>
        </ul>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">À faire</h3>
            <div class="code-example">
              <pre><code><span class="function">feat</span>: implémenter le système de cache</code></pre>
              <pre><code><span class="function">fix</span>(ui): résoudre le problème d'alignement mobile</code></pre>
            </div>
          </div>
          
          <div>
            <h3 class="text-purple">À éviter</h3>
            <div class="code-example">
              <pre><code><span class="comment"># Mauvais - verbe à l'infinitif</span>
feat: implémentation du système de cache</code></pre>
              <pre><code><span class="comment"># Mauvais - trop long</span>
feat: ajouter un nouveau système de cache pour améliorer les performances de l'application</code></pre>
            </div>
          </div>
        </div>
      </section>

      <!-- Commit conventionnel complet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple de commit conventionnel complet</h2>
        
        <div class="code-example">
          <pre><code><span class="function">feat</span>(api): ajouter l'endpoint pour les statistiques utilisateurs

Ajouter un nouvel endpoint GET /api/users/stats qui renvoie:
- Nombre total d'utilisateurs
- Nombre d'utilisateurs actifs
- Répartition par pays

L'endpoint nécessite une authentification admin.

<span class="comment">Closes #123</span>
<span class="comment">BREAKING CHANGE: L'endpoint /api/stats est maintenant déprécié</span></code></pre>
        </div>
        
        <p class="textExemple">Ce commit montre comment structurer un message complet avec toutes les sections optionnelles.</p>
      </section>

      <!-- Outils et intégrations -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils et intégrations</h2>
        
        <h3 class="text-purple">Validation des commits</h3>
        <p>Plusieurs outils peuvent vous aider à valider la conformité de vos commits :</p>
        
        <ul>
          <li><strong>commitlint :</strong> Linter pour les messages de commit</li>
          <li><strong>husky :</strong> Hooks Git pour automatiser les vérifications</li>
          <li><strong>commitizen :</strong> Interface en ligne de commande pour créer des commits conventionnels</li>
          <li><strong>semantic-release :</strong> Automatisation du versioning et publication</li>
        </ul>
        
        <div class="code-example">
          <h3 class="text-purple">Configuration commitlint</h3>
          <pre><code><span class="comment">// .commitlintrc.js</span>
<span class="keyword">module</span>.<span class="variable">exports</span> = {
  <span class="variable">extends</span>: [<span class="string">'@commitlint/config-conventional'</span>]
};</code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <p>Transformez ces messages de commit non conventionnels en commits sémantiques :</p>
          
          <ol>
            <li>"J'ai ajouté un nouveau bouton dans le header"</li>
            <li>"J'ai réparé le bug sur la page de connexion"</li>
            <li>"Mise à jour de la documentation API"</li>
            <li>"Optimisation des images pour le chargement plus rapide"</li>
            <li>"Refonte du système de notifications"</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir les solutions</summary>
            <div class="solution-content">
              <h4>Solutions suggérées :</h4>
              <ol>
                <li><code>feat(ui): ajouter un bouton dans le header</code></li>
                <li><code>fix(auth): corriger le bug sur la page de connexion</code></li>
                <li><code>docs(api): mettre à jour la documentation</code></li>
                <li><code>perf(assets): optimiser le chargement des images</code></li>
                <li><code>refactor(notifications): refondre le système de notifications</code></li>
              </ol>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <p class="text-white">L'adoption des commits sémantiques demande un peu d'effort au début, mais les bénéfices à long terme sont considérables. Votre historique Git devient plus lisible, la collaboration est facilitée, et l'automatisation des releases devient possible.</p>
        
        <div class="textExemple text-white">
          <p><strong>Prochaines étapes :</strong></p>
          <ul>
            <li>Implémenter commitlint dans votre projet</li>
            <li>Configurer des hooks Git avec Husky</li>
            <li>Étudier semantic-release pour l'automatisation</li>
          </ul>
        </div>
        
        <a href="#" class="btn-purple btn-hover">Retour à l'accueil</a>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SemanticCommitsLesson',
  // Si vous utilisez Nuxt Content ou d'autres fonctionnalités spécifiques,
  // vous pouvez ajouter la logique ici
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