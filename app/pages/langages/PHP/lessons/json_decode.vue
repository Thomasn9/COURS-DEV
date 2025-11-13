<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">La fonction json_decode() en PHP</h1>
        <p class="lesson-meta text-white">Conversion et manipulation de données JSON en PHP</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p class="textExemple">
          La fonction <code>json_decode()</code> est la fonction complémentaire de <code>json_encode()</code> en PHP. 
          Elle permet de convertir une chaîne de caractères au format JSON en variables PHP (tableaux ou objets). 
          Cette fonction est essentielle pour traiter les données JSON reçues d'API externes, de requêtes AJAX, ou de fichiers de configuration.
        </p>
      </section>

      <!-- Syntaxe de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de base</h2>
        <p class="textExemple">
          La syntaxe de la fonction <code>json_decode()</code> est la suivante :
        </p>
        <div class="code-example">
          <pre><code><span class="function">json_decode</span>(<span class="variable">$json</span>[, <span class="variable">$associative</span> = <span class="keyword">false</span>[, <span class="variable">$depth</span> = <span class="number">512</span>[, <span class="variable">$options</span> = <span class="number">0</span>]]]) : <span class="keyword">mixed</span></code></pre>
        </div>
        <p class="textExemple">
          <strong>Paramètres :</strong>
        </p>
        <ul class="textExemple">
          <li><code><span class="variable">$json</span></code> : La chaîne JSON à décoder</li>
          <li><code><span class="variable">$associative</span></code> : Si <code><span class="keyword">true</span></code>, retourne un tableau associatif au lieu d'un objet (optionnel)</li>
          <li><code><span class="variable">$depth</span></code> : Profondeur maximale de décodage (optionnel)</li>
          <li><code><span class="variable">$options</span></code> : Options de décodage (optionnel)</li>
        </ul>
        <p class="textExemple">
          <strong>Valeur de retour :</strong> La valeur décodée ou <code><span class="keyword">null</span></code> en cas d'échec.
        </p>
      </section>

      <!-- Exemples d'utilisation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples d'utilisation</h2>
        
        <h3 class="text-purple">1. Décoder en objet (comportement par défaut)</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="variable">$json</span> = <span class="string">'{"nom":"Dupont","prenom":"Jean","age":30,"ville":"Paris"}'</span>;

<span class="variable">$objet</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>);

<span class="function">echo</span> <span class="variable">$objet</span>-><span class="variable">nom</span>;      <span class="comment">// Affiche "Dupont"</span>
<span class="function">echo</span> <span class="variable">$objet</span>-><span class="variable">prenom</span>;   <span class="comment">// Affiche "Jean"</span>
<span class="function">echo</span> <span class="variable">$objet</span>-><span class="variable">age</span>;      <span class="comment">// Affiche 30</span></code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Structure résultante</h4>
            <pre><code><span class="class-name">stdClass</span> <span class="variable">Object</span>
(
    [<span class="variable">nom</span>] => <span class="string">Dupont</span>
    [<span class="variable">prenom</span>] => <span class="string">Jean</span>
    [<span class="variable">age</span>] => <span class="number">30</span>
    [<span class="variable">ville</span>] => <span class="string">Paris</span>
)</code></pre>
          </div>
        </div>

        <h3 class="text-purple">2. Décoder en tableau associatif</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="variable">$json</span> = <span class="string">'{"nom":"Dupont","prenom":"Jean","age":30,"ville":"Paris"}'</span>;

<span class="variable">$tableau</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>, <span class="keyword">true</span>);

<span class="function">echo</span> <span class="variable">$tableau</span>[<span class="string">'nom'</span>];    <span class="comment">// Affiche "Dupont"</span>
<span class="function">echo</span> <span class="variable">$tableau</span>[<span class="string">'prenom'</span>]; <span class="comment">// Affiche "Jean"</span>
<span class="function">echo</span> <span class="variable">$tableau</span>[<span class="string">'age'</span>];    <span class="comment">// Affiche 30</span></code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Structure résultante</h4>
            <pre><code><span class="variable">Array</span>
(
    [<span class="variable">nom</span>] => <span class="string">Dupont</span>
    [<span class="variable">prenom</span>] => <span class="string">Jean</span>
    [<span class="variable">age</span>] => <span class="number">30</span>
    [<span class="variable">ville</span>] => <span class="string">Paris</span>
)</code></pre>
          </div>
        </div>

        <h3 class="text-purple">3. Décoder des tableaux JSON</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="variable">$json</span> = <span class="string">'["pomme", "banane", "orange"]'</span>;

<span class="variable">$fruits</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>);

