<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Typage en PHP</h1>
        <p class="lesson-meta text-white">Types de données, déclarations de type et bonnes pratiques</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction au typage en PHP</h2>
        <p class="textExemple">
          PHP est un langage à typage dynamique et faible. Cependant, depuis PHP 7, le langage a introduit 
          des déclarations de type strictes qui permettent un meilleur contrôle des types de données.
        </p>
        <p class="textExemple">
          Comprendre le typage est essentiel pour écrire du code robuste, maintenable et moins sujet aux erreurs.
        </p>
      </section>

      <!-- Types scalaires -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types scalaires de base</h2>
        <p class="textExemple">
          PHP supporte plusieurs types de données scalaires :
        </p>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Types numériques</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Entier (int)</span>
<span class="variable">$age</span> = <span class="number">25</span>;
<span class="variable">$temperature</span> = -<span class="number">5</span>;

<span class="comment">// Nombre à virgule flottante (float/double)</span>
<span class="variable">$prix</span> = <span class="number">19.99</span>;
<span class="variable">$pourcentage</span> = <span class="number">0.15</span>;

<span class="comment">// Vérification des types</span>
<span class="function">var_dump</span>(<span class="function">is_int</span>(<span class="variable">$age</span>));        <span class="comment">// bool(true)</span>
<span class="function">var_dump</span>(<span class="function">is_float</span>(<span class="variable">$prix</span>));     <span class="comment">// bool(true)</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Chaînes et booléens</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Chaîne de caractères (string)</span>
<span class="variable">$nom</span> = <span class="string">"Jean Dupont"</span>;
<span class="variable">$message</span> = <span class="string">'Bonjour le monde'</span>;

<span class="comment">// Booléen (bool)</span>
<span class="variable">$estActif</span> = <span class="keyword">true</span>;
<span class="variable">$estVide</span> = <span class="keyword">false</span>;

<span class="comment">// Vérification des types</span>
<span class="function">var_dump</span>(<span class="function">is_string</span>(<span class="variable">$nom</span>));     <span class="comment">// bool(true)</span>
<span class="function">var_dump</span>(<span class="function">is_bool</span>(<span class="variable">$estActif</span>));  <span class="comment">// bool(true)</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Types composés -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types composés</h2>
        <p class="textExemple">
          PHP supporte également des types de données plus complexes :
        </p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Tableau (array)</span>
<span class="variable">$fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];
<span class="variable">$personne</span> = [
    <span class="string">"nom"</span> =&gt; <span class="string">"Alice"</span>,
    <span class="string">"age"</span> =&gt; <span class="number">30</span>,
    <span class="string">"ville"</span> =&gt; <span class="string">"Paris"</span>
];

<span class="comment">// Objet (object)</span>
<span class="keyword">class</span> <span class="class-name">Utilisateur</span> {
    <span class="keyword">public</span> <span class="variable">$nom</span>;
    <span class="keyword">public</span> <span class="variable">$email</span>;
}
<span class="variable">$user</span> = <span class="keyword">new</span> <span class="class-name">Utilisateur</span>();

<span class="comment">// Vérifications</span>
<span class="function">var_dump</span>(<span class="function">is_array</span>(<span class="variable">$fruits</span>));   <span class="comment">// bool(true)</span>
<span class="function">var_dump</span>(<span class="function">is_object</span>(<span class="variable">$user</span>));   <span class="comment">// bool(true)</span></code></pre>
        </div>
      </section>

      <!-- Types spéciaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types spéciaux</h2>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Null</span>
<span class="variable">$variableNulle</span> = <span class="keyword">null</span>;
<span class="function">var_dump</span>(<span class="function">is_null</span>(<span class="variable">$variableNulle</span>));  <span class="comment">// bool(true)</span>

<span class="comment">// Ressource</span>
<span class="variable">$fichier</span> = <span class="function">fopen</span>(<span class="string">'test.txt'</span>, <span class="string">'r'</span>);
<span class="function">var_dump</span>(<span class="function">is_resource</span>(<span class="variable">$fichier</span>));      <span class="comment">// bool(true)</span>
<span class="function">fclose</span>(<span class="variable">$fichier</span>);

