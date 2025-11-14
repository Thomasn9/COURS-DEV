<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <div class="lesson-header">
        <h1 class="text-white">Quality Gates</h1>
        <p class="lesson-meta text-white">Portes de qualité dans le développement logiciel</p>
      </div>

      <!-- Introduction -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Quality Gates</h2>
        <p class="textExemple">
          Les Quality Gates (portes de qualité) sont des points de contrôle définis dans le cycle de développement logiciel 
          qui permettent de s'assurer que le code répond à des critères de qualité prédéfinis avant de passer à l'étape suivante.
        </p>
        <p class="textExemple">
          Ces portes servent de barrières de qualité qui empêchent la progression du code défectueux ou de mauvaise qualité 
          dans le pipeline de livraison.
        </p>
      </div>

      <!-- Objectifs des Quality Gates -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs des Quality Gates</h2>
        <ul class="textExemple">
          <li><strong>Détection précoce des défauts</strong> : Identifier les problèmes le plus tôt possible</li>
          <li><strong>Standardisation de la qualité</strong> : Appliquer des standards cohérents</li>
          <li><strong>Réduction des coûts</strong> : Éviter les corrections tardives plus coûteuses</li>
          <li><strong>Amélioration continue</strong> : Mesurer et améliorer constamment la qualité</li>
          <li><strong>Confiance dans les livraisons</strong> : Garantir la fiabilité des releases</li>
        </ul>
      </div>

      <!-- Types de Quality Gates -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de Quality Gates</h2>
        
        <h3 class="text-purple">1. Quality Gates de développement</h3>
        <p class="textExemple">
          Appliquées pendant la phase de développement, ces portes vérifient la qualité du code source.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Exemple de configuration SonarQube</h4>
          <pre><code class="yaml"><span class="comment"># sonar-project.properties</span>
<span class="variable">sonar.projectKey</span>=<span class="string">mon-projet</span>
<span class="variable">sonar.projectName</span>=<span class="string">Mon Projet</span>

<span class="comment"># Quality Gate configuration</span>
<span class="variable">sonar.qualitygate</span>=<span class="string">Strict</span>

