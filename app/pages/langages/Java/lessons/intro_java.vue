<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Installation de Java et IntelliJ IDEA</h1>
                <p class="lesson-meta text-white">Guide complet pour configurer votre environnement de développement Java</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction au développement Java</h2>
                <p class="textExemple">
                    Java est l'un des langages de programmation les plus populaires et puissants au monde. 
                    Pour commencer à développer en Java, vous avez besoin de deux composants essentiels :
                </p>
                <ol class="textExemple">
                    <li><strong>Java Development Kit (JDK)</strong> : L'environnement d'exécution et les outils de développement</li>
                    <li><strong>IntelliJ IDEA</strong> : Un IDE puissant et intuitif pour développer en Java</li>
                </ol>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Environnement de développement Java complet</span>
JDK (Java Development Kit) → IntelliJ IDEA (IDE) → Applications Java</code></pre>
                </div>
            </div>

            <!-- Section 1 : Installation du JDK -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Section 1 : Installation du JDK</h2>
                <p class="textExemple">
                    Le JDK contient tout ce dont vous avez besoin pour compiler, déboguer et exécuter des applications Java.
                    Nous recommandons d'installer la version LTS (Long Term Support) pour une stabilité optimale.
                </p>

                <h3 class="text-purple">1.1 Choisir la bonne version</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Versions JDK recommandées</span>
- <span class="bash-keyword">Java 21 LTS</span> : Version stable avec support long terme (recommandée)
- <span class="bash-keyword">Java 17 LTS</span> : Version LTS précédente, encore très utilisée
- <span class="bash-keyword">Java 11 LTS</span> : Ancienne version LTS, encore en support</code></pre>
                </div>

                <p class="textExemple">
                    <strong>Conseil :</strong> Installez Java 21 LTS pour bénéficier des dernières fonctionnalités et du support à long terme.
                </p>
            </div>

            <!-- Installation JDK sur Windows -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">2. Installation du JDK sur Windows</h2>
                
                <h3 class="text-purple">2.1 Téléchargement</h3>
                <p class="textExemple">
                    Rendez-vous sur le site officiel d'Oracle ou d'Adoptium pour télécharger le JDK :
                </p>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Oracle JDK (gratuit pour usage personnel)</h4>
                        <pre v-pre><code class="language-text">https://www.oracle.com/java/technologies/downloads/</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Eclipse Adoptium (open source)</h4>
                        <pre v-pre><code class="language-text">https://adoptium.net/</code></pre>
                    </div>
                </div>

                <h3 class="text-purple">2.2 Processus d'installation</h3>
                <div class="code-example">
                    <h4 class="text-purple">Etapes d'installation sur Windows</h4>
                    <pre v-pre><code class="language-text">1. Executez le fichier .exe téléchargé
2. Suivez l'assistant d'installation
3. Acceptez les conditions d'utilisation
4. Choisissez le dossier d'installation (par défaut recommandé)
5. Laissez l'installateur configurer les variables d'environnement
6. Attendez la fin de l'installation</code></pre>
                </div>

                <h3 class="text-purple">2.3 Vérification de l'installation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-cmd"><span class="bash-comment"># Ouvrez l'invite de commandes (CMD) ou PowerShell</span>
C:\Users\VotreNom&gt; <span class="bash-command">java --version</span>

<span class="bash-comment"># Résultat attendu :</span>
java version "21.0.1" 2023-10-17 LTS
Java(TM) SE Runtime Environment (build 21.0.1+12-LTS-29)
Java HotSpot(TM) 64-Bit Server VM (build 21.0.1+12-LTS-29, mixed mode, sharing)</code></pre>
                </div>

                <h3 class="text-purple">2.4 Configuration des variables d'environnement (si nécessaire)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">1. Clique droit sur "Ce PC" → Propriétés
2. Paramètres système avancés → Variables d'environnement
3. Sous "Variables système", sélectionnez "Path" → Modifier
4. Ajoutez le chemin du dossier "bin" de votre JDK :
   C:\Program Files\Java\jdk-21\bin
