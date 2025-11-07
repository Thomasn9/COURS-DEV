<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Installation et Configuration de Jenkins</h1>
        <p class="lesson-meta text-white">Mettez en place un serveur d'intégration continue pour automatiser vos déploiements</p>
      </header>

      <!-- Section Objectifs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'apprentissage</h2>
        <div class="objectives-grid">
          <div class="objective-item">
            <h3 class="text-purple">Comprendre Jenkins</h3>
            <p class="textExemple">Savoir ce qu'est Jenkins et son rôle dans le CI/CD</p>
          </div>
          <div class="objective-item">
            <h3 class="text-purple">Installation</h3>
            <p class="textExemple">Installer Jenkins sur différents systèmes</p>
          </div>
          <div class="objective-item">
            <h3 class="text-purple">Configuration</h3>
            <p class="textExemple">Configurer Jenkins pour un projet réel</p>
          </div>
          <div class="objective-item">
            <h3 class="text-purple">Pipeline CI/CD</h3>
            <p class="textExemple">Créer un pipeline d'intégration continue</p>
          </div>
        </div>
      </section>

      <!-- Section 1: Introduction à Jenkins -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que Jenkins ?</h2>
        
        <div class="definition-card">
          <div class="definition-content">
            <h3 class="text-purple">Définition</h3>
            <p class="textExemple">
              <strong>Jenkins</strong> est un serveur open source d'automatisation qui permet d'implémenter 
              des pipelines d'intégration et de déploiement continus (CI/CD).
            </p>
            <div class="key-points">
              <div class="key-point">
                <strong>Open Source</strong> : Gratuit et communauté active
              </div>
              <div class="key-point">
                <strong>Extensible</strong> : Plus de 1500 plugins disponibles
              </div>
              <div class="key-point">
                <strong>Cross-platform</strong> : Fonctionne sur Windows, Linux, macOS
              </div>
            </div>
          </div>
          <div class="definition-meta">
            <div class="meta-item">
              <strong>Créateur :</strong> Kohsuke Kawaguchi
            </div>
            <div class="meta-item">
              <strong>Première version :</strong> 2011
            </div>
            <div class="meta-item">
              <strong>Langage :</strong> Java
            </div>
            <div class="meta-item">
              <strong>GitHub :</strong> 20k+ stars
            </div>
          </div>
        </div>

        <div class="philosophy-section">
          <h3 class="text-purple">Pourquoi utiliser Jenkins ?</h3>
          <p class="textExemple">
            Jenkins automatise les processus de build, test et déploiement, permettant aux équipes de développement 
            de livrer du code plus rapidement et avec plus de fiabilité.
          </p>
        </div>
      </section>

      <!-- Section 2: Prérequis -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Prérequis d'installation</h2>
        
        <div class="prerequisites-grid">
          <div class="prerequisite-card">
            <h3 class="text-purple">Java</h3>
            <p class="textExemple">Java 8 ou 11 requis</p>
            <pre><code class="language-bash"><span class="comment"># Vérifier la version de Java</span>
<span class="command">java</span> <span class="parameter">-version</span>

<span class="comment"># Installation sur Ubuntu</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">update</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">install</span> <span class="parameter">openjdk-11-jdk</span></code></pre>
          </div>

          <div class="prerequisite-card">
            <h3 class="text-purple">Système</h3>
            <p class="textExemple">Minimum 256 MB RAM, 1 GB recommandé</p>
            <pre><code class="language-bash"><span class="comment"># Vérifier la mémoire disponible</span>
<span class="command">free</span> <span class="parameter">-h</span>

<span class="comment"># Vérifier l'espace disque</span>
<span class="command">df</span> <span class="parameter">-h</span></code></pre>
          </div>

          <div class="prerequisite-card">
            <h3 class="text-purple">Réseau</h3>
            <p class="textExemple">Accès internet pour télécharger les plugins</p>
            <pre><code class="language-bash"><span class="comment"># Tester la connectivité</span>
