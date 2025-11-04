<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Audit d'Architecture Logicielle</h1>
                <p class="lesson-meta text-white">Comprendre les principes, méthodes et outils d'analyse pour évaluer la
                    qualité d'une architecture</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'un audit d'architecture ?</h2>
                <p class="textExemple">
                    Un <strong>audit d'architecture</strong> est une <strong>évaluation structurée de la conception
                        technique et organisationnelle</strong>
                    d'une application ou d'un système logiciel.
                </p>

                <div class="bg-gradient-primary text-white"
                    style="padding: 1.5rem; border-radius: 10px; margin: 1.5rem 0;">
                    <h3 class="text-white">Il vise à déterminer :</h3>
                    <ul>
                        <li>Si l'architecture répond <strong>aux besoins actuels et futurs</strong> du projet</li>
                        <li>Si elle respecte les <strong>principes de conception</strong> (modularité, séparation des
                            responsabilités, scalabilité)</li>
                        <li>Si elle permet une <strong>maintenance efficace</strong> et une <strong>évolution
                                maîtrisée</strong></li>
                    </ul>
                </div>

                <div class="solution-content">
                    <h4 class="text-purple">🎯 Objectif principal</h4>
                    <p>
                        L'objectif n'est pas de juger le code ligne par ligne, mais d'analyser <strong>la structure
                            globale</strong>
                        et les <strong>choix de conception</strong>.
                    </p>
                </div>
            </section>

            <!-- Objectifs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">🎯 Objectifs d'un audit d'architecture</h2>

                <div class="code-comparison">
                    <div class="objective-card">
                        <h4 class="text-purple">📊 Évaluer la cohérence</h4>
                        <p>Vérifier que les choix d'architecture sont alignés avec les objectifs métier et techniques
                        </p>
                    </div>
                    <div class="objective-card">
                        <h4 class="text-purple">🛡️ Mesurer la robustesse</h4>
                        <p>Identifier les points de fragilité et les dépendances critiques</p>
                    </div>
                    <div class="objective-card">
                        <h4 class="text-purple">📈 Évaluer l'évolutivité</h4>
                        <p>Analyser la capacité du système à évoluer sans régression</p>
                    </div>
                    <div class="objective-card">
                        <h4 class="text-purple">💰 Contrôler la dette technique</h4>
                        <p>Identifier les compromis techniques devenus coûteux dans le temps</p>
                    </div>
                </div>
            </section>

            <!-- Périmètre -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">🧩 Périmètre d'un audit d'architecture</h2>

                <div class="scope-grid">
                    <div class="scope-item">
                        <h4 class="text-purple">🏗️ Structure logicielle</h4>
                        <p>Découpage en couches, modules, microservices, dépendances</p>
                    </div>
                    <div class="scope-item">
                        <h4 class="text-purple">🔗 Couplage et cohésion</h4>
                        <p>Relations entre modules, indépendance des composants</p>
                    </div>
                    <div class="scope-item">
                        <h4 class="text-purple">📡 Flux de données</h4>
                        <p>Circulation, transformation et stockage des informations</p>
                    </div>
                    <div class="scope-item">
                        <h4 class="text-purple">🌐 Interopérabilité</h4>
                        <p>Communication entre systèmes et services externes</p>
                    </div>
                    <div class="scope-item">
                        <h4 class="text-purple">🛡️ Sécurité et fiabilité</h4>
                        <p>Points de vulnérabilité et redondance</p>
                    </div>
                    <div class="scope-item">
                        <h4 class="text-purple">🚀 Scalabilité et performance</h4>
                        <p>Capacité de montée en charge</p>
                    </div>
                </div>
            </section>

            <!-- Méthodologie -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">🧠 Méthodologie d'un audit d'architecture</h2>

                <div class="methodology-steps">
                    <div class="step">
                        <h3 class="text-purple">1️⃣ Préparation</h3>
                        <ul>
                            <li>Définir le <strong>périmètre</strong> et les <strong>objectifs</strong></li>
                            <li>Recueillir la <strong>documentation existante</strong></li>
                            <li>Identifier les <strong>acteurs</strong></li>
                            <li>Choisir le <strong>modèle d'évaluation</strong> (ISO 25010, ATAM, SAAM)</li>
                        </ul>
                    </div>

                    <div class="step">
                        <h3 class="text-purple">2️⃣ Analyse</h3>
                        <ul>
                            <li>Étudier la <strong>topologie du système</strong></li>
                            <li>Identifier les <strong>dépendances critiques</strong></li>
                            <li>Vérifier la <strong>cohérence des flux</strong></li>
                            <li>Évaluer la <strong>résilience et sécurité</strong></li>
                        </ul>
                    </div>

                    <div class="step">
                        <h3 class="text-purple">3️⃣ Évaluation et scoring</h3>
                        <div class="evaluation-grid">
                            <div class="eval-item">
                                <strong>Cohérence</strong>
                                <p>Les choix d'architecture sont-ils homogènes ?</p>
                                <span class="score">Faible / Moyen / Fort</span>
                            </div>
                            <div class="eval-item">
                                <strong>Évolutivité</strong>
                                <p>Peut-on ajouter un module sans tout casser ?</p>
                                <span class="score">Faible / Moyen / Fort</span>
                            </div>
                            <div class="eval-item">
                                <strong>Résilience</strong>
                                <p>Que se passe-t-il si un service tombe ?</p>
                                <span class="score">Faible / Moyen / Fort</span>
                            </div>
                        </div>
                    </div>

                    <div class="step">
                        <h3 class="text-purple">4️⃣ Rapport et recommandations</h3>
                        <ul>
                            <li>Synthèse des <strong>forces et faiblesses</strong></li>
                            <li>Recommandations <strong>concrètes</strong> (court, moyen, long terme)</li>
                            <li>Proposition d'un plan de <strong>refactoring ou migration</strong></li>
                            <li>Axes de <strong>formation ou documentation</strong></li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Indicateurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">🔍 Indicateurs et critères d'évaluation</h2>

                <div class="indicators-grid">
                    <div class="indicator-card">
                        <h4 class="text-purple">📊 Complexité</h4>
                        <p><strong>Indicateurs :</strong> Nombre de dépendances, couches, modules</p>
                        <p><strong>Objectif :</strong> Évaluer la lisibilité et la modularité</p>
                    </div>
                    <div class="indicator-card">
                        <h4 class="text-purple">🎯 Cohérence</h4>
                        <p><strong>Indicateurs :</strong> Respect des patterns (MVC, DDD, hexagonale…)</p>
                        <p><strong>Objectif :</strong> Garantir une architecture claire</p>
                    </div>
                    <div class="indicator-card">
                        <h4 class="text-purple">⚡ Performance</h4>
                        <p><strong>Indicateurs :</strong> Temps de réponse global, latence inter-services</p>
                        <p><strong>Objectif :</strong> Identifier les points de ralentissement</p>
                    </div>
                    <div class="indicator-card">
                        <h4 class="text-purple">🔄 Disponibilité</h4>
                        <p><strong>Indicateurs :</strong> Taux de panne, redondance, SLA</p>
                        <p><strong>Objectif :</strong> Mesurer la robustesse</p>
                    </div>
                </div>
            </section>

            <!-- Outils -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">🧰 Outils et supports d'analyse</h2>

                <div class="tools-comparison">
                    <div>
                        <h4 class="text-purple">📐 Modélisation</h4>
                        <ul>
                            <li><strong>Draw.io, PlantUML</strong> - Visualisation de l'architecture</li>
                            <li><strong>Lucidchart, Structurizr</strong> - Diagrammes professionnels</li>
                        </ul>
                    </div>

                    <div>
                        <h4 class="text-purple">🔍 Analyse de dépendances</h4>
                        <ul>
                            <li><strong>ArchUnit, NDepend</strong> - Analyse statique des relations</li>
                            <li><strong>Dependency Cruiser</strong> - Cartographie des dépendances</li>
                        </ul>
                    </div>

                    <div>
                        <h4 class="text-purple">📊 Monitoring</h4>
                        <ul>
                            <li><strong>Grafana, Prometheus</strong> - Analyse des métriques</li>
                            <li><strong>Jaeger</strong> - Traçage distribué</li>
                        </ul>
                    </div>

                    <div>
                        <h4 class="text-purple">📚 Documentation</h4>
                        <ul>
                            <li><strong>ADRs</strong> - Architecture Decision Records</li>
                            <li><strong>MkDocs, Docusaurus</strong> - Documentation vivante</li>
                        </ul>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Exemple d'analyse avec ArchUnit</h4>
                    <pre><code class="java"><span class="keyword">public class</span> <span class="class-name">ArchitectureTest</span> {
    
    <span class="comment">// Vérifier que les services ne dépendent pas des contrôleurs</span>
    @<span class="class-name">Test</span>
    <span class="keyword">public void</span> <span class="function">services_should_not_depend_on_controllers</span>() {
        <span class="class-name">JavaClasses</span> <span class="variable">classes</span> = <span class="class-name">ClassFileImporter</span>.<span class="function">importPackages</span>(<span class="string">"com.myapp"</span>);
        
        <span class="class-name">ArchRule</span> <span class="variable">rule</span> = <span class="class-name">classes</span>()
            .<span class="function">that</span>().<span class="function">resideInPackage</span>(<span class="string">"..service.."</span>)
            .<span class="function">should</span>().<span class="function">onlyDependOnClassesThat</span>()
            .<span class="function">resideOutsideOfPackage</span>(<span class="string">"..controller.."</span>);
            
        <span class="variable">rule</span>.<span class="function">check</span>(<span class="variable">classes</span>);
    }
}</code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">💡 Bonnes pratiques issues d'un audit</h2>

                <div class="best-practices">
                    <div class="practice">
                        <h4 class="text-purple">🏗️ Modularité</h4>
                        <p><strong>Pratique :</strong> Isoler les responsabilités dans des modules autonomes</p>
                        <p><strong>Objectif :</strong> Faciliter la maintenance</p>
                    </div>
                    <div class="practice">
                        <h4 class="text-purple">🔗 Couplage</h4>
                        <p><strong>Pratique :</strong> Réduire les dépendances entre modules</p>
                        <p><strong>Objectif :</strong> Limiter les effets de bord</p>
                    </div>
                    <div class="practice">
                        <h4 class="text-purple">📚 Documentation</h4>
                        <p><strong>Pratique :</strong> Tenir à jour les diagrammes et décisions</p>
                        <p><strong>Objectif :</strong> Préserver la cohérence</p>
                    </div>
                    <div class="practice">
                        <h4 class="text-purple">🛡️ Résilience</h4>
                        <p><strong>Pratique :</strong> Utiliser des files de messages / retries</p>
                        <p><strong>Objectif :</strong> Tolérer les pannes</p>
                    </div>
                </div>
            </section>

            <!-- Livrables -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">📊 Livrables typiques d'un audit d'architecture</h2>

                <div class="deliverables">
                    <div class="deliverable">
                        <h4 class="text-white">📋 Rapport d'audit complet</h4>
                        <ul>
                            <li>Contexte et périmètre</li>
                            <li>Diagrammes et cartographie du système</li>
                            <li>Points forts et faibles identifiés</li>
                            <li>Évaluation de la dette d'architecture</li>
                        </ul>
                    </div>

                    <div class="deliverable">
                        <h4 class="text-white">📈 Tableau d'évaluation</h4>
                        <p>Score par domaine (scalabilité, sécurité, modularité, performance)</p>
                    </div>

                    <div class="deliverable">
                        <h4 class="text-white">🎯 Plan d'action et recommandations</h4>
                        <p>Refactoring, migration, documentation, formation</p>
                    </div>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">💻 Exercice pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Analyse d'une architecture monolithique</h3>
                    <p class="textExemple">
                        Vous devez auditer une application monolithique présentant les problèmes suivants :
                    </p>
                    <ul>
                        <li>Couplage fort entre les modules métier</li>
                        <li>Absence de documentation à jour</li>
                        <li>Tests difficiles à mettre en place</li>
                        <li>Temps de build de plus en plus long</li>
                    </ul>

                    <p class="textExemple">
                        Proposez une méthodologie d'audit et des recommandations d'amélioration.
                    </p>
                </div>

                <details class="solution">
                    <summary class="btn-purple">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Méthodologie recommandée :</h4>
                        <ol>
                            <li><strong>Analyse des dépendances</strong> : Identifier les cycles et couplages forts</li>
                            <li><strong>Revue de code</strong> : Évaluer la qualité et la testabilité</li>
                            <li><strong>Interview des développeurs</strong> : Comprendre les difficultés rencontrées
                            </li>
                            <li><strong>Analyse des métriques</strong> : Temps de build, couverture de tests, dette
                                technique</li>
                        </ol>

                        <h4 class="text-purple">Recommandations :</h4>
                        <ul>
                            <li>Introduire une architecture en couches clairement définies</li>
                            <li>Implémenter des tests d'intégration automatisés</li>
                            <li>Documenter les patterns d'architecture utilisés</li>
                            <li>Envisager une migration progressive vers les microservices</li>
                        </ul>
                    </div>
                </details>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">🧭 En résumé</h2>

                <div class="summary-content">
                    <blockquote class="summary-quote">
                        L'audit d'architecture vise à s'assurer que <strong>le système est solide, compréhensible,
                            évolutif et aligné sur les besoins métiers.</strong>
                    </blockquote>

                    <div class="key-points">
                        <div class="point">
                            <span class="emoji">🔍</span>
                            <p>Il met en lumière la <strong>qualité structurelle</strong> d'une application</p>
                        </div>
                        <div class="point">
                            <span class="emoji">🧱</span>
                            <p>Il évalue les <strong>dépendances, la modularité et la résilience</strong></p>
                        </div>
                        <div class="point">
                            <span class="emoji">⚙️</span>
                            <p>Il oriente les <strong>choix d'évolution</strong> pour garantir la pérennité</p>
                        </div>
                        <div class="point">
                            <span class="emoji">📈</span>
                            <p>Il s'inscrit dans une démarche <strong>continue d'amélioration technique</strong></p>
                        </div>
                    </div>

                    <div class="final-quote">
                        <p>💬 "Une bonne architecture ne se voit pas : elle rend le changement facile."</p>
                    </div>
                </div>

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

