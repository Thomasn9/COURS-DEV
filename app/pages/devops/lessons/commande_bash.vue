<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Commandes Bash - Les Fondamentaux</h1>
                <p class="lesson-meta text-white">
                    Maîtrisez le terminal Linux avec les commandes essentielles
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Bash ?</h2>
                <p class="textExemple">
                    Bash (Bourne-Again SHell) est un shell Unix et un langage de commande.
                    C'est l'interpréteur de commandes par défaut sur la plupart des systèmes Linux et macOS.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Caractéristiques principales :</h3>
                    <ul>
                        <li><strong>Puissant</strong> : Automatisation de tâches complexes</li>
                        <li><strong>Flexible</strong> : Scripting et ligne de commande</li>
                        <li><strong>Universel</strong> : Disponible sur tous les systèmes Unix/Linux</li>
                        <li><strong>Extensible</strong> : Fonctions, alias et personnalisation</li>
                    </ul>
                </div>
            </section>

            <!-- Navigation système de fichiers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Navigation dans le système de fichiers</h2>

                <div class="code-example">
                    <h3 class="text-purple">Commandes de base</h3>
                    <div class="code-block">
                        <pre><code># Afficher le répertoire courant
pwd

# Changer de répertoire
cd /chemin/vers/dossier
cd ..          # Remonter d'un niveau
cd ~           # Aller au répertoire home
cd -           # Revenir au répertoire précédent

# Lister les fichiers
ls
ls -l          # Format détaillé
ls -a          # Afficher les fichiers cachés
ls -la         # Combiné détaillé + cachés
ls -lh         Taille lisible par l'humain

# Afficher le manuel d'une commande
man ls
man cd</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des fichiers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des fichiers et répertoires</h2>

                <div class="code-example">
                    <h3 class="text-purple">Création et suppression</h3>
                    <div class="code-block">
                        <pre><code># Créer des répertoires
mkdir nouveau_dossier
mkdir -p parent/enfant/petit_enfant  # Créer l'arborescence

# Créer des fichiers
touch nouveau_fichier.txt
touch fichier1.txt fichier2.txt fichier3.txt

# Copier des fichiers
cp source.txt destination.txt
cp -r source_dir/ destination_dir/  # Copier récursivement

# Déplacer/renommer des fichiers
mv ancien_nom.txt nouveau_nom.txt
mv fichier.txt /autre/dossier/

# Supprimer des fichiers
rm fichier.txt
rm -r dossier/          # Supprimer récursivement
rm -rf dossier/         # Forcer la suppression

# Lier des fichiers
ln -s /chemin/cible lien_symbolique</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Visualisation et édition</h3>
                    <div class="code-block">
                        <pre><code># Afficher le contenu d'un fichier
cat fichier.txt
less fichier.txt        # Navigation interactive
head -n 10 fichier.txt  # 10 premières lignes
tail -n 10 fichier.txt  # 10 dernières lignes
tail -f logs.txt        # Suivre en temps réel

# Éditer des fichiers
nano fichier.txt
vim fichier.txt
code fichier.txt        # VS Code

# Comparer des fichiers
diff fichier1.txt fichier2.txt
cmp fichier1.txt fichier2.txt</code></pre>
                    </div>
                </div>
            </section>

            <!-- Recherche et filtrage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Recherche et filtrage</h2>

                <div class="code-example">
                    <h3 class="text-purple">Commandes de recherche</h3>
                    <div class="code-block">
                        <pre><code># Rechercher des fichiers
find /home -name "*.txt"
find . -type f -name "*.js" -mtime -7  # Modifiés dernière semaine
find /var/log -size +1G                # Fichiers > 1Go

# Rechercher du texte dans des fichiers
grep "motif" fichier.txt
grep -r "erreur" /var/log/             # Récursif
grep -i "warning" app.log              # Insensible à la casse
grep -v "debug" logs.txt               # Exclure le motif

# Recherche avec expressions régulières
grep "^[A-Z]" fichier.txt              # Lignes commençant par majuscule
grep "[0-9]{3}-[0-9]{4}" contacts.txt  # Numéros de téléphone

# Autres outils de recherche
locate nom_fichier
which node              # Emplacement d'une commande
whereis python</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Filtrage et traitement</h3>
                    <div class="code-block">
                        <pre><code># Trier et filtrer
sort noms.txt
sort -r noms.txt        # Ordre inverse
sort -n nombres.txt     # Numérique
uniq doublons.txt       # Supprimer doublons

# Compter
wc fichier.txt          # Lignes, mots, caractères
wc -l access.log        # Nombre de lignes seulement

# Extraire des colonnes
cut -d',' -f1,3 data.csv  # Colonnes 1 et 3
awk '{print $1}' fichier.txt

# Flux et pipes
cat logs.txt | grep "ERROR" | wc -l
ps aux | grep nginx | awk '{print $2}'</code></pre>
                    </div>
                </div>
            </section>

            <!-- Permissions et propriété -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Permissions et propriété</h2>

                <div class="code-example">
                    <h3 class="text-purple">Gestion des permissions</h3>
                    <div class="code-block">
                        <pre><code># Afficher les permissions