<span class="command">ping</span> <span class="parameter">-c 3 google.com</span>

<span class="comment"># Vérifier les ports ouverts</span>
<span class="command">netstat</span> <span class="parameter">-tulpn | grep :8080</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Section 3: Installation sur Ubuntu -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Installation sur Ubuntu</h2>
        
        <div class="installation-steps">
          <div class="step">
            <h3 class="text-purple">Étape 1 : Ajouter le repository Jenkins</h3>
            <pre><code class="language-bash"><span class="comment"># Mettre à jour le système</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">update</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">upgrade</span> <span class="parameter">-y</span>

<span class="comment"># Installer les dépendances</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">install</span> <span class="parameter">wget curl gnupg</span>

<span class="comment"># Ajouter la clé GPG de Jenkins</span>
<span class="command">curl</span> <span class="parameter">-fsSL https://pkg.jenkins.io/debian/jenkins.io.key</span> | <span class="command">sudo</span> <span class="command">tee</span> \
  <span class="parameter">/usr/share/keyrings/jenkins-keyring.asc</span> <span class="operator">></span> <span class="parameter">/dev/null</span>

<span class="comment"># Ajouter le repository Jenkins</span>
<span class="command">echo</span> <span class="string">"deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/"</span> | <span class="command">sudo</span> <span class="command">tee</span> \
  <span class="parameter">/etc/apt/sources.list.d/jenkins.list</span> <span class="operator">></span> <span class="parameter">/dev/null</span>

<span class="comment"># Mettre à jour les packages</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">update</span></code></pre>
          </div>

          <div class="step">
            <h3 class="text-purple">Étape 2 : Installer Jenkins</h3>
            <pre><code class="language-bash"><span class="comment"># Installer Jenkins</span>
<span class="command">sudo</span> <span class="command">apt</span> <span class="command">install</span> <span class="parameter">jenkins</span>

<span class="comment"># Démarrer le service Jenkins</span>
<span class="command">sudo</span> <span class="command">systemctl</span> <span class="command">start</span> <span class="parameter">jenkins</span>

<span class="comment"># Activer le démarrage automatique</span>
<span class="command">sudo</span> <span class="command">systemctl</span> <span class="command">enable</span> <span class="parameter">jenkins</span>

<span class="comment"># Vérifier le statut du service</span>
<span class="command">sudo</span> <span class="command">systemctl</span> <span class="command">status</span> <span class="parameter">jenkins</span></code></pre>
          </div>

          <div class="step">
            <h3 class="text-purple">Étape 3 : Configuration initiale</h3>
            <pre><code class="language-bash"><span class="comment"># Obtenir le mot de passe initial</span>
<span class="command">sudo</span> <span class="command">cat</span> <span class="parameter">/var/lib/jenkins/secrets/initialAdminPassword</span>

<span class="comment"># Ouvrir le firewall pour le port 8080</span>
<span class="command">sudo</span> <span class="command">ufw</span> <span class="command">allow</span> <span class="parameter">8080</span>
<span class="command">sudo</span> <span class="command">ufw</span> <span class="command">status</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Section 4: Installation avec Docker -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Installation avec Docker</h2>
        
        <div class="docker-installation">
          <h3 class="text-purple">Méthode recommandée pour le développement</h3>
          
          <div class="code-example">
            <h4 class="text-purple">Docker Compose</h4>
            <pre><code class="language-yaml"><span class="key">version</span>: <span class="string">'3.8'</span>
