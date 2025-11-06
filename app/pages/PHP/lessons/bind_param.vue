<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Binding de Paramètres en PHP</h1>
        <p class="lesson-meta text-white">
          Maîtriser la sécurisation des requêtes SQL avec le binding de paramètres PDO et MySQLi
        </p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction au Binding de Paramètres</h2>
        <p class="textExemple">
          Le binding de paramètres (ou requêtes préparées) est une technique essentielle en PHP 
          pour sécuriser les interactions avec les bases de données et prévenir les injections SQL.
        </p>
        <p class="textExemple">
          Cette technique permet de séparer les données de la structure de la requête SQL, 
          éliminant les risques d'injection de code malveillant.
        </p>
      </section>

      <!-- Objectifs de la leçon -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'Apprentissage</h2>
        <ul class="textExemple">
          <li>Comprendre les risques des injections SQL</li>
          <li>Maîtriser PDO avec les requêtes préparées</li>
          <li>Utiliser MySQLi avec le binding de paramètres</li>
          <li>Connaître les différents types de binding</li>
          <li>Implémenter des patterns sécurisés</li>
          <li>Gérer les erreurs efficacement</li>
        </ul>
      </section>

      <!-- Pourquoi utiliser le binding -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi Utiliser le Binding de Paramètres ?</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">❌ À Éviter - Concatenation Dangereuse</h3>
            <pre><code class="php"><span class="variable">$username</span> = <span class="variable">$_POST</span>[<span class="string">'username'</span>];
<span class="variable">$password</span> = <span class="variable">$_POST</span>[<span class="string">'password'</span>];

<span class="comment">// VULNÉRABLE aux injections SQL !</span>
<span class="variable">$sql</span> = <span class="string">"SELECT * FROM users WHERE username = '</span><span class="variable">$username</span><span class="string">' AND password = '</span><span class="variable">$password</span><span class="string">'"</span>;
<span class="variable">$result</span> = <span class="variable">$conn</span>-><span class="function">query</span>(<span class="variable">$sql</span>);</code></pre>
            <p class="textExemple">
              Si un attaquant entre <code>admin' --</code> comme nom d'utilisateur, 
              la requête devient toujours vraie !
            </p>
          </div>

          <div class="code-example">
            <h3 class="text-purple">✅ Bonne Pratique - Binding Sécurisé</h3>
            <pre><code class="php"><span class="variable">$username</span> = <span class="variable">$_POST</span>[<span class="string">'username'</span>];
<span class="variable">$password</span> = <span class="variable">$_POST</span>[<span class="string">'password'</span>];

<span class="comment">// SÉCURISÉ avec binding</span>
<span class="variable">$stmt</span> = <span class="variable">$conn</span>-><span class="function">prepare</span>(
    <span class="string">"SELECT * FROM users WHERE username = ? AND password = ?"</span>
);
<span class="variable">$stmt</span>-><span class="function">bind_param</span>(<span class="string">"ss"</span>, <span class="variable">$username</span>, <span class="variable">$password</span>);
<span class="variable">$stmt</span>-><span class="function">execute</span>();</code></pre>
            <p class="textExemple">
              Les données sont traitées séparément de la requête, 
              éliminant tout risque d'injection.
            </p>
          </div>
        </div>
      </section>

      <!-- Méthodes PDO -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Binding avec PDO</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Méthode 1 : bindParam()</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"INSERT INTO users (name, email, age) VALUES (:name, :email, :age)"</span>
);

<span class="comment">// Liaison par référence</span>
<span class="variable">$stmt</span>-><span class="function">bindParam</span>(<span class="string">':name'</span>, <span class="variable">$name</span>);
<span class="variable">$stmt</span>-><span class="function">bindParam</span>(<span class="string">':email'</span>, <span class="variable">$email</span>);
<span class="variable">$stmt</span>-><span class="function">bindParam</span>(<span class="string">':age'</span>, <span class="variable">$age</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_INT</span>);

