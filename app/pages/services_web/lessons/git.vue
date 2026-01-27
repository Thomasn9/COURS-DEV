<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Git : Gestion de version</h1>
                <p class="lesson-meta text-white">Maîtrisez les bases de Git pour vos projets de développement</p>
            </header>

            <!-- Introduction à Git -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Git ?</h2>
                <p class="textExemple">
                    Git est un système de contrôle de version distribué qui permet de suivre les modifications
                    apportées aux fichiers d'un projet au fil du temps. Il est largement utilisé dans le
                    développement logiciel pour collaborer efficacement et gérer les différentes versions d'un projet.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Avantages de Git :</h3>
                    <ul>
                        <li>Historique complet des modifications</li>
                        <li>Collaboration simplifiée entre développeurs</li>
                        <li>Possibilité de travailler sur différentes fonctionnalités simultanément (branches)</li>
                        <li>Restauration facile de versions antérieures</li>
                        <li>Intégration avec les plateformes comme GitHub, GitLab, Bitbucket</li>
                    </ul>
                </div>
            </section>

            <!-- NOUVELLE SECTION : Comment débuter avec Git -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comment débuter avec Git</h2>
                <p class="textExemple">
                    Pour commencer à utiliser Git, suivez ces étapes simples qui vous permettront de vous familiariser
                    avec les concepts de base et de mettre en pratique vos premières commandes.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">1. Installation de Git</h3>
                    <p>Téléchargez et installez Git sur votre système :</p>
                    
                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Windows :</h4>
                            <ul>
                                <li>Téléchargez l'installateur depuis <a href="https://git-scm.com/" target="_blank" class="text-purple">git-scm.com</a></li>
                                <li>Exécutez l'installateur avec les paramètres par défaut</li>
                                <li>Vérifiez l'installation avec :</li>
                                <pre><code class="language-bash">git --version</code></pre>
                            </ul>
                        </div>
                        
                        <div>
                            <h4 class="text-purple">MacOS :</h4>
                            <ul>
                                <li>Avec Homebrew :</li>
                                <pre><code class="language-bash">brew install git</code></pre>
                                <li>Ou téléchargez depuis le site officiel</li>
                            </ul>
                            
                            <h4 class="text-purple">Linux (Debian/Ubuntu) :</h4>
                            <pre><code class="language-bash">sudo apt-get update
sudo apt-get install git</code></pre>
                        </div>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">2. Configuration initiale</h3>
                    <p>Après l'installation, configurez votre identité Git :</p>
                    <pre><code class="language-bash"># Configurer votre nom d'utilisateur
git config --global user.name "Votre Nom"

# Configurer votre email
git config --global user.email "votre.email@exemple.com"

# Vérifier la configuration
git config --list</code></pre>
                    <p class="textExemple">
                        Ces informations apparaîtront dans tous vos commits et sont essentielles pour collaborer.
                    </p>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">3. Premier pas : créer un dépôt local</h3>
                    <p>Commencez par créer un projet test pour vous familiariser :</p>
                    <pre><code class="language-bash"># Créer un dossier pour votre projet test
mkdir mon-premier-projet-git
cd mon-premier-projet-git

# Initialiser un dépôt Git
git init

# Créer un premier fichier
echo "# Mon Premier Projet Git" > README.md

