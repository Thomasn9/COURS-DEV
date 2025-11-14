<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <div class="lesson-header">
        <h1 class="text-white">Test Driven Development (TDD)</h1>
        <p class="lesson-meta text-white">Développement piloté par les tests</p>
      </div>

      <!-- Introduction -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction au TDD</h2>
        <p class="textExemple">
          Le Test Driven Development (TDD) est une méthode de développement logiciel qui consiste à écrire les tests avant d'écrire le code fonctionnel. 
          Cette approche permet de concevoir des logiciels plus robustes, maintenables et testables.
        </p>
        <p class="textExemple">
          Le TDD suit un cycle en trois étapes, souvent appelé le cycle "Red-Green-Refactor" :
        </p>
        <ul class="textExemple">
          <li><strong>Red</strong> : Écrire un test qui échoue</li>
          <li><strong>Green</strong> : Écrire le code minimal pour faire passer le test</li>
          <li><strong>Refactor</strong> : Améliorer le code tout en maintenant les tests verts</li>
        </ul>
      </div>

      <!-- Les trois lois du TDD -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les trois lois du TDD</h2>
        <p class="textExemple">
          Selon Robert C. Martin (Uncle Bob), le TDD repose sur trois lois fondamentales :
        </p>
        <ol class="textExemple">
          <li>Vous ne devez pas écrire de code de production tant que vous n'avez pas écrit un test qui échoue</li>
          <li>Vous ne devez pas écrire plus d'un test que nécessaire pour échouer, ou ne pas compiler</li>
          <li>Vous ne devez pas écrire plus de code de production que nécessaire pour passer le test qui échoue actuellement</li>
        </ol>
      </div>

      <!-- Le cycle Red-Green-Refactor -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Le cycle Red-Green-Refactor</h2>
        
        <h3 class="text-purple">Étape 1: Red - Écrire un test qui échoue</h3>
        <p class="textExemple">
          Dans cette première étape, nous écrivons un test unitaire pour une fonctionnalité que nous souhaitons implémenter. 
          Ce test doit échouer car la fonctionnalité n'existe pas encore.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Exemple : Test pour une fonction d'addition</h4>
          <pre><code class="javascript">// test/addition.test.js
<span class="keyword">const</span> <span class="variable">add</span> = <span class="function">require</span>(<span class="string">'../src/addition'</span>);

<span class="function">describe</span>(<span class="string">'Addition function'</span>, () => {
  <span class="function">test</span>(<span class="string">'adds 1 + 2 to equal 3'</span>, () => {
    <span class="function">expect</span>(<span class="function">add</span>(<span class="number">1</span>, <span class="number">2</span>)).<span class="function">toBe</span>(<span class="number">3</span>);
  });
});</code></pre>
        </div>

        <h3 class="text-purple">Étape 2: Green - Faire passer le test</h3>
        <p class="textExemple">
          Dans cette étape, nous écrivons le code minimal nécessaire pour faire passer le test. 
          L'objectif n'est pas d'écrire un code parfait, mais simplement de satisfaire le test.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Exemple : Implémentation minimale</h4>
          <pre><code class="javascript">// src/addition.js
<span class="keyword">function</span> <span class="function">add</span>(a, b) {
  <span class="keyword">return</span> <span class="number">3</span>; <span class="comment">// Solution minimale pour passer le test</span>
}

<span class="variable">module</span>.<span class="variable">exports</span> = add;</code></pre>
        </div>

        <h3 class="text-purple">Étape 3: Refactor - Améliorer le code</h3>
        <p class="textExemple">
          Une fois le test passé, nous pouvons améliorer le code en le rendant plus propre, plus efficace ou plus générique, 
          tout en nous assurant que tous les tests continuent de passer.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple">Exemple : Code refactorisé</h4>
          <pre><code class="javascript">// src/addition.js
<span class="keyword">function</span> <span class="function">add</span>(a, b) {
  <span class="keyword">return</span> a + b; <span class="comment">// Solution générique</span>
}

<span class="variable">module</span>.<span class="variable">exports</span> = add;</code></pre>
        </div>
      </div>

      <!-- Avantages du TDD -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Avantages du TDD</h2>
        <ul class="textExemple">
          <li><strong>Code plus robuste</strong> : Les tests couvrent le code dès le début</li>
          <li><strong>Meilleure conception</strong> : Le code est conçu pour être testable</li>
          <li><strong>Documentation vivante</strong> : Les tests servent de documentation</li>
          <li><strong>Réduction des bugs</strong> : Les régressions sont détectées rapidement</li>
          <li><strong>Refactoring sécurisé</strong> : Possibilité de refactoriser en confiance</li>
        </ul>
      </div>

      <!-- Exemple complet -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple complet : Calculatrice</h2>
        <p class="textExemple">
          Voyons un exemple plus complet avec une calculatrice simple.
        </p>

        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Tests</h4>
            <pre><code class="javascript"><span class="comment">// test/calculator.test.js</span>
