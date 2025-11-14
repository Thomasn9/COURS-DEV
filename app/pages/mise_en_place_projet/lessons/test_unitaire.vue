<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Tests unitaires avec Vitest</h1>
                <p class="lesson-meta text-white">Apprenez à configurer et utiliser Vitest pour tester votre code
                    JavaScript</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    Les tests unitaires sont essentiels pour garantir la fiabilité de votre code. Ils permettent de
                    vérifier que chaque partie de votre application fonctionne correctement, isolément. Dans cette
                    leçon, nous allons découvrir comment configurer et utiliser Vitest, un framework de test rapide et
                    moderne pour JavaScript.
                </p>
            </section>

            <!-- Configuration initiale -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Configuration initiale du projet</h2>
                <p class="textExemple">
                    Commençons par initialiser un nouveau projet Node.js et installer les dépendances nécessaires.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Initialisation du projet</h4>
                    <pre><code class="language-bash"><span class="comment"># Crée un nouveau projet</span>
<span class="function">npm init</span></code></pre>
                </div>

                <p class="textExemple">
                    Cette commande crée un fichier <code>package.json</code> avec les valeurs par défaut.
                </p>
            </section>

            <!-- Création des fichiers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Création des fichiers</h2>
                <p class="textExemple">
                    Nous allons maintenant créer les fichiers nécessaires pour notre exemple de test.
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Fichier index.js</h4>
                        <pre><code class="language-javascript"><span class="comment">// Fonction à tester</span>
<span class="keyword">export function</span> <span class="function">add</span>(<span class="variable">a</span>, <span class="variable">b</span>) {
  <span class="keyword">return</span> <span class="variable">a</span> <span class="operator">+</span> <span class="variable">b</span>;
}

<span class="keyword">export function</span> <span class="function">subtract</span>(<span class="variable">a</span>, <span class="variable">b</span>) {
  <span class="keyword">return</span> <span class="variable">a</span> <span class="operator">-</span> <span class="variable">b</span>;
}

<span class="keyword">export function</span> <span class="function">multiply</span>(<span class="variable">a</span>, <span class="variable">b</span>) {
  <span class="keyword">return</span> <span class="variable">a</span> <span class="operator">*</span> <span class="variable">b</span>;
}

