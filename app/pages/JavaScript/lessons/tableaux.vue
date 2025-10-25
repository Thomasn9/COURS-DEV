<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les Tableaux en JavaScript</h1>
                <p class="lesson-meta text-white">Maîtrisez la manipulation des tableaux et leurs méthodes</p>
                <p class="lesson-meta text-white">
                    <span>Niveau : Débutant / intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Tableaux</h2>
                <p class="textExemple">
                    Les tableaux (Arrays) sont des structures de données qui permettent de stocker plusieurs valeurs
                    dans une seule variable. Ils sont ordonnés, modifiables et peuvent contenir différents types de
                    données.
                </p>
            </section>

            <!-- Création de tableaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Création de Tableaux</h2>
                <p class="textExemple">
                    Il existe plusieurs façons de créer des tableaux en JavaScript :
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Syntaxe littérale (recommandée)</h4>
                        <pre><code><span class="comment">// Tableau vide</span>
<span class="keyword">const</span> <span class="variable">tableauVide</span> = [];

<span class="comment">// Tableau avec éléments</span>
<span class="keyword">const</span> <span class="variable">fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];

<span class="comment">// Tableau mixte</span>
<span class="keyword">const</span> <span class="variable">mixte</span> = [<span class="string">"texte"</span>, <span class="number">42</span>, <span class="keyword">true</span>, <span class="keyword">null</span>];

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>[<span class="number">0</span>]); <span class="comment">// "pomme"</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>.<span class="variable">length</span>); <span class="comment">// 3</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Constructeur Array</h4>
                        <pre><code><span class="comment">// Tableau vide</span>
<span class="keyword">const</span> <span class="variable">tableau1</span> = <span class="keyword">new</span> <span class="class-name">Array</span>();

<span class="comment">// Tableau avec taille spécifique</span>
<span class="keyword">const</span> <span class="variable">tableau2</span> = <span class="keyword">new</span> <span class="class-name">Array</span>(<span class="number">5</span>); <span class="comment">// 5 éléments vides</span>

