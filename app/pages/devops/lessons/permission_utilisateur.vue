<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Gestion des Permissions Linux</h1>
        <p class="lesson-meta text-white">Comprendre et maîtriser les utilisateurs, groupes et permissions sous Linux</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux permissions Linux</h2>
        <p class="textExemple">
          Le système de permissions Linux est un mécanisme de sécurité fondamental qui contrôle l'accès aux fichiers, répertoires et ressources système. Une bonne compréhension de ce système est essentielle pour :
        </p>
        <ul class="textExemple">
          <li>Sécuriser l'accès aux fichiers sensibles</li>
          <li>Gérer plusieurs utilisateurs sur un même système</li>
          <li>Configurer correctement les services et applications</li>
          <li>Éviter les failles de sécurité</li>
        </ul>
      </section>

      <!-- Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Concepts fondamentaux</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Les trois types d'entités</h3>
          <ul class="textExemple">
            <li><strong>Utilisateur (User - u)</strong> : Le propriétaire du fichier</li>
            <li><strong>Groupe (Group - g)</strong> : Les membres du groupe associé</li>
            <li><strong>Autres (Others - o)</strong> : Tous les autres utilisateurs</li>
          </ul>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Les trois types de permissions</h3>
          <ul class="textExemple">
            <li><strong>Lecture (Read - r)</strong> : Permission de lire un fichier</li>
            <li><strong>Écriture (Write - w)</strong> : Permission de modifier un fichier</li>
            <li><strong>Exécution (Execute - x)</strong> : Permission d'exécuter un fichier</li>
          </ul>
        </div>
      </section>

      <!-- Visualisation des permissions -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Visualisation des permissions</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Commande ls -l</h3>
          <pre><code class="language-bash"><span class="comment"># Afficher les permissions détaillées</span>
ls -l

<span class="comment"># Exemple de sortie :</span>
-rwxr-xr-- 1 john developers 2048 Jan 15 10:30 mon_script.sh
drwxr-x--- 2 alice www-data 4096 Jan 15 10:25 mon_dossier/</code></pre>
          
          <div class="textExemple">
            <p><strong>Structure de la sortie :</strong></p>
            <ul>
              <li><strong>-rwxr-xr--</strong> : Permissions (10 caractères)</li>
              <li><strong>1</strong> : Nombre de liens</li>
              <li><strong>john</strong> : Propriétaire</li>
              <li><strong>developers</strong> : Groupe</li>
              <li><strong>2048</strong> : Taille en octets</li>
              <li><strong>Jan 15 10:30</strong> : Date de modification</li>
              <li><strong>mon_script.sh</strong> : Nom du fichier</li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Comprendre le format des permissions</h3>
          <pre><code class="language-bash"><span class="comment"># Exemple : -rwxr-xr--</span>
<span class="comment"># Position 1 : Type de fichier</span>
- <span class="comment">= fichier ordinaire</span>
d <span class="comment">= répertoire</span>
l <span class="comment">= lien symbolique</span>

<span class="comment"># Positions 2-4 : Permissions utilisateur (u)</span>
rwx <span class="comment">= lecture, écriture, exécution</span>

<span class="comment"># Positions 5-7 : Permissions groupe (g)</span>
r-x <span class="comment">= lecture, pas écriture, exécution</span>

<span class="comment"># Positions 8-10 : Permissions autres (o)</span>
r-- <span class="comment">= lecture, pas écriture, pas exécution</span></code></pre>
        </div>
      </section>

      <!-- Modification des permissions -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Modification des permissions avec chmod</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Méthode symbolique</h3>
          <pre><code class="language-bash"><span class="comment"># Syntaxe : chmod [ugoa][+-=][rwx] fichier</span>

<span class="comment"># Ajouter la permission d'exécution pour l'utilisateur</span>
chmod u+x mon_script.sh

<span class="comment"># Retirer la permission d'écriture pour le groupe</span>
chmod g-w mon_fichier.txt

<span class="comment"># Définir des permissions spécifiques pour les autres</span>
chmod o=r mon_fichier.conf

<span class="comment"># Combinaisons multiples</span>
chmod ug+rw,o-rwx fichier_important</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Méthode numérique (octale)</h3>
          <pre><code class="language-bash"><span class="comment"># Syntaxe : chmod XXX fichier</span>
<span class="comment"># Lecture (r) = 4, Écriture (w) = 2, Exécution (x) = 1</span>

<span class="comment"># Exemples courants :</span>
chmod 644 mon_fichier.txt      <span class="comment"># rw-r--r--</span>
chmod 755 mon_script.sh        <span class="comment"># rwxr-xr-x</span>
chmod 600 fichier_prive.key    <span class="comment"># rw-------</span>
chmod 750 dossier_restreint/   <span class="comment"># rwxr-x---</span>
chmod 777 tout_le_monde        <span class="comment"># rwxrwxrwx (DÉCONSEILLÉ !)</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Permissions récursives</h3>
          <pre><code class="language-bash"><span class="comment"># Appliquer les permissions à un dossier et son contenu</span>
chmod -R 755 mon_dossier/

