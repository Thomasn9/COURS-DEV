<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Installer Java, IntelliJ et démarrer avec Git</h1>
                <p class="lesson-meta text-white">Java • JDK • IntelliJ IDEA • Git • Premier projet</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    Avant d'écrire la moindre ligne de code Java, il faut mettre en place un environnement de
                    développement correct : le <strong>JDK</strong> (Java Development Kit) qui contient le compilateur
                    et la machine virtuelle, un <strong>IDE</strong> (IntelliJ IDEA) pour écrire et exécuter le code
                    confortablement, et <strong>Git</strong> pour versionner le projet dès sa création.
                </p>
                <p class="textExemple">
                    Cette leçon vous guide pas à pas : installation du JDK, installation d'IntelliJ IDEA, création
                    d'un premier projet Java, puis initialisation d'un dépôt Git local relié à un dépôt distant
                    (GitHub).
                </p>
            </section>

            <!-- Architecture / vue d'ensemble -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Vue d'ensemble de la chaîne d'outils</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Les 3 briques de l'environnement</h3>
                    <ul>
                        <li><strong>JDK</strong> : compile le code source (.java) en bytecode (.class) et fournit la JVM pour l'exécuter</li>
                        <li><strong>IntelliJ IDEA</strong> : l'éditeur qui gère le projet, la compilation, l'exécution et le débogage</li>
                        <li><strong>Git</strong> : versionne le code source et permet de le partager (GitHub, GitLab...)</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Vous                 IntelliJ IDEA              JDK / JVM
  │                       │                          │
  │ ── Écrit .java ─────→ │                          │
  │                       │ ── javac (compile) ────→ │
  │                       │ ←── .class (bytecode) ── │
  │                       │ ── java (exécute) ─────→ │
  │ ←── Résultat console ─│ ←── Sortie programme ──── │
  │                       │                          │
  │                       │                          │
Git (local)          Dépôt distant (GitHub)
  │                       │
  │ ── git add/commit ──→ │ (historique local)
  │ ── git push ─────────────────────────────────→   │</code></pre>
                    </div>
                </div>
            </section>

            <!-- Installation du JDK -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation du JDK (Java Development Kit)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Qu'est-ce que le JDK exactement ?</h3>
                    <p>
                        Le <strong>JDK (Java Development Kit)</strong> est la boîte à outils complète du développeur
                        Java. Il contient trois éléments indispensables :
                    </p>
                    <ul>
                        <li><strong><code>javac</code></strong> : le compilateur, qui transforme votre code source lisible (<code>.java</code>) en bytecode (<code>.class</code>) compréhensible par la machine</li>
                        <li><strong>la JVM (Java Virtual Machine)</strong> : le programme qui exécute réellement ce bytecode, quel que soit le système d'exploitation (« write once, run anywhere »)</li>
                        <li><strong>des outils annexes</strong> : débogueur, générateur de documentation (<code>javadoc</code>), archiveur (<code>jar</code>), etc.</li>
                    </ul>
                    <p>
                        Sans le JDK, impossible de compiler du code Java soi-même : c'est le premier outil à installer.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">⚠️ JDK ou JRE : lequel choisir ?</h3>
                    <div class="warning-section">
                        <h4 class="text-purple">Prenez toujours le JDK, jamais le JRE</h4>
                        <p class="warning-text">
                            Le <strong>JRE (Java Runtime Environment)</strong> permet uniquement d'<em>exécuter</em>
                            un programme Java déjà compilé (c'est ce qu'installe un simple utilisateur pour faire
                            tourner une application Java). Il ne contient pas <code>javac</code>, donc il est
                            impossible de compiler ou de développer avec.
                        </p>
                        <p class="warning-text">
                            Le <strong>JDK</strong> inclut le JRE <em>et</em> le compilateur : c'est celui-là qu'il
                            faut télécharger pour développer. Sur la page de téléchargement (Adoptium, Oracle...),
                            il y a toujours deux boutons ou onglets « JDK » et « JRE » côte à côte : cliquez sur
                            <strong>JDK</strong>.
                        </p>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Choisir une distribution</h3>
                    <p>
                        Java est un standard ouvert : plusieurs éditeurs proposent des distributions gratuites et
                        équivalentes du JDK, toutes basées sur le même code source ouvert (OpenJDK). Les plus
                        utilisées sont <strong>Eclipse Temurin (Adoptium)</strong>, <strong>Oracle JDK</strong>
                        et <strong>OpenJDK</strong>. Cette leçon utilise <strong>Adoptium / Temurin</strong>
                        (<code>adoptium.net</code>), une distribution gratuite maintenue par la fondation Eclipse,
                        très largement utilisée en entreprise.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Lire la page de téléchargement Adoptium</h3>
                    <p>
                        La page <code>adoptium.net</code> affiche une carte par système d'exploitation (Linux,
                        Windows, macOS), et pour chacune plusieurs choix à faire :
                    </p>
                    <ul>
                        <li><strong>JDK / JRE</strong> : toujours cliquer sur <strong>JDK</strong> (voir encadré ci-dessus)</li>
                        <li><strong>L'architecture du processeur</strong> : <code>x64</code> pour un processeur Intel/AMD classique, <code>aarch64</code> (« ARM64 ») pour un Mac Apple Silicon (M1/M2/M3/M4) ou un ordinateur ARM</li>
                        <li><strong>Le format de fichier</strong> : change uniquement la façon dont l'installation se déroule, pas le contenu du JDK</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Format    Système        Comportement