5. Ajoutez une nouvelle variable JAVA_HOME :
   Nom : JAVA_HOME
   Valeur : C:\Program Files\Java\jdk-21</code></pre>
                </div>
            </div>

            <!-- Installation JDK sur macOS -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">3. Installation du JDK sur macOS</h2>

                <h3 class="text-purple">3.1 Méthode recommandée : Homebrew</h3>
                <p class="textExemple">
                    Si vous avez Homebrew installé, c'est la méthode la plus simple :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Installation avec Homebrew</span>
<span class="bash-prompt">$</span> <span class="bash-command">brew update</span>
<span class="bash-prompt">$</span> <span class="bash-command">brew install openjdk@21</span>

<span class="bash-comment"># Lien symbolique pour que java soit accessible</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo ln -sfn /opt/homebrew/opt/openjdk@21/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-21.jdk</span></code></pre>
                </div>

                <h3 class="text-purple">3.2 Méthode manuelle</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">1. Téléchargez le JDK depuis adoptium.net
2. Ouvrez le fichier .pkg téléchargé
3. Suivez l'assistant d'installation
4. Vérifiez l'installation dans le terminal</code></pre>
                </div>

                <h3 class="text-purple">3.3 Vérification sur macOS</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">java --version</span>

<span class="bash-comment"># Résultat attendu :</span>
openjdk 21.0.1 2023-10-17 LTS
OpenJDK Runtime Environment Temurin-21.0.1+12 (build 21.0.1+12-LTS)
OpenJDK 64-Bit Server VM Temurin-21.0.1+12 (build 21.0.1+12-LTS, mixed mode)</code></pre>
                </div>

                <h3 class="text-purple">3.4 Configuration de JAVA_HOME sur macOS</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Ajouter à ~/.zshrc ou ~/.bash_profile</span>
<span class="bash-prompt">$</span> <span class="bash-command">nano ~/.zshrc</span>

<span class="bash-comment"># Ajoutez ces lignes :</span>
export JAVA_HOME=$(/usr/libexec/java_home -v 21)
export PATH="$JAVA_HOME/bin:$PATH"

<span class="bash-comment"># Appliquez les changements</span>
<span class="bash-prompt">$</span> <span class="bash-command">source ~/.zshrc</span></code></pre>
                </div>
            </div>

            <!-- Installation JDK sur Linux -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">4. Installation du JDK sur Linux</h2>

                <h3 class="text-purple">4.1 Ubuntu/Debian (APT)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Mise à jour des paquets</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo apt update && sudo apt upgrade -y</span>

<span class="bash-comment"># Installation d'OpenJDK 21</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo apt install openjdk-21-jdk -y</span>

<span class="bash-comment"># Installation des outils de développement supplémentaires</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo apt install maven gradle -y</span></code></pre>
                </div>

                <h3 class="text-purple">4.2 Fedora/RHEL (DNF/YUM)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Fedora</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo dnf install java-21-openjdk-devel</span>

<span class="bash-comment"># RHEL/CentOS</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo yum install java-21-openjdk-devel</span></code></pre>
                </div>

                <h3 class="text-purple">4.3 Vérification sur Linux</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">java --version</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac --version</span>  <span class="bash-comment"># Vérifie le compilateur</span>

<span class="bash-comment"># Configuration de JAVA_HOME</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo "export JAVA_HOME=/usr/lib/jvm/java-21-openjdk" >> ~/.bashrc</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo "export PATH=\$JAVA_HOME/bin:\$PATH" >> ~/.bashrc</span>
<span class="bash-prompt">$</span> <span class="bash-command">source ~/.bashrc</span></code></pre>
                </div>
            </div>

            <!-- Vérification complète de l'installation JDK -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">5. Vérification complète de l'installation JDK</h2>
                
                <div class="code-example">
                    <h4 class="text-purple">Test complet sur tous les systèmes</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># 1. Vérification de la version Java</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --version</span>

