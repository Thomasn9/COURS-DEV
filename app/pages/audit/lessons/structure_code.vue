<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Structure de Code dans le Contexte d'un Audit</h1>
        <p class="lesson-meta text-white">Audit technique • Architecture • Maintenabilité • Bonnes pratiques</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à l'audit de structure de code</h2>
        <p class="textExemple">
          L'audit de structure de code examine l'organisation, l'architecture et les principes de conception 
          d'une base de code pour évaluer sa maintenabilité, son évolutivité et sa conformité aux standards. 
          Il va au-delà de la simple vérification syntaxique pour analyser les fondations du système.
        </p>
        <p class="textExemple">
          Une structure de code solide est essentielle pour la longévité des projets, la facilité de maintenance 
          et la réduction des dettes techniques.
        </p>
      </section>

      <!-- Objectifs de l'audit de structure -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs de l'audit de structure de code</h2>
        <ul>
          <li><strong>Évaluer la maintenabilité</strong> : Analyser la facilité de compréhension et de modification du code</li>
          <li><strong>Vérifier l'évolutivité</strong> : S'assurer que l'architecture supporte les évolutions futures</li>
          <li><strong>Identifier les dettes techniques</strong> : Détecter les choix structurels problématiques</li>
          <li><strong>Valider les principes SOLID</strong> : Vérifier l'application des bonnes pratiques de conception</li>
          <li><strong>Optimiser les performances</strong> : Repérer les inefficacités architecturales</li>
        </ul>
      </section>

      <!-- Aspects évalués -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Aspects structurels évalués</h2>
        
        <h3 class="text-purple">1. Architecture et patterns</h3>
        <p class="textExemple">
          Évaluation des patterns architecturaux (MVC, Microservices, Hexagonale) et leur mise en œuvre cohérente.
        </p>
        
        <h3 class="text-purple">2. Organisation des modules</h3>
        <p class="textExemple">
          Analyse de la modularité, de la séparation des concerns et de la cohésion des composants.
        </p>
        
        <h3 class="text-purple">3. Qualité des abstractions</h3>
        <p class="textExemple">
          Vérification de l'encapsulation, des interfaces et de la gestion des dépendances.
        </p>

        <h3 class="text-purple">4. Gestion des données</h3>
        <p class="textExemple">
          Évaluation des modèles de données, du mapping objet-relationnel et des stratégies de persistance.
        </p>
      </section>

      <!-- Processus d'audit structurel -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Processus d'audit de structure de code</h2>
        
        <div class="process-step">
          <h3 class="text-purple">1. Analyse architecturale globale</h3>
          <p class="textExemple">
            Examiner le diagramme d'architecture, identifier les patterns utilisés 
            et évaluer la cohérence d'ensemble.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">2. Revue de la modularité</h3>
          <p class="textExemple">
            Analyser la structure des packages/modules, les dépendances circulaires 
            et la séparation des responsabilités.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">3. Évaluation des principes SOLID</h3>
          <p class="textExemple">
            Vérifier l'application des principes de conception orientée objet 
            et identifier les violations structurelles.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">4. Métriques et rapports</h3>
          <p class="textExemple">
            Calculer les métriques de complexité, générer des visualisations 
            et documenter les recommandations d'amélioration.
          </p>
        </div>
      </section>

      <!-- Critères d'évaluation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Critères d'évaluation de la structure</h2>
        
        <div class="severity-grid">
          <div class="severity-item severity-critical">
            <h4 class="text-white">ARCHITECTURE DÉFAILLANTE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Remise en cause totale de la base code</p>
              <p><strong>Indicateurs :</strong></p>
              <ul>
                <li>God objects et classes omnipotentes</li>
                <li>Dépendances circulaires généralisées</li>
                <li>Absence de séparation des concerns</li>
                <li>Couplage fort entre tous les modules</li>
              </ul>
              <p><strong>Action :</strong> Refactorisation majeure nécessaire</p>
            </div>
          </div>
          
          <div class="severity-item severity-high">
            <h4 class="text-white">PROBLÈMES STRUCTURELS MAJEURS</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Difficultés importantes de maintenance</p>
              <p><strong>Indicateurs :</strong></p>
              <ul>
                <li>Violations multiples des principes SOLID</li>
                <li>Modules trop gros et peu cohésifs</li>
                <li>Dépendances inappropriées</li>
                <li>Duplication de code structurelle</li>
              </ul>
              <p><strong>Action :</strong> Refactorisation ciblée requise</p>
            </div>
          </div>
          
          <div class="severity-item severity-medium">
            <h4 class="text-white">AMÉLIORATIONS RECOMMANDÉES</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Opportunités d'optimisation</p>
              <p><strong>Indicateurs :</strong></p>
              <ul>
                <li>Certaines classes trop longues</li>
                <li>Interfaces peu spécifiques</li>
                <li>Opportunités de réutilisation</li>
                <li>Organisation sous-optimale</li>
              </ul>
              <p><strong>Action :</strong> Améliorations progressives</p>
            </div>
          </div>
          
          <div class="severity-item severity-low">
            <h4 class="text-white">STRUCTURE SATISFAISANTE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Excellente maintenabilité</p>
              <p><strong>Indicateurs :</strong></p>
              <ul>
                <li>Architecture cohérente et documentée</li>
                <li>Modules bien définis et cohésifs</li>
                <li>Faible couplage, forte cohésion</li>
                <li>Respect des principes SOLID</li>
              </ul>
              <p><strong>Action :</strong> Maintenance des bonnes pratiques</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Principes SOLID évalués -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Principes SOLID évalués</h2>
        
        <div class="solid-grid">
          <div class="solid-item">
            <h4 class="text-purple">S - Single Responsibility</h4>
            <p><strong>Une classe = une responsabilité</strong></p>
            <ul>
              <li>Classes focalisées sur un métier précis</li>
              <li>Éviter les classes "fourre-tout"</li>
              <li>Facilite les tests unitaires</li>
              <li>Réduit l'impact des changements</li>
            </ul>
          </div>
          
          <div class="solid-item">
            <h4 class="text-purple">O - Open/Closed</h4>
            <p><strong>Ouvert à l'extension, fermé à la modification</strong></p>
            <ul>
              <li>Utilisation d'interfaces et d'abstractions</li>
              <li>Extension par héritage/composition</li>
              <li>Éviter les modifications de code existant</li>
              <li>Favoriser l'injection de dépendances</li>
            </ul>
          </div>
          
          <div class="solid-item">
            <h4 class="text-purple">L - Liskov Substitution</h4>
            <p><strong>Substitution transparente</strong></p>
            <ul>
              <li>Les sous-classes remplacent les parentes</li>
              <li>Respect des contrats d'interface</li>
              <li>Pas d'exceptions inattendues</li>
              <li>Comportement prévisible</li>
            </ul>
          </div>
          
          <div class="solid-item">
            <h4 class="text-purple">I - Interface Segregation</h4>
            <p><strong>Interfaces spécifiques et fines</strong></p>
            <ul>
              <li>Éviter les interfaces "obèses"</li>
              <li>Segmentation par rôle/utilisateur</li>
              <li>Clients ne dépendent que de ce qu'ils utilisent</li>
              <li>Réduction du couplage</li>
            </ul>
          </div>

          <div class="solid-item">
            <h4 class="text-purple">D - Dependency Inversion</h4>
            <p><strong>Dépendre des abstractions</strong></p>
            <ul>
              <li>Modules haut niveau indépendants des bas niveau</li>
              <li>Abstractions stables, implémentations changeantes</li>
              <li>Inversion de contrôle (IoC)</li>
              <li>Facilite les tests et la modularité</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Exemples de code -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples de structures problématiques vs optimales</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Structure problématique - God Object</h4>
            <pre><code><span class="keyword">class</span> <span class="class-name">UserManager</span> {
  <span class="comment">// Violation SRP - Trop de responsabilités</span>
  <span class="function">createUser</span>() { <span class="comment">/*...*/</span> }
  <span class="function">deleteUser</span>() { <span class="comment">/*...*/</span> }
  <span class="function">sendEmail</span>() { <span class="comment">/*...*/</span> }
  <span class="function">validatePassword</span>() { <span class="comment">/*...*/</span> }
  <span class="function">generateReport</span>() { <span class="comment">/*...*/</span> }
  <span class="function">updateProfile</span>() { <span class="comment">/*...*/</span> }
  <span class="function">processPayment</span>() { <span class="comment">/*...*/</span> }
  <span class="function">logActivity</span>() { <span class="comment">/*...*/</span> }
}