<span class="comment"># Seuils de qualité</span>
<span class="variable">sonar.coverage.exclusions</span>=<span class="string">**/test/**,**/node_modules/**</span>
<span class="variable">sonar.cpd.exclusions</span>=<span class="string">**/test/**</span></code></pre>
        </div>

        <h3 class="text-purple">2. Quality Gates d'intégration</h3>
        <p class="textExemple">
          Vérifications effectuées lors de l'intégration continue (CI/CD).
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Exemple GitHub Actions</h4>
          <pre><code class="yaml"><span class="comment"># .github/workflows/quality-gate.yml</span>
<span class="variable">name</span>: <span class="string">Quality Gate</span>
<span class="variable">on</span>: [<span class="string">push</span>, <span class="string">pull_request</span>]

<span class="variable">jobs</span>:
  <span class="variable">quality-check</span>:
    <span class="variable">runs-on</span>: <span class="string">ubuntu-latest</span>
    <span class="variable">steps</span>:
      - <span class="variable">uses</span>: <span class="string">actions/checkout@v3</span>
      
      - <span class="variable">name</span>: <span class="string">Run tests</span>
        <span class="variable">run</span>: <span class="string">|
          npm install
          npm test
          npm run coverage</span>
      
      - <span class="variable">name</span>: <span class="string">Static analysis</span>
        <span class="variable">run</span>: <span class="string">npm run lint</span>
      
      - <span class="variable">name</span>: <span class="string">Security audit</span>
        <span class="variable">run</span>: <span class="string">npm audit</span>
      
      - <span class="variable">name</span>: <span class="string">Quality Gate</span>
        <span class="variable">run</span>: <span class="string">|
          if [ $TEST_COVERAGE -lt 80 ]; then
            echo "❌ Coverage insuffisant: $TEST_COVERAGE% (minimum 80%)"
            exit 1
          fi</span></code></pre>
        </div>

        <h3 class="text-purple">3. Quality Gates de déploiement</h3>
        <p class="textExemple">
          Contrôles effectués avant le déploiement en production.
        </p>
      </div>

      <!-- Métriques clés pour les Quality Gates -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Métriques clés pour les Quality Gates</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Métriques de qualité de code</h4>
            <ul class="textExemple">
              <li><strong>Couverture de tests</strong> : ≥ 80%</li>
              <li><strong>Dette technique</strong> : ≤ 5%</li>
              <li><strong>Duplication de code</strong> : ≤ 3%</li>
              <li><strong>Violations de règles</strong> : 0 blocantes</li>
              <li><strong>Maintenabilité</strong> : Note A/B</li>
            </ul>
          </div>
          <div>
            <h4 class="text-purple">Métriques de sécurité</h4>
            <ul class="textExemple">
              <li><strong>Vulnérabilités</strong> : 0 critiques</li>
              <li><strong>Dépendances</strong> : Aucune vulnérable</li>
              <li><strong>Code smells</strong> : ≤ 10 majeurs</li>
              <li><strong>Securité</strong> : Note A/B</li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Exemple de configuration des seuils</h4>
          <pre><code class="javascript"><span class="comment">// quality-gate.config.js</span>
<span class="keyword">module</span>.<span class="variable">exports</span> = {
  <span class="variable">testCoverage</span>: {
    <span class="variable">minimum</span>: <span class="number">80</span>,
    <span class="variable">warning</span>: <span class="number">70</span>
  },
  <span class="variable">codeDuplication</span>: {
    <span class="variable">maximum</span>: <span class="number">3</span>
  },
  <span class="variable">technicalDebt</span>: {
    <span class="variable">maximum</span>: <span class="number">5</span>
  },
  <span class="variable">security</span>: {
    <span class="variable">blockingIssues</span>: <span class="number">0</span>,
    <span class="variable">criticalIssues</span>: <span class="number">0</span>
  },
  <span class="variable">maintainability</span>: {
    <span class="variable">minimumRating</span>: <span class="string">'B'</span>
  }
};</code></pre>
        </div>
      </div>

      <!-- Implémentation avec SonarQube -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Implémentation avec SonarQube</h2>
        <p class="textExemple">
          SonarQube est l'outil le plus populaire pour implémenter des Quality Gates.
        </p>

        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Configuration Quality Gate</h4>
            <pre><code class="yaml"><span class="comment"># Quality Gate Definition</span>
<span class="variable">name</span>: <span class="string">"Strict Quality Gate"</span>

<span class="variable">conditions</span>:
  - <span class="variable">metric</span>: <span class="string">"new_coverage"</span>
    <span class="variable">op</span>: <span class="string">"LT"</span>
    <span class="variable">error</span>: <span class="string">"80"</span>
  
  - <span class="variable">metric</span>: <span class="string">"new_duplicated_lines_density"</span>
    <span class="variable">op</span>: <span class="string">"GT"</span>
    <span class="variable">error</span>: <span class="string">"3.0"</span>
  
  - <span class="variable">metric</span>: <span class="string">"new_blocker_issues"</span>
    <span class="variable">op</span>: <span class="string">"GT"</span>
    <span class="variable">error</span>: <span class="string">"0"</span>
  
  - <span class="variable">metric</span>: <span class="string">"new_vulnerabilities"</span>
    <span class="variable">op</span>: <span class="string">"GT"</span>
    <span class="variable">error</span>: <span class="string">"0"</span>
  
  - <span class="variable">metric</span>: <span class="string">"sqale_rating"</span>
    <span class="variable">op</span>: <span class="string">"GT"</span>
    <span class="variable">error</span>: <span class="string">"2"</span></code></pre>
          </div>
          <div>
            <h4 class="text-purple">Pipeline d'intégration</h4>
            <pre><code class="yaml"><span class="comment"># .gitlab-ci.yml</span>
<span class="variable">stages</span>:
  - <span class="string">test</span>
  - <span class="string">quality</span>
  - <span class="string">deploy</span>

<span class="variable">sonarqube-check</span>:
  <span class="variable">stage</span>: <span class="string">quality</span>
  <span class="variable">image</span>: <span class="string">sonarsource/sonar-scanner-cli:latest</span>
  <span class="variable">script</span>:
    - <span class="string">sonar-scanner</span>
      -<span class="string">Dsonar.projectKey=my-project</span>
      -<span class="string">Dsonar.sources=.</span>
      -<span class="string">Dsonar.host.url=$SONAR_HOST_URL</span>
      -<span class="string">Dsonar.login=$SONAR_TOKEN</span>
  <span class="variable">only</span>:
    - <span class="string">merge_requests</span>
    - <span class="string">main</span>

<span class="variable">quality-gate</span>:
  <span class="variable">stage</span>: <span class="string">quality</span>
  <span class="variable">script</span>:
    - <span class="string">|
        response=$(curl -u $SONAR_TOKEN: "$SONAR_HOST_URL/api/qualitygates/project_status?projectKey=my-project")
        status=$(echo "$response" | jq -r '.projectStatus.status')
        
        if [ "$status" != "OK" ]; then
          echo "❌ Quality Gate failed"
          exit 1
        fi</span>
  <span class="variable">needs</span>: [<span class="string">"sonarqube-check"</span>]</code></pre>
          </div>
        </div>
      </div>

      <!-- Bonnes pratiques -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques pour les Quality Gates</h2>
        <ul class="textExemple">
          <li><strong>Définir des seuils réalistes</strong> : Commencer avec des exigences atteignables</li>
          <li><strong>Impliquer toute l'équipe</strong> : Les développeurs doivent comprendre et adhérer aux règles</li>
          <li><strong>Automatiser complètement</strong> : Éviter les validations manuelles</li>
          <li><strong>Revoir régulièrement</strong> : Ajuster les seuils selon l'évolution du projet</li>
          <li><strong>Fournir un feedback rapide</strong> : Les résultats doivent être disponibles rapidement</li>
          <li><strong>Éviter les faux positifs</strong> : Configurer soigneusement les règles</li>
        </ul>
      </div>

      <!-- Exemple pratique -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Mise en place pas à pas</h2>
        
        <h3 class="text-purple">Étape 1: Configuration de base</h3>
        <div class="code-example">
          <pre><code class="bash"><span class="comment"># Installation des outils</span>
npm install --save-dev jest eslint sonar-scanner

<span class="comment"># Configuration ESLint</span>
npx eslint --init

<span class="comment"># Configuration Jest</span>
npx jest --init</code></pre>
        </div>

        <h3 class="text-purple">Étape 2: Scripts de qualité</h3>
        <div class="code-example">
          <pre><code class="json"><span class="comment">// package.json</span>
{
  <span class="string">"scripts"</span>: {
    <span class="string">"test"</span>: <span class="string">"jest"</span>,
    <span class="string">"test:coverage"</span>: <span class="string">"jest --coverage"</span>,
    <span class="string">"lint"</span>: <span class="string">"eslint src/ --ext .js,.vue"</span>,
    <span class="string">"lint:fix"</span>: <span class="string">"eslint src/ --ext .js,.vue --fix"</span>,
    <span class="string">"audit"</span>: <span class="string">"npm audit"</span>,
    <span class="string">"quality:check"</span>: <span class="string">"npm run lint && npm run test:coverage && npm audit"</span>,
    <span class="string">"sonar:scan"</span>: <span class="string">"sonar-scanner"</span>
  }
}</code></pre>
        </div>

        <h3 class="text-purple">Étape 3: Configuration CI/CD</h3>
        <div class="code-example">
          <pre><code class="yaml"><span class="comment"># .github/workflows/quality.yml</span>
<span class="variable">name</span>: <span class="string">Quality Gate</span>

<span class="variable">on</span>:
  <span class="variable">push</span>:
    <span class="variable">branches</span>: [ <span class="string">main</span>, <span class="string">develop</span> ]
  <span class="variable">pull_request</span>:
    <span class="variable">branches</span>: [ <span class="string">main</span> ]

<span class="variable">jobs</span>:
  <span class="variable">quality</span>:
    <span class="variable">runs-on</span>: <span class="string">ubuntu-latest</span>
    
    <span class="variable">steps</span>:
    - <span class="variable">uses</span>: <span class="string">actions/checkout@v3</span>
    
    - <span class="variable">name</span>: <span class="string">Setup Node.js</span>
      <span class="variable">uses</span>: <span class="string">actions/setup-node@v3</span>
      <span class="variable">with</span>:
        <span class="variable">node-version</span>: <span class="string">'18'</span>
    
    - <span class="variable">name</span>: <span class="string">Install dependencies</span>
      <span class="variable">run</span>: <span class="string">npm ci</span>
    
    - <span class="variable">name</span>: <span class="string">Run linting</span>
      <span class="variable">run</span>: <span class="string">npm run lint</span>
    
    - <span class="variable">name</span>: <span class="string">Run tests with coverage</span>
      <span class="variable">run</span>: <span class="string">npm run test:coverage</span>
    
    - <span class="variable">name</span>: <span class="string">Security audit</span>
      <span class="variable">run</span>: <span class="string">npm audit --audit-level=high</span>
    
    - <span class="variable">name</span>: <span class="string">Check coverage threshold</span>
      <span class="variable">run</span>: <span class="string">|
        COVERAGE=$(node -e "console.log(require('./coverage/coverage-summary.json').total.lines.pct)")
        if [ $(echo "$COVERAGE < 80" | bc) -eq 1 ]; then
          echo "❌ Coverage insuffisant: $COVERAGE%"
          exit 1
        fi</span></code></pre>
        </div>
      </div>

      <!-- Exercice pratique -->
      <div class="lesson-section bg-light-purple border-purple exercise">
        <h2 class="text-purple">Exercice pratique</h2>
        <p class="textExemple">
          Configurez une Quality Gate pour un projet Vue.js/Nuxt avec les exigences suivantes :
        </p>
        <ul class="textExemple">
          <li>Couverture de tests ≥ 75%</li>
          <li>0 vulnérabilités de sécurité critiques</li>
          <li>Maximum 5 code smells majeurs</li>
          <li>Duplication de code ≤ 5%</li>
          <li>Tous les tests doivent passer</li>
        </ul>

        <details class="solution">
          <summary class="btn-purple btn-hover">Voir la solution</summary>
          <div class="solution-content">
            <h4 class="text-purple">Configuration SonarQube</h4>
            <pre><code class="yaml"><span class="comment"># sonar-project.properties</span>
<span class="variable">sonar.projectKey</span>=<span class="string">vuejs-quality-gate</span>
<span class="variable">sonar.projectName</span>=<span class="string">Vue.js Quality Gate Example</span>
<span class="variable">sonar.projectVersion</span>=<span class="string">1.0</span>

<span class="variable">sonar.sources</span>=<span class="string">components,layouts,middleware,pages,plugins,store</span>
<span class="variable">sonar.tests</span>=<span class="string">test</span>
<span class="variable">sonar.test.inclusions</span>=<span class="string">test/**/*</span>