<span class="bash-comment"># 2. Vérification du compilateur</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac --version</span>

<span class="bash-comment"># 3. Vérification de JAVA_HOME</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo $JAVA_HOME</span>        <span class="bash-comment"># Linux/macOS</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo %JAVA_HOME%</span>       <span class="bash-comment"># Windows (CMD)</span>
<span class="bash-prompt">$</span> <span class="bash-command">$env:JAVA_HOME</span>        <span class="bash-comment"># Windows (PowerShell)</span>

<span class="bash-comment"># 4. Création et compilation d'un premier programme</span>
<span class="bash-prompt">$</span> <span class="bash-command">cat &gt; HelloWorld.java &lt;&lt; 'EOF'</span>
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
EOF

<span class="bash-prompt">$</span> <span class="bash-command">javac HelloWorld.java</span>   <span class="bash-comment"># Compilation</span>
<span class="bash-prompt">$</span> <span class="bash-command">java HelloWorld</span>         <span class="bash-comment"># Execution</span>

<span class="bash-comment"># Résultat attendu : Hello, World!</span></code></pre>
                </div>
            </div>

            <!-- Section 2 : Installation d'IntelliJ IDEA -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Section 2 : Installation d'IntelliJ IDEA</h2>
                <p class="textExemple">
                    IntelliJ IDEA est l'IDE le plus populaire pour le développement Java, développé par JetBrains.
                    Il existe deux versions :
                </p>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">IntelliJ IDEA Community</h4>
                        <pre v-pre><code class="language-text">• Gratuite et open source
• Supporte Java, Kotlin, Groovy
• Ideale pour les débutants et étudiants
• Fonctionnalités de base complètes</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">IntelliJ IDEA Ultimate</h4>
                        <pre v-pre><code class="language-text">• Version payante (gratuite pour étudiants)
• Support avancé pour Java EE, Spring
• Base de données, outils web
• Framework JavaScript, Python
• Gratuit avec licence étudiante</code></pre>
                    </div>
                </div>
            </div>

            <!-- Installation d'IntelliJ sur Windows -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">6. Installation d'IntelliJ IDEA sur Windows</h2>

                <h3 class="text-purple">6.1 Téléchargement</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Site officiel : https://www.jetbrains.com/idea/download/

Choisissez :
• Community (gratuit) - Recommandé pour débuter
• Ultimate (payant) - Si vous êtes étudiant, utilisez votre mail académique</code></pre>
                </div>

                <h3 class="text-purple">6.2 Processus d'installation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Etapes d'installation :

1. Executez le fichier .exe téléchargé
2. Choisissez le dossier d'installation
3. Cochez les options suivantes :
   ✓ Créer une icône sur le bureau
   ✓ Associer les fichiers .java
   ✓ Ajouter au PATH (recommandé)
4. Choisissez le thème (Dark/Light)
5. Installez les plugins recommandés</code></pre>
                </div>

                <h3 class="text-purple">6.3 Configuration initiale</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Premier lancement :
1. Acceptez les termes d'utilisation
2. Partagez ou non les données d'utilisation
3. Choisissez le thème UI (Darcula recommandé)
4. Selectionnez les plugins (Java, Kotlin par défaut)
5. Détection automatique du JDK installé
6. Créez un nouveau projet pour tester</code></pre>
                </div>
            </div>

            <!-- Installation d'IntelliJ sur macOS -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">7. Installation d'IntelliJ IDEA sur macOS</h2>

                <h3 class="text-purple">7.1 Méthode 1 : Téléchargement direct</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Télécharger depuis le site JetBrains</span>
https://www.jetbrains.com/idea/download/

<span class="bash-comment"># Extraire et installer</span>
1. Ouvrez le fichier .dmg téléchargé
2. Glissez IntelliJ IDEA dans le dossier Applications
3. Lancez depuis Launchpad ou Applications</code></pre>
                </div>

                <h3 class="text-purple">7.2 Méthode 2 : Homebrew (recommandée)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Installation via Homebrew</span>