<span class="comment">// Fort couplage entre modules</span>
<span class="keyword">class</span> <span class="class-name">OrderService</span> {
  <span class="function">processOrder</span>() {
    <span class="variable">userManager</span> = <span class="keyword">new</span> <span class="class-name">UserManager</span>();
    <span class="variable">paymentProcessor</span> = <span class="keyword">new</span> <span class="class-name">PaymentProcessor</span>();
    <span class="comment">// Logique métier entremêlée...</span>
  }
}</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Structure optimale - Séparation des concerns</h4>
            <pre><code><span class="comment">// Classes focalisées - Respect SRP</span>
<span class="keyword">class</span> <span class="class-name">UserService</span> {
  <span class="function">constructor</span>(<span class="variable">userRepo</span>, <span class="variable">validator</span>) {}
  <span class="function">createUser</span>() { <span class="comment">/*...*/</span> }
  <span class="function">updateUser</span>() { <span class="comment">/*...*/</span> }
}

<span class="keyword">class</span> <span class="class-name">EmailService</span> {
  <span class="function">sendWelcomeEmail</span>() { <span class="comment">/*...*/</span> }
}

<span class="keyword">class</span> <span class="class-name">ReportGenerator</span> {
  <span class="function">generateUserReport</span>() { <span class="comment">/*...*/</span> }
}

