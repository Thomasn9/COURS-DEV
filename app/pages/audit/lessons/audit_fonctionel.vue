<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Audit Fonctionnel dans la Gestion de Projet</h1>
        <p class="lesson-meta text-white">Gestion de projet • Spécifications fonctionnelles • Qualité métier</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à l'audit fonctionnel</h2>
        <p class="textExemple">
          L'audit fonctionnel est une démarche systématique d'évaluation de la conformité d'une application 
          ou d'un système par rapport aux besoins métier exprimés. Il vise à s'assurer que les fonctionnalités 
          développées répondent correctement aux exigences des utilisateurs finaux.
        </p>
        <p class="textExemple">
          Contrairement à l'audit technique qui se concentre sur la qualité du code, l'audit fonctionnel 
          s'intéresse à la valeur métier délivrée par le produit.
        </p>
      </section>

      <!-- Objectifs d'un audit fonctionnel -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'un audit fonctionnel</h2>
        <ul>
          <li><strong>Vérifier la conformité métier</strong> : S'assurer que le produit répond aux besoins utilisateurs</li>
          <li><strong>Identifier les écarts fonctionnels</strong> : Détecter les différences entre les spécifications et la réalisation</li>
          <li><strong>Améliorer l'expérience utilisateur</strong> : Évaluer l'ergonomie et la facilité d'utilisation</li>
          <li><strong>Valider les processus métier</strong> : Vérifier l'adéquation avec les workflows réels</li>
          <li><strong>Optimiser la valeur business</strong> : S'assurer que le produit délivre la valeur attendue</li>
        </ul>
      </section>

      <!-- Types d'audits fonctionnels -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types d'audits fonctionnels</h2>
        
        <h3 class="text-purple">1. Audit de conformité</h3>
        <p class="textExemple">
          Vérification systématique du respect des spécifications fonctionnelles et du cahier des charges.
        </p>
        
        <h3 class="text-purple">2. Audit d'utilisabilité</h3>
        <p class="textExemple">
          Évaluation de l'expérience utilisateur, de l'ergonomie et de la facilité de prise en main.
        </p>
        
        <h3 class="text-purple">3. Audit de processus</h3>
        <p class="textExemple">
          Analyse de l'adéquation entre les fonctionnalités et les processus métier réels.
        </p>

        <h3 class="text-purple">4. Audit de recette</h3>
        <p class="textExemple">
          Validation finale avant mise en production impliquant les utilisateurs métier.
        </p>
      </section>

      <!-- Processus d'audit fonctionnel -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Processus d'audit fonctionnel</h2>
        
        <div class="process-step">
          <h3 class="text-purple">1. Préparation et cadrage</h3>
          <p class="textExemple">
            Définir le périmètre, identifier les parties prenantes, réviser la documentation 
            (cahier des charges, user stories, maquettes).
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">2. Analyse des spécifications</h3>
          <p class="textExemple">
            Examiner la complétude et la cohérence des exigences fonctionnelles, 
            identifier les ambiguïtés et les contradictions.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">3. Tests et validation</h3>
          <p class="textExemple">
            Exécuter des scénarios de test, vérifier les cas d'utilisation, 
            valider les workflows métier et l'ergonomie.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">4. Rapport et recommandations</h3>
          <p class="textExemple">
            Documenter les écarts identifiés, prioriser les corrections, 
            proposer des améliorations fonctionnelles.
          </p>
        </div>
      </section>

      <!-- Degrés de gravité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Degrés de gravité des écarts fonctionnels</h2>
        
        <div class="severity-grid">
          <div class="severity-item severity-critical">
            <h4 class="text-white">CRITIQUE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Bloque l'utilisation du produit</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Fonctionnalité core non implémentée</li>
                <li>Workflow métier principal impossible</li>
                <li>Données critiques perdues ou corrompues</li>
                <li>Non-conformité réglementaire</li>
              </ul>
              <p><strong>Action :</strong> Correction immédiate avant mise en production</p>
            </div>
          </div>
          
          <div class="severity-item severity-high">
            <h4 class="text-white">ÉLEVÉE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Impact majeur sur l'expérience utilisateur</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Workflow métier partiellement fonctionnel</li>
                <li>Performance inacceptable pour l'usage métier</li>
                <li>Ergonomie très dégradée</li>
                <li>Fonctionnalité secondaire manquante mais importante</li>
              </ul>
              <p><strong>Action :</strong> Correction requise avant livraison</p>
            </div>
          </div>
          
          <div class="severity-item severity-medium">
            <h4 class="text-white">MOYENNE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Gêne occasionnelle pour l'utilisateur</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Message d'erreur peu clair</li>
                <li>Workflow non optimal mais fonctionnel</li>
                <li>Documentation incomplète</li>
                <li>Petite incohérence interface utilisateur</li>
              </ul>
              <p><strong>Action :</strong> Correction planifiée pour prochaine version</p>
            </div>
          </div>
          
          <div class="severity-item severity-low">
            <h4 class="text-white">FAIBLE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Impact cosmétique ou très mineur</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Faute d'orthographe dans un libellé</li>
                <li>Alignement visuel imparfait</li>
                <li>Couleur non conforme au guide de style</li>
                <li>Message de confirmation optionnel manquant</li>
              </ul>
              <p><strong>Action :</strong> Correction optionnelle</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Méthodes et techniques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Méthodes et techniques d'audit fonctionnel</h2>
        
        <h3 class="text-purple">Revue de documentation</h3>
        <p class="textExemple">
          Analyse des spécifications fonctionnelles, user stories, maquettes et cahier des charges 
          pour identifier les incohérences et les ambiguïtés.
        </p>
        
        <h3 class="text-purple">Tests manuels</h3>
        <p class="textExemple">
          Exécution de scénarios de test couvrant les cas d'utilisation principaux, 
          les cas limites et les parcours utilisateur critiques.
        </p>
        
        <h3 class="text-purple">Ateliers utilisateurs</h3>
        <p class="textExemple">
          Sessions de travail avec les utilisateurs finaux pour valider l'adéquation 
          des fonctionnalités avec leurs besoins réels.
        </p>

        <h3 class="text-purple">Checklists fonctionnelles</h3>
        <p class="textExemple">
          Utilisation de listes de contrôle standardisées pour garantir 
          une couverture complète des vérifications.
        </p>
      </section>

      <!-- Outils d'audit fonctionnel -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils d'audit fonctionnel</h2>
        
        <h3 class="text-purple">Gestion des tests</h3>
        <ul>
          <li><strong>JIRA</strong> : Suivi des bugs et gestion des user stories</li>
          <li><strong>TestRail</strong> : Gestion des cas de test et reporting</li>
          <li><strong>Zephyr</strong> : Solution de test intégrée à JIRA</li>
        </ul>
        
        <h3 class="text-purple">Capture et reporting</h3>
        <ul>
          <li><strong>Snagit</strong> : Capture d'écran et annotations</li>
          <li><strong>Loom</strong> : Enregistrement vidéo des anomalies</li>
          <li><strong>SharePoint</strong> : Centralisation de la documentation</li>
        </ul>
        
        <h3 class="text-purple">Collaboration</h3>
        <ul>
          <li><strong>Confluence</strong> : Documentation des spécifications</li>
          <li><strong>Figma</strong> : Revue des maquettes et prototypage</li>
          <li><strong>Miro</strong> : Ateliers collaboratifs en ligne</li>
        </ul>
      </section>

      <!-- Exemples de scénarios de test -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples de scénarios de test fonctionnel</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Scénario e-commerce - Paiement</h4>
            <pre><code><span class="comment">// Cas nominal - Paiement réussi</span>
