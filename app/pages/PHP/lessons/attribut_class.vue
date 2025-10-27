<template>
  <div class="lesson-container">
    <div class="lesson-content">
      
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les attributs d'une classe en PHP</h1>
        <p class="lesson-meta text-white">Programmation Orientée Objet (POO) - PHP</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p>En programmation orientée objet (POO), les attributs (ou propriétés) sont les variables internes d'une classe qui définissent son état. Ils représentent les caractéristiques ou données d'un objet.</p>
        <p>Dans cette leçon, nous allons explorer comment déclarer, utiliser et manipuler les attributs d'une classe en PHP.</p>
      </section>

      <!-- Déclaration des attributs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Déclaration des attributs</h2>
        <p>En PHP, les attributs sont déclarés au sein d'une classe en utilisant les mots-clés de visibilité (<code>public</code>, <code>protected</code>, <code>private</code>).</p>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de déclaration</h3>
          <pre><code>&lt;?php
class <span class="class-name">Personne</span> {
    // Attributs publics (accessibles de partout)
    <span class="keyword">public</span> <span class="variable">$nom</span>;
    <span class="keyword">public</span> <span class="variable">$prenom</span>;
    
    // Attribut protégé (accessible dans la classe et ses enfants)
    <span class="keyword">protected</span> <span class="variable">$age</span>;
    
    // Attribut privé (accessible uniquement dans la classe)
    <span class="keyword">private</span> <span class="variable">$email</span>;
    
    // Attribut avec valeur par défaut
    <span class="keyword">public</span> <span class="variable">$statut</span> = <span class="string">"actif"</span>;
}</code></pre>
        </div>
      </section>

      <!-- Visibilité des attributs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Visibilité des attributs</h2>
        <p>PHP propose trois niveaux de visibilité pour les attributs :</p>
        
        <div class="code-comparison">
          <div class="code-block">
            <h3 class="text-purple">Public</h3>
            <p>Accessible de partout, même en dehors de la classe.</p>
            <pre><code>&lt;?php
class <span class="class-name">Exemple</span> {
    <span class="keyword">public</span> <span class="variable">$attributPublic</span>;
}

<span class="variable">$obj</span> = <span class="keyword">new</span> <span class="class-name">Exemple</span>();
<span class="variable">$obj</span>->attributPublic = <span class="string">"Valeur"</span>; <span class="comment">// Accès direct autorisé</span></code></pre>
          </div>
          
          <div class="code-block">
            <h3 class="text-purple">Protégé</h3>
            <p>Accessible uniquement dans la classe et ses classes dérivées.</p>
            <pre><code>&lt;?php
class <span class="class-name">Exemple</span> {
    <span class="keyword">protected</span> <span class="variable">$attributProtege</span>;
}

class <span class="class-name">Enfant</span> <span class="keyword">extends</span> <span class="class-name">Exemple</span> {
    <span class="keyword">public</span> <span class="function">fonction</span>() {
        <span class="variable">$this</span>->attributProtege = <span class="string">"Valeur"</span>; <span class="comment">// Accès autorisé</span>
    }
}</code></pre>
          </div>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Privé</h3>
          <p>Accessible uniquement dans la classe qui les déclare.</p>
          <pre><code>&lt;?php
class <span class="class-name">Exemple</span> {
    <span class="keyword">private</span> <span class="variable">$attributPrive</span>;
    
    <span class="keyword">public</span> <span class="function">fonction</span>() {
        <span class="variable">$this</span>->attributPrive = <span class="string">"Valeur"</span>; <span class="comment">// Accès autorisé</span>
    }
}

<span class="variable">$obj</span> = <span class="keyword">new</span> <span class="class-name">Exemple</span>();
<span class="comment">// $obj->attributPrive = "Valeur"; // ERREUR: accès interdit</span></code></pre>
        </div>
      </section>

      <!-- Accès et modification des attributs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Accès et modification des attributs</h2>
        <p>Pour accéder et modifier les attributs d'un objet, on utilise l'opérateur <code>-></code>.</p>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple complet</h3>
          <pre><code>&lt;?php