<span class="comment">// Injection de dépendances - Respect DIP</span>
<span class="keyword">class</span> <span class="class-name">OrderService</span> {
  <span class="function">constructor</span>(<span class="variable">userService</span>, <span class="variable">paymentService</span>, <span class="variable">emailService</span>) {}
  
  <span class="function">processOrder</span>(<span class="variable">order</span>) {
    <span class="variable">user</span> = <span class="keyword">this</span>.<span class="variable">userService</span>.<span class="function">getUser</span>(<span class="variable">order</span>.<span class="variable">userId</span>);
    <span class="variable">payment</span> = <span class="keyword">this</span>.<span class="variable">paymentService</span>.<span class="function">process</span>(<span class="variable">order</span>);
    <span class="keyword">this</span>.<span class="variable">emailService</span>.<span class="function">sendConfirmation</span>(<span class="variable">user</span>, <span class="variable">order</span>);
  }
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Métriques structurelles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Métriques de qualité structurelle</h2>
        
        <div class="metrics-grid">
          <div class="metric-item">
            <h4 class="text-purple">Complexité cyclomatique</h4>
            <p>Nombre de chemins indépendants dans une méthode. Cible : &lt; 10 par méthode.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Couplage afférent</h4>
            <p>Nombre de classes qui dépendent de la classe courante. Cible : faible.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Cohésion LCOM</h4>
            <p>Manque de cohésion dans les méthodes. Cible : &lt; 1.0.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Profondeur d'héritage</h4>
            <p>Nombre de niveaux dans la hiérarchie d'héritage. Cible : &lt; 4.</p>
          </div>
        </div>

        <div class="metrics-grid">
          <div class="metric-item">
            <h4 class="text-purple">Taille des classes (LOC)</h4>
            <p>Nombre de lignes par classe. Cible : &lt; 200 lignes.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Taille des méthodes</h4>
            <p>Nombre de lignes par méthode. Cible : &lt; 20 lignes.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Dépendances circulaires</h4>
            <p>Présence de cycles dans le graphe de dépendances. Cible : 0.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Duplication de code</h4>
            <p>Pourcentage de code dupliqué. Cible : &lt; 3%.</p>
          </div>
        </div>
      </section>

      <!-- Outils d'analyse -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils d'analyse structurelle</h2>
        
        <h3 class="text-purple">Analyse statique avancée</h3>
        <ul>
          <li><strong>SonarQube</strong> : Métriques complètes et détection de dette technique</li>
          <li><strong>NDepend</strong> : Analyse approfondie des dépendances et métriques .NET</li>
          <li><strong>Checkstyle/PMD</strong> : Règles architecturales pour Java</li>
        </ul>
        
        <h3 class="text-purple">Visualisation d'architecture</h3>
        <ul>
          <li><strong>Structure101</strong> : Analyse et visualisation des dépendances</li>
          <li><strong>Lattix</strong> : Modélisation et gestion de l'architecture</li>
          <li><strong>PlantUML</strong> : Génération de diagrammes à partir du code</li>
        </ul>
        
        <h3 class="text-purple">Analyse de dépendances</h3>
        <ul>
          <li><strong>JDepend</strong> : Métriques de qualité pour packages Java</li>
          <li><strong>Depends</strong> : Analyse de dépendances multi-langages</li>
          <li><strong>CodeMaT</strong> : Cartographie des dépendances et métriques</li>
        </ul>
      </section>

      <!-- Patterns architecturaux courants -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Patterns architecturaux évalués</h2>
        
        <div class="architecture-grid">
          <div class="architecture-item">
            <h4 class="text-purple">🏗️ Architecture en couches</h4>
            <p><strong>Presentation → Business → Data</strong></p>
            <ul>
              <li>Facile à comprendre</li>
              <li>Risque de couplage entre couches</li>
              <li>Évolutivité limitée</li>
              <li>Bon pour applications simples</li>
            </ul>
          </div>
          
          <div class="architecture-item">
            <h4 class="text-purple">🔗 Architecture hexagonale</h4>
            <p><strong>Domain au centre, adapters en périphérie</strong></p>
            <ul>
              <li>Isolation du domaine métier</li>
              <li>Testabilité excellente</li>
              <li>Complexité initiale plus élevée</li>
              <li>Idéal pour DDD</li>
            </ul>
          </div>
          
          <div class="architecture-item">
            <h4 class="text-purple">⚡ Microservices</h4>
            <p><strong>Services indépendants et spécialisés</strong></p>
            <ul>
              <li>Évolutivité horizontale</li>
              <li>Déploiements indépendants</li>
              <li>Complexité opérationnelle</li>
              <li>Nécessite maturité DevOps</li>
            </ul>
          </div>
          
          <div class="architecture-item">
            <h4 class="text-purple">🎯 CQRS + Event Sourcing</h4>
            <p><strong>Séparation lecture/écriture + événements</strong></p>
            <ul>
              <li>Performance lecture optimisée</li>
              <li>Audit trail naturel</li>
              <li>Complexité cognitive</li>
              <li>Spécialisé pour systèmes complexes</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Checklist d'audit -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Checklist d'audit de structure</h2>
        
        <div class="code-example">
          <pre><code><span class="comment">// Checklist d'évaluation structurelle</span>
<span class="number">□</span> Architecture documentée et comprise par l'équipe
<span class="number">□</span> Séparation claire des concerns (présentation, métier, données)
<span class="number">□</span> Absence de dépendances circulaires
<span class="number">□</span> Modules avec forte cohésion et faible couplage
<span class="number">□</span> Respect des principes SOLID
<span class="number">□</span> Taille des classes et méthodes raisonnable
<span class="number">□</span> Utilisation appropriée des patterns de conception
<span class="number">□</span> Gestion cohérente des exceptions
<span class="number">□</span> Stratégie de logging structurée
<span class="number">□</span> Configuration externalisée et organisée
<span class="number">□</span> Tests unitaires couvrant les composants métier
<span class="number">□</span> Documentation des interfaces et contrats
<span class="number">□</span> Gestion des dépendances claire (IoC/DI)
<span class="number">□</span> Absence de code dupliqué structurel
<span class="number">□</span> Organisation cohérente des packages/namespaces</code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Audit d'une base de code existante</h3>
          <p class="textExemple">
            Vous devez réaliser un audit structurel sur un module de gestion des commandes. 
            Le module contient 15 classes et 2 000 lignes de code. Réalisez les étapes suivantes :
          </p>
          <ol>
            <li>Analysez la structure des packages et des dépendances</li>
            <li>Identifiez les violations des principes SOLID</li>
            <li>Calculez les métriques de complexité principales</li>
            <li>Évaluez la qualité des abstractions et interfaces</li>
            <li>Proposez un plan de refactorisation priorisé</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir un exemple de solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Rapport d'audit structurel - Module Commandes</h4>
              <p><strong>Module :</strong> Gestion des commandes "OrderManagement"</p>
              <p><strong>Taille :</strong> 15 classes, 2 150 LOC</p>
              
              <h4 class="text-purple">Problèmes structurels identifiés :</h4>
              <div class="structure-examples">
                <div class="structure-example critical">
                  <strong>CRITIQUE :</strong> Classe OrderProcessor (450 LOC) - God object violant SRP
                </div>
                <div class="structure-example high">
                  <strong>ÉLEVÉ :</strong> Dépendances circulaires entre OrderService et PaymentService
                </div>
                <div class="structure-example medium">
                  <strong>MOYEN :</strong> Interface IOrderManager trop large (15 méthodes)
                </div>
                <div class="structure-example low">
                  <strong>FAIBLE :</strong> Organisation sous-optimale des packages
                </div>
              </div>
              
              <h4 class="text-purple">Métriques calculées :</h4>
              <ul>
                <li><strong>Complexité cyclomatique moyenne :</strong> 8.2 (cible : &lt; 10)</li>
                <li><strong>Couplage afférent moyen :</strong> 4.1 (cible : &lt; 5)</li>
                <li><strong>Taille moyenne des classes :</strong> 143 LOC (cible : &lt; 200)</li>
                <li><strong>Duplication de code :</strong> 5.8% (cible : &lt; 3%)</li>
              </ul>

              <h4 class="text-purple">Plan de refactorisation :</h4>
              <ul>
                <li><strong>Phase 1 (Urgent) :</strong> Découper OrderProcessor en 4 classes spécialisées</li>
                <li><strong>Phase 2 (Important) :</strong> Introduire une interface pour briser les dépendances circulaires</li>
                <li><strong>Phase 3 (Recommandé) :</strong> Segmente IOrderManager en 3 interfaces spécifiques</li>
                <li><strong>Phase 4 (Amélioration) :</strong> Réorganiser les packages par feature</li>
              </ul>

              <h4 class="text-purple">Estimation d'effort :</h4>
              <ul>
                <li><strong>Refactorisation critique :</strong> 3-5 jours</li>
                <li><strong>Améliorations structurelles :</strong> 2-3 jours</li>
                <li><strong>Tests de non-régression :</strong> 2 jours</li>
                <li><strong>Total estimé :</strong> 7-10 jours</li>
              </ul>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <p class="text-white">
          L'audit de structure de code représente l'examen fondamental des fondations d'un système logiciel. 
          Au-delà de la correction des bugs immédiats, il s'attaque aux causes profondes des difficultés 
          de maintenance et des limitations d'évolutivité qui handicapent les projets à long terme.
        </p>
        
        <h3 class="text-white">Investissement stratégique</h3>
        <p class="text-white">
          Les efforts consacrés à l'amélioration structurelle du code constituent un investissement stratégique 
          qui paie des dividendes tout au long du cycle de vie du projet. Une architecture solide réduit 
          les coûts de maintenance, accélère le développement de nouvelles fonctionnalités et améliore 
          la satisfaction des équipes de développement.
        </p>
        
        <h3 class="text-white">Culture de qualité</h3>
        <p class="text-white">
          Les audits structurels réguliers contribuent à instaurer une culture de qualité technique 
          au sein des équipes. En sensibilisant aux principes de conception et en fournissant des retours 
          concrets, ils transforment la dette technique d'un problème subi en une opportunité d'amélioration maîtrisée.
        </p>
        
        <h3 class="text-white">Approche pragmatique</h3>
        <p class="text-white">
          L'audit structurel efficace ne recherche pas la perfection théorique mais l'optimisation pragmatique. 
          Il identifie les problèmes ayant le plus d'impact sur la productivité et propose des plans de correction 
          réalistes, priorisés en fonction du rapport coût/bénéfice pour l'organisation.
        </p>
        
        <p class="text-white">
          En intégrant l'audit de structure dans les pratiques courantes de développement, les organisations 
          s'assurent non seulement de la qualité technique de leurs produits, mais aussi de leur capacité 
          à évoluer durablement dans un environnement technologique en perpétuel changement.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CodeStructureAuditLesson',
  head() {
    return {
      title: 'Structure de Code - Audit Technique',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Leçon complète sur l\'audit de structure de code : principes SOLID, métriques, patterns architecturaux et bonnes pratiques.'
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

/* Niveaux de qualité structurelle */
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

/* Grille SOLID */
.solid-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.solid-item {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    border-left: 4px solid #8B5FBF;
}

.solid-item h4 {
    margin-top: 0;
    margin-bottom: 0.5rem;
}

.solid-item p {
    font-weight: 600;
    margin-bottom: 1rem;
    color: #6A3093;
}

.solid-item ul {
    margin: 0;
    padding-left: 1.2rem;
}

.solid-item li {
    margin-bottom: 0.3rem;
}

/* Grille architecture */
.architecture-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.architecture-item {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    border-left: 4px solid #8B5FBF;
}

.architecture-item h4 {
    margin-top: 0;
    margin-bottom: 0.5rem;
}

.architecture-item p {
    font-weight: 600;
    margin-bottom: 1rem;
    color: #6A3093;
}

.architecture-item ul {
    margin: 0;
    padding-left: 1.2rem;
}

.architecture-item li {
    margin-bottom: 0.3rem;
}

/* Exemples de structure dans la solution */
.structure-examples {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: 1rem 0;
}

.structure-example {
    padding: 0.75rem;
    border-radius: 6px;
    border-left: 4px solid;
}

.structure-example.critical {
    background: #f8d7da;
    border-left-color: #dc3545;
}

.structure-example.high {
    background: #ffe5d0;
    border-left-color: #fd7e14;
}

.structure-example.medium {
    background: #fff3cd;
    border-left-color: #ffc107;
}

.structure-example.low {
    background: #d1e7dd;
    border-left-color: #28a745;
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
    
    .solid-grid {
        grid-template-columns: 1fr;
    }
    
    .architecture-grid {
        grid-template-columns: 1fr;
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