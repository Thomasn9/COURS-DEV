<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Git Flow - Gestion des branches</h1>
        <p class="lesson-meta text-white">Maîtrisez le workflow de développement collaboratif avec Git</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à Git Flow</h2>
        <p class="textExemple">
          Git Flow est un modèle de workflow de branchement pour Git, créé par Vincent Driessen. 
          Il fournit un ensemble robuste de commandes pour accomplir des tâches de branchement et de fusion de haut niveau.
        </p>
        <p class="textExemple">
          Ce modèle définit une structure de branchement stricte conçue autour du cycle de publication du projet. 
          Il attribue des rôles très spécifiques à différentes branches et définit comment et quand elles doivent interagir.
        </p>
      </section>

      <!-- Les branches principales -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les branches principales</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Branche master/main</h3>
          <p class="textExemple">
            La branche <strong>master</strong> (ou <strong>main</strong> dans les projets récents) contient le code de production.
            Chaque commit sur cette branche représente une nouvelle version publiée.
          </p>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Branche develop</h3>
          <p class="textExemple">
            La branche <strong>develop</strong> sert d'intégration pour les fonctionnalités. 
            C'est la branche où le code est fusionné après le développement des fonctionnalités et avant la préparation d'une release.
          </p>
        </div>

        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Créer la branche develop</h4>
            <pre><code class="language-bash"><span class="comment"># Se positionner sur master</span>
<span class="keyword">git checkout</span> master

<span class="comment"># Créer et basculer sur develop</span>
<span class="keyword">git checkout</span> -b develop

<span class="comment"># Pousser develop sur le dépôt distant</span>
<span class="keyword">git push</span> -u origin develop</code></pre>
          </div>
          <div class="code-block">
            <h4 class="text-purple">Vérifier les branches</h4>
            <pre><code class="language-bash"><span class="comment"># Lister toutes les branches</span>
<span class="keyword">git branch</span> -a

<span class="comment"># Voir le dernier commit sur chaque branche</span>
<span class="keyword">git branch</span> -v</code></pre>
          </div>
        </div>
      </section>

      <!-- Les branches de support -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les branches de support</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Branches de fonctionnalités (feature)</h3>
          <p class="textExemple">
            Les branches de fonctionnalités sont utilisées pour développer de nouvelles fonctionnalités pour les prochaines releases.
            Elles partent de <strong>develop</strong> et doivent y être fusionnées.
          </p>
        </div>

        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Créer une feature</h4>
            <pre><code class="language-bash"><span class="comment"># Se positionner sur develop</span>
<span class="keyword">git checkout</span> develop

<span class="comment"># Créer une branche feature</span>
<span class="keyword">git checkout</span> -b feature/nouvelle-fonctionnalite</code></pre>
          </div>
          <div class="code-block">
            <h4 class="text-purple">Fusionner une feature</h4>
            <pre><code class="language-bash"><span class="comment"># Une fois le développement terminé</span>
<span class="keyword">git checkout</span> develop
<span class="keyword">git merge</span> --no-ff feature/nouvelle-fonctionnalite

<span class="comment"># Supprimer la branche feature (optionnel)</span>
<span class="keyword">git branch</span> -d feature/nouvelle-fonctionnalite</code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Branches de release</h3>
          <p class="textExemple">
            Les branches de release préparent une nouvelle version de production. 
            Elles permettent les derniers ajustements mineurs et les corrections de bugs.
          </p>
        </div>

        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Créer une release</h4>
            <pre><code class="language-bash"><span class="comment"># Se positionner sur develop</span>
<span class="keyword">git checkout</span> develop

<span class="comment"># Créer une branche release</span>
<span class="keyword">git checkout</span> -b release/1.2.0</code></pre>
          </div>
          <div class="code-block">
            <h4 class="text-purple">Finaliser une release</h4>
            <pre><code class="language-bash"><span class="comment"># Fusionner dans master</span>
<span class="keyword">git checkout</span> master
<span class="keyword">git merge</span> --no-ff release/1.2.0

<span class="comment"># Taguer la release</span>
<span class="keyword">git tag</span> -a v1.2.0 -m <span class="string">"Version 1.2.0"</span>

