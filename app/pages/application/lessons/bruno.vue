<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Bruno : Client API Open Source</h1>
        <p class="lesson-meta text-white">Découvrez l'alternative moderne à Postman pour tester vos APIs</p>
      </header>

      <!-- Introduction à Bruno -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que Bruno ?</h2>
        <p class="textExemple">
          Bruno est un client API open-source et innovant qui stocke vos collections directement dans 
          le système de fichiers, contrairement aux outils traditionnels comme Postman. Il utilise 
          des dossiers et fichiers pour organiser vos requêtes, ce qui les rend versionnables avec Git.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Avantages de Bruno :</h3>
          <ul>
            <li><strong>Open Source</strong> - Gratuit et communautaire</li>
            <li><strong>Versionnable</strong> - Collections stockées en clair dans des fichiers</li>
            <li><strong>Hors ligne</strong> - Pas de compte cloud obligatoire</li>
            <li><strong>Rapide</strong> - Interface légère et performante</li>
            <li><strong>Collaboratif</strong> - Intégration naturelle avec Git</li>
          </ul>
        </div>
      </section>

      <!-- Installation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Installation de Bruno</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Installation via NPM (Recommandé)</h4>
            <pre><code class="language-bash"><span class="comment"># Installation globale</span>
<span class="keyword">npm install</span> <span class="variable">-g</span> <span class="string">@usebruno/bruno</span>

<span class="comment"># Lancer Bruno</span>
<span class="keyword">bruno</span>

<span class="comment"># Ou créer un nouveau projet</span>
<span class="keyword">bruno init</span> <span class="variable">mon-api-project</span></code></pre>
          </div>
          
          <div>
            <h4 class="text-purple">Téléchargement direct</h4>
            <pre><code class="language-bash"><span class="comment"># Télécharger depuis GitHub</span>
<span class="comment"># https://github.com/usebruno/bruno/releases</span>

<span class="comment"># Ou utiliser brew sur Mac</span>
<span class="keyword">brew install</span> <span class="variable">bruno</span>

<span class="comment"># Sur Windows, télécharger le .exe</span>
<span class="comment"># Sur Linux, utiliser AppImage ou Snap</span></code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Vérification de l'installation</h3>
          <pre><code class="language-bash"><span class="comment"># Vérifier la version installée</span>
<span class="keyword">bruno</span> <span class="variable">--version</span>

<span class="comment"># Afficher l'aide</span>
<span class="keyword">bruno</span> <span class="variable">--help</span></code></pre>
        </div>
      </section>

      <!-- Structure d'un projet Bruno -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Structure d'un projet Bruno</h2>
        <p class="textExemple">
          Contrairement à Postman, Bruno organise les collections dans une structure de dossiers :
        </p>
        
        <div class="code-example">
          <pre><code class="language-text">mon-projet-api/
├── <span class="variable">bruno.json</span>          <span class="comment"># Configuration du projet</span>
├── <span class="variable">collections/</span>        <span class="comment"># Dossier des collections</span>
│   └── <span class="variable">api-utilisateurs/</span>
│       ├── <span class="variable">bru.json</span>    <span class="comment"># Configuration de la collection</span>
│       ├── <span class="variable">GET-utilisateurs.bru</span>    <span class="comment"># Requête GET</span>
│       ├── <span class="variable">POST-utilisateurs.bru</span>   <span class="comment"># Requête POST</span>
│       └── <span class="variable">environments/</span>
│           └── <span class="variable">dev.bru</span> <span class="comment"># Variables d'environnement</span>
└── <span class="variable">scripts/</span>            <span class="comment"># Scripts personnalisés</span></code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Fichier de configuration bruno.json</h3>
          <pre><code class="language-json">{
  <span class="variable">"version"</span>: <span class="string">"1"</span>,
  <span class="variable">"name"</span>: <span class="string">"Mon Projet API"</span>,
  <span class="variable">"type"</span>: <span class="string">"collection"</span>
}</code></pre>
        </div>
      </section>

      <!-- Créer sa première collection -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Créer sa première collection</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Méthode 1 : Via l'interface graphique</h3>
          <ol>
            <li>Ouvrir Bruno</li>
            <li>Cliquer sur "Create New Collection"</li>
            <li>Choisir le dossier de destination</li>
            <li>Nommer la collection</li>
            <li>Ajouter des requêtes via le bouton "+"</li>
          </ol>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Méthode 2 : Via le terminal</h3>
          <pre><code class="language-bash"><span class="comment"># Créer un nouveau projet Bruno</span>