──────────────────────────────────────────────────────────
.msi      Windows        Installeur graphique classique (recommandé)
.zip      Windows/Linux  Archive à décompresser soi-même, sans installeur
.pkg      macOS          Installeur graphique classique (recommandé)
.tar.gz   macOS/Linux    Archive à décompresser soi-même, sans installeur</code></pre>
                    </div>
                    <p>
                        <strong>En résumé, pour un usage normal :</strong>
                    </p>
                    <ul>
                        <li>Windows → bouton <strong>JDK</strong>, format <strong>.msi</strong> (x64 dans la grande majorité des cas)</li>
                        <li>macOS → bouton <strong>JDK</strong>, format <strong>.pkg</strong> (aarch64 sur Mac M1/M2/M3/M4, x64 sur Mac Intel)</li>
                        <li>Linux → bouton <strong>JDK</strong>, format <strong>.tar.gz</strong> — ou, plus simple, passer par le gestionnaire de paquets de votre distribution (voir plus bas)</li>
                    </ul>
                    <p>
                        Les petites icônes à côté de chaque lien (bouclier, empreinte digitale...) donnent accès aux
                        sommes de contrôle et signatures : elles servent à vérifier que le fichier téléchargé n'a
                        pas été corrompu, elles ne sont pas nécessaires pour une installation classique.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Installation sur Windows</h3>
                    <ol>
                        <li>Sur <code>adoptium.net</code>, sélectionner l'onglet <strong>JDK</strong> puis télécharger le fichier <code>.msi</code> (colonne Windows)</li>
                        <li>Double-cliquer sur le fichier téléchargé pour lancer l'installeur</li>
                        <li>Lors de l'étape « Custom Setup », cocher l'option <strong>« Set JAVA_HOME variable »</strong> pour que le système sache où trouver le JDK</li>
                        <li>Cocher également <strong>« Add to PATH »</strong> pour utiliser <code>java</code> depuis n'importe quel terminal</li>
                        <li>Terminer l'installation puis ouvrir un <strong>nouveau</strong> terminal (PowerShell)</li>
                    </ol>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Vérifier la variable d'environnement (PowerShell)
echo $env:JAVA_HOME

# Vérifier l'installation
java -version
javac -version</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Installation sur macOS</h3>
                    <p>
                        Sur Mac, il est plus simple d'installer le JDK via <strong>Homebrew</strong> (gestionnaire
                        de paquets) plutôt que de télécharger manuellement le <code>.pkg</code> depuis Adoptium ;
                        les mises à jour sont ensuite automatisées.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Avec Homebrew (recommandé)