<span class="function">echo</span> <span class="variable">$fruits</span>[<span class="number">0</span>];  <span class="comment">// Affiche "pomme"</span>
<span class="function">echo</span> <span class="variable">$fruits</span>[<span class="number">1</span>];  <span class="comment">// Affiche "banane"</span>
<span class="function">echo</span> <span class="variable">$fruits</span>[<span class="number">2</span>];  <span class="comment">// Affiche "orange"</span></code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Structure résultante</h4>
            <pre><code><span class="variable">Array</span>
(
    [<span class="number">0</span>] => <span class="string">pomme</span>
    [<span class="number">1</span>] => <span class="string">banane</span>
    [<span class="number">2</span>] => <span class="string">orange</span>
)</code></pre>
          </div>
        </div>
      </section>

      <!-- Options de décodage -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Options de décodage</h2>
        <p class="textExemple">
          Le quatrième paramètre de <code>json_decode()</code> permet de spécifier des options pour personnaliser le décodage.
          Voici les principales options :
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">JSON_BIGINT_AS_STRING</h3>
          <p class="textExemple">Convertit les grands entiers en chaînes au lieu de nombres flottants :</p>
          <pre><code><span class="variable">$json</span> = <span class="string">'{"valeur": 12345678901234567890}'</span>;
<span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>, <span class="keyword">false</span>, <span class="number">512</span>, <span class="constant">JSON_BIGINT_AS_STRING</span>);

<span class="function">var_dump</span>(<span class="variable">$data</span>-><span class="variable">valeur</span>); <span class="comment">// string(20) "12345678901234567890"</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">JSON_OBJECT_AS_ARRAY</h3>
          <p class="textExemple">Décode les objets JSON en tableaux associatifs :</p>
          <pre><code><span class="variable">$json</span> = <span class="string">'{"nom": "Dupont", "age": 30}'</span>;
<span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>, <span class="keyword">false</span>, <span class="number">512</span>, <span class="constant">JSON_OBJECT_AS_ARRAY</span>);

<span class="function">var_dump</span>(<span class="variable">$data</span>[<span class="string">'nom'</span>]); <span class="comment">// string(6) "Dupont"</span></code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">JSON_THROW_ON_ERROR</h3>
          <p class="textExemple">Lève une exception en cas d'erreur de décodage (PHP 7.3+) :</p>
          <pre><code><span class="keyword">try</span> {
    <span class="variable">$json</span> = <span class="string">'{"nom": "Dupont"'</span>; <span class="comment">// JSON invalide (accolade fermante manquante)</span>
    <span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>, <span class="keyword">false</span>, <span class="number">512</span>, <span class="constant">JSON_THROW_ON_ERROR</span>);
} <span class="keyword">catch</span> (<span class="class-name">JsonException</span> <span class="variable">$e</span>) {
    <span class="function">echo</span> <span class="string">"Erreur JSON: "</span> . <span class="variable">$e</span>-><span class="function">getMessage</span>();
}</code></pre>
        </div>
      </section>

      <!-- Gestion des erreurs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Gestion des erreurs</h2>
        <p class="textExemple">
          Il est crucial de vérifier si le décodage a réussi, car <code>json_decode()</code> retourne <code><span class="keyword">null</span></code> en cas d'échec.
        </p>
        <div class="code-example">
          <h3 class="text-purple">Méthode classique</h3>
          <pre><code><span class="variable">$json</span> = <span class="string">'{"nom": "Dupont", "age": 30}'</span>;

<span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>);

<span class="keyword">if</span> (<span class="variable">$data</span> === <span class="keyword">null</span> && <span class="function">json_last_error</span>() !== <span class="constant">JSON_ERROR_NONE</span>) {
    <span class="function">echo</span> <span class="string">"Erreur de décodage JSON: "</span> . <span class="function">json_last_error_msg</span>();
} <span class="keyword">else</span> {
    <span class="comment">// Utiliser $data</span>
    <span class="function">echo</span> <span class="variable">$data</span>-><span class="variable">nom</span>;
}</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Avec JSON_THROW_ON_ERROR (PHP 7.3+)</h3>
          <pre><code><span class="keyword">try</span> {
    <span class="variable">$json</span> = <span class="string">'{"nom": "Dupont", "age": 30}'</span>;
    <span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>, <span class="keyword">false</span>, <span class="number">512</span>, <span class="constant">JSON_THROW_ON_ERROR</span>);
    <span class="function">echo</span> <span class="variable">$data</span>-><span class="variable">nom</span>;
} <span class="keyword">catch</span> (<span class="class-name">JsonException</span> <span class="variable">$e</span>) {
    <span class="function">echo</span> <span class="string">"Erreur JSON: "</span> . <span class="variable">$e</span>-><span class="function">getMessage</span>();
}</code></pre>
        </div>
      </section>

      <!-- Cas d'utilisation courants -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Cas d'utilisation courants</h2>
        
        <h3 class="text-purple">1. Traitement de données d'API REST</h3>
        <p class="textExemple">
          Récupérer et traiter des données depuis une API externe :
        </p>
        <div class="code-example">
          <pre><code><span class="comment">// Récupérer les données JSON depuis une API</span>