<span class="key">services</span>:
  <span class="key">jenkins</span>:
    <span class="key">image</span>: <span class="string">jenkins/jenkins:lts</span>
    <span class="key">container_name</span>: <span class="string">jenkins</span>
    <span class="key">privileged</span>: <span class="boolean">true</span>
    <span class="key">user</span>: <span class="string">root</span>
    <span class="key">ports</span>:
      - <span class="string">"8080:8080"</span>
      - <span class="string">"50000:50000"</span>
    <span class="key">volumes</span>:
      - <span class="string">./jenkins_home:/var/jenkins_home</span>
      - <span class="string">/var/run/docker.sock:/var/run/docker.sock</span>
    <span class="key">environment</span>:
      - <span class="string">JAVA_OPTS=-Djenkins.install.runSetupWizard=false</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">Commandes Docker directes</h4>
            <pre><code class="language-bash"><span class="comment"># Créer un volume pour la persistance</span>
<span class="command">docker</span> <span class="command">volume</span> <span class="command">create</span> <span class="parameter">jenkins_data</span>

<span class="comment"># Lancer le conteneur Jenkins</span>
<span class="command">docker</span> <span class="command">run</span> <span class="parameter">-d</span> \
  <span class="parameter">--name</span> <span class="string">jenkins</span> \
  <span class="parameter">-p</span> <span class="string">8080:8080</span> \
  <span class="parameter">-p</span> <span class="string">50000:50000</span> \
  <span class="parameter">-v</span> <span class="string">jenkins_data:/var/jenkins_home</span> \
  <span class="parameter">-v</span> <span class="string">/var/run/docker.sock:/var/run/docker.sock</span> \
  <span class="parameter">--restart</span> <span class="string">unless-stopped</span> \
  <span class="string">jenkins/jenkins:lts</span>

<span class="comment"># Voir les logs du conteneur</span>
<span class="command">docker</span> <span class="command">logs</span> <span class="parameter">-f jenkins</span>

<span class="comment"># Obtenir le mot de passe initial</span>
<span class="command">docker</span> <span class="command">exec</span> <span class="parameter">jenkins cat /var/jenkins_home/secrets/initialAdminPassword</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Section 5: Configuration initiale -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Configuration initiale de Jenkins</h2>
        
        <div class="configuration-steps">
          <div class="config-step">
            <h3 class="text-purple">Étape 1 : Accès à l'interface web</h3>
            <p class="textExemple">Ouvrez votre navigateur et accédez à :</p>
            <pre><code class="language-bash"><span class="comment"># URL d'accès à Jenkins</span>
<span class="string">http://localhost:8080</span>
<span class="comment"># ou</span>
<span class="string">http://votre-serveur-ip:8080</span></code></pre>
          </div>

          <div class="config-step">
            <h3 class="text-purple">Étape 2 : Installation des plugins</h3>
            <p class="textExemple">Installez les plugins recommandés :</p>
            <pre><code class="language-text">Plugins recommandés :
✓ Git
✓ Pipeline
✓ Blue Ocean
✓ Docker
✓ SSH
✓ Email Extension
✓ HTML Publisher</code></pre>
          </div>

          <div class="config-step">
            <h3 class="text-purple">Étape 3 : Création de l'administrateur</h3>
            <pre><code class="language-text">Formulaire de création d'administrateur :
Username: admin
Password: [votre mot de passe sécurisé]
Full name: Administrateur Jenkins
Email: admin@votre-entreprise.com</code></pre>
          </div>

          <div class="config-step">
            <h3 class="text-purple">Étape 4 : Configuration de l'URL</h3>
            <pre><code class="language-text">URL de Jenkins : http://votre-serveur:8080