<span class="comment">// Tableau avec éléments</span>
<span class="keyword">const</span> <span class="variable">tableau3</span> = <span class="keyword">new</span> <span class="class-name">Array</span>(<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">tableau3</span>[<span class="number">1</span>]); <span class="comment">// "b"</span></code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Tableaux multidimensionnels</h4>
                    <pre><code><span class="comment">// Matrice 2x3</span>
<span class="keyword">const</span> <span class="variable">matrice</span> = [
  [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>],
  [<span class="number">4</span>, <span class="number">5</span>, <span class="number">6</span>],
  [<span class="number">7</span>, <span class="number">8</span>, <span class="number">9</span>]
];

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">matrice</span>[<span class="number">1</span>][<span class="number">2</span>]); <span class="comment">// 6</span>

<span class="comment">// Tableau d'objets</span>
<span class="keyword">const</span> <span class="variable">personnes</span> = [
  { <span class="variable">nom</span>: <span class="string">"Alice"</span>, <span class="variable">age</span>: <span class="number">25</span> },
  { <span class="variable">nom</span>: <span class="string">"Bob"</span>, <span class="variable">age</span>: <span class="number">30</span> }
];

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">personnes</span>[<span class="number">0</span>].<span class="variable">nom</span>); <span class="comment">// "Alice"</span></code></pre>
                </div>
            </section>

            <!-- Méthodes d'accès et modification -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Accès et Modification</h2>
                <p class="textExemple">
                    Les tableaux sont mutables - vous pouvez modifier leurs éléments après leur création.
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Accès aux éléments</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">couleurs</span> = [<span class="string">"rouge"</span>, <span class="string">"vert"</span>, <span class="string">"bleu"</span>];

<span class="comment">// Accès par index</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">couleurs</span>[<span class="number">0</span>]); <span class="comment">// "rouge"</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">couleurs</span>[<span class="variable">couleurs</span>.<span class="variable">length</span> - <span class="number">1</span>]); <span class="comment">// "bleu" (dernier élément)</span>

<span class="comment">// Modification</span>
<span class="variable">couleurs</span>[<span class="number">1</span>] = <span class="string">"jaune"</span>;
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">couleurs</span>); <span class="comment">// ["rouge", "jaune", "bleu"]</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Méthodes basiques</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>];

<span class="comment">// Ajouter à la fin</span>
<span class="variable">nombres</span>.<span class="function">push</span>(<span class="number">4</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 2, 3, 4]</span>

<span class="comment">// Retirer le dernier</span>
<span class="keyword">const</span> <span class="variable">dernier</span> = <span class="variable">nombres</span>.<span class="function">pop</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">dernier</span>); <span class="comment">// 4</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 2, 3]</span>

<span class="comment">// Ajouter au début</span>
<span class="variable">nombres</span>.<span class="function">unshift</span>(<span class="number">0</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [0, 1, 2, 3]</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes de transformation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes de Transformation</h2>
                <p class="textExemple">
                    Les méthodes qui créent un nouveau tableau à partir d'un tableau existant.
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple"><code>map()</code> - Transformer</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>];

<span class="comment">// Créer un nouveau tableau avec les carrés</span>
<span class="keyword">const</span> <span class="variable">carres</span> = <span class="variable">nombres</span>.<span class="function">map</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> * <span class="variable">n</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">carres</span>); <span class="comment">// [1, 4, 9, 16]</span>

<span class="comment">// Transformer des objets</span>
<span class="keyword">const</span> <span class="variable">users</span> = [
  { <span class="variable">name</span>: <span class="string">"Alice"</span>, <span class="variable">age</span>: <span class="number">25</span> },
  { <span class="variable">name</span>: <span class="string">"Bob"</span>, <span class="variable">age</span>: <span class="number">30</span> }
];

<span class="keyword">const</span> <span class="variable">noms</span> = <span class="variable">users</span>.<span class="function">map</span>(<span class="variable">user</span> <span class="operator">=></span> <span class="variable">user</span>.<span class="variable">name</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">noms</span>); <span class="comment">// ["Alice", "Bob"]</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple"><code>filter()</code> - Filtrer</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>, <span class="number">6</span>];

<span class="comment">// Nombres pairs</span>
<span class="keyword">const</span> <span class="variable">pairs</span> = <span class="variable">nombres</span>.<span class="function">filter</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> % <span class="number">2</span> === <span class="number">0</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">pairs</span>); <span class="comment">// [2, 4, 6]</span>

<span class="comment">// Utilisateurs majeurs</span>
<span class="keyword">const</span> <span class="variable">users</span> = [
  { <span class="variable">name</span>: <span class="string">"Alice"</span>, <span class="variable">age</span>: <span class="number">17</span> },
  { <span class="variable">name</span>: <span class="string">"Bob"</span>, <span class="variable">age</span>: <span class="number">25</span> },
  { <span class="variable">name</span>: <span class="string">"Charlie"</span>, <span class="variable">age</span>: <span class="number">16</span> }
];

<span class="keyword">const</span> <span class="variable">majeurs</span> = <span class="variable">users</span>.<span class="function">filter</span>(<span class="variable">user</span> <span class="operator">=></span> <span class="variable">user</span>.<span class="variable">age</span> >= <span class="number">18</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">majeurs</span>); <span class="comment">// [{ name: "Bob", age: 25 }]</span></code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple"><code>reduce()</code> - Réduire</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>];

<span class="comment">// Somme</span>
<span class="keyword">const</span> <span class="variable">somme</span> = <span class="variable">nombres</span>.<span class="function">reduce</span>((<span class="variable">acc</span>, <span class="variable">n</span>) <span class="operator">=></span> <span class="variable">acc</span> + <span class="variable">n</span>, <span class="number">0</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">somme</span>); <span class="comment">// 10</span>

<span class="comment">// Produit</span>
<span class="keyword">const</span> <span class="variable">produit</span> = <span class="variable">nombres</span>.<span class="function">reduce</span>((<span class="variable">acc</span>, <span class="variable">n</span>) <span class="operator">=></span> <span class="variable">acc</span> * <span class="variable">n</span>, <span class="number">1</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">produit</span>); <span class="comment">// 24</span>

<span class="comment">// Maximum</span>
<span class="keyword">const</span> <span class="variable">max</span> = <span class="variable">nombres</span>.<span class="function">reduce</span>((<span class="variable">acc</span>, <span class="variable">n</span>) <span class="operator">=></span> <span class="variable">n</span> > <span class="variable">acc</span> ? <span class="variable">n</span> : <span class="variable">acc</span>, <span class="variable">nombres</span>[<span class="number">0</span>]);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">max</span>); <span class="comment">// 4</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple"><code>flat()</code> - Aplatir</h4>
                        <pre><code><span class="comment">// Tableau multidimensionnel</span>
<span class="keyword">const</span> <span class="variable">tableauImbrique</span> = [<span class="number">1</span>, [<span class="number">2</span>, <span class="number">3</span>], [<span class="number">4</span>, [<span class="number">5</span>, <span class="number">6</span>]]];

<span class="comment">// Aplatir un niveau</span>
<span class="keyword">const</span> <span class="variable">aplati1</span> = <span class="variable">tableauImbrique</span>.<span class="function">flat</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">aplati1</span>); <span class="comment">// [1, 2, 3, 4, [5, 6]]</span>

<span class="comment">// Aplatir complètement</span>
<span class="keyword">const</span> <span class="variable">aplati2</span> = <span class="variable">tableauImbrique</span>.<span class="function">flat</span>(<span class="number">2</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">aplati2</span>); <span class="comment">// [1, 2, 3, 4, 5, 6]</span>

<span class="comment">// Aplatir à l'infini</span>
<span class="keyword">const</span> <span class="variable">aplatiInfini</span> = <span class="variable">tableauImbrique</span>.<span class="function">flat</span>(<span class="class-name">Infinity</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">aplatiInfini</span>); <span class="comment">// [1, 2, 3, 4, 5, 6]</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes de recherche -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes de Recherche</h2>
                <p class="textExemple">
                    Trouver des éléments spécifiques dans un tableau.
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple"><code>find()</code> et <code>findIndex()</code></h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">users</span> = [
  { <span class="variable">id</span>: <span class="number">1</span>, <span class="variable">name</span>: <span class="string">"Alice"</span> },
  { <span class="variable">id</span>: <span class="number">2</span>, <span class="variable">name</span>: <span class="string">"Bob"</span> },
  { <span class="variable">id</span>: <span class="number">3</span>, <span class="variable">name</span>: <span class="string">"Charlie"</span> }
];

<span class="comment">// Trouver l'élément</span>
<span class="keyword">const</span> <span class="variable">user</span> = <span class="variable">users</span>.<span class="function">find</span>(<span class="variable">u</span> <span class="operator">=></span> <span class="variable">u</span>.<span class="variable">id</span> === <span class="number">2</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">user</span>); <span class="comment">// { id: 2, name: "Bob" }</span>

<span class="comment">// Trouver l'index</span>
<span class="keyword">const</span> <span class="variable">index</span> = <span class="variable">users</span>.<span class="function">findIndex</span>(<span class="variable">u</span> <span class="operator">=></span> <span class="variable">u</span>.<span class="variable">name</span> === <span class="string">"Charlie"</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">index</span>); <span class="comment">// 2</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple"><code>includes()</code> et <code>indexOf()</code></h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];

<span class="comment">// Vérifier la présence</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>.<span class="function">includes</span>(<span class="string">"banane"</span>)); <span class="comment">// true</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>.<span class="function">includes</span>(<span class="string">"kiwi"</span>));   <span class="comment">// false</span>

<span class="comment">// Trouver l'index</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>.<span class="function">indexOf</span>(<span class="string">"orange"</span>)); <span class="comment">// 2</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>.<span class="function">indexOf</span>(<span class="string">"kiwi"</span>));   <span class="comment">// -1 (non trouvé)</span>

<span class="comment">// Dernière occurrence</span>
<span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">2</span>, <span class="number">1</span>];
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>.<span class="function">lastIndexOf</span>(<span class="number">2</span>)); <span class="comment">// 3</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes de tri -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Tri et Ordonnancement</h2>
                <p class="textExemple">
                    Organiser les éléments d'un tableau dans un ordre spécifique.
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple"><code>sort()</code> - Trier</h4>
                        <pre><code><span class="comment">// Tri de chaînes (alphabétique)</span>
<span class="keyword">const</span> <span class="variable">fruits</span> = [<span class="string">"banane"</span>, <span class="string">"pomme"</span>, <span class="string">"orange"</span>];
<span class="variable">fruits</span>.<span class="function">sort</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">fruits</span>); <span class="comment">// ["banane", "orange", "pomme"]</span>

<span class="comment">// Tri de nombres (attention!)</span>
<span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">10</span>, <span class="number">2</span>, <span class="number">1</span>, <span class="number">20</span>];
<span class="variable">nombres</span>.<span class="function">sort</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 10, 2, 20] (tri lexicographique)</span>

<span class="comment">// Tri numérique correct</span>
<span class="variable">nombres</span>.<span class="function">sort</span>((<span class="variable">a</span>, <span class="variable">b</span>) <span class="operator">=></span> <span class="variable">a</span> - <span class="variable">b</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 2, 10, 20]</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple"><code>reverse()</code> - Inverser</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">lettres</span> = [<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>];
<span class="variable">lettres</span>.<span class="function">reverse</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">lettres</span>); <span class="comment">// ["c", "b", "a"]</span>

<span class="comment">// Combinaison sort + reverse</span>
<span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">3</span>, <span class="number">1</span>, <span class="number">4</span>, <span class="number">2</span>];
<span class="variable">nombres</span>.<span class="function">sort</span>((<span class="variable">a</span>, <span class="variable">b</span>) <span class="operator">=></span> <span class="variable">b</span> - <span class="variable">a</span>); <span class="comment">// Tri décroissant</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [4, 3, 2, 1]</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes utilitaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes Utilitaires</h2>
                <p class="textExemple">
                    Autres méthodes utiles pour manipuler et inspecter les tableaux.
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple"><code>forEach()</code> - Itérer</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];

<span class="comment">// Exécuter une fonction pour chaque élément</span>
<span class="variable">fruits</span>.<span class="function">forEach</span>((<span class="variable">fruit</span>, <span class="variable">index</span>) <span class="operator">=></span> {
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">`<span class="operator">${</span><span class="variable">index</span><span class="operator">}</span>: <span class="operator">${</span><span class="variable">fruit</span><span class="operator">}</span>`</span>);
});

<span class="comment">// Résultat:</span>
<span class="comment">// 0: pomme</span>
<span class="comment">// 1: banane</span>
<span class="comment">// 2: orange</span>

<span class="comment">// Attention: forEach() ne retourne rien (undefined)</span>
<span class="keyword">const</span> <span class="variable">resultat</span> = <span class="variable">fruits</span>.<span class="function">forEach</span>(<span class="variable">fruit</span> <span class="operator">=></span> <span class="variable">fruit</span>.<span class="function">toUpperCase</span>());
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">resultat</span>); <span class="comment">// undefined</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple"><code>some()</code> et <code>every()</code></h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">2</span>, <span class="number">4</span>, <span class="number">6</span>, <span class="number">8</span>];
<span class="keyword">const</span> <span class="variable">mixte</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>];

<span class="comment">// every() - tous les éléments vérifient la condition</span>
<span class="keyword">const</span> <span class="variable">tousPairs</span> = <span class="variable">nombres</span>.<span class="function">every</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> % <span class="number">2</span> === <span class="number">0</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">tousPairs</span>); <span class="comment">// true</span>

<span class="comment">// some() - au moins un élément vérifie la condition</span>
<span class="keyword">const</span> <span class="variable">auMoinsUnPair</span> = <span class="variable">mixte</span>.<span class="function">some</span>(<span class="variable">n</span> <span class="operator">=></span> <span class="variable">n</span> % <span class="number">2</span> === <span class="number">0</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">auMoinsUnPair</span>); <span class="comment">// true</span>

<span class="comment">// Vérifications pratiques</span>
<span class="keyword">const</span> <span class="variable">users</span> = [
  { <span class="variable">name</span>: <span class="string">"Alice"</span>, <span class="variable">active</span>: <span class="keyword">true</span> },
  { <span class="variable">name</span>: <span class="string">"Bob"</span>, <span class="variable">active</span>: <span class="keyword">false</span> }
];

<span class="keyword">const</span> <span class="variable">tousActifs</span> = <span class="variable">users</span>.<span class="function">every</span>(<span class="variable">user</span> <span class="operator">=></span> <span class="variable">user</span>.<span class="variable">active</span>);
<span class="keyword">const</span> <span class="variable">auMoinsUnActif</span> = <span class="variable">users</span>.<span class="function">some</span>(<span class="variable">user</span> <span class="operator">=></span> <span class="variable">user</span>.<span class="variable">active</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="variable">tousActifs</span>);    <span class="comment">// false</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">auMoinsUnActif</span>); <span class="comment">// true</span></code></pre>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple"><code>slice()</code> - Extraire</h4>
                        <pre><code><span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];

<span class="comment">// Extraire une partie</span>
<span class="keyword">const</span> <span class="variable">partie</span> = <span class="variable">nombres</span>.<span class="function">slice</span>(<span class="number">1</span>, <span class="number">4</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">partie</span>); <span class="comment">// [2, 3, 4]</span>

<span class="comment">// Copier un tableau</span>
<span class="keyword">const</span> <span class="variable">copie</span> = <span class="variable">nombres</span>.<span class="function">slice</span>();
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">copie</span>); <span class="comment">// [1, 2, 3, 4, 5]</span>

<span class="comment">// Derniers éléments</span>
<span class="keyword">const</span> <span class="variable">derniers</span> = <span class="variable">nombres</span>.<span class="function">slice</span>(-<span class="number">2</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">derniers</span>); <span class="comment">// [4, 5]</span></code></pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple"><code>splice()</code> - Modifier</h4>
                        <pre><code><span class="keyword">let</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];

<span class="comment">// Supprimer des éléments</span>
<span class="keyword">const</span> <span class="variable">supprimes</span> = <span class="variable">nombres</span>.<span class="function">splice</span>(<span class="number">1</span>, <span class="number">2</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">supprimes</span>); <span class="comment">// [2, 3]</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 4, 5]</span>

<span class="comment">// Remplacer des éléments</span>
<span class="variable">nombres</span>.<span class="function">splice</span>(<span class="number">1</span>, <span class="number">1</span>, <span class="number">6</span>, <span class="number">7</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 6, 7, 5]</span>

<span class="comment">// Ajouter sans supprimer</span>
<span class="variable">nombres</span>.<span class="function">splice</span>(<span class="number">2</span>, <span class="number">0</span>, <span class="number">8</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nombres</span>); <span class="comment">// [1, 6, 8, 7, 5]</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h4 class="text-purple">Exercice 1: Statistiques sur un tableau</h4>
                    <p>Créez une fonction qui prend un tableau de nombres et retourne un objet avec la somme, moyenne,
                        minimum et maximum.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="keyword">function</span> <span class="function">statistiques</span>(<span class="variable">nombres</span>) {
  <span class="keyword">const</span> <span class="variable">somme</span> = <span class="variable">nombres</span>.<span class="function">reduce</span>((<span class="variable">acc</span>, <span class="variable">n</span>) <span class="operator">=></span> <span class="variable">acc</span> + <span class="variable">n</span>, <span class="number">0</span>);
  <span class="keyword">const</span> <span class="variable">moyenne</span> = <span class="variable">somme</span> / <span class="variable">nombres</span>.<span class="variable">length</span>;
  <span class="keyword">const</span> <span class="variable">min</span> = <span class="class-name">Math</span>.<span class="function">min</span>(...<span class="variable">nombres</span>);
  <span class="keyword">const</span> <span class="variable">max</span> = <span class="class-name">Math</span>.<span class="function">max</span>(...<span class="variable">nombres</span>);
  
  <span class="keyword">return</span> {
    <span class="variable">somme</span>,
    <span class="variable">moyenne</span>: <span class="function">parseFloat</span>(<span class="variable">moyenne</span>.<span class="function">toFixed</span>(<span class="number">2</span>)),
    <span class="variable">min</span>,
    <span class="variable">max</span>
  };
}

<span class="keyword">const</span> <span class="variable">nombres</span> = [<span class="number">10</span>, <span class="number">20</span>, <span class="number">30</span>, <span class="number">40</span>, <span class="number">50</span>];
<span class="function">console</span>.<span class="function">log</span>(<span class="function">statistiques</span>(<span class="variable">nombres</span>));
<span class="comment">// { somme: 150, moyenne: 30, min: 10, max: 50 }</span></code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h4 class="text-purple">Exercice 2: Filtrer et transformer</h4>
                    <p>À partir d'un tableau d'objets utilisateurs, créez un nouveau tableau avec les noms des
                        utilisateurs majeurs en majuscules.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="keyword">const</span> <span class="variable">utilisateurs</span> = [
  { <span class="variable">nom</span>: <span class="string">"alice"</span>, <span class="variable">age</span>: <span class="number">17</span> },
  { <span class="variable">nom</span>: <span class="string">"bob"</span>, <span class="variable">age</span>: <span class="number">25</span> },
  { <span class="variable">nom</span>: <span class="string">"charlie"</span>, <span class="variable">age</span>: <span class="number">16</span> },
  { <span class="variable">nom</span>: <span class="string">"david"</span>, <span class="variable">age</span>: <span class="number">30</span> }
];

<span class="keyword">function</span> <span class="function">nomsMajeursMajuscules</span>(<span class="variable">users</span>) {
  <span class="keyword">return</span> <span class="variable">users</span>
    .<span class="function">filter</span>(<span class="variable">user</span> <span class="operator">=></span> <span class="variable">user</span>.<span class="variable">age</span> >= <span class="number">18</span>)
    .<span class="function">map</span>(<span class="variable">user</span> <span class="operator">=></span> <span class="variable">user</span>.<span class="variable">nom</span>.<span class="function">toUpperCase</span>());
}

<span class="keyword">const</span> <span class="variable">resultat</span> = <span class="function">nomsMajeursMajuscules</span>(<span class="variable">utilisateurs</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">resultat</span>); <span class="comment">// ["BOB", "DAVID"]</span></code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h4 class="text-purple">Exercice 3: Supprimer les doublons</h4>
                    <p>Créez une fonction qui supprime les doublons d'un tableau.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="keyword">function</span> <span class="function">supprimerDoublons</span>(<span class="variable">tableau</span>) {
  <span class="comment">// Avec Set (méthode moderne)</span>
  <span class="keyword">return</span> [...<span class="keyword">new</span> <span class="class-name">Set</span>(<span class="variable">tableau</span>)];
}

<span class="comment">// Version avec filter</span>
<span class="keyword">function</span> <span class="function">supprimerDoublonsFilter</span>(<span class="variable">tableau</span>) {
  <span class="keyword">return</span> <span class="variable">tableau</span>.<span class="function">filter</span>((<span class="variable">element</span>, <span class="variable">index</span>) <span class="operator">=></span> 
    <span class="variable">tableau</span>.<span class="function">indexOf</span>(<span class="variable">element</span>) === <span class="variable">index</span>);
}

<span class="keyword">const</span> <span class="variable">avecDoublons</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">4</span>, <span class="number">5</span>];
<span class="function">console</span>.<span class="function">log</span>(<span class="function">supprimerDoublons</span>(<span class="variable">avecDoublons</span>)); <span class="comment">// [1, 2, 3, 4, 5]</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Résumé et conclusion -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Résumé</h2>
                <p class="text-white">
                    Les tableaux sont une structure de données fondamentale en JavaScript. Voici les points clés :
                </p>
                <ul class="text-white">
                    <li><strong>Création</strong> : Syntaxe littérale <code>[]</code> recommandée</li>
                    <li><strong>Accès</strong> : Par index <code>tableau[index]</code></li>
                    <li><strong>Modification</strong> : <code>push()</code>, <code>pop()</code>, <code>splice()</code>
                    </li>
                    <li><strong>Transformation</strong> : <code>map()</code>, <code>filter()</code>,
                        <code>reduce()</code></li>
                    <li><strong>Recherche</strong> : <code>find()</code>, <code>includes()</code>,
                        <code>indexOf()</code></li>
                    <li><strong>Tri</strong> : <code>sort()</code> avec fonction de comparaison pour les nombres</li>
                </ul>
                <p class="text-white">
                    Maîtriser les méthodes de tableau est essentiel pour manipuler efficacement les collections de
                    données.
                </p>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaScriptArraysLesson',
    // Vous pouvez ajouter des données ou méthodes si nécessaire
}
</script>

<style scoped>
/* Le CSS reste identique à celui fourni précédemment */
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
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (const, let, function, return, etc.) */
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