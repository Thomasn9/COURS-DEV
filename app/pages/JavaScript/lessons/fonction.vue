<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Fonctions en JavaScript</h1>
        <p class="lesson-meta text-white">Apprenez à créer et utiliser des fonctions en JavaScript</p>
        <p class="lesson-meta text-white">
                    <span>Niveau : Débutant</span>
                </p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Fonctions</h2>
        <p class="textExemple">
          Une fonction en JavaScript est un bloc de code conçu pour effectuer une tâche particulière. 
          Elle est exécutée lorsqu'elle est "appelée" (invoked). Les fonctions sont essentielles pour 
          organiser, réutiliser et maintenir votre code.
        </p>
      </section>

      <!-- Déclaration de fonctions -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Déclaration de Fonctions</h2>
        <p class="textExemple">
          Il existe plusieurs façons de déclarer une fonction en JavaScript :
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">1. Déclaration de fonction</h4>
            <pre><code><span class="keyword">function</span> <span class="function">saluer</span>(<span class="variable">nom</span>) {
  <span class="keyword">return</span> <span class="string">"Bonjour "</span> + <span class="variable">nom</span> + <span class="string">"!"</span>;
}

<span class="comment">// Appel de la fonction</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">saluer</span>(<span class="string">"Alice"</span>)); <span class="comment">// "Bonjour Alice!"</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">2. Expression de fonction</h4>
            <pre><code><span class="comment">// Expression de fonction</span>
<span class="keyword">const</span> <span class="variable">saluer</span> = <span class="keyword">function</span>(<span class="variable">nom</span>) {
  <span class="keyword">return</span> <span class="string">"Bonjour "</span> + <span class="variable">nom</span> + <span class="string">"!"</span>;
};

<span class="comment">// Appel de la fonction</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">saluer</span>(<span class="string">"Bob"</span>)); <span class="comment">// "Bonjour Bob!"</span></code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">3. Fonction fléchée (ES6)</h4>
            <pre><code><span class="comment">// Fonction fléchée</span>
<span class="keyword">const</span> <span class="variable">saluer</span> = (<span class="variable">nom</span>) <span class="operator">=></span> {
  <span class="keyword">return</span> <span class="string">"Bonjour "</span> + <span class="variable">nom</span> + <span class="string">"!"</span>;
};

<span class="comment">// Version simplifiée (retour implicite)</span>
<span class="keyword">const</span> <span class="variable">saluerSimple</span> = <span class="variable">nom</span> <span class="operator">=></span> <span class="string">"Bonjour "</span> + <span class="variable">nom</span> + <span class="string">"!"</span>;

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">saluerSimple</span>(<span class="string">"Charlie"</span>)); <span class="comment">// "Bonjour Charlie!"</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">4. Fonction constructeur</h4>
            <pre><code><span class="comment">// Fonction constructeur (moins utilisée aujourd'hui)</span>
