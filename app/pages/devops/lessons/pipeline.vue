<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Pipeline CI/CD : pilier du DevOps</h1>
                <p class="lesson-meta text-white">DevOps • CI/CD • Automatisation • Intégration continue • Livraison continue</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu’est‑ce qu’un pipeline ?</h2>
                <p class="textExemple">
                    Un <strong>pipeline CI/CD</strong> est une séquence automatisée d’étapes exécutées à chaque modification du code source (commit, pull request). Il incarne les principes fondamentaux du <strong>DevOps</strong> : casser les silos entre développement et exploitation, et accélérer la livraison de valeur tout en garantissant la qualité.
                </p>
                <p class="textExemple">
                    Dans un workflow DevOps, le pipeline prend en charge des tâches comme la compilation, les tests, l’analyse statique, la construction d’images, le déploiement et la surveillance. Il rend le processus reproductible, traçable et fiable.
                </p>
            </section>

            <!-- Pourquoi un pipeline est indispensable dans une démarche DevOps -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi un pipeline ? (Résolution des problèmes traditionnels)</h2>
                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Sans pipeline (approche classique)</h3>
                        <ul>
                            <li>Compilation manuelle par chaque développeur → environnement hétérogène.</li>
                            <li>Tests exécutés à la demande, souvent oubliés → bugs en production.</li>
                            <li>Déploiement manuel, scripté à l’arrache → erreurs humaines fréquentes.</li>
                            <li>Feedback tardif → cycle de livraison long (plusieurs semaines).</li>
                            <li>Aucune traçabilité claire des versions.</li>
                        </ul>
                    </div>
                    <div>
                        <h3 class="text-purple">Avec pipeline (DevOps)</h3>
                        <ul>
                            <li>Automatisation totale → gain de temps et réduction des erreurs.</li>
                            <li>Tests systématiques à chaque commit → qualité garantie.</li>
                            <li>Déploiement reproductible (environnements dev/staging/prod).</li>
                            <li>Feedback immédiat pour le développeur (en quelques minutes).</li>
                            <li>Traçabilité complète : qui a changé quoi, quand, et le statut du pipeline.</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Étapes typiques d’un pipeline -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étapes classiques d’un pipeline CI/CD</h2>
                <div class="textExemple">
                    <ol class="mb-4">
                        <li><strong>Checkout</strong> : récupération du code source depuis le gestionnaire de versions (Git).</li>
                        <li><strong>Installation des dépendances</strong> (Composer, npm, pip, etc.).</li>
                        <li><strong>Linting / Analyse statique</strong> (PHPStan, ESLint, Psalm) pour détecter les erreurs potentielles.</li>
                        <li><strong>Tests unitaires et d’intégration</strong> (PHPUnit, Jest, pytest).</li>
                        <li><strong>Construction / compilation</strong> (Webpack, Docker build).</li>
                        <li><strong>Analyse de sécurité / Scan de vulnérabilités</strong> (SonarQube, Trivy).</li>
                        <li><strong>Déploiement dans un environnement de test (staging)</strong>.</li>
                        <li><strong>Tests fonctionnels / end‑to‑end</strong> (Cypress, Playwright).</li>
                        <li><strong>Déploiement en production</strong> (si la branche est main ou release).</li>
                    </ol>
                    <p>Ces étapes sont généralement définies dans un fichier de configuration (ex: <code>.gitlab-ci.yml</code>, <code>.github/workflows/ci.yml</code>).</p>
                </div>
            </section>

            <!-- Exemple concret : pipeline pour une application Symfony (GitHub Actions) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple de pipeline GitHub Actions (Symfony)</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-yaml"># .github/workflows/symfony.yml
