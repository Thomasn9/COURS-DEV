<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Le Protocole SCP</h1>
                <p class="lesson-meta text-white">
                    Transfert sécurisé de fichiers entre systèmes avec SSH
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que SCP ?</h2>
                <p class="textExemple">
                    SCP (Secure Copy Protocol) est un protocole de transfert de fichiers qui utilise SSH (Secure Shell)
                    pour assurer la sécurité des données pendant le transfert. Il permet de copier des fichiers et des
                    répertoires entre des machines locales et distantes de manière cryptée.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Caractéristiques principales :</h3>
                    <ul>
                        <li><strong>Sécurisé</strong> : Utilise le chiffrement SSH</li>
                        <li><strong>Simple</strong> : Syntaxe de commande intuitive</li>
                        <li><strong>Fiable</strong> : Transfert avec vérification d'intégrité</li>
                        <li><strong>Authentifié</strong> : Utilise les mêmes mécanismes d'authentification que SSH</li>
                    </ul>
                </div>
            </section>

            <!-- Exemples pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples pratiques de commandes SCP</h2>

                <div class="code-example">
                    <h3 class="text-purple">Transfert local vers distant</h3>
                    <div class="code-block">
                        <pre><code># Copier un fichier local vers un serveur distant
scp monfichier.txt utilisateur@serveur.com:/home/utilisateur/

# Copier un répertoire complet (récursif)
scp -r mondossier/ utilisateur@serveur.com:/home/utilisateur/

# Spécifier un port personnalisé (ex: 2222)
scp -P 2222 monfichier.txt utilisateur@serveur.com:/home/utilisateur/

# Utiliser une clé SSH spécifique
scp -i ~/.ssh/ma_cle_privée monfichier.txt utilisateur@serveur.com:/home/</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Transfert distant vers local</h3>
                    <div class="code-block">
                        <pre><code># Copier un fichier du serveur distant vers la machine locale
scp utilisateur@serveur.com:/home/utilisateur/monfichier.txt ./

# Copier un répertoire distant vers le local
scp -r utilisateur@serveur.com:/home/utilisateur/mondossier/ ./

# Copier avec compression activée
scp -C utilisateur@serveur.com:/home/utilisateur/grosfichier.tar.gz ./

# Mode verbeux pour le débogage
scp -v utilisateur@serveur.com:/home/utilisateur/fichier.log ./</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Transfert entre deux machines distantes</h3>
                    <div class="code-block">
                        <pre><code># Copier directement entre deux serveurs
scp utilisateur1@serveur1.com:/fichier/source.txt utilisateur2@serveur2.com:/fichier/destination/

# Avec authentification par clé et port spécifique
scp -i ~/.ssh/ma_cle -P 2222 \
  utilisateur1@serveur1.com:/backup/database.sql \
  utilisateur2@serveur2.com:/backup/archives/</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Exemples avancés</h3>
                    <div class="code-block">
                        <pre><code># Copier en préservant les permissions et timestamps
scp -p monfichier.txt utilisateur@serveur.com:/home/utilisateur/

# Limiter la bande passante (ex: 1000 KB/s)
scp -l 1000 grosfichier.iso utilisateur@serveur.com:/home/

# Utiliser une configuration SSH spécifique
scp -F ~/.ssh/config_alternatif monfichier.txt myserver:/home/

# Copier plusieurs fichiers simultanément
scp fichier1.txt fichier2.txt fichier3.txt utilisateur@serveur.com:/home/</code></pre>
                    </div>
                </div>
            </section>

            <!-- Fonctionnement -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comment fonctionne SCP ?</h2>
                <p class="textExemple">
                    SCP établit une connexion SSH sécurisée entre la machine source et la machine destination.
                    Toutes les données transférées sont chiffrées, protégeant ainsi les informations sensibles
                    contre les interceptions pendant le transit sur le réseau.
                </p>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Avantages</h3>
                        <ul>
                            <li>Chiffrement des données en transit</li>
                            <li>Authentification forte</li>
                            <li>Intégrité des fichiers assurée</li>
                            <li>Compatibilité avec tous les systèmes Unix/Linux</li>
                            <li>Utilisation simple en ligne de commande</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Limitations</h3>
                        <ul>
                            <li>Pas de reprise de transfert interrompu</li>
                            <li>Pas de progression détaillée du transfert</li>
                            <li>Moins performant que rsync pour les gros volumes</li>
                            <li>Pas de synchronisation bidirectionnelle</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Cas d'utilisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas d'utilisation typiques</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Transferts simples</h3>
                        <ul>
                            <li>Copie de fichiers de configuration</li>
                            <li>Transfert de scripts</li>
                            <li>Sauvegarde de petits fichiers</li>
                            <li>Déploiement de mises à jour</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Environnements</h3>
                        <ul>
                            <li>Administration système</li>
                            <li>Déploiement d'applications</li>
                            <li>Transfert entre serveurs</li>
                            <li>Sauvegarde distribuée</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe et paramètres</h2>
                <p class="textExemple">
                    La commande SCP suit une structure simple qui permet de spécifier la source, la destination
                    et diverses options de transfert.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Structure générale</h3>
                    <p>La syntaxe basique suit le modèle : <strong>scp [options] source destination</strong></p>

                    <h3 class="text-purple">Options courantes</h3>
                    <ul>
                        <li><strong>-P port</strong> : Spécifier le port SSH (par défaut 22)</li>
                        <li><strong>-r</strong> : Copier des répertoires récursivement</li>
                        <li><strong>-v</strong> : Mode verbeux pour le débogage</li>
                        <li><strong>-C</strong> : Compression des données pendant le transfert</li>
                        <li><strong>-i</strong> : Spécifier une clé d'identité SSH</li>
                        <li><strong>-p</strong> : Préserver les permissions et timestamps</li>
                        <li><strong>-l</strong> : Limiter la bande passante (en Kbit/s)</li>
                    </ul>
                </div>
            </section>

            <!-- Méthodes d'authentification -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes d'authentification</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Authentification par mot de passe</h3>
                        <p>La méthode la plus simple où l'utilisateur saisit son mot de passe lors de la connexion.
                            Pratique pour les transferts occasionnels mais moins sécurisée que les clés.</p>
                        <div class="code-block">
                            <pre><code># Authentification par mot de passe (saisie interactive)