<span class="keyword">const</span> <span class="variable">saluer</span> = <span class="keyword">new</span> <span class="class-name">Function</span>(<span class="string">"nom"</span>, <span class="string">"return 'Bonjour ' + nom + '!'"</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">saluer</span>(<span class="string">"David"</span>)); <span class="comment">// "Bonjour David!"</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Paramètres et arguments -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Paramètres et Arguments</h2>
        <p class="textExemple">
          Les fonctions peuvent recevoir des paramètres (définis lors de la déclaration) 
          et des arguments (valeurs passées lors de l'appel).
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Fonction avec paramètres</span>
<span class="keyword">function</span> <span class="function">calculerPrix</span>(<span class="variable">prixHT</span>, <span class="variable">tauxTVA</span> = <span class="number">20</span>) {
  <span class="comment">// tauxTVA a une valeur par défaut de 20</span>
  <span class="keyword">return</span> <span class="variable">prixHT</span> + (<span class="variable">prixHT</span> * <span class="variable">tauxTVA</span> / <span class="number">100</span>);
}

<span class="comment">// Appels avec différents arguments</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">calculerPrix</span>(<span class="number">100</span>));      <span class="comment">// 120 (utilise la valeur par défaut)</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">calculerPrix</span>(<span class="number">100</span>, <span class="number">10</span>));  <span class="comment">// 110</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">calculerPrix</span>(<span class="number">100</span>, <span class="number">5.5</span>)); <span class="comment">// 105.5</span></code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Paramètres REST</h4>
          <pre><code><span class="comment">// Fonction avec paramètres REST</span>
<span class="keyword">function</span> <span class="function">additionner</span>(...<span class="variable">nombres</span>) {
  <span class="keyword">let</span> <span class="variable">total</span> = <span class="number">0</span>;
  <span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">nombre</span> <span class="keyword">of</span> <span class="variable">nombres</span>) {
    <span class="variable">total</span> += <span class="variable">nombre</span>;
  }
  <span class="keyword">return</span> <span class="variable">total</span>;
}

<span class="function">console</span>.<span class="function">log</span>(<span class="function">additionner</span>(<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>));        <span class="comment">// 6</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">additionner</span>(<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>));  <span class="comment">// 15</span></code></pre>
        </div>
      </section>

      <!-- Retour de valeurs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Retour de Valeurs</h2>
        <p class="textExemple">
          Les fonctions peuvent retourner des valeurs avec l'instruction <code>return</code>. 
          Si aucune valeur n'est retournée, la fonction renvoie <code>undefined</code>.
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Fonction avec retour</span>
<span class="keyword">function</span> <span class="function">estMajeur</span>(<span class="variable">age</span>) {
  <span class="keyword">if</span> (<span class="variable">age</span> >= <span class="number">18</span>) {
    <span class="keyword">return</span> <span class="keyword">true</span>;
  } <span class="keyword">else</span> {
    <span class="keyword">return</span> <span class="keyword">false</span>;
  }
}

<span class="comment">// Fonction sans retour explicite</span>
<span class="keyword">function</span> <span class="function">afficherMessage</span>(<span class="variable">message</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">message</span>);
  <span class="comment">// Pas de return -> retourne undefined</span>
}

<span class="keyword">const</span> <span class="variable">resultat</span> = <span class="function">estMajeur</span>(<span class="number">20</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">resultat</span>); <span class="comment">// true</span>

<span class="keyword">const</span> <span class="variable">autreResultat</span> = <span class="function">afficherMessage</span>(<span class="string">"Hello!"</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">autreResultat</span>); <span class="comment">// undefined</span></code></pre>
        </div>
      </section>

      <!-- Portée des variables -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Portée des Variables</h2>
        <p class="textExemple">
          Les variables déclarées dans une fonction ont une portée locale (ne sont accessibles 
          qu'à l'intérieur de la fonction), tandis que les variables déclarées en dehors ont 
          une portée globale.
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Variable globale</span>
<span class="keyword">let</span> <span class="variable">compteurGlobal</span> = <span class="number">0</span>;

<span class="keyword">function</span> <span class="function">incrementerCompteur</span>() {
  <span class="comment">// Variable locale</span>
  <span class="keyword">let</span> <span class="variable">compteurLocal</span> = <span class="number">0</span>;
  <span class="variable">compteurLocal</span><span class="operator">++</span>;
  <span class="variable">compteurGlobal</span><span class="operator">++</span>;
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">"Local: "</span> + <span class="variable">compteurLocal</span>); <span class="comment">// Augmente à chaque appel</span>
}

<span class="function">incrementerCompteur</span>(); <span class="comment">// Local: 1, Global: 1</span>
<span class="function">incrementerCompteur</span>(); <span class="comment">// Local: 1, Global: 2</span>
<span class="function">incrementerCompteur</span>(); <span class="comment">// Local: 1, Global: 3</span>

<span class="comment">// console.log(compteurLocal); // Erreur: compteurLocal n'est pas défini</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">compteurGlobal</span>); <span class="comment">// 3</span></code></pre>
        </div>
      </section>

      <!-- Fonctions d'ordre supérieur -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Fonctions d'Ordre Supérieur</h2>
        <p class="textExemple">
          Les fonctions d'ordre supérieur sont des fonctions qui prennent d'autres fonctions 
          en paramètre ou qui retournent une fonction.
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Fonction qui prend une fonction en paramètre</span>
<span class="keyword">function</span> <span class="function">appliquerOperation</span>(<span class="variable">nombres</span>, <span class="variable">operation</span>) {
  <span class="keyword">const</span> <span class="variable">resultats</span> = [];
  <span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">nombre</span> <span class="keyword">of</span> <span class="variable">nombres</span>) {
    <span class="variable">resultats</span>.<span class="function">push</span>(<span class="function">operation</span>(<span class="variable">nombre</span>));
  }
  <span class="keyword">return</span> <span class="variable">resultats</span>;
}

<span class="comment">// Fonctions à passer en paramètre</span>
<span class="keyword">function</span> <span class="function">doubler</span>(<span class="variable">x</span>) { <span class="keyword">return</span> <span class="variable">x</span> * <span class="number">2</span>; }
<span class="keyword">function</span> <span class="function">carre</span>(<span class="variable">x</span>) { <span class="keyword">return</span> <span class="variable">x</span> * <span class="variable">x</span>; }

<span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];
<span class="function">console</span>.<span class="function">log</span>(<span class="function">appliquerOperation</span>(<span class="variable">nombres</span>, <span class="variable">doubler</span>)); <span class="comment">// [2, 4, 6, 8, 10]</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">appliquerOperation</span>(<span class="variable">nombres</span>, <span class="variable">carre</span>));   <span class="comment">// [1, 4, 9, 16, 25]</span></code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Fonction qui retourne une fonction</h4>
          <pre><code><span class="comment">// Fonction qui retourne une fonction</span>
<span class="keyword">function</span> <span class="function">creerMultiplicateur</span>(<span class="variable">facteur</span>) {
  <span class="keyword">return</span> <span class="keyword">function</span>(<span class="variable">nombre</span>) {
    <span class="keyword">return</span> <span class="variable">nombre</span> * <span class="variable">facteur</span>;
  };
}

<span class="keyword">const</span> <span class="variable">triple</span> = <span class="function">creerMultiplicateur</span>(<span class="number">3</span>);
<span class="keyword">const</span> <span class="variable">quadruple</span> = <span class="function">creerMultiplicateur</span>(<span class="number">4</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="function">triple</span>(<span class="number">5</span>)); <span class="comment">// 15</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">quadruple</span>(<span class="number">5</span>)); <span class="comment">// 20</span></code></pre>
        </div>
      </section>

      <!-- Fonctions fléchées avancées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Fonctions Fléchées Avancées</h2>
        <p class="textExemple">
          Les fonctions fléchées ont une syntaxe plus concise et ne possèdent pas leur propre 
          contexte <code>this</code> (elles héritent du <code>this</code> du contexte parent).
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Différence entre fonction classique et fonction fléchée</span>
<span class="keyword">const</span> <span class="variable">objet</span> = {
  <span class="variable">valeur</span>: <span class="number">42</span>,
  <span class="function">methodeClassique</span>: <span class="keyword">function</span>() {
    <span class="function">console</span>.<span class="function">log</span>(<span class="string">"Classique:"</span>, <span class="keyword">this</span>.<span class="variable">valeur</span>); <span class="comment">// 42 (this = objet)</span>
  },
  <span class="function">methodeFlechee</span>: () <span class="operator">=></span> {
    <span class="function">console</span>.<span class="function">log</span>(<span class="string">"Fléchée:"</span>, <span class="keyword">this</span>.<span class="variable">valeur</span>); <span class="comment">// undefined (this ≠ objet)</span>
  }
};

<span class="variable">objet</span>.<span class="function">methodeClassique</span>();
<span class="variable">objet</span>.<span class="function">methodeFlechee</span>();</code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Cas d'utilisation des fonctions fléchées</h4>
          <pre><code><span class="comment">// Idéal pour les callbacks et les fonctions courtes</span>
<span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];

