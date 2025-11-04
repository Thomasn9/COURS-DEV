<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Audit de Performance dans la Gestion de Projet</h1>
                <p class="lesson-meta text-white">Optimiser l'efficacité et la réussite de vos projets</p>
            </header>

            <!-- Section 1 : Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux audits de performance</h2>
                <p class="textExemple">
                    L'audit de performance est un processus systématique d'évaluation qui permet de mesurer l'efficacité
                    d'un projet par rapport aux objectifs fixés. Il identifie les écarts entre les performances
                    attendues
                    et réelles, et propose des recommandations pour améliorer l'efficience du projet.
                </p>
                <p class="textExemple">
                    Dans un contexte de gestion de projet, l'audit de performance ne se limite pas à l'analyse
                    financière,
                    mais englobe tous les aspects : délais, qualité, ressources, risques et satisfaction des parties
                    prenantes.
                </p>
            </section>

            <!-- Section 2 : Objectifs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Objectifs d'un audit de performance</h2>
                <ul>
                    <li><strong>Évaluer l'efficacité</strong> : Mesurer dans quelle mesure les objectifs du projet sont
                        atteints</li>
                    <li><strong>Identifier les écarts</strong> : Repérer les différences entre le planifié et le réalisé
                    </li>
                    <li><strong>Analyser les causes</strong> : Comprendre les raisons des écarts de performance</li>
                    <li><strong>Proposer des correctifs</strong> : Recommander des actions d'amélioration</li>
                    <li><strong>Capitaliser sur les bonnes pratiques</strong> : Identifier et partager les réussites
                    </li>
                </ul>
            </section>

            <!-- Section 3 : Méthodologie -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodologie d'audit de performance</h2>

                <h3 class="text-purple">1. Phase de préparation</h3>
                <p class="textExemple">
                    Définir le périmètre, les objectifs spécifiques, les critères d'évaluation et constituer l'équipe
                    d'audit.
                </p>

                <h3 class="text-purple">2. Collecte des données</h3>
                <p class="textExemple">
                    Rassembler toutes les informations pertinentes : documents de projet, rapports, entretiens avec
                    l'équipe, etc.
                </p>

                <h3 class="text-purple">3. Analyse des données</h3>
                <p class="textExemple">
                    Examiner les écarts, identifier les causes racines, évaluer l'impact sur les objectifs du projet.
                </p>

                <h3 class="text-purple">4. Rédaction du rapport</h3>
                <p class="textExemple">
                    Présenter les constats, les conclusions et les recommandations d'amélioration.
                </p>

                <h3 class="text-purple">5. Suivi des actions</h3>
                <p class="textExemple">
                    Vérifier la mise en œuvre des recommandations et mesurer leur efficacité.
                </p>
            </section>

            <!-- Section 4 : Indicateurs de performance DÉTAILLÉE -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Indicateurs Clés de Performance (KPI) détaillés</h2>

                <p class="textExemple">
                    Les KPI sont des mesures quantifiables qui permettent d'évaluer la performance d'un projet
                    par rapport à ses objectifs stratégiques. Ils doivent être SMART : Spécifiques, Mesurables,
                    Atteignables, Réalistes et Temporels.
                </p>

                <!-- Indicateurs de délais -->
                <div class="code-example">
                    <h3 class="text-purple">📅 Indicateurs de délais et planning</h3>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Écart de Planning (Schedule Variance - SV)</h4>
                            <p><strong>Formule :</strong> SV = Valeur Acquise (EV) - Valeur Planifiée (PV)</p>
                            <p><strong>Interprétation :</strong></p>
                            <ul>
                                <li>SV > 0 : Projet en avance</li>
                                <li>SV = 0 : Projet dans les temps</li>
                                <li>SV < 0 : Projet en retard</li>
                            </ul>

                            <h4 class="text-purple">Indice de Performance des Délais (SPI)</h4>
                            <p><strong>Formule :</strong> SPI = EV / PV</p>
                            <p><strong>Interprétation :</strong></p>
                            <ul>
                                <li>SPI > 1 : Performance positive</li>
                                <li>SPI = 1 : Performance conforme</li>
                                <li>SPI < 1 : Performance négative</li>
                            </ul>
                        </div>

                        <div>
                            <div class="code-block">
                                <pre><code>// Exemple de calcul en JavaScript