# Vérifier l'état de votre dépôt
git status</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">4. Comprendre les trois états de Git</h3>
                    <p>Git fonctionne avec trois états principaux :</p>
                    
                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">📁 Working Directory</h4>
                            <ul>
                                <li>Fichiers sur votre ordinateur</li>
                                <li>Modifications non suivies</li>
                                <li>État : <code>untracked</code> ou <code>modified</code></li>
                            </ul>
                        </div>
                        
                        <div>
                            <h4 class="text-purple">📦 Staging Area</h4>
                            <ul>
                                <li>Zone de préparation</li>
                                <li>Fichiers prêts à être commités</li>
                                <li>Commande : <code>git add</code></li>
                            </ul>
                        </div>
                        
                        <div>
                            <h4 class="text-purple">💾 Repository</h4>
                            <ul>
                                <li>Base de données Git</li>
                                <li>Historique des commits</li>
                                <li>Commande : <code>git commit</code></li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="workflow-visual">
                        <h4 class="text-purple">📋 Workflow de base :</h4>
                        <div class="workflow-steps">
                            <div class="step">
                                <span class="step-number">1</span>
                                <span class="step-text">Modifier des fichiers</span>
                            </div>
                            <div class="step-arrow">→</div>
                            <div class="step">
                                <span class="step-number">2</span>
                                <span class="step-text"><code>git add</code> (staging)</span>
                            </div>
                            <div class="step-arrow">→</div>
                            <div class="step">
                                <span class="step-number">3</span>
                                <span class="step-text"><code>git commit</code> (sauvegarde)</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">5. Ressources pour apprendre</h3>
                    <p>Pour approfondir vos connaissances :</p>
                    
                    <div class="resources-grid">
                        <div class="resource-card">
                            <h4 class="text-purple">📚 Documentation officielle</h4>
                            <ul>
                                <li><a href="https://git-scm.com/doc" target="_blank" class="text-purple">Documentation Git</a></li>
                                <li>Pro Git (livre gratuit)</li>
                                <li>Git Cheat Sheet</li>
                            </ul>
                        </div>
                        
                        <div class="resource-card">
                            <h4 class="text-purple">🎮 Apprentissage interactif</h4>
                            <ul>
                                <li>GitHub Learning Lab</li>
                                <li>Atlassian Git Tutorial</li>
                                <li>Codecademy Git Course</li>
                            </ul>
                        </div>
                        
                        <div class="resource-card">
                            <h4 class="text-purple">🛠️ Outils recommandés</h4>
                            <ul>
                                <li>Git Bash (Windows)</li>
                                <li>GitKraken (GUI)</li>
                                <li>VS Code Git intégration</li>
                            </ul>
                        </div>
                    </div>
                </div>
                
                <div class="tip-box">
                    <h4 class="text-purple">💡 Conseil pour débutants</h4>
                    <p class="textExemple">
                        Commencez par utiliser Git en local pour des projets personnels avant de vous lancer dans la collaboration.
                        Pratiquez les commandes de base jusqu'à ce qu'elles deviennent naturelles. N'ayez pas peur de faire
                        des erreurs – c'est en forgeant qu'on devient forgeron !
                    </p>
                </div>
            </section>

            <!-- Utilité de Git dans un projet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilité de Git dans un projet</h2>
                <p class="textExemple">
                    Git est essentiel dans tout projet de développement, qu'il soit personnel ou professionnel.
                    Voici pourquoi il est indispensable :
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Sans Git :</h4>
                        <ul>
                            <li>Fichiers sauvegardés manuellement (v1, v2, v3_final, v3_final_reel...)</li>
                            <li>Difficile de collaborer sans écraser le travail des autres</li>
                            <li>Impossible de savoir qui a modifié quoi et quand</li>
                            <li>Risque de perdre des modifications importantes</li>
                        </ul>
                    </div>

                    <div>
                        <h4 class="text-purple">Avec Git :</h4>
                        <ul>
                            <li>Historique organisé et détaillé de toutes les modifications</li>
                            <li>Collaboration simultanée sans conflits</li>
                            <li>Traçabilité complète des changements</li>
                            <li>Sécurité et possibilité de revenir en arrière à tout moment</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Étapes pour lier un projet à un dépôt -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étapes pour lier un projet à un dépôt Git</h2>
                <p class="textExemple">
                    Voici comment initialiser Git dans un projet existant et le lier à un dépôt distant :
                </p>

                <div class="code-example">
                    <h3 class="text-purple">1. Initialiser Git dans votre projet</h3>
                    <p>Ouvrez votre terminal dans le dossier de votre projet et exécutez :</p>
                    <pre><code class="language-bash">git init</code></pre>
                    <p>Cette commande crée un nouveau dépôt Git local.</p>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">2. Ajouter tous les fichiers au suivi de Git</h3>
                    <pre><code class="language-bash">git add .</code></pre>
                    <p>Ou pour ajouter un fichier spécifique :</p>
                    <pre><code class="language-bash">git add nom_du_fichier</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">3. Effectuer le premier commit</h3>
                    <pre><code class="language-bash">git commit -m "Message décrivant les modifications"</code></pre>
                    <p>Exemple :</p>
                    <pre><code class="language-bash">git commit -m "Initial commit - configuration du projet"</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">4. Lier au dépôt distant (GitHub, GitLab, etc.)</h3>
                    <pre><code class="language-bash">git remote add origin https://github.com/votre-utilisateur/votre-depot.git</code></pre>
                    <p>Remplacez l'URL par celle de votre propre dépôt.</p>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">5. Pousser le code vers le dépôt distant</h3>
                    <pre><code class="language-bash">git push -u origin main</code></pre>
                    <p>Ou selon le nom de votre branche par défaut :</p>
                    <pre><code class="language-bash">git push -u origin master</code></pre>
                </div>
            </section>

            <!-- Créer un nouveau dépôt -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer un nouveau dépôt Git</h2>
                <p class="textExemple">
                    Vous pouvez créer un nouveau dépôt Git de deux manières : en initialisant un projet existant
                    ou en créant un nouveau dépôt sur une plateforme comme GitHub.
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Méthode 1 : Initialiser un projet existant</h4>
                        <pre><code class="language-bash"># Se placer dans le dossier du projet
