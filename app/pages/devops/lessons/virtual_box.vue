<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Installation d'une Machine Virtuelle avec VirtualBox</h1>
        <p class="lesson-meta text-white">Guide complet pour virtualiser des systèmes d'exploitation</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à la virtualisation</h2>
        <p class="textExemple">
          VirtualBox est un logiciel de virtualisation qui permet d'exécuter plusieurs systèmes d'exploitation simultanément sur une même machine physique. Idéal pour :
        </p>
        <ul class="textExemple">
          <li>Développement et tests logiciels</li>
          <li>Apprentissage de nouveaux systèmes d'exploitation</li>
          <li>Création d'environnements de production isolés</li>
          <li>Sécurité et isolation d'applications</li>
        </ul>
      </section>

      <!-- Étape 1 : Installation de VirtualBox -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 1 : Installation de VirtualBox</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Sur Windows</h3>
          <pre><code class="language-bash"><span class="comment"># 1. Télécharger VirtualBox depuis le site officiel</span>
<span class="comment"># https://www.virtualbox.org/wiki/Downloads</span>

<span class="comment"># 2. Exécuter l'installateur</span>
<span class="comment"># - Double-cliquer sur VirtualBox-*-Win.exe</span>
<span class="comment"># - Suivre l'assistant d'installation</span>
<span class="comment"># - Accepter les installations des pilotes</span>

<span class="comment"># 3. Redémarrer si nécessaire</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Sur Linux (Ubuntu/Debian)</h3>
          <pre><code class="language-bash"><span class="comment"># Méthode 1 : Depuis les dépôts officiels</span>
<span class="keyword">sudo</span> apt update
<span class="keyword">sudo</span> apt install virtualbox virtualbox-ext-pack

<span class="comment"># Méthode 2 : Depuis le site officiel</span>
<span class="comment"># Télécharger le .deb sur virtualbox.org</span>
<span class="keyword">sudo</span> dpkg -i virtualbox-*.deb
<span class="keyword">sudo</span> apt install -f <span class="comment"># Résoudre les dépendances</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Sur macOS</h3>
          <pre><code class="language-bash"><span class="comment"># 1. Télécharger le .dmg depuis virtualbox.org</span>
<span class="comment"># 2. Ouvrir le fichier .dmg</span>
<span class="comment"># 3. Glisser VirtualBox dans le dossier Applications</span>
<span class="comment"># 4. Lancer VirtualBox depuis Applications</span>
<span class="comment"># 5. Autoriser l'extension dans Préférences de Sécurité</span></code></pre>
        </div>
      </section>

      <!-- Étape 2 : Téléchargement d'une ISO -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 2 : Téléchargement d'un système d'exploitation</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Ubuntu Server (Recommandé pour SSH)</h3>
          <pre><code class="language-bash"><span class="comment"># Télécharger Ubuntu Server LTS</span>
<span class="comment"># https://ubuntu.com/download/server</span>

<span class="comment"># Ou via ligne de commande (Linux)</span>
wget https://releases.ubuntu.com/22.04/ubuntu-22.04.3-live-server-amd64.iso</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Autres distributions populaires</h3>
          <pre><code class="language-bash"><span class="comment"># Debian</span>
<span class="comment"># https://www.debian.org/distrib/</span>

<span class="comment"># CentOS Stream</span>
<span class="comment"># https://www.centos.org/centos-stream/</span>

<span class="comment"># Alpine Linux (léger)</span>
<span class="comment"># https://alpinelinux.org/downloads/</span></code></pre>
        </div>

        <div class="warning-box">
          <p><strong>💡 Conseil :</strong> Pour l'apprentissage de SSH, Ubuntu Server est recommandé car il est bien documenté et largement utilisé en production.</p>
        </div>
      </section>

      <!-- Étape 3 : Création de la VM -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 3 : Création de la machine virtuelle</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Lancement de VirtualBox</h3>
          <pre><code class="language-bash"><span class="comment"># Sur Windows : Menu Démarrer → Oracle VM VirtualBox</span>
