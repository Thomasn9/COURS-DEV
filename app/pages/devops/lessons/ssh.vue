<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">SSH (Secure Shell)</h1>
        <p class="lesson-meta text-white">Protocole de communication sécurisé pour l'accès à distance</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à SSH</h2>
        <p class="textExemple">
          SSH (Secure Shell) est un protocole de communication sécurisé qui permet d'établir une connexion chiffrée entre un client et un serveur. Il est principalement utilisé pour :
        </p>
        <ul class="textExemple">
          <li>L'accès à distance à des serveurs</li>
          <li>L'exécution de commandes à distance</li>
          <li>Le transfert sécurisé de fichiers</li>
          <li>Le tunneling de ports</li>
        </ul>
      </section>

      <!-- Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Concepts fondamentaux</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Architecture client-serveur</h3>
          <p>SSH fonctionne selon un modèle client-serveur :</p>
          <pre><code>Client SSH → Serveur SSH (sshd)</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Méthodes d'authentification</h3>
          <ul>
            <li>Authentification par mot de passe</li>
            <li>Authentification par clé publique/privée (recommandée)</li>
          </ul>
        </div>
      </section>

      <!-- Installation et configuration -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Installation et configuration</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Installation côté client</h3>
            <pre><code class="language-bash"><span class="comment"># Sur Ubuntu/Debian</span>
<span class="keyword">sudo</span> apt update
<span class="keyword">sudo</span> apt install openssh-client

<span class="comment"># Sur CentOS/RHEL</span>
<span class="keyword">sudo</span> yum install openssh-clients

<span class="comment"># Sur macOS (déjà installé)</span>
<span class="comment"># Sur Windows : utiliser Git Bash ou WSL</span></code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Installation côté serveur</h3>
            <pre><code class="language-bash"><span class="comment"># Sur Ubuntu/Debian</span>
<span class="keyword">sudo</span> apt update
<span class="keyword">sudo</span> apt install openssh-server

<span class="comment"># Sur CentOS/RHEL</span>
<span class="keyword">sudo</span> yum install openssh-server

<span class="comment"># Démarrer le service</span>
<span class="keyword">sudo</span> systemctl start ssh
<span class="keyword">sudo</span> systemctl enable ssh</code></pre>
          </div>
        </div>
      </section>

      <!-- Utilisation basique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Utilisation basique de SSH</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Connexion simple</h3>
          <pre><code class="language-bash"><span class="comment"># Syntaxe de base</span>
ssh <span class="variable">utilisateur</span>@<span class="variable">hôte</span>

<span class="comment"># Exemple</span>
ssh john@192.168.1.100
ssh admin@monserveur.com</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Spécifier un port différent</h3>
          <pre><code class="language-bash"><span class="comment"># Le port par défaut est 22</span>
<span class="comment"># Pour utiliser un port différent :</span>
ssh -p <span class="number">2222</span> utilisateur@hôte</code></pre>
        </div>
      </section>

      <!-- Clés SSH -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Authentification par clés SSH</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Génération de clés</h3>
          <pre><code class="language-bash"><span class="comment"># Générer une paire de clés RSA (4096 bits)</span>
ssh-keygen -t rsa -b <span class="number">4096</span> -C <span class="string">"votre_email@exemple.com"</span>

<span class="comment"># Générer une paire de clés Ed25519 (plus sécurisée)</span>
ssh-keygen -t ed25519 -C <span class="string">"votre_email@exemple.com"</span>

<span class="comment"># Emplacement par défaut : ~/.ssh/id_rsa (privée) et ~/.ssh/id_rsa.pub (publique)</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Copie de la clé publique sur le serveur</h3>
          <pre><code class="language-bash"><span class="comment"># Méthode automatique</span>
ssh-copy-id utilisateur@hôte

<span class="comment"># Méthode manuelle</span>
cat ~/.ssh/id_rsa.pub | ssh utilisateur@hôte <span class="string">"mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"</span></code></pre>
        </div>
      </section>

      <!-- Configuration avancée -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Configuration avancée</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Fichier de configuration SSH (~/.ssh/config)</h3>
          <pre><code class="language-bash"><span class="comment"># Exemple de configuration</span>
