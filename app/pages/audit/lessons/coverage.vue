<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Couverture dans le Contexte d'un Audit</h1>
        <p class="lesson-meta text-white">Audit • Métriques • Exhaustivité • Qualité de l'évaluation</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à la couverture d'audit</h2>
        <p class="textExemple">
          La couverture d'audit représente l'étendue et la profondeur de l'examen réalisé lors d'un processus d'audit.
          Elle mesure le degré d'exhaustivité avec lequel les différents aspects du système, processus ou produit
          ont été évalués par rapport au périmètre défini.
        </p>
        <p class="textExemple">
          Une couverture adéquate est essentielle pour garantir la fiabilité des conclusions d'audit
          et la détection effective des risques et non-conformités.
        </p>
      </section>

      <!-- Objectifs de la couverture d'audit -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs de la mesure de couverture</h2>
        <ul>
          <li><strong>Évaluer l'exhaustivité</strong> : Mesurer la proportion du périmètre effectivement audité</li>
          <li><strong>Garantir la représentativité</strong> : S'assurer que l'échantillon couvre tous les aspects
            critiques</li>
          <li><strong>Optimiser les ressources</strong> : Allouer efficacement le temps et les moyens d'audit</li>
          <li><strong>Démontrer la diligence</strong> : Fournir des preuves de l'étendue des vérifications</li>
          <li><strong>Améliorer la planification</strong> : Ajuster les futurs audits basés sur les couvertures
            réalisées</li>
        </ul>
      </section>

      <!-- Types de couverture -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de couverture d'audit</h2>

        <h3 class="text-purple">1. Couverture fonctionnelle</h3>
        <p class="textExemple">
          Pourcentage des fonctionnalités, processus métier ou cas d'usage couverts par les tests d'audit.
        </p>

        <h3 class="text-purple">2. Couverture technique</h3>
        <p class="textExemple">
          Étendue de l'examen des composants techniques, de l'infrastructure et des aspects architecturaux.
        </p>

        <h3 class="text-purple">3. Couverture des risques</h3>
        <p class="textExemple">
          Proportion des risques identifiés dans la cartographie qui ont fait l'objet de vérifications spécifiques.
        </p>

        <h3 class="text-purple">4. Couverture réglementaire</h3>
        <p class="textExemple">
          Pourcentage des exigences légales et normatives applicables qui ont été vérifiées durant l'audit.
        </p>
      </section>

      <!-- Processus de mesure de couverture -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Processus de mesure de la couverture</h2>

        <div class="process-step">
          <h3 class="text-purple">1. Définition du périmètre total</h3>
          <p class="textExemple">
            Identifier et documenter l'ensemble des éléments devant être couverts par l'audit
            (fonctionnalités, processus, risques, exigences).
          </p>
        </div>

        <div class="process-step">
          <h3 class="text-purple">2. Échantillonnage et planification</h3>
          <p class="textExemple">
            Sélectionner les éléments à auditer en fonction des critères de risque,
            de criticité et de représentativité.
          </p>
        </div>

        <div class="process-step">
          <h3 class="text-purple">3. Exécution et traçabilité</h3>
          <p class="textExemple">
            Réaliser les vérifications d'audit tout en documentant systématiquement
            les éléments couverts et les preuves collectées.
          </p>
        </div>

        <div class="process-step">
          <h3 class="text-purple">4. Calcul et analyse</h3>
          <p class="textExemple">
            Mesurer les taux de couverture obtenus, analyser les écarts
            et évaluer l'impact sur la confiance dans les conclusions.
          </p>
        </div>
      </section>

      <!-- Niveaux de couverture acceptables -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Niveaux de couverture acceptables</h2>

        <div class="severity-grid">
          <div class="severity-item severity-excellent">
            <h4 class="text-white">EXCELLENTE</h4>
            <div class="severity-content">
              <p><strong>Couverture :</strong> 90-100%</p>
              <p><strong>Contexte d'application :</strong></p>
              <ul>
                <li>Audits réglementaires critiques</li>
                <li>Systèmes de sécurité/sécurité de vie</li>
                <li>Certifications majeures</li>
                <li>Due diligence d'acquisition</li>
              </ul>
              <p><strong>Confiance :</strong> Très élevée - conclusions hautement fiables</p>
            </div>
          </div>

          <div class="severity-item severity-good">
            <h4 class="text-white">BONNE</h4>
            <div class="severity-content">
              <p><strong>Couverture :</strong> 75-89%</p>
              <p><strong>Contexte d'application :</strong></p>
              <ul>
                <li>Audits internes standards</li>
                <li>Contrôles qualité périodiques</li>
                <li>Revues de projet importantes</li>
                <li>Audits de conformité majeurs</li>
              </ul>
              <p><strong>Confiance :</strong> Élevée - conclusions fiables</p>
            </div>
          </div>

          <div class="severity-item severity-moderate">
            <h4 class="text-white">MODÉRÉE</h4>
            <div class="severity-content">
              <p><strong>Couverture :</strong> 50-74%</p>
              <p><strong>Contexte d'application :</strong></p>
              <ul>
                <li>Audits exploratoires</li>
                <li>Évaluations préliminaires</li>
                <li>Contrôles de routine</li>
                <li>Surveillance continue</li>
              </ul>
              <p><strong>Confiance :</strong> Modérée - conclusions avec réserves</p>
            </div>
          </div>

          <div class="severity-item severity-poor">
            <h4 class="text-white">INSUFFISANTE</h4>
            <div class="severity-content">
              <p><strong>Couverture :</strong> &lt; 50%</p>
              <p><strong>Contexte d'application :</strong></p>
              <ul>
                <li>Échantillons pilotes</li>
                <li>Tests de faisabilité</li>
                <li>Audits limités par le temps</li>
                <li>Évaluations à haut niveau</li>
              </ul>
              <p><strong>Confiance :</strong> Faible - conclusions non définitives</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Techniques d'échantillonnage -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Techniques d'échantillonnage pour optimiser la couverture</h2>

        <div class="sampling-grid">
          <div class="sampling-item">
            <h4 class="text-purple">📊 Échantillonnage aléatoire</h4>
            <p><strong>Utilisation :</strong> Population homogène</p>
            <ul>
              <li>Sélection aléatoire d'éléments</li>
              <li>Représentativité statistique</li>
              <li>Risque de manquer des éléments critiques</li>
              <li>Calcul simple de la couverture</li>
            </ul>
          </div>

          <div class="sampling-item">
            <h4 class="text-purple">🎯 Échantillonnage dirigé par le risque</h4>
            <p><strong>Utilisation :</strong> Optimisation des ressources</p>
            <ul>
              <li>Focus sur les zones à haut risque</li>
              <li>Couverture prioritaire des éléments critiques</li>
              <li>Efficacité accrue de l'audit</li>
              <li>Calcul de couverture pondéré</li>
            </ul>
          </div>

          <div class="sampling-item">
            <h4 class="text-purple">🔍 Échantillonnage systématique</h4>
            <p><strong>Utilisation :</strong> Grands volumes</p>
            <ul>
              <li>Sélection à intervalle régulier</li>
              <li>Couverture étendue de la population</li>
              <li>Répartition uniforme</li>
              <li>Facile à planifier et exécuter</li>
            </ul>
          </div>

          <div class="sampling-item">
            <h4 class="text-purple">📈 Échantillonnage stratifié</h4>
            <p><strong>Utilisation :</strong> Populations hétérogènes</p>
            <ul>
              <li>Division en sous-groupes homogènes</li>
              <li>Échantillonnage par strate</li>
              <li>Représentativité garantie</li>
              <li>Calcul de couverture par segment</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Méthodes de calcul -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Méthodes de calcul de la couverture</h2>

        <h3 class="text-purple">Couverture simple</h3>
        <div class="code-example">
          <pre><code><span class="comment">// Calcul de base</span>
