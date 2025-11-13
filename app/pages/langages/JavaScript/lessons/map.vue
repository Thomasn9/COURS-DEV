<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">La fonction map() en JavaScript</h1>
                <p class="lesson-meta text-white">Manipuler et transformer des tableaux efficacement</p>
                <p class="lesson-meta text-white">
                    <span>Niveau : intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->s
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    La fonction <code>map()</code> est l'une des méthodes les plus utiles et couramment utilisées en
                    JavaScript pour manipuler des tableaux. Elle permet de créer un nouveau tableau en appliquant une
                    fonction à chaque élément d'un tableau existant, sans modifier le tableau original.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de base</h2>
                <p class="textExemple">
                    La syntaxe de la fonction <code>map()</code> est la suivante :
                </p>
                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> nouveauTableau <span class="token operator">=</span> tableau<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token parameter">element<span class="token punctuation">,</span> index<span class="token punctuation">,</span> tableau</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token comment">// Code à exécuter pour chaque élément</span>
  <span class="token keyword">return</span> nouvelleValeur<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
                </div>

                <p class="textExemple">
                    Avec les fonctions fléchées (arrow functions), la syntaxe devient plus concise :
                </p>
                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> nouveauTableau <span class="token operator">=</span> tableau<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token parameter">element<span class="token punctuation">,</span> index<span class="token punctuation">,</span> tableau</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token comment">// Code à exécuter pour chaque élément</span>
  <span class="token keyword">return</span> nouvelleValeur<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
                </div>

                <p class="textExemple">
                    Ou encore plus court si la fonction ne contient qu'une seule instruction :
                </p>
                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> nouveauTableau <span class="token operator">=</span> tableau<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">element</span> <span class="token operator">=></span> nouvelleValeur<span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
                </div>
            </section>

            <!-- Exemples pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples pratiques</h2>

                <h3 class="text-purple">Exemple 1 : Doubler les nombres</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Avec une boucle for classique</h4>
                        <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> doubles <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">let</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator"><</span> nombres<span class="token punctuation">.</span>length<span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  doubles<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>nombres<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>doubles<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4, 6, 8, 10]</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Avec la fonction map()</h4>
                        <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> doubles <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>doubles<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4, 6, 8, 10]</span></code></pre>
                    </div>
                </div>

                <h3 class="text-purple">Exemple 2 : Extraire des propriétés d'objets</h3>
                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> personnes <span class="token operator">=</span> <span class="token punctuation">[</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Alice'</span><span class="token punctuation">,</span> age<span class="token operator">:</span> <span class="token number">25</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Bob'</span><span class="token punctuation">,</span> age<span class="token operator">:</span> <span class="token number">30</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Charlie'</span><span class="token punctuation">,</span> age<span class="token operator">:</span> <span class="token number">35</span> <span class="token punctuation">}</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> noms <span class="token operator">=</span> personnes<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">personne</span> <span class="token operator">=></span> personne<span class="token punctuation">.</span>nom<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>noms<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// ['Alice', 'Bob', 'Charlie']</span></code></pre>
                </div>

                <h3 class="text-purple">Exemple 3 : Formater des données</h3>
                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> produits <span class="token operator">=</span> <span class="token punctuation">[</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Ordinateur'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">1000</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Souris'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">25</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Clavier'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">50</span> <span class="token punctuation">}</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> produitsFormates <span class="token operator">=</span> produits<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">produit</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token keyword">return</span> <span class="token punctuation">{</span>
    nom<span class="token operator">:</span> produit<span class="token punctuation">.</span>nom<span class="token punctuation">.</span><span class="token function">toUpperCase</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    prixHT<span class="token operator">:</span> produit<span class="token punctuation">.</span>prix<span class="token punctuation">,</span>
    prixTTC<span class="token operator">:</span> produit<span class="token punctuation">.</span>prix <span class="token operator">*</span> <span class="token number">1.2</span>
  <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>produitsFormates<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">// [</span>
<span class="token comment">//   { nom: 'ORDINATEUR', prixHT: 1000, prixTTC: 1200 },</span>
<span class="token comment">//   { nom: 'SOURIS', prixHT: 25, prixTTC: 30 },</span>
<span class="token comment">//   { nom: 'CLAVIER', prixHT: 50, prixTTC: 60 }</span>
<span class="token comment">// ]</span></code></pre>
                </div>
            </section>

            <!-- Paramètres de la fonction map() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Paramètres de la fonction map()</h2>
                <p class="textExemple">
                    La fonction de callback passée à <code>map()</code> peut recevoir trois paramètres :
                </p>

                <ul class="textExemple">
                    <li><strong>element</strong> : L'élément actuel du tableau en cours de traitement</li>
                    <li><strong>index</strong> (optionnel) : L'index de l'élément actuel dans le tableau</li>
                    <li><strong>tableau</strong> (optionnel) : Le tableau sur lequel <code>map()</code> a été appelé
                    </li>
                </ul>

                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">10</span><span class="token punctuation">,</span> <span class="token number">20</span><span class="token punctuation">,</span> <span class="token number">30</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> resultats <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token parameter">element<span class="token punctuation">,</span> index<span class="token punctuation">,</span> tableau</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token template-string"><span class="token template-punctuation string">`</span><span class="token string">Élément: </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>element<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">, Index: </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>index<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">, Tableau: [</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>tableau<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">]</span><span class="token template-punctuation string">`</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">return</span> element <span class="token operator">*</span> index<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>resultats<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [0, 20, 60]</span></code></pre>
                </div>
            </section>

            <!-- Différences avec d'autres méthodes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Différences avec d'autres méthodes de tableau</h2>

                <h3 class="text-purple">map() vs forEach()</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">forEach()</h4>
                        <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> resultats <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

nombres<span class="token punctuation">.</span><span class="token function">forEach</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  resultats<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>resultats<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4, 6]</span></code></pre>
                        <p class="textExemple">forEach() exécute une fonction sur chaque élément mais ne retourne pas de
                            nouveau tableau.</p>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">map()</h4>
                        <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> resultats <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>resultats<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4, 6]</span></code></pre>
                        <p class="textExemple">map() retourne automatiquement un nouveau tableau avec les résultats.</p>
                    </div>
                </div>

                <h3 class="text-purple">map() vs filter()</h3>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">filter()</h4>
                        <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> pairs <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">filter</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> nombre <span class="token operator">%</span> <span class="token number">2</span> <span class="token operator">===</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>pairs<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4]</span></code></pre>
                        <p class="textExemple">filter() crée un nouveau tableau avec les éléments qui passent un test.
                        </p>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">map()</h4>
                        <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> doubles <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>doubles<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4, 6, 8, 10]</span></code></pre>
                        <p class="textExemple">map() transforme chaque élément du tableau.</p>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec map()</h2>

                <h3 class="text-purple">1. Toujours retourner une valeur</h3>
                <div class="code-example">
                    <pre><code><span class="token comment">// ❌ Mauvais - oublie de retourner une valeur</span>
<span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> resultats <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">;</span> <span class="token comment">// Pas de return</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>resultats<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [undefined, undefined, undefined]</span>

<span class="token comment">// ✅ Bon - retourne explicitement une valeur</span>
<span class="token keyword">const</span> bonsResultats <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token keyword">return</span> nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>bonsResultats<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [2, 4, 6]</span></code></pre>
                </div>

                <h3 class="text-purple">2. Utiliser des fonctions pures quand possible</h3>
                <div class="code-example">
                    <pre><code><span class="token comment">// ❌ Mauvais - effet de bord</span>
<span class="token keyword">let</span> total <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> resultats <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  total <span class="token operator">+=</span> nombre<span class="token punctuation">;</span> <span class="token comment">// Effet de bord</span>
  <span class="token keyword">return</span> nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// ✅ Bon - fonction pure</span>
<span class="token keyword">const</span> bonsResultats <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> nombre <span class="token operator">*</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
                </div>

                <h3 class="text-purple">3. Chaîner avec d'autres méthodes</h3>
                <div class="code-example">
                    <pre><code><span class="token keyword">const</span> produits <span class="token operator">=</span> <span class="token punctuation">[</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Ordinateur'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">1000</span><span class="token punctuation">,</span> categorie<span class="token operator">:</span> <span class="token string">'électronique'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Chaise'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">150</span><span class="token punctuation">,</span> categorie<span class="token operator">:</span> <span class="token string">'mobilier'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Souris'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">25</span><span class="token punctuation">,</span> categorie<span class="token operator">:</span> <span class="token string">'électronique'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Table'</span><span class="token punctuation">,</span> prix<span class="token operator">:</span> <span class="token number">300</span><span class="token punctuation">,</span> categorie<span class="token operator">:</span> <span class="token string">'mobilier'</span> <span class="token punctuation">}</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token comment">// Filtrer les produits électroniques, puis formater leurs noms</span>
<span class="token keyword">const</span> nomsProduitsElectroniques <span class="token operator">=</span> produits
  <span class="token punctuation">.</span><span class="token function">filter</span><span class="token punctuation">(</span><span class="token parameter">produit</span> <span class="token operator">=></span> produit<span class="token punctuation">.</span>categorie <span class="token operator">===</span> <span class="token string">'électronique'</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">produit</span> <span class="token operator">=></span> produit<span class="token punctuation">.</span>nom<span class="token punctuation">.</span><span class="token function">toUpperCase</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>nomsProduitsElectroniques<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// ['ORDINATEUR', 'SOURIS']</span></code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Convertir des températures</h3>
                    <p class="textExemple">
                        Écrivez une fonction qui prend un tableau de températures en Celsius et retourne un nouveau
                        tableau avec ces températures converties en Fahrenheit. La formule de conversion est : F = C ×
                        9/5 + 32.
                    </p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="token keyword">const</span> temperaturesCelsius <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">15</span><span class="token punctuation">,</span> <span class="token number">25</span><span class="token punctuation">,</span> <span class="token number">30</span><span class="token punctuation">,</span> <span class="token number">40</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> temperaturesFahrenheit <span class="token operator">=</span> temperaturesCelsius<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">celsius</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token keyword">return</span> celsius <span class="token operator">*</span> <span class="token number">9</span><span class="token operator">/</span><span class="token number">5</span> <span class="token operator">+</span> <span class="token number">32</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>temperaturesFahrenheit<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [32, 59, 77, 86, 104]</span></code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Calculer des carrés</h3>
                    <p class="textExemple">
                        Écrivez une fonction qui prend un tableau de nombres et retourne un nouveau tableau contenant
                        les carrés de ces nombres.
                    </p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="token keyword">const</span> nombres <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> carres <span class="token operator">=</span> nombres<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">nombre</span> <span class="token operator">=></span> nombre <span class="token operator">**</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>carres<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// [1, 4, 9, 16, 25]</span></code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Formater des dates</h3>
                    <p class="textExemple">
                        Écrivez une fonction qui prend un tableau d'objets contenant des dates au format ISO et retourne
                        un nouveau tableau avec les dates formatées en français (JJ/MM/AAAA).
                    </p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="token keyword">const</span> evenements <span class="token operator">=</span> <span class="token punctuation">[</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Réunion'</span><span class="token punctuation">,</span> date<span class="token operator">:</span> <span class="token string">'2023-10-15'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Anniversaire'</span><span class="token punctuation">,</span> date<span class="token operator">:</span> <span class="token string">'2023-11-20'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span> nom<span class="token operator">:</span> <span class="token string">'Conférence'</span><span class="token punctuation">,</span> date<span class="token operator">:</span> <span class="token string">'2023-12-05'</span> <span class="token punctuation">}</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> evenementsFormates <span class="token operator">=</span> evenements<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token parameter">evenement</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token keyword">const</span> date <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span>evenement<span class="token punctuation">.</span>date<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">const</span> jour <span class="token operator">=</span> date<span class="token punctuation">.</span><span class="token function">getDate</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">toString</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">padStart</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token string">'0'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">const</span> mois <span class="token operator">=</span> <span class="token punctuation">(</span>date<span class="token punctuation">.</span><span class="token function">getMonth</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">toString</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">padStart</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token string">'0'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">const</span> annee <span class="token operator">=</span> date<span class="token punctuation">.</span><span class="token function">getFullYear</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  
  <span class="token keyword">return</span> <span class="token punctuation">{</span>
    nom<span class="token operator">:</span> evenement<span class="token punctuation">.</span>nom<span class="token punctuation">,</span>
    dateFormatee<span class="token operator">:</span> <span class="token template-string"><span class="token template-punctuation string">`</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>jour<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">/</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>mois<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">/</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>annee<span class="token interpolation-punctuation punctuation">}</span></span><span class="token template-punctuation string">`</span></span>
  <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token console class-name">console</span><span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>evenementsFormates<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">// [</span>
<span class="token comment">//   { nom: 'Réunion', dateFormatee: '15/10/2023' },</span>
<span class="token comment">//   { nom: 'Anniversaire', dateFormatee: '20/11/2023' },</span>
<span class="token comment">//   { nom: 'Conférence', dateFormatee: '05/12/2023' }</span>
<span class="token comment">// ]</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    La fonction <code>map()</code> est un outil puissant et essentiel en JavaScript moderne. Elle permet
                    de transformer des tableaux de manière déclarative et fonctionnelle, rendant le code plus lisible et
                    maintenable.
                </p>
                <p class="textExemple">
                    Points clés à retenir :
                </p>
                <ul class="textExemple">
                    <li><code>map()</code> crée un nouveau tableau sans modifier l'original</li>
                    <li>Elle est idéale pour transformer chaque élément d'un tableau</li>
                    <li>Elle peut être chaînée avec d'autres méthodes comme <code>filter()</code> et
                        <code>reduce()</code></li>
                    <li>Utilisez des fonctions pures dans <code>map()</code> pour éviter les effets de bord</li>
                </ul>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'LessonMapFunction',
    // Vous pouvez ajouter ici des données ou méthodes si nécessaire
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

/* Couleurs VS Code pour la syntaxe JavaScript */
.token.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (for, while, if, function, etc.) */
.token.variable {
    color: #9cdcfe !important;
}

/* Variables et noms de fonctions */
.token.string {
    color: #ce9178 !important;
}

/* Chaînes de caractères */
.token.comment {
    color: #6a9955 !important;
}

/* Commentaires */
.token.function {
    color: #dcdcaa !important;
}

/* Noms de fonctions */
.token.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs (+, -, =, =>, etc.) */
.token.constant {
    color: #4fc1ff !important;
}

/* Constantes */
.token.number {
    color: #b5cea8 !important;
}

/* Nombres */
.token.class-name {
    color: #4ec9b0 !important;
}

/* Noms de classes */
.token.console {
    color: #9cdcfe !important;
}

/* Objets console */
.token.parameter {
    color: #9cdcfe !important;
}

/* Paramètres de fonction */
.token.template-string {
    color: #ce9178 !important;
}

/* Template strings */
.token.interpolation {
    color: #9cdcfe !important;
}

/* Interpolation dans les templates */
.token.interpolation-punctuation {
    color: #d4d4d4 !important;
}

/* Ponctuation d'interpolation */
.token.punctuation {
    color: #d4d4d4 !important;
}

/* Ponctuation générale */

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