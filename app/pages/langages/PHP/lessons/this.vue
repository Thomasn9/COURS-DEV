<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">$this en POO PHP</h1>
        <p class="lesson-meta text-white">Programmation Orientée Objet - Référence à l'objet courant</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction à $this</h2>
        <p class="textExemple">
          En PHP orienté objet, <code>$this</code> est une variable spéciale qui fait référence à l'objet courant. 
          Elle est utilisée à l'intérieur des méthodes d'une classe pour accéder aux propriétés et méthodes de cet objet.
        </p>
        <p class="textExemple">
          <code>$this</code> n'est disponible que dans le contexte d'une méthode d'objet (non statique) et ne peut pas être utilisée 
          en dehors d'une classe ou dans des méthodes statiques.
        </p>
      </section>

      <!-- Utilisation de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Utilisation de base</h2>
        <p class="textExemple">
          Voici un exemple simple montrant comment utiliser <code>$this</code> pour accéder aux propriétés d'une classe :
        </p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">Personne</span> {
    <span class="keyword">public</span> <span class="variable">$nom</span>;
    <span class="keyword">public</span> <span class="variable">$age</span>;
    
    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$nom</span>, <span class="variable">$age</span>) {
        <span class="variable">$this</span>-&gt;nom = <span class="variable">$nom</span>;
        <span class="variable">$this</span>-&gt;age = <span class="variable">$age</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">sePresenter</span>() {
        <span class="keyword">echo</span> <span class="string">"Je m'appelle "</span> . <span class="variable">$this</span>-&gt;nom . <span class="string">" et j'ai "</span> . <span class="variable">$this</span>-&gt;age . <span class="string">" ans."</span>;
    }
}

<span class="variable">$personne</span> = <span class="keyword">new</span> <span class="class-name">Personne</span>(<span class="string">"Alice"</span>, <span class="number">25</span>);
<span class="variable">$personne</span>-&gt;sePresenter();
<span class="comment">// Affiche : Je m'appelle Alice et j'ai 25 ans.</span></code></pre>
        </div>
      </section>

      <!-- Accès aux méthodes -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Accès aux méthodes avec $this</h2>
        <p class="textExemple">
          <code>$this</code> peut également être utilisé pour appeler d'autres méthodes de la même classe :
        </p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">Calculatrice</span> {
    <span class="keyword">private</span> <span class="variable">$resultat</span> = <span class="number">0</span>;
    
    <span class="keyword">public function</span> <span class="function">additionner</span>(<span class="variable">$valeur</span>) {
        <span class="variable">$this</span>-&gt;resultat += <span class="variable">$valeur</span>;
        <span class="keyword">return</span> <span class="variable">$this</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">multiplier</span>(<span class="variable">$valeur</span>) {
        <span class="variable">$this</span>-&gt;resultat *= <span class="variable">$valeur</span>;
        <span class="keyword">return</span> <span class="variable">$this</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">afficher</span>() {
        <span class="keyword">echo</span> <span class="string">"Résultat : "</span> . <span class="variable">$this</span>-&gt;resultat;
    }
    
    <span class="keyword">public function</span> <span class="function">calculer</span>(<span class="variable">$a</span>, <span class="variable">$b</span>) {
        <span class="variable">$this</span>-&gt;additionner(<span class="variable">$a</span>)-&gt;multiplier(<span class="variable">$b</span>)-&gt;afficher();
    }
}