brew install --cask temurin

# Vérifier l'installation
java -version
javac -version

# Vérifier la variable JAVA_HOME
/usr/libexec/java_home -V</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Installation sur Linux (Debian / Ubuntu)</h3>
                    <p>
                        Sur Linux, plutôt que de télécharger l'archive <code>.tar.gz</code> à la main, on utilise
                        généralement le gestionnaire de paquets du système, plus simple à maintenir à jour.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Mettre à jour les paquets
sudo apt update

# Installer le JDK (OpenJDK 21)
sudo apt install openjdk-21-jdk

# Vérifier l'installation
java -version
javac -version

# Localiser l'installation pour JAVA_HOME
update-alternatives --list java</code></pre>
                    </div>
                </div>
            </section>

            <!-- Installation d'IntelliJ -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation d'IntelliJ IDEA</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Qu'est-ce qu'IntelliJ IDEA exactement ?</h3>
                    <p>
                        Le JDK, installé précédemment, sait compiler et exécuter du Java, mais uniquement en ligne
                        de commande (<code>javac</code> puis <code>java</code>). <strong>IntelliJ IDEA</strong> est
                        un <strong>IDE</strong> (Integrated Development Environment, « environnement de
                        développement intégré ») : un logiciel qui rassemble en une seule interface tout ce dont
                        on a besoin au quotidien pour développer, à savoir :
                    </p>
                    <ul>
                        <li><strong>un éditeur de code intelligent</strong> : coloration syntaxique, autocomplétion, détection d'erreurs en temps réel</li>
                        <li><strong>la gestion du projet</strong> : organisation des fichiers, des dépendances, du SDK utilisé</li>
                        <li><strong>la compilation et l'exécution</strong> : IntelliJ appelle <code>javac</code> puis <code>java</code> à votre place, en un clic ou un raccourci clavier</li>
                        <li><strong>le débogage</strong> : possibilité de mettre le programme en pause (points d'arrêt) pour inspecter les variables pendant l'exécution</li>
                        <li><strong>l'intégration Git</strong> : commit, push, historique, sans quitter l'éditeur</li>
                    </ul>
                    <p>
                        En résumé : le JDK est le moteur, IntelliJ IDEA est le tableau de bord qui pilote ce moteur
                        confortablement.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Community vs Ultimate</h3>
                    <ul>
                        <li><strong>Community Edition</strong> : gratuite et open source, largement suffisante pour du Java « pur » et l'apprentissage</li>
                        <li><strong>Ultimate Edition</strong> : payante (gratuite pour les étudiants), ajoute le support Spring, JavaEE, bases de données, frameworks web...</li>
                    </ul>
                    <p>Pour cette leçon, la <strong>Community Edition</strong> est amplement suffisante.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Procédure d'installation</h3>
                    <ol>
                        <li>Se rendre sur <code>jetbrains.com/idea/download</code></li>
                        <li>Télécharger la version Community correspondant à votre OS (Windows / macOS / Linux)</li>
                        <li>Lancer l'installeur et suivre les étapes par défaut</li>
                        <li>Sur l'écran « Installation Options », cocher les cases recommandées (voir détail ci-dessous)</li>
                        <li>Au premier lancement, choisir le thème (Light/Dark) puis ignorer ou installer les plugins additionnels</li>
                    </ol>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Alternative multiplateforme : installer via JetBrains Toolbox
# (gère les mises à jour et versions multiples des IDE JetBrains)
# Télécharger depuis jetbrains.com/toolbox-app puis installer
# "IntelliJ IDEA Community" depuis l'application Toolbox</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">L'écran « Installation Options » (Windows)</h3>
                    <p>
                        Pendant l'installation sur Windows, une fenêtre « Configure your IntelliJ IDEA installation »
                        propose plusieurs cases à cocher, réparties en 4 groupes. Voici ce que fait chacune et ce
                        qu'il est recommandé de cocher pour cette leçon :
                    </p>
                    <ul>
                        <li>
                            <strong>Create Desktop Shortcut → ☑ IntelliJ IDEA</strong><br>
                            Crée un raccourci sur le bureau pour lancer l'IDE rapidement. À cocher pour votre confort, sans impact technique.
                        </li>
                        <li>
                            <strong>Update PATH Variable → ☑ Add "bin" folder to the PATH</strong><br>
                            Ajoute IntelliJ à la variable d'environnement PATH, ce qui permet de lancer l'IDE depuis
                            un terminal avec la commande <code>idea</code> (utile mais optionnel). Un redémarrage
                            de la session Windows est nécessaire pour que le changement soit pris en compte.
                        </li>
                        <li>
                            <strong>Update Context Menu → ☑ Add "Open Folder as Project"</strong><br>
                            Ajoute une entrée dans le clic droit de l'explorateur Windows pour ouvrir directement
                            n'importe quel dossier comme projet IntelliJ. Très pratique, à cocher.
                        </li>
                        <li>
                            <strong>Create Associations → ☑ .java</strong> (et éventuellement <strong>.gradle</strong>, <strong>.pom</strong> si vous les utilisez plus tard)<br>
                            Fait en sorte qu'un double-clic sur un fichier <code>.java</code> dans l'explorateur
                            Windows l'ouvre automatiquement avec IntelliJ. Cocher au minimum <code>.java</code>.
                            Les cases <code>.groovy</code>, <code>.kt</code>, <code>.kts</code> concernent d'autres
                            langages (Groovy, Kotlin) : elles ne sont pas nécessaires pour cette leçon, laissez-les décochées.
                        </li>
                    </ul>
                    <p>
                        Aucune de ces options n'est bloquante : elles ajoutent simplement des raccourcis de confort.
                        En cas de doute, cocher <strong>Create Desktop Shortcut</strong>, <strong>Add "bin" folder to the PATH</strong>,
                        <strong>Add "Open Folder as Project"</strong> et <strong>.java</strong> couvre les besoins
                        d'un débutant. Cliquer ensuite sur <strong>Next &gt;</strong> pour continuer l'installation.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Vérifier que le JDK est reconnu par IntelliJ</h3>
                    <p>
                        À la création d'un projet, IntelliJ propose de sélectionner un SDK. S'il détecte
                        automatiquement le JDK installé, il apparaît dans la liste déroulante. Sinon, il faut
                        l'ajouter manuellement via le chemin d'installation.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">File → Project Structure → Project → SDK
  → Add SDK → Download JDK (ou Add JDK si déjà installé)
  → Sélectionner le dossier d'installation du JDK
  → Choisir la version (21 recommandé)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Créer le premier projet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer un premier projet Java</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Nouveau projet dans IntelliJ</h3>
                    <ol>
                        <li>Sur l'écran d'accueil, cliquer sur <strong>New Project</strong></li>
                        <li>Choisir <strong>Java</strong> dans la liste des types de projet</li>
                        <li>Nommer le projet, par exemple <code>mon-premier-projet-java</code></li>
                        <li>Sélectionner le SDK installé précédemment</li>
                        <li>Cocher « Add sample code » pour générer un fichier <code>Main.java</code> de démonstration</li>
                        <li>Cliquer sur <strong>Create</strong></li>
                    </ol>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Structure générée</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">mon-premier-projet-java/
├── .idea/              # Fichiers de configuration IntelliJ (à ignorer dans Git)
├── out/                # Fichiers compilés (à ignorer dans Git)
├── src/
│   └── Main.java       # Point d'entrée du programme
└── mon-premier-projet-java.iml</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Le fichier Main.java</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Main {

    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }

}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exécuter le programme</h3>
                    <p>
                        Cliquer sur la flèche verte à côté de la méthode <code>main</code>, ou utiliser le
                        raccourci <code>Shift + F10</code> (Windows/Linux) ou <code>Ctrl + R</code> (macOS).
                        La sortie s'affiche dans la console en bas de l'IDE.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">"C:\...\java.exe" ... Main