<span class="bash-prompt">$</span> <span class="bash-command">brew install --cask intellij-idea-ce</span>  <span class="bash-comment"># Community Edition</span>
<span class="bash-comment"># OU</span>
<span class="bash-prompt">$</span> <span class="bash-command">brew install --cask intellij-idea</span>      <span class="bash-comment"># Ultimate Edition</span></code></pre>
                </div>

                <h3 class="text-purple">7.3 Configuration sur macOS</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Pour ajouter IntelliJ au PATH</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo 'export PATH="/Applications/IntelliJ IDEA.app/Contents/MacOS:$PATH"' >> ~/.zshrc</span>
<span class="bash-prompt">$</span> <span class="bash-command">source ~/.zshrc</span>

<span class="bash-comment"># Vérification</span>
<span class="bash-prompt">$</span> <span class="bash-command">idea</span>  <span class="bash-comment"># Doit lancer IntelliJ IDEA</span></code></pre>
                </div>
            </div>

            <!-- Installation d'IntelliJ sur Linux -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">8. Installation d'IntelliJ IDEA sur Linux</h2>

                <h3 class="text-purple">8.1 Installation via Snap (Ubuntu)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Installation la plus simple</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo snap install intellij-idea-community --classic</span>
<span class="bash-comment"># OU pour la version Ultimate</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo snap install intellij-idea-ultimate --classic</span></code></pre>
                </div>

                <h3 class="text-purple">8.2 Installation manuelle</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Téléchargement et extraction</span>
<span class="bash-prompt">$</span> <span class="bash-command">wget https://download.jetbrains.com/idea/ideaIC-2023.3.tar.gz</span>
<span class="bash-prompt">$</span> <span class="bash-command">tar -xzf ideaIC-2023.3.tar.gz -C /opt/</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo mv /opt/idea-IC-* /opt/intellij</span>

<span class="bash-comment"># Création du lanceur</span>
<span class="bash-prompt">$</span> <span class="bash-command">sudo nano /usr/share/applications/intellij.desktop</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Contenu du fichier .desktop</h4>
                    <pre v-pre><code class="language-ini">[Desktop Entry]
Name=IntelliJ IDEA
Comment=Java IDE
Exec=/opt/intellij/bin/idea.sh
Icon=/opt/intellij/bin/idea.png
Terminal=false
Type=Application
Categories=Development;IDE;</code></pre>
                </div>
            </div>

            <!-- Configuration d'IntelliJ IDEA -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">9. Configuration d'IntelliJ IDEA</h2>

                <h3 class="text-purple">9.1 Premier lancement et configuration</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Etapes de configuration initiale :

1. Import des paramètres : "Do not import settings" (si première installation)
2. Choix du thème : Darcula (sombre) ou Light
3. Plugins recommandés :
   ✓ Java
   ✓ Kotlin
   ✓ Version Control (Git)
   ✓ Terminal
4. Configuration du JDK (détecté automatiquement)
5. Création d'un compte JetBrains (optionnel mais utile)</code></pre>
                </div>

                <h3 class="text-purple">9.2 Configuration du JDK dans IntelliJ</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Pour vérifier/ajouter un JDK :

1. File → Project Structure → Project
2. Dans "Project SDK", cliquez sur "New..."
3. Selectionnez "JDK"
4. Naviguez vers le dossier d'installation de votre JDK
   • Windows : C:\Program Files\Java\jdk-21
   • macOS : /Library/Java/JavaVirtualMachines/jdk-21.jdk
   • Linux : /usr/lib/jvm/java-21-openjdk
5. Cliquez sur OK</code></pre>
                </div>

                <h3 class="text-purple">9.3 Paramètres recommandés</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Paramètres optimaux (File → Settings) :

Editor → Font :
• Font : JetBrains Mono, Size: 14
• Line spacing: 1.2