<span class="variable">Couverture</span> = (<span class="variable">Éléments vérifiés</span> / <span class="variable">Éléments totaux</span>) × 100

<span class="comment">// Exemple : Audit d'une application avec 150 fonctionnalités</span>
<span class="variable">Fonctionnalités totales</span> = 150
<span class="variable">Fonctionnalités testées</span> = 112
<span class="variable">Couverture fonctionnelle</span> = (112 / 150) × 100 = <span class="number">74.7%</span></code></pre>
        </div>

        <h3 class="text-purple">Couverture pondérée</h3>
        <div class="code-example">
          <pre><code><span class="comment">// Prise en compte de la criticité</span>
<span class="variable">Couverture pondérée</span> = Σ(<span class="variable">Poids</span> × <span class="variable">Couverture segment</span>)

<span class="comment">// Exemple avec pondération par risque</span>
<span class="variable">Fonctionnalités critiques</span> (poids 0.6) : 20/20 testées → 100%
<span class="variable">Fonctionnalités majeures</span> (poids 0.3) : 45/60 testées → 75%
<span class="variable">Fonctionnalités mineures</span> (poids 0.1) : 47/70 testées → 67%

<span class="variable">Couverture pondérée</span> = (0.6×100) + (0.3×75) + (0.1×67) = <span class="number">87.7%</span></code></pre>
        </div>
      </section>

      <!-- Outils de mesure -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils de mesure et suivi de la couverture</h2>

        <h3 class="text-purple">Gestion des tests</h3>
        <ul>
          <li><strong>JIRA + Xray</strong> : Suivi de la couverture des exigences</li>
          <li><strong>TestRail</strong> : Reporting avancé de couverture de test</li>
          <li><strong>qTest</strong> : Métriques de couverture en temps réel</li>
        </ul>

        <h3 class="text-purple">Analyse de code</h3>
        <ul>
          <li><strong>SonarQube</strong> : Couverture du code et des branches</li>
          <li><strong>JaCoCo</strong> : Couverture des tests unitaires</li>
          <li><strong>Coverage.py</strong> : Couverture Python</li>
        </ul>

        <h3 class="text-purple">Tableaux de bord</h3>
        <ul>
          <li><strong>Power BI</strong> : Visualisation des métriques de couverture</li>
          <li><strong>Grafana</strong> : Monitoring en temps réel</li>
          <li><strong>Excel avancé</strong> : Calculs personnalisés et rapports</li>
        </ul>
      </section>

      <!-- Exemples de matrices de couverture -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples de matrices de couverture</h2>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Matrice de couverture fonctionnelle</h4>
            <pre><code><span class="comment">// Application de gestion des ventes</span>