<span class="comment"># Sur Linux : virtualbox ou via le menu applications</span>
<span class="comment"># Sur macOS : Applications → VirtualBox</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Création d'une nouvelle VM</h3>
          <pre><code class="language-bash"><span class="comment"># 1. Cliquer sur "Nouvelle"</span>
<span class="comment"># 2. Configurer les paramètres :</span>

<span class="comment"># - Nom : "Ubuntu-SSH-Server"</span>
<span class="comment"># - Dossier de la machine : Laisser par défaut</span>
<span class="comment"># - Type : Linux</span>
<span class="comment"># - Version : Ubuntu (64-bit)</span>

<span class="comment"># 3. Mémoire vive : 2048 MB (minimum recommandé)</span>
<span class="comment"># 4. Disque dur : Créer un disque virtuel maintenant</span>
<span class="comment"># 5. Type de disque : VDI (VirtualBox Disk Image)</span>
<span class="comment"># 6. Stockage : Dynamiquement alloué</span>
<span class="comment"># 7. Taille : 20 GB (suffisant pour les exercices)</span></code></pre>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Paramètres recommandés pour SSH :</h4>
          <ul>
            <li><strong>RAM :</strong> 2-4 GB selon votre machine hôte</li>
            <li><strong>Stockage :</strong> 20-30 GB en allocation dynamique</li>
            <li><strong>Processeurs :</strong> 2 cœurs minimum</li>
          </ul>
        </div>
      </section>

      <!-- Étape 4 : Configuration réseau -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 4 : Configuration réseau pour SSH</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Configuration de l'adaptateur réseau</h3>
          <pre><code class="language-bash"><span class="comment"># 1. Sélectionner la VM → Paramètres → Réseau</span>
<span class="comment"># 2. Adaptateur 1 :</span>

<span class="comment"># - Cochez "Activer l'adaptateur réseau"</span>
<span class="comment"># - Attaché à : "Accès par pont"</span>
<span class="comment"># - Nom : Votre carte réseau principale</span>
<span class="comment"># - Cochez "Câble branché"</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Types de réseau expliqués</h3>
          <pre><code class="language-bash"><span class="comment"># NAT : VM partage l'IP de l'hôte (par défaut)</span>
<span class="comment"># Accès par pont : VM a sa propre IP sur le réseau local</span>
<span class="comment"># Réseau interne : Réseau privé entre VMs seulement</span>
<span class="comment"># Hôte seul : Communication VM ↔ Hôte seulement</span></code></pre>
          
          <div class="textExemple">
            <p><strong>Pour SSH :</strong> L'<strong>Accès par pont</strong> est recommandé car il permet de se connecter à la VM depuis n'importe quelle machine du réseau local.</p>
          </div>
        </div>
      </section>

      <!-- Étape 5 : Installation du système -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 5 : Installation d'Ubuntu Server</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Montage de l'ISO</h3>
          <pre><code class="language-bash"><span class="comment"># 1. Sélectionner la VM → Paramètres → Stockage</span>
<span class="comment"># 2. Contrôleur : IDE → CD/DVD</span>
<span class="comment"># 3. Cochez "Lecteur de CD/DVD"</span>
<span class="comment"># 4. Choisir "Fichier ISO" → Parcourir</span>
<span class="comment"># 5. Sélectionner votre fichier ubuntu-*.iso</span>
<span class="comment"># 6. OK pour valider</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Démarrage et installation</h3>
          <pre><code class="language-bash"><span class="comment"># 1. Démarrer la VM</span>
<span class="comment"># 2. Au démarrage, appuyer sur F12 si nécessaire</span>
<span class="comment"># 3. Sélectionner "Try or Install Ubuntu Server"</span>