function calculateSchedulePerformance(earnedValue, plannedValue) {
  const SV = earnedValue - plannedValue;
  const SPI = earnedValue / plannedValue;
  
  return {
    scheduleVariance: SV,
    schedulePerformanceIndex: SPI,
    status: SPI >= 1 ? "Dans les temps" : "En retard"
  };
}

// Données du projet
const earnedValue = 425000; // Valeur du travail accompli
const plannedValue = 500000; // Valeur du travail planifié

const performance = calculateSchedulePerformance(earnedValue, plannedValue);
console.log(performance);
// Résultat: { scheduleVariance: -75000, schedulePerformanceIndex: 0.85, status: "En retard" }</code></pre>
                            </div>
                        </div>
                    </div>

                    <h4 class="text-purple">Autres indicateurs de délais :</h4>
                    <ul>
                        <li><strong>Taux d'avancement réel :</strong> Pourcentage de travail accompli vs total</li>
                        <li><strong>Délai moyen par tâche :</strong> Temps moyen pour compléter une tâche</li>
                        <li><strong>Respect des jalons :</strong> Pourcentage de jalons respectés dans les temps</li>
                    </ul>
                </div>

                <!-- Indicateurs de coûts -->
                <div class="code-example">
                    <h3 class="text-purple">💰 Indicateurs de coûts et budget</h3>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Écart de Coût (Cost Variance - CV)</h4>
                            <p><strong>Formule :</strong> CV = Valeur Acquise (EV) - Coût Réel (AC)</p>
                            <p><strong>Interprétation :</strong></p>
                            <ul>
                                <li>CV > 0 : Sous le budget</li>
                                <li>CV = 0 : Dans le budget</li>
                                <li>CV < 0 : Dépassement budgétaire</li>
                            </ul>

                            <h4 class="text-purple">Indice de Performance des Coûts (CPI)</h4>
                            <p><strong>Formule :</strong> CPI = EV / AC</p>
                            <p><strong>Interprétation :</strong></p>
                            <ul>
                                <li>CPI > 1 : Coût efficace</li>
                                <li>CPI = 1 : Coût conforme</li>
                                <li>CPI < 1 : Dépenses excessives</li>
                            </ul>

                            <h4 class="text-purple">Estimation à Terminaison (EAC)</h4>
                            <p><strong>Formule :</strong> EAC = Budget à Terminaison (BAC) / CPI</p>
                            <p>Estime le coût total du projet en se basant sur la performance actuelle.</p>
                        </div>

                        <div>
                            <div class="code-block">
                                <pre><code>// Calcul complet des indicateurs financiers
class ProjectFinancialMetrics {
  constructor(budgetAtCompletion, earnedValue, actualCost) {
    this.BAC = budgetAtCompletion;
    this.EV = earnedValue;
    this.AC = actualCost;
  }
  
  calculateCostVariance() {
    return this.EV - this.AC;
  }
  
  calculateCostPerformanceIndex() {
    return this.EV / this.AC;
  }
  
  calculateEstimateAtCompletion() {
    const CPI = this.calculateCostPerformanceIndex();
    return this.BAC / CPI;
  }
  
  calculateVarianceAtCompletion() {
    const EAC = this.calculateEstimateAtCompletion();
    return this.BAC - EAC;
  }
  
  generateReport() {
    const CV = this.calculateCostVariance();
    const CPI = this.calculateCostPerformanceIndex();
    const EAC = this.calculateEstimateAtCompletion();
    const VAC = this.calculateVarianceAtCompletion();
    
    return {
      costVariance: CV,
      costPerformanceIndex: CPI.toFixed(2),
      estimateAtCompletion: EAC,
      varianceAtCompletion: VAC,
      status: CPI >= 1 ? "✅ Dans le budget" : "⚠️ Dépassement"
    };
  }
}