<span class="keyword">export function</span> <span class="function">divide</span>(<span class="variable">a</span>, <span class="variable">b</span>) {
  <span class="keyword">if</span> (<span class="variable">b</span> <span class="operator">===</span> <span class="number">0</span>) {
    <span class="keyword">throw new</span> <span class="class-name">Error</span>(<span class="string">'Division par zéro impossible'</span>);
  }
  <span class="keyword">return</span> <span class="variable">a</span> <span class="operator">/</span> <span class="variable">b</span>;
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Fichier index.test.js</h4>
                        <pre><code class="language-javascript"><span class="comment">// Import des fonctions à tester</span>
<span class="keyword">import</span> { <span class="variable">add</span>, <span class="variable">subtract</span>, <span class="variable">multiply</span>, <span class="variable">divide</span> } <span class="keyword">from</span> <span class="string">'./index.js'</span>;

<span class="comment">// Import des utilitaires de test de Vitest</span>
<span class="keyword">import</span> { <span class="variable">test</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">'vitest'</span>;

<span class="comment">// Tests pour la fonction add</span>
<span class="function">test</span>(<span class="string">'additionne deux nombres'</span>, () => {
  <span class="function">expect</span>(<span class="function">add</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">5</span>);
  <span class="function">expect</span>(<span class="function">add</span>(<span class="operator">-</span><span class="number">1</span>, <span class="number">1</span>)).<span class="function">toBe</span>(<span class="number">0</span>);
  <span class="function">expect</span>(<span class="function">add</span>(<span class="number">0</span>, <span class="number">0</span>)).<span class="function">toBe</span>(<span class="number">0</span>);
});

<span class="comment">// Tests pour la fonction subtract</span>
<span class="function">test</span>(<span class="string">'soustrait deux nombres'</span>, () => {
  <span class="function">expect</span>(<span class="function">subtract</span>(<span class="number">5</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">2</span>);
  <span class="function">expect</span>(<span class="function">subtract</span>(<span class="number">0</span>, <span class="number">5</span>)).<span class="function">toBe</span>(<span class="operator">-</span><span class="number">5</span>);
});

<span class="comment">// Tests pour la fonction multiply</span>
<span class="function">test</span>(<span class="string">'multiplie deux nombres'</span>, () => {
  <span class="function">expect</span>(<span class="function">multiply</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">6</span>);
  <span class="function">expect</span>(<span class="function">multiply</span>(<span class="operator">-</span><span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="operator">-</span><span class="number">6</span>);
  <span class="function">expect</span>(<span class="function">multiply</span>(<span class="number">0</span>, <span class="number">5</span>)).<span class="function">toBe</span>(<span class="number">0</span>);
});

<span class="comment">// Tests pour la fonction divide</span>
<span class="function">test</span>(<span class="string">'divise deux nombres'</span>, () => {
  <span class="function">expect</span>(<span class="function">divide</span>(<span class="number">6</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">2</span>);
  <span class="function">expect</span>(<span class="function">divide</span>(<span class="number">5</span>, <span class="number">2</span>)).<span class="function">toBe</span>(<span class="number">2.5</span>);
});

<span class="function">test</span>(<span class="string">'lève une erreur lors d\'une division par zéro'</span>, () => {
  <span class="function">expect</span>(() => <span class="function">divide</span>(<span class="number">5</span>, <span class="number">0</span>)).<span class="function">toThrow</span>(<span class="string">'Division par zéro impossible'</span>);
});</code></pre>
                    </div>
                </div>
            </section>

            <!-- Explication des fonctions Vitest -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comprendre les fonctions de base de Vitest</h2>

                <div class="function-explanation">
                    <h3 class="text-purple">La fonction <code>test()</code></h3>
                    <p class="textExemple">
                        La fonction <code>test()</code> (ou son alias <code>it()</code>) est utilisée pour définir un
                        test individuel. Elle prend deux paramètres :
                    </p>
                    <ul class="textExemple">
                        <li><strong>Nom du test</strong> : Une chaîne de caractères descriptive qui explique ce que le
                            test vérifie</li>
                        <li><strong>Fonction de test</strong> : Une fonction qui contient la logique du test et les
                            assertions</li>
                    </ul>

                    <div class="code-example">
                        <pre><code class="language-javascript"><span class="comment">// Structure de base d'un test</span>
<span class="function">test</span>(<span class="string">'description du test'</span>, () => {
  <span class="comment">// Logique du test et assertions</span>
});</code></pre>
                    </div>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple">La fonction <code>expect()</code></h3>
                    <p class="textExemple">
                        La fonction <code>expect()</code> est utilisée pour créer une assertion. Elle prend une valeur
                        (le résultat de votre fonction) et retourne un objet qui vous permet de vérifier cette valeur
                        contre des conditions spécifiques.
                    </p>

                    <div class="code-example">
                        <pre><code class="language-javascript"><span class="comment">// expect() prend la valeur à tester</span>
<span class="function">expect</span>(<span class="function">add</span>(<span class="number">2</span>, <span class="number">3</span>))</code></pre>
                    </div>

                    <p class="textExemple">
                        Après <code>expect()</code>, vous pouvez chaîner différents <strong>matchers</strong> pour
                        vérifier différentes conditions.
                    </p>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple">Le matcher <code>toBe()</code></h3>
                    <p class="textExemple">
                        <code>toBe()</code> est un <strong>matcher</strong> qui vérifie l'égalité stricte (comme
                        <code>===</code> en JavaScript). Il est idéal pour comparer des valeurs primitives (nombres,
                        chaînes, booléens).
                    </p>

                    <div class="code-example">
                        <pre><code class="language-javascript"><span class="comment">// Vérifie que le résultat est exactement 5</span>
<span class="function">expect</span>(<span class="function">add</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">5</span>);</code></pre>
                    </div>

                    <p class="textExemple">
                        <strong>Attention</strong> : <code>toBe()</code> ne fonctionne pas bien avec les objets ou
                        tableaux. Pour ces types, utilisez <code>toEqual()</code>.
                    </p>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple">Autres matchers utiles</h3>
                    <p class="textExemple">
                        Vitest propose de nombreux matchers pour différentes situations :
                    </p>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Comparaison d'objets</h4>
                            <pre><code class="language-javascript"><span class="comment">// Pour les objets et tableaux</span>
<span class="function">expect</span>(<span class="variable">obj</span>).<span class="function">toEqual</span>({ <span class="property">name</span>: <span class="string">'John'</span> });</code></pre>
                        </div>
                        <div>
                            <h4 class="text-purple">Vérification d'erreurs</h4>
                            <pre><code class="language-javascript"><span class="comment">// Pour vérifier qu'une erreur est levée</span>
<span class="function">expect</span>(() => <span class="function">divide</span>(<span class="number">5</span>, <span class="number">0</span>)).<span class="function">toThrow</span>();</code></pre>
                        </div>
                    </div>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Vérifications de vérité</h4>
                            <pre><code class="language-javascript"><span class="comment">// Pour les valeurs truthy/falsy</span>
<span class="function">expect</span>(<span class="variable">result</span>).<span class="function">toBeTruthy</span>();
<span class="function">expect</span>(<span class="variable">result</span>).<span class="function">toBeFalsy</span>();</code></pre>
                        </div>
                        <div>
                            <h4 class="text-purple">Vérifications de null/undefined</h4>
                            <pre><code class="language-javascript"><span class="comment">// Pour les valeurs nulles ou non définies</span>
<span class="function">expect</span>(<span class="variable">value</span>).<span class="function">toBeNull</span>();
<span class="function">expect</span>(<span class="variable">value</span>).<span class="function">toBeUndefined</span>();</code></pre>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Installation de Vitest -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et configuration de Vitest</h2>
                <p class="textExemple">
                    Maintenant, installons Vitest et configurons notre projet pour exécuter les tests.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Installation de Vitest</h4>
                    <pre><code class="language-bash"><span class="function">npm install -D vitest</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Configuration du package.json</h4>
                    <pre><code class="language-json">{
  <span class="property">"name"</span>: <span class="string">"testing"</span>,
  <span class="property">"version"</span>: <span class="string">"1.0.0"</span>,
  <span class="property">"description"</span>: <span class="string">""</span>,
  <span class="property">"main"</span>: <span class="string">"index.js"</span>,
  <span class="property">"scripts"</span>: {
    <span class="property">"test"</span>: <span class="string">"vitest"</span>
  },
  <span class="property">"author"</span>: <span class="string">""</span>,
  <span class="property">"license"</span>: <span class="string">"ISC"</span>,
  <span class="property">"devDependencies"</span>: {
    <span class="property">"vitest"</span>: <span class="string">"^4.0.9"</span>
  }
}</code></pre>
                </div>

                <p class="textExemple">
                    Notez l'ajout du script <code>"test": "vitest"</code> pour exécuter les tests.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Installation des dépendances</h4>
                    <pre><code class="language-bash"><span class="function">npm install</span></code></pre>
                </div>
            </section>

            <!-- Exécution des tests -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exécution des tests</h2>
                <p class="textExemple">
                    Tout est maintenant configuré! Exécutons nos tests pour vérifier que tout fonctionne correctement.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Lancement des tests</h4>
                    <pre><code class="language-bash"><span class="function">npm run test</span></code></pre>
                </div>

                <p class="textExemple">
                    Cette commande lance Vitest en mode watch, ce qui signifie qu'il surveillera vos fichiers et
                    relancera les tests automatiquement à chaque modification.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Exécution unique des tests</h4>
                    <pre><code class="language-bash"><span class="function">npm test</span></code></pre>
                </div>

                <p class="textExemple">
                    Cette commande est équivalente à <code>npm run test</code> et exécute les tests.
                </p>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec Vitest</h2>
                <p class="textExemple">
                    Voici quelques bonnes pratiques à suivre lorsque vous écrivez des tests avec Vitest:
                </p>

                <ul class="textExemple">
                    <li>Nommez vos tests de manière descriptive</li>
                    <li>Créer un fichier par fonction pour la tester</li>
                    <li>Testez les cas limites (edge cases)</li>
                    <li>Organisez vos tests avec <code>describe</code> pour regrouper les tests liés</li>
                    <li>Utilisez les matchers appropriés (<code>toBe</code>, <code>toEqual</code>, <code>toThrow</code>,
                        etc.)</li>
                    <li>Gardez vos tests simples et isolés</li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Exemple d'organisation avec describe</h4>
                    <pre><code class="language-javascript"><span class="keyword">import</span> { <span class="variable">describe</span>, <span class="variable">test</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">'vitest'</span>;
<span class="keyword">import</span> { <span class="variable">add</span>, <span class="variable">subtract</span> } <span class="keyword">from</span> <span class="string">'./index.js'</span>;

<span class="function">describe</span>(<span class="string">'Fonctions mathématiques'</span>, () => {
  <span class="function">describe</span>(<span class="string">'add'</span>, () => {
    <span class="function">test</span>(<span class="string">'additionne deux nombres positifs'</span>, () => {
      <span class="function">expect</span>(<span class="function">add</span>(<span class="number">2</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">5</span>);
    });
    
    <span class="function">test</span>(<span class="string">'additionne un nombre positif et un négatif'</span>, () => {
      <span class="function">expect</span>(<span class="function">add</span>(<span class="operator">-</span><span class="number">1</span>, <span class="number">1</span>)).<span class="function">toBe</span>(<span class="number">0</span>);
    });
  });
  
  <span class="function">describe</span>(<span class="string">'subtract'</span>, () => {
    <span class="function">test</span>(<span class="string">'soustrait deux nombres positifs'</span>, () => {
      <span class="function">expect</span>(<span class="function">subtract</span>(<span class="number">5</span>, <span class="number">3</span>)).<span class="function">toBe</span>(<span class="number">2</span>);
    });
  });
});</code></pre>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Maintenant que vous avez compris les bases, essayez de créer vos propres tests!
                    </p>

                    <h4 class="text-purple">Consigne</h4>
                    <p class="textExemple">
                        Créez une fonction <code>isEven</code> qui prend un nombre en paramètre et retourne
                        <code>true</code> si le nombre est pair, <code>false</code> sinon. Ensuite, écrivez des tests
                        pour cette fonction en couvrant différents cas:
                    </p>

                    <ul class="textExemple">
                        <li>Nombres pairs positifs</li>
                        <li>Nombres impairs positifs</li>
                        <li>Zéro</li>
                        <li>Nombres négatifs</li>
                    </ul>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Fichier index.js</h4>
                        <pre><code class="language-javascript"><span class="keyword">export function</span> <span class="function">isEven</span>(<span class="variable">number</span>) {
  <span class="keyword">return</span> <span class="variable">number</span> <span class="operator">%</span> <span class="number">2</span> <span class="operator">===</span> <span class="number">0</span>;
}</code></pre>

                        <h4 class="text-purple">Fichier index.test.js</h4>
                        <pre><code class="language-javascript"><span class="keyword">import</span> { <span class="variable">test</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">'vitest'</span>;
<span class="keyword">import</span> { <span class="variable">isEven</span> } <span class="keyword">from</span> <span class="string">'./index.js'</span>;

<span class="function">test</span>(<span class="string">'retourne true pour les nombres pairs'</span>, () => {
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="number">2</span>)).<span class="function">toBe</span>(<span class="keyword">true</span>);
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="number">4</span>)).<span class="function">toBe</span>(<span class="keyword">true</span>);
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="number">0</span>)).<span class="function">toBe</span>(<span class="keyword">true</span>);
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="operator">-</span><span class="number">2</span>)).<span class="function">toBe</span>(<span class="keyword">true</span>);
});

<span class="function">test</span>(<span class="string">'retourne false pour les nombres impairs'</span>, () => {
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="number">1</span>)).<span class="function">toBe</span>(<span class="keyword">false</span>);
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="number">3</span>)).<span class="function">toBe</span>(<span class="keyword">false</span>);
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="operator">-</span><span class="number">1</span>)).<span class="function">toBe</span>(<span class="keyword">false</span>);
  <span class="function">expect</span>(<span class="function">isEven</span>(<span class="operator">-</span><span class="number">3</span>)).<span class="function">toBe</span>(<span class="keyword">false</span>);
});</code></pre>
                    </div>
                </details>
            </section>

            <!-- Nouvelle section: Exemple avancé avec gestion d'erreurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple avancé : Tests avec gestion d'erreurs</h2>
                <p class="textExemple">
                    Voyons maintenant un exemple plus complexe avec une fonction qui applique un pourcentage de
                    réduction à un prix, avec une gestion robuste des erreurs.
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Fichier applyPercentage.js</h4>
                        <pre><code class="language-javascript"><span class="keyword">export function</span> <span class="function">applyPercentage</span>(<span class="variable">price</span>, <span class="variable">pct</span>) {
  <span class="comment">// Vérification des types</span>
  <span class="keyword">if</span> (<span class="keyword">typeof</span> <span class="variable">price</span> !== <span class="string">'number'</span> || <span class="keyword">typeof</span> <span class="variable">pct</span> !== <span class="string">'number'</span>) {
    <span class="keyword">throw new</span> <span class="class-name">TypeError</span>(<span class="string">'numbers expected'</span>);
  }
  
  <span class="comment">// Vérification de la plage du pourcentage</span>
  <span class="keyword">if</span> (<span class="variable">pct</span> < <span class="number">0</span> || <span class="variable">pct</span> > <span class="number">100</span>) {
    <span class="keyword">throw new</span> <span class="class-name">RangeError</span>(<span class="string">'pct out of range'</span>);
  }
  
  <span class="comment">// Calcul du résultat avec arrondi à 2 décimales</span>
  <span class="keyword">const</span> <span class="variable">result</span> = <span class="variable">price</span> * (<span class="number">1</span> - <span class="variable">pct</span> / <span class="number">100</span>);
  <span class="keyword">return</span> <span class="class-name">Math</span>.<span class="function">round</span>(<span class="variable">result</span> * <span class="number">100</span>) / <span class="number">100</span>;
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Fichier applyPercentage.test.js</h4>
                        <pre><code class="language-javascript"><span class="comment">// applyPercentage.test.js</span>
<span class="keyword">import</span> { <span class="variable">applyPercentage</span> } <span class="keyword">from</span> <span class="string">"./applyPercentage"</span>;
<span class="keyword">import</span> { <span class="variable">describe</span>, <span class="variable">test</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">"vitest"</span>;

<span class="function">describe</span>(<span class="string">"test de la fonction applyPercentage"</span>, () => {
  <span class="function">test</span>(<span class="string">"test du cas nominal"</span>, () => {
    <span class="function">expect</span>(<span class="function">applyPercentage</span>(<span class="number">10</span>, <span class="number">10</span>)).<span class="function">toBe</span>(<span class="number">9</span>);
  });

  <span class="function">test</span>(<span class="string">"test avec un pourcentage de 100 et prix de 0"</span>, () => {
    <span class="function">expect</span>(<span class="function">applyPercentage</span>(<span class="number">100</span>, <span class="number">100</span>)).<span class="function">toBe</span>(<span class="number">0</span>);
  });

  <span class="function">test</span>(<span class="string">"Cas avec arrondi: 15% sur 12.99"</span>, () => {
    <span class="comment">// 12.99 - 15% = 11.0365 => 11.04</span>
    <span class="function">expect</span>(<span class="function">applyPercentage</span>(<span class="number">12.99</span>, <span class="number">15</span>)).<span class="function">toBe</span>(<span class="number">11.04</span>);
  });

  <span class="comment">// Test des types de données</span>
  <span class="function">test</span>(<span class="string">"cas avec des entrées non numériques"</span>, () => {
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="string">"100"</span>, <span class="number">10</span>)).<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>);
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">100</span>, <span class="string">"10"</span>)).<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>);
  });

  <span class="comment">// Test des plages de données</span>
  <span class="function">test</span>(<span class="string">"cas avec des entrées hors de portée pour le pct"</span>, () => {
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">10</span>, <span class="number">110</span>)).<span class="function">toThrowError</span>(<span class="class-name">RangeError</span>);
  });

  <span class="function">test</span>(<span class="string">"cas avec un nombre négatif pour le pct"</span>, () => {
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">10</span>, <span class="operator">-</span><span class="number">10</span>)).<span class="function">toThrowError</span>(<span class="class-name">RangeError</span>);
  });
});</code></pre>
                    </div>
                </div>
            </section>

            <!-- Nouvelle section: Explication des matchers toThrowError -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comprendre toThrowError(TypeError) et toThrowError(RangeError)</h2>

                <div class="function-explanation">
                    <h3 class="text-purple">Le matcher <code>toThrowError()</code></h3>
                    <p class="textExemple">
                        Le matcher <code>toThrowError()</code> est utilisé pour vérifier qu'une fonction lève une erreur
                        lorsqu'elle est exécutée. Il existe plusieurs façons de l'utiliser :
                    </p>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Vérifier qu'une erreur est levée</h4>
                            <pre><code class="language-javascript"><span class="comment">// Vérifie simplement qu'une erreur est levée</span>