(Assurez-vous que cette URL est accessible)</code></pre>
          </div>
        </div>
      </section>

      <!-- Section 6: Premier pipeline -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Création de votre premier pipeline</h2>
        
        <div class="pipeline-example">
          <h3 class="text-purple">Pipeline Jenkins déclaratif</h3>
          
          <div class="code-example">
            <h4 class="text-purple">Jenkinsfile</h4>
            <pre><code class="language-groovy"><span class="keyword">pipeline</span> {
    <span class="property">agent</span> <span class="string">any</span>
    
    <span class="property">environment</span> {
        <span class="variable">NODE_VERSION</span> = <span class="string">'18'</span>
        <span class="variable">DOCKER_REGISTRY</span> = <span class="string">'mon-registry'</span>
    }
    
    <span class="property">stages</span> {
        <span class="keyword">stage</span>(<span class="string">'Checkout'</span>) {
            <span class="property">steps</span> {
                <span class="method">git</span> <span class="string">branch: 'main'</span>,
                    <span class="string">url: 'https://github.com/votre-org/votre-repo.git'</span>
            }
        }
        
        <span class="keyword">stage</span>(<span class="string">'Install Dependencies'</span>) {
            <span class="property">steps</span> {
                <span class="method">sh</span> <span class="string">'npm install'</span>
            }
        }
        
        <span class="keyword">stage</span>(<span class="string">'Tests'</span>) {
            <span class="property">steps</span> {
                <span class="method">sh</span> <span class="string">'npm test'</span>
            }
            <span class="property">post</span> {
                <span class="keyword">always</span> {
                    <span class="method">junit</span> <span class="string">'reports/**/*.xml'</span>
                }
            }
        }
        
        <span class="keyword">stage</span>(<span class="string">'Build Docker'</span>) {
            <span class="property">steps</span> {
                <span class="method">sh</span> <span class="string">'''
                    docker build -t $DOCKER_REGISTRY/app:$BUILD_NUMBER .
                    docker push $DOCKER_REGISTRY/app:$BUILD_NUMBER
                '''</span>
            }
        }
        
        <span class="keyword">stage</span>(<span class="string">'Deploy to Staging'</span>) {
            <span class="property">when</span> {
                <span class="property">branch</span> <span class="string">'main'</span>
            }
            <span class="property">steps</span> {
                <span class="method">sh</span> <span class="string">'kubectl set image deployment/app app=$DOCKER_REGISTRY/app:$BUILD_NUMBER'</span>
            }
        }
    }
    
    <span class="property">post</span> {
        <span class="keyword">always</span> {
            <span class="method">emailext</span> (
                <span class="string">subject: "Build ${currentBuild.result}: Job ${env.JOB_NAME}"</span>,
                <span class="string">body: "Détails: ${env.BUILD_URL}"</span>,
                <span class="string">to: "dev-team@company.com"</span>
            )
        }
    }
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Section 7: Sécurité et bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Sécurité et bonnes pratiques</h2>
        
        <div class="security-grid">
          <div class="security-card">
            <h3 class="text-purple">Authentification</h3>
            <pre><code class="language-groovy"><span class="comment">// Configuration de la sécurité dans Jenkins</span>
<span class="comment">// Gestionnaire de sécurité → Realm de sécurité</span>
<span class="comment">// ✓ Activer l'authentification</span>
<span class="comment">// ✓ Créer des utilisateurs</span>
<span class="comment">// ✓ Définir les permissions</span></code></pre>
          </div>

          <div class="security-card">
            <h3 class="text-purple">Credentials</h3>
            <pre><code class="language-groovy"><span class="comment">// Stockage sécurisé des secrets</span>
<span class="keyword">withCredentials</span>([<span class="method">usernamePassword</span>(
    <span class="property">credentialsId</span>: <span class="string">'docker-registry'</span>,
    <span class="property">usernameVariable</span>: <span class="string">'USERNAME'</span>,
    <span class="property">passwordVariable</span>: <span class="string">'PASSWORD'</span>
)]) {
    <span class="method">sh</span> <span class="string">'docker login -u $USERNAME -p $PASSWORD'</span>
}</code></pre>
          </div>

          <div class="security-card">
            <h3 class="text-purple">Backup automatique</h3>
            <pre><code class="language-xml"><span class="comment">&lt;!-- Configuration du plugin ThinBackup --&gt;</span>
<span class="tag">&lt;<span class="name">backupPath</span>&gt;</span>/var/jenkins_backup<span class="tag">&lt;/<span class="name">backupPath</span>&gt;</span>
<span class="tag">&lt;<span class="name">backupSchedule</span>&gt;</span>0 2 * * *<span class="tag">&lt;/<span class="name">backupSchedule</span>&gt;</span>
<span class="tag">&lt;<span class="name">maxBackupNumber</span>&gt;</span>10<span class="tag">&lt;/<span class="name">maxBackupNumber</span>&gt;</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Section 8: Conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Conclusion</h2>
        
        <div class="conclusion-content">
          <div class="conclusion-summary">
            <h3 class="text-white">Récapitulatif des points clés</h3>
            <ul class="text-white">
              <li><strong>Installation flexible</strong> - Jenkins peut être installé via package manager, Docker, ou manuellement</li>
              <li><strong>Configuration sécurisée</strong> - Mise en place d'authentification et gestion des credentials</li>
              <li><strong>Pipelines as code</strong> - Définition des pipelines dans des Jenkinsfiles versionnés</li>
              <li><strong>Écosystème étendu</strong> - Plus de 1500 plugins pour étendre les fonctionnalités</li>
              <li><strong>Intégration continue</strong> - Automatisation du build, test et déploiement</li>
            </ul>
          </div>

          <div class="conclusion-perspective">
            <h3 class="text-white">Jenkins dans l'écosystème DevOps</h3>
            <p class="text-white">
              Jenkins reste un outil majeur dans le paysage DevOps malgré l'émergence de solutions plus récentes. 
              Sa maturité, sa stabilité et son écosystème de plugins en font un choix robuste pour les entreprises 
              de toutes tailles.
            </p>
          </div>

          <div class="conclusion-benefits">
            <h3 class="text-white">Prochaines étapes recommandées</h3>
            <div class="benefits-grid">
              <div class="benefit-item">
                <h4 class="text-white">Plugins essentiels</h4>
                <p class="text-white">Explorer les plugins Blue Ocean, Docker, et Kubernetes</p>
              </div>
              <div class="benefit-item">
                <h4 class="text-white">Intégrations avancées</h4>
                <p class="text-white">Configurer l'intégration avec GitHub, GitLab, ou Bitbucket</p>
              </div>
              <div class="benefit-item">
                <h4 class="text-white">Scale horizontal</h4>
                <p class="text-white">Mettre en place des agents Jenkins pour distribuer la charge</p>
              </div>
              <div class="benefit-item">
                <h4 class="text-white">Monitoring</h4>
                <p class="text-white">Configurer la surveillance des performances et des logs</p>
              </div>
            </div>
          </div>

          <div class="conclusion-final">
            <div class="final-thoughts">
              <p class="text-white">
                <strong>Vous avez maintenant les bases pour déployer et configurer Jenkins en production.</strong> 
                La maîtrise de Jenkins vous permettra d'automatiser complètement votre processus de développement 
                et de déploiement, réduisant les erreurs humaines et accélérant la livraison.
              </p>
              <p class="text-white">
                N'oubliez pas que la configuration de Jenkins est itérative - commencez par un pipeline simple 
                et complexifiez-le au fur et à mesure que vos besoins évoluent.
              </p>
            </div>
            
            <div class="action-call">
              <p class="text-white" style="text-align: center; font-weight: 600;">
                Votre infrastructure CI/CD est maintenant opérationnelle ! Continuez à expérimenter 
                avec différents plugins et configurations pour optimiser votre workflow.
              </p>
            </div>
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

/* Header amélioré */
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
    margin-bottom: 1.5rem;
}