<span class="keyword">const</span> <span class="variable">Calculator</span> = <span class="function">require</span>(<span class="string">'../src/calculator'</span>);

<span class="function">describe</span>(<span class="string">'Calculator'</span>, () => {
  <span class="keyword">let</span> calculator;

  <span class="function">beforeEach</span>(() => {
    calculator = <span class="keyword">new</span> <span class="class-name">Calculator</span>();
  });

  <span class="function">test</span>(<span class="string">'should add two numbers'</span>, () => {
    <span class="function">expect</span>(calculator.<span class="function">add</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">5</span>);
  });

  <span class="function">test</span>(<span class="string">'should subtract two numbers'</span>, () => {
    <span class="function">expect</span>(calculator.<span class="function">subtract</span>(<span class="number">5</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">2</span>);
  });

  <span class="function">test</span>(<span class="string">'should multiply two numbers'</span>, () => {
    <span class="function">expect</span>(calculator.<span class="function">multiply</span>(<span class="number">4</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">12</span>);
  });

  <span class="function">test</span>(<span class="string">'should divide two numbers'</span>, () => {
    <span class="function">expect</span>(calculator.<span class="function">divide</span>(<span class="number">10</span>, <span class="number">2</span>)).<span class="function">toBe</span>(<span class="number">5</span>);
  });

  <span class="function">test</span>(<span class="string">'should throw error when dividing by zero'</span>, () => {
    <span class="function">expect</span>(() => calculator.<span class="function">divide</span>(<span class="number">10</span>, <span class="number">0</span>)).<span class="function">toThrow</span>(<span class="string">'Division by zero'</span>);
  });
});</code></pre>
          </div>
          <div>
            <h4 class="text-purple">Implémentation</h4>
            <pre><code class="javascript"><span class="comment">// src/calculator.js</span>
<span class="keyword">class</span> <span class="class-name">Calculator</span> {
  <span class="function">add</span>(a, b) {
    <span class="keyword">return</span> a + b;
  }

  <span class="function">subtract</span>(a, b) {
    <span class="keyword">return</span> a - b;
  }

  <span class="function">multiply</span>(a, b) {
    <span class="keyword">return</span> a * b;
  }

  <span class="function">divide</span>(a, b) {
    <span class="keyword">if</span> (b === <span class="number">0</span>) {
      <span class="keyword">throw</span> <span class="keyword">new</span> <span class="class-name">Error</span>(<span class="string">'Division by zero'</span>);
    }
    <span class="keyword">return</span> a / b;
  }
}

<span class="variable">module</span>.<span class="variable">exports</span> = Calculator;</code></pre>
          </div>
        </div>
      </div>

      <!-- Bonnes pratiques -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques du TDD</h2>
        <ul class="textExemple">
          <li><strong>Tests rapides</strong> : Les tests doivent s'exécuter rapidement</li>
          <li><strong>Tests indépendants</strong> : Chaque test doit être indépendant des autres</li>
          <li><strong>Nommage explicite</strong> : Les noms des tests doivent décrire clairement leur intention</li>
          <li><strong>Un seul concept par test</strong> : Évitez les tests qui vérifient plusieurs choses</li>
          <li><strong>Tests FIRST</strong> :
            <ul>
              <li><strong>F</strong>ast (Rapide)</li>
              <li><strong>I</strong>ndependent (Indépendant)</li>
              <li><strong>R</strong>epeatable (Répétable)</li>
              <li><strong>S</strong>elf-validating (Auto-validant)</li>
              <li><strong>T</strong>imely (Opportun)</li>
            </ul>
          </li>
        </ul>
      </div>

      <!-- Exercice pratique -->
      <div class="lesson-section bg-light-purple border-purple exercise">
        <h2 class="text-purple">Exercice pratique</h2>
        <p class="textExemple">
          Implémentez une classe <code>StringUtils</code> avec les méthodes suivantes en utilisant l'approche TDD :
        </p>
        <ul class="textExemple">
          <li><code>reverse(str)</code> : inverse une chaîne de caractères</li>
          <li><code>isPalindrome(str)</code> : vérifie si une chaîne est un palindrome</li>
          <li><code>countVowels(str)</code> : compte le nombre de voyelles dans une chaîne</li>
        </ul>

        <details class="solution">
          <summary class="btn-purple btn-hover">Voir la solution</summary>
          <div class="solution-content">
            <h4 class="text-purple">Tests</h4>
            <pre><code class="javascript"><span class="comment">// test/stringUtils.test.js</span>
<span class="keyword">const</span> <span class="variable">StringUtils</span> = <span class="function">require</span>(<span class="string">'../src/stringUtils'</span>);

<span class="function">describe</span>(<span class="string">'StringUtils'</span>, () => {
  <span class="keyword">let</span> stringUtils;

  <span class="function">beforeEach</span>(() => {
    stringUtils = <span class="keyword">new</span> <span class="class-name">StringUtils</span>();
  });

  <span class="function">test</span>(<span class="string">'should reverse a string'</span>, () => {
    <span class="function">expect</span>(stringUtils.<span class="function">reverse</span>(<span class="string">'hello'</span>)).<span class="function">toBe</span>(<span class="string">'olleh'</span>);
  });

  <span class="function">test</span>(<span class="string">'should check if string is palindrome'</span>, () => {
    <span class="function">expect</span>(stringUtils.<span class="function">isPalindrome</span>(<span class="string">'radar'</span>)).<span class="function">toBe</span>(<span class="keyword">true</span>);
    <span class="function">expect</span>(stringUtils.<span class="function">isPalindrome</span>(<span class="string">'hello'</span>)).<span class="function">toBe</span>(<span class="keyword">false</span>);
  });

  <span class="function">test</span>(<span class="string">'should count vowels in a string'</span>, () => {
    <span class="function">expect</span>(stringUtils.<span class="function">countVowels</span>(<span class="string">'Hello World'</span>)).<span class="function">toBe</span>(<span class="number">3</span>);
  });
});</code></pre>

            <h4 class="text-purple">Implémentation</h4>
            <pre><code class="javascript"><span class="comment">// src/stringUtils.js</span>
<span class="keyword">class</span> <span class="class-name">StringUtils</span> {
  <span class="function">reverse</span>(str) {
    <span class="keyword">return</span> str.<span class="function">split</span>(<span class="string">''</span>).<span class="function">reverse</span>().<span class="function">join</span>(<span class="string">''</span>);
  }

  <span class="function">isPalindrome</span>(str) {
    <span class="keyword">const</span> reversed = <span class="keyword">this</span>.<span class="function">reverse</span>(str);
    <span class="keyword">return</span> str === reversed;
  }

  <span class="function">countVowels</span>(str) {
    <span class="keyword">const</span> vowels = str.<span class="function">match</span>(<span class="regex">/[aeiou]/gi</span>);
    <span class="keyword">return</span> vowels ? vowels.<span class="variable">length</span> : <span class="number">0</span>;
  }
}

<span class="variable">module</span>.<span class="variable">exports</span> = StringUtils;</code></pre>
          </div>
        </details>
      </div>

      <!-- Conclusion -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          Le TDD est une pratique puissante qui transforme la façon dont nous développons des logiciels. 
          Bien qu'il puisse sembler contre-intuitif au début, il offre de nombreux avantages à long terme :
        </p>
        <ul class="textExemple">
          <li>Réduction du temps de débogage</li>
          <li>Amélioration de la qualité du code</li>
          <li>Facilitation des refactorisations</li>
          <li>Documentation vivante et à jour</li>
          <li>Confiance accrue lors des déploiements</li>
        </ul>
        <p class="textExemple">
          Comme toute compétence, le TDD nécessite de la pratique pour être maîtrisé. 
          Commencez par de petits projets et augmentez progressivement la complexité.
        </p>
      </div>

      <!-- Ressources supplémentaires -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Ressources supplémentaires</h2>
        <ul class="textExemple">
          <li>Livre : "Test-Driven Development: By Example" de Kent Beck</li>
          <li>Livre : "Clean Code" de Robert C. Martin</li>
          <li>Framework de test : Jest (JavaScript)</li>
          <li>Framework de test : PHPUnit (PHP)</li>
          <li>Framework de test : JUnit (Java)</li>
        </ul>
        <a href="#" class="btn-purple btn-hover">Voir d'autres leçons</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TDDLesson',
  // Vous pouvez ajouter des métadonnées SEO ici si nécessaire
  head() {
    return {
      title: 'TDD - Test Driven Development',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez le Test Driven Development (TDD) avec cette leçon complète incluant des exemples pratiques et des exercices.'
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