<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Audit de Conformité dans la Gestion de Projet</h1>
        <p class="lesson-meta text-white">Gestion de projet • Conformité réglementaire • Normes et standards</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à l'audit de conformité</h2>
        <p class="textExemple">
          L'audit de conformité est un processus systématique de vérification du respect des exigences légales, 
          réglementaires, contractuelles et normatives applicables à un projet ou une organisation. 
          Il garantit que les activités et livrables sont en adéquation avec le cadre contraignant.
        </p>
        <p class="textExemple">
          Dans un contexte de plus en plus réglementé, l'audit de conformité devient un enjeu critique 
          pour la pérennité des projets et la protection des organisations.
        </p>
      </section>

      <!-- Objectifs d'un audit de conformité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'un audit de conformité</h2>
        <ul>
          <li><strong>Vérifier le respect des obligations légales</strong> : S'assurer de la conformité aux lois et réglementations</li>
          <li><strong>Prévenir les risques juridiques</strong> : Identifier les écarts pouvant entraîner des sanctions</li>
          <li><strong>Protéger l'organisation</strong> : Éviter les amendes, poursuites et atteintes à la réputation</li>
          <li><strong>Garantir l'intégrité des processus</strong> : Vérifier l'application des procédures établies</li>
          <li><strong>Améliorer la gouvernance</strong> : Renforcer le cadre de contrôle interne</li>
        </ul>
      </section>

      <!-- Types d'audits de conformité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types d'audits de conformité</h2>
        
        <h3 class="text-purple">1. Audit réglementaire</h3>
        <p class="textExemple">
          Vérification du respect des lois et réglementations sectorielles (RGPD, SOX, HIPAA, etc.).
        </p>
        
        <h3 class="text-purple">2. Audit normatif</h3>
        <p class="textExemple">
          Contrôle de la conformité aux standards et normes (ISO, CMMI, ITIL, etc.).
        </p>
        
        <h3 class="text-purple">3. Audit contractuel</h3>
        <p class="textExemple">
          Vérification du respect des clauses contractuelles avec les clients et fournisseurs.
        </p>

        <h3 class="text-purple">4. Audit interne</h3>
        <p class="textExemple">
          Évaluation du respect des politiques et procédures internes de l'organisation.
        </p>
      </section>

      <!-- Processus d'audit de conformité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Processus d'audit de conformité</h2>
        
        <div class="process-step">
          <h3 class="text-purple">1. Identification du cadre applicable</h3>
          <p class="textExemple">
            Recenser toutes les exigences légales, réglementaires, contractuelles et normatives 
            applicables au projet ou à l'organisation.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">2. Évaluation des risques de conformité</h3>
          <p class="textExemple">
            Analyser les zones à risque, prioriser les domaines critiques et définir 
            le plan d'audit en conséquence.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">3. Collecte des preuves</h3>
          <p class="textExemple">
            Rassembler la documentation, interroger les responsables, observer les processus 
            et recueillir les éléments probants.
          </p>
        </div>
        
        <div class="process-step">
          <h3 class="text-purple">4. Analyse et reporting</h3>
          <p class="textExemple">
            Évaluer les écarts, mesurer leur impact, rédiger le rapport d'audit 
            et formuler des recommandations correctives.
          </p>
        </div>
      </section>

      <!-- Degrés de gravité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Degrés de gravité des non-conformités</h2>
        
        <div class="severity-grid">
          <div class="severity-item severity-critical">
            <h4 class="text-white">CRITIQUE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Mise en danger de l'organisation</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Violation de réglementation entraînant des sanctions pénales</li>
                <li>Non-respect de clauses contractuelles critiques</li>
                <li>Manquement aux exigences de sécurité fondamentales</li>
                <li>Fraude ou malversation avérée</li>
              </ul>
              <p><strong>Action :</strong> Correction immédiate et déclaration obligatoire</p>
            </div>
          </div>
          
          <div class="severity-item severity-high">
            <h4 class="text-white">ÉLEVÉE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Risque juridique ou financier significatif</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Non-conformité réglementaire pouvant entraîner des amendes</li>
                <li>Manquement aux obligations de reporting</li>
                <li>Défaut de sécurité important</li>
                <li>Violation de propriété intellectuelle</li>
              </ul>
              <p><strong>Action :</strong> Plan de correction urgent sous 30 jours</p>
            </div>
          </div>
          
          <div class="severity-item severity-medium">
            <h4 class="text-white">MOYENNE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Risque modéré nécessitant correction</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Écart par rapport aux procédures internes</li>
                <li>Documentation incomplète ou obsolète</li>
                <li>Non-respect partiel d'une norme</li>
                <li>Défaut de traçabilité modéré</li>
              </ul>
              <p><strong>Action :</strong> Correction planifiée sous 90 jours</p>
            </div>
          </div>
          
          <div class="severity-item severity-low">
            <h4 class="text-white">FAIBLE</h4>
            <div class="severity-content">
              <p><strong>Impact :</strong> Amélioration recommandée</p>
              <p><strong>Exemples :</strong></p>
              <ul>
                <li>Écart mineur de documentation</li>
                <li>Amélioration possible d'un processus</li>
                <li>Non-conformité esthétique ou cosmétique</li>
                <li>Opportunité d'amélioration continue</li>
              </ul>
              <p><strong>Action :</strong> Correction optionnelle ou amélioration future</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Cadres réglementaires courants -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Cadres réglementaires et normatifs courants</h2>
        
        <div class="regulatory-grid">
          <div class="regulatory-item">
            <h4 class="text-purple">🔒 RGPD</h4>
            <p><strong>Protection des données personnelles</strong></p>
            <ul>
              <li>Consentement explicite</li>
              <li>Droit à l'effacement</li>
              <li>Notification des violations</li>
              <li>Privacy by design</li>
            </ul>
          </div>
          
          <div class="regulatory-item">
            <h4 class="text-purple">💳 PCI DSS</h4>
            <p><strong>Sécurité des données cartes</strong></p>
            <ul>
              <li>Chiffrement des données</li>
              <li>Contrôle d'accès strict</li>
              <li>Surveillance des réseaux</li>
              <li>Tests de sécurité réguliers</li>
            </ul>
          </div>
          
          <div class="regulatory-item">
            <h4 class="text-purple">🏥 HIPAA</h4>
            <p><strong>Santé aux États-Unis</strong></p>
            <ul>
              <li>Protection des données médicales</li>
              <li>Confidentialité patient</li>
              <li>Sécurité des échanges</li>
              <li>Audit trail obligatoire</li>
            </ul>
          </div>
          
          <div class="regulatory-item">
            <h4 class="text-purple">📊 SOX</h4>
            <p><strong>Gouvernance d'entreprise</strong></p>
            <ul>
              <li>Contrôles financiers</li>
              <li>Certification des états</li>
              <li>Traçabilité des processus</li>
              <li>Documentation des contrôles</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Méthodologies d'audit -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Méthodologies d'audit de conformité</h2>
        
        <h3 class="text-purple">Approche par risques</h3>
        <p class="textExemple">
          Concentration des efforts d'audit sur les zones présentant le plus grand risque 
          de non-conformité et d'impact pour l'organisation.
        </p>
        
        <h3 class="text-purple">Vérification par échantillonnage</h3>
        <p class="textExemple">
          Sélection d'un échantillon représentatif pour vérifier la conformité 
          sans avoir à examiner l'ensemble des éléments.
        </p>
        
        <h3 class="text-purple">Tests de conformité</h3>
        <p class="textExemple">
          Exécution de procédures spécifiques pour vérifier le respect 
          d'exigences particulières.
        </p>

        <h3 class="text-purple">Revue de documentation</h3>
        <p class="textExemple">
          Examen systématique des politiques, procédures, registres et rapports 
          pour s'assurer de leur conformité.
        </p>
      </section>

      <!-- Outils d'audit de conformité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils d'audit de conformité</h2>
        
        <h3 class="text-purple">Gestion de la conformité</h3>
        <ul>
          <li><strong>Logiciel GRC</strong> : RSA Archer, SAP GRC, MetricStream</li>
          <li><strong>Plateformes dédiées</strong> : OneTrust, TrustArc, LogicGate</li>
          <li><strong>Solutions cloud</strong> : ServiceNow GRC, IBM OpenPages</li>
        </ul>
        
        <h3 class="text-purple">Documentation et reporting</h3>
        <ul>
          <li><strong>Gestion documentaire</strong> : SharePoint, Confluence, Documentum</li>
          <li><strong>Création de rapports</strong> : Microsoft Office, LaTeX, Power BI</li>
          <li><strong>Gestion des preuves</strong> : CaseWare, AuditFile</li>
        </ul>
        
        <h3 class="text-purple">Collaboration</h3>
        <ul>
          <li><strong>Suivi des actions</strong> : JIRA, Trello, Asana</li>
          <li><strong>Communication sécurisée</strong> : Microsoft Teams, Slack Enterprise</li>
          <li><strong>Stockage sécurisé</strong> : Box, Dropbox Business, OneDrive</li>
        </ul>
      </section>

      <!-- Exemples de checklist -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples de checklist de conformité</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Checklist RGPD - Traitement des données</h4>
            <pre><code><span class="comment">// Conformité RGPD - Article 5</span>