<span class="function">expect</span>(() => <span class="function">maFonction</span>()).<span class="function">toThrowError</span>();</code></pre>
                        </div>
                        <div>
                            <h4 class="text-purple">Vérifier le message d'erreur</h4>
                            <pre><code class="language-javascript"><span class="comment">// Vérifie le message d'erreur exact</span>
<span class="function">expect</span>(() => <span class="function">maFonction</span>())
  .<span class="function">toThrowError</span>(<span class="string">'message d\\'erreur spécifique'</span>);</code></pre>
                        </div>
                    </div>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Vérifier le type d'erreur</h4>
                            <pre><code class="language-javascript"><span class="comment">// Vérifie le type d'erreur (TypeError, RangeError, etc.)</span>
<span class="function">expect</span>(() => <span class="function">maFonction</span>())
  .<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>);</code></pre>
                        </div>
                        <div>
                            <h4 class="text-purple">Vérifier type et message</h4>
                            <pre><code class="language-javascript"><span class="comment">// Vérifie le type et le message d'erreur</span>
<span class="function">expect</span>(() => <span class="function">maFonction</span>())
  .<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>, <span class="string">'message spécifique'</span>);</code></pre>
                        </div>
                    </div>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple"><code>toThrowError(TypeError)</code></h3>
                    <p class="textExemple">
                        <code>toThrowError(TypeError)</code> vérifie qu'une fonction lève spécifiquement une erreur de
                        type <strong>TypeError</strong>. Ce type d'erreur est généralement utilisé lorsque :
                    </p>

                    <ul class="textExemple">
                        <li>Un argument a un type incorrect</li>
                        <li>Une opération est effectuée sur un type de données incompatible</li>
                        <li>Une fonction est appelée avec des paramètres de mauvais type</li>
                    </ul>

                    <div class="code-example">
                        <h4 class="text-purple">Exemple dans applyPercentage</h4>
                        <pre><code class="language-javascript"><span class="comment">// Dans la fonction : vérification des types</span>