<span class="comment"># Changer les permissions de tous les fichiers .sh</span>
chmod +x *.sh</code></pre>
        </div>
      </section>

      <!-- Gestion des utilisateurs et groupes -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Gestion des utilisateurs et groupes</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Commandes utilisateurs</h3>
          <pre><code class="language-bash"><span class="comment"># Ajouter un nouvel utilisateur</span>
<span class="keyword">sudo</span> useradd -m -s /bin/bash nouvel_utilisateur

<span class="comment"># OU (méthode recommandée sur Ubuntu/Debian)</span>
<span class="keyword">sudo</span> adduser nouvel_utilisateur

<span class="comment"># Supprimer un utilisateur</span>
<span class="keyword">sudo</span> userdel -r ancien_utilisateur

<span class="comment"># Modifier un utilisateur</span>
<span class="keyword">sudo</span> usermod -aG sudo utilisateur  <span class="comment"># Ajouter aux sudoers</span>
<span class="keyword">sudo</span> usermod -s /bin/sh utilisateur <span class="comment"># Changer le shell</span>

<span class="comment"># Vérifier les informations d'un utilisateur</span>
id utilisateur
whoami</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Commandes groupes</h3>
          <pre><code class="language-bash"><span class="comment"># Créer un nouveau groupe</span>
<span class="keyword">sudo</span> groupadd mon_groupe

<span class="comment"># Supprimer un groupe</span>
<span class="keyword">sudo</span> groupdel ancien_groupe

<span class="comment"># Ajouter un utilisateur à un groupe</span>
<span class="keyword">sudo</span> usermod -aG mon_groupe utilisateur

<span class="comment"># Vérifier les groupes d'un utilisateur</span>
groups utilisateur

<span class="comment"># Lister tous les groupes</span>
getent group</code></pre>
        </div>
      </section>

      <!-- Obtention des droits sudo -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Obtention des droits administrateur (sudo)</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Vérification des droits actuels</h3>
          <pre><code class="language-bash"><span class="comment"># Vérifier si vous avez les droits sudo</span>
<span class="keyword">sudo</span> -l

<span class="comment"># Tester une commande avec sudo</span>
<span class="keyword">sudo</span> whoami  <span class="comment"># Doit retourner "root"</span>

<span class="comment"># Vérifier les groupes de l'utilisateur</span>
groups $USER</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Méthodes pour obtenir les droits sudo</h3>
          
          <h4 class="text-purple">Méthode 1 : Ajouter l'utilisateur au groupe sudo</h4>
          <pre><code class="language-bash"><span class="comment"># Se connecter en tant que root ou avec un utilisateur ayant déjà sudo</span>
<span class="keyword">sudo</span> usermod -aG sudo nom_utilisateur

<span class="comment"># Déconnexion/reconnexion nécessaire pour que les changements prennent effet</span></code></pre>

          <h4 class="text-purple">Méthode 2 : Modifier le fichier sudoers</h4>
          <pre><code class="language-bash"><span class="comment"># Éditer le fichier sudoers de manière sécurisée</span>
<span class="keyword">sudo</span> visudo

<span class="comment"># Ajouter la ligne suivante :</span>
nom_utilisateur ALL=(ALL:ALL) ALL</code></pre>

          <div class="warning-box">
            <p><strong>⚠️ Attention :</strong> Utilisez toujours <code>visudo</code> pour modifier le fichier sudoers. Une erreur de syntaxe peut rendre le système inaccessible !</p>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Configuration avancée sudoers</h3>
          <pre><code class="language-bash"><span class="comment"># Exemples de configurations dans /etc/sudoers :</span>

<span class="comment"># Permettre toutes les commandes</span>
utilisateur ALL=(ALL:ALL) ALL

<span class="comment"># Permettre seulement certaines commandes</span>
utilisateur ALL=(ALL:ALL) /bin/systemctl, /usr/bin/apt

<span class="comment"># Sans demande de mot de passe</span>
utilisateur ALL=(ALL:ALL) NOPASSWD: ALL

<span class="comment"># Groupe entier</span>
%sudo ALL=(ALL:ALL) ALL</code></pre>
        </div>
      </section>

      <!-- Changement de propriétaire avec chown -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Changement de propriétaire avec chown</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Utilisation de base</h3>
          <pre><code class="language-bash"><span class="comment"># Changer le propriétaire d'un fichier</span>
<span class="keyword">sudo</span> chown nouvel_utilisateur mon_fichier.txt

<span class="comment"># Changer le groupe d'un fichier</span>
<span class="keyword">sudo</span> chgrp nouveau_groupe mon_fichier.txt

<span class="comment"># Changer propriétaire et groupe en une commande</span>
<span class="keyword">sudo</span> chown utilisateur:groupe mon_fichier.txt

<span class="comment"># Appliquer récursivement</span>
<span class="keyword">sudo</span> chown -R utilisateur:groupe mon_dossier/</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Cas d'utilisation courants</h3>
          <pre><code class="language-bash"><span class="comment"># Donner l'accès à un dossier web à l'utilisateur www-data</span>
<span class="keyword">sudo</span> chown -R www-data:www-data /var/www/html/

<span class="comment"># Partager un dossier entre plusieurs utilisateurs</span>
<span class="keyword">sudo</span> chown -R utilisateur:groupe_partage /dossier_partage/
<span class="keyword">sudo</span> chmod -R 775 /dossier_partage/</code></pre>
        </div>
      </section>

      <!-- Permissions spéciales -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Permissions spéciales</h2>
        
        <div class="code-example">
          <h3 class="text-purple">SUID (Set User ID)</h3>
          <pre><code class="language-bash"><span class="comment"># Fichier exécuté avec les permissions du propriétaire</span>
chmod u+s fichier_executable
<span class="comment"># OU</span>
chmod 4755 fichier_executable

<span class="comment"># Exemple : /usr/bin/passwd</span>
ls -l /usr/bin/passwd
<span class="comment"># -rwsr-xr-x 1 root root ...</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">SGID (Set Group ID)</h3>
          <pre><code class="language-bash"><span class="comment"># Fichiers créés dans le dossier héritent du groupe du dossier</span>
chmod g+s mon_dossier/
<span class="comment"># OU</span>
chmod 2755 mon_dossier/</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Sticky Bit</h3>
          <pre><code class="language-bash"><span class="comment"># Seul le propriétaire peut supprimer ses fichiers dans un dossier partagé</span>
chmod +t /dossier_partage/
<span class="comment"># OU</span>
chmod 1777 /dossier_partage/

<span class="comment"># Exemple : /tmp</span>
ls -ld /tmp
<span class="comment"># drwxrwxrwt ...</span></code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques de sécurité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques de sécurité</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Règles essentielles</h3>
          <ul class="textExemple">
            <li><strong>Principe du moindre privilège</strong> : Donner seulement les permissions nécessaires</li>
            <li><strong>Éviter chmod 777</strong> : Très dangereux pour la sécurité</li>
            <li><strong>Utiliser les groupes</strong> pour gérer les accès multiples</li>
            <li><strong>Auditer régulièrement</strong> les permissions des fichiers sensibles</li>
            <li><strong>Limiter l'usage de SUID/SGID</strong> aux cas absolument nécessaires</li>
          </ul>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Permissions recommandées</h3>
          <pre><code class="language-bash"><span class="comment"># Fichiers de configuration sensibles</span>
chmod 600 /etc/motd
chmod 640 /etc/shadow

<span class="comment"># Scripts système</span>
chmod 755 /usr/local/bin/mon_script

<span class="comment"># Dossiers partagés</span>
chmod 2775 /opt/partage_equipe

<span class="comment"># Clés SSH</span>
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 700 ~/.ssh/</code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Analyse de permissions</h3>
          <p>Créez un fichier et analysez ses permissions avec <code>ls -l</code>. Comprenez chaque partie de la sortie.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code class="language-bash">touch mon_fichier.txt
ls -l mon_fichier.txt</code></pre>
              <p>Analysez : type de fichier, permissions utilisateur/groupe/autres, propriétaire, groupe, etc.</p>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Configuration d'un dossier partagé</h3>
          <p>Créez un dossier partagé accessible en lecture/écriture par un groupe spécifique.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>Étape 1 : Création du groupe et des utilisateurs</h4>
              <pre><code class="language-bash">sudo groupadd equipe_dev
sudo usermod -aG equipe_dev utilisateur1
sudo usermod -aG equipe_dev utilisateur2</code></pre>
              
              <h4>Étape 2 : Configuration du dossier</h4>
              <pre><code class="language-bash">sudo mkdir /opt/projet_equipe
sudo chown root:equipe_dev /opt/projet_equipe
sudo chmod 2775 /opt/projet_equipe</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 3 : Obtention des droits sudo</h3>
          <p>Si vous n'avez pas les droits sudo, demandez à un administrateur de vous les accorder en utilisant les méthodes appropriées.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>Méthode recommandée :</h4>
              <pre><code class="language-bash"><span class="comment"># L'administrateur doit exécuter :</span>
sudo usermod -aG sudo votre_nom_utilisateur</code></pre>
              <p>Déconnectez-vous et reconnectez-vous pour que les changements prennent effet.</p>
            </div>
          </details>
        </div>
      </section>

      <!-- Ressources supplémentaires -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        <div class="code-example">
          <ul>
            <li><a href="https://man7.org/linux/man-pages/man1/chmod.1.html" class="btn-purple btn-hover" target="_blank">Manuel chmod</a></li>
            <li><a href="https://man7.org/linux/man-pages/man1/chown.1.html" class="btn-purple btn-hover" target="_blank">Manuel chown</a></li>
            <li><a href="https://man7.org/linux/man-pages/man5/sudoers.5.html" class="btn-purple btn-hover" target="_blank">Manuel sudoers</a></li>
            <li><a href="/lessons/ssh" class="btn-purple btn-hover">Leçon sur SSH</a></li>
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

.warning-box p {
    margin-bottom: 0.5rem;
    color: #856404;
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