/* Couleurs VS Code pour la syntaxe Java */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés */
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

/* Opérateurs */
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

/* Styles spécifiques pour cette leçon */
.objective-card,
.scope-item,
.indicator-card,
.practice {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
    margin-bottom: 1rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.scope-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
}

.indicators-grid,
.best-practices {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
}

.methodology-steps .step {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    margin-bottom: 1.5rem;
    border-left: 4px solid #6A3093;
}

.evaluation-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
}

.eval-item {
    background: #f8f6ff;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
}

.score {
    display: block;
    background: #6A3093;
    color: white;
    padding: 0.5rem;
    border-radius: 4px;
    margin-top: 0.5rem;
    font-weight: bold;
}

.tools-comparison {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.deliverables {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
}

.deliverable {
    background: rgba(255, 255, 255, 0.1);
    padding: 1.5rem;
    border-radius: 10px;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.summary-content {
    text-align: center;
}

.summary-quote {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    font-style: italic;
    font-size: 1.2rem;
    margin-bottom: 2rem;
    border-left: 4px solid #6A3093;
}

.key-points {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin: 2rem 0;
}

.point {
    display: flex;
    align-items: center;
    gap: 1rem;
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
}

.emoji {
    font-size: 2rem;
}

.final-quote {
    background: #f8f6ff;
    padding: 1.5rem;
    border-radius: 10px;
    font-style: italic;
    text-align: center;
    margin-top: 2rem;
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

    .code-comparison,
    .scope-grid,
    .indicators-grid,
    .best-practices,
    .tools-comparison,
    .deliverables,
    .key-points {
        grid-template-columns: 1fr;
        gap: 1rem;
    }

    .evaluation-grid {
        grid-template-columns: 1fr;
    }

    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
    }

    .point {
        flex-direction: column;
        text-align: center;
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