// Utilisation
const project = new ProjectFinancialMetrics(1000000, 425000, 480000);
console.log(project.generateReport());</code></pre>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Indicateurs de qualité -->
                <div class="code-example">
                    <h3 class="text-purple">🎯 Indicateurs de qualité</h3>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Métriques de défauts</h4>
                            <ul>
                                <li><strong>Taux de défauts :</strong> Nombre de défauts / unité de travail</li>
                                <li><strong>Densité de défauts :</strong> Défauts par point de fonction ou ligne de code
                                </li>
                                <li><strong>Temps moyen entre défaillances :</strong> Fiabilité du produit</li>
                            </ul>

                            <h4 class="text-purple">Indicateurs de processus</h4>
                            <ul>
                                <li><strong>Taux de rework :</strong> Pourcentage de travail refait</li>
                                <li><strong>Efficacité des tests :</strong> Pourcentage de défauts détectés avant
                                    livraison</li>
                                <li><strong>Conformité aux standards :</strong> Respect des normes qualité</li>
                            </ul>
                        </div>

                        <div>
                            <div class="code-block">
                                <pre><code>// Tableau de bord qualité
const qualityMetrics = {
  defects: {
    totalDefects: 15,
    criticalDefects: 3,
    majorDefects: 7,
    minorDefects: 5,
    calculateDefectDensity: function(functionPoints) {
      return this.totalDefects / functionPoints;
    },
    calculateCriticalDefectRate: function() {
      return (this.criticalDefects / this.totalDefects) * 100;
    }
  },
  
  testing: {
    testCasesExecuted: 450,
    testCasesPassed: 420,
    defectsFoundInTesting: 12,
    defectsFoundInProduction: 3,
    calculateTestEffectiveness: function() {
      return (this.defectsFoundInTesting / 
             (this.defectsFoundInTesting + this.defectsFoundInProduction)) * 100;
    },
    calculateTestPassRate: function() {
      return (this.testCasesPassed / this.testCasesExecuted) * 100;
    }
  },
  
  customerSatisfaction: {
    surveyScore: 4.2, // sur 5
    netPromoterScore: 35, // NPS
    supportTickets: 24,
    calculateSatisfactionLevel: function() {
      if (this.surveyScore >= 4.5) return "Excellent";
      if (this.surveyScore >= 4.0) return "Bon";
      if (this.surveyScore >= 3.0) return "Moyen";
      return "Faible";
    }
  }
};

// Génération du rapport qualité
console.log("=== RAPPORT QUALITÉ ===");
console.log(`Densité de défauts: ${qualityMetrics.defects.calculateDefectDensity(1000).toFixed(2)}`);
console.log(`Taux de défauts critiques: ${qualityMetrics.defects.calculateCriticalDefectRate().toFixed(1)}%`);
console.log(`Efficacité des tests: ${qualityMetrics.testing.calculateTestEffectiveness().toFixed(1)}%`);
console.log(`Taux de réussite tests: ${qualityMetrics.testing.calculateTestPassRate().toFixed(1)}%`);
console.log(`Niveau satisfaction: ${qualityMetrics.customerSatisfaction.calculateSatisfactionLevel()}`);</code></pre>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Indicateurs des ressources -->
                <div class="code-example">
                    <h3 class="text-purple">👥 Indicateurs des ressources humaines</h3>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Productivité</h4>
                            <ul>
                                <li><strong>Velocity (Agile) :</strong> Points d'histoire complétés par sprint</li>
                                <li><strong>Taux d'utilisation :</strong> Pourcentage du temps productif</li>
                                <li><strong>Output par ressource :</strong> Livrables par personne/mois</li>
                            </ul>

                            <h4 class="text-purple">Engagement et rétention</h4>
                            <ul>
                                <li><strong>Taux de turnover :</strong> Pourcentage de départ de l'équipe</li>
                                <li><strong>Satisfaction de l'équipe :</strong> Résultats d'enquêtes internes</li>
                                <li><strong>Taux d'absentéisme :</strong> Jours d'absence non planifiés</li>
                            </ul>
                        </div>

                        <div>
                            <div class="code-block">
                                <pre><code>// Analyse des ressources et productivité