<span class="number">□</span> Finalité du traitement clairement définie
<span class="number">□</span> Base légale identifiée et documentée
<span class="number">□</span> Données collectées limitées au nécessaire
<span class="number">□</span> Exactitude des données vérifiée
<span class="number">□</span> Durée de conservation définie
<span class="number">□</span> Sécurité appropriée mise en œuvre
<span class="number">□</span> Registre des traitement à jour
<span class="number">□</span> DPO désigné et contactable
<span class="number">□</span> AIPD réalisée si nécessaire
<span class="number">□</span> Procédure de violation documentée</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Checklist Sécurité - ISO 27001</h4>
            <pre><code><span class="comment">// Contrôles de sécurité informatique</span>
<span class="number">□</span> Politique de sécurité documentée
<span class="number">□</span> Analyse des risques réalisée
<span class="number">□</span> Contrôle d'accès physique effectif
<span class="number">□</span> Authentification multi-facteurs
<span class="number">□</span> Chiffrement des données sensibles
<span class="number">□</span> Sauvegardes régulières testées
<span class="number">□</span> Plan de reprise activité opérationnel
<span class="number">□</span> Journalisation des événements
<span class="number">□</span> Formation sécurité des employés
<span class="number">□</span> Revue de sécurité périodique</code></pre>
          </div>
        </div>
      </section>

      <!-- Métriques de conformité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Métriques de performance de conformité</h2>
        
        <div class="metrics-grid">
          <div class="metric-item">
            <h4 class="text-purple">Taux de conformité global</h4>
            <p>Pourcentage d'exigences conformes par rapport au total des exigences applicables.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Délai moyen de correction</h4>
            <p>Temps moyen entre l'identification d'une non-conformité et sa correction effective.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Taux de récidive</h4>
            <p>Pourcentage de non-conformités récurrentes malgré les actions correctives.</p>
          </div>
          
          <div class="metric-item">
            <h4 class="text-purple">Couverture réglementaire</h4>
            <p>Pourcentage du cadre réglementaire couvert par les contrôles en place.</p>
          </div>
        </div>
      </section>

      <!-- Intégration dans le cycle de projet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Intégration dans le cycle de projet</h2>
        
        <h3 class="text-purple">Phase d'initialisation</h3>
        <p class="textExemple">
          Identification des exigences de conformité applicables au projet, 
          intégration dans le cahier des charges et analyse des risques réglementaires.
        </p>
        
        <h3 class="text-purple">Phase de planification</h3>
        <p class="textExemple">
          Définition des contrôles de conformité, allocation des ressources dédiées 
          et planification des audits intermédiaires.
        </p>
        
        <h3 class="text-purple">Phase d'exécution</h3>
        <p class="textExemple">
          Surveillance continue de la conformité, documentation des preuves 
          et mise en œuvre des actions correctives.
        </p>

        <h3 class="text-purple">Phase de clôture</h3>
        <p class="textExemple">
          Audit final de conformité, archivage des preuves et capitalisation 
          des bonnes pratiques pour les projets futurs.
        </p>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Audit de conformité RGPD</h3>
          <p class="textExemple">
            Vous êtes chargé de réaliser un audit de conformité RGPD pour une application 
            de gestion des ressources humaines. Réalisez les étapes suivantes :
          </p>
          <ol>
            <li>Identifiez les 10 exigences RGPD principales applicables</li>
            <li>Créez une grille d'évaluation avec critères de conformité</li>
            <li>Simulez la collecte de preuves pour 3 processus clés</li>
            <li>Évaluez le niveau de conformité et identifiez les écarts</li>
            <li>Rédigez un plan d'action correctif priorisé</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir un exemple de solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Rapport d'audit RGPD - Application RH</h4>
              <p><strong>Application :</strong> Système de gestion du personnel "HRSoft"</p>
              <p><strong>Date :</strong> [Date de l'audit]</p>
              
              <h4 class="text-purple">Non-conformités identifiées :</h4>
              <div class="severity-examples">
                <div class="severity-example critical">
                  <strong>Critique :</strong> Absence de registre des traitement - Article 30 RGPD
                </div>
                <div class="severity-example high">
                  <strong>Élevée :</strong> Données sensibles non chiffrées - Article 32 RGPD
                </div>
                <div class="severity-example medium">
                  <strong>Moyenne :</strong> Délai de conservation non défini - Article 5 RGPD
                </div>
                <div class="severity-example low">
                  <strong>Faible :</strong> Formulaire de consentement peu clair - Article 7 RGPD
                </div>
              </div>
              
              <h4 class="text-purple">Plan d'action prioritaire :</h4>
              <ul>
                <li>Créer et maintenir le registre des traitement (CRITIQUE - 15 jours)</li>
                <li>Implémenter le chiffrement AES-256 pour les données sensibles (ÉLEVÉE - 30 jours)</li>
                <li>Définir les durées de conservation par type de données (MOYENNE - 60 jours)</li>
                <li>Améliorer la clarté des formulaires de consentement (FAIBLE - 90 jours)</li>
              </ul>

              <h4 class="text-purple">Métriques de conformité :</h4>
              <ul>
                <li><strong>Taux de conformité global :</strong> 65%</li>
                <li><strong>Exigences critiques conformes :</strong> 40%</li>
                <li><strong>Délai moyen de correction estimé :</strong> 45 jours</li>
                <li><strong>Risque réglementaire :</strong> Élevé</li>
              </ul>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <p class="text-white">
          L'audit de conformité représente bien plus qu'une obligation réglementaire - c'est un pilier 
          essentiel de la gouvernance d'entreprise et de la gestion des risques. Dans un environnement 
          réglementaire de plus en plus complexe, il constitue un avantage compétitif et un gage de 
          pérennité pour les organisations.
        </p>
        
        <h3 class="text-white">Valeur stratégique</h3>
        <p class="text-white">
          Au-delà de la simple conformité, un programme d'audit bien structuré permet d'anticiper 
          les évolutions réglementaires, de renforcer la confiance des parties prenantes et de 
          protéger la réputation de l'organisation. Il transforme la contrainte réglementaire 
          en opportunité d'amélioration continue.
        </p>
        
        <h3 class="text-white">Culture de conformité</h3>
        <p class="text-white">
          Les organisations matures intègrent la conformité dans leur ADN, faisant de chaque 
          collaborateur un acteur de la conformité. Cette culture partagée réduit considérablement 
          les risques et optimise l'efficacité des contrôles.
        </p>
        
        <h3 class="text-white">Approche proactive</h3>
        <p class="text-white">
          L'audit de conformité ne doit pas être perçu comme une activité punitive mais comme 
          un outil d'amélioration continue. Une approche proactive permet d'identifier les 
          écarts potentiels avant qu'ils ne deviennent des violations, réduisant ainsi les 
          coûts de correction et les impacts négatifs.
        </p>
        
        <p class="text-white">
          En faisant de l'audit de conformité une pratique intégrée et valorisée, les organisations 
          s'assurent non seulement de leur conformité aux exigences, mais aussi de leur résilience 
          face aux évolutions réglementaires et de leur excellence opérationnelle durable.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ComplianceAuditLesson',
  head() {
    return {
      title: 'Audit de Conformité - Gestion de Projet',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Leçon complète sur les audits de conformité dans la gestion de projet : réglementations, normes, méthodologies et bonnes pratiques.'
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

/* Grille réglementaire */
.regulatory-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.regulatory-item {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    border-left: 4px solid #8B5FBF;
}

.regulatory-item h4 {
    margin-top: 0;
    margin-bottom: 0.5rem;
}

.regulatory-item p {
    font-weight: 600;
    margin-bottom: 1rem;
    color: #6A3093;
}

.regulatory-item ul {
    margin: 0;
    padding-left: 1.2rem;
}

.regulatory-item li {
    margin-bottom: 0.3rem;
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
    
    .regulatory-grid {
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