<span class="keyword">if</span> (<span class="keyword">typeof</span> <span class="variable">price</span> !== <span class="string">'number'</span> || <span class="keyword">typeof</span> <span class="variable">pct</span> !== <span class="string">'number'</span>) {
  <span class="keyword">throw new</span> <span class="class-name">TypeError</span>(<span class="string">'numbers expected'</span>);
}

<span class="comment">// Dans le test : vérification que TypeError est levée</span>
<span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="string">"100"</span>, <span class="number">10</span>))
  .<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>);</code></pre>
                    </div>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple"><code>toThrowError(RangeError)</code></h3>
                    <p class="textExemple">
                        <code>toThrowError(RangeError)</code> vérifie qu'une fonction lève spécifiquement une erreur de
                        type <strong>RangeError</strong>. Ce type d'erreur est généralement utilisé lorsque :
                    </p>

                    <ul class="textExemple">
                        <li>Une valeur numérique est en dehors de sa plage autorisée</li>
                        <li>Un index est en dehors des limites d'un tableau</li>
                        <li>Une valeur ne respecte pas les contraintes de domaine</li>
                    </ul>

                    <div class="code-example">
                        <h4 class="text-purple">Exemple dans applyPercentage</h4>
                        <pre><code class="language-javascript"><span class="comment">// Dans la fonction : vérification de la plage</span>