<span class="comment">// Exécution</span>
<span class="variable">$name</span> = <span class="string">"John Doe"</span>;
<span class="variable">$email</span> = <span class="string">"john@example.com"</span>;
<span class="variable">$age</span> = <span class="number">30</span>;
<span class="variable">$stmt</span>-><span class="function">execute</span>();</code></pre>
            <p class="textExemple">
              <code>bindParam()</code> lie par référence - les valeurs sont lues au moment de l'exécution.
            </p>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Méthode 2 : bindValue()</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"INSERT INTO products (name, price, category) VALUES (?, ?, ?)"</span>
);

<span class="comment">// Liaison par valeur</span>
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">1</span>, <span class="string">"Laptop"</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">2</span>, <span class="number">999.99</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_STR</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">3</span>, <span class="string">"Electronics"</span>);

<span class="variable">$stmt</span>-><span class="function">execute</span>();</code></pre>
            <p class="textExemple">
              <code>bindValue()</code> lie par valeur - la valeur est fixée immédiatement.
            </p>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Méthode 3 : Tableau dans execute()</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"UPDATE users SET email = ?, active = ? WHERE id = ?"</span>
);

<span class="comment">// Toutes les valeurs dans execute()</span>
<span class="variable">$stmt</span>-><span class="function">execute</span>([
    <span class="string">"newemail@example.com"</span>,
    <span class="number">1</span>,
    <span class="number">42</span>
]);</code></pre>
            <p class="textExemple">
              Méthode la plus concise - parfaite pour les cas simples.
            </p>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Méthode 4 : Noms de paramètres</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"SELECT * FROM orders WHERE status = :status AND total > :min_total"</span>
);

<span class="comment">// Avec des paramètres nommés</span>
<span class="variable">$stmt</span>-><span class="function">execute</span>([
    <span class="string">':status'</span> => <span class="string">'completed'</span>,
    <span class="string">':min_total'</span> => <span class="number">100.00</span>
]);</code></pre>
            <p class="textExemple">
              Plus lisible, surtout avec beaucoup de paramètres.
            </p>
          </div>
        </div>
      </section>

      <!-- Types de données PDO -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de Données PDO</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Constantes de Type PDO</h3>
          <pre><code class="php"><span class="class-name">PDO</span>::<span class="constant">PARAM_BOOL</span>    <span class="comment">// Booléen</span>
<span class="class-name">PDO</span>::<span class="constant">PARAM_NULL</span>    <span class="comment">// Valeur NULL</span>
<span class="class-name">PDO</span>::<span class="constant">PARAM_INT</span>     <span class="comment">// Entier</span>
<span class="class-name">PDO</span>::<span class="constant">PARAM_STR</span>     <span class="comment">// Chaîne de caractères</span>
<span class="class-name">PDO</span>::<span class="constant">PARAM_LOB</span>     <span class="comment">// Large Object (BLOB)</span>
<span class="class-name">PDO</span>::<span class="constant">PARAM_STMT</span>    <span class="comment">// Statement (curseur)</span>
<span class="class-name">PDO</span>::<span class="constant">PARAM_INPUT_OUTPUT</span> <span class="comment">// Paramètre de sortie</span></code></pre>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Exemple avec Types Explicites</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"INSERT INTO products (name, price, in_stock, description) VALUES (?, ?, ?, ?)"</span>
);

<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">1</span>, <span class="variable">$name</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_STR</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">2</span>, <span class="variable">$price</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_STR</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">3</span>, <span class="variable">$in_stock</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_BOOL</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">4</span>, <span class="variable">$description</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_STR</span>);

<span class="variable">$stmt</span>-><span class="function">execute</span>();</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Gestion des NULL</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"UPDATE users SET phone = ?, notes = ? WHERE id = ?"</span>
);

<span class="comment">// Gestion propre des valeurs NULL</span>
<span class="variable">$phone</span> = <span class="keyword">null</span>;
<span class="variable">$notes</span> = <span class="string">"Client important"</span>;