cd mon-projet

# Initialiser Git
git init

# Ajouter les fichiers
git add .

# Premier commit
git commit -m "Initial commit"

# Créer le dépôt sur GitHub (manuellement)
# Puis lier le dépôt local au distant
git remote add origin https://github.com/utilisateur/mon-projet.git
git push -u origin main</code></pre>
                    </div>

                    <div>
                        <h4 class="text-purple">Méthode 2 : Créer d'abord sur GitHub</h4>
                        <pre><code class="language-bash"># Créer le dépôt sur GitHub (via l'interface web)
# Puis cloner le dépôt vide
git clone https://github.com/utilisateur/mon-projet.git

# Se déplacer dans le dossier
cd mon-projet

# Ajouter vos fichiers
# Puis les commiter et pousser
git add .
git commit -m "Ajout des fichiers du projet"
git push origin main</code></pre>
                    </div>
                </div>
            </section>

            <!-- Commandes Git essentielles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Commandes Git essentielles</h2>
                <p class="textExemple">
                    Voici les commandes Git de base que vous utiliserez quotidiennement :
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Workflow de base</h3>
                    <pre><code class="language-bash"># Vérifier l'état des fichiers
git status

# Ajouter des fichiers à l'index
git add fichier.html
git add .  # Tous les fichiers

# Consigner les modifications
git commit -m "Description des changements"

# Envoyer les modifications vers le dépôt distant
git push</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Récupérer les modifications</h3>
                    <pre><code class="language-bash"># Télécharger les dernières modifications
git pull

# Voir l'historique des commits
git log

# Voir les différences entre les fichiers
git diff</code></pre>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer un nouveau projet, l'initialiser avec Git et le pousser sur
                        GitHub.
                    </p>

                    <ol>
                        <li>Créez un nouveau dossier pour votre projet</li>
                        <li>Initialisez Git dans ce dossier</li>
                        <li>Créez un fichier README.md avec une brève description</li>
                        <li>Ajoutez ce fichier à l'index Git</li>
                        <li>Effectuez un premier commit</li>
                        <li>Créez un nouveau dépôt sur GitHub</li>
                        <li>Lie votre dépôt local au dépôt distant</li>
                        <li>Poussez votre code vers GitHub</li>
                    </ol>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution étape par étape :</h4>

                            <p>1. Créer et se déplacer dans le dossier :</p>
                            <pre><code class="language-bash">mkdir mon-nouveau-projet
cd mon-nouveau-projet</code></pre>

                            <p>2. Initialiser Git :</p>
                            <pre><code class="language-bash">git init</code></pre>

                            <p>3. Créer le fichier README.md :</p>
                            <pre><code class="language-bash">echo "# Mon Nouveau Projet" >> README.md