Editor → Color Scheme → Java :
• Activer "Semantic highlighting"

Build, Execution, Deployment → Build Tools :
• Maven/Gradle : Auto-import activé

Tools → Terminal :
• Shell path : /bin/bash (Linux) ou PowerShell (Windows)

Appearance & Behavior → System Settings :
• Synchronization : Désactivé (améliore les performances)</code></pre>
                </div>
            </div>

            <!-- Création du premier projet -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">10. Création de votre premier projet Java</h2>

                <h3 class="text-purple">10.1 Nouveau projet</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">1. Welcome Screen → "New Project"
2. Selectionnez "Java"
3. Choisissez le JDK 21
4. Ne cochez pas "Create project from template"
5. Nommez votre projet : "HelloWorld"
6. Choisissez l'emplacement
7. Cliquez sur "Create"</code></pre>
                </div>

                <h3 class="text-purple">10.2 Structure du projet</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Structure automatiquement créée :
HelloWorld/
├── .idea/           (dossier de configuration IntelliJ)
├── src/             (dossier source)
└── HelloWorld.iml   (fichier de module)</code></pre>
                </div>

                <h3 class="text-purple">10.3 Création de votre première classe</h3>
                <div class="code-example">
                    <h4 class="text-purple">Etapes dans IntelliJ :</h4>
                    <pre v-pre><code class="language-text">1. Clique droit sur le dossier "src"
2. New → Java Class
3. Nom : "Main"
4. Tapez le code suivant :</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Code Main.java</h4>
                    <pre v-pre><code class="language-java"><span class="java-keyword">public class</span> <span class="java-class">Main</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Hello from IntelliJ IDEA!"</span>);
        
        <span class="java-comment">// Exemple de calcul</span>
        <span class="java-keyword">int</span> <span class="java-variable">a</span> = <span class="java-number">10</span>;
        <span class="java-keyword">int</span> <span class="java-variable">b</span> = <span class="java-number">20</span>;
        <span class="java-keyword">int</span> <span class="java-variable">sum</span> = <span class="java-variable">a</span> + <span class="java-variable">b</span>;
        
        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Sum: "</span> + <span class="java-variable">sum</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">10.4 Exécution du programme</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Plusieurs méthodes pour exécuter :

1. Clique droit dans l'éditeur → "Run Main.main()"
2. Bouton vert en haut à droite
3. Menu Run → Run 'Main'
4. Touche raccourci : Shift + F10

Résultat attendu dans la console :
Hello from IntelliJ IDEA!
Sum: 30</code></pre>
                </div>
            </div>

            <!-- Raccourcis clés IntelliJ -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">11. Raccourcis clés IntelliJ IDEA</h2>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Navigation</h4>
                        <pre v-pre><code class="language-text">Ctrl+N : Chercher une classe
Ctrl+Shift+N : Chercher un fichier
Ctrl+E : Fichiers récents
Ctrl+Shift+E : Editeurs récents
Ctrl+B : Aller à la déclaration
Ctrl+Alt+←/→ : Navigation arrière/avant</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Edition</h4>
                        <pre v-pre><code class="language-text">Ctrl+Space : Auto-complétion
Ctrl+Shift+Space : Complétion intelligente
Ctrl+Alt+L : Formater le code
Ctrl+D : Dupliquer la ligne
Ctrl+Y : Supprimer la ligne
Ctrl+/ : Commenter/décommenter</code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Execution/Débogage</h4>
                        <pre v-pre><code class="language-text">Shift+F10 : Executer
Shift+F9 : Déboguer
F8 : Step Over
F7 : Step Into
Shift+F8 : Step Out
Ctrl+F2 : Arrêter l'execution</code></pre>
                    </div>
                    <div class="code-example">
                        <h4 class="text-purple">Refactoring</h4>
                        <pre v-pre><code class="language-text">Shift+F6 : Renommer
