<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Attribution des droits Sudo sous Linux</h1>
                <p class="lesson-meta text-white">Guide complet pour donner les privilèges administrateur à un
                    utilisateur</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux droits Sudo</h2>
                <p class="textExemple">
                    Les droits <strong>sudo</strong> (SuperUser DO) permettent à un utilisateur standard d'exécuter des
                    commandes avec les privilèges d'administration. Cette leçon couvre toutes les méthodes pour accorder
                    ces droits de manière sécurisée.
                </p>

                <div class="warning-box">
                    <p><strong>⚠️ Précautions importantes :</strong></p>
                    <ul>
                        <li>Ne donnez les droits sudo qu'aux utilisateurs de confiance</li>
                        <li>Utilisez toujours des méthodes sécurisées pour modifier les permissions</li>
                        <li>Auditez régulièrement les utilisateurs ayant des privilèges sudo</li>
                    </ul>
                </div>
            </section>

            <!-- Prérequis et vérifications -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis et vérifications</h2>

                <div class="code-example">
                    <h3 class="text-purple">Vérifier les droits actuels</h3>
                    <pre><code class="language-bash"><span class="comment"># Vérifier si l'utilisateur a déjà des droits sudo</span>
<span class="keyword">sudo</span> -l

<span class="comment"># Tester une commande sudo</span>
<span class="keyword">sudo</span> whoami

<span class="comment"># Vérifier les groupes de l'utilisateur</span>
groups $USER
id $USER

<span class="comment"># Vérifier si l'utilisateur existe</span>
id nom_utilisateur</code></pre>

                    <div class="textExemple">
                        <p><strong>Interprétation des résultats :</strong></p>
                        <ul>
                            <li>Si <code>sudo whoami</code> retourne <code>root</code> → droits sudo actifs</li>
                            <li>Si <code>groups</code> montre <code>sudo</code> ou <code>wheel</code> → probablement des
                                droits sudo</li>
                            <li>Si erreur "user is not in the sudoers file" → pas de droits sudo</li>
                        </ul>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Vérifier l'accès root</h3>
                    <pre><code class="language-bash"><span class="comment"># Se connecter en tant que root (si le mot de passe root est activé)</span>
su -

<span class="comment"># OU utiliser sudo si vous avez déjà les droits</span>
<span class="keyword">sudo</span> -i</code></pre>

                    <div class="warning-box">
                        <p><strong>Note :</strong> Vous devez avoir un accès root (direct ou via un autre utilisateur
                            sudo) pour accorder les droits sudo à un nouvel utilisateur.</p>
                    </div>
                </div>
            </section>

            <!-- Méthode 1 : Groupe sudo -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 1 : Ajout au groupe sudo (Recommandée)</h2>

                <div class="code-example">
                    <h3 class="text-purple">Pour Ubuntu/Debian/Mint</h3>
                    <pre><code class="language-bash"><span class="comment"># Se connecter en tant que root ou avec un utilisateur ayant sudo</span>
<span class="keyword">sudo</span> su -

<span class="comment"># Ajouter l'utilisateur au groupe sudo</span>
usermod -aG sudo nom_utilisateur

<span class="comment"># Vérifier l'ajout</span>
groups nom_utilisateur</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Pour CentOS/RHEL/Fedora</h3>
                    <pre><code class="language-bash"><span class="comment"># Sur les systèmes utilisant le groupe 'wheel'</span>
usermod -aG wheel nom_utilisateur

<span class="comment"># Vérifier l'ajout</span>
groups nom_utilisateur</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Pour Arch Linux</h3>
                    <pre><code class="language-bash"><span class="comment"># Ajouter au groupe wheel</span>
usermod -aG wheel nom_utilisateur

<span class="comment"># Vérifier que wheel est configuré dans sudoers</span>
grep wheel /etc/sudoers</code></pre>
                </div>

                <div class="textExemple">
                    <h4 class="text-purple">Avantages de cette méthode :</h4>
                    <ul>
                        <li>✅ Simple et rapide</li>
                        <li>✅ Gestion centralisée via les groupes</li>
                        <li>✅ Facile à auditer</li>
                        <li>✅ Moins de risques d'erreur</li>
                    </ul>
                </div>
            </section>

            <!-- Méthode 2 : Fichier sudoers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 2 : Modification du fichier sudoers</h2>

                <div class="code-example">
                    <h3 class="text-purple">Utilisation de visudo (SÉCURISÉ)</h3>
                    <pre><code class="language-bash"><span class="comment"># Toujours utiliser visudo pour modifier sudoers</span>