<span class="keyword">bruno init</span> <span class="variable">mon-api-collection</span>

<span class="comment"># Se déplacer dans le dossier</span>
<span class="keyword">cd</span> <span class="variable">mon-api-collection</span>

<span class="comment"># Structure créée automatiquement</span>
<span class="keyword">ls</span> <span class="variable">-la</span></code></pre>
        </div>
      </section>

      <!-- Les fichiers .bru -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Anatomie d'un fichier .bru</h2>
        <p class="textExemple">
          Chaque requête API est stockée dans un fichier .bru avec une syntaxe simple :
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de requête GET</h3>
          <pre><code class="language-yaml"><span class="variable">meta:</span>
  <span class="variable">name:</span> <span class="string">"Récupérer tous les utilisateurs"</span>
  <span class="variable">type:</span> <span class="string">"http"</span>
  <span class="variable">seq:</span> <span class="number">1</span>

<span class="variable">request:</span>
  <span class="variable">method:</span> <span class="string">"GET"</span>
  <span class="variable">url:</span> <span class="string">"{{base_url}}/api/users"</span>
  <span class="variable">headers:</span>
    - <span class="variable">name:</span> <span class="string">"Authorization"</span>
      <span class="variable">value:</span> <span class="string">"Bearer {{token}}"</span>
    - <span class="variable">name:</span> <span class="string">"Content-Type"</span>
      <span class="variable">value:</span> <span class="string">"application/json"</span>

<span class="variable">response:</span>
  - <span class="variable">name:</span> <span class="string">"Success"</span>
    <span class="variable">status:</span> <span class="number">200</span>
    <span class="variable">body:</span> |
      {
        <span class="string">"users"</span>: [
          {
            <span class="string">"id"</span>: <span class="number">1</span>,
            <span class="string">"name"</span>: <span class="string">"John Doe"</span>,
            <span class="string">"email"</span>: <span class="string">"john@example.com"</span>
          }
        ]
      }</code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de requête POST</h3>
          <pre><code class="language-yaml"><span class="variable">meta:</span>
  <span class="variable">name:</span> <span class="string">"Créer un nouvel utilisateur"</span>
  <span class="variable">type:</span> <span class="string">"http"</span>
  <span class="variable">seq:</span> <span class="number">2</span>

<span class="variable">request:</span>
  <span class="variable">method:</span> <span class="string">"POST"</span>
  <span class="variable">url:</span> <span class="string">"{{base_url}}/api/users"</span>
  <span class="variable">headers:</span>
    - <span class="variable">name:</span> <span class="string">"Authorization"</span>
      <span class="variable">value:</span> <span class="string">"Bearer {{token}}"</span>
    - <span class="variable">name:</span> <span class="string">"Content-Type"</span>
      <span class="variable">value:</span> <span class="string">"application/json"</span>
  <span class="variable">body:</span> |
    {
      <span class="string">"name"</span>: <span class="string">"Jane Doe"</span>,
      <span class="string">"email"</span>: <span class="string">"jane@example.com"</span>,
      <span class="string">"password"</span>: <span class="string">"securepassword"</span>
    }

<span class="variable">response:</span>
  - <span class="variable">name:</span> <span class="string">"Success"</span>
    <span class="variable">status:</span> <span class="number">201</span>
    <span class="variable">body:</span> |
      {
        <span class="string">"id"</span>: <span class="number">2</span>,
        <span class="string">"name"</span>: <span class="string">"Jane Doe"</span>,
        <span class="string">"email"</span>: <span class="string">"jane@example.com"</span>
      }</code></pre>
        </div>
      </section>

      <!-- Variables d'environnement -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Variables d'environnement</h2>
        <p class="textExemple">
          Bruno supporte les variables d'environnement pour gérer différentes configurations (dev, staging, prod).
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Fichier d'environnement dev.bru</h3>
          <pre><code class="language-yaml"><span class="variable">name:</span> <span class="string">"Development"</span>