Ctrl+Alt+M : Extraire une méthode
Ctrl+Alt+V : Extraire une variable
Ctrl+Alt+C : Extraire une constante
Ctrl+Alt+P : Extraire un paramètre</code></pre>
                    </div>
                </div>
            </div>

            <!-- Installation des outils complémentaires -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">12. Outils complémentaires recommandés</h2>

                <h3 class="text-purple">12.1 Git (Contrôle de version)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Windows : https://git-scm.com/download/win</span>
<span class="bash-comment"># macOS : brew install git</span>
<span class="bash-comment"># Linux : sudo apt install git</span>

<span class="bash-comment"># Configuration Git</span>
<span class="bash-prompt">$</span> <span class="bash-command">git config --global user.name "Votre Nom"</span>
<span class="bash-prompt">$</span> <span class="bash-command">git config --global user.email "votre@email.com"</span>
<span class="bash-prompt">$</span> <span class="bash-command">git config --global core.editor "code --wait"</span>  <span class="bash-comment"># ou "nano"</span></code></pre>
                </div>

                <h3 class="text-purple">12.2 Maven ou Gradle (Gestion de projets)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Maven</span>
<span class="bash-prompt">$</span> <span class="bash-command">mvn --version</span>

<span class="bash-comment"># Gradle</span>
<span class="bash-prompt">$</span> <span class="bash-command">gradle --version</span></code></pre>
                </div>

                <h3 class="text-purple">12.3 Extensions IntelliJ recommandées</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Plugins essentiels (Settings → Plugins) :

• Atom Material Icons : Icones modernes
• Rainbow Brackets : Couleurs pour les parenthèses
• SonarLint : Analyse de code
• Key Promoter X : Aide à apprendre les raccourcis
• GitToolBox : Fonctionnalités Git avancées</code></pre>
                </div>
            </div>

            <!-- Dépannage commun -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">13. Dépannage des problèmes courants</h2>

                <h3 class="text-purple">Problème 1 : JDK non détecté</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Symptôme : "No JDK found" ou "Invalid JDK"

Solution :
1. Vérifiez l'installation : java --version
2. Dans IntelliJ : File → Project Structure
3. Project SDK → Add JDK
4. Naviguez vers le dossier d'installation
5. Redémarrez IntelliJ</code></pre>
                </div>

                <h3 class="text-purple">Problème 2 : Erreurs de compilation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Symptôme : "Cannot resolve symbol" ou erreurs rouges

Solutions :
1. File → Invalidate Caches → Invalidate and Restart
2. Maven/Gradle : Reimport le projet
3. Vérifiez le JDK : File → Project Structure
4. Build → Rebuild Project</code></pre>
                </div>

                <h3 class="text-purple">Problème 3 : Performances lentes</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-text">Symptôme : IntelliJ est lent

Optimisations :
1. Augmentez la mémoire : Help → Edit Custom VM Options
   -Xmx2048m → -Xmx4096m (pour 4GB RAM)
2. Désactivez les plugins inutiles
3. File → Invalidate Caches
4. Désactivez l'antivirus temporairement</code></pre>
                </div>

                <h3 class="text-purple">Problème 4 : Problèmes de ligne de commande</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Vérification complète</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --version</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac --version</span>
<span class="bash-prompt">$</span> <span class="bash-command">echo $JAVA_HOME</span>  <span class="bash-comment"># ou %JAVA_HOME% sur Windows</span>

<span class="bash-comment"># Si JAVA_HOME n'est pas défini :</span>
<span class="bash-comment"># Windows :</span>
setx JAVA_HOME "C:\Program Files\Java\jdk-21"

