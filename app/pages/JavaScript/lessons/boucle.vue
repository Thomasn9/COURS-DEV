<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Boucles en JavaScript</h1>
        <p class="lesson-meta text-white">Maîtrisez les différentes boucles pour itérer efficacement en JavaScript</p>
        <p class="lesson-meta text-white">
                    <span>Niveau : Débutant</span>
                </p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Boucles</h2>
        <p class="textExemple">
          Les boucles permettent d'exécuter un bloc de code plusieurs fois de suite. 
          Elles sont essentielles pour traiter des collections de données, répéter des opérations 
          et automatiser des tâches répétitives.
        </p>
      </section>

      <!-- Boucle for -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Boucle <code>for</code></h2>
        <p class="textExemple">
          La boucle <code>for</code> est la plus classique. Elle comprend trois parties : 
          initialisation, condition, et incrémentation.
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Syntaxe de base</span>
<span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">0</span>; <span class="variable">i</span> &lt; <span class="number">5</span>; <span class="variable">i</span><span class="operator">++</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">"Itération numéro "</span> + <span class="variable">i</span>);
}

<span class="comment">// Résultat:</span>
<span class="comment">// Itération numéro 0</span>
<span class="comment">// Itération numéro 1</span>
<span class="comment">// Itération numéro 2</span>
<span class="comment">// Itération numéro 3</span>
<span class="comment">// Itération numéro 4</span></code></pre>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Boucle for avec tableau</h4>
            <pre><code><span class="keyword">const</span> <span class="variable">fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];

<span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">0</span>; <span class="variable">i</span> &lt; <span class="variable">fruits</span>.<span class="variable">length</span>; <span class="variable">i</span><span class="operator">++</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>[<span class="variable">i</span>]);
}

<span class="comment">// Résultat:</span>
<span class="comment">// pomme</span>
<span class="comment">// banane</span>
<span class="comment">// orange</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">Boucle for avec décrémentation</h4>
            <pre><code><span class="comment">// Compter à rebours</span>
<span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">10</span>; <span class="variable">i</span> &gt;= <span class="number">0</span>; <span class="variable">i</span><span class="operator">--</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">i</span>);
}

<span class="comment">// Résultat: 10, 9, 8, ..., 0</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Boucle while -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Boucle <code>while</code></h2>
        <p class="textExemple">
          La boucle <code>while</code> exécute un bloc de code tant qu'une condition est vraie.
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Boucle while classique</h4>
            <pre><code><span class="keyword">let</span> <span class="variable">compteur</span> = <span class="number">0</span>;

<span class="keyword">while</span> (<span class="variable">compteur</span> &lt; <span class="number">5</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">"Compteur: "</span> + <span class="variable">compteur</span>);
  <span class="variable">compteur</span><span class="operator">++</span>;
}

<span class="comment">// Résultat: Compteur: 0, 1, 2, 3, 4</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">Boucle do...while</h4>
            <pre><code><span class="keyword">let</span> <span class="variable">nombre</span>;

<span class="keyword">do</span> {
  <span class="variable">nombre</span> = <span class="function">prompt</span>(<span class="string">"Entrez un nombre supérieur à 10:"</span>);
} <span class="keyword">while</span> (<span class="variable">nombre</span> &lt;= <span class="number">10</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="string">"Merci! Vous avez entré: "</span> + <span class="variable">nombre</span>);</code></pre>
          </div>
        </div>
      </section>

      <!-- Boucle for...of -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Boucle <code>for...of</code> (ES6)</h2>
        <p class="textExemple">
          La boucle <code>for...of</code> permet d'itérer sur les éléments des objets itérables 
          (tableaux, chaînes, Map, Set, etc.).
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Avec les tableaux</h4>
            <pre><code><span class="keyword">const</span> <span class="variable">couleurs</span> = [<span class="string">"rouge"</span>, <span class="string">"vert"</span>, <span class="string">"bleu"</span>];

<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">couleur</span> <span class="keyword">of</span> <span class="variable">couleurs</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">couleur</span>);
}

<span class="comment">// Résultat: rouge, vert, bleu</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple">Avec les chaînes de caractères</h4>
            <pre><code><span class="keyword">const</span> <span class="variable">message</span> = <span class="string">"Hello"</span>;

<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">lettre</span> <span class="keyword">of</span> <span class="variable">message</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">lettre</span>);
}