class <span class="class-name">Voiture</span> {
    <span class="keyword">public</span> <span class="variable">$marque</span>;
    <span class="keyword">public</span> <span class="variable">$modele</span>;
    <span class="keyword">private</span> <span class="variable">$kilometrage</span> = <span class="number">0</span>;
    
    <span class="comment">// Méthode pour accéder à un attribut privé</span>
    <span class="keyword">public</span> <span class="function">getKilometrage</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->kilometrage;
    }
    
    <span class="comment">// Méthode pour modifier un attribut privé</span>
    <span class="keyword">public</span> <span class="function">ajouterKilometres</span>(<span class="variable">$km</span>) {
        <span class="variable">$this</span>->kilometrage += <span class="variable">$km</span>;
    }
}

<span class="comment">// Création d'un objet</span>
<span class="variable">$maVoiture</span> = <span class="keyword">new</span> <span class="class-name">Voiture</span>();

<span class="comment">// Accès aux attributs publics</span>
<span class="variable">$maVoiture</span>->marque = <span class="string">"Renault"</span>;
<span class="variable">$maVoiture</span>->modele = <span class="string">"Clio"</span>;

<span class="comment">// Modification d'un attribut privé via une méthode</span>
<span class="variable">$maVoiture</span>->ajouterKilometres(<span class="number">150</span>);

<span class="comment">// Affichage des valeurs</span>
<span class="function">echo</span> <span class="string">"Marque: "</span> . <span class="variable">$maVoiture</span>->marque . <span class="string">"&lt;br&gt;"</span>;
<span class="function">echo</span> <span class="string">"Modèle: "</span> . <span class="variable">$maVoiture</span>->modele . <span class="string">"&lt;br&gt;"</span>;
<span class="function">echo</span> <span class="string">"Kilométrage: "</span> . <span class="variable">$maVoiture</span>->getKilometrage() . <span class="string">" km"</span>;</code></pre>
        </div>
      </section>

      <!-- Attributs statiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Attributs statiques</h2>
        <p>Les attributs statiques appartiennent à la classe elle-même plutôt qu'aux instances. Ils sont partagés par toutes les instances de la classe.</p>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple d'attribut statique</h3>
          <pre><code>&lt;?php
class <span class="class-name">Compteur</span> {
    <span class="keyword">public</span> <span class="keyword">static</span> <span class="variable">$nombreInstances</span> = <span class="number">0</span>;
    
    <span class="keyword">public</span> <span class="function">__construct</span>() {
        <span class="comment">// Incrémenter le compteur à chaque nouvelle instance</span>
        <span class="keyword">self</span>::<span class="variable">$nombreInstances</span>++;
    }
    
    <span class="keyword">public</span> <span class="keyword">static</span> <span class="function">getNombreInstances</span>() {
        <span class="keyword">return</span> <span class="keyword">self</span>::<span class="variable">$nombreInstances</span>;
    }
}

<span class="comment">// Création d'instances</span>
<span class="variable">$obj1</span> = <span class="keyword">new</span> <span class="class-name">Compteur</span>();
<span class="variable">$obj2</span> = <span class="keyword">new</span> <span class="class-name">Compteur</span>();
<span class="variable">$obj3</span> = <span class="keyword">new</span> <span class="class-name">Compteur</span>();

<span class="comment">// Accès à l'attribut statique</span>
<span class="function">echo</span> <span class="string">"Nombre d'instances: "</span> . <span class="class-name">Compteur</span>::getNombreInstances(); <span class="comment">// Affiche 3</span></code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        <div class="exercise">
          <h3 class="text-purple">Création d'une classe "Livre"</h3>
          <p>Créez une classe <code>Livre</code> avec les attributs suivants :</p>
          <ul>
            <li><code>titre</code> (public)</li>
            <li><code>auteur</code> (public)</li>
            <li><code>prix</code> (privé)</li>
            <li><code>nombrePages</code> (protégé)</li>
          </ul>
          <p>Ajoutez des méthodes pour :</p>
          <ul>
            <li>Définir et obtenir le prix</li>
            <li>Définir et obtenir le nombre de pages</li>
            <li>Afficher toutes les informations du livre</li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code>&lt;?php