<span class="comment"># 4. Configuration de l'installation :</span>
<span class="comment"># - Langue : English ou Français</span>
<span class="comment"># - Clavier : French ou votre layout</span>
<span class="comment"># - Type d'installation : Normal</span>
<span class="comment"># - Réseau : Configurer IPv4 si nécessaire</span>
<span class="comment"># - Proxy : Laisser vide</span>
<span class="comment"># - Mirror : Laisser par défaut</span>
<span class="comment"># - Stockage : Use entire disk</span>
<span class="comment"># - Profil : Install OpenSSH server (IMPORTANT!)</span>
<span class="comment"># - Snaps : Sélectionner selon besoins</span>
<span class="comment"># - Nom : ubuntu-server (ou autre)</span>
<span class="comment"># - Nom d'utilisateur : votre_nom</span>
<span class="comment"># - Mot de passe : ****** (notez-le!)</span></code></pre>
        </div>

        <div class="warning-box">
          <p><strong>⚠️ IMPORTANT :</strong> Cochez <strong>"Install OpenSSH server"</strong> pendant l'installation ! Cela évite d'avoir à l'installer manuellement après.</p>
        </div>
      </section>

      <!-- Étape 6 : Configuration SSH -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 6 : Configuration et test SSH</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Premier démarrage et connexion</h3>
          <pre><code class="language-bash"><span class="comment"># Après installation, la VM redémarre</span>
<span class="comment"># Se connecter avec l'utilisateur créé</span>

<span class="comment"># Vérifier l'adresse IP de la VM</span>
ip addr show
<span class="comment"># ou</span>
ip a

<span class="comment"># Notez l'adresse IP (ex: 192.168.1.50)</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Test de connexion SSH depuis l'hôte</h3>
          <pre><code class="language-bash"><span class="comment"># Depuis votre machine hôte (Windows/Linux/macOS)</span>
ssh utilisateur@adresse_ip_vm

<span class="comment"># Exemple :</span>
ssh john@192.168.1.50

<span class="comment"># Accepter l'empreinte SSH à la première connexion</span>
<span class="comment"># Saisir le mot de passe</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Si SSH n'est pas installé</h3>
          <pre><code class="language-bash"><span class="comment"># Se connecter directement sur la VM</span>
<span class="comment"># Installer OpenSSH :</span>
<span class="keyword">sudo</span> apt update
<span class="keyword">sudo</span> apt install openssh-server

<span class="comment"># Vérifier le service</span>
<span class="keyword">sudo</span> systemctl status ssh
<span class="keyword">sudo</span> systemctl enable ssh</code></pre>
        </div>
      </section>

      <!-- Étape 7 : Optimisations -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Étape 7 : Optimisations et bonnes pratiques</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Installation des Guest Additions</h3>
          <pre><code class="language-bash"><span class="comment"># Dans la VM, installer les outils nécessaires</span>
<span class="keyword">sudo</span> apt update
<span class="keyword">sudo</span> apt install build-essential dkms linux-headers-$(uname -r)

<span class="comment"># Dans le menu VirtualBox :</span>
<span class="comment"># Périphériques → Insérer l'image CD des Guest Additions</span>

<span class="comment"># Dans la VM :</span>
<span class="keyword">sudo</span> mount /dev/cdrom /mnt
<span class="keyword">sudo</span> /mnt/VBoxLinuxAdditions.run
<span class="keyword">sudo</span> reboot</code></pre>
          
          <div class="textExemple">
            <p><strong>Avantages des Guest Additions :</strong></p>
            <ul>
              <li>Meilleures performances graphiques</li>
              <li>Presse-papiers partagé</li>
              <li>Drag & drop entre hôte et invité</li>
              <li>Redimensionnement automatique de l'écran</li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Configuration des sauvegardes</h3>
          <pre><code class="language-bash"><span class="comment"># Cloner la VM pour faire des sauvegardes</span>
<span class="comment"># Clic droit sur la VM → Cloner</span>

<span class="comment"># Créer des snapshots avant des changements majeurs</span>
<span class="comment"># Machine → Prendre un snapshot</span>

<span class="comment"># Exporter la VM pour la déplacer</span>
<span class="comment"># Fichier → Exporter un appliance virtuel</span></code></pre>
        </div>
      </section>

      <!-- Résolution des problèmes -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Résolution des problèmes courants</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Problème : SSH impossible</h3>
          <pre><code class="language-bash"><span class="comment"># Vérifier que la VM est démarrée</span>