<span class="comment"># Fusionner dans develop</span>
<span class="keyword">git checkout</span> develop
<span class="keyword">git merge</span> --no-ff release/1.2.0</code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Branches de correctif (hotfix)</h3>
          <p class="textExemple">
            Les branches de correctif sont nécessaires pour agir immédiatement sur un problème en production.
            Elles partent de <strong>master</strong> et doivent être fusionnées à la fois dans <strong>master</strong> et <strong>develop</strong>.
          </p>
        </div>

        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Créer un hotfix</h4>
            <pre><code class="language-bash"><span class="comment"># Se positionner sur master</span>
<span class="keyword">git checkout</span> master

<span class="comment"># Créer un hotfix</span>
<span class="keyword">git checkout</span> -b hotfix/urgence-production</code></pre>
          </div>
          <div class="code-block">
            <h4 class="text-purple">Finaliser un hotfix</h4>
            <pre><code class="language-bash"><span class="comment"># Fusionner dans master</span>
<span class="keyword">git checkout</span> master
<span class="keyword">git merge</span> --no-ff hotfix/urgence-production

<span class="comment"># Taguer la correction</span>
<span class="keyword">git tag</span> -a v1.2.1 -m <span class="string">"Correctif urgent v1.2.1"</span>

<span class="comment"># Fusionner dans develop</span>
<span class="keyword">git checkout</span> develop
<span class="keyword">git merge</span> --no-ff hotfix/urgence-production</code></pre>
          </div>
        </div>
      </section>

      <!-- Workflow complet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Workflow Git Flow complet</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Installation de Git Flow</h3>
          <p class="textExemple">
            Git Flow peut être utilisé avec des extensions qui simplifient les commandes.
          </p>
          <pre><code class="language-bash"><span class="comment"># Installation sur macOS avec Homebrew</span>
brew install git-flow

<span class="comment"># Installation sur Linux</span>
apt-get install git-flow

<span class="comment"># Initialisation dans un dépôt existant</span>
git flow init</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Commandes Git Flow simplifiées</h3>
          <div class="code-comparison">
            <div class="code-block">
              <h4 class="text-purple">Démarrer une feature</h4>
              <pre><code class="language-bash">git flow feature start nouvelle-fonctionnalite</code></pre>
            </div>
            <div class="code-block">
              <h4 class="text-purple">Terminer une feature</h4>
              <pre><code class="language-bash">git flow feature finish nouvelle-fonctionnalite</code></pre>
            </div>
          </div>
          
          <div class="code-comparison">
            <div class="code-block">
              <h4 class="text-purple">Démarrer une release</h4>
              <pre><code class="language-bash">git flow release start 1.3.0</code></pre>
            </div>
            <div class="code-block">
              <h4 class="text-purple">Terminer une release</h4>
              <pre><code class="language-bash">git flow release finish 1.3.0</code></pre>
            </div>
          </div>
          
          <div class="code-comparison">
            <div class="code-block">
              <h4 class="text-purple">Démarrer un hotfix</h4>
              <pre><code class="language-bash">git flow hotfix start 1.3.1</code></pre>
            </div>
            <div class="code-block">
              <h4 class="text-purple">Terminer un hotfix</h4>
              <pre><code class="language-bash">git flow hotfix finish 1.3.1</code></pre>
            </div>
          </div>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques Git Flow</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Conventions de nommage</h3>
          <ul class="textExemple">
            <li><strong>feature/</strong> : pour les nouvelles fonctionnalités (ex: feature/user-authentication)</li>
            <li><strong>release/</strong> : pour les préparations de release (ex: release/1.2.0)</li>
            <li><strong>hotfix/</strong> : pour les correctifs urgents (ex: hotfix/critical-security-fix)</li>
            <li><strong>bugfix/</strong> : pour les corrections de bugs non critiques</li>
          </ul>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Règles importantes</h3>
          <ul class="textExemple">
            <li>Ne jamais pousser directement sur <strong>master</strong> ou <strong>develop</strong></li>
            <li>Utiliser des messages de commit clairs et descriptifs</li>
            <li>Fusionner avec <code>--no-ff</code> pour garder l'historique des branches</li>
            <li>Supprimer les branches de support après fusion</li>
            <li>Taguer systématiquement les releases sur master</li>
          </ul>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Mise en place de Git Flow</h3>
          <p class="textExemple">
            Initialisez Git Flow dans un dépôt Git existant et configurez les branches principales.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code class="language-bash"><span class="comment"># Se positionner dans votre dépôt</span>