<span class="comment">// Résultat: H, e, l, l, o</span></code></pre>
          </div>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Avec Map et Set</h4>
          <pre><code><span class="comment">// Avec Map</span>
<span class="keyword">const</span> <span class="variable">map</span> = <span class="keyword">new</span> <span class="class-name">Map</span>([
  [<span class="string">"nom"</span>, <span class="string">"Alice"</span>],
  [<span class="string">"age"</span>, <span class="number">30</span>]
]);

<span class="keyword">for</span> (<span class="keyword">const</span> [<span class="variable">cle</span>, <span class="variable">valeur</span>] <span class="keyword">of</span> <span class="variable">map</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">cle</span> + <span class="string">": "</span> + <span class="variable">valeur</span>);
}

<span class="comment">// Avec Set</span>
<span class="keyword">const</span> <span class="variable">set</span> = <span class="keyword">new</span> <span class="class-name">Set</span>([<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">2</span>, <span class="number">1</span>]);

<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">valeur</span> <span class="keyword">of</span> <span class="variable">set</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">valeur</span>);
}

<span class="comment">// Résultat: 1, 2, 3 (les doublons sont supprimés)</span></code></pre>
        </div>
      </section>

      <!-- Boucle for...in -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Boucle <code>for...in</code></h2>
        <p class="textExemple">
          La boucle <code>for...in</code> permet d'itérer sur les propriétés énumérables d'un objet.
        </p>

        <div class="code-example">
          <pre><code><span class="keyword">const</span> <span class="variable">personne</span> = {
  <span class="variable">nom</span>: <span class="string">"Jean"</span>,
  <span class="variable">age</span>: <span class="number">25</span>,
  <span class="variable">ville</span>: <span class="string">"Paris"</span>
};

<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">propriete</span> <span class="keyword">in</span> <span class="variable">personne</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">propriete</span> + <span class="string">": "</span> + <span class="variable">personne</span>[<span class="variable">propriete</span>]);
}

<span class="comment">// Résultat:</span>
<span class="comment">// nom: Jean</span>
<span class="comment">// age: 25</span>
<span class="comment">// ville: Paris</span></code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Attention avec les tableaux</h4>
          <pre><code><span class="keyword">const</span> <span class="variable">tableau</span> = [<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>];

<span class="comment">// for...in itère sur les indices (propriétés énumérables)</span>
<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">index</span> <span class="keyword">in</span> <span class="variable">tableau</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">index</span> + <span class="string">": "</span> + <span class="variable">tableau</span>[<span class="variable">index</span>]);
}

<span class="comment">// Résultat: 0: a, 1: b, 2: c</span>

<span class="comment">// Pour les tableaux, préférez for...of</span>
<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">element</span> <span class="keyword">of</span> <span class="variable">tableau</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">element</span>);
}

<span class="comment">// Résultat: a, b, c</span></code></pre>
        </div>
      </section>

      <!-- Méthodes de tableau fonctionnelles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Méthodes Fonctionnelles de Tableau</h2>
        <p class="textExemple">
          JavaScript offre des méthodes fonctionnelles pour itérer sur les tableaux sans utiliser de boucles traditionnelles.
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple"><code>forEach()</code></h4>
            <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];

<span class="variable">nombres</span>.<span class="function">forEach</span>((<span class="variable">nombre</span>, <span class="variable">index</span>) <span class="operator">=></span> {
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">`Index <span class="operator">${</span><span class="variable">index</span><span class="operator">}</span>: <span class="operator">${</span><span class="variable">nombre</span><span class="operator">}</span>`</span>);
});

<span class="comment">// Résultat: Index 0: 1, Index 1: 2, ...</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple"><code>map()</code></h4>
            <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>];
<span class="keyword">const</span> <span class="variable">carres</span> = <span class="variable">nombres</span>.<span class="function">map</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> * <span class="variable">n</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">carres</span>); <span class="comment">// [1, 4, 9]</span></code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple"><code>filter()</code></h4>
            <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];
<span class="keyword">const</span> <span class="variable">pairs</span> = <span class="variable">nombres</span>.<span class="function">filter</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> % <span class="number">2</span> === <span class="number">0</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">pairs</span>); <span class="comment">// [2, 4]</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple"><code>reduce()</code></h4>
            <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>];
