<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Audit de Code dans la Gestion de Projet</h1>
        <p class="lesson-meta text-white">Gestion de projet • Qualité du code • Bonnes pratiques</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux audits de code</h2>
        <p class="textExemple">
          L'audit de code est un processus systématique d'examen du code source d'une application 
          pour identifier les problèmes de qualité, de sécurité et de maintenabilité. Dans le contexte 
          de la gestion de projet, il s'agit d'un outil essentiel pour garantir la qualité du produit 
          final et réduire les risques techniques.
        </p>
        <p class="textExemple">
          Un audit de code bien mené permet de détecter précocement les défauts, d'améliorer 
          la cohérence du code et de faciliter la maintenance future du projet.
        </p>
      </section>

      <!-- Objectifs d'un audit de code -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'un audit de code</h2>
        <ul>
          <li><strong>Identifier les vulnérabilités de sécurité</strong> : Détecter les failles potentielles avant la mise en production</li>
          <li><strong>Améliorer la qualité du code</strong> : Vérifier la conformité aux standards et bonnes pratiques</li>
          <li><strong>Faciliter la maintenance</strong> : S'assurer que le code est compréhensible et modifiable</li>
          <li><strong>Optimiser les performances</strong> : Repérer les goulots d'étranglement et les inefficacités</li>
          <li><strong>Partager les connaissances</strong> : Favoriser l'apprentissage collectif au sein de l'équipe</li>
        </ul>
      </section>

      <!-- Types d'audits de code -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types d'audits de code</h2>
        
        <h3 class="text-purple">1. Audit manuel</h3>
        <p class="textExemple">
          Révision du code par des développeurs expérimentés qui examinent le code ligne par ligne.
        </p>
        
        <h3 class="text-purple">2. Audit automatisé</h3>
        <p class="textExemple">
          Utilisation d'outils spécialisés pour analyser le code selon des règles prédéfinies.
        </p>
        
        <h3 class="text-purple">3. Audit hybride</h3>
        <p class="textExemple">
          Combinaison des approches manuelles et automatisées pour un audit plus complet.
        </p>
      </section>

      <!-- Processus d'audit de code -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Processus d'audit de code</h2>
        
        <div class="process-step">
          <h3 class="text-purple">1. Préparation</h3>
          <p class="textExemple">
            Définir les objectifs, le périmètre et les critères d'évaluation. Sélectionner 
            les outils et constituer l'équipe d'audit.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">2. Collecte et analyse</h3>
          <p class="textExemple">
            Examiner le code source, exécuter les outils d'analyse automatique et documenter 
            les observations.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">3. Évaluation et rapport</h3>
          <p class="textExemple">
            Classifier les problèmes identifiés par niveau de criticité et rédiger un rapport 
            détaillé avec des recommandations.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">4. Suivi et amélioration</h3>
          <p class="textExemple">
            Planifier la correction des problèmes identifiés et mettre en place des actions 
            préventives pour l'avenir.
          </p>
        </div>
      </section>

      <!-- Audit de Dépendances API -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Audit de Dépendances API</h2>
        
        <p class="textExemple">
          L'audit des dépendances API est crucial dans les applications modernes qui reposent 
          sur de nombreuses bibliothèques externes et services tiers. Cet audit vise à garantir 
          la sécurité, la performance et la maintenabilité des dépendances utilisées.
        </p>

        <h3 class="text-purple">Pourquoi auditer les dépendances API ?</h3>
        <ul>
          <li><strong>Sécurité</strong> : Détecter les vulnérabilités connues dans les dépendances</li>
          <li><strong>Compatibilité</strong> : Vérifier la compatibilité entre les différentes versions</li>
          <li><strong>Performance</strong> : Identifier les dépendances lourdes ou obsolètes</li>
          <li><strong>Licences</strong> : S'assurer de la conformité des licences logicielles</li>
          <li><strong>Maintenance</strong> : Éviter les dépendances abandonnées ou non maintenues</li>
        </ul>

        <h3 class="text-purple">Méthodologie d'audit des dépendances</h3>
        
        <div class="process-step">
          <h4 class="text-purple">1. Inventaire des dépendances</h4>
          <p class="textExemple">
            Lister toutes les dépendances directes et transitives de votre projet. 
            Utiliser des outils comme <code>npm ls</code>, <code>yarn list</code>, ou <code>pipdeptree</code>.
          </p>
        </div>

        <div class="process-step">
          <h4 class="text-purple">2. Analyse de sécurité</h4>
          <p class="textExemple">
            Scanner les dépendances pour détecter les vulnérabilités connues (CVE) 
            en utilisant des bases de données comme NVD, Snyk, ou GitHub Security Advisories.
          </p>
        </div>

        <div class="process-step">
          <h4 class="text-purple">3. Vérification des licences</h4>
          <p class="textExemple">
            Analyser la conformité des licences logicielles avec les exigences de votre organisation 
            et identifier les conflits potentiels.
          </p>
        </div>

        <div class="process-step">
          <h4 class="text-purple">4. Évaluation de la qualité</h4>
          <p class="textExemple">
            Examiner la santé des projets dépendants (fréquence des mises à jour, 
            communauté active, documentation, etc.).
          </p>
        </div>

        <h3 class="text-purple">Outils d'audit de dépendances</h3>
        
        <div class="tools-grid">
          <div class="tool-item">
            <h4 class="text-purple">Sécurité</h4>
            <ul>
              <li><strong>npm audit</strong> : Scanner natif pour les projets Node.js</li>
              <li><strong>OWASP Dependency Check</strong> : Outil open-source multi-langages</li>
              <li><strong>Snyk</strong> : Plateforme complète de sécurité des dépendances</li>
              <li><strong>GitHub Dependabot</strong> : Intégré à GitHub, détection automatique</li>
            </ul>
          </div>

          <div class="tool-item">
            <h4 class="text-purple">Licences</h4>
            <ul>
              <li><strong>Licensee</strong> : Détection des licences open-source</li>
              <li><strong>FOSSA</strong> : Gestion des conformités et licences</li>
              <li><strong>WhiteSource</strong> : Analyse complète des licences</li>
            </ul>
          </div>

          <div class="tool-item">
            <h4 class="text-purple">Qualité</h4>
            <ul>
              <li><strong>BundlePhobia</strong> : Analyse de taille des packages JavaScript</li>
              <li><strong>npm trends</strong> : Comparaison de popularité des packages</li>
              <li><strong>Libraries.io</strong> : Métriques de santé des projets open-source</li>
            </ul>
          </div>
        </div>

        <h3 class="text-purple">Bonnes pratiques</h3>
        
        <div class="best-practices">
          <div class="practice-item">
            <h4 class="text-purple">🔒 Sécurisation du Supply Chain</h4>
            <p>Utiliser des registres privés, signer les commits, et vérifier les intégrités des packages.</p>
          </div>

          <div class="practice-item">
            <h4 class="text-purple">📦 Gestion des versions</h4>
            <p>Épingler les versions exactes, utiliser les lockfiles, et mettre à jour régulièrement.</p>
          </div>

          <div class="practice-item">
            <h4 class="text-purple">🛡️ Intégration continue</h4>
            <p>Intégrer l'audit des dépendances dans la pipeline CI/CD pour une détection précoce.</p>
          </div>

          <div class="practice-item">
            <h4 class="text-purple">📊 Monitoring continu</h4>
            <p>Mettre en place un monitoring actif des nouvelles vulnérabilités.</p>
          </div>
        </div>

        <h3 class="text-purple">Exemple de configuration d'audit</h3>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">package.json non sécurisé</h4>
            <pre><code>{
  <span class="string">"dependencies"</span>: {
    <span class="string">"express"</span>: <span class="string">"*"</span>,
    <span class="string">"lodash"</span>: <span class="string">"^4.0.0"</span>,
    <span class="string">"vulnerable-package"</span>: <span class="string">"1.0.0"</span>
  },
  <span class="string">"scripts"</span>: {
    <span class="string">"start"</span>: <span class="string">"node app.js"</span>
  }
}</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">package.json sécurisé</h4>
            <pre><code>{
  <span class="string">"dependencies"</span>: {
    <span class="string">"express"</span>: <span class="string">"4.18.2"</span>,
    <span class="string">"lodash"</span>: <span class="string">"4.17.21"</span>
  },
  <span class="string">"devDependencies"</span>: {
    <span class="string">"npm-audit-resolver"</span>: <span class="string">"^3.0.0"</span>
  },
  <span class="string">"scripts"</span>: {
    <span class="string">"start"</span>: <span class="string">"node app.js"</span>,
    <span class="string">"audit"</span>: <span class="string">"npm audit"</span>,
    <span class="string">"audit:fix"</span>: <span class="string">"npm audit fix"</span>,
    <span class="string">"security-check"</span>: <span class="string">"npx audit-ci --moderate"</span>
  }
}</code></pre>
          </div>
        </div>

        <h3 class="text-purple">Workflow d'audit automatisé</h3>
        
        <div class="workflow-steps">
          <div class="workflow-step">
            <div class="step-number">1</div>
            <div class="step-content">
              <h4 class="text-purple">Détection automatique</h4>
              <p>Intégration dans la pipeline CI/CD avec des outils comme Dependabot ou Snyk</p>
            </div>
          </div>

          <div class="workflow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <h4 class="text-purple">Analyse des rapports</h4>
              <p>Examen quotidien des alertes de sécurité et classification par criticité</p>
            </div>
          </div>

          <div class="workflow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <h4 class="text-purple">Correction priorisée</h4>
              <p>Planification des mises à jour en fonction de la criticité des vulnérabilités</p>
            </div>
          </div>

          <div class="workflow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <h4 class="text-purple">Validation et déploiement</h4>
              <p>Tests complets après mise à jour et déploiement sécurisé</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Degrés de gravité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Degrés de gravité des problèmes identifiés</h2>
        
        <div class="severity-grid">
          <div class="severity-item severity-critical">
            <h4 class="text-white">CRITIQUE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Bloquant pour le projet</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Vulnérabilités de sécurité critiques</li>
                <li>Fonctionnalités principales non opérationnelles</li>
                <li>Problèmes empêchant le déploiement</li>
                <li>Fuites de données sensibles</li>
              </ul>
              <p><strong>Action :</strong> Correction immédiate requise</p>
            </div>
          </div>
          
          <div class="severity-item severity-high">
            <h4 class="text-white">ÉLEVÉE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Impact significatif sur la qualité</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Problèmes de performance majeurs</li>
                <li>Architecture non scalable</li>
                <li>Absence de tests critiques</li>
                <li>Mauvaises pratiques de sécurité</li>
              </ul>
              <p><strong>Action :</strong> Correction à planifier rapidement</p>
            </div>
          </div>
          
          <div class="severity-item severity-medium">
            <h4 class="text-white">MOYENNE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Impact sur la maintenabilité</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Code dupliqué</li>
                <li>Complexité cyclomatique élevée</li>
                <li>Documentation insuffisante</li>
                <li>Violations des conventions de code</li>
              </ul>
              <p><strong>Action :</strong> Correction à moyen terme</p>
            </div>
          </div>
          
          <div class="severity-item severity-low">
            <h4 class="text-white">FAIBLE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Impact mineur sur la qualité</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Formatage incohérent</li>
                <li>Commentaires manquants non essentiels</li>
                <li>Nommage peu explicite</li>
                <li>Problèmes cosmétiques</li>
              </ul>
              <p><strong>Action :</strong> Correction optionnelle</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Outils d'audit de code -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils d'audit de code</h2>
        
        <h3 class="text-purple">Analyse statique</h3>
        <ul>
          <li><strong>SonarQube</strong> : Plateforme complète d'analyse de la qualité du code</li>
          <li><strong>ESLint</strong> : Pour JavaScript/TypeScript</li>
          <li><strong>Checkstyle</strong> : Pour Java</li>
          <li><strong>Pylint</strong> : Pour Python</li>
        </ul>
        
        <h3 class="text-purple">Analyse de sécurité</h3>
        <ul>
          <li><strong>OWASP Dependency Check</strong> : Détection des vulnérabilités dans les dépendances</li>
          <li><strong>Snyk</strong> : Plateforme de sécurité des applications</li>
          <li><strong>GitHub Security Code Scanning</strong> : Intégré à GitHub</li>
        </ul>
        
        <h3 class="text-purple">Mesure de la qualité</h3>
        <ul>
          <li><strong>CodeClimate</strong> : Métriques de qualité et maintenabilité</li>
          <li><strong>Codacy</strong> : Analyse automatique de la qualité du code</li>
        </ul>
      </section>

      <!-- Exemples de code -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples de problèmes courants</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code problématique</h4>
            <pre><code><span class="keyword">function</span> <span class="function">processUserData</span>(<span class="variable">user</span>) {
  <span class="comment">// Pas de validation des entrées</span>
  <span class="keyword">let</span> <span class="variable">name</span> = <span class="variable">user</span>.<span class="variable">name</span>;
  <span class="keyword">let</span> <span class="variable">email</span> = <span class="variable">user</span>.<span class="variable">email</span>;
  
  <span class="comment">// Injection SQL potentielle</span>
  <span class="keyword">let</span> <span class="variable">query</span> = <span class="string">"INSERT INTO users VALUES ('"</span> + <span class="variable">name</span> + <span class="string">"', '"</span> + <span class="variable">email</span> + <span class="string">"')"</span>;
  
  <span class="comment">// Gestion d'erreur insuffisante</span>
  <span class="variable">db</span>.<span class="function">execute</span>(<span class="variable">query</span>);
}</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Code amélioré</h4>
            <pre><code><span class="keyword">function</span> <span class="function">processUserData</span>(<span class="variable">user</span>) {
  <span class="comment">// Validation des entrées</span>
  <span class="keyword">if</span> (!<span class="variable">user</span> || !<span class="variable">user</span>.<span class="variable">name</span> || !<span class="variable">user</span>.<span class="variable">email</span>) {
    <span class="keyword">throw new</span> <span class="class-name">Error</span>(<span class="string">"Données utilisateur invalides"</span>);
  }
  
  <span class="keyword">let</span> <span class="variable">name</span> = <span class="variable">user</span>.<span class="variable">name</span>.<span class="function">trim</span>();
  <span class="keyword">let</span> <span class="variable">email</span> = <span class="variable">user</span>.<span class="variable">email</span>.<span class="function">trim</span>();
  
  <span class="comment">// Utilisation de requêtes paramétrées</span>
  <span class="keyword">let</span> <span class="variable">query</span> = <span class="string">"INSERT INTO users (name, email) VALUES (?, ?)"</span>;
  
  <span class="keyword">try</span> {
    <span class="comment">// Gestion appropriée des erreurs</span>
    <span class="variable">db</span>.<span class="function">execute</span>(<span class="variable">query</span>, [<span class="variable">name</span>, <span class="variable">email</span>]);
  } <span class="keyword">catch</span> (<span class="variable">error</span>) {
    <span class="variable">console</span>.<span class="function">error</span>(<span class="string">"Erreur lors de l'insertion:"</span>, <span class="variable">error</span>);
    <span class="keyword">throw new</span> <span class="class-name">Error</span>(<span class="string">"Échec de l'enregistrement de l'utilisateur"</span>);
  }
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Métriques de qualité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Métriques de qualité du code</h2>
        
        <div class="metrics-grid">
          <div class="metric-item">
            <h4 class="text-purple">Complexité cyclomatique</h4>
            <p>Mesure la complexité structurelle du code. Une valeur élevée indique un code difficile à maintenir.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Dette technique</h4>
            <p>Estimation du temps nécessaire pour corriger les problèmes de qualité identifiés.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Couverture de tests</h4>
            <p>Pourcentage du code couvert par des tests automatisés.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Maintenabilité</h4>
            <p>Indice calculé basé sur plusieurs facteurs comme la complexité et la duplication.</p>
          </div>
        </div>
      </section>

      <!-- Intégration dans le cycle de projet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Intégration dans le cycle de projet</h2>
        
        <h3 class="text-purple">Développement Agile</h3>
        <p class="textExemple">
          Dans une approche Agile, les audits de code peuvent être intégrés aux revues de code 
          régulières, aux définition of done des user stories, et aux rétrospectives d'itération.
        </p>
        
        <h3 class="text-purple">Intégration continue</h3>
        <p class="textExemple">
          Les outils d'analyse statique peuvent être intégrés dans la pipeline CI/CD pour 
          détecter automatiquement les problèmes à chaque commit ou pull request.
        </p>
        
        <h3 class="text-purple">Points de contrôle projet</h3>
        <p class="textExemple">
          Planifier des audits formels à des moments clés du projet : avant les livraisons majeures, 
          lors de l'intégration de nouveaux modules, ou après des refactorisations importantes.
        </p>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Audit d'un module existant</h3>
          <p class="textExemple">
            Prenez un petit projet ou module de code que vous avez développé récemment et réalisez un audit complet :
          </p>
          <ol>
            <li>Exécutez un outil d'analyse statique (ESLint, SonarQube, etc.)</li>
            <li>Identifiez au moins 5 problèmes de qualité</li>
            <li>Classez-les par niveau de criticité en utilisant l'échelle de gravité</li>
            <li>Proposez des correctifs pour au moins 3 problèmes identifiés</li>
            <li>Rédigez un bref rapport d'audit avec vos conclusions</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir un exemple de solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Rapport d'audit exemple</h4>
              <p><strong>Projet :</strong> Module d'authentification utilisateur</p>
              <p><strong>Date :</strong> [Date de l'audit]</p>
              
              <h4 class="text-purple">Problèmes identifiés :</h4>
              <div class="severity-examples">
                <div class="severity-example critical">
                  <strong>Critique :</strong> Mot de passe stocké en clair dans la base de données
                </div>
                <div class="severity-example high">
                  <strong>Élevée :</strong> Absence de validation des entrées utilisateur
                </div>
                <div class="severity-example medium">
                  <strong>Moyenne :</strong> Code dupliqué dans les fonctions de vérification
                </div>
                <div class="severity-example low">
                  <strong>Faible :</strong> Formatage incohérent des fichiers
                </div>
              </div>
              
              <h4 class="text-purple">Recommandations :</h4>
              <ul>
                <li>Implémenter le hachage des mots de passe avec bcrypt (CRITIQUE)</li>
                <li>Ajouter une validation côté serveur pour tous les champs de formulaire (ÉLEVÉE)</li>
                <li>Refactoriser le code dupliqué en une fonction utilitaire (MOYENNE)</li>
                <li>Configurer un formateur de code automatique (FAIBLE)</li>
              </ul>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <p class="text-white">
          L'audit de code représente bien plus qu'une simple vérification technique - c'est un investissement stratégique 
          dans la qualité et la pérennité de vos projets. En intégrant systématiquement cette pratique dans votre gestion 
          de projet, vous transformez la qualité du code d'une préoccupation ponctuelle en un processus continu d'amélioration.
        </p>
        
        <h3 class="text-white">Bénéfices à long terme</h3>
        <p class="text-white">
          Les audits réguliers permettent de construire une base code solide qui réduit considérablement les coûts de maintenance, 
          améliore la satisfaction des équipes de développement et renforce la confiance des parties prenantes. Un code de qualité 
          est également plus facile à faire évoluer, permettant de répondre plus rapidement aux changements métier.
        </p>
        
        <h3 class="text-white">Culture qualité</h3>
        <p class="text-white">
          Au-delà des aspects techniques, l'audit de code favorise l'émergence d'une culture qualité au sein des équipes. 
          Il encourage le partage des connaissances, la standardisation des pratiques et la responsabilisation collective 
          sur la qualité du produit livré.
        </p>
        
        <h3 class="text-white">Recommandations finales</h3>
        <p class="text-white">
          Pour maximiser l'impact des audits, intégrez-les progressivement dans votre workflow, formez les équipes aux bonnes 
          pratiques identifiées, et utilisez les métriques de qualité pour mesurer l'amélioration dans le temps. N'oubliez pas 
          que l'objectif n'est pas la perfection immédiate, mais l'amélioration continue.
        </p>
        
        <p class="text-white">
          En faisant des audits de code une pratique régulière et structurée, vous positionnez la qualité comme un atout 
          compétitif durable pour vos projets.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CodeAuditLesson',
  head() {
    return {
      title: 'Audit de Code - Gestion de Projet',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Leçon complète sur les audits de code dans la gestion de projet : objectifs, processus, outils et bonnes pratiques.'
        }
      ]
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

/* Styles supplémentaires pour cette page */
.process-step {
    margin-bottom: 1.5rem;
}

.metrics-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
}

.metric-item {
    padding: 1rem;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.metric-item h4 {
    margin-top: 0;
}

/* Degrés de gravité */
.severity-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.severity-item {
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    transition: transform 0.3s ease;
}

.severity-item:hover {
    transform: translateY(-5px);
}

.severity-item h4 {
    padding: 1rem;
    margin: 0;
    text-align: center;
    font-weight: bold;
}

.severity-content {
    padding: 1.5rem;
    background: white;
}

.severity-critical {
    border: 2px solid #dc3545;
}

.severity-critical h4 {
    background: #dc3545;
}

.severity-high {
    border: 2px solid #fd7e14;
}

.severity-high h4 {
    background: #fd7e14;
}

.severity-medium {
    border: 2px solid #ffc107;
}

.severity-medium h4 {
    background: #ffc107;
    color: #212529 !important;
}

.severity-low {
    border: 2px solid #28a745;
}

.severity-low h4 {
    background: #28a745;
}

/* Exemples de sévérité dans la solution */
.severity-examples {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: 1rem 0;
}

.severity-example {
    padding: 0.75rem;
    border-radius: 6px;
    border-left: 4px solid;
}

.severity-example.critical {
    background: #f8d7da;
    border-left-color: #dc3545;
}

.severity-example.high {
    background: #ffe5d0;
    border-left-color: #fd7e14;
}

.severity-example.medium {
    background: #fff3cd;
    border-left-color: #ffc107;
}

.severity-example.low {
    background: #d1e7dd;
    border-left-color: #28a745;
}

/* NOUVEAUX STYLES POUR LA SECTION AUDIT DE DÉPENDANCES */
.tools-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
    margin: 1.5rem 0;
}

.tool-item {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.08);
    border-left: 4px solid #8B5FBF;
}

.tool-item h4 {
    margin-top: 0;
    margin-bottom: 1rem;
    color: #6A3093;
}

.best-practices {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
    margin: 1.5rem 0;
}

.practice-item {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.06);
    border: 1px solid #e0d6ff;
}

.practice-item h4 {
    margin-top: 0;
    margin-bottom: 0.5rem;
    color: #6A3093;
}

.workflow-steps {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin: 1.5rem 0;
}

.workflow-step {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.06);
}

.step-number {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
    color: white;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    flex-shrink: 0;
}

.step-content {
    flex: 1;
}

.step-content h4 {
    margin-top: 0;
    margin-bottom: 0.5rem;
    color: #6A3093;
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
    
    .metrics-grid {
        grid-template-columns: 1fr;
    }
    
    .severity-grid {
        grid-template-columns: 1fr;
    }
    
    .tools-grid {
        grid-template-columns: 1fr;
    }
    
    .best-practices {
        grid-template-columns: 1fr;
    }
    
    .workflow-step {
        flex-direction: column;
        text-align: center;
    }
    
    .step-number {
        align-self: center;
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