<span class="variable">Module</span>          | <span class="variable">Fonctionnalités</span> | <span class="variable">Testées</span> | <span class="variable">Couverture</span>
<span class="variable">Gestion clients</span>  | 25              | 22       | <span class="number">88%</span>
<span class="variable">Gestion produits</span> | 18              | 15       | <span class="number">83%</span>
<span class="variable">Ventes</span>           | 35              | 28       | <span class="number">80%</span>
<span class="variable">Reporting</span>        | 12              | 8        | <span class="number">67%</span>
<span class="variable">TOTAL</span>           | 90              | 73       | <span class="number">81%</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">Matrice de couverture des risques</h4>
            <pre><code><span class="comment">// Audit de sécurité informatique</span>
<span class="variable">Catégorie de risque</span> | <span class="variable">Risques</span> | <span class="variable">Contrôlés</span> | <span class="variable">Couverture</span>
<span class="variable">Accès illégitime</span>   | 8       | 7          | <span class="number">88%</span>
<span class="variable">Perte de données</span>   | 6       | 4          | <span class="number">67%</span>
<span class="variable">Non-conformité</span>     | 5       | 3          | <span class="number">60%</span>
<span class="variable">Disponibilité</span>      | 4       | 4          | <span class="number">100%</span>
<span class="variable">TOTAL</span>              | 23      | 18         | <span class="number">78%</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Métriques de performance -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Métriques de performance de couverture</h2>

        <div class="metrics-grid">
          <div class="metric-item">
            <h4 class="text-purple">Taux de couverture global</h4>
            <p>Pourcentage moyen de couverture sur l'ensemble du périmètre d'audit.</p>
          </div>

          <div class="metric-item">
            <h4 class="text-purple">Couverture des éléments critiques</h4>
            <p>Pourcentage spécifique de couverture des éléments à haut risque ou haute criticité.</p>
          </div>

          <div class="metric-item">
            <h4 class="text-purple">Densité de couverture</h4>
            <p>Nombre de tests ou vérifications par élément audité, mesurant la profondeur.</p>
          </div>

          <div class="metric-item">
            <h4 class="text-purple">Écart de couverture</h4>
            <p>Différence entre la couverture planifiée et la couverture réellement atteinte.</p>
          </div>
        </div>
      </section>

      <!-- Facteurs influençant la couverture -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Facteurs influençant la couverture d'audit</h2>

        <h3 class="text-purple">Contraintes de ressources</h3>
        <p class="textExemple">
          Le temps disponible, le budget alloué et les compétences de l'équipe d'audit
          impactent directement l'étendue de la couverture réalisable.
        </p>

        <h3 class="text-purple">Complexité du sujet</h3>
        <p class="textExemple">
          La complexité technique, l'étendue fonctionnelle et l'interconnexion des systèmes
          influencent la profondeur d'analyse possible.
        </p>

        <h3 class="text-purple">Accessibilité des informations</h3>
        <p class="textExemple">
          La disponibilité des documentations, l'accès aux systèmes et la collaboration
          des audités conditionnent l'exhaustivité des vérifications.
        </p>

        <h3 class="text-purple">Objectifs de l'audit</h3>
        <p class="textExemple">
          La nature de l'audit (réglementaire, interne, certification) détermine
          le niveau de couverture requis et acceptable.
        </p>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>

        <div class="exercise">
          <h3 class="text-purple">Planification de la couverture d'audit</h3>
          <p class="textExemple">
            Vous devez planifier un audit de sécurité pour une application web de commerce électronique.
            L'audit doit être réalisé en 5 jours avec une équipe de 2 auditeurs. Réalisez les étapes suivantes :
          </p>
          <ol>
            <li>Identifiez les 5 domaines principaux à couvrir</li>
            <li>Estimez le nombre d'éléments par domaine</li>
            <li>Définissez une stratégie d'échantillonnage adaptée</li>
            <li>Calculez la couverture cible réaliste</li>
            <li>Établissez un plan de priorisation</li>
          </ol>

          <details class="solution">
            <summary class="btn-purple btn-hover">Voir un exemple de solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Plan de couverture - Audit sécurité e-commerce</h4>
              <p><strong>Application :</strong> Plateforme "ShopSecure"</p>
              <p><strong>Contraintes :</strong> 5 jours × 2 auditeurs = 80 heures-homme</p>

              <h4 class="text-purple">Domaines et couverture planifiée :</h4>
              <div class="coverage-examples">
                <div class="coverage-example critical">
                  <strong>Authentification (CRITIQUE) :</strong> 15 éléments → 100% cible (15 éléments)
                </div>
                <div class="coverage-example high">
                  <strong>Paiement (ÉLEVÉ) :</strong> 20 éléments → 80% cible (16 éléments)
                </div>
                <div class="coverage-example medium">
                  <strong>Données clients (MOYEN) :</strong> 25 éléments → 60% cible (15 éléments)
                </div>
                <div class="coverage-example low">
                  <strong>Interface admin (FAIBLE) :</strong> 30 éléments → 40% cible (12 éléments)
                </div>
              </div>

              <h4 class="text-purple">Stratégie d'échantillonnage :</h4>
              <ul>
                <li><strong>Échantillonnage dirigé par le risque</strong> pour les domaines critiques</li>
                <li><strong>Échantillonnage systématique</strong> pour les domaines à volume élevé</li>
                <li><strong>Couverture pondérée cible :</strong> 85% (basé sur la criticité)</li>
                <li><strong>Éléments totaux à auditer :</strong> 58 sur 90 (64% de couverture brute)</li>
              </ul>

              <h4 class="text-purple">Répartition temporelle :</h4>
              <ul>
                <li><strong>Authentification :</strong> 25 heures (31% du temps)</li>
                <li><strong>Paiement :</strong> 20 heures (25% du temps)</li>
                <li><strong>Données clients :</strong> 20 heures (25% du temps)</li>
                <li><strong>Interface admin :</strong> 15 heures (19% du temps)</li>
              </ul>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        <p class="text-white">
          La couverture d'audit est bien plus qu'une simple métrique quantitative - elle représente
          l'épine dorsale de la crédibilité et de la fiabilité des conclusions d'audit. Une couverture
          bien planifiée et correctement mesurée transforme un exercice de conformité en une évaluation
          stratégique porteuse de valeur ajoutée.
        </p>

        <h3 class="text-white">Équilibre optimal</h3>
        <p class="text-white">
          L'art de l'audit consiste à trouver l'équilibre parfait entre l'exhaustivité de la couverture
          et l'efficacité des ressources. Une couverture à 100% n'est ni toujours nécessaire, ni souvent
          réalisable, mais une couverture ciblée et stratégique garantit que les risques majeurs sont
          identifiés et que les conclusions sont fondées.
        </p>

        <h3 class="text-white">Approche adaptative</h3>
        <p class="text-white">
          Les auditeurs expérimentés adaptent continuellement leur approche de couverture en fonction
          des découvertes faites durant l'audit. Cette flexibilité permet de réallouer les efforts
          vers les zones présentant le plus grand potentiel de risque ou de non-conformité.
        </p>

        <h3 class="text-white">Transparence et communication</h3>
        <p class="text-white">
          La communication claire des limites de couverture et des méthodologies d'échantillonnage
          utilisées renforce la confiance dans les résultats d'audit. Cette transparence permet
          aux parties prenantes de comprendre précisément la portée et les limites des conclusions présentées.
        </p>

        <p class="text-white">
          En maîtrisant les concepts de couverture d'audit, les professionnels transforment une contrainte
          opérationnelle en un levier stratégique, garantissant que chaque heure d'audit contribue
          maximalement à la réduction des risques et à l'amélioration des processus organisationnels.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AuditCoverageLesson',
  head() {
    return {
      title: 'Couverture d\'Audit - Gestion de Projet',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Leçon complète sur la couverture dans le contexte d\'audit : méthodes de mesure, échantillonnage, métriques et bonnes pratiques.'
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
.code-example,
.code-block {
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
  /* Permet le retour à la ligne */
  word-wrap: break-word;
  /* Casse les mots longs */
  word-break: break-word;
  /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
  display: block;
  white-space: pre-wrap;
  /* Retour à la ligne automatique */
  overflow-x: auto;
  max-width: 100%;
  width: 100%;
  word-wrap: break-word;
  word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword {
  color: #c586c0 !important;
}

/* Mots-clés (for, while, if, function, etc.) */
.variable {
  color: #9cdcfe !important;
}

/* Variables et noms de fonctions */
.string {
  color: #ce9178 !important;
}

/* Chaînes de caractères */
.comment {
  color: #6a9955 !important;
}

/* Commentaires */
.function {
  color: #dcdcaa !important;
}

/* Noms de fonctions */
.operator {
  color: #d4d4d4 !important;
}

/* Opérateurs (+, -, =, =>, etc.) */
.constant {
  color: #4fc1ff !important;
}

/* Constantes */
.number {
  color: #b5cea8 !important;
}

/* Nombres */
.class-name {
  color: #4ec9b0 !important;
}

/* Noms de classes */

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
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.metric-item h4 {
  margin-top: 0;
}

/* Niveaux de couverture */
.severity-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.severity-item {
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
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

.severity-excellent {
  border: 2px solid #28a745;
}

.severity-excellent h4 {
  background: #28a745;
}

.severity-good {
  border: 2px solid #20c997;
}

.severity-good h4 {
  background: #20c997;
}

.severity-moderate {
  border: 2px solid #ffc107;
}

.severity-moderate h4 {
  background: #ffc107;
  color: #212529 !important;
}

.severity-poor {
  border: 2px solid #fd7e14;
}

.severity-poor h4 {
  background: #fd7e14;
}

/* Grille d'échantillonnage */
.sampling-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.sampling-item {
  padding: 1.5rem;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #8B5FBF;
}

.sampling-item h4 {
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.sampling-item p {
  font-weight: 600;
  margin-bottom: 1rem;
  color: #6A3093;
}

.sampling-item ul {
  margin: 0;
  padding-left: 1.2rem;
}

.sampling-item li {
  margin-bottom: 0.3rem;
}

/* Exemples de couverture dans la solution */
.coverage-examples {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin: 1rem 0;
}

.coverage-example {
  padding: 0.75rem;
  border-radius: 6px;
  border-left: 4px solid;
}

.coverage-example.critical {
  background: #d1e7dd;
  border-left-color: #28a745;
}

.coverage-example.high {
  background: #d1ecf1;
  border-left-color: #17a2b8;
}

.coverage-example.medium {
  background: #fff3cd;
  border-left-color: #ffc107;
}

.coverage-example.low {
  background: #f8d7da;
  border-left-color: #dc3545;
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

  .sampling-grid {
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

.lesson-section:nth-child(1) {
  animation-delay: 0.1s;
}

.lesson-section:nth-child(2) {
  animation-delay: 0.2s;
}

.lesson-section:nth-child(3) {
  animation-delay: 0.3s;
}

.lesson-section:nth-child(4) {
  animation-delay: 0.4s;
}

.lesson-section:nth-child(5) {
  animation-delay: 0.5s;
}
</style>