<span class="variable">$json</span> = <span class="function">file_get_contents</span>(<span class="string">'https://api.example.com/users'</span>);

<span class="comment">// Décoder en tableau associatif</span>
<span class="variable">$users</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>, <span class="keyword">true</span>);

<span class="keyword">if</span> (<span class="variable">$users</span> !== <span class="keyword">null</span>) {
    <span class="keyword">foreach</span> (<span class="variable">$users</span> <span class="keyword">as</span> <span class="variable">$user</span>) {
        <span class="function">echo</span> <span class="string">"Nom: "</span> . <span class="variable">$user</span>[<span class="string">'name'</span>] . <span class="string">", Email: "</span> . <span class="variable">$user</span>[<span class="string">'email'</span>] . <span class="string">"&lt;br&gt;"</span>;
    }
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Erreur lors du décodage des données"</span>;
}</code></pre>
        </div>

        <h3 class="text-purple">2. Traitement de données POST AJAX</h3>
        <p class="textExemple">
          Recevoir et traiter des données JSON envoyées via une requête AJAX :
        </p>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="comment">// Récupérer les données JSON du corps de la requête</span>
<span class="variable">$inputJSON</span> = <span class="function">file_get_contents</span>(<span class="string">'php://input'</span>);
<span class="variable">$input</span> = <span class="function">json_decode</span>(<span class="variable">$inputJSON</span>, <span class="keyword">true</span>);

<span class="comment">// Traiter les données</span>
<span class="variable">$response</span> = [
    <span class="string">'success'</span> => <span class="keyword">true</span>,
    <span class="string">'message'</span> => <span class="string">'Données reçues avec succès'</span>,
    <span class="string">'received'</span> => <span class="variable">$input</span>
];

<span class="function">header</span>(<span class="string">'Content-Type: application/json'</span>);
<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$response</span>);</code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Code JavaScript</h4>
            <pre><code><span class="comment">// Envoi des données depuis JavaScript</span>
<span class="function">fetch</span>(<span class="string">'api.php'</span>, {
    <span class="variable">method</span>: <span class="string">'POST'</span>,
    <span class="variable">headers</span>: {
        <span class="string">'Content-Type'</span>: <span class="string">'application/json'</span>
    },
    <span class="variable">body</span>: <span class="function">JSON.stringify</span>({
        <span class="variable">nom</span>: <span class="string">'Dupont'</span>,
        <span class="variable">email</span>: <span class="string">'dupont@example.com'</span>
    })
});</code></pre>
          </div>
        </div>

        <h3 class="text-purple">3. Lecture de fichiers de configuration JSON</h3>
        <p class="textExemple">
          Charger et utiliser des paramètres depuis un fichier JSON :
        </p>
        <div class="code-example">
          <pre><code><span class="comment">// config.json</span>
<span class="comment">// {</span>
<span class="comment">//     "database": {</span>
<span class="comment">//         "host": "localhost",</span>
<span class="comment">//         "username": "root",</span>
<span class="comment">//         "password": "secret"</span>
<span class="comment">//     },</span>
<span class="comment">//     "debug": true</span>
<span class="comment">// }</span>

<span class="variable">$configJSON</span> = <span class="function">file_get_contents</span>(<span class="string">'config.json'</span>);
<span class="variable">$config</span> = <span class="function">json_decode</span>(<span class="variable">$configJSON</span>, <span class="keyword">true</span>);

<span class="keyword">if</span> (<span class="variable">$config</span> !== <span class="keyword">null</span>) {
    <span class="variable">$dbHost</span> = <span class="variable">$config</span>[<span class="string">'database'</span>][<span class="string">'host'</span>];
    <span class="variable">$dbUser</span> = <span class="variable">$config</span>[<span class="string">'database'</span>][<span class="string">'username'</span>];
    <span class="variable">$isDebug</span> = <span class="variable">$config</span>[<span class="string">'debug'</span>];
    
    <span class="function">echo</span> <span class="string">"Connexion à la base de données: </span><span class="variable">$dbHost</span><span class="string"> avec l'utilisateur </span><span class="variable">$dbUser</span><span class="string">"</span>;
}</code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Décodage simple</h3>
          <p class="textExemple">
            Décodez la chaîne JSON suivante et affichez le nom et l'âge de l'utilisateur :
          </p>
          <pre><code><span class="string">'{"utilisateur": {"nom": "Martin", "age": 25, "ville": "Lyon"}}'</span></code></pre>
          <details>
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="variable">$json</span> = <span class="string">'{"utilisateur": {"nom": "Martin", "age": 25, "ville": "Lyon"}}'</span>;