<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">1</span>, <span class="variable">$phone</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_NULL</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">2</span>, <span class="variable">$notes</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_STR</span>);
<span class="variable">$stmt</span>-><span class="function">bindValue</span>(<span class="number">3</span>, <span class="variable">$user_id</span>, <span class="class-name">PDO</span>::<span class="constant">PARAM_INT</span>);</code></pre>
          </div>
        </div>
      </section>

      <!-- Méthodes MySQLi -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Binding avec MySQLi</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Procédural</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="function">mysqli_prepare</span>(
    <span class="variable">$conn</span>, 
    <span class="string">"INSERT INTO logs (message, level, timestamp) VALUES (?, ?, ?)"</span>
);

<span class="comment">// "sss" = 3 paramètres de type string</span>
<span class="function">mysqli_stmt_bind_param</span>(<span class="variable">$stmt</span>, <span class="string">"sss"</span>, <span class="variable">$message</span>, <span class="variable">$level</span>, <span class="variable">$timestamp</span>);

<span class="variable">$message</span> = <span class="string">"User logged in"</span>;
<span class="variable">$level</span> = <span class="string">"INFO"</span>;
<span class="variable">$timestamp</span> = <span class="function">date</span>(<span class="string">"Y-m-d H:i:s"</span>);

<span class="function">mysqli_stmt_execute</span>(<span class="variable">$stmt</span>);</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Oriente Objet</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$conn</span>-><span class="function">prepare</span>(
    <span class="string">"UPDATE products SET stock = ?, price = ? WHERE id = ?"</span>
);

<span class="comment">// "idi" = integer, double, integer</span>
<span class="variable">$stmt</span>-><span class="function">bind_param</span>(<span class="string">"idi"</span>, <span class="variable">$stock</span>, <span class="variable">$price</span>, <span class="variable">$product_id</span>);

<span class="variable">$stock</span> = <span class="number">15</span>;
<span class="variable">$price</span> = <span class="number">29.99</span>;
<span class="variable">$product_id</span> = <span class="number">101</span>;

<span class="variable">$stmt</span>-><span class="function">execute</span>();</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Types de Paramètres MySQLi</h3>
          <pre><code class="php"><span class="string">"i"</span>  <span class="comment">// integer (entier)</span>
<span class="string">"d"</span>  <span class="comment">// double (nombre à virgule)</span>
<span class="string">"s"</span>  <span class="comment">// string (chaîne)</span>
<span class="string">"b"</span>  <span class="comment">// blob (données binaires)</span>

<span class="comment">// Exemples combinés:</span>
<span class="string">"iss"</span>    <span class="comment">// integer, string, string</span>
<span class="string">"sdi"</span>    <span class="comment">// string, double, integer</span>
<span class="string">"isssi"</span>  <span class="comment">// integer, string, string, string, integer</span></code></pre>
        </div>
      </section>

      <!-- Récupération des résultats -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Récupération des Résultats</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Avec PDO</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
    <span class="string">"SELECT id, name, email FROM users WHERE active = ?"</span>
);
<span class="variable">$stmt</span>-><span class="function">execute</span>([<span class="number">1</span>]);

<span class="comment">// Récupération en tableau associatif</span>
<span class="variable">$users</span> = <span class="variable">$stmt</span>-><span class="function">fetchAll</span>(<span class="class-name">PDO</span>::<span class="constant">FETCH_ASSOC</span>);

<span class="keyword">foreach</span> (<span class="variable">$users</span> <span class="keyword">as</span> <span class="variable">$user</span>) {
    <span class="keyword">echo</span> <span class="string">"Nom: {</span><span class="variable">$user</span>[<span class="string">'name'</span>]<span class="string">}, Email: {</span><span class="variable">$user</span>[<span class="string">'email'</span>]<span class="string">}\n"</span>;
}</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Avec MySQLi</h3>
            <pre><code class="php"><span class="variable">$stmt</span> = <span class="variable">$conn</span>-><span class="function">prepare</span>(
    <span class="string">"SELECT id, title, content FROM articles WHERE published = ?"</span>
);
<span class="variable">$stmt</span>-><span class="function">bind_param</span>(<span class="string">"i"</span>, <span class="variable">$published</span>);
<span class="variable">$published</span> = <span class="number">1</span>;
<span class="variable">$stmt</span>-><span class="function">execute</span>();