class TeamPerformance {
  constructor(teamMembers, sprintDuration) {
    this.teamMembers = teamMembers;
    this.sprintDuration = sprintDuration;
    this.sprintData = [];
  }
  
  addSprint(storyPointsCompleted, actualHours, plannedHours) {
    this.sprintData.push({
      storyPointsCompleted,
      actualHours,
      plannedHours,
      velocity: storyPointsCompleted,
      utilization: (actualHours / plannedHours) * 100,
      efficiency: storyPointsCompleted / actualHours
    });
  }
  
  calculateAverageVelocity() {
    const totalVelocity = this.sprintData.reduce((sum, sprint) => sum + sprint.velocity, 0);
    return totalVelocity / this.sprintData.length;
  }
  
  calculateTeamProductivity() {
    const avgVelocity = this.calculateAverageVelocity();
    const avgEfficiency = this.sprintData.reduce((sum, sprint) => sum + sprint.efficiency, 0) / this.sprintData.length;
    
    return {
      averageVelocity: avgVelocity.toFixed(1),
      averageEfficiency: avgEfficiency.toFixed(2),
      teamCapacity: avgVelocity * this.teamMembers,
      performanceLevel: avgVelocity > 20 ? "Élevée" : avgVelocity > 15 ? "Moyenne" : "Faible"
    };
  }
  
  generateResourceReport() {
    const productivity = this.calculateTeamProductivity();
    const avgUtilization = this.sprintData.reduce((sum, sprint) => sum + sprint.utilization, 0) / this.sprintData.length;
    
    return {
      ...productivity,
      averageUtilization: `${avgUtilization.toFixed(1)}%`,
      recommendedTeamSize: Math.ceil(productivity.teamCapacity / 25) // Basé sur capacité cible
    };
  }
}

// Exemple d'utilisation
const devTeam = new TeamPerformance(8, 2); // 8 personnes, sprints de 2 semaines
devTeam.addSprint(85, 520, 640); // 85 points, 520h réelles, 640h planifiées
devTeam.addSprint(92, 580, 640);
devTeam.addSprint(78, 510, 640);

console.log(devTeam.generateResourceReport());</code></pre>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Tableau de bord consolidé -->
                <div class="code-example">
                    <h3 class="text-purple">📊 Tableau de bord de performance consolidé</h3>

                    <div class="code-block">
                        <pre><code>// Tableau de bord exécutif