<span class="keyword">const</span> <span class="variable">somme</span> = <span class="variable">nombres</span>.<span class="function">reduce</span>((<span class="variable">acc</span>, <span class="variable">n</span>) <span class="operator">=></span> <span class="variable">acc</span> + <span class="variable">n</span>, <span class="number">0</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">somme</span>); <span class="comment">// 10</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Contrôle des boucles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Contrôle des Boucles</h2>
        <p class="textExemple">
          Les instructions <code>break</code> et <code>continue</code> permettent de contrôler le flux d'exécution des boucles.
        </p>

        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple"><code>break</code> - Arrêt prématuré</h4>
            <pre><code><span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">0</span>; <span class="variable">i</span> &lt; <span class="number">10</span>; <span class="variable">i</span><span class="operator">++</span>) {
  <span class="keyword">if</span> (<span class="variable">i</span> === <span class="number">5</span>) {
    <span class="keyword">break</span>; <span class="comment">// Arrête la boucle quand i atteint 5</span>
  }
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">i</span>);
}

<span class="comment">// Résultat: 0, 1, 2, 3, 4</span></code></pre>
          </div>

          <div class="code-example">
            <h4 class="text-purple"><code>continue</code> - Passer à l'itération suivante</h4>
            <pre><code><span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">0</span>; <span class="variable">i</span> &lt; <span class="number">5</span>; <span class="variable">i</span><span class="operator">++</span>) {
  <span class="keyword">if</span> (<span class="variable">i</span> === <span class="number">2</span>) {
    <span class="keyword">continue</span>; <span class="comment">// Saute l'itération quand i vaut 2</span>
  }
  <span class="function">console</span>.<span class="function">log</span>(<span class="variable">i</span>);
}

<span class="comment">// Résultat: 0, 1, 3, 4</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Boucles imbriquées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Boucles Imbriquées</h2>
        <p class="textExemple">
          Il est possible d'imbriquer des boucles pour traiter des structures de données multidimensionnelles.
        </p>

        <div class="code-example">
          <pre><code><span class="comment">// Tableau multidimensionnel (matrice)</span>
<span class="keyword">const</span> <span class="variable">matrice</span> = [
  [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>],
  [<span class="number">4</span>, <span class="number">5</span>, <span class="number">6</span>],
  [<span class="number">7</span>, <span class="number">8</span>, <span class="number">9</span>]
];

<span class="comment">// Boucles imbriquées pour parcourir la matrice</span>
<span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">0</span>; <span class="variable">i</span> &lt; <span class="variable">matrice</span>.<span class="variable">length</span>; <span class="variable">i</span><span class="operator">++</span>) {
  <span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">j</span> = <span class="number">0</span>; <span class="variable">j</span> &lt; <span class="variable">matrice</span>[<span class="variable">i</span>].<span class="variable">length</span>; <span class="variable">j</span><span class="operator">++</span>) {
    <span class="function">console</span>.<span class="function">log</span>(<span class="string">`matrice[<span class="operator">${</span><span class="variable">i</span><span class="operator">}</span>][<span class="operator">${</span><span class="variable">j</span><span class="operator">}</span>] = <span class="operator">${</span><span class="variable">matrice</span>[<span class="variable">i</span>][<span class="variable">j</span>]<span class="operator">}</span>`</span>);
  }
}

<span class="comment">// Avec for...of</span>
<span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">ligne</span> <span class="keyword">of</span> <span class="variable">matrice</span>) {
  <span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">element</span> <span class="keyword">of</span> <span class="variable">ligne</span>) {
    <span class="function">console</span>.<span class="function">log</span>(<span class="variable">element</span>);
  }
}</code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices Pratiques</h2>
        
        <div class="exercise">
          <h4 class="text-purple">Exercice 1: Somme des nombres pairs</h4>
          <p>Écrivez une fonction qui calcule la somme de tous les nombres pairs d'un tableau.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">sommePairs</span>(<span class="variable">nombres</span>) {
  <span class="keyword">let</span> <span class="variable">somme</span> = <span class="number">0</span>;
  
  <span class="keyword">for</span> (<span class="keyword">const</span> <span class="variable">nombre</span> <span class="keyword">of</span> <span class="variable">nombres</span>) {
    <span class="keyword">if</span> (<span class="variable">nombre</span> % <span class="number">2</span> === <span class="number">0</span>) {
      <span class="variable">somme</span> += <span class="variable">nombre</span>;
    }
  }
  
  <span class="keyword">return</span> <span class="variable">somme</span>;
}