<span class="variable">type:</span> <span class="string">"environment"</span>
<span class="variable">values:</span>
  - <span class="variable">key:</span> <span class="string">"base_url"</span>
    <span class="variable">value:</span> <span class="string">"https://api.dev.monsite.com"</span>
    <span class="variable">enabled:</span> <span class="constant">true</span>
  - <span class="variable">key:</span> <span class="string">"token"</span>
    <span class="variable">value:</span> <span class="string">"dev_token_123"</span>
    <span class="variable">enabled:</span> <span class="constant">true</span></code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Fichier d'environnement prod.bru</h3>
          <pre><code class="language-yaml"><span class="variable">name:</span> <span class="string">"Production"</span>
<span class="variable">type:</span> <span class="string">"environment"</span>
<span class="variable">values:</span>
  - <span class="variable">key:</span> <span class="string">"base_url"</span>
    <span class="variable">value:</span> <span class="string">"https://api.monsite.com"</span>
    <span class="variable">enabled:</span> <span class="constant">true</span>
  - <span class="variable">key:</span> <span class="string">"token"</span>
    <span class="variable">value:</span> <span class="string">"prod_token_456"</span>
    <span class="variable">enabled:</span> <span class="constant">true</span></code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Utilisation dans les requêtes</h3>
          <pre><code class="language-yaml"><span class="variable">request:</span>
  <span class="variable">method:</span> <span class="string">"GET"</span>
  <span class="variable">url:</span> <span class="string">"{{base_url}}/api/users"</span>  <span class="comment"># Utilise la variable base_url</span>
  <span class="variable">headers:</span>
    - <span class="variable">name:</span> <span class="string">"Authorization"</span>
      <span class="variable">value:</span> <span class="string">"Bearer {{token}}"</span>  <span class="comment"># Utilise la variable token</span></code></pre>
        </div>
      </section>

      <!-- Tests et assertions -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Tests et assertions</h2>
        <p class="textExemple">
          Bruno permet d'écrire des tests JavaScript pour valider vos réponses API.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Exemple de tests</h3>
          <pre><code class="language-javascript"><span class="variable">tests:</span> |
  <span class="comment">// Test du statut HTTP</span>
  <span class="function">bruno</span>.<span class="function">test</span>(<span class="string">"Status code est 200"</span>, () => {
    <span class="function">expect</span>(<span class="variable">response</span>.<span class="variable">status</span>).<span class="function">toBe</span>(<span class="number">200</span>);
  });

  <span class="comment">// Test de la structure JSON</span>
  <span class="function">bruno</span>.<span class="function">test</span>(<span class="string">"Réponse contient un tableau users"</span>, () => {
    <span class="keyword">const</span> <span class="variable">json</span> = <span class="variable">response</span>.<span class="function">json</span>();
    <span class="function">expect</span>(<span class="class-name">Array</span>.<span class="function">isArray</span>(<span class="variable">json</span>.<span class="variable">users</span>)).<span class="function">toBe</span>(<span class="constant">true</span>);
  });

  <span class="comment">// Test des données</span>
  <span class="function">bruno</span>.<span class="function">test</span>(<span class="string">"Premier utilisateur a un email"</span>, () => {
    <span class="keyword">const</span> <span class="variable">json</span> = <span class="variable">response</span>.<span class="function">json</span>();
    <span class="function">expect</span>(<span class="variable">json</span>.<span class="variable">users</span>[<span class="number">0</span>].<span class="variable">email</span>).<span class="function">toBeDefined</span>();
    <span class="function">expect</span>(<span class="variable">json</span>.<span class="variable">users</span>[<span class="number">0</span>].<span class="variable">email</span>).<span class="function">toContain</span>(<span class="string">"@"</span>);
  });

  <span class="comment">// Test des headers</span>
  <span class="function">bruno</span>.<span class="function">test</span>(<span class="string">"Content-Type est application/json"</span>, () => {
    <span class="function">expect</span>(<span class="variable">response</span>.<span class="variable">headers</span>[<span class="string">'content-type'</span>]).<span class="function">toContain</span>(<span class="string">'application/json'</span>);
  });</code></pre>
        </div>
      </section>

      <!-- Scripts pré-requêtes -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Scripts et automatisation</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Script pré-requête (pre-request)</h4>
            <pre><code class="language-javascript"><span class="variable">preRequest:</span> |
  <span class="comment">// Générer un timestamp</span>
  <span class="keyword">const</span> <span class="variable">timestamp</span> = <span class="class-name">Date</span>.<span class="function">now</span>();
  <span class="function">bruno</span>.<span class="function">setEnvironmentVariable</span>(<span class="string">"timestamp"</span>, <span class="variable">timestamp</span>);

  <span class="comment">// Hasher un mot de passe (exemple)</span>
  <span class="keyword">const</span> <span class="variable">password</span> = <span class="string">"monMotDePasse"</span>;
  <span class="keyword">const</span> <span class="variable">hashedPassword</span> = <span class="function">bruno</span>.<span class="variable">hash</span>.<span class="function">sha256</span>(<span class="variable">password</span>);
  <span class="function">bruno</span>.<span class="function">setEnvironmentVariable</span>(<span class="string">"hashed_password"</span>, <span class="variable">hashedPassword</span>);</code></pre>
          </div>
          
          <div>
            <h4 class="text-purple">Script post-requête</h4>
            <pre><code class="language-javascript"><span class="variable">postResponse:</span> |
  <span class="comment">// Sauvegarder le token d'authentification</span>
  <span class="keyword">if</span> (<span class="variable">response</span>.<span class="variable">status</span> === <span class="number">200</span>) {
    <span class="keyword">const</span> <span class="variable">json</span> = <span class="variable">response</span>.<span class="function">json</span>();
    <span class="function">bruno</span>.<span class="function">setEnvironmentVariable</span>(<span class="string">"auth_token"</span>, <span class="variable">json</span>.<span class="variable">token</span>);
    
    <span class="comment">// Logger pour le debug</span>
    <span class="function">bruno</span>.<span class="function">log</span>(<span class="string">"Token sauvegardé: "</span> + <span class="variable">json</span>.<span class="variable">token</span>);
  }

  <span class="comment">// Mettre à jour des variables globales</span>
  <span class="function">bruno</span>.<span class="function">setEnvironmentVariable</span>(<span class="string">"last_request_time"</span>, <span class="keyword">new</span> <span class="class-name">Date</span>().<span class="function">toISOString</span>());</code></pre>
          </div>
        </div>
      </section>

      <!-- Intégration avec Git -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Intégration avec Git</h2>
        <p class="textExemple">
          La grande force de Bruno : tout est versionnable avec Git !
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Initialiser un dépôt Git</h3>
          <pre><code class="language-bash"><span class="comment"># Se placer dans le dossier Bruno</span>