class <span class="class-name">Livre</span> {
    <span class="keyword">public</span> <span class="variable">$titre</span>;
    <span class="keyword">public</span> <span class="variable">$auteur</span>;
    <span class="keyword">private</span> <span class="variable">$prix</span>;
    <span class="keyword">protected</span> <span class="variable">$nombrePages</span>;
    
    <span class="comment">// Constructeur</span>
    <span class="keyword">public</span> <span class="function">__construct</span>(<span class="variable">$titre</span>, <span class="variable">$auteur</span>) {
        <span class="variable">$this</span>->titre = <span class="variable">$titre</span>;
        <span class="variable">$this</span>->auteur = <span class="variable">$auteur</span>;
    }
    
    <span class="comment">// Getters et setters pour l'attribut privé $prix</span>
    <span class="keyword">public</span> <span class="function">setPrix</span>(<span class="variable">$prix</span>) {
        <span class="keyword">if</span> (<span class="variable">$prix</span> >= <span class="number">0</span>) {
            <span class="variable">$this</span>->prix = <span class="variable">$prix</span>;
        }
    }
    
    <span class="keyword">public</span> <span class="function">getPrix</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->prix;
    }
    
    <span class="comment">// Getters et setters pour l'attribut protégé $nombrePages</span>
    <span class="keyword">public</span> <span class="function">setNombrePages</span>(<span class="variable">$pages</span>) {
        <span class="keyword">if</span> (<span class="variable">$pages</span> > <span class="number">0</span>) {
            <span class="variable">$this</span>->nombrePages = <span class="variable">$pages</span>;
        }
    }
    
    <span class="keyword">public</span> <span class="function">getNombrePages</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->nombrePages;
    }
    
    <span class="comment">// Méthode pour afficher les informations</span>
    <span class="keyword">public</span> <span class="function">afficherInfos</span>() {
        <span class="function">echo</span> <span class="string">"Titre: "</span> . <span class="variable">$this</span>->titre . <span class="string">"&lt;br&gt;"</span>;
        <span class="function">echo</span> <span class="string">"Auteur: "</span> . <span class="variable">$this</span>->auteur . <span class="string">"&lt;br&gt;"</span>;
        <span class="function">echo</span> <span class="string">"Prix: "</span> . <span class="variable">$this</span>->getPrix() . <span class="string">" €&lt;br&gt;"</span>;
        <span class="function">echo</span> <span class="string">"Nombre de pages: "</span> . <span class="variable">$this</span>->getNombrePages() . <span class="string">"&lt;br&gt;"</span>;
    }
}

<span class="comment">// Utilisation de la classe</span>
<span class="variable">$monLivre</span> = <span class="keyword">new</span> <span class="class-name">Livre</span>(<span class="string">"Le Petit Prince"</span>, <span class="string">"Antoine de Saint-Exupéry"</span>);
<span class="variable">$monLivre</span>->setPrix(<span class="number">12.50</span>);
<span class="variable">$monLivre</span>->setNombrePages(<span class="number">96</span>);
<span class="variable">$monLivre</span>->afficherInfos();</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary text-white">
        <h2>Conclusion</h2>
        <div class="textExemple">
          <p>Dans cette leçon, nous avons exploré les concepts fondamentaux des attributs de classe en PHP :</p>
          <ul>
            <li>Les attributs définissent l'état et les caractéristiques d'un objet</li>
            <li>Les niveaux de visibilité (<code>public</code>, <code>protected</code>, <code>private</code>) contrôlent l'accès aux données</li>
            <li>L'encapsulation permet de protéger les données internes via des méthodes d'accès</li>
            <li>Les attributs statiques sont partagés entre toutes les instances d'une classe</li>
          </ul>
          <p>La maîtrise des attributs est essentielle pour créer des classes robustes et maintenables en programmation orientée objet. En appliquant les bonnes pratiques d'encapsulation, vous créerez un code plus sécurisé et plus facile à faire évoluer.</p>
          <p>Ces connaissances vous serviront de base solide pour aborder des concepts plus avancés de la POO en PHP comme l'héritage, le polymorphisme et les interfaces.</p>
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