echo "Ceci est mon premier projet versionné avec Git." >> README.md</code></pre>

                            <p>4. Ajouter le fichier à l'index :</p>
                            <pre><code class="language-bash">git add README.md</code></pre>

                            <p>5. Effectuer le premier commit :</p>
                            <pre><code class="language-bash">git commit -m "Ajout du fichier README"</code></pre>

                            <p>6. Créer le dépôt sur GitHub (via l'interface web)</p>

                            <p>7. Lier le dépôt local au distant :</p>
                            <pre><code class="language-bash">git remote add origin https://github.com/votre-utilisateur/mon-nouveau-projet.git</code></pre>

                            <p>8. Pousser le code :</p>
                            <pre><code class="language-bash">git push -u origin main</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Navigation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pour aller plus loin</h2>
                <p class="textExemple">
                    Maintenant que vous maîtrisez les bases de Git, vous pouvez explorer des concepts plus avancés :
                </p>

                <div class="code-example">
                    <ul>
                        <li>Les branches et les fusions (git branch, git merge)</li>
                        <li>La résolution de conflits</li>
                        <li>Les tags pour marquer des versions (git tag)</li>
                        <li>Git stash pour sauvegarder temporairement des modifications</li>
                        <li>Les hooks Git pour automatiser des tâches</li>
                    </ul>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'GitLesson',
    // Si vous utilisez la composition API
    setup() {
        return {
            // Données ou méthodes si nécessaires
        }
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
    /* Permet le retour à la ligne */
    word-wrap: break-word;
    /* Casse les mots longs */
    word-break: break-word;
    /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Styles pour la nouvelle section */
.workflow-visual {
    margin: 1.5rem 0;
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

.workflow-steps {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 1rem;
    margin-top: 1rem;
}

.step {
    flex: 1;
    min-width: 120px;
    text-align: center;
    padding: 1rem;
    background: #f8f6ff;
    border-radius: 8px;
    border: 2px solid #e0d6ff;
}

.step-number {
    display: block;
    width: 30px;
    height: 30px;
    background: #6A3093;
    color: white;
    border-radius: 50%;
    margin: 0 auto 0.5rem auto;
    line-height: 30px;
    font-weight: bold;
}

.step-text {
    display: block;
    font-size: 0.9rem;
}

.step-arrow {
    color: #6A3093;
    font-size: 1.5rem;
    font-weight: bold;
}

.resources-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
}

.resource-card {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    border: 1px solid #e0d6ff;
    transition: transform 0.3s ease;
}

.resource-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 15px rgba(106, 48, 147, 0.1);
}

.tip-box {
    margin-top: 2rem;
    padding: 1.5rem;
    background: linear-gradient(135deg, #e6f7ff 0%, #f0e6ff 100%);
    border-radius: 10px;
    border-left: 4px solid #6A3093;
}

.tip-box h4 {
    margin-top: 0;
}

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (for, while, if, function, etc.) */
.variable {
    color: #9cdcfe !important;
}

/* Variables et noms de fonctions */
.string {
    color: #ce9178 !important;
}

/* Chaînes de caractères */
.comment {
    color: #6a9955 !important;
}

/* Commentaires */
.function {
    color: #dcdcaa !important;
}

/* Noms de fonctions */
.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs (+, -, =, =>, etc.) */
.constant {
    color: #4fc1ff !important;
}

/* Constantes */
.number {
    color: #b5cea8 !important;
}

/* Nombres */
.class-name {
    color: #4ec9b0 !important;
}

/* Noms de classes */

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

/* Liens */
a.text-purple {
    color: #6A3093;
    text-decoration: none;
    font-weight: 500;
}

a.text-purple:hover {
    text-decoration: underline;
    color: #5a287a;
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

    .workflow-steps {
        flex-direction: column;
    }
    
    .step-arrow {
        transform: rotate(90deg);
    }
    
    .resources-grid {
        grid-template-columns: 1fr;
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
    
    .step {
        min-width: 100%;
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