<span class="bash-comment"># Linux/macOS :</span>
export JAVA_HOME=/path/to/jdk
echo 'export JAVA_HOME=/path/to/jdk' >> ~/.bashrc</code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">14. Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Configurer un environnement de développement Java complet et créer une application simple.
                    </p>
                    <ol class="textExemple">
                        <li>Installez JDK 21 sur votre système</li>
                        <li>Installez IntelliJ IDEA Community Edition</li>
                        <li>Configurez les variables d'environnement (JAVA_HOME et PATH)</li>
                        <li>Créez un nouveau projet "Calculator" dans IntelliJ</li>
                        <li>Implémentez une calculatrice avec :
                            <ul>
                                <li>Addition, soustraction, multiplication, division</li>
                                <li>Interface en ligne de commande</li>
                                <li>Gestion des erreurs (division par zéro)</li>
                            </ul>
                        </li>
                        <li>Testez votre programme et vérifiez qu'il fonctionne</li>
                        <li>Initialisez un dépôt Git pour votre projet</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Etapes de la solution :</h4>
                        
                        <h5 class="text-purple">Fichier Calculator.java :</h5>
                        <div class="code-example">
                            <pre v-pre><code class="language-java"><span class="java-keyword">import</span> <span class="java-class">java.util.Scanner</span>;

<span class="java-keyword">public class</span> <span class="java-class">Calculator</span> {
    <span class="java-keyword">public static void</span> <span class="java-function">main</span>(<span class="java-class">String</span>[] <span class="java-variable">args</span>) {
        <span class="java-class">Scanner</span> <span class="java-variable">scanner</span> = <span class="java-keyword">new</span> <span class="java-class">Scanner</span>(<span class="java-class">System</span>.<span class="java-variable">in</span>);
        
        <span class="java-keyword">while</span> (<span class="java-keyword">true</span>) {
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"\n=== CALCULATRICE ==="</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"1. Addition"</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"2. Soustraction"</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"3. Multiplication"</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"4. Division"</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"5. Quitter"</span>);
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">print</span>(<span class="java-string">"Choisissez une opération : "</span>);
            
            <span class="java-keyword">int</span> <span class="java-variable">choice</span> = <span class="java-variable">scanner</span>.<span class="java-function">nextInt</span>();
            
            <span class="java-keyword">if</span> (<span class="java-variable">choice</span> == <span class="java-number">5</span>) {
                <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Au revoir !"</span>);
                <span class="java-keyword">break</span>;
            }
            
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">print</span>(<span class="java-string">"Entrez le premier nombre : "</span>);
            <span class="java-keyword">double</span> <span class="java-variable">num1</span> = <span class="java-variable">scanner</span>.<span class="java-function">nextDouble</span>();
            <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">print</span>(<span class="java-string">"Entrez le deuxième nombre : "</span>);
            <span class="java-keyword">double</span> <span class="java-variable">num2</span> = <span class="java-variable">scanner</span>.<span class="java-function">nextDouble</span>();
            
            <span class="java-keyword">double</span> <span class="java-variable">result</span> = <span class="java-number">0</span>;
            <span class="java-keyword">boolean</span> <span class="java-variable">error</span> = <span class="java-keyword">false</span>;
            
            <span class="java-keyword">switch</span> (<span class="java-variable">choice</span>) {
                <span class="java-keyword">case</span> <span class="java-number">1</span>:
                    <span class="java-variable">result</span> = <span class="java-variable">num1</span> + <span class="java-variable">num2</span>;
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-number">2</span>:
                    <span class="java-variable">result</span> = <span class="java-variable">num1</span> - <span class="java-variable">num2</span>;
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-number">3</span>:
                    <span class="java-variable">result</span> = <span class="java-variable">num1</span> * <span class="java-variable">num2</span>;
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">case</span> <span class="java-number">4</span>:
                    <span class="java-keyword">if</span> (<span class="java-variable">num2</span> != <span class="java-number">0</span>) {
                        <span class="java-variable">result</span> = <span class="java-variable">num1</span> / <span class="java-variable">num2</span>;
                    } <span class="java-keyword">else</span> {
                        <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Erreur : Division par zéro !"</span>);
                        <span class="java-variable">error</span> = <span class="java-keyword">true</span>;
                    }
                    <span class="java-keyword">break</span>;
                <span class="java-keyword">default</span>:
                    <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">println</span>(<span class="java-string">"Choix invalide !"</span>);
                    <span class="java-keyword">continue</span>;
            }
            
            <span class="java-keyword">if</span> (!<span class="java-variable">error</span>) {
                <span class="java-class">System</span>.<span class="java-variable">out</span>.<span class="java-function">printf</span>(<span class="java-string">"Résultat : %.2f\n"</span>, <span class="java-variable">result</span>);
            }
        }
        
        <span class="java-variable">scanner</span>.<span class="java-function">close</span>();
    }
}</code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">15. Conclusion et ressources</h2>
                <p class="textExemple">
                    Félicitations ! Vous avez maintenant un environnement de développement Java complet et fonctionnel.
                    Vous êtes prêt à développer des applications Java avec IntelliJ IDEA, l'un des meilleurs IDE disponibles.
                </p>

                <h3 class="text-purple">Prochaines étapes :</h3>
                <ul class="textExemple">
                    <li>Apprendre les bases de la programmation Java (variables, boucles, conditions)</li>
                    <li>Découvrir la programmation orientée objet (classes, objets, héritage)</li>
                    <li>Explorer les collections Java (List, Set, Map)</li>
                    <li>Apprendre à utiliser Maven ou Gradle pour gérer les dépendances</li>
                    <li>Découvrir les tests unitaires avec JUnit</li>
                </ul>

                <h3 class="text-purple">Ressources supplémentaires :</h3>
                <ul class="textExemple">
                    <li><a href="https://docs.oracle.com/javase/tutorial/" target="_blank" class="btn-purple btn-hover">Tutoriel officiel Java (Oracle)</a></li>
                    <li><a href="https://www.jetbrains.com/idea/documentation/" target="_blank" class="btn-purple btn-hover">Documentation IntelliJ IDEA</a></li>
                    <li><a href="https://www.baeldung.com/" target="_blank" class="btn-purple btn-hover">Baeldung - Tutorials Java & Spring</a></li>
                    <li><a href="https://www.jetbrains.com/help/idea/getting-started.html" target="_blank" class="btn-purple btn-hover">Guide de démarrage IntelliJ</a></li>
                    <li><a href="https://github.com/iluwatar/java-design-patterns" target="_blank" class="btn-purple btn-hover">Design Patterns en Java (GitHub)</a></li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Vérification finale de votre installation</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Ouvrez un terminal et exécutez :</span>