<span class="keyword">sudo</span> visudo</code></pre>

                    <div class="warning-box">
                        <p><strong>⚠️ CRITIQUE :</strong> Utilisez <strong>toujours</strong> <code>visudo</code> et
                            jamais <code>nano /etc/sudoers</code> directement. <code>visudo</code> vérifie la syntaxe et
                            empêche les erreurs qui pourraient bloquer l'accès sudo !</p>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Ajouter un utilisateur spécifique</h3>
                    <pre><code class="language-bash"><span class="comment"># Dans visudo, ajouter à la fin :</span>

<span class="comment"># Donner tous les droits</span>
nom_utilisateur ALL=(ALL:ALL) ALL

<span class="comment"># OU donner des droits limités</span>
nom_utilisateur ALL=(ALL:ALL) /bin/systemctl, /usr/bin/apt

<span class="comment"># OU sans mot de passe (DÉCONSEILLÉ)</span>
nom_utilisateur ALL=(ALL:ALL) NOPASSWD: ALL</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Explications de la syntaxe</h3>
                    <pre><code class="language-bash">utilisateur machines=(cible:groupe_cible) commandes

<span class="comment"># Exemple : john ALL=(ALL:ALL) ALL</span>
<span class="comment"># john → Nom de l'utilisateur</span>
<span class="comment"># ALL → Toutes les machines</span>
<span class="comment"># (ALL:ALL) → Peut exécuter en tant que n'importe quel utilisateur et groupe</span>
<span class="comment"># ALL → Toutes les commandes</span></code></pre>
                </div>
            </section>

            <!-- Méthode 3 : Fichiers inclus -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 3 : Fichiers inclus (Recommandée pour les serveurs)</h2>

                <div class="code-example">
                    <h3 class="text-purple">Créer un fichier dans /etc/sudoers.d/</h3>
                    <pre><code class="language-bash"><span class="comment"># Créer un fichier dédié pour l'utilisateur</span>
<span class="keyword">sudo</span> visudo -f /etc/sudoers.d/nom_utilisateur

<span class="comment"># Ajouter la configuration :</span>
nom_utilisateur ALL=(ALL:ALL) ALL

<span class="comment"># Vérifier les permissions du fichier</span>
<span class="keyword">sudo</span> chmod 440 /etc/sudoers.d/nom_utilisateur</code></pre>
                </div>

                <div class="textExemple">
                    <h4 class="text-purple">Avantages de cette méthode :</h4>
                    <ul>
                        <li>✅ Configuration modulaire</li>
                        <li>✅ Facile à gérer et supprimer</li>
                        <li>✅ Évite les conflits lors des mises à jour</li>
                        <li>✅ Idéal pour l'automatisation</li>
                    </ul>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Exemple de gestion automatisée</h3>
                    <pre><code class="language-bash"><span class="comment"># Script pour ajouter un utilisateur sudo rapidement</span>
<span class="keyword">sudo</span> useradd -m -s /bin/bash nouvel_admin
<span class="keyword">sudo</span> passwd nouvel_admin
echo "nouvel_admin ALL=(ALL:ALL) ALL" | <span class="keyword">sudo</span> tee /etc/sudoers.d/nouvel_admin
<span class="keyword">sudo</span> chmod 440 /etc/sudoers.d/nouvel_admin</code></pre>
                </div>
            </section>

            <!-- Méthode 4 : Droits limités -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 4 : Droits sudo limités</h2>

                <div class="code-example">
                    <h3 class="text-purple">Exemples de configurations spécifiques</h3>
                    <pre><code class="language-bash"><span class="comment"># Permettre seulement la gestion des services</span>
utilisateur_services ALL=(ALL:ALL) /bin/systemctl

<span class="comment"># Permettre seulement la gestion des paquets</span>
utilisateur_paquets ALL=(ALL:ALL) /usr/bin/apt, /usr/bin/apt-get

<span class="comment"># Permettre seulement le redémarrage de services spécifiques</span>
utilisateur_web ALL=(ALL:ALL) /bin/systemctl restart apache2, /bin/systemctl restart nginx

<span class="comment"># Permettre la gestion des sauvegardes</span>
utilisateur_backup ALL=(ALL:ALL) /bin/tar, /usr/bin/rsync, /bin/mkdir</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Avec restrictions de répertoire</h3>
                    <pre><code class="language-bash"><span class="comment"># Permettre toutes les commandes dans un répertoire spécifique</span>