.lesson-duration {
    display: flex;
    gap: 1rem;
    justify-content: center;
    position: relative;
}

.duration-badge, .level-badge {
    background: rgba(255, 255, 255, 0.2);
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.9rem;
}

/* Grille des objectifs */
.objectives-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.objective-item {
    text-align: center;
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
    transition: transform 0.3s ease;
}

.objective-item:hover {
    transform: translateY(-5px);
}

/* Cartes de définition */
.definition-card {
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 2rem;
    margin: 1.5rem 0;
}

.key-points {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-top: 1rem;
}

.key-point {
    padding: 0.5rem;
    background: #f8f6ff;
    border-radius: 5px;
    border-left: 3px solid #8B5FBF;
}

.definition-meta {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

.meta-item {
    margin-bottom: 0.5rem;
    padding: 0.5rem 0;
    border-bottom: 1px solid #f0f0f0;
}

.meta-item:last-child {
    border-bottom: none;
    margin-bottom: 0;
}

/* Grille des prérequis */
.prerequisites-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.prerequisite-card {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
    transition: transform 0.3s ease;
}

.prerequisite-card:hover {
    transform: translateY(-5px);
}

/* Étapes d'installation */
.installation-steps {
    display: flex;
    flex-direction: column;
    gap: 2rem;
    margin-top: 1.5rem;
}

.step {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

/* Installation Docker */
.docker-installation {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.code-example {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
}

/* Configuration */
.configuration-steps {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.config-step {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

/* Pipeline */
.pipeline-example {
    margin-top: 1.5rem;
}

/* Sécurité */
.security-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.security-card {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border: 2px solid #e0d6ff;
    transition: transform 0.3s ease;
}

.security-card:hover {
    transform: translateY(-5px);
}

/* Conclusion */
.conclusion-content {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.conclusion-summary,
.conclusion-perspective,
.conclusion-benefits,
.conclusion-final {
    padding: 1.5rem;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    border-left: 4px solid rgba(255, 255, 255, 0.3);
    backdrop-filter: blur(10px);
}

.benefits-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
}

.benefit-item {
    padding: 1rem;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 8px;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.action-call {
    background: rgba(255, 255, 255, 0.1);
    padding: 2rem;
    border-radius: 15px;
    text-align: center;
    margin-top: 2rem;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

/* Styles existants conservés */
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

/* Styles pour les blocs de code avec coloration VS Code complète */
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
    word-wrap: break-word;
    word-break: break-word;
    margin: 1rem 0;
}

/* Coloration syntaxique VS Code complète */
.language-bash .command { color: #569cd6 !important; }
.language-bash .parameter { color: #9cdcfe !important; }
.language-bash .string { color: #ce9178 !important; }
.language-bash .comment { color: #6a9955 !important; }
.language-bash .operator { color: #d4d4d4 !important; }

.language-groovy .keyword { color: #569cd6 !important; }
.language-groovy .string { color: #ce9178 !important; }
.language-groovy .comment { color: #6a9955 !important; }
.language-groovy .method { color: #dcdcaa !important; }
.language-groovy .property { color: #9cdcfe !important; }
.language-groovy .variable { color: #9cdcfe !important; }

.language-yaml .key { color: #9cdcfe !important; }
.language-yaml .string { color: #ce9178 !important; }
.language-yaml .number { color: #b5cea8 !important; }
.language-yaml .boolean { color: #569cd6 !important; }

.language-xml .tag { color: #569cd6 !important; }
.language-xml .tag .name { color: #569cd6 !important; }
.language-xml .comment { color: #6a9955 !important; }

.language-text .string { color: #ce9178 !important; }
.language-text .comment { color: #6a9955 !important; }

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* Responsive */
@media (max-width: 768px) {
    .lesson-container {
        padding: 1rem;
    }
    
    .definition-card,
    .prerequisites-grid,
    .security-grid {
        grid-template-columns: 1fr;
    }
    
    .objectives-grid,
    .benefits-grid {
        grid-template-columns: 1fr;
    }
    
    .lesson-header {
        padding: 2rem 1rem;
    }
    
    .lesson-header h1 {
        font-size: 2rem;
    }
    
    .lesson-duration {
        flex-direction: column;
        align-items: center;
    }
    
    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
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
.lesson-section:nth-child(6) { animation-delay: 0.6s; }
.lesson-section:nth-child(7) { animation-delay: 0.7s; }
.lesson-section:nth-child(8) { animation-delay: 0.8s; }
</style>