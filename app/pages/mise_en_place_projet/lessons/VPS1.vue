<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Créer un utilisateur Linux sur un VPS</h1>
                <p class="lesson-meta text-white">Linux • VPS • SSH • Sudo • Sécurité • MobaXterm</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi créer un utilisateur dédié ?</h2>
                <p class="textExemple">
                    Lors de la première connexion à un VPS (serveur privé virtuel), vous disposez généralement d’un accès <code>root</code>
                    via SSH. Utiliser le compte <code>root</code> pour les opérations quotidiennes est dangereux :
                    une erreur peut détruire le système, et les attaques par force brute ciblent souvent <code>root</code>.
                </p>
                <p class="textExemple">
                    La bonne pratique consiste à créer un utilisateur classique avec les droits <code>sudo</code>,
                    puis à désactiver l’accès SSH direct à <code>root</code>. Cette leçon vous guide pas à pas,
                    y compris avec l’outil <strong>MobaXterm</strong> sous Windows.
                </p>
            </section>

            <!-- Prérequis -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis</h2>
                <ul class="textExemple">
                    <li>Un VPS avec une distribution Linux (Ubuntu, Debian, CentOS, etc.)</li>
                    <li>Accès SSH avec le mot de passe ou la clé root fourni par l’hébergeur</li>
                    <li>Connexion Internet active</li>
                    <li>Optionnel : <strong>MobaXterm</strong> installé sur votre machine Windows (édition gratuite disponible sur mobaxterm.mobatek.net)</li>
                </ul>
            </section>

            <!-- Étape 1 : Connexion en root (avec MobaXterm) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">1. Se connecter en tant que root</h2>
                <p class="textExemple">
                    Utilisez la commande SSH avec l’adresse IP de votre VPS et le mot de passe root fourni.
                    Avec MobaXterm, la connexion est graphique.
                </p>

                <h3 class="text-purple">Avec MobaXterm :</h3>
                <ol>
                    <li>Lancez MobaXterm.</li>
                    <li>Cliquez sur <strong>Session</strong> (en haut à gauche) → <strong>SSH</strong>.</li>
                    <li>Dans le champ <strong>Remote host</strong>, saisissez l’IP ou le domaine de votre VPS.</li>
                    <li>Spécifiez le nom d’utilisateur : <code>root</code>.</li>
                    <li>Laissez le port par défaut (22) sauf si votre hébergeur en utilise un autre.</li>
                    <li>Cliquez sur <strong>OK</strong>. Une fenêtre de terminal s’ouvre et vous demande le mot de passe root.</li>
                </ol>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Variante en ligne de commande (si vous préférez)
ssh root@votre_ip_ou_domaine</code></pre>
                </div>
                <div class="warning-section">
                    <p class="warning-text">⚠️ Important : ne restez pas connecté en root plus longtemps que nécessaire.</p>
                </div>
            </section>

            <!-- Étape 2 : Créer un nouvel utilisateur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">2. Créer un utilisateur standard</h2>
                <p class="textExemple">
                    Une fois la session SSH ouverte (dans MobaXterm, vous êtes directement dans un terminal bash),
                    exécutez la commande <code>adduser</code> (plus conviviale) ou <code>useradd</code>.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Remplacer "monutilisateur" par le nom souhaité
adduser monutilisateur</code></pre>
                </div>
                <p class="textExemple">
                    Le système vous demandera de définir un mot de passe et quelques informations (nom, téléphone, etc.).
                    Vous pouvez laisser ces champs vides en appuyant sur Entrée.
                </p>
                <p class="textExemple">Variante avec <code>useradd</code> (plus minimal) :</p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">useradd -m -s /bin/bash monutilisateur
passwd monutilisateur</code></pre>
                </div>
                <ul>
                    <li><code>-m</code> : crée le répertoire home <code>/home/monutilisateur</code></li>
                    <li><code>-s /bin/bash</code> : définit le shell bash</li>
                </ul>
            </section>

            <!-- Étape 3 : Ajouter l'utilisateur au groupe sudo -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">3. Donner les droits sudo</h2>
                <p class="textExemple">
                    L’utilisateur doit pouvoir exécuter des commandes administratives sans être root. Sous Ubuntu/Debian,
                    on utilise le groupe <code>sudo</code>. Sous CentOS/RHEL, le groupe se nomme <code>wheel</code>.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Ubuntu / Debian
usermod -aG sudo monutilisateur