<span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$json</span>);

<span class="keyword">if</span> (<span class="variable">$data</span> !== <span class="keyword">null</span>) {
    <span class="function">echo</span> <span class="string">"Nom: "</span> . <span class="variable">$data</span>-><span class="variable">utilisateur</span>-><span class="variable">nom</span> . <span class="string">"&lt;br&gt;"</span>;
    <span class="function">echo</span> <span class="string">"Age: "</span> . <span class="variable">$data</span>-><span class="variable">utilisateur</span>-><span class="variable">age</span>;
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Erreur de décodage"</span>;
}</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Décodage avec gestion d'erreur avancée</h3>
          <p class="textExemple">
            Créez une fonction qui décode une chaîne JSON et gère les erreurs de manière robuste :
          </p>
          <ul class="textExemple">
            <li>Retourne les données décodées en cas de succès</li>
            <li>Retourne un tableau d'erreur en cas d'échec</li>
            <li>Logge l'erreur dans un fichier</li>
          </ul>
          <details>
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">decodeJSONSafe</span>(<span class="variable">$jsonString</span>, <span class="variable">$associative</span> = <span class="keyword">true</span>) {
    <span class="variable">$data</span> = <span class="function">json_decode</span>(<span class="variable">$jsonString</span>, <span class="variable">$associative</span>);
    
    <span class="keyword">if</span> (<span class="variable">$data</span> === <span class="keyword">null</span> && <span class="function">json_last_error</span>() !== <span class="constant">JSON_ERROR_NONE</span>) {
        <span class="variable">$error</span> = <span class="function">json_last_error_msg</span>();
        
        <span class="comment">// Log de l'erreur</span>
        <span class="function">error_log</span>(<span class="string">"Erreur JSON: </span><span class="variable">$error</span><span class="string"> - Données: </span><span class="variable">$jsonString</span><span class="string">"</span>);
        
        <span class="keyword">return</span> [
            <span class="string">'success'</span> => <span class="keyword">false</span>,
            <span class="string">'error'</span> => <span class="variable">$error</span>,
            <span class="string">'data'</span> => <span class="keyword">null</span>
        ];
    }
    
    <span class="keyword">return</span> [
        <span class="string">'success'</span> => <span class="keyword">true</span>,
        <span class="string">'error'</span> => <span class="keyword">null</span>,
        <span class="string">'data'</span> => <span class="variable">$data</span>
    ];
}

<span class="comment">// Utilisation</span>
<span class="variable">$result</span> = <span class="function">decodeJSONSafe</span>(<span class="string">'{"nom": "Test"}'</span>);

<span class="keyword">if</span> (<span class="variable">$result</span>[<span class="string">'success'</span>]) {
    <span class="function">print_r</span>(<span class="variable">$result</span>[<span class="string">'data'</span>]);
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="string">"Erreur: "</span> . <span class="variable">$result</span>[<span class="string">'error'</span>];
}</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <ul class="textExemple">
          <li><code>json_decode()</code> convertit les chaînes JSON en variables PHP (objets ou tableaux)</li>
          <li>Le deuxième paramètre contrôle si le résultat est un objet (<code>false</code>) ou un tableau associatif (<code>true</code>)</li>
          <li>Toujours vérifier le retour avec <code>json_last_error()</code> pour détecter les échecs de décodage</li>
          <li>Utilisez <code>JSON_THROW_ON_ERROR</code> (PHP 7.3+) pour une gestion d'erreur plus propre avec des exceptions</li>
          <li>Les grands nombres peuvent être convertis en chaînes avec <code>JSON_BIGINT_AS_STRING</code></li>
          <li>La fonction est essentielle pour traiter les données d'API, les requêtes AJAX et les fichiers de configuration</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JsonDecodeLesson',
  head() {
    return {
      title: 'json_decode() en PHP - Cours de programmation',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez à utiliser la fonction json_decode() en PHP pour convertir des données JSON en variables PHP. Exemples pratiques et bonnes pratiques.'
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

/* Couleurs VS Code pour la syntaxe PHP et JavaScript */
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