ls -l
stat fichier.txt

# Changer les permissions (notation symbolique)
chmod u+x script.sh      # Ajouter execution pour user
chmod go-w fichier.txt   # Retirer écriture group/other
chmod 755 script.sh      # rwxr-xr-x

# Changer le propriétaire
chown user:group fichier.txt
chown -R www-data:www-data /var/www/  # Récursif

# Changer le groupe
chgrp developers script.sh

# Masque par défaut
umask
umask 0022</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Explications des permissions</h3>
                    <div class="code-block">
                        <pre><code># Lecture des permissions: drwxr-xr-x
# d = directory, - = file
# rwx = user (read, write, execute)
# r-x = group (read, execute)
# r-x = other (read, execute)

# Valeurs numériques:
# 0 = --- (no permission)
# 1 = --x (execute only)
# 2 = -w- (write only)
# 3 = -wx (write + execute)
# 4 = r-- (read only)
# 5 = r-x (read + execute)
# 6 = rw- (read + write)
# 7 = rwx (all permissions)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Processus et système -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des processus et système</h2>

                <div class="code-example">
                    <h3 class="text-purple">Surveillance système</h3>
                    <div class="code-block">
                        <pre><code># Afficher les processus
ps
ps aux                 # Tous les processus
ps -ef | grep nginx    # Filtrer par nom

# Afficher en temps réel
top
htop

# Informations système
uname -a               # Info noyau
free -h                # Mémoire
df -h                  # Espace disque
du -sh dossier/        # Taille dossier

# Historique des commandes
history
history | grep "ssh"   # Rechercher dans l'historique
!42                    # Exécuter la commande #42</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Contrôle des processus</h3>
                    <div class="code-block">
                        <pre><code># Exécuter en arrière-plan
./script.sh &
nohup ./server.sh &    # Ignorer signaux de déconnexion

# Gérer les jobs
jobs                   # Lister les jobs
fg %1                  # Ramener au premier plan
bg %1                  # Remettre en arrière-plan

# Tuer des processus
kill 1234              # Par PID
kill -9 1234           # Forcer la fermeture
pkill firefox          # Par nom
killall nginx

# Planifier des tâches
sleep 10 && echo "Dix secondes écoulées"
at 14:30 -f script.sh  # Exécuter à une heure
crontab -e             # Éditer crontab</code></pre>
                    </div>
                </div>
            </section>

            <!-- Réseau -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Commandes réseau</h2>

                <div class="code-example">
                    <h3 class="text-purple">Diagnostic réseau</h3>
                    <div class="code-block">
                        <pre><code># Test de connectivité
ping google.com
ping -c 4 8.8.8.8      # 4 paquets seulement

# Informations réseau
ifconfig
ip addr show
netstat -tulpn          # Ports ouverts
ss -tulpn               # Version moderne

# Résolution DNS
nslookup google.com
dig google.com
host google.com

# Transfert de fichiers
wget https://example.com/file.zip
curl -O https://example.com/file.txt
scp fichier.txt user@server:/path/</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Connexions et debugging</h3>
                    <div class="code-block">
                        <pre><code># Tester les ports
telnet example.com 80
nc -zv localhost 3306   # Test port MySQL

# Informations détaillées
traceroute google.com
tracepath google.com
mtr google.com          # Combinaison ping+traceroute

# Analyse réseau
tcpdump -i eth0 port 80
tcpdump -i any host 192.168.1.1

# Configuration réseau
route -n                # Table de routage
arp -a                  # Cache ARP</code></pre>
                    </div>
                </div>
            </section>

            <!-- Compression et archives -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Compression et archives</h2>

                <div class="code-example">
                    <h3 class="text-purple">Gestion des archives</h3>
                    <div class="code-block">
                        <pre><code># Fichiers tar
tar -cvf archive.tar dossier/     # Créer
tar -xvf archive.tar              # Extraire
tar -tzf archive.tar.gz           # Lister

# Compression gzip
gzip fichier.txt                  # Compresser
gunzip fichier.txt.gz             # Décompresser
tar -czf archive.tar.gz dossier/  # Tar + gzip

# Compression bzip2
bzip2 fichier.txt
bunzip2 fichier.txt.bz2
tar -cjf archive.tar.bz2 dossier/

# Zip/Unzip
zip archive.zip fichier1.txt fichier2.txt
unzip archive.zip
unzip -l archive.zip              # Lister</code></pre>
                    </div>
                </div>
            </section>

            <!-- Scripting Bash -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Scripting Bash de base</h2>

                <div class="code-example">
                    <h3 class="text-purple">Structures de contrôle</h3>
                    <div class="code-block">
                        <pre><code>#!/bin/bash
# Script exemple

# Variables
NOM="Alice"
AGE=30
echo "Bonjour $NOM, vous avez $AGE ans"