<span class="keyword">cd</span> <span class="variable">mon-projet-bruno</span>

<span class="comment"># Initialiser Git</span>
<span class="keyword">git init</span>

<span class="comment"># Ajouter tous les fichiers</span>
<span class="keyword">git add</span> <span class="variable">.</span>

<span class="comment"># Premier commit</span>
<span class="keyword">git commit</span> <span class="variable">-m</span> <span class="string">"Initialisation collection API"</span>

<span class="comment"># Créer un dépôt distant et pousser</span>
<span class="keyword">git remote add</span> <span class="variable">origin</span> <span class="string">https://github.com/user/mon-api-collection.git</span>
<span class="keyword">git push</span> <span class="variable">-u origin main</span></code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Fichier .gitignore recommandé</h3>
          <pre><code class="language-text"><span class="comment"># Fichiers temporaires Bruno</span>
<span class="variable">*.tmp</span>
<span class="variable">*.log</span>

<span class="comment"># Environnements sensibles (à versionner avec précaution)</span>
<span class="comment"># environments/prod.bru</span>

<span class="comment"># Dossiers système</span>
<span class="variable">.DS_Store</span>
<span class="variable">Thumbs.db</span></code></pre>
        </div>
      </section>

      <!-- Comparaison avec Postman -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bruno vs Postman</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">Postman</h4>
            <ul>
              <li>✅ Interface très mature</li>
              <li>✅ Grande communauté</li>
              <li>✅ Documentation complète</li>
              <li>❌ Compte cloud requis</li>
              <li>❌ Collections pas facilement versionnables</li>
              <li>❌ Freemium avec limitations</li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-purple">Bruno</h4>
            <ul>
              <li>✅ 100% open source</li>
              <li>✅ Collections versionnables avec Git</li>
              <li>✅ Pas de compte requis</li>
              <li>✅ Structure fichiers/dossiers claire</li>
              <li>❌ Plus récent, écosystème en développement</li>
              <li>❌ Moins de fonctionnalités avancées</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique : Créer une collection API</h2>
        <div class="exercise">
          <p class="textExemple">
            <strong>Objectif :</strong> Créer une collection Bruno complète pour une API de blog.
          </p>
          
          <ol>
            <li>Installez Bruno sur votre machine</li>
            <li>Créez un nouveau projet "blog-api"</li>
            <li>Configurez un environnement de développement</li>
            <li>Créez des requêtes pour :
              <ul>
                <li>GET /api/posts - Lister les articles</li>
                <li>POST /api/posts - Créer un article</li>
                <li>GET /api/posts/1 - Récupérer un article</li>
                <li>PUT /api/posts/1 - Modifier un article</li>
              </ul>
            </li>
            <li>Ajoutez des tests pour chaque endpoint</li>
            <li>Versionnez la collection avec Git</li>
          </ol>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Structure du projet</h4>
              <pre><code class="language-text"><span class="variable">blog-api/</span>