<span class="comment">// Version avec reduce</span>
<span class="keyword">function</span> <span class="function">sommePairsReduce</span>(<span class="variable">nombres</span>) {
  <span class="keyword">return</span> <span class="variable">nombres</span>.<span class="function">reduce</span>((<span class="variable">acc</span>, <span class="variable">n</span>) <span class="operator">=></span> 
    <span class="variable">n</span> % <span class="number">2</span> === <span class="number">0</span> ? <span class="variable">acc</span> + <span class="variable">n</span> : <span class="variable">acc</span>, <span class="number">0</span>);
}

<span class="keyword">const</span> <span class="variable">test</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>, <span class="number">6</span>];
<span class="function">console</span>.<span class="function">log</span>(<span class="function">sommePairs</span>(<span class="variable">test</span>)); <span class="comment">// 12 (2 + 4 + 6)</span></code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h4 class="text-purple">Exercice 2: Recherche d'élément</h4>
          <p>Écrivez une fonction qui cherche si un élément existe dans un tableau et retourne son index.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">trouverIndex</span>(<span class="variable">tableau</span>, <span class="variable">element</span>) {
  <span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">0</span>; <span class="variable">i</span> &lt; <span class="variable">tableau</span>.<span class="variable">length</span>; <span class="variable">i</span><span class="operator">++</span>) {
    <span class="keyword">if</span> (<span class="variable">tableau</span>[<span class="variable">i</span>] === <span class="variable">element</span>) {
      <span class="keyword">return</span> <span class="variable">i</span>; <span class="comment">// Retourne l'index si trouvé</span>
    }
  }
  <span class="keyword">return</span> -<span class="number">1</span>; <span class="comment">// Retourne -1 si non trouvé</span>
}

<span class="comment">// Version avec indexOf</span>
<span class="keyword">function</span> <span class="function">trouverIndexSimple</span>(<span class="variable">tableau</span>, <span class="variable">element</span>) {
  <span class="keyword">return</span> <span class="variable">tableau</span>.<span class="function">indexOf</span>(<span class="variable">element</span>);
}

<span class="keyword">const</span> <span class="variable">fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];
<span class="function">console</span>.<span class="function">log</span>(<span class="function">trouverIndex</span>(<span class="variable">fruits</span>, <span class="string">"banane"</span>)); <span class="comment">// 1</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="function">trouverIndex</span>(<span class="variable">fruits</span>, <span class="string">"kiwi"</span>));   <span class="comment">// -1</span></code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h4 class="text-purple">Exercice 3: Table de multiplication</h4>
          <p>Créez une fonction qui génère la table de multiplication d'un nombre donné.</p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">tableMultiplication</span>(<span class="variable">nombre</span>) {
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">`Table de multiplication de <span class="operator">${</span><span class="variable">nombre</span><span class="operator">}</span>:`</span>);
  
  <span class="keyword">for</span> (<span class="keyword">let</span> <span class="variable">i</span> = <span class="number">1</span>; <span class="variable">i</span> &lt;= <span class="number">10</span>; <span class="variable">i</span><span class="operator">++</span>) {
    <span class="keyword">const</span> <span class="variable">resultat</span> = <span class="variable">nombre</span> * <span class="variable">i</span>;
    <span class="function">console</span>.<span class="function">log</span>(<span class="string">`<span class="operator">${</span><span class="variable">nombre</span><span class="operator">}</span> × <span class="operator">${</span><span class="variable">i</span><span class="operator">}</span> = <span class="operator">${</span><span class="variable">resultat</span><span class="operator">}</span>`</span>);
  }
}

<span class="function">tableMultiplication</span>(<span class="number">7</span>);</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Résumé et conclusion -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Résumé</h2>
        <p class="text-white">
          Les boucles sont fondamentales en programmation. Chaque type a ses cas d'usage spécifiques :
        </p>
        <ul class="text-white">
          <li><strong>for</strong> : Quand vous connaissez le nombre d'itérations</li>
          <li><strong>while</strong> : Quand la condition d'arrêt est complexe</li>
          <li><strong>for...of</strong> : Pour itérer sur les éléments des collections</li>
          <li><strong>for...in</strong> : Pour itérer sur les propriétés d'objets</li>
          <li><strong>Méthodes fonctionnelles</strong> : Pour un code plus déclaratif</li>
        </ul>
        <p class="text-white">
          Maîtriser les différentes boucles vous permettra d'écrire du code plus efficace et plus lisible.
        </p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JavaScriptLoopsLesson',
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