# Conditions
if [ $AGE -ge 18 ]; then
    echo "Majeur"
else
    echo "Mineur"
fi

# Boucles
for i in {1..5}; do
    echo "Itération $i"
done

# Boucle while
COMPTEUR=1
while [ $COMPTEUR -le 3 ]; do
    echo "Compteur: $COMPTEUR"
    ((COMPTEUR++))
done

# Case
case $1 in
    start)
        echo "Démarrage..."
        ;;
    stop)
        echo "Arrêt..."
        ;;
    *)
        echo "Usage: $0 {start|stop}"
        ;;
esac</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Fonctions et paramètres</h3>
                    <div class="code-block">
                        <pre><code>#!/bin/bash

# Fonctions
bonjour() {
    echo "Bonjour $1"
}

bonjour "Pierre"

# Paramètres de script
echo "Nom du script: $0"
echo "Premier paramètre: $1"
echo "Nombre de paramètres: $#"
echo "Tous les paramètres: $@"

# Test de fichiers
if [ -f "/etc/passwd" ]; then
    echo "Fichier existe"
fi

if [ -d "/home" ]; then
    echo "Répertoire existe"
fi

# Opérations arithmétiques
RESULTAT=$((5 + 3))
echo "5 + 3 = $RESULTAT"</code></pre>
                    </div>
                </div>
            </section>

            <!-- Variables d'environnement -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Variables d'environnement</h2>

                <div class="code-example">
                    <h3 class="text-purple">Variables importantes</h3>
                    <div class="code-block">
                        <pre><code># Afficher les variables
env
printenv

# Variables courantes
echo $HOME              # Répertoire home
echo $USER              # Utilisateur courant
echo $PATH              # Chemins des exécutables
echo $PWD               # Répertoire courant
echo $SHELL             # Shell utilisé

# Définir des variables
export MA_VARIABLE="valeur"
export PATH=$PATH:/mon/dossier

# Variables spéciales
echo $$                 # PID du shell
echo $?                 # Code de retour dernière commande
echo $RANDOM            # Nombre aléatoire

# Alias courants
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'</code></pre>
                    </div>
                </div>
            </section>

            <!-- Redirections et pipes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Redirections et pipes</h2>

                <div class="code-example">
                    <h3 class="text-purple">Gestion des flux</h3>
                    <div class="code-block">
                        <pre><code># Redirections standard
ls > fichiers.txt          # Stdout vers fichier
ls >> fichiers.txt         # Append au fichier
grep "erreur" 2> errors.txt  # Stderr vers fichier
grep "motif" &> output.txt # Stdout + stderr

# Pipes
cat fichier.txt | grep "motif" | sort | uniq
ps aux | grep "nginx" | awk '{print $2}'

# Entrée standard
wc -l < fichier.txt
grep "motif" < input.txt

# Combinaisons
commande > output.txt 2>&1          # Tout vers un fichier
commande 2>&1 | tee log.txt         # Vers fichier + stdout

# Here document
cat << EOF
Ceci est un
texte multiligne
EOF

# Here string
grep "motif" <<< "texte avec motif"</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques Bash</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Sécurité</h3>
                        <ul>
                            <li>Toujours citer les variables</li>
                            <li>Utiliser "#!/bin/bash" en shebang</li>
                            <li>Valider les entrées utilisateur</li>
                            <li>Éviter l'utilisation de "eval"</li>
                            <li>Utiliser des chemins absolus pour les scripts critiques</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Productivité</h3>
                        <ul>
                            <li>Utiliser la complétion par tabulation</li>
                            <li>Créer des alias pour les commandes fréquentes</li>
                            <li>Utiliser l'historique efficacement</li>
                            <li>Apprendre les raccourcis clavier</li>
                            <li>Documenter les scripts</li>
                        </ul>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Raccourcis clavier utiles</h3>
                    <div class="code-block">
                        <pre><code>Ctrl + A      # Début de ligne
Ctrl + E      # Fin de ligne
Ctrl + U      # Effacer jusqu'au début
Ctrl + K      # Effacer jusqu'à la fin
Ctrl + W      # Effacer mot précédent
Ctrl + R      # Recherche dans l'historique
Ctrl + L      # Clear screen
Ctrl + C      # Interrompre
Ctrl + D      # EOF / Déconnexion
Ctrl + Z      # Suspendre</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et Ressources</h2>
                <p class="textExemple">
                    Maîtriser les commandes Bash est essentiel pour tout développeur ou administrateur système.
                    Ces fondamentaux vous permettront d'être plus efficace et productif dans votre travail quotidien.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Ressources pour Approfondir</h3>
                    <ul>
                        <li><strong>man pages</strong> : Documentation intégrée</li>
                        <li><strong>tldr.sh</strong> : Exemples pratiques de commandes</li>
                        <li><strong>Bash Guide</strong> : Guide complet en ligne</li>
                        <li><strong>Linux Documentation Project</strong> : Ressources étendues</li>
                        <li><strong>Stack Overflow</strong> : Questions et réponses</li>
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