<span class="comment">// Liaison des résultats</span>
<span class="variable">$stmt</span>-><span class="function">bind_result</span>(<span class="variable">$id</span>, <span class="variable">$title</span>, <span class="variable">$content</span>);

<span class="keyword">while</span> (<span class="variable">$stmt</span>-><span class="function">fetch</span>()) {
    <span class="keyword">echo</span> <span class="string">"ID: </span><span class="variable">$id</span><span class="string">, Titre: </span><span class="variable">$title</span><span class="string">\n"</span>;
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Patterns avancés -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Patterns Avancés</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Requêtes Dynamiques</h3>
            <pre><code class="php"><span class="function">function</span> <span class="function">searchUsers</span>(<span class="variable">$filters</span> = []) {
    <span class="variable">$sql</span> = <span class="string">"SELECT * FROM users WHERE 1=1"</span>;
    <span class="variable">$params</span> = [];
    <span class="variable">$types</span> = <span class="string">""</span>;
    
    <span class="keyword">if</span> (!<span class="function">empty</span>(<span class="variable">$filters</span>[<span class="string">'name'</span>])) {
        <span class="variable">$sql</span> .= <span class="string">" AND name LIKE ?"</span>;
        <span class="variable">$params</span>[] = <span class="string">"%{</span><span class="variable">$filters</span>[<span class="string">'name'</span>]<span class="string">}%"</span>;
        <span class="variable">$types</span> .= <span class="string">"s"</span>;
    }
    
    <span class="keyword">if</span> (!<span class="function">empty</span>(<span class="variable">$filters</span>[<span class="string">'min_age'</span>])) {
        <span class="variable">$sql</span> .= <span class="string">" AND age >= ?"</span>;
        <span class="variable">$params</span>[] = <span class="variable">$filters</span>[<span class="string">'min_age'</span>];
        <span class="variable">$types</span> .= <span class="string">"i"</span>;
    }
    
    <span class="variable">$stmt</span> = <span class="variable">$conn</span>-><span class="function">prepare</span>(<span class="variable">$sql</span>);
    <span class="variable">$stmt</span>-><span class="function">bind_param</span>(<span class="variable">$types</span>, ...<span class="variable">$params</span>);
    <span class="variable">$stmt</span>-><span class="function">execute</span>();
    
    <span class="keyword">return</span> <span class="variable">$stmt</span>-><span class="function">get_result</span>()-><span class="function">fetch_all</span>(<span class="class-name">MYSQLI_ASSOC</span>);
}</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Transactions avec Binding</h3>
            <pre><code class="php"><span class="keyword">try</span> {
    <span class="variable">$pdo</span>-><span class="function">beginTransaction</span>();
    
    <span class="comment">// Première requête</span>
    <span class="variable">$stmt1</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
        <span class="string">"UPDATE accounts SET balance = balance - ? WHERE id = ?"</span>
    );
    <span class="variable">$stmt1</span>-><span class="function">execute</span>([<span class="number">100</span>, <span class="number">1</span>]);
    
    <span class="comment">// Seconde requête</span>
    <span class="variable">$stmt2</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(
        <span class="string">"UPDATE accounts SET balance = balance + ? WHERE id = ?"</span>
    );
    <span class="variable">$stmt2</span>-><span class="function">execute</span>([<span class="number">100</span>, <span class="number">2</span>]);
    
    <span class="variable">$pdo</span>-><span class="function">commit</span>();
    
} <span class="keyword">catch</span> (<span class="class-name">Exception</span> <span class="variable">$e</span>) {
    <span class="variable">$pdo</span>-><span class="function">rollBack</span>();
    <span class="keyword">echo</span> <span class="string">"Erreur: "</span> . <span class="variable">$e</span>-><span class="function">getMessage</span>();
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Gestion des erreurs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Gestion des Erreurs</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Avec PDO</h3>
            <pre><code class="php"><span class="keyword">try</span> {
    <span class="variable">$pdo</span> = <span class="keyword">new</span> <span class="class-name">PDO</span>(
        <span class="string">"mysql:host=localhost;dbname=test;charset=utf8mb4"</span>,
        <span class="string">"username"</span>,
        <span class="string">"password"</span>,
        [
            <span class="class-name">PDO</span>::<span class="constant">ATTR_ERRMODE</span> => <span class="class-name">PDO</span>::<span class="constant">ERRMODE_EXCEPTION</span>,
            <span class="class-name">PDO</span>::<span class="constant">ATTR_EMULATE_PREPARES</span> => <span class="keyword">false</span>
        ]
    );
    
    <span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(<span class="string">"SELECT * FROM users WHERE id = ?"</span>);
    <span class="variable">$stmt</span>-><span class="function">execute</span>([<span class="variable">$user_id</span>]);
    
} <span class="keyword">catch</span> (<span class="class-name">PDOException</span> <span class="variable">$e</span>) {
    <span class="function">error_log</span>(<span class="string">"Erreur PDO: {</span><span class="variable">$e</span>-><span class="function">getMessage</span>()<span class="string">}"</span>);
    <span class="keyword">echo</span> <span class="string">"Une erreur est survenue"</span>;
}</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Avec MySQLi</h3>
            <pre><code class="php"><span class="function">mysqli_report</span>(<span class="class-name">MYSQLI_REPORT_ERROR</span> | <span class="class-name">MYSQLI_REPORT_STRICT</span>);

<span class="keyword">try</span> {
    <span class="variable">$conn</span> = <span class="function">mysqli_connect</span>(<span class="string">"localhost"</span>, <span class="string">"username"</span>, <span class="string">"password"</span>, <span class="string">"test"</span>);
    
    <span class="variable">$stmt</span> = <span class="function">mysqli_prepare</span>(<span class="variable">$conn</span>, <span class="string">"INSERT INTO logs (message) VALUES (?)"</span>);
    <span class="function">mysqli_stmt_bind_param</span>(<span class="variable">$stmt</span>, <span class="string">"s"</span>, <span class="variable">$message</span>);
    <span class="function">mysqli_stmt_execute</span>(<span class="variable">$stmt</span>);
    
} <span class="keyword">catch</span> (<span class="class-name">mysqli_sql_exception</span> <span class="variable">$e</span>) {
    <span class="function">error_log</span>(<span class="string">"Erreur MySQLi: {</span><span class="variable">$e</span>-><span class="function">getMessage</span>()<span class="string">}"</span>);
    <span class="keyword">echo</span> <span class="string">"Une erreur de base de données est survenue"</span>;
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice Pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Énoncé</h3>
          <p class="textExemple">
            Vous devez créer une fonction <code>getUserOrders</code> qui récupère les commandes 
            d'un utilisateur avec des filtres optionnels. La fonction doit :
          </p>
          <ul class="textExemple">
            <li>Accepter un user_id obligatoire</li>
            <li>Accepter des filtres optionnels : status, date_min, date_max</li>
            <li>Utiliser le binding de paramètres pour la sécurité</li>
            <li>Retourner les résultats sous forme de tableau</li>
            <li>Gérer proprement les erreurs</li>
          </ul>
          
          <p class="textExemple">
            Implémentez cette fonction en utilisant PDO avec une approche sécurisée.
          </p>
        </div>

        <details class="solution">
          <summary class="btn-purple btn-hover">Voir la Solution</summary>
          <div class="solution-content">
            <h4 class="text-purple">Solution Complète</h4>
            
            <div class="textExemple">
              <h5 class="text-purple">Implémentation avec PDO</h5>
              <pre><code class="php"><span class="function">function</span> <span class="function">getUserOrders</span>(<span class="variable">$user_id</span>, <span class="variable">$filters</span> = []) {
    <span class="keyword">try</span> {
        <span class="variable">$sql</span> = <span class="string">"SELECT * FROM orders WHERE user_id = :user_id"</span>;
        <span class="variable">$params</span> = [<span class="string">':user_id'</span> => <span class="variable">$user_id</span>];
        
        <span class="comment">// Filtre par statut</span>
        <span class="keyword">if</span> (!<span class="function">empty</span>(<span class="variable">$filters</span>[<span class="string">'status'</span>])) {
            <span class="variable">$sql</span> .= <span class="string">" AND status = :status"</span>;
            <span class="variable">$params</span>[<span class="string">':status'</span>] = <span class="variable">$filters</span>[<span class="string">'status'</span>];
        }
        
        <span class="comment">// Filtre par date minimum</span>
        <span class="keyword">if</span> (!<span class="function">empty</span>(<span class="variable">$filters</span>[<span class="string">'date_min'</span>])) {
            <span class="variable">$sql</span> .= <span class="string">" AND order_date >= :date_min"</span>;
            <span class="variable">$params</span>[<span class="string">':date_min'</span>] = <span class="variable">$filters</span>[<span class="string">'date_min'</span>];
        }
        
        <span class="comment">// Filtre par date maximum</span>
        <span class="keyword">if</span> (!<span class="function">empty</span>(<span class="variable">$filters</span>[<span class="string">'date_max'</span>])) {
            <span class="variable">$sql</span> .= <span class="string">" AND order_date <= :date_max"</span>;
            <span class="variable">$params</span>[<span class="string">':date_max'</span>] = <span class="variable">$filters</span>[<span class="string">'date_max'</span>];
        }
        
        <span class="variable">$sql</span> .= <span class="string">" ORDER BY order_date DESC"</span>;
        
        <span class="variable">$stmt</span> = <span class="variable">$pdo</span>-><span class="function">prepare</span>(<span class="variable">$sql</span>);
        <span class="variable">$stmt</span>-><span class="function">execute</span>(<span class="variable">$params</span>);
        
        <span class="keyword">return</span> <span class="variable">$stmt</span>-><span class="function">fetchAll</span>(<span class="class-name">PDO</span>::<span class="constant">FETCH_ASSOC</span>);
        
    } <span class="keyword">catch</span> (<span class="class-name">PDOException</span> <span class="variable">$e</span>) {
        <span class="function">error_log</span>(<span class="string">"Erreur getUserOrders: {</span><span class="variable">$e</span>-><span class="function">getMessage</span>()<span class="string">}"</span>);
        <span class="keyword">return</span> [];
    }
}

<span class="comment">// Exemple d'utilisation</span>
<span class="variable">$orders</span> = <span class="function">getUserOrders</span>(<span class="number">42</span>, [
    <span class="string">'status'</span> => <span class="string">'completed'</span>,
    <span class="string">'date_min'</span> => <span class="string">'2024-01-01'</span>,
    <span class="string">'date_max'</span> => <span class="string">'2024-12-31'</span>
]);</code></pre>
            </div>

            <div class="textExemple">
              <h5 class="text-purple">Points Clés de la Solution</h5>
              <ul>
                <li>✅ Utilisation de paramètres nommés pour plus de clarté</li>
                <li>✅ Construction dynamique sécurisée de la requête</li>
                <li>✅ Binding automatique via le tableau dans execute()</li>
                <li>✅ Gestion propre des erreurs avec try/catch</li>
                <li>✅ Retour cohérent (tableau vide en cas d'erreur)</li>
                <li>✅ Requête optimisée avec ORDER BY</li>
              </ul>
            </div>
          </div>
        </details>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes Pratiques</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Recommandations Essentielles</h3>
          <ul>
            <li>✅ <strong>Toujours</strong> utiliser le binding de paramètres pour les données externes</li>
            <li>✅ Préférer PDO pour sa portabilité entre bases de données</li>
            <li>✅ Désactiver les préparations émulées : <code>PDO::ATTR_EMULATE_PREPARES => false</code></li>
            <li>✅ Utiliser le mode exception : <code>PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION</code></li>
            <li>✅ Spécifier l'encodage UTF-8 dans le DSN</li>
            <li>✅ Valider et filtrer les données avant le binding</li>
            <li>✅ Utiliser des transactions pour les opérations multiples</li>
            <li>✅ Fermer les statements après utilisation</li>
          </ul>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Configuration PDO Recommandée</h3>
            <pre><code class="php"><span class="variable">$pdo</span> = <span class="keyword">new</span> <span class="class-name">PDO</span>(
    <span class="string">"mysql:host=localhost;dbname=ma_base;charset=utf8mb4"</span>,
    <span class="string">"utilisateur"</span>,
    <span class="string">"mot_de_passe"</span>,
    [
        <span class="class-name">PDO</span>::<span class="constant">ATTR_ERRMODE</span> => <span class="class-name">PDO</span>::<span class="constant">ERRMODE_EXCEPTION</span>,
        <span class="class-name">PDO</span>::<span class="constant">ATTR_EMULATE_PREPARES</span> => <span class="keyword">false</span>,
        <span class="class-name">PDO</span>::<span class="constant">ATTR_DEFAULT_FETCH_MODE</span> => <span class="class-name">PDO</span>::<span class="constant">FETCH_ASSOC</span>
    ]
);</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Validation des Données</h3>
            <pre><code class="php"><span class="function">function</span> <span class="function">validateUserInput</span>(<span class="variable">$data</span>) {
    <span class="variable">$user_id</span> = <span class="function">filter_var</span>(<span class="variable">$data</span>[<span class="string">'user_id'</span>], <span class="class-name">FILTER_VALIDATE_INT</span>);
    <span class="keyword">if</span> (<span class="variable">$user_id</span> === <span class="keyword">false</span>) {
        <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"ID utilisateur invalide"</span>);
    }
    
    <span class="variable">$email</span> = <span class="function">filter_var</span>(<span class="variable">$data</span>[<span class="string">'email'</span>], <span class="class-name">FILTER_VALIDATE_EMAIL</span>);
    <span class="keyword">if</span> (<span class="variable">$email</span> === <span class="keyword">false</span>) {
        <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"Email invalide"</span>);
    }
    
    <span class="keyword">return</span> [
        <span class="string">'user_id'</span> => <span class="variable">$user_id</span>,
        <span class="string">'email'</span> => <span class="variable">$email</span>
    ];
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Checklist de connaissances -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Checklist de Connaissances</h2>
        
        <div class="textExemple">
          <ul>
            <li>✅ Comprendre les risques des injections SQL</li>
            <li>✅ Maîtriser les 4 méthodes de binding PDO</li>
            <li>✅ Connaître les types de paramètres MySQLi (i,d,s,b)</li>
            <li>✅ Savoir récupérer les résultats après binding</li>
            <li>✅ Implémenter des requêtes dynamiques sécurisées</li>
            <li>✅ Gérer les transactions avec binding</li>
            <li>✅ Configurer PDO correctement</li>
            <li>✅ Valider les données avant binding</li>
            <li>✅ Gérer les erreurs proprement</li>
          </ul>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          Le binding de paramètres n'est pas une option mais une nécessité absolue pour 
          toute application PHP qui interagit avec une base de données. C'est la seule 
          méthode fiable pour prévenir les injections SQL et assurer la sécurité des données.
        </p>
        <p class="textExemple">
          Que vous utilisiez PDO ou MySQLi, adoptez systématiquement les requêtes préparées 
          et faites du binding de paramètres un réflexe dans votre développement.
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

/* Couleurs VS Code pour la syntaxe PHP */
.keyword { color: #c586c0 !important; } /* Mots-clés (function, if, foreach, etc.) */
.variable { color: #9cdcfe !important; } /* Variables */
.string { color: #ce9178 !important; } /* Chaînes de caractères */
.comment { color: #6a9955 !important; } /* Commentaires */
.function { color: #dcdcaa !important; } /* Noms de fonctions */
.operator { color: #d4d4d4 !important; } /* Opérateurs */
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