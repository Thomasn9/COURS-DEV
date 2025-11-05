<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Localhost - Le Serveur Local</h1>
        <p class="lesson-meta text-white">
          Comprendre et utiliser l'hôte local pour le développement
        </p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que le Localhost ?</h2>
        <p class="textExemple">
          Localhost est un nom d'hôte qui se réfère à la machine locale sur laquelle un programme s'exécute. 
          Il permet d'accéder aux services réseau fonctionnant sur l'ordinateur local via l'adresse IP <strong>127.0.0.1</strong>.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Caractéristiques principales :</h3>
          <ul>
            <li><strong>Adresse réservée</strong> : 127.0.0.1 dans IPv4, ::1 dans IPv6</li>
            <li><strong>Bouclage</strong> : Le trafic ne quitte jamais la machine</li>
            <li><strong>Développement</strong> : Idéal pour tester des applications localement</li>
            <li><strong>Sécurité</strong> : Accès restreint à la machine locale uniquement</li>
          </ul>
        </div>
      </section>

      <!-- Adresses et ports -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Adresses et Ports du Localhost</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Adresses de bouclage</h3>
            <ul>
              <li><strong>127.0.0.1</strong> - IPv4 standard</li>
              <li><strong>localhost</strong> - Nom d'hôte résolu en 127.0.0.1</li>
              <li><strong>::1</strong> - IPv6 localhost</li>
              <li><strong>127.0.0.0/8</strong> - Bloc entier pour le bouclage</li>
              <li><strong>0.0.0.0</strong> - Toutes les interfaces</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Ports courants</h3>
            <ul>
              <li><strong>80</strong> - HTTP</li>
              <li><strong>443</strong> - HTTPS</li>
              <li><strong>3000</strong> - Applications Node.js</li>
              <li><strong>8080</strong> - Serveurs de développement</li>
              <li><strong>3306</strong> - MySQL</li>
              <li><strong>5432</strong> - PostgreSQL</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Exemples pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples pratiques d'utilisation</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Démarrer des serveurs locaux</h3>
          <div class="code-block">
            <pre><code># Serveur HTTP Python 3
python -m http.server 8000
# Accès: http://localhost:8000

# Serveur PHP intégré
php -S localhost:8080
# Accès: http://localhost:8080

# Serveur HTTP Node.js avec http-server
npx http-server -p 3000
# Accès: http://localhost:3000

# Serveur Live-reload pour le développement
npx live-server --port=5500
# Accès: http://localhost:5500</code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Applications de développement</h3>
          <div class="code-block">
            <pre><code># React.js (Create React App)
npm start
# Par défaut: http://localhost:3000

# Vue.js
npm run serve
# Par défaut: http://localhost:8080

# Angular
ng serve
# Par défaut: http://localhost:4200

# Next.js
npm run dev
# Par défaut: http://localhost:3000

# Nuxt.js
npm run dev
# Par défaut: http://localhost:3000</code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Bases de données locales</h3>
          <div class="code-block">
            <pre><code># Connexion à MySQL local
mysql -h 127.0.0.1 -u root -p
# Ou: mysql -h localhost -u root -p

# Connexion à PostgreSQL local
psql -h localhost -U postgres -d ma_base

# MongoDB local
mongosh --host localhost:27017

# Redis local
redis-cli -h localhost</code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Tests réseau et diagnostics</h3>
          <div class="code-block">
            <pre><code># Tester la connectivité localhost
ping localhost
ping 127.0.0.1

# Vérifier les ports ouverts
netstat -an | grep 127.0.0.1
# Sur Windows: netstat -an | findstr 127.0.0.1

# Tester un service sur un port spécifique
telnet localhost 8080
# Ou: nc -zv localhost 8080