<span class="comment"># Vérifier l'adresse IP</span>
ip a

<span class="comment"># Vérifier le service SSH</span>
<span class="keyword">sudo</span> systemctl status ssh

<span class="comment"># Vérifier le firewall</span>
<span class="keyword">sudo</span> ufw status
<span class="comment"># Si actif, autoriser SSH :</span>
<span class="keyword">sudo</span> ufw allow ssh</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Problème : Pas d'accès réseau</h3>
          <pre><code class="language-bash"><span class="comment"># Vérifier la configuration réseau de la VM</span>
<span class="comment"># Paramètres → Réseau → Accès par pont</span>

<span class="comment"># Redémarrer le service réseau</span>
<span class="keyword">sudo</span> systemctl restart systemd-networkd

<span class="comment"># Vérifier la connexion</span>
ping 8.8.8.8</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Problème : Performances lentes</h3>
          <pre><code class="language-bash"><span class="comment"># Augmenter la RAM et les processeurs</span>
<span class="comment"># Paramètres → Système</span>

<span class="comment"># Activer l'accélération matérielle</span>
<span class="comment"># Paramètres → Système → Accélération</span>

<span class="comment"># Installer les Guest Additions</span>
<span class="comment"># Voir étape 7</span></code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Installation complète</h3>
          <p>Créez une VM Ubuntu Server avec SSH fonctionnel et connectez-vous depuis votre machine hôte.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>Étapes :</h4>
              <ol>
                <li>Installer VirtualBox</li>
                <li>Télécharger Ubuntu Server ISO</li>
                <li>Créer une VM avec accès par pont</li>
                <li>Installer Ubuntu avec OpenSSH server</li>
                <li>Noter l'adresse IP et se connecter via SSH</li>
              </ol>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Configuration avancée SSH</h3>
          <p>Configurez l'authentification par clés SSH sur votre VM.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code class="language-bash"><span class="comment"># Sur la machine hôte :</span>
ssh-keygen -t ed25519 -C "vm-ssh"
ssh-copy-id utilisateur@ip_vm

<span class="comment"># Test :</span>
ssh utilisateur@ip_vm
<span class="comment"># Doit se connecter sans mot de passe</span></code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 3 : Sauvegarde et restauration</h3>
          <p>Créez un snapshot de votre VM, puis restaurez-le.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>Étapes :</h4>
              <ol>
                <li>Machine → Prendre un snapshot (nom : "avant-changements")</li>
                <li>Faire des modifications dans la VM</li>
                <li>Machine → Restaurer le snapshot</li>
                <li>Vérifier que les modifications ont disparu</li>
              </ol>
            </div>
          </details>
        </div>
      </section>

      <!-- Ressources supplémentaires -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        <div class="code-example">
          <ul>
            <li><a href="https://www.virtualbox.org/manual/UserManual.html" class="btn-purple btn-hover" target="_blank">Manuel officiel VirtualBox</a></li>
            <li><a href="https://ubuntu.com/tutorials" class="btn-purple btn-hover" target="_blank">Tutoriels Ubuntu</a></li>
            <li><a href="/lessons/ssh" class="btn-purple btn-hover">Leçon sur SSH</a></li>
            <li><a href="/lessons/linux-permissions" class="btn-purple btn-hover">Leçon sur les permissions Linux</a></li>
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

/* Warning box */
.warning-box {
    background: #fff3cd;
    border: 1px solid #ffeaa7;
    border-radius: 8px;
    padding: 1.5rem;
    margin: 1rem 0;
    border-left: 4px solid #fdcb6e;
}

.warning-box p, .warning-box ul {
    margin-bottom: 0.5rem;
    color: #856404;
}

.warning-box ul {
    margin-left: 1.5rem;
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
    white-space: pre-wrap;
    word-wrap: break-word;
    word-break: break-word;
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
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