Hello, world!

Process finished with exit code 0</code></pre>
                    </div>
                </div>
            </section>

            <!-- Créer le dépôt Git -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer un dépôt Git pour le projet</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Vérifier que Git est installé</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">git --version

# Si Git n'est pas installé :
# Windows : télécharger sur git-scm.com
# macOS   : brew install git
# Linux   : sudo apt install git</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Initialiser le dépôt en ligne de commande</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Se placer à la racine du projet
cd mon-premier-projet-java

# Initialiser le dépôt Git local
git init

# Configurer son identité (une seule fois par machine)
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer un fichier .gitignore adapté à Java/IntelliJ</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext"># .gitignore

# Dossiers de compilation
out/
target/
build/
*.class

# Fichiers IntelliJ IDEA
.idea/
*.iml
*.iws
*.ipr

# Fichiers système
.DS_Store
Thumbs.db</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Premier commit</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Ajouter tous les fichiers suivis (hors .gitignore)
git add .

# Vérifier ce qui va être commité
git status

# Créer le premier commit
git commit -m "Initial commit: structure du projet Java"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Relier le dépôt local à GitHub</h3>
                    <ol>
                        <li>Créer un nouveau dépôt vide sur GitHub (sans README ni .gitignore pour éviter les conflits)</li>
                        <li>Copier l'URL du dépôt distant (HTTPS ou SSH)</li>
                        <li>Lier puis pousser le dépôt local</li>
                    </ol>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Ajouter le dépôt distant