scp monfichier.txt utilisateur@serveur.com:/home/</code></pre>
                        </div>
                    </div>

                    <div>
                        <h3 class="text-purple">Authentification par clé SSH</h3>
                        <p>Utilise une paire de clés cryptographiques (publique/privée) pour l'authentification.
                            Plus sécurisée et permet l'automatisation des transferts sans intervention manuelle.</p>
                        <div class="code-block">
                            <pre><code># Authentification par clé SSH
scp -i ~/.ssh/id_rsa monfichier.txt utilisateur@serveur.com:/home/</code></pre>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques de sécurité</h2>

                <div class="code-example">
                    <h3 class="text-purple">Recommandations</h3>
                    <ul>
                        <li><strong>Utiliser des clés SSH</strong> plutôt que des mots de passe</li>
                        <li><strong>Changer le port SSH par défaut</strong> pour réduire les attaques automatisées</li>
                        <li><strong>Limiter les permissions</strong> des clés SSH</li>
                        <li><strong>Vérifier les fingerprints</strong> des serveurs distants</li>
                        <li><strong>Utiliser des connexions VPN</strong> pour les transferts sensibles</li>
                    </ul>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Alternatives à considérer</h3>
                    <ul>
                        <li><strong>Rsync over SSH</strong> : Pour les transferts incrémentiels et la synchronisation
                        </li>
                        <li><strong>SFTP</strong> : Pour une interface interactive de gestion de fichiers</li>
                        <li><strong>FTP over TLS</strong> : Pour les transferts nécessitant une interface graphique</li>
                        <li><strong>Git</strong> : Pour le versioning et la collaboration sur le code</li>
                    </ul>
                </div>
            </section>

            <!-- Dépannage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Dépannage courant</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Problèmes fréquents</h3>
                        <ul>
                            <li>Erreurs de permissions sur les fichiers</li>
                            <li>Problèmes d'authentification SSH</li>
                            <li>Port SSH bloqué par le firewall</li>
                            <li>Espaces insuffisants sur le disque</li>
                            <li>Chemins de fichiers incorrects</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Solutions</h3>
                        <ul>
                            <li>Vérifier les permissions avec <strong>chmod</strong></li>
                            <li>Tester la connexion SSH d'abord</li>
                            <li>Utiliser l'option <strong>-v</strong> pour le débogage</li>
                            <li>Vérifier l'espace disque disponible</li>
                            <li>Utiliser des chemins absolus</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Comparaison avec autres protocoles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comparaison avec d'autres protocoles</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">SCP vs FTP</h3>
                        <ul>
                            <li><strong>SCP</strong> : Chiffrement natif, plus sécurisé</li>
                            <li><strong>FTP</strong> : Données en clair, moins sécurisé</li>
                            <li><strong>FTPS</strong> : FTP avec SSL/TLS, bonne alternative</li>
                            <li><strong>SFTP</strong> : SSH File Transfer Protocol, très similaire à SCP</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">SCP vs Rsync</h3>
                        <ul>
                            <li><strong>SCP</strong> : Transfert simple et direct</li>
                            <li><strong>Rsync</strong> : Synchronisation intelligente</li>
                            <li><strong>Rsync</strong> : Transfert incrémentiel plus rapide</li>
                            <li><strong>SCP</strong> : Plus simple pour les transferts uniques</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Conclusion et ressources -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et Ressources</h2>
                <p class="textExemple">
                    SCP reste un outil essentiel pour tout administrateur système ou développeur travaillant
                    avec des serveurs distants. Sa simplicité et sa sécurité en font le choix par défaut pour
                    les transferts de fichiers occasionnels dans des environnements Unix/Linux.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Ressources pour Approfondir</h3>
                    <ul>
                        <li><strong>Documentation officielle</strong> : man scp</li>
                        <li><strong>Tutoriels</strong> : Guide SCP de Linuxize</li>
                        <li><strong>Sécurité</strong> : Bonnes pratiques SSH de Mozilla</li>
                        <li><strong>Outils graphiques</strong> : WinSCP, FileZilla (avec SFTP)</li>
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