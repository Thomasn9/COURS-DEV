<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Git : Branches et Fusions</h1>
        <p class="lesson-meta text-white">Maîtrisez le travail avec les branches et les fusions dans Git</p>
      </header>

      <!-- Introduction aux branches -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce qu'une branche Git ?</h2>
        <p class="textExemple">
          Une branche dans Git est un pointeur vers un commit spécifique. Elle vous permet de développer 
          des fonctionnalités, de corriger des bugs ou d'expérimenter des idées dans une zone isolée 
          sans affecter la branche principale de votre projet.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Avantages du travail avec des branches :</h3>
          <ul>
            <li>Développement isolé de nouvelles fonctionnalités</li>
            <li>Expérimentation sans risque</li>
            <li>Collaboration parallèle sur différentes parties du projet</li>
            <li>Organisation claire du workflow de développement</li>
            <li>Facilité de revue de code via les pull requests</li>
          </ul>
        </div>
      </section>

      <!-- Commandes de base des branches -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Commandes de base pour les branches</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Création et navigation</h4>
            <pre><code class="language-bash"># Lister toutes les branches
git branch

# Créer une nouvelle branche
git branch nouvelle-branche

# Se déplacer vers une branche
git checkout nouvelle-branche

# Créer et se déplacer vers une nouvelle branche
git checkout -b nouvelle-branche

# Supprimer une branche (locale)
git branch -d branche-a-supprimer

# Supprimer une branche (forcée)
git branch -D branche-a-supprimer</code></pre>
          </div>
          
          <div>
            <h4 class="text-purple">Branches distantes</h4>
            <pre><code class="language-bash"># Lister les branches distantes
git branch -r

# Lister toutes les branches (locales et distantes)
git branch -a

# Pousser une branche vers le dépôt distant
git push -u origin ma-branche

# Récupérer les branches distantes
git fetch --all