<span class="number">1.</span> Ajouter un produit au panier
<span class="number">2.</span> Accéder au panier
<span class="number">3.</span> Cliquer sur "Procéder au paiement"
<span class="number">4.</span> Remplir les informations de livraison
<span class="number">5.</span> Sélectionner le mode de livraison
<span class="number">6.</span> Saisir les informations de carte valide
<span class="number">7.</span> Confirmer la commande
<span class="number">8.</span> <span class="keyword">VÉRIFIER</span> : Page de confirmation affichée
<span class="number">9.</span> <span class="keyword">VÉRIFIER</span> : Email de confirmation reçu
<span class="number">10.</span> <span class="keyword">VÉRIFIER</span> : Statut commande "Confirmée"</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Scénario CRM - Création client</h4>
            <pre><code><span class="comment">// Cas d'erreur - Validation formulaire</span>
<span class="number">1.</span> Naviguer vers "Nouveau client"
<span class="number">2.</span> Laisser le champ "Nom" vide
<span class="number">3.</span> Saisir un email invalide "email@invalide"
<span class="number">4.</span> Cliquer sur "Enregistrer"
<span class="number">5.</span> <span class="keyword">VÉRIFIER</span> : Message erreur "Nom obligatoire"
<span class="number">6.</span> <span class="keyword">VÉRIFIER</span> : Message erreur "Email invalide"
<span class="number">7.</span> <span class="keyword">VÉRIFIER</span> : Formulaire non soumis
<span class="number">8.</span> Corriger les erreurs
<span class="number">9.</span> <span class="keyword">VÉRIFIER</span> : Messages erreur disparus
<span class="number">10.</span> <span class="keyword">VÉRIFIER</span> : Enregistrement réussi</code></pre>
          </div>
        </div>
      </section>

      <!-- Métriques fonctionnelles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Métriques de qualité fonctionnelle</h2>
        
        <div class="metrics-grid">
          <div class="metric-item">
            <h4 class="text-purple">Taux de couverture fonctionnelle</h4>
            <p>Pourcentage des exigences métier couvertes par des tests validés.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Densité des défauts</h4>
            <p>Nombre de défauts fonctionnels identifiés par rapport à la taille fonctionnelle.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Taux de satisfaction utilisateur</h4>
            <p>Score de satisfaction collecté auprès des utilisateurs métier.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Adéquation processus</h4>
            <p>Pourcentage de conformité entre les fonctionnalités et les processus métier réels.</p>
          </div>
        </div>
      </section>

      <!-- Intégration dans le cycle de projet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Intégration dans le cycle de projet</h2>
        
        <h3 class="text-purple">Méthode Agile</h3>
        <p class="textExemple">
          Dans les sprints Agile, l'audit fonctionnel est intégré aux Definition of Done, 
          aux démonstrations de fin de sprint et aux tests d'acceptation par le Product Owner.
        </p>
        
        <h3 class="text-purple">Cycle en V</h3>
        <p class="textExemple">
          L'audit fonctionnel intervient lors de la phase de recette où l'on vérifie 
          la conformité avec les spécifications détaillées établies en amont.
        </p>
        
        <h3 class="text-purple">Livraison continue</h3>
        <p class="textExemple">
          Des audits fonctionnels automatisés peuvent être intégrés dans les pipelines 
          de déploiement pour les régressions fonctionnelles critiques.
        </p>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Audit d'une application existante</h3>
          <p class="textExemple">
            Choisissez une application web que vous connaissez bien (site e-commerce, application métier, etc.) 
            et réalisez un audit fonctionnel complet :
          </p>
          <ol>
            <li>Identifiez 3 processus métier principaux</li>
            <li>Créez des scénarios de test pour chaque processus</li>
            <li>Exécutez les tests et documentez les écarts</li>
            <li>Classez les problèmes par niveau de gravité</li>
            <li>Rédigez un rapport d'audit avec recommandations</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir un exemple de solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Rapport d'audit fonctionnel - Site e-commerce</h4>
              <p><strong>Application :</strong> Boutique en ligne "TechStore"</p>
              <p><strong>Date :</strong> [Date de l'audit]</p>
              
              <h4 class="text-purple">Problèmes identifiés :</h4>
              <div class="severity-examples">
                <div class="severity-example critical">
                  <strong>Critique :</strong> Impossible de finaliser une commande - erreur système au paiement
                </div>
                <div class="severity-example high">
                  <strong>Élevée :</strong> Processus de retour client non implémenté
                </div>
                <div class="severity-example medium">
                  <strong>Moyenne :</strong> Recherche produit ne respecte pas les filtres avancés
                </div>
                <div class="severity-example low">
                  <strong>Faible :</strong> Libellé "Ajouter au panier" mal orthographié
                </div>
              </div>
              
              <h4 class="text-purple">Recommandations prioritaires :</h4>
              <ul>
                <li>Corriger le processus de paiement en urgence (CRITIQUE)</li>
                <li>Implémenter le module de gestion des retours (ÉLEVÉE)</li>
                <li>Améliorer le moteur de recherche avec les filtres (MOYENNE)</li>
                <li>Corriger les fautes d'orthographe (FAIBLE)</li>
              </ul>

              <h4 class="text-purple">Métriques de qualité :</h4>
              <ul>
                <li><strong>Taux de couverture fonctionnelle :</strong> 75%</li>
                <li><strong>Défauts critiques identifiés :</strong> 2</li>
                <li><strong>Satisfaction utilisateur estimée :</strong> 6/10</li>
              </ul>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <p class="text-white">
          L'audit fonctionnel constitue un pilier essentiel de l'assurance qualité dans la gestion de projet. 
          Il représente le lien crucial entre les attentes métier et la réalisation technique, garantissant 
          que le produit délivré répond véritablement aux besoins des utilisateurs finaux.
        </p>
        
        <h3 class="text-white">Valeur stratégique</h3>
        <p class="text-white">
          Au-delà de la simple détection des anomalies, l'audit fonctionnel permet d'aligner continuellement 
          le développement sur la valeur business. Il transforme la validation qualité d'une contrainte en 
          un levier stratégique pour l'adoption utilisateur et le retour sur investissement.
        </p>
        
        <h3 class="text-white">Approche proactive</h3>
        <p class="text-white">
          Les organisations matures intègrent l'audit fonctionnel tout au long du cycle de vie du produit, 
          depuis la spécification jusqu'à la maintenance. Cette approche proactive permet d'anticiper les 
          écarts fonctionnels plutôt que de les subir, réduisant considérablement les coûts de correction.
        </p>
        
        <h3 class="text-white">Excellence opérationnelle</h3>
        <p class="text-white">
          Un audit fonctionnel bien mené ne se limite pas à vérifier la conformité aux spécifications. 
          Il évalue également l'ergonomie, l'efficacité des workflows et l'adéquation avec les processus 
          métier réels, contribuant ainsi à l'excellence opérationnelle de l'organisation.
        </p>
        
        <p class="text-white">
          En institutionnalisant la pratique de l'audit fonctionnel, les entreprises s'assurent non seulement 
          de la qualité de leurs livrables, mais aussi de leur pertinence business et de leur valeur durable 
          pour les utilisateurs finaux.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FunctionalAuditLesson',
  head() {
    return {
      title: 'Audit Fonctionnel - Gestion de Projet',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Leçon complète sur les audits fonctionnels dans la gestion de projet : méthodes, processus, outils et bonnes pratiques métier.'
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