<span class="comment">// Callable</span>
<span class="variable">$maFonction</span> = <span class="keyword">function</span>(<span class="variable">$x</span>) { <span class="keyword">return</span> <span class="variable">$x</span> * <span class="number">2</span>; };
<span class="function">var_dump</span>(<span class="function">is_callable</span>(<span class="variable">$maFonction</span>));  <span class="comment">// bool(true)</span>

<span class="comment">// Iterable (PHP 7.1+)</span>
<span class="variable">$tableauIterable</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>];
<span class="function">var_dump</span>(<span class="function">is_iterable</span>(<span class="variable">$tableauIterable</span>)); <span class="comment">// bool(true)</span></code></pre>
        </div>
      </section>

      <!-- Déclarations de type -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Déclarations de type (Type Hints)</h2>
        <p class="textExemple">
          Depuis PHP 7, vous pouvez spécifier le type des paramètres et des valeurs de retour :
        </p>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Types scalaires</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Déclaration de type pour les paramètres</span>
<span class="keyword">function</span> <span class="function">additionner</span>(<span class="keyword">int</span> <span class="variable">$a</span>, <span class="keyword">int</span> <span class="variable">$b</span>): <span class="keyword">int</span> {
    <span class="keyword">return</span> <span class="variable">$a</span> + <span class="variable">$b</span>;
}

<span class="keyword">function</span> <span class="function">formaterMessage</span>(<span class="keyword">string</span> <span class="variable">$nom</span>, <span class="keyword">float</span> <span class="variable">$score</span>): <span class="keyword">string</span> {
    <span class="keyword">return</span> <span class="string">"<span class="variable">$nom</span> a un score de <span class="variable">$score</span>"</span>;
}

<span class="keyword">echo</span> <span class="function">additionner</span>(<span class="number">5</span>, <span class="number">3</span>);          <span class="comment">// 8</span>
<span class="keyword">echo</span> <span class="function">formaterMessage</span>(<span class="string">"Alice"</span>, <span class="number">95.5</span>);</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Types composés</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Tableaux et objets</span>
<span class="keyword">function</span> <span class="function">traiterTableau</span>(<span class="keyword">array</span> <span class="variable">$data</span>): <span class="keyword">array</span> {
    <span class="keyword">return</span> <span class="function">array_map</span>(<span class="string">'strtoupper'</span>, <span class="variable">$data</span>);
}

<span class="keyword">class</span> <span class="class-name">Personne</span> {
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">sePresenter</span>(): <span class="keyword">string</span> {
        <span class="keyword">return</span> <span class="string">"Je suis une personne"</span>;
    }
}