<span class="keyword">if</span> (<span class="variable">pct</span> < <span class="number">0</span> || <span class="variable">pct</span> > <span class="number">100</span>) {
  <span class="keyword">throw new</span> <span class="class-name">RangeError</span>(<span class="string">'pct out of range'</span>);
}

<span class="comment">// Dans le test : vérification que RangeError est levée</span>
<span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">10</span>, <span class="number">110</span>))
  .<span class="function">toThrowError</span>(<span class="class-name">RangeError</span>);</code></pre>
                    </div>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple">Pourquoi utiliser des types d'erreur spécifiques ?</h3>
                    <p class="textExemple">
                        L'utilisation de types d'erreur spécifiques comme <code>TypeError</code> et
                        <code>RangeError</code> plutôt que le générique <code>Error</code> offre plusieurs avantages :
                    </p>

                    <ul class="textExemple">
                        <li><strong>Meilleure sémantique</strong> : Le type d'erreur indique la nature du problème</li>
                        <li><strong>Gestion d'erreurs plus précise</strong> : Permet de catcher des types d'erreurs
                            spécifiques</li>
                        <li><strong>Meilleure documentation</strong> : Le code est plus lisible et compréhensible</li>
                        <li><strong>Tests plus robustes</strong> : Permet de vérifier non seulement qu'une erreur est
                            levée, mais aussi qu'elle est du bon type</li>
                    </ul>

                    <div class="code-example">
                        <h4 class="text-purple">Exemple de gestion d'erreurs spécifiques</h4>
                        <pre><code class="language-javascript"><span class="keyword">try</span> {
  <span class="function">applyPercentage</span>(<span class="string">"invalid"</span>, <span class="number">10</span>);
} <span class="keyword">catch</span> (<span class="variable">error</span>) {
  <span class="keyword">if</span> (<span class="variable">error</span> <span class="keyword">instanceof</span> <span class="class-name">TypeError</span>) {
    <span class="comment">// Gestion spécifique des erreurs de type</span>
    <span class="function">afficherMessageErreur</span>(<span class="string">'Veuillez entrer des nombres valides'</span>);
  } <span class="keyword">else if</span> (<span class="variable">error</span> <span class="keyword">instanceof</span> <span class="class-name">RangeError</span>) {
    <span class="comment">// Gestion spécifique des erreurs de plage</span>
    <span class="function">afficherMessageErreur</span>(<span class="string">'Le pourcentage doit être entre 0 et 100'</span>);
  }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Nouvelle section: Bonnes pratiques pour les tests d'erreurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques pour tester les erreurs</h2>

                <div class="function-explanation">
                    <h3 class="text-purple">Structure des tests d'erreurs</h3>
                    <p class="textExemple">
                        Lorsque vous testez des fonctions qui peuvent lever des erreurs, suivez ces bonnes pratiques :
                    </p>

                    <ul class="textExemple">
                        <li><strong>Utilisez une fonction fléchée</strong> : Pour tester qu'une erreur est levée, vous
                            devez passer une fonction à <code>expect()</code></li>
                        <li><strong>Testez tous les cas d'erreur</strong> : Vérifiez chaque condition qui peut mener à
                            une erreur</li>
                        <li><strong>Utilisez des types d'erreur appropriés</strong> : Choisissez le type d'erreur qui
                            correspond le mieux à la situation</li>
                        <li><strong>Testez les messages d'erreur</strong> : Les messages doivent être clairs et
                            informatifs</li>
                    </ul>

                    <div class="code-example">
                        <h4 class="text-purple">Exemple complet de test d'erreurs</h4>
                        <pre><code class="language-javascript"><span class="function">describe</span>(<span class="string">"Gestion des erreurs"</span>, () => {
  <span class="function">test</span>(<span class="string">"lève TypeError pour les entrées non numériques"</span>, () => {
    <span class="comment">// Test avec une chaîne pour le prix</span>
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="string">"100"</span>, <span class="number">10</span>))
      .<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>);
    
    <span class="comment">// Test avec une chaîne pour le pourcentage</span>
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">100</span>, <span class="string">"10"</span>))
      .<span class="function">toThrowError</span>(<span class="class-name">TypeError</span>);
  });

  <span class="function">test</span>(<span class="string">"lève RangeError pour les pourcentages invalides"</span>, () => {
    <span class="comment">// Test avec pourcentage trop élevé</span>
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">10</span>, <span class="number">110</span>))
      .<span class="function">toThrowError</span>(<span class="class-name">RangeError</span>);
    
    <span class="comment">// Test avec pourcentage négatif</span>
    <span class="function">expect</span>(() => <span class="function">applyPercentage</span>(<span class="number">10</span>, <span class="operator">-</span><span class="number">10</span>))
      .<span class="function">toThrowError</span>(<span class="class-name">RangeError</span>);
  });
});</code></pre>
                    </div>
                </div>
            </section>
            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Félicitations ! Vous avez maintenant acquis une compréhension approfondie des tests unitaires avec
                    Vitest. Vous maîtrisez désormais :
                </p>

                <ul class="textExemple">
                    <li><strong>Les bases de Vitest</strong> : Configuration, écriture et exécution de tests</li>
                    <li><strong>Les fonctions essentielles</strong> : <code>test()</code>, <code>expect()</code> et les
                        principaux matchers comme <code>toBe()</code></li>
                    <li><strong>L'organisation des tests</strong> : Utilisation de <code>describe()</code> pour
                        structurer vos suites de tests</li>
                    <li><strong>La gestion des erreurs avancée</strong> : Tests avec <code>toThrowError()</code> pour
                        différents types d'erreurs</li>
                </ul>

                <div class="function-explanation">
                    <h3 class="text-purple">Points clés sur la gestion d'erreurs</h3>
                    <p class="textExemple">
                        Vous avez appris à tester spécifiquement différents types d'erreurs :
                    </p>

                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">TypeError</h4>
                            <ul class="textExemple">
                                <li>Pour les types de données incorrects</li>
                                <li>Exemple : arguments non numériques</li>
                                <li>Test : <code>toThrowError(TypeError)</code></li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-purple">RangeError</h4>
                            <ul class="textExemple">
                                <li>Pour les valeurs hors plage autorisée</li>
                                <li>Exemple : pourcentages invalides</li>
                                <li>Test : <code>toThrowError(RangeError)</code></li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple">Bonnes pratiques consolidées</h3>
                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Écriture des tests</h4>
                            <ul class="textExemple">
                                <li>Nommez les tests de manière descriptive</li>
                                <li>Testez les cas nominaux ET les cas d'erreur</li>
                                <li>Utilisez <code>describe</code> pour organiser les tests</li>
                                <li>Créez un fichier de test par fonction/module</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-purple">Gestion des erreurs</h4>
                            <ul class="textExemple">
                                <li>Utilisez des types d'erreur spécifiques</li>
                                <li>Testez tous les scénarios d'erreur possibles</li>
                                <li>Vérifiez les messages d'erreur pour la clarté</li>
                                <li>Utilisez des fonctions fléchées pour tester les erreurs</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div class="function-explanation">
                    <h3 class="text-purple">Prochaines étapes</h3>
                    <p class="textExemple">
                        Pour approfondir vos connaissances, explorez ces concepts avancés :
                    </p>

                    <ul class="textExemple">
                        <li><strong>Tests asynchrones</strong> : Fonctions async/await avec Vitest</li>
                        <li><strong>Mocks et spies</strong> : Simuler des dépendances externes</li>
                        <li><strong>Tests de composants</strong> : Testing Library pour les composants Vue</li>
                        <li><strong>Couverture de code</strong> : Mesurer l'efficacité de vos tests</li>
                        <li><strong>Tests d'intégration</strong> : Tester plusieurs modules ensemble</li>
                    </ul>
                </div>

                <p class="textExemple">
                    <strong>Rappel important</strong> : Les tests ne sont pas une fin en soi, mais un moyen d'atteindre
                    plusieurs objectifs cruciaux :
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Avantages des tests</h4>
                        <ul class="textExemple">
                            <li>✅ Détection précoce des bugs</li>
                            <li>✅ Documentation vivante du code</li>
                            <li>✅ Confiance lors des refactorisations</li>
                            <li>✅ Meilleure conception du code</li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="text-purple">Dans votre projet</h4>
                        <ul class="textExemple">
                            <li> Testez vos fonctions utilitaires</li>
                            <li> Vérifiez les cas limites</li>
                            <li> Couvrez les chemins d'erreur</li>
                            <li> Maintenez vos tests à jour</li>
                        </ul>
                    </div>
                </div>

                <p class="textExemple">
                    Continuez à pratiquer en ajoutant des tests à vos projets existants. Commencez par les fonctions les
                    plus critiques, puis étendez progressivement votre couverture de tests. Plus vous écrirez de tests,
                    plus vous développerez votre intuition pour anticiper les cas problématiques et créer du code plus
                    robuste et maintenable !
                </p>
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

/* Styles pour les explications de fonctions */
.function-explanation {
    margin-bottom: 2rem;
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

.function-explanation h3 {
    margin-top: 0;
    margin-bottom: 1rem;
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
.property {
    color: #9cdcfe !important;
}

/* Propriétés d'objets */

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

    .function-explanation {
        padding: 1rem;
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

    .function-explanation {
        padding: 0.75rem;
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