# Curl vers un service local
curl http://localhost:3000/api/users
curl -X POST http://localhost:8080/login</code></pre>
          </div>
        </div>
      </section>

      <!-- Fichier hosts -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Le fichier hosts</h2>
        <p class="textExemple">
          Le fichier hosts est un fichier système qui associe des noms d'hôtes à des adresses IP. 
          Il est consulté avant les serveurs DNS et permet de rediriger des domaines vers localhost.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Emplacement du fichier hosts</h3>
          <ul>
            <li><strong>Windows</strong> : C:\Windows\System32\drivers\etc\hosts</li>
            <li><strong>Linux/macOS</strong> : /etc/hosts</li>
          </ul>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Exemples de configuration</h3>
          <div class="code-block">
            <pre><code># Fichier hosts - Redirections vers localhost
127.0.0.1   localhost
127.0.0.1   mon-site.local
127.0.0.1   api.mon-app.test
127.0.0.1   admin.mon-site.dev
127.0.0.1   boutique.local

# IPv6
::1         localhost

# Commentaire: Les lignes commençant par # sont ignorées

# Exemple pour un projet spécifique
127.0.0.1   mon-projet.test
127.0.0.1   www.mon-projet.test
127.0.0.1   admin.mon-projet.test</code></pre>
          </div>
        </div>
      </section>

      <!-- Cas d'utilisation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Cas d'utilisation du Localhost</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Développement Web</h3>
            <ul>
              <li>Tests d'applications web</li>
              <li>Développement frontend</li>
              <li>API REST locales</li>
              <li>Microservices en local</li>
              <li>Tests de bases de données</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Réseau et Sécurité</h3>
            <ul>
              <li>Tests de services réseau</li>
              <li>Développement sécurisé</li>
              <li>Isolation des environnements</li>
              <li>Tests de configuration</li>
              <li>Debugging réseau</li>
            </ul>
          </div>
        </div>

        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Conteneurs et Virtualisation</h3>
            <ul>
              <li>Docker avec port mapping</li>
              <li>Applications conteneurisées</li>
              <li>Environnements de test</li>
              <li>Orchestration locale</li>
              <li>Services en isolation</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Outils DevOps</h3>
            <ul>
              <li>CI/CD local avec Jenkins</li>
              <li>Monitoring local</li>
              <li>Tests de déploiement</li>
              <li>Configuration d'outils</li>
              <li>Automation locale</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Docker et localhost -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Localhost avec Docker</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Exemples Docker</h3>
          <div class="code-block">
            <pre><code># Lancer un serveur web Nginx
docker run -p 8080:80 nginx
# Accès: http://localhost:8080

# Base de données MySQL
docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret mysql
# Connexion: mysql -h 127.0.0.1 -u root -p

# Application Node.js avec volume
docker run -p 3000:3000 -v $(pwd):/app node:16 npm start

# Docker Compose avec multiple services
# docker-compose.yml
version: '3'
services:
  web:
    build: .
    ports:
      - "8000:8000"
  db:
    image: postgres:13
    ports:
      - "5432:5432"</code></pre>
          </div>
        </div>
      </section>

      <!-- Dépannage -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Dépannage Courant</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Problèmes Fréquents</h3>
            <ul>
              <li>Port déjà utilisé</li>
              <li>Firewall bloquant</li>
              <li>Service non démarré</li>
              <li>Mauvaise configuration</li>
              <li>Cache DNS</li>
              <li>Permissions insuffisantes</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Solutions</h3>
            <ul>
              <li>Vérifier les ports avec netstat/lsof</li>
              <li>Changer le port de l'application</li>
              <li>Désactiver le firewall temporairement</li>
              <li>Redémarrer le service</li>
              <li>Vider le cache DNS</li>
              <li>Exécuter en tant qu'administrateur</li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Commandes de diagnostic</h3>
          <div class="code-block">
            <pre><code># Vérifier si un port est utilisé
# Linux/macOS:
lsof -i :3000
netstat -tulpn | grep :3000

# Windows:
netstat -ano | findstr :3000

# Tester la résolution DNS
nslookup localhost
ping localhost

# Vérifier la configuration réseau
ipconfig /all  # Windows
ifconfig       # Linux/macOS