<span class="variable">$calc</span> = <span class="keyword">new</span> <span class="class-name">Calculatrice</span>();
<span class="variable">$calc</span>-&gt;calculer(<span class="number">5</span>, <span class="number">3</span>);
<span class="comment">// Affiche : Résultat : 15</span></code></pre>
        </div>
      </section>

      <!-- Méthodes chaînables -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Méthodes chaînables avec $this</h2>
        <p class="textExemple">
          En retournant <code>$this</code> dans une méthode, vous pouvez créer des appels de méthodes chaînés (method chaining) :
        </p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">QueryBuilder</span> {
    <span class="keyword">private</span> <span class="variable">$table</span>;
    <span class="keyword">private</span> <span class="variable">$conditions</span> = [];
    
    <span class="keyword">public function</span> <span class="function">table</span>(<span class="variable">$table</span>) {
        <span class="variable">$this</span>-&gt;table = <span class="variable">$table</span>;
        <span class="keyword">return</span> <span class="variable">$this</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">where</span>(<span class="variable">$colonne</span>, <span class="variable">$valeur</span>) {
        <span class="variable">$this</span>-&gt;conditions[] = <span class="string">"<span class="variable">$colonne</span> = '<span class="variable">$valeur</span>'"</span>;
        <span class="keyword">return</span> <span class="variable">$this</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">get</span>() {
        <span class="variable">$sql</span> = <span class="string">"SELECT * FROM <span class="variable">$this</span>-&gt;table"</span>;
        <span class="keyword">if</span> (!<span class="function">empty</span>(<span class="variable">$this</span>-&gt;conditions)) {
            <span class="variable">$sql</span> .= <span class="string">" WHERE "</span> . <span class="function">implode</span>(<span class="string">" AND "</span>, <span class="variable">$this</span>-&gt;conditions);
        }
        <span class="keyword">return</span> <span class="variable">$sql</span>;
    }
}

<span class="variable">$query</span> = <span class="keyword">new</span> <span class="class-name">QueryBuilder</span>();
<span class="variable">$sql</span> = <span class="variable">$query</span>-&gt;table(<span class="string">"utilisateurs"</span>)
               -&gt;where(<span class="string">"age"</span>, <span class="number">25</span>)
               -&gt;where(<span class="string">"ville"</span>, <span class="string">"Paris"</span>)
               -&gt;get();
               
<span class="keyword">echo</span> <span class="variable">$sql</span>;
<span class="comment">// Affiche : SELECT * FROM utilisateurs WHERE age = '25' AND ville = 'Paris'</span></code></pre>
        </div>
      </section>

      <!-- Différences avec self et static -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">$this vs self vs static</h2>
        <p class="textExemple">
          Il est important de comprendre la différence entre <code>$this</code>, <code>self</code> et <code>static</code> :
        </p>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">$this</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">ParentClass</span> {
    <span class="keyword">public function</span> <span class="function">testThis</span>() {
        <span class="keyword">return</span> <span class="function">get_class</span>(<span class="variable">$this</span>);
    }
}

<span class="keyword">class</span> <span class="class-name">ChildClass</span> <span class="keyword">extends</span> <span class="class-name">ParentClass</span> {}

<span class="variable">$obj</span> = <span class="keyword">new</span> <span class="class-name">ChildClass</span>();
<span class="keyword">echo</span> <span class="variable">$obj</span>-&gt;testThis();
<span class="comment">// Affiche : ChildClass</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">self</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">ParentClass</span> {
    <span class="keyword">public static function</span> <span class="function">testSelf</span>() {
        <span class="keyword">return</span> <span class="class-name">__CLASS__</span>;
    }
}

<span class="keyword">class</span> <span class="class-name">ChildClass</span> <span class="keyword">extends</span> <span class="class-name">ParentClass</span> {}

<span class="keyword">echo</span> <span class="class-name">ChildClass</span>::testSelf();
<span class="comment">// Affiche : ParentClass</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Cas d'erreurs courantes -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Erreurs courantes avec $this</h2>
        <p class="textExemple">
          Voici quelques erreurs fréquentes lors de l'utilisation de <code>$this</code> :
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Utilisation dans une méthode statique</h4>
          <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">MauvaiseClasse</span> {
    <span class="keyword">public static function</span> <span class="function">methodeStatique</span>() {
        <span class="comment">// ERREUR : $this ne peut pas être utilisé dans une méthode statique</span>
        <span class="variable">$this</span>-&gt;propriete = <span class="string">"valeur"</span>;
    }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple">Utilisation en dehors d'une classe</h4>
          <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// ERREUR : $this ne peut pas être utilisé en dehors d'une classe</span>