const executiveDashboard = {
  project: "Digital Transformation v2.0",
  period: "Q3 2024",
  
  kpiSummary: {
    schedule: { spi: 0.85, target: 1.0, weight: 0.3 },
    cost: { cpi: 0.73, target: 1.0, weight: 0.3 },
    quality: { defectRate: 2.1, target: 1.5, weight: 0.2 },
    resources: { utilization: 78, target: 85, weight: 0.1 },
    risks: { exposure: 42, target: 25, weight: 0.1 }
  },
  
  calculateOverallHealth: function() {
    const kpis = this.kpiSummary;
    let score = 0;
    
    // Calcul score planning
    score += Math.max(0, kpis.schedule.spi / kpis.schedule.target) * kpis.schedule.weight * 100;
    
    // Calcul score coûts
    score += Math.max(0, kpis.cost.cpi / kpis.cost.target) * kpis.cost.weight * 100;
    
    // Calcul score qualité (inversé car moins de défauts = mieux)
    score += Math.max(0, (kpis.quality.target / kpis.quality.defectRate)) * kpis.quality.weight * 100;
    
    // Calcul score ressources
    score += (kpis.resources.utilization / kpis.resources.target) * kpis.resources.weight * 100;
    
    // Calcul score risques (inversé car moins d'exposition = mieux)
    score += Math.max(0, (kpis.risks.target / kpis.risks.exposure)) * kpis.risks.weight * 100;
    
    return {
      score: Math.min(100, score),
      details: {
        schedule: `${(kpis.schedule.spi * 100).toFixed(0)}%`,
        cost: `${(kpis.cost.cpi * 100).toFixed(0)}%`,
        quality: `${kpis.quality.defectRate}%`,
        resources: `${kpis.resources.utilization}%`,
        risks: kpis.risks.exposure
      }
    };
  },
  
  generateExecutiveReport: function() {
    const metrics = this.calculateOverallHealth();
    const health = metrics.score >= 80 ? "✅ Excellent" : metrics.score >= 60 ? "⚠️ Moyen" : "❌ Critique";
    
    return {
      project: this.project,
      period: this.period,
      overallStatus: health,
      healthScore: `${metrics.score.toFixed(1)}%`,
      kpiDetails: metrics.details,
      recommendations: this.generateRecommendations()
    };
  },
  
  generateRecommendations: function() {
    const kpis = this.kpiSummary;
    const recommendations = [];
    
    if (kpis.schedule.spi < 0.9) {
      recommendations.push("Accélérer les livraisons critiques et réviser le planning");
    }
    
    if (kpis.cost.cpi < 0.8) {
      recommendations.push("Contrôler strictement les dépenses et optimiser les ressources");
    }
    
    if (kpis.quality.defectRate > kpis.quality.target) {
      recommendations.push("Renforcer les revues de code et les tests automatisés");
    }
    
    if (kpis.risks.exposure > kpis.risks.target) {
      recommendations.push("Mettre en œuvre des plans de mitigation pour les risques élevés");
    }
    
    return recommendations;
  }
};

// Génération du rapport exécutif
console.log("=== TABLEAU DE BORD EXÉCUTIF ===");
const report = executiveDashboard.generateExecutiveReport();
console.log(report);</code></pre>
                    </div>

                    <div class="solution">
                        <details>
                            <summary class="btn-purple btn-hover">📋 Checklist : Implémentation des KPI</summary>
                            <div class="solution-content">
                                <h4 class="text-purple">Étapes pour une mise en œuvre efficace :</h4>

                                <ol>
                                    <li><strong>Identifier les KPI alignés avec les objectifs stratégiques</strong></li>
                                    <li><strong>Définir des cibles réalistes et mesurables</strong></li>
                                    <li><strong>Mettre en place un système de collecte automatisé</strong></li>
                                    <li><strong>Établir des fréquences de reporting adaptées</strong></li>
                                    <li><strong>Former les équipes à l'interprétation des KPI</strong></li>
                                    <li><strong>Créer des tableaux de bord visuels et accessibles</strong></li>
                                    <li><strong>Revue régulière et ajustement des KPI</strong></li>
                                </ol>

                                <h4 class="text-purple">Pièges à éviter :</h4>
                                <ul>
                                    <li>❌ Trop de KPI qui noient l'information essentielle</li>
                                    <li>❌ KPI non actionnables sans pouvoir de décision</li>
                                    <li>❌ Focus exclusif sur les résultats sans analyse des causes</li>
                                    <li>❌ Absence de contexte pour interpréter les variations</li>
                                </ul>
                            </div>
                        </details>
                    </div>
                </div>
            </section>

            <!-- Section 5 : Outils d'audit -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils et techniques d'audit</h2>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Outils d'analyse quantitative</h4>
                        <ul>
                            <li>Analyse de la valeur acquise (Earned Value Management)</li>
                            <li>Diagrammes de Gantt comparatifs</li>
                            <li>Tableaux de bord de performance</li>
                            <li>Analyse des écarts</li>
                            <li>Courbes de tendance</li>
                        </ul>
                    </div>

                    <div>
                        <h4 class="text-purple">Outils d'analyse qualitative</h4>
                        <ul>
                            <li>Entretiens individuels et collectifs</li>
                            <li>Questionnaires de satisfaction</li>
                            <li>Analyse SWOT</li>
                            <li>Diagramme causes-effets (Ishikawa)</li>
                            <li>Matrice de compétences</li>
                        </ul>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">🛠️ Outils logiciels recommandés</h4>
                    <ul>
                        <li><strong>JIRA</strong> : Suivi agile et reporting</li>
                        <li><strong>Microsoft Project</strong> : Planification et suivi</li>
                        <li><strong>Tableau/Power BI</strong> : Tableaux de bord visuels</li>
                        <li><strong>Excel/Sheets</strong> : Analyses personnalisées</li>
                        <li><strong>Smartsheet</strong> : Collaboration et reporting</li>
                    </ul>
                </div>
            </section>

            <!-- Section 6 : Exemple de rapport d'audit -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure type d'un rapport d'audit</h2>

                <div class="code-block">
                    <pre><code>RAPPORT D'AUDIT DE PERFORMANCE