<span class="comment">// Avec fonction fléchée</span>
<span class="keyword">const</span> <span class="variable">carres</span> = <span class="variable">nombres</span>.<span class="function">map</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> * <span class="variable">n</span>);
<span class="keyword">const</span> <span class="variable">pairs</span> = <span class="variable">nombres</span>.<span class="function">filter</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> % <span class="number">2</span> === <span class="number">0</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">carres</span>); <span class="comment">// [1, 4, 9, 16, 25]</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">pairs</span>);  <span class="comment">// [2, 4]</span></code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices Pratiques</h2>
        
        <div class="exercise">
          <h4 class="text-purple">Exercice 1: Calculatrice simple</h4>
          <p>Créez une fonction qui prend deux nombres et une opération (+, -, *, /) et retourne le résultat.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">calculer</span>(<span class="variable">a</span>, <span class="variable">b</span>, <span class="variable">operation</span>) {
  <span class="keyword">switch</span>(<span class="variable">operation</span>) {
    <span class="keyword">case</span> <span class="string">'+'</span>:
      <span class="keyword">return</span> <span class="variable">a</span> + <span class="variable">b</span>;
    <span class="keyword">case</span> <span class="string">'-'</span>:
      <span class="keyword">return</span> <span class="variable">a</span> - <span class="variable">b</span>;
    <span class="keyword">case</span> <span class="string">'*'</span>:
      <span class="keyword">return</span> <span class="variable">a</span> * <span class="variable">b</span>;
    <span class="keyword">case</span> <span class="string">'/'</span>:
      <span class="keyword">return</span> <span class="variable">b</span> !== <span class="number">0</span> ? <span class="variable">a</span> / <span class="variable">b</span> : <span class="string">"Erreur: division par zéro"</span>;
    <span class="keyword">default</span>:
      <span class="keyword">return</span> <span class="string">"Opération non valide"</span>;
  }
}