# Test de connectivité TCP
telnet 127.0.0.1 8080</code></pre>
          </div>
        </div>
      </section>

      <!-- Sécurité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Aspects Sécurité</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Avantages Sécurité</h3>
            <ul>
              <li>Isolation du réseau externe</li>
              <li>Pas d'exposition internet</li>
              <li>Tests sécurisés d'applications</li>
              <li>Développement en sandbox</li>
              <li>Contrôle total de l'environnement</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Considérations</h3>
            <ul>
              <li>Services exposés accidentellement</li>
              <li>Configurations trop permissives</li>
              <li>Failles de sécurité locales</li>
              <li>Données sensibles en local</li>
              <li>Mauvaise configuration réseau</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Développement</h3>
          <ul>
            <li>Utiliser des ports standards pour chaque type d'application</li>
            <li>Configurer des noms de domaine locaux dans le fichier hosts</li>
            <li>Utiliser HTTPS même en local avec des certificats auto-signés</li>
            <li>Documenter les ports utilisés dans la documentation du projet</li>
            <li>Utiliser des variables d'environnement pour les configurations</li>
          </ul>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Configuration</h3>
          <ul>
            <li>Sauvegarder le fichier hosts avant modifications</li>
            <li>Utiliser des outils comme dnsmasq pour la gestion DNS locale</li>
            <li>Configurer des alias dans le shell pour les commandes fréquentes</li>
            <li>Utiliser Docker pour isoler les environnements</li>
            <li>Mettre en place des scripts de démarrage automatique</li>
          </ul>
        </div>
      </section>

      <!-- Outils utiles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils Utiles</h2>
        
        <div class="code-comparison">
          <div>
            <h3 class="text-purple">Développement</h3>
            <ul>
              <li><strong>ngrok</strong> : Exposition sécurisée de localhost</li>
              <li><strong>localhost.run</strong> : Tunnel HTTP vers l'extérieur</li>
              <li><strong>serve</strong> : Serveur HTTP statique</li>
              <li><strong>live-server</strong> : Serveur avec rechargement automatique</li>
              <li><strong>json-server</strong> : API REST factice</li>
            </ul>
          </div>
          
          <div>
            <h3 class="text-purple">Réseau</h3>
            <ul>
              <li><strong>Wireshark</strong> : Analyseur de paquets</li>
              <li><strong>Postman</strong> : Tests d'API</li>
              <li><strong>curl</strong> : Ligne de commande HTTP</li>
              <li><strong>netcat</strong> : Utilitaire réseau</li>
              <li><strong>telnet</strong> : Connexion TCP</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion et Ressources</h2>
        <p class="textExemple">
          Localhost est un concept fondamental en développement et administration système. 
          Il permet de créer des environnements de développement isolés, sécurisés et reproductibles, 
          essentiels pour le développement moderne d'applications.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Ressources pour Approfondir</h3>
          <ul>
            <li><strong>RFC 6761</strong> : Spécial-Purpose Domain Names</li>
            <li><strong>Documentation Docker</strong> : Network configuration</li>
            <li><strong>MDN Web Docs</strong> : Localhost development</li>
            <li><strong>Stack Overflow</strong> : Troubleshooting guides</li>
            <li><strong>GitHub</strong> : Exemples de configuration</li>
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

/* Styles pour les blocs de code */
.code-block {
    background: #2d2d2d;
    border-radius: 8px;
    padding: 1.5rem;
    margin: 1rem 0;
    overflow-x: auto;
    border-left: 4px solid #8B5FBF;
}

.code-block pre {
    margin: 0;
    color: #f8f8f2;
    font-family: 'Courier New', monospace;
    font-size: 0.9rem;
    line-height: 1.4;
}

.code-block code {
    color: #f8f8f2;
    background: none;
    padding: 0;
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
    
    .code-block {
        padding: 1rem;
        font-size: 0.8rem;
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
    
    .code-block {
        padding: 0.8rem;
        font-size: 0.75rem;
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