Projet: Digital Transformation
Période: Janvier - Mars 2024
Date d'audit: 15 Avril 2024

1. SYNTHÈSE EXÉCUTIVE
   - Objectifs de l'audit: Évaluer la performance du projet après 6 mois
   - Principaux constats: Retard de 15%, dépassement budgétaire de 12%
   - Recommandations majeures: Révision planning, optimisation ressources

2. CONTEXTE ET MÉTHODOLOGIE
   - Périmètre: Phases 1 à 3 du projet
   - Méthodes: Analyse documents, entretiens, observation
   - Équipe d'audit: 3 auditeurs certifiés

3. ANALYSE DES PERFORMANCES
   3.1. Performance sur les délais
     - État d'avancement: 70% réalisé vs 85% planifié
     - Écarts identifiés: Retard cumulé de 45 jours
     - Causes des écarts: Changements de scope non contrôlés
   
   3.2. Performance sur les coûts
     - Budget consommé: 480K€ vs 425K€ planifié
     - Évolution des coûts: Dérive progressive depuis M3
     - Facteurs d'écarts: Heures supplémentaires, réwork
   
   3.3. Performance sur la qualité
     - Respect des spécifications: 88%
     - Satisfaction client: 7.2/10
     - Points d'amélioration: Processus de test

4. RECOMMANDATIONS
   - Actions prioritaires (2 semaines):
     * Gel des changements de scope
     * Révision du plan de projet
   - Actions moyen terme (1 mois):
     * Mise en place de revues qualité
     * Formation équipe aux bonnes pratiques