name: Symfony CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    services:
      mysql:
        image: mysql:8.0
        env:
          MYSQL_ROOT_PASSWORD: root
          MYSQL_DATABASE: test
        ports:
          - 3306:3306
        options: --health-cmd="mysqladmin ping" --health-interval=10s --health-timeout=5s --health-retries=3

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '8.2'
          extensions: mbstring, pdo_mysql, intl
          coverage: xdebug

      - name: Install Composer dependencies
        run: composer install --no-progress --prefer-dist

      - name: Run PHPStan (static analysis)
        run: vendor/bin/phpstan analyse src --level=5

      - name: Run PHPUnit (unit & integration tests)
        run: |
          php bin/console doctrine:database:create --env=test
          php bin/console doctrine:schema:create --env=test
          php bin/console doctrine:fixtures:load --env=test --no-interaction
          php bin/phpunit
        env:
          DATABASE_URL: mysql://root:root@127.0.0.1:3306/test

      - name: Build Docker image (optionnel)
        run: docker build -t myapp/symfony:latest .</code></pre>
                </div>
                <p class="textExemple">
                    Ce pipeline s’exécute automatiquement à chaque `push` ou `pull request`. Il garantit que le code est analysé, testé et prêt à être déployé. Si une étape échoue, l’équipe est immédiatement notifiée.
                </p>
            </section>

            <!-- Bénéfices pour le workflow d’équipe -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comment un pipeline améliore le workflow collaboratif</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Intégration continue (CI)</strong> : tous les changements sont fusionnés fréquemment (plusieurs fois par jour). Le pipeline valide que l’intégration ne casse rien.</li>
                        <li><strong>Livraison continue (CD)</strong> : le pipeline peut déployer automatiquement sur un environnement de préproduction (staging) ou même en production si les tests passent.</li>
                        <li><strong>Code review efficace</strong> : la pull request affiche le statut du pipeline. Seul un code vert (passant tous les tests) peut être fusionné.</li>
                        <li><strong>Traçabilité et reproductibilité</strong> : chaque exécution est enregistrée (logs, durée, artefacts). On sait exactement ce qui a été testé et comment.</li>
                        <li><strong>Détection précoce des régressions</strong> : un test qui échoue sur la branche `develop` bloque la fusion → pas de bug en production.</li>
                    </ul>
                </div>
            </section>

            <!-- Place du pipeline dans le cycle DevOps -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le pipeline au cœur du cycle DevOps</h2>
                <p class="textExemple">
                    Le modèle DevOps illustre un cycle infini : <strong>Plan → Code → Build → Test → Release → Deploy → Operate → Monitor</strong>.
                    Le pipeline CI/CD automatise la chaîne <strong>Code → Build → Test → Release → Deploy</strong>. Il fait le lien entre le développement et l’exploitation.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-plaintext">Développeur          Pipeline CI/CD          Environnements
     │                      │                        │
     │── git push ─────────→│                        │
     │                      │──→ Build               │
     │                      │──→ Test Unités         │
     │                      │──→ Analyse statique    │
     │                      │──→ Tests intégration   │
     │                      │──→ Docker build        │
     │←─────── Succès ──────│                        │
     │                      │──→ Déploiement staging │
     │                      │                        │──→ Staging
     │                      │──→ Tests E2E           │
     │                      │──→ Déploiement prod    │
     │                      │                        │──→ Production</code></pre>
                </div>
                <p class="textExemple">
                    Les retours d’exploitation (monitoring, remontées d’erreurs) alimentent la phase <strong>Plan</strong> pour les itérations futures. Le pipeline assure une boucle de feedback accélérée.
                </p>
            </section>

            <!-- Outils populaires pour implémenter un pipeline -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Quels outils utiliser ?</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>GitHub Actions</strong> – intégré à GitHub, très flexible, grande marketplace d’actions.</li>
                        <li><strong>GitLab CI/CD</strong> – natif dans GitLab, excellent pour les auto-hébergés.</li>
                        <li><strong>Jenkins</strong> – historique, très personnalisable (mais nécessite plus d’administration).</li>
                        <li><strong>Bitbucket Pipelines</strong> – pour les équipes Bitbucket.</li>
                        <li><strong>CircleCI, Travis CI, Azure Pipelines</strong> – alternatives matures.</li>
                        <li><strong>Drone, Tekton</strong> – orientés Kubernetes.</li>
                    </ul>
                    <p>Pour une équipe Symfony classique, GitHub Actions ou GitLab CI sont des choix parfaits.</p>
                </div>
            </section>

            <!-- Bonnes pratiques pour un pipeline efficace -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li><strong>Garder le pipeline rapide</strong> : paralléliser les jobs, utiliser le cache des dépendances.</li>
                    <li><strong>Éviter les « flaky tests »</strong> : les tests non déterministes ruinent la confiance.</li>
                    <li><strong>Utiliser des environnements éphémères</strong> (conteneurs jetables) pour les tests.</li>
                    <li><strong>Sécuriser les secrets</strong> (variables d’environnement chiffrées).</li>
                    <li><strong>Définir des règles de protection sur les branches</strong> (exiger un pipeline vert avant fusion).</li>
                    <li><strong>Instrumenter le pipeline lui-même</strong> (temps d’exécution, taux de réussite).</li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Un pipeline CI/CD est bien plus qu’une simple automatisation : c’est le <strong>moteur de transformation DevOps</strong>. Il incarne la culture d’amélioration continue, de feedback rapide et de fiabilité.
                    </p>
                    <ul>
                        <li>Il libère les développeurs des tâches répétitives et chronophages.</li>
                        <li>Il sécurise le workflow en validant systématiquement chaque changement.</li>
                        <li>Il rapproche dev et ops en rendant le déploiement prévisible et documenté.</li>
                        <li>Il est la première brique pour passer d’une livraison semestrielle à des releases quotidiennes.</li>
                    </ul>
                    <p>
                        Adopter un pipeline, c’est faire un pas décisif vers une <strong>organisation agile, résiliente et compétitive</strong>. Dans les prochaines leçons, nous verrons comment intégrer des tests de sécurité automatisés (DevSecOps) et comment gérer des pipelines complexes avec des stratégies de déploiement (blue/green, canary).
                    </p>
                    <p class="mt-4 font-bold text-purple">
                        À retenir : Sans pipeline, le DevOps reste un vœu pieux ; avec un pipeline bien conçu, l’équipe devient véritablement autonome et réactive.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'DevopsPipelineLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const languages = ['yaml', 'plaintext', 'bash'];
                    let loaded = 0;
                    languages.forEach(lang => {
                        const langScript = document.createElement('script');
                        langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`;
                        langScript.onload = () => {
                            loaded++;
                            if (loaded === languages.length) resolve();
                        };
                        document.head.appendChild(langScript);
                    });
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
/* === Style identique aux leçons précédentes === */
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
    top: 0; left: 0; right: 0; bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
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

.lesson-section {
    padding: 2rem;
    margin-bottom: 2rem;
    border-radius: 15px;
    transition: all 0.3s ease;
    width: 100%;
    overflow-x: hidden;
    box-sizing: border-box;
    animation: fadeInUp 0.6s ease forwards;
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

.bg-light-purple { background-color: #f8f6ff; }

.border-purple {
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.text-purple { color: #6A3093 !important; }
.text-white  { color: white !important; }

.code-example {
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
    width: 100%;
    box-sizing: border-box;
    white-space: pre;
    margin: 0;
}

pre code {
    display: block;
    white-space: pre;
    width: 100%;
}

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

@media (max-width: 768px) {
    .lesson-container  { padding: 1rem; }
    .lesson-header     { padding: 2rem 1rem; }
    .lesson-header h1  { font-size: 2rem; }
    .lesson-section    { padding: 1.5rem; }
    .code-comparison   { grid-template-columns: 1fr; gap: 1rem; }
    pre                { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre               { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section   { padding: 1rem; }
    .lesson-header    { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}
</style>