<span class="keyword">function</span> <span class="function">saluterPersonne</span>(<span class="class-name">Personne</span> <span class="variable">$personne</span>): <span class="keyword">string</span> {
    <span class="keyword">return</span> <span class="string">"Bonjour, "</span> . <span class="variable">$personne</span>-&gt;sePresenter();
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Mode strict vs coercitif -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Mode strict vs coercitif</h2>
        <p class="textExemple">
          PHP offre deux modes pour le typage : coercitif (par défaut) et strict.
        </p>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Mode coercitif (défaut)</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// PHP tentera de convertir les types</span>
<span class="keyword">function</span> <span class="function">additionner</span>(<span class="keyword">int</span> <span class="variable">$a</span>, <span class="keyword">int</span> <span class="variable">$b</span>): <span class="keyword">int</span> {
    <span class="keyword">return</span> <span class="variable">$a</span> + <span class="variable">$b</span>;
}

<span class="comment">// Conversion automatique</span>
<span class="keyword">echo</span> <span class="function">additionner</span>(<span class="string">"5"</span>, <span class="string">"3"</span>);     <span class="comment">// 8 - conversion en int</span>
<span class="keyword">echo</span> <span class="function">additionner</span>(<span class="number">5.7</span>, <span class="number">3.2</span>);    <span class="comment">// 8 - troncature en int</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">Mode strict</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Doit être la première instruction du fichier</span>
<span class="function">declare</span>(strict_types=<span class="number">1</span>);

<span class="keyword">function</span> <span class="function">additionnerStrict</span>(<span class="keyword">int</span> <span class="variable">$a</span>, <span class="keyword">int</span> <span class="variable">$b</span>): <span class="keyword">int</span> {
    <span class="keyword">return</span> <span class="variable">$a</span> + <span class="variable">$b</span>;
}

<span class="comment">// Erreur en mode strict !</span>
<span class="comment">// echo additionnerStrict("5", "3"); // TypeError</span>
<span class="keyword">echo</span> <span class="function">additionnerStrict</span>(<span class="number">5</span>, <span class="number">3</span>);    <span class="comment">// 8 - fonctionne</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Types union -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types union (PHP 8.0+)</h2>
        <p class="textExemple">
          PHP 8 a introduit les types union, permettant à un paramètre ou retour d'accepter plusieurs types.
        </p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Types union avec |</span>
<span class="keyword">function</span> <span class="function">formaterValeur</span>(<span class="keyword">string</span>|<span class="keyword">int</span>|<span class="keyword">float</span> <span class="variable">$valeur</span>): <span class="keyword">string</span> {
    <span class="keyword">return</span> (<span class="keyword">string</span>)<span class="variable">$valeur</span>;
}

<span class="keyword">function</span> <span class="function">traiterReponse</span>(<span class="keyword">array</span>|<span class="keyword">string</span>|<span class="keyword">null</span> <span class="variable">$data</span>): <span class="keyword">void</span> {
    <span class="keyword">if</span> (<span class="function">is_array</span>(<span class="variable">$data</span>)) {
        <span class="function">print_r</span>(<span class="variable">$data</span>);
    } <span class="keyword">elseif</span> (<span class="function">is_string</span>(<span class="variable">$data</span>)) {
        <span class="keyword">echo</span> <span class="variable">$data</span>;
    } <span class="keyword">else</span> {
        <span class="keyword">echo</span> <span class="string">"Aucune donnée"</span>;
    }
}

<span class="comment">// Utilisation</span>
<span class="function">formaterValeur</span>(<span class="number">42</span>);           <span class="comment">// "42"</span>
<span class="function">formaterValeur</span>(<span class="number">3.14</span>);         <span class="comment">// "3.14"</span>
<span class="function">formaterValeur</span>(<span class="string">"hello"</span>);      <span class="comment">// "hello"</span></code></pre>
        </div>
      </section>

      <!-- Type mixed -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Type mixed (PHP 8.0+)</h2>
        <p class="textExemple">
          Le type <code>mixed</code> est un alias pour plusieurs types et est équivalent à <code>array|bool|callable|int|float|null|object|resource|string</code>.
        </p>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// mixed accepte n'importe quel type</span>
<span class="keyword">function</span> <span class="function">logger</span>(<span class="keyword">mixed</span> <span class="variable">$message</span>): <span class="keyword">void</span> {
    <span class="variable">$timestamp</span> = <span class="function">date</span>(<span class="string">'Y-m-d H:i:s'</span>);
    <span class="variable">$logMessage</span> = <span class="string">"[<span class="variable">$timestamp</span>] "</span> . <span class="function">print_r</span>(<span class="variable">$message</span>, <span class="keyword">true</span>);
    <span class="keyword">echo</span> <span class="variable">$logMessage</span> . <span class="string">"<span class="operator">&lt;</span>br<span class="operator">&gt;</span>"</span>;
}

<span class="comment">// Tous ces appels sont valides</span>
<span class="function">logger</span>(<span class="string">"Message texte"</span>);
<span class="function">logger</span>(<span class="number">42</span>);
<span class="function">logger</span>([<span class="string">"data"</span> =&gt; <span class="string">"value"</span>]);
<span class="function">logger</span>(<span class="keyword">null</span>);
<span class="function">logger</span>(<span class="keyword">new</span> <span class="class-name">stdClass</span>());</code></pre>
        </div>
      </section>

      <!-- Retour void et never -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de retour void et never</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">void</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// void : la fonction ne retourne rien</span>
<span class="keyword">function</span> <span class="function">afficherMessage</span>(<span class="keyword">string</span> <span class="variable">$message</span>): <span class="keyword">void</span> {
    <span class="keyword">echo</span> <span class="variable">$message</span>;
    <span class="comment">// Pas de return ou return; sans valeur</span>
}

<span class="keyword">function</span> <span class="function">enregistrerLog</span>(<span class="keyword">string</span> <span class="variable">$log</span>): <span class="keyword">void</span> {
    <span class="function">file_put_contents</span>(<span class="string">'app.log'</span>, <span class="variable">$log</span> . <span class="string">"<span class="operator">&lt;</span>br<span class="operator">&gt;</span>"</span>, FILE_APPEND);
    <span class="keyword">return</span>; <span class="comment">// Optionnel</span>
}</code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">never (PHP 8.1+)</h4>
            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// never : la fonction ne termine pas normalement</span>
<span class="keyword">function</span> <span class="function">rediriger</span>(<span class="keyword">string</span> <span class="variable">$url</span>): <span class="keyword">never</span> {
    <span class="function">header</span>(<span class="string">"Location: <span class="variable">$url</span>"</span>);
    <span class="keyword">exit</span>(); <span class="comment">// Le script s'arrête ici</span>
}

<span class="keyword">function</span> <span class="function">lancerException</span>(<span class="keyword">string</span> <span class="variable">$message</span>): <span class="keyword">never</span> {
    <span class="keyword">throw new</span> <span class="class-name">Exception</span>(<span class="variable">$message</span>);
    <span class="comment">// Le code après throw n'est jamais exécuté</span>
}

<span class="comment">// rediriger("https://example.com"); // Arrête le script</span>
<span class="comment">// lancerException("Erreur critique"); // Lance une exception</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Vérifications et conversions -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Vérifications et conversions de type</h2>
        
        <div class="code-example">
          <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Fonctions de vérification</span>
<span class="variable">$valeur</span> = <span class="string">"123"</span>;

<span class="function">var_dump</span>(<span class="function">is_int</span>(<span class="variable">$valeur</span>));        <span class="comment">// bool(false)</span>
<span class="function">var_dump</span>(<span class="function">is_numeric</span>(<span class="variable">$valeur</span>));    <span class="comment">// bool(true)</span>
<span class="function">var_dump</span>(<span class="function">ctype_digit</span>(<span class="variable">$valeur</span>));    <span class="comment">// bool(true)</span>

<span class="comment">// Conversion de types</span>
<span class="variable">$nombre</span> = (<span class="keyword">int</span>)<span class="variable">$valeur</span>;           <span class="comment">// 123</span>
<span class="variable">$texte</span> = (<span class="keyword">string</span>)<span class="number">456</span>;             <span class="comment">// "456"</span>
<span class="variable">$booleen</span> = (<span class="keyword">bool</span>)<span class="string">""</span>;             <span class="comment">// false</span>

<span class="comment">// Fonctions de conversion</span>
<span class="variable">$entier</span> = <span class="function">intval</span>(<span class="variable">$valeur</span>);        <span class="comment">// 123</span>
<span class="variable">$chaine</span> = <span class="function">strval</span>(<span class="number">789</span>);            <span class="comment">// "789"</span>
<span class="variable">$bool</span> = <span class="function">boolval</span>(<span class="string">"hello"</span>);        <span class="comment">// true</span>

<span class="comment">// gettype() et settype()</span>
<span class="function">var_dump</span>(<span class="function">gettype</span>(<span class="variable">$valeur</span>));       <span class="comment">// string(6) "string"</span>
<span class="function">settype</span>(<span class="variable">$valeur</span>, <span class="string">"int"</span>);
<span class="function">var_dump</span>(<span class="function">gettype</span>(<span class="variable">$valeur</span>));       <span class="comment">// string(3) "integer"</span></code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        <div class="exercise">
          <p class="textExemple">
            <strong>Objectif :</strong> Créez une classe <code>Validateur</code> avec les méthodes suivantes :
          </p>
          <ul class="textExemple">
            <li><code>estEmailValide(string $email): bool</code> - vérifie si un email est valide</li>
            <li><code>filtrerNombres(array $data): array</code> - retourne seulement les nombres du tableau</li>
            <li><code>convertirEnTableau(mixed $valeur): array</code> - convertit une valeur en tableau</li>
            <li><code>calculerMoyenne(array $nombres): ?float</code> - calcule la moyenne ou retourne null si vide</li>
          </ul>
          <p class="textExemple">
            Utilisez les déclarations de type appropriées et gérez les différents cas.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">&lt;?php</span>
<span class="keyword">class</span> <span class="class-name">Validateur</span> {
    
    <span class="keyword">public static function</span> <span class="function">estEmailValide</span>(<span class="keyword">string</span> <span class="variable">$email</span>): <span class="keyword">bool</span> {
        <span class="keyword">return</span> <span class="function">filter_var</span>(<span class="variable">$email</span>, FILTER_VALIDATE_EMAIL) !== <span class="keyword">false</span>;
    }
    
    <span class="keyword">public static function</span> <span class="function">filtrerNombres</span>(<span class="keyword">array</span> <span class="variable">$data</span>): <span class="keyword">array</span> {
        <span class="keyword">return</span> <span class="function">array_filter</span>(<span class="variable">$data</span>, <span class="keyword">function</span>(<span class="variable">$valeur</span>) {
            <span class="keyword">return</span> <span class="function">is_numeric</span>(<span class="variable">$valeur</span>);
        });
    }
    
    <span class="keyword">public static function</span> <span class="function">convertirEnTableau</span>(<span class="keyword">mixed</span> <span class="variable">$valeur</span>): <span class="keyword">array</span> {
        <span class="keyword">if</span> (<span class="function">is_array</span>(<span class="variable">$valeur</span>)) {
            <span class="keyword">return</span> <span class="variable">$valeur</span>;
        } <span class="keyword">elseif</span> (<span class="function">is_scalar</span>(<span class="variable">$valeur</span>)) {
            <span class="keyword">return</span> [<span class="variable">$valeur</span>];
        } <span class="keyword">else</span> {
            <span class="keyword">return</span> (<span class="keyword">array</span>)<span class="variable">$valeur</span>;
        }
    }
    
    <span class="keyword">public static function</span> <span class="function">calculerMoyenne</span>(<span class="keyword">array</span> <span class="variable">$nombres</span>): ?<span class="keyword">float</span> {
        <span class="variable">$nombresFiltres</span> = <span class="function">array_filter</span>(<span class="variable">$nombres</span>, <span class="string">'is_numeric'</span>);
        
        <span class="keyword">if</span> (<span class="function">empty</span>(<span class="variable">$nombresFiltres</span>)) {
            <span class="keyword">return</span> <span class="keyword">null</span>;
        }
        
        <span class="variable">$somme</span> = <span class="function">array_sum</span>(<span class="variable">$nombresFiltres</span>);
        <span class="variable">$count</span> = <span class="function">count</span>(<span class="variable">$nombresFiltres</span>);
        
        <span class="keyword">return</span> <span class="variable">$somme</span> / <span class="variable">$count</span>;
    }
}

<span class="comment">// Tests</span>
<span class="function">var_dump</span>(<span class="class-name">Validateur</span>::estEmailValide(<span class="string">"test@example.com"</span>)); <span class="comment">// true</span>
<span class="function">var_dump</span>(<span class="class-name">Validateur</span>::estEmailValide(<span class="string">"invalid-email"</span>));   <span class="comment">// false</span>

<span class="variable">$donnees</span> = [<span class="number">1</span>, <span class="string">"2"</span>, <span class="string">"abc"</span>, <span class="number">3.5</span>, <span class="string">"4"</span>];
<span class="function">var_dump</span>(<span class="class-name">Validateur</span>::filtrerNombres(<span class="variable">$donnees</span>)); <span class="comment">// [1, "2", 3.5, "4"]</span>

<span class="function">var_dump</span>(<span class="class-name">Validateur</span>::calculerMoyenne([<span class="number">10</span>, <span class="number">20</span>, <span class="number">30</span>])); <span class="comment">// 20.0</span>
<span class="function">var_dump</span>(<span class="class-name">Validateur</span>::calculerMoyenne([]));        <span class="comment">// null</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Résumé -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">Résumé</h2>
        <div class="text-white">
          <ul>
            <li>PHP est à typage dynamique mais supporte les déclarations de type depuis PHP 7</li>
            <li>Utilisez <code>declare(strict_types=1)</code> pour activer le mode strict</li>
            <li>Les types union (|) permettent d'accepter plusieurs types</li>
            <li><code>mixed</code> accepte n'importe quel type</li>
            <li><code>void</code> pour les fonctions sans retour, <code>never</code> pour celles qui ne terminent pas</li>
            <li>Les déclarations de type améliorent la robustesse et la maintenabilité du code</li>
          </ul>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonTypagePHP',
  data() {
    return {
      lessonTitle: 'Typage en PHP'
    }
  },
  head() {
    return {
      title: this.lessonTitle,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Comprendre et maîtriser le typage en PHP : types scalaires, déclarations de type, mode strict, types union et bonnes pratiques'
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