├── <span class="variable">bruno.json</span>
├── <span class="variable">collections/</span>
│   └── <span class="variable">blog-api/</span>
│       ├── <span class="variable">bru.json</span>
│       ├── <span class="variable">GET-posts.bru</span>
│       ├── <span class="variable">POST-posts.bru</span>
│       ├── <span class="variable">GET-posts-[id].bru</span>
│       ├── <span class="variable">PUT-posts-[id].bru</span>
│       └── <span class="variable">environments/</span>
│           ├── <span class="variable">dev.bru</span>
│           └── <span class="variable">local.bru</span>
└── <span class="variable">README.md</span></code></pre>
              
              <h4 class="text-purple">Environnement de développement (dev.bru)</h4>
              <pre><code class="language-yaml"><span class="variable">name:</span> <span class="string">"Development"</span>
<span class="variable">type:</span> <span class="string">"environment"</span>
<span class="variable">values:</span>
  - <span class="variable">key:</span> <span class="string">"base_url"</span>
    <span class="variable">value:</span> <span class="string">"https://jsonplaceholder.typicode.com"</span>
    <span class="variable">enabled:</span> <span class="constant">true</span></code></pre>
              
              <h4 class="text-purple">Exemple de requête GET /posts</h4>
              <pre><code class="language-yaml"><span class="variable">meta:</span>
  <span class="variable">name:</span> <span class="string">"Lister les articles"</span>
  <span class="variable">type:</span> <span class="string">"http"</span>
  <span class="variable">seq:</span> <span class="number">1</span>

<span class="variable">request:</span>
  <span class="variable">method:</span> <span class="string">"GET"</span>
  <span class="variable">url:</span> <span class="string">"{{base_url}}/posts"</span>

<span class="variable">tests:</span> |
  <span class="function">bruno</span>.<span class="function">test</span>(<span class="string">"Status 200"</span>, () => {
    <span class="function">expect</span>(<span class="variable">response</span>.<span class="variable">status</span>).<span class="function">toBe</span>(<span class="number">200</span>);
  });
  
  <span class="function">bruno</span>.<span class="function">test</span>(<span class="string">"Retourne un tableau"</span>, () => {
    <span class="keyword">const</span> <span class="variable">json</span> = <span class="variable">response</span>.<span class="function">json</span>();
    <span class="function">expect</span>(<span class="class-name">Array</span>.<span class="function">isArray</span>(<span class="variable">json</span>)).<span class="function">toBe</span>(<span class="constant">true</span>);
  });</code></pre>
              
              <h4 class="text-purple">Initialisation Git</h4>
              <pre><code class="language-bash"><span class="keyword">cd</span> <span class="variable">blog-api</span>