<span class="variable">sonar.javascript.lcov.reportPaths</span>=<span class="string">coverage/lcov.info</span>
<span class="variable">sonar.coverage.exclusions</span>=<span class="string">**/*.spec.js,**/node_modules/**</span>

<span class="variable">sonar.qualitygate.wait</span>=<span class="string">true</span></code></pre>

            <h4 class="text-purple">Quality Gate Definition</h4>
            <pre><code class="json">{
  <span class="string">"conditions"</span>: [
    {
      <span class="string">"metric"</span>: <span class="string">"coverage"</span>,
      <span class="string">"operator"</span>: <span class="string">"LT"</span>,
      <span class="string">"value"</span>: <span class="string">"75"</span>,
      <span class="string">"error"</span>: <span class="string">"Coverage insuffisant"</span>
    },
    {
      <span class="string">"metric"</span>: <span class="string">"vulnerabilities"</span>,
      <span class="string">"operator"</span>: <span class="string">"GT"</span>,
      <span class="string">"value"</span>: <span class="string">"0"</span>,
      <span class="string">"error"</span>: <span class="string">"Vulnérabilités critiques détectées"</span>
    },
    {
      <span class="string">"metric"</span>: <span class="string">"code_smells"</span>,
      <span class="string">"operator"</span>: <span class="string">"GT"</span>,
      <span class="string">"value"</span>: <span class="string">"5"</span>,
      <span class="string">"error"</span>: <span class="string">"Trop de code smells majeurs"</span>
    },
    {
      <span class="string">"metric"</span>: <span class="string">"duplicated_lines_density"</span>,
      <span class="string">"operator"</span>: <span class="string">"GT"</span>,
      <span class="string">"value"</span>: <span class="string">"5.0"</span>,
      <span class="string">"error"</span>: <span class="string">"Duplication de code trop élevée"</span>
    }
  ]
}</code></pre>

            <h4 class="text-purple">Script de vérification</h4>
            <pre><code class="javascript"><span class="comment">// scripts/check-quality-gate.js</span>
<span class="keyword">const</span> <span class="variable">exec</span> = <span class="function">require</span>(<span class="string">'child_process'</span>).<span class="variable">execSync</span>;

<span class="keyword">function</span> <span class="function">checkQualityGate</span>() {
  <span class="keyword">try</span> {
    <span class="comment">// Exécuter les tests</span>
    <span class="function">exec</span>(<span class="string">'npm test'</span>, { <span class="variable">stdio</span>: <span class="string">'inherit'</span> });
    
    <span class="comment">// Vérifier la couverture</span>
    <span class="keyword">const</span> coverage = <span class="function">exec</span>(<span class="string">'node -e "console.log(require(\\'./coverage/coverage-summary.json\\').total.lines.pct)"'</span>)
      .<span class="function">toString</span>().<span class="function">trim</span>();
    
    <span class="keyword">if</span> (<span class="function">parseFloat</span>(coverage) < <span class="number">75</span>) {
      <span class="keyword">throw</span> <span class="keyword">new</span> <span class="class-name">Error</span>(<span class="string">`Couverture insuffisante: <span class="variable">${coverage}</span>%`</span>);
    }
    
    <span class="comment">// Vérifier les vulnérabilités</span>
    <span class="function">exec</span>(<span class="string">'npm audit --audit-level=critical'</span>, { <span class="variable">stdio</span>: <span class="string">'inherit'</span> });
    
    <span class="variable">console</span>.<span class="function">log</span>(<span class="string">'✅ Quality Gate passed!'</span>);
    
  } <span class="keyword">catch</span> (error) {
    <span class="variable">console</span>.<span class="function">error</span>(<span class="string">'❌ Quality Gate failed:'</span>, error.<span class="variable">message</span>);
    <span class="variable">process</span>.<span class="function">exit</span>(<span class="number">1</span>);
  }
}

<span class="function">checkQualityGate</span>();</code></pre>
          </div>
        </details>
      </div>

      <!-- Outils populaires -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils populaires pour les Quality Gates</h2>
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Analyse statique</h4>
            <ul class="textExemple">
              <li><strong>SonarQube</strong> : Analyse complète de la qualité</li>
              <li><strong>ESLint</strong> : Analyse du code JavaScript</li>
              <li><strong>Prettier</strong> : Formatage du code</li>
              <li><strong>Checkstyle</strong> : Pour Java</li>
              <li><strong>Pylint</strong> : Pour Python</li>
            </ul>
          </div>
          <div>
            <h4 class="text-purple">Tests et couverture</h4>
            <ul class="textExemple">
              <li><strong>Jest</strong> : Framework de tests JavaScript</li>
              <li><strong>JUnit</strong> : Tests Java</li>
              <li><strong>pytest</strong> : Tests Python</li>
              <li><strong>Istanbul</strong> : Couverture de code</li>
              <li><strong>JaCoCo</strong> : Couverture Java</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Conclusion -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          Les Quality Gates sont essentielles pour maintenir des standards de qualité élevés dans le développement logiciel. 
          Elles permettent de :
        </p>
        <ul class="textExemple">
          <li>Détecter les problèmes tôt dans le cycle de développement</li>
          <li>Standardiser la qualité à travers les équipes</li>
          <li>Réduire les coûts de correction</li>
          <li>Améliorer la maintenabilité du code</li>
          <li>Renforcer la confiance dans les déploiements</li>
        </ul>
        <p class="textExemple">
          L'implémentation réussie des Quality Gates nécessite une approche progressive, 
          une automatisation complète et l'adhésion de toute l'équipe.
        </p>
      </div>

      <!-- Ressources supplémentaires -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        <ul class="textExemple">
          <li>Documentation officielle : <a href="https://docs.sonarqube.org/latest/user-guide/quality-gates/" target="_blank">SonarQube Quality Gates</a></li>
          <li>Livre : "Continuous Delivery" de Jez Humble et David Farley</li>
          <li>Article : "Implementing Quality Gates in CI/CD Pipelines" sur MartinFowler.com</li>
          <li>Outils : ESLint, Prettier, Jest, SonarQube, CodeClimate</li>
        </ul>
        <a href="#" class="btn-purple btn-hover">Voir d'autres leçons</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QualityGateLesson',
  head() {
    return {
      title: 'Quality Gates - Portes de qualité en développement',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez à implémenter des Quality Gates pour améliorer la qualité de votre code avec des exemples pratiques et des configurations détaillées.'
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

/* Couleurs VS Code pour la syntaxe */
.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }

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