Host myserver
    HostName monserveur.com
    User john
    Port <span class="number">2222</span>
    IdentityFile ~/.ssh/id_rsa_monserveur

Host vps
    HostName 192.168.1.100
    User root
    IdentitiesOnly yes

<span class="comment"># Utilisation : ssh myserver au lieu de ssh john@monserveur.com -p 2222</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Transfert de fichiers avec SCP</h3>
          <pre><code class="language-bash"><span class="comment"># Copier un fichier local vers le serveur distant</span>
scp monfichier.txt utilisateur@hôte:/chemin/destination/

<span class="comment"># Copier un fichier du serveur distant vers le local</span>
scp utilisateur@hôte:/chemin/fichier.txt .

<span class="comment"># Copier un dossier récursivement</span>
scp -r mondossier utilisateur@hôte:/chemin/destination/</code></pre>
        </div>
      </section>

      <!-- Sécurité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques de sécurité</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Renforcer la sécurité SSH</h3>
          <pre><code class="language-bash"><span class="comment"># Éditer le fichier de configuration du serveur SSH</span>
<span class="keyword">sudo</span> nano /etc/ssh/sshd_config

<span class="comment"># Modifications recommandées :</span>
<span class="variable">Port</span> <span class="number">2222</span>                    <span class="comment"># Changer le port par défaut</span>
<span class="variable">PermitRootLogin</span> no           <span class="comment"># Interdire la connexion root directe</span>
<span class="variable">PasswordAuthentication</span> no   <span class="comment"># Désactiver l'authentification par mot de passe</span>
<span class="variable">PubkeyAuthentication</span> yes    <span class="comment"># Activer l'authentification par clé</span>
<span class="variable">MaxAuthTries</span> <span class="number">3</span>               <span class="comment"># Limiter les tentatives d'authentification</span>
<span class="variable">ClientAliveInterval</span> <span class="number">300</span>     <span class="comment"># Déconnexion automatique après inactivité</span>
<span class="variable">ClientAliveCountMax</span> <span class="number">2</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Redémarrer le service après modifications</h3>
          <pre><code class="language-bash"><span class="comment"># Redémarrer le service SSH</span>
<span class="keyword">sudo</span> systemctl restart ssh

<span class="comment"># Vérifier le statut</span>
<span class="keyword">sudo</span> systemctl status ssh</code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Première connexion</h3>
          <p>Connectez-vous à un serveur SSH en utilisant l'authentification par mot de passe.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code class="language-bash">ssh utilisateur@adresse_du_serveur</code></pre>
              <p>Remplacez "utilisateur" par votre nom d'utilisateur et "adresse_du_serveur" par l'adresse IP ou le nom de domaine du serveur.</p>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Configuration de clés SSH</h3>
          <p>Générez une paire de clés SSH et configurez l'authentification sans mot de passe sur un serveur.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>Étape 1 : Génération des clés</h4>
              <pre><code class="language-bash">ssh-keygen -t ed25519 -C "votre_email@exemple.com"</code></pre>
              
              <h4>Étape 2 : Copie de la clé publique</h4>
              <pre><code class="language-bash">ssh-copy-id utilisateur@adresse_du_serveur</code></pre>
              
              <h4>Étape 3 : Test de connexion</h4>
              <pre><code class="language-bash">ssh utilisateur@adresse_du_serveur</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 3 : Configuration avancée</h3>
          <p>Créez un alias dans votre fichier ~/.ssh/config pour simplifier la connexion à un serveur spécifique.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code class="language-bash">Host monalias
    HostName adresse_du_serveur
    User votre_utilisateur
    Port 2222
    IdentityFile ~/.ssh/ma_cle_privee</code></pre>
              <p>Utilisation : <code>ssh monalias</code></p>
            </div>
          </details>
        </div>
      </section>

      <!-- Ressources supplémentaires -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        <div class="code-example">
          <ul>
            <li><a href="https://www.ssh.com/academy/ssh" class="btn-purple btn-hover" target="_blank">Documentation officielle SSH</a></li>
            <li><a href="https://man.openbsd.org/ssh" class="btn-purple btn-hover" target="_blank">Manuel SSH</a></li>
            <li><a href="https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server" class="btn-purple btn-hover" target="_blank">Tutoriel DigitalOcean</a></li>
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