<span class="bash-prompt">$</span> <span class="bash-command">java --version</span>
<span class="bash-prompt">$</span> <span class="bash-command">javac --version</span>
<span class="bash-prompt">$</span> <span class="bash-command">idea --version</span>  <span class="bash-comment"># Si IntelliJ est dans le PATH</span>

<span class="bash-comment"># Tout doit fonctionner ! Vous êtes prêt à coder.</span>
<span class="bash-comment"># Bon développement Java !</span></code></pre>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaInstallationLesson'
}
</script>

<style scoped>
/* Styles en violet pour correspondre à votre projet */
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

pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs Java */
.java-keyword {
    color: #569CD6 !important;
}

.java-function {
    color: #DCDCAA !important;
}

.java-class {
    color: #4EC9B0 !important;
}

.java-variable {
    color: #9CDCFE !important;
}

.java-string {
    color: #CE9178 !important;
}

.java-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.java-number {
    color: #B5CEA8 !important;
}

/* Couleurs Bash */
.bash-prompt {
    color: #2ECC71 !important;
    font-weight: bold;
}

.bash-command {
    color: #F1C40F !important;
}

.bash-comment {
    color: #7F8C8D !important;
    font-style: italic;
}

.bash-string {
    color: #E74C3C !important;
}

.bash-keyword {
    color: #3498DB !important;
}

.bash-parameter {
    color: #9B59B6 !important;
}

.bash-number {
    color: #1ABC9C !important;
}

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

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

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

@media (min-width: 1400px) {
    .lesson-content {
        max-width: 1300px;
    }
}

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
</style>