5. ANNEXES
   - Données détaillées de performance
   - Grilles d'entretien utilisées
   - Documents de référence analysés</code></pre>
                </div>
            </section>

            <!-- Section 7 : Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Cas d'étude : Projet "Digital Transformation"</h3>
                    <p class="textExemple">
                        Vous êtes chargé d'auditer le projet "Digital Transformation" de l'entreprise Innovatech.
                        Le projet, initialement prévu sur 12 mois avec un budget de 500 000€, en est à son 10ème mois.
                    </p>

                    <p class="textExemple">
                        <strong>Données disponibles :</strong><br>
                        - Budget à terminaison (BAC) : 500 000€<br>
                        - Budget consommé (AC) : 480 000€<br>
                        - Valeur acquise (EV) : 350 000€<br>
                        - Valeur planifiée (PV) : 425 000€<br>
                        - Travail planifié : 85%<br>
                        - Travail réellement accompli : 70%<br>
                        - 3 retours clients négatifs sur les livrables récents<br>
                        - 2 membres clés de l'équipe ont quitté le projet au 6ème mois
                    </p>

                    <p class="textExemple">
                        <strong>Questions :</strong><br>
                        1. Calculez les indicateurs de performance des délais (SV, SPI) et des coûts (CV, CPI)<br>
                        2. Calculez l'estimation à terminaison (EAC) et la variance à terminaison (VAC)<br>
                        3. Identifiez les principaux problèmes de performance<br>
                        4. Proposez 3 recommandations d'amélioration prioritaires
                    </p>
                </div>

                <div class="solution">
                    <details>
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Réponses suggérées :</h4>

                            <p><strong>1. Calcul des indicateurs :</strong></p>
                            <ul>
                                <li>Écart de planning (SV) = EV - PV = 350 000€ - 425 000€ = <strong>-75 000€</strong>
                                </li>
                                <li>Indice de performance des délais (SPI) = EV / PV = 350 000€ / 425 000€ =
                                    <strong>0,82</strong></li>
                                <li>Écart de coût (CV) = EV - AC = 350 000€ - 480 000€ = <strong>-130 000€</strong></li>
                                <li>Indice de performance des coûts (CPI) = EV / AC = 350 000€ / 480 000€ =
                                    <strong>0,73</strong></li>
                            </ul>

                            <p><strong>2. Projections :</strong></p>
                            <ul>
                                <li>Estimation à terminaison (EAC) = BAC / CPI = 500 000€ / 0,73 = <strong>684
                                        931€</strong></li>
                                <li>Variance à terminaison (VAC) = BAC - EAC = 500 000€ - 684 931€ = <strong>-184
                                        931€</strong></li>
                            </ul>

                            <p><strong>3. Problèmes identifiés :</strong></p>
                            <ul>
                                <li>Retard important (SPI = 0,82 < 1)</li>
                                <li>Dépassement budgétaire significatif (CPI = 0,73 < 1)</li>
                                <li>Problèmes de qualité (retours clients négatifs)</li>
                                <li>Instabilité de l'équipe (départs de membres clés)</li>
                                <li>Dérive des coûts projetée à +37%</li>
                            </ul>

                            <p><strong>4. Recommandations prioritaires :</strong></p>
                            <ol>
                                <li>Organiser un atelier de replanification avec réévaluation des objectifs</li>
                                <li>Mettre en place un comité de contrôle des changements strict</li>
                                <li>Renforcer l'équipe avec des ressources expérimentées et mettre en place un plan de
                                    rétention</li>
                            </ol>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Section 8 : Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques pour un audit réussi</h2>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ À faire</h4>
                        <ul>
                            <li><strong>Préparer minutieusement</strong> : Définir clairement le périmètre et les
                                objectifs</li>
                            <li><strong>Communiquer transparent</strong> : Expliquer le processus à toutes les parties
                                prenantes</li>
                            <li><strong>Être factuel</strong> : Baser les conclusions sur des données tangibles</li>
                            <li><strong>Proposer des solutions</strong> : Associer chaque constat à des recommandations
                            </li>
                            <li><strong>Assurer le suivi</strong> : Vérifier la mise en œuvre des actions correctives
                            </li>
                        </ul>
                    </div>

                    <div>
                        <h4 class="text-purple">❌ À éviter</h4>
                        <ul>
                            <li><strong>Juger sans preuves</strong> : Éviter les conclusions hâtives</li>
                            <li><strong>Pointer des personnes</strong> : Se concentrer sur les processus, pas les
                                individus</li>
                            <li><strong>Négliger le contexte</strong> : Prendre en compte les contraintes externes</li>
                            <li><strong>Surcharger le rapport</strong> : Prioriser l'information essentielle</li>
                            <li><strong>Oublier les réussites</strong> : Mettre en valeur les bonnes pratiques</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Section 9 : Conclusion -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Conclusion</h2>
                <p class="text-white">
                    L'audit de performance est un outil essentiel pour améliorer continuellement la gestion de projet.
                    Il permet non seulement d'identifier les problèmes, mais aussi de valoriser les bonnes pratiques
                    et de renforcer les capacités de l'organisation à mener ses projets avec succès.
                </p>
                <p class="text-white">
                    Un audit bien mené crée de la valeur en transformant les constats en actions d'amélioration
                    concrètes,
                    contribuant ainsi à la réussite des projets futurs et au développement des compétences des équipes.
                </p>
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

.text-center {
    text-align: center;
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