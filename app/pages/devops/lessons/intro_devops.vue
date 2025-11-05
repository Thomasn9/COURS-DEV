<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Introduction au DevOps</h1>
                <p class="lesson-meta text-white">
                    Automatisation, collaboration et déploiement continu dans le développement web
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le DevOps ?</h2>
                <p class="textExemple">
                    Le DevOps est une culture, une philosophie et un ensemble de pratiques qui visent à
                    rapprocher les équipes de développement (Dev) et d'exploitation (Ops). L'objectif
                    principal est de réduire le cycle de vie du développement des applications tout en
                    assurant une livraison continue de haute qualité.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Les 5 piliers du DevOps :</h3>
                    <ul>
                        <li><strong>Culture</strong> : Collaboration entre Dev et Ops</li>
                        <li><strong>Automatisation</strong> : Réduction des tâches manuelles</li>
                        <li><strong>Mesure</strong> : Métriques et monitoring</li>
                        <li><strong>Partage</strong> : Communication et transparence</li>
                        <li><strong>Lean</strong> : Amélioration continue</li>
                    </ul>
                </div>
            </section>

            <!-- Cycle de vie DevOps -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le Cycle de Vie DevOps</h2>
                <p class="textExemple">
                    Le cycle de vie DevOps suit un processus en boucle continue, souvent représenté
                    par l'infini (∞), comprenant les phases suivantes :
                </p>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Planification</h3>
                        <p>Définition des fonctionnalités, suivi des bugs, gestion des projets avec des outils comme
                            Jira, Trello ou Azure DevOps</p>
                    </div>

                    <div>
                        <h3 class="text-purple">Développement</h3>
                        <p>Codage, révision, intégration continue utilisant Git, GitHub, GitLab ou Bitbucket</p>
                    </div>
                </div>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Livraison</h3>
                        <p>Gestion des artefacts, déploiement continu avec Docker, Kubernetes ou Jenkins</p>
                    </div>

                    <div>
                        <h3 class="text-purple">Exploitation</h3>
                        <p>Monitoring, gestion des incidents, maintenance utilisant Prometheus, Grafana ou New Relic</p>
                    </div>
                </div>
            </section>

            <!-- CI/CD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">CI/CD : Cœur du DevOps</h2>
                <p class="textExemple">
                    L'Intégration Continue (CI) et le Déploiement Continu (CD) sont les pratiques
                    fondamentales du DevOps qui automatisent le processus de livraison des applications.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Intégration Continue (CI)</h3>
                    <p>L'intégration continue automatise la construction et les tests à chaque modification de code.
                        Chaque fois qu'un développeur pousse du code, le système CI construit automatiquement
                        l'application
                        et exécute tous les tests pour détecter rapidement les erreurs.</p>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Déploiement Continu (CD)</h3>
                    <p>Le déploiement continu prend le relais après l'intégration continue en automatisant
                        le déploiement vers différents environnements (staging, production). Cela permet de livrer
                        rapidement et fréquemment de nouvelles fonctionnalités aux utilisateurs.</p>
                </div>
            </section>

            <!-- Infrastructure as Code -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Infrastructure as Code (IaC)</h2>
                <p class="textExemple">
                    L'IaC permet de gérer et provisionner l'infrastructure via du code plutôt que
                    par des processus manuels, rendant l'infrastructure reproductible et versionnée.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Avantages de l'IaC</h3>
                    <ul>
                        <li><strong>Reproductibilité</strong> : Même infrastructure à chaque déploiement</li>
                        <li><strong>Versioning</strong> : Suivi des changements d'infrastructure</li>
                        <li><strong>Automatisation</strong> : Provisionnement automatique des ressources</li>
                        <li><strong>Consistance</strong> : Environnements identiques entre dev et prod</li>
                    </ul>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Outils populaires</h3>
                    <p>Terraform, Ansible, CloudFormation, Docker et Kubernetes permettent de définir
                        l'infrastructure sous forme de code, facilitant la gestion et la scalabilité.</p>
                </div>
            </section>

            <!-- Monitoring et Observability -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Monitoring et Observabilité</h2>
                <p class="textExemple">
                    Le monitoring permet de surveiller la santé des applications en production,
                    tandis que l'observabilité donne la capacité de comprendre ce qui se passe
                    à l'intérieur du système à partir de ses sorties externes.
                </p>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Métriques Clés</h3>
                        <ul>
                            <li><strong>Latence</strong> : Temps de réponse des requêtes</li>
                            <li><strong>Trafic</strong> : Nombre de demandes par seconde</li>
                            <li><strong>Erreurs</strong> : Taux d'échec des requêtes</li>
                            <li><strong>Saturation</strong> : Utilisation des ressources (CPU, mémoire)</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Outils Populaires</h3>
                        <ul>
                            <li>Prometheus + Grafana pour les métriques</li>
                            <li>Datadog pour le monitoring complet</li>
                            <li>New Relic pour les performances applicatives</li>
                            <li>ELK Stack pour les logs et l'analyse</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Avantages du DevOps -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages du DevOps</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Pour les équipes</h3>
                        <ul>
                            <li>Délais de livraison réduits</li>
                            <li>Meilleure collaboration entre équipes</li>
                            <li>Résolution rapide des problèmes</li>
                            <li>Environnements de travail plus stables</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Pour l'entreprise</h3>
                        <ul>
                            <li>Time-to-market accéléré</li>
                            <li>Réduction des coûts d'exploitation</li>
                            <li>Amélioration de la qualité logicielle</li>
                            <li>Meilleure satisfaction client</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Conclusion et ressources -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et Ressources</h2>
                <p class="textExemple">
                    Le DevOps n'est pas seulement un ensemble d'outils, mais une culture de collaboration
                    et d'amélioration continue. En adoptant les pratiques DevOps, les équipes peuvent
                    livrer des logiciels plus rapidement, plus fiables et avec une meilleure qualité.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Ressources pour Approfondir</h3>
                    <ul>
                        <li><strong>Livres</strong> : "The Phoenix Project", "The DevOps Handbook"</li>
                        <li><strong>Formations</strong> : AWS DevOps, Azure DevOps, Google Cloud DevOps</li>
                        <li><strong>Certifications</strong> : Docker Certified Associate, Kubernetes CKAD/CKA</li>
                        <li><strong>Communautés</strong> : DevOps subreddit, DevOps conferences</li>
                    </ul>
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
}

/* POUR LES TRÈS PETITS ÉCRANS */
@media (max-width: 480px) {
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