utilisateur_dev ALL=(ALL:ALL) /home/projets/*

<span class="comment"># Interdire certaines commandes dangereuses</span>
utilisateur ALL=(ALL:ALL) ALL, !/bin/su, !/usr/bin/passwd root</code></pre>
                </div>
            </section>

            <!-- Validation et test -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Validation et tests</h2>

                <div class="code-example">
                    <h3 class="text-purple">Tests de fonctionnement</h3>
                    <pre><code class="language-bash"><span class="comment"># Se déconnecter et se reconnecter pour appliquer les changements</span>
logout
<span class="comment"># Puis se reconnecter</span>

<span class="comment"># Tester les droits sudo</span>
<span class="keyword">sudo</span> whoami
<span class="comment"># Doit retourner : root</span>

<span class="comment"># Vérifier les commandes autorisées</span>
<span class="keyword">sudo</span> -l

<span class="comment"># Tester une commande administrateur</span>
<span class="keyword">sudo</span> apt update
<span class="keyword">sudo</span> systemctl status ssh</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Dépannage des problèmes courants</h3>
                    <pre><code class="language-bash"><span class="comment"># Erreur : "user is not in the sudoers file"</span>
<span class="comment"># → Vérifier l'orthographe du nom d'utilisateur</span>
<span class="comment"># → Vérifier le groupe sudo/wheel</span>
<span class="comment"># → Vérifier la syntaxe dans sudoers</span>

<span class="comment"># Erreur de syntaxe dans sudoers</span>
<span class="comment"># → Utiliser visudo pour corriger</span>
<span class="comment"># → Vérifier avec : visudo -c</span>

<span class="comment"># Problème de groupe</span>
<span class="comment"># → Vérifier : groups nom_utilisateur</span>
<span class="comment"># → Réappliquer : usermod -aG sudo nom_utilisateur</span></code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques de sécurité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques de sécurité</h2>

                <div class="code-example">
                    <h3 class="text-purple">Règles essentielles</h3>
                    <ul class="textExemple">
                        <li><strong>Principe du moindre privilège</strong> : Donnez seulement les permissions
                            nécessaires</li>
                        <li><strong>Évitez NOPASSWD</strong> : Sauf pour des cas très spécifiques et contrôlés</li>
                        <li><strong>Audit régulier</strong> : Vérifiez périodiquement les utilisateurs sudo</li>
                        <li><strong>Utilisez des groupes</strong> : Plus facile à gérer que les utilisateurs individuels
                        </li>
                        <li><strong>Journalisation</strong> : Surveillez l'usage des commandes sudo</li>
                    </ul>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Commandes d'audit</h3>
                    <pre><code class="language-bash"><span class="comment"># Lister tous les utilisateurs sudo</span>
getent group sudo
getent group wheel

<span class="comment"># Vérifier les fichiers sudoers actifs</span>
<span class="keyword">sudo</span> grep -r -i "" /etc/sudoers.d/

<span class="comment"># Voir les logs sudo</span>
<span class="keyword">sudo</span> tail -f /var/log/auth.log | grep sudo
<span class="comment"># Ou sur CentOS/RHEL :</span>
<span class="keyword">sudo</span> tail -f /var/log/secure | grep sudo</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Configuration de journalisation avancée</h3>
                    <pre><code class="language-bash"><span class="comment"># Dans /etc/sudoers, ajouter :</span>
Defaults logfile="/var/log/sudo.log"
Defaults log_input, log_output</code></pre>
                </div>
            </section>

            <!-- Récupération en cas d'erreur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récupération d'urgence</h2>

                <div class="code-example">
                    <h3 class="text-purple">Si sudo est cassé</h3>
                    <pre><code class="language-bash"><span class="comment"># Méthode 1 : Accès root direct</span>
su -
<span class="comment"># (nécessite que le mot de passe root soit activé)</span>

<span class="comment"># Méthode 2 : Mode single user (redémarrage requis)</span>
<span class="comment"># Au démarrage GRUB, appuyer sur 'e' pour éditer</span>
<span class="comment"># Ajouter 'single' à la fin de la ligne linux</span>
<span class="comment"># Ctrl+X pour démarrer</span>

<span class="comment"># Méthode 3 : Live CD/USB</span>
<span class="comment"># Démarrer sur un média live, monter le disque et corriger</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Correction depuis un Live USB</h3>
                    <pre><code class="language-bash"><span class="comment"># Après démarrage sur Live USB :</span>
<span class="keyword">sudo</span> -i
mkdir /mnt/root
mount /dev/sda1 /mnt/root  <span class="comment"># Adapter la partition</span>
chroot /mnt/root

<span class="comment"># Maintenant corriger les fichiers :</span>
visudo
<span class="comment"># OU supprimer un fichier problématique :</span>
rm /etc/sudoers.d/fichier_erroné</code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Attribution basique</h3>
                    <p>Créez un nouvel utilisateur et donnez-lui les droits sudo via le groupe sudo.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-bash"><span class="comment"># Créer l'utilisateur</span>
sudo adduser nouvel_admin

<span class="comment"># Ajouter au groupe sudo</span>
sudo usermod -aG sudo nouvel_admin

<span class="comment"># Vérifier</span>
groups nouvel_admin</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Droits limités</h3>
                    <p>Créez un utilisateur qui ne peut exécuter que les commandes apt (gestion des paquets).</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-bash"><span class="comment"># Créer l'utilisateur</span>
sudo adduser gestionnaire_paquets

<span class="comment"># Créer un fichier sudoers dédié</span>
echo "gestionnaire_paquets ALL=(ALL:ALL) /usr/bin/apt, /usr/bin/apt-get" | sudo tee /etc/sudoers.d/gestionnaire_paquets
sudo chmod 440 /etc/sudoers.d/gestionnaire_paquets</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Audit de sécurité</h3>
                    <p>Listez tous les utilisateurs ayant des droits sudo sur le système et vérifiez leur activité.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-bash"><span class="comment"># Lister les membres du groupe sudo</span>
getent group sudo

<span class="comment"># Vérifier chaque utilisateur</span>
for user in $(getent group sudo | cut -d: -f4 | tr ',' ' '); do
    echo "=== Utilisateur: $user ==="
    sudo -l -U $user
done

<span class="comment"># Vérifier les logs récents</span>
sudo grep sudo /var/log/auth.log | tail -20</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Tableau récapitulatif -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Tableau récapitulatif des méthodes</h2>

                <div class="code-example">
                    <table class="methods-table">
                        <thead>
                            <tr>
                                <th>Méthode</th>
                                <th>Utilisation</th>
                                <th>Complexité</th>
                                <th>Sécurité</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><strong>Groupe sudo</strong></td>
                                <td>Utilisateurs standards</td>
                                <td>⭐</td>
                                <td>⭐⭐⭐⭐</td>
                            </tr>
                            <tr>
                                <td><strong>Fichier sudoers</strong></td>
                                <td>Configurations avancées</td>
                                <td>⭐⭐⭐</td>
                                <td>⭐⭐⭐</td>
                            </tr>
                            <tr>
                                <td><strong>/etc/sudoers.d/</strong></td>
                                <td>Serveurs, automation</td>
                                <td>⭐⭐</td>
                                <td>⭐⭐⭐⭐</td>
                            </tr>
                            <tr>
                                <td><strong>Droits limités</strong></td>
                                <td>Applications spécifiques</td>
                                <td>⭐⭐⭐⭐</td>
                                <td>⭐⭐⭐⭐⭐</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- Ressources supplémentaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Ressources supplémentaires</h2>
                <div class="code-example">
                    <ul>
                        <li><a href="https://man7.org/linux/man-pages/man8/visudo.8.html" class="btn-purple btn-hover"
                                target="_blank">Manuel visudo</a></li>
                        <li><a href="https://man7.org/linux/man-pages/man5/sudoers.5.html" class="btn-purple btn-hover"
                                target="_blank">Manuel sudoers</a></li>
                        <li><a href="/lessons/linux-permissions" class="btn-purple btn-hover">Leçon sur les permissions
                                Linux</a></li>
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

.warning-box p,
.warning-box ul {
    margin-bottom: 0.5rem;
    color: #856404;
}

.warning-box ul {
    margin-left: 1.5rem;
}

/* Tableau des méthodes */
.methods-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
}

.methods-table th,
.methods-table td {
    padding: 12px;
    text-align: left;
    border-bottom: 1px solid #e0d6ff;
}

.methods-table th {
    background-color: #6A3093;
    color: white;
    font-weight: 600;
}

.methods-table tr:hover {
    background-color: #f8f6ff;
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
.keyword {
    color: #c586c0 !important;
}

.variable {
    color: #9cdcfe !important;
}

.string {
    color: #ce9178 !important;
}

.comment {
    color: #6a9955 !important;
}

.function {
    color: #dcdcaa !important;
}

.operator {
    color: #d4d4d4 !important;
}

.constant {
    color: #4fc1ff !important;
}

.number {
    color: #b5cea8 !important;
}

.class-name {
    color: #4ec9b0 !important;
}

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

    .methods-table {
        font-size: 0.8rem;
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

    .methods-table {
        display: block;
        overflow-x: auto;
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