<span class="function">console</span>.<span class="function">log</span>(<span class="function">calculer</span>(<span class="number">10</span>, <span class="number">5</span>, <span class="string">'+'</span>)); <span class="comment">// 15</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">calculer</span>(<span class="number">10</span>, <span class="number">5</span>, <span class="string">'/'</span>)); <span class="comment">// 2</span></code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h4 class="text-purple">Exercice 2: Compteur avec fermeture</h4>
          <p>Créez une fonction qui retourne une fonction de compteur. Chaque appel incrémente le compteur.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">creerCompteur</span>() {
  <span class="keyword">let</span> <span class="variable">compteur</span> = <span class="number">0</span>;
  <span class="keyword">return</span> <span class="keyword">function</span>() {
    <span class="variable">compteur</span><span class="operator">++</span>;
    <span class="keyword">return</span> <span class="variable">compteur</span>;
  };
}

<span class="keyword">const</span> <span class="variable">monCompteur</span> = <span class="function">creerCompteur</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="function">monCompteur</span>()); <span class="comment">// 1</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">monCompteur</span>()); <span class="comment">// 2</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">monCompteur</span>()); <span class="comment">// 3</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Résumé et conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Résumé</h2>
        <p class="text-white">
          Les fonctions sont un concept fondamental en JavaScript. Elles permettent de :
        </p>
        <ul class="text-white">
          <li>Organiser et structurer votre code</li>
          <li>Réutiliser des blocs de code</li>
          <li>Faciliter la maintenance et le débogage</li>
          <li>Créer des abstractions et des niveaux d'abstraction</li>
        </ul>
        <p class="text-white">
          Maîtriser les différentes façons de déclarer et d'utiliser les fonctions est essentiel 
          pour devenir un développeur JavaScript compétent.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JavaScriptFunctionsLesson',
  // Vous pouvez ajouter des données ou méthodes si nécessaire
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
.keyword { color: #c586c0 !important; } /* Mots-clés (function, return, const, let, etc.) */
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