# CentOS / RHEL
usermod -aG wheel monutilisateur</code></pre>
                </div>
                <p class="textExemple">
                    Vérifiez que l’utilisateur est bien dans le groupe :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">groups monutilisateur</code></pre>
                </div>
            </section>

            <!-- Étape 4 : Configurer SSH (clé publique) avec MobaXterm -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">4. Configurer l’authentification par clé SSH (avec MobaXterm)</h2>
                <p class="textExemple">
                    L’utilisation d’une clé SSH est plus sécurisée que le mot de passe. MobaXterm intègre un outil graphique pour générer et copier les clés.
                </p>

                <h3 class="text-purple">Générer une paire de clés (si vous n’en avez pas) :</h3>
                <ol>
                    <li>Dans MobaXterm, allez dans <strong>Tools</strong> → <strong>MobaKeyGen</strong>.</li>
                    <li>Cliquez sur <strong>Generate</strong>. Bougez la souris pour créer l’aléa.</li>
                    <li>Une fois générée, vous pouvez ajouter un commentaire (ex: <code>ma-cle-vps</code>) et un mot de passe (optionnel).</li>
                    <li>Sauvegardez la clé privée (format .ppk ou OpenSSH) et la clé publique (fichier .pub).</li>
                </ol>

                <h3 class="text-purple">Copier la clé publique sur le serveur :</h3>
                <p class="textExemple">
                    Depuis votre session root (dans MobaXterm), créez le répertoire <code>.ssh</code> de l’utilisateur et ajoutez-y la clé publique.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">mkdir -p /home/monutilisateur/.ssh
nano /home/monutilisateur/.ssh/authorized_keys
# Collez le contenu de votre clé publique (fichier .pub)
chown -R monutilisateur:monutilisateur /home/monutilisateur/.ssh
chmod 700 /home/monutilisateur/.ssh
chmod 600 /home/monutilisateur/.ssh/authorized_keys</code></pre>
                </div>
                <p class="textExemple">
                    <strong>Alternative plus simple avec MobaXterm :</strong> utilisez l’outil intégré <strong>MobaSSHKeyCopy</strong> (Tools → MobaSSHKeyCopy) 
                    pour envoyer automatiquement votre clé publique vers l’utilisateur distant.
                </p>
                <p class="textExemple">
                    Pour les utilisateurs d’OpenSSH classique, la commande <code>ssh-copy-id</code> fonctionne aussi depuis le terminal MobaXterm :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">ssh-copy-id monutilisateur@votre_ip</code></pre>
                </div>
            </section>

            <!-- Étape 5 : Désactiver l’accès root SSH -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">5. Désactiver la connexion SSH root (sécurité)</h2>
                <p class="textExemple">
                    Une fois que l’utilisateur sudo fonctionne et que vous pouvez vous connecter avec lui,
                    éditez le fichier de configuration SSH pour interdire root.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">nano /etc/ssh/sshd_config</code></pre>
                </div>
                <p class="textExemple">
                    Trouvez la ligne <code>PermitRootLogin</code> et changez-la en :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-text">PermitRootLogin no</code></pre>
                </div>
                <p class="textExemple">
                    Redémarrez le service SSH :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">systemctl restart sshd   # ou service ssh restart</code></pre>
                </div>
                <div class="warning-section">
                    <p class="warning-text">
                        ⚠️ Avant de fermer la session root, <strong>testez impérativement</strong> une nouvelle connexion avec votre utilisateur
                        dans un autre onglet MobaXterm (ou une nouvelle session). Sinon, vous pourriez vous verrouiller hors du serveur.
                    </p>
                </div>
            </section>

            <!-- Étape 6 : Autres sécurisations recommandées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">6. Sécurisations complémentaires</h2>
                <div class="textExemple">
                    <h3 class="text-purple">Changer le port SSH (optionnel)</h3>
                    <p>Modifiez le port par défaut 22 pour réduire les attaques automatiques :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">Port 2222</code></pre>
                    </div>
                    <p>N’oubliez pas d’ouvrir ce port dans le pare-feu.</p>

                    <h3 class="text-purple">Désactiver l’authentification par mot de passe (clé uniquement)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-text">PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no</code></pre>
                    </div>

                    <h3 class="text-purple">Configurer le pare-feu (UFW)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">ufw allow 22/tcp      # ou votre nouveau port