<span class="keyword">cd</span> mon-projet

<span class="comment"># Initialiser Git Flow</span>
git flow init

<span class="comment"># Accepter les valeurs par défaut ou les modifier</span>
<span class="comment"># Les valeurs par défaut sont généralement :</span>
<span class="comment"># - Branche de production : master</span>
<span class="comment"># - Branche de développement : develop</span>
<span class="comment"># - Préfixe feature : feature/</span>
<span class="comment"># - Préfixe release : release/</span>
<span class="comment"># - Préfixe hotfix : hotfix/</span>
<span class="comment"># - Préfixe support : support/</span>
<span class="comment"># - Préfixe versiontag : (vide)</span></code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Cycle de développement complet</h3>
          <p class="textExemple">
            Réalisez un cycle complet de développement avec Git Flow :
          </p>
          <ol class="textExemple">
            <li>Créez une nouvelle fonctionnalité</li>
            <li>Préparez une release</li>
            <li>Corrigez un bug en production avec un hotfix</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>1. Création d'une fonctionnalité</h4>
              <pre><code class="language-bash">git flow feature start ajout-panier
<span class="comment"># Développez votre fonctionnalité...</span>
<span class="keyword">git add</span> .
<span class="keyword">git commit</span> -m <span class="string">"Ajout du panier d'achat"</span>
git flow feature finish ajout-panier</code></pre>

              <h4>2. Préparation d'une release</h4>
              <pre><code class="language-bash">git flow release start 1.0.0
<span class="comment"># Effectuez les derniers ajustements...</span>
git flow release finish 1.0.0</code></pre>

              <h4>3. Correction d'un bug en production</h4>
              <pre><code class="language-bash">git flow hotfix start correction-prix
<span class="comment"># Corrigez le bug...</span>
<span class="keyword">git add</span> .
<span class="keyword">git commit</span> -m <span class="string">"Correction du calcul des prix"</span>
git flow hotfix finish correction-prix</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Ressources supplémentaires -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Liens utiles</h3>
          <ul class="textExemple">
            <li><a href="https://nvie.com/posts/a-successful-git-branching-model/" class="btn-purple btn-hover" target="_blank">Article original de Vincent Driessen</a></li>
            <li><a href="https://github.com/nvie/gitflow" class="btn-purple btn-hover" target="_blank">Extension Git Flow officielle</a></li>
            <li><a href="https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow" class="btn-purple btn-hover" target="_blank">Tutoriel Git Flow par Atlassian</a></li>
          </ul>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Outils complémentaires</h3>
          <ul class="textExemple">
            <li><strong>GitKraken</strong> : Client Git avec support visuel de Git Flow</li>
            <li><strong>SourceTree</strong> : Client Git gratuit d'Atlassian</li>
            <li><strong>GitHub Desktop</strong> : Client officiel GitHub avec workflow simplifié</li>
          </ul>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GitFlowLesson',
  head() {
    return {
      title: 'Git Flow - Leçon sur la gestion des branches',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez à utiliser Git Flow pour une gestion efficace des branches dans vos projets de développement.'
        }
      ]
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

/* Couleurs VS Code pour la syntaxe Bash */
.keyword { color: #c586c0 !important; } /* Mots-clés Git (checkout, branch, merge, etc.) */
.comment { color: #6a9955 !important; } /* Commentaires */
.string { color: #ce9178 !important; } /* Chaînes de caractères */
.function { color: #dcdcaa !important; } /* Noms de fonctions/commandes */
.operator { color: #d4d4d4 !important; } /* Opérateurs (+, -, =, etc.) */
.constant { color: #4fc1ff !important; } /* Constantes */
.number { color: #b5cea8 !important; } /* Nombres */
.variable { color: #9cdcfe !important; } /* Variables */

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