<span class="keyword">git init</span>
<span class="keyword">git add</span> <span class="variable">.</span>
<span class="keyword">git commit</span> <span class="variable">-m</span> <span class="string">"Collection API Blog"</span>
<span class="keyword">git remote add</span> <span class="variable">origin</span> <span class="string">https://github.com/user/blog-api.git</span>
<span class="keyword">git push</span> <span class="variable">-u origin main</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques avec Bruno</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Organisation des collections</h3>
          <ul>
            <li>Une collection par microservice/domaine</li>
            <li>Nommage cohérent des fichiers .bru</li>
            <li>Utilisation des variables d'environnement</li>
            <li>Séparation des environnements sensibles</li>
          </ul>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Collaboration en équipe</h3>
          <ul>
            <li>Versionner les collections avec Git</li>
            <li>Utiliser des branches pour les nouvelles fonctionnalités</li>
            <li>Code review des collections API</li>
            <li>Documentation dans les README</li>
          </ul>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary border-purple">
        <h2 class="text-white">Conclusion</h2>
        <div class="textExemple text-white">
          <p>
            <strong>Bruno représente une avancée significative</strong> dans le monde des clients API en apportant 
            une approche moderne, open-source et centrée sur le développeur. En choisissant de stocker 
            les collections sous forme de fichiers dans le système de fichiers, Bruno résout plusieurs 
            limitations des outils traditionnels comme Postman.
          </p>
          
          <p>
            <strong>Les avantages clés de Bruno :</strong>
          </p>
          <ul>
            <li><strong>Versionnement natif</strong> avec Git pour une collaboration efficace</li>
            <li><strong>Indépendance des plateformes cloud</strong> et respect de la vie privée</li>
            <li><strong>Structure transparente</strong> qui facilite la maintenance</li>
            <li><strong>Scripting puissant</strong> pour l'automatisation des tests</li>
            <li><strong>Communauté open-source</strong> active et croissante</li>
          </ul>
          
          <p>
            Bien que plus récent et avec un écosystème encore en développement, Bruno offre déjà 
            toutes les fonctionnalités essentielles pour tester et documenter vos APIs. Son adoption 
            est particulièrement recommandée pour les équipes qui valorisent la transparence, 
            la collaboration via Git et l'indépendance vis-à-vis des solutions SaaS.
          </p>
          
          <p>
            <strong>Bruno n'est pas juste un outil, c'est une philosophie</strong> : celle de remettre 
            le contrôle entre les mains des développeurs et de favoriser des pratiques de développement 
            modernes et collaboratives.
          </p>
        </div>
      </section>

      <!-- Navigation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pour aller plus loin</h2>
        <p class="textExemple">
          Explorez ces ressources pour approfondir votre maîtrise de Bruno :
        </p>
        
        <div class="code-example">
          <ul>
            <li><a href="https://docs.usebruno.com" class="text-purple">Documentation officielle de Bruno</a></li>
            <li><a href="https://github.com/usebruno/bruno" class="text-purple">Dépôt GitHub</a></li>
            <li>Intégration avec les pipelines CI/CD</li>
            <li>Scripts avancés et hooks personnalisés</li>
            <li>Création de templates de collections</li>
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

/* Couleurs VS Code pour la syntaxe */
.keyword { color: #c586c0 !important; } /* Mots-clés (const, if, function, etc.) */
.variable { color: #9cdcfe !important; } /* Variables et noms */
.string { color: #ce9178 !important; } /* Chaînes de caractères */
.comment { color: #6a9955 !important; } /* Commentaires */
.function { color: #dcdcaa !important; } /* Noms de fonctions */
.operator { color: #d4d4d4 !important; } /* Opérateurs (+, -, =, =>, etc.) */
.constant { color: #4fc1ff !important; } /* Constantes (true, false, null) */
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