git remote add origin https://github.com/votre-utilisateur/mon-premier-projet-java.git

# Renommer la branche principale si besoin
git branch -M main

# Pousser le code vers GitHub
git push -u origin main</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser Git directement depuis IntelliJ</h3>
                    <p>
                        IntelliJ intègre nativement Git : pas besoin de sortir du terminal pour les opérations
                        courantes.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">VCS → Enable Version Control Integration → Git
  → Clic droit sur le projet → Git → Add
  → Commit (Ctrl+K)
  → Push (Ctrl+Shift+K)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Environnement de développement</h3>
                    <ul>
                        <li><strong>Toujours utiliser une version LTS</strong> du JDK (17 ou 21) pour la stabilité</li>
                        <li><strong>Configurer JAVA_HOME</strong> correctement pour éviter les conflits d'outils en ligne de commande</li>
                        <li><strong>Ne jamais versionner</strong> les dossiers <code>.idea/</code>, <code>out/</code> ou <code>target/</code></li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Git et versionning</h3>
                    <ul>
                        <li>Créer le <code>.gitignore</code> <strong>avant</strong> le premier commit</li>
                        <li>Faire des commits petits et fréquents avec des messages clairs</li>
                        <li>Ne jamais commiter de mots de passe ou clés API dans le code source</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Vous disposez maintenant d'un environnement complet : le JDK pour compiler et exécuter
                        Java, IntelliJ IDEA pour développer confortablement, et un dépôt Git prêt à accueillir
                        l'historique du projet.
                    </p>
                    <p>
                        Dans la prochaine leçon, nous découvrirons la syntaxe de base du langage Java : variables,
                        types primitifs, structures conditionnelles et boucles.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaInstallationLesson',

    mounted() {
        // Charger highlight.js + thème VS Code Dark via CDN
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel  = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    // Charger le langage Java en plus
                    const javaScript = document.createElement('script');
                    javaScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/java.min.js';
                    javaScript.onload = resolve;
                    document.head.appendChild(javaScript);
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            // Appliquer la coloration sur tous les blocs de code
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
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

.border-purple {
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.text-purple { color: #6A3093 !important; }
.text-white  { color: white !important; }

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

.success-text {
    color: #00b894;
    font-weight: bold;
    margin-top: 0.5rem;
}

.exercise { margin: 2rem 0; }
.solution { margin: 1rem 0; }

.solution-content {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #8B5FBF;
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
    .code-comparison   { grid-template-columns: 1fr; gap: 1rem; }
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