# Supprimer une branche distante
git push origin --delete branche-distante</code></pre>
          </div>
        </div>
      </section>

      <!-- Types de branches courantes -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de branches courantes</h2>
        <p class="textExemple">
          Dans un workflow Git typique, on utilise généralement plusieurs types de branches :
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Branches principales</h3>
          <ul>
            <li><strong>main/master</strong> : Branche principale de production</li>
            <li><strong>develop</strong> : Branche de développement intégré</li>
            <li><strong>feature/*</strong> : Branches pour les nouvelles fonctionnalités</li>
            <li><strong>hotfix/*</strong> : Branches pour les corrections urgentes</li>
            <li><strong>release/*</strong> : Branches pour la préparation des versions</li>
          </ul>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de workflow avec branches</h3>
          <pre><code class="language-bash"># Créer une branche pour une nouvelle fonctionnalité
git checkout -b feature/ajout-paiement

# Travailler sur la fonctionnalité...
git add .
git commit -m "Ajout du système de paiement"

# Une fois terminé, merger dans develop
git checkout develop
git merge feature/ajout-paiement

# Pour une release
git checkout -b release/v1.2.0
# Préparer la release, puis merger dans main et develop</code></pre>
        </div>
      </section>

      <!-- Les fusions (merge) -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les fusions (Merge) dans Git</h2>
        <p class="textExemple">
          La fusion permet de combiner le travail de différentes branches. Git propose plusieurs 
          stratégies de fusion selon vos besoins.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Types de fusion</h3>
          <pre><code class="language-bash"># Fusion simple (fast-forward si possible)
git merge nom-branche

# Fusion avec création d'un commit de merge
git merge --no-ff nom-branche

# Fusion avec stratégie spécifique
git merge -s recursive nom-branche

# Annuler une fusion en cours (en cas de conflit)
git merge --abort</code></pre>
        </div>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Fast-Forward Merge</h4>
            <p>Se produit quand il n'y a pas de nouveaux commits sur la branche de destination.</p>
            <pre><code class="language-bash"># Avant fusion
A---B---C main
         \
          D---E feature

# Après fusion fast-forward
A---B---C---D---E main</code></pre>
          </div>
          
          <div>
            <h4 class="text-purple">3-Way Merge</h4>
            <p>Se produit quand les deux branches ont de nouveaux commits.</p>
            <pre><code class="language-bash"># Avant fusion
A---B---C---F main
         \
          D---E feature

# Après fusion 3-way
A---B---C---F---G main
         \       /
          D---E</code></pre>
          </div>
        </div>
      </section>

      <!-- Résolution de conflits -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Résolution des conflits de fusion</h2>
        <p class="textExemple">
          Les conflits surviennent quand Git ne peut pas fusionner automatiquement des modifications 
          contradictoires dans le même fichier.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Processus de résolution</h3>
          <pre><code class="language-bash"># Tentative de fusion qui génère un conflit
git merge feature/conflit

# Git vous indique les fichiers en conflit
# Éditez les fichiers et résolvez les conflits

# Marquez les conflits comme résolus
git add fichier-conflit.txt

# Finalisez la fusion
git commit</code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de conflit dans un fichier</h3>
          <pre><code class="language-text">&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD
Ceci est le contenu de la branche principale.
=======
Ceci est le contenu de la branche feature.
&gt;&gt;&gt;&gt;&gt;&gt;&gt; feature/conflit</code></pre>
          
          <p>Pour résoudre, choisissez une version ou combinez les deux :</p>
          <pre><code class="language-text">Ceci est le contenu combiné des deux branches.
Ceci est le contenu de la branche principale.
Ceci est le contenu de la branche feature.</code></pre>
        </div>
      </section>

      <!-- Les rebase -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Rebase vs Merge</h2>
        <p class="textExemple">
          Le rebase est une alternative à la fusion qui réécrit l'historique des commits pour 
          créer un historique linéaire plus propre.
        </p>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Git Merge</h4>
            <pre><code class="language-bash"># Historique avant
A---B---C main
         \
          D---E feature

# Après git merge feature
A---B---C---F main
         \   /
          D---E</code></pre>
            <p><strong>Avantages :</strong></p>
            <ul>
              <li>Historique complet et fidèle</li>
              <li>Simple à comprendre</li>
              <li>Conserve le contexte</li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-purple">Git Rebase</h4>
            <pre><code class="language-bash"># Historique avant
A---B---C main
         \
          D---E feature

# Après git rebase main (depuis feature)
A---B---C---D'---E' main
                 feature</code></pre>
            <p><strong>Avantages :</strong></p>
            <ul>
              <li>Historique linéaire et propre</li>
              <li>Facilite la lecture de l'historique</li>
              <li>Meilleur pour les petites fonctionnalités</li>
            </ul>
          </div>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Commandes Rebase</h3>
          <pre><code class="language-bash"># Rebase interactif
git rebase -i main

# Rebase simple
git rebase main

# Continuer après résolution de conflit
git rebase --continue

# Annuler un rebase
git rebase --abort</code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques pour les branches</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Conventions de nommage</h3>
          <pre><code class="language-bash"># Fonctionnalités
feature/nom-fonctionnalite
feature/user-authentication

# Corrections de bugs
fix/nom-bug
fix/login-error

# Corrections urgentes
hotfix/nom-urgence
hotfix/security-patch

# Releases
release/version
release/v1.2.0</code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Workflow recommandé</h3>
          <ul>
            <li>Une branche par fonctionnalité/bug</li>
            <li>Branches courtes et spécifiques</li>
            <li>Commits atomiques et descriptifs</li>
            <li>Review de code avant merge</li>
            <li>Suppression des branches fusionnées</li>
          </ul>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique : Gestion des branches</h2>
        <div class="exercise">
          <p class="textExemple">
            <strong>Objectif :</strong> Créer et gérer des branches pour développer une nouvelle fonctionnalité.
          </p>
          
          <ol>
            <li>Créez une nouvelle branche "feature/contact-form"</li>
            <li>Ajoutez un fichier contact.html avec un formulaire basique</li>
            <li>Faites plusieurs commits pour différentes parties du formulaire</li>
            <li>Revenez sur la branche main et modifiez le fichier README</li>
            <li>Revenez sur votre branche feature et fusionnez les modifications de main</li>
            <li>Résolvez les éventuels conflits</li>
            <li>Fusionnez la branche feature dans main</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Solution étape par étape :</h4>
              
              <p>1. Créer et se déplacer vers la nouvelle branche :</p>
              <pre><code class="language-bash">git checkout -b feature/contact-form</code></pre>
              
              <p>2. Créer le fichier contact.html :</p>
              <pre><code class="language-bash">echo "&lt;form&gt;&lt;input placeholder='Nom'&gt;&lt;/form&gt;" > contact.html
git add contact.html
git commit -m "Ajout structure basique formulaire contact"</code></pre>
              
              <p>3. Ajouter des styles et validation :</p>
              <pre><code class="language-bash">echo "&lt;style&gt;form { margin: 20px; }&lt;/style&gt;" >> contact.html
git add contact.html
git commit -m "Ajout styles pour le formulaire"</code></pre>
              
              <p>4. Revenir sur main et modifier README :</p>
              <pre><code class="language-bash">git checkout main
echo "Projet avec formulaire de contact" >> README.md
git add README.md
git commit -m "Mise à jour documentation"</code></pre>
              
              <p>5. Revenir sur feature et merger main :</p>
              <pre><code class="language-bash">git checkout feature/contact-form
git merge main</code></pre>
              
              <p>6. Si conflit dans README.md, résoudre :</p>
              <pre><code class="language-bash"># Éditer README.md pour combiner les contenus
git add README.md
git commit -m "Résolution conflit README"</code></pre>
              
              <p>7. Fusionner feature dans main :</p>
              <pre><code class="language-bash">git checkout main
git merge feature/contact-form
git branch -d feature/contact-form</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Scénarios avancés -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Scénarios avancés</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Stash pour sauvegarder temporairement</h3>
          <pre><code class="language-bash"># Sauvegarder les modifications en cours
git stash

# Appliquer les modifications sauvegardées
git stash pop

# Lister tous les stash
git stash list

# Supprimer un stash spécifique
git stash drop stash@{0}</code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Cherry-pick pour prendre des commits spécifiques</h3>
          <pre><code class="language-bash"># Prendre un commit spécifique d'une autre branche
git cherry-pick abc123

# Prendre plusieurs commits
git cherry-pick abc123 def456</code></pre>
        </div>
      </section>

      <!-- Navigation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pour aller plus loin</h2>
        <p class="textExemple">
          Maintenant que vous maîtrisez les branches et fusions, explorez ces concepts avancés :
        </p>
        
        <div class="code-example">
          <ul>
            <li>Git Flow et GitHub Flow (workflows de branchement)</li>
            <li>Les hooks Git pour automatiser les processus</li>
            <li>Les tags pour marquer des releases</li>
            <li>Les sous-modules Git pour les projets complexes</li>
            <li>Les stratégies de merge avancées</li>
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