<span class="variable">$this</span>-&gt;variable = <span class="string">"test"</span>;</code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        <div class="exercise">
          <p class="textExemple">
            <strong>Objectif :</strong> Créez une classe <code>CompteBancaire</code> avec les fonctionnalités suivantes :
          </p>
          <ul class="textExemple">
            <li>Propriétés : <code>$titulaire</code>, <code>$solde</code></li>
            <li>Méthodes : 
              <ul>
                <li><code>deposer($montant)</code> - ajoute un montant au solde</li>
                <li><code>retirer($montant)</code> - retire un montant du solde (si le solde est suffisant)</li>
                <li><code>getSolde()</code> - retourne le solde actuel</li>
                <li><code>virerVers($compte, $montant)</code> - transfère un montant vers un autre compte</li>
              </ul>
            </li>
          </ul>
          <p class="textExemple">
            Utilisez <code>$this</code> pour accéder aux propriétés et méthodes de la classe.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">CompteBancaire</span> {
    <span class="keyword">private</span> <span class="variable">$titulaire</span>;
    <span class="keyword">private</span> <span class="variable">$solde</span>;
    
    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$titulaire</span>, <span class="variable">$soldeInitial</span> = <span class="number">0</span>) {
        <span class="variable">$this</span>-&gt;titulaire = <span class="variable">$titulaire</span>;
        <span class="variable">$this</span>-&gt;solde = <span class="variable">$soldeInitial</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">deposer</span>(<span class="variable">$montant</span>) {
        <span class="keyword">if</span> (<span class="variable">$montant</span> &gt; <span class="number">0</span>) {
            <span class="variable">$this</span>-&gt;solde += <span class="variable">$montant</span>;
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">retirer</span>(<span class="variable">$montant</span>) {
        <span class="keyword">if</span> (<span class="variable">$montant</span> &gt; <span class="number">0</span> <span class="operator">&amp;&amp;</span> <span class="variable">$this</span>-&gt;solde &gt;= <span class="variable">$montant</span>) {
            <span class="variable">$this</span>-&gt;solde -= <span class="variable">$montant</span>;
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }
    
    <span class="keyword">public function</span> <span class="function">getSolde</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;solde;
    }
    
    <span class="keyword">public function</span> <span class="function">virerVers</span>(<span class="class-name">CompteBancaire</span> <span class="variable">$compte</span>, <span class="variable">$montant</span>) {
        <span class="keyword">if</span> (<span class="variable">$this</span>-&gt;retirer(<span class="variable">$montant</span>)) {
            <span class="variable">$compte</span>-&gt;deposer(<span class="variable">$montant</span>);
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }
}

<span class="comment">// Test de la classe</span>
<span class="variable">$compte1</span> = <span class="keyword">new</span> <span class="class-name">CompteBancaire</span>(<span class="string">"Alice"</span>, <span class="number">1000</span>);
<span class="variable">$compte2</span> = <span class="keyword">new</span> <span class="class-name">CompteBancaire</span>(<span class="string">"Bob"</span>, <span class="number">500</span>);

<span class="variable">$compte1</span>-&gt;virerVers(<span class="variable">$compte2</span>, <span class="number">200</span>);

<span class="keyword">echo</span> <span class="string">"Solde compte1: "</span> . <span class="variable">$compte1</span>-&gt;getSolde() . <span class="string">"<span class="operator">&lt;</span>br<span class="operator">&gt;</span>"</span>;
<span class="keyword">echo</span> <span class="string">"Solde compte2: "</span> . <span class="variable">$compte2</span>-&gt;getSolde();
<span class="comment">// Affiche: Solde compte1: 800</span>
<span class="comment">//         Solde compte2: 700</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Résumé -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Résumé</h2>
        <div class="text-white">
          <ul>
            <li><code>$this</code> fait référence à l'objet courant dans une classe</li>
            <li>Il est utilisé pour accéder aux propriétés et méthodes de l'objet</li>
            <li>Il ne peut être utilisé que dans des méthodes non statiques</li>
            <li>Retourner <code>$this</code> permet de créer des méthodes chaînables</li>
            <li><code>$this</code> est différent de <code>self</code> et <code>static</code></li>
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