ufw allow 80/tcp
ufw allow 443/tcp
ufw enable</code></pre>
                    </div>

                    <h3 class="text-purple">Utiliser MobaXterm pour gérer plusieurs sessions</h3>
                    <p>
                        MobaXterm permet d’enregistrer des sessions SSH avec des utilisateurs différents.
                        Créez une session pour <code>monutilisateur</code> (avec clé privée) et une autre pour <code>root</code> (si besoin de secours).
                        Vous pouvez ainsi basculer facilement.
                    </p>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques essentielles</h2>
                <ul class="textExemple">
                    <li><strong>Utilisez des mots de passe complexes</strong> pour l’utilisateur (ou mieux, des clés SSH).</li>
                    <li><strong>Ne travaillez jamais directement en root</strong> ; utilisez <code>sudo</code> avec parcimonie.</li>
                    <li><strong>Activez l’historique des commandes sudo</strong> pour auditer les actions.</li>
                    <li><strong>Mettez à jour régulièrement le système</strong> (<code>apt update &amp;&amp; apt upgrade</code>).</li>
                    <li><strong>Surveillez les tentatives de connexion</strong> avec <code>fail2ban</code>.</li>
                    <li><strong>Sauvegardez la configuration SSH</strong> avant toute modification.</li>
                    <li><strong>Avec MobaXterm</strong>, pensez à utiliser le gestionnaire de mots de passe intégré pour stocker vos identifiants en sécurité.</li>
                </ul>
            </section>

            <!-- Section dédiée à MobaXterm (synthèse) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi et comment utiliser MobaXterm ?</h2>
                <p class="textExemple">
                    MobaXterm est un client SSH, X11 et RDP tout-en-un pour Windows. Il offre une interface onglets,
                    un explorateur de fichiers intégré, un transfert de fichiers glisser-déposer, et bien plus.
                </p>
                <h3 class="text-purple">Avantages pour la gestion de VPS :</h3>
                <ul>
                    <li><strong>Connexion SSH rapide</strong> : enregistrez vos serveurs avec nom d’utilisateur, port et clé privée.</li>
                    <li><strong>Transfert de fichiers</strong> : glissez-déposez depuis l’explorateur Windows vers le serveur (ou l’inverse).</li>
                    <li><strong>Gestion de clés intégrée</strong> : MobaKeyGen et MobaSSHKeyCopy facilitent la mise en place de l’authentification par clé.</li>
                    <li><strong>Multi-sessions</strong> : ouvrez plusieurs onglets pour différents utilisateurs ou serveurs.</li>
                    <li><strong>Terminal local + distant</strong> : vous pouvez aussi exécuter des commandes locales (Windows) dans le même outil.</li>
                </ul>
                <p class="textExemple">
                    Pour suivre les étapes de cette leçon avec MobaXterm, il vous suffit de remplacer chaque commande SSH classique
                    par une session graphique. Toutes les commandes Linux (adduser, usermod, nano, etc.) s’exécutent exactement de la même manière
                    dans le terminal de MobaXterm une fois connecté.
                </p>
                <p class="textExemple">
                    <strong>Récapitulatif des actions dans MobaXterm :</strong>
                </p>
                <ol>
                    <li>Créer une session SSH root (host = IP, user = root).</li>
                    <li>Exécuter <code>adduser</code> et <code>usermod</code>.</li>
                    <li>Générer/copier la clé publique via MobaKeyGen.</li>
                    <li>Se déconnecter root, puis créer une nouvelle session SSH avec l’utilisateur standard (en utilisant la clé privée).</li>
                    <li>Modifier <code>/etc/ssh/sshd_config</code> avec <code>nano</code> depuis cette session (ou via sudo).</li>
                    <li>Redémarrer SSH et tester.</li>
                </ol>
            </section>

            <!-- Vérification et dépannage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Vérifications et commandes utiles</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Voir les utilisateurs du système
cat /etc/passwd

# Voir les groupes d’un utilisateur
groups monutilisateur

# Vérifier la configuration SSH sans redémarrer
sshd -t

# Lister les sessions actives
who
w

# Basculer sur l’utilisateur sans se déconnecter (root -> utilisateur)
su - monutilisateur

# Exécuter une commande spécifique avec sudo
sudo -l   # lister les droits disponibles</code></pre>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    La création d’un utilisateur dédié dès la première connexion à un VPS est une étape fondamentale de la sécurisation.
                    Elle isole les actions administratives, réduit les risques d’erreurs destructrices et limite la surface d’attaque.
                </p>
                <p class="textExemple">
                    En utilisant <strong>MobaXterm</strong>, vous bénéficiez d’un environnement graphique puissant qui simplifie la gestion
                    des clés SSH, le transfert de fichiers et la navigation entre plusieurs sessions.
                </p>
                <p class="textExemple">
                    Une fois l’utilisateur configuré avec <code>sudo</code> et l’authentification par clé SSH, vous pouvez administrer
                    votre serveur sereinement, tout en ayant désactivé l’accès root direct.
                </p>
                <p class="textExemple">
                    Prochaines étapes recommandées : installer et configurer <code>fail2ban</code>, mettre en place une veille de sécurité,
                    et automatiser les mises à jour avec <code>unattended-upgrades</code>.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'LinuxUserCreationLesson',

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
                    const languages = ['bash', 'text'];
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
/* === Styles identiques aux leçons précédentes (formulaires Symfony, migrations, etc.) === */
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
.border-purple { border: 2px solid #e0d6ff; transition: all 0.3s ease; }
.text-purple { color: #6A3093 !important; }
.text-white { color: white !important; }

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

.code-example {
    margin: 1.5rem 0;
    width: 100%;
    box-sizing: border-box;
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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
}

.warning-text {
    color: #d63031;
    font-weight: bold;
    margin-top: 0.5rem;
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