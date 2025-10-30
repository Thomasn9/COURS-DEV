<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les Repository dans l'Architecture MVC</h1>
                <p class="lesson-meta text-white">PHP • MVC • Design Patterns • Repository • Data Access Layer</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Repository</h2>
                <p class="textExemple">
                    Le pattern <strong>Repository</strong> est un design pattern qui fait partie de la couche d'accès aux données
                    dans une architecture MVC. Il agit comme une couche d'abstraction entre le domaine métier et la couche de persistance.
                </p>
                <p class="textExemple">
                    Les Repository encapsulent la logique d'accès aux données, permettant de découpler la logique métier
                    des détails techniques de stockage et de récupération des données.
                </p>
            </section>

            <!-- Concepts de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts Fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Rôle du Repository</h3>
                    <ul>
                        <li><strong>Abstraction de l'accès aux données</strong> : Cache les détails de la base de données</li>
                        <li><strong>Interface unique</strong> pour les opérations CRUD</li>
                        <li><strong>Découplage</strong> entre la logique métier et la persistance</li>
                        <li><strong>Facilitation des tests</strong> avec des repositories mock</li>
                        <li><strong>Centralisation</strong> des requêtes complexes</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Architecture typique MVC avec Repository</h3>
                    <div class="code-example">
                        <pre><code>Architecture MVC avec Repository :
┌─────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│    Controller   │ ── │     Service      │ ── │   Repository     │
│                 │    │                  │    │                  │
│ - Gère requêtes │    │ - Logique métier │    │ - Accès données  │
│ - Retourne vues │    │ - Règles métier  │    │ - Opérations CRUD│
└─────────────────┘    └──────────────────┘    └──────────────────┘
                                                           │
                                                           ▼
                                                 ┌──────────────────┐
                                                 │  Base de données │
                                                 │                  │
                                                 │ - Tables         │
                                                 │ - Requêtes SQL   │
                                                 └──────────────────┘</code></pre>
                    </div>
                </div>
            </section>

            <!-- Interface Repository de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Interface Repository de Base</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Interface générique</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">interface</span> <span class="php-class">RepositoryInterface</span> {
    <span class="php-comment">/**
     * Trouver un élément par son ID
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">find</span>(<span class="php-var">$id</span>);
    
    <span class="php-comment">/**
     * Trouver tous les éléments
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findAll</span>();
    
    <span class="php-comment">/**
     * Trouver des éléments par critères
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findBy</span>(<span class="php-keyword">array</span> <span class="php-var">$criteria</span>, <span class="php-keyword">array</span> <span class="php-var">$orderBy</span> = <span class="php-keyword">null</span>, <span class="php-var">$limit</span> = <span class="php-keyword">null</span>, <span class="php-var">$offset</span> = <span class="php-keyword">null</span>);
    
    <span class="php-comment">/**
     * Sauvegarder un élément
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">save</span>(<span class="php-var">$entity</span>);
    
    <span class="php-comment">/**
     * Supprimer un élément
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">delete</span>(<span class="php-var">$entity</span>);
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Interface étendue pour des besoins spécifiques</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">interface</span> <span class="php-class">UserRepositoryInterface</span> <span class="php-keyword">extends</span> <span class="php-class">RepositoryInterface</span> {
    <span class="php-comment">/**
     * Trouver un utilisateur par email
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findByEmail</span>(<span class="php-var">$email</span>);
    
    <span class="php-comment">/**
     * Trouver des utilisateurs actifs
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findActiveUsers</span>();
    
    <span class="php-comment">/**
     * Compter les utilisateurs par rôle
     */</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">countByRole</span>(<span class="php-var">$role</span>);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Entité et Repository Utilisateur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Entité et Repository Utilisateur</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Classe Entité User</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">User</span> {
    <span class="php-keyword">private</span> <span class="php-var">$id</span>;
    <span class="php-keyword">private</span> <span class="php-var">$email</span>;
    <span class="php-keyword">private</span> <span class="php-var">$password</span>;
    <span class="php-keyword">private</span> <span class="php-var">$firstName</span>;
    <span class="php-keyword">private</span> <span class="php-var">$lastName</span>;
    <span class="php-keyword">private</span> <span class="php-var">$role</span>;
    <span class="php-keyword">private</span> <span class="php-var">$isActive</span>;
    <span class="php-keyword">private</span> <span class="php-var">$createdAt</span>;
    
    <span class="php-comment">// Constructeur</span>
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$email</span>, <span class="php-var">$password</span>, <span class="php-var">$firstName</span>, <span class="php-var">$lastName</span>, <span class="php-var">$role</span> = <span class="php-string">'user'</span>) {
        <span class="php-var">$this</span>-&gt;email = <span class="php-var">$email</span>;
        <span class="php-var">$this</span>-&gt;<span class="php-function">setPassword</span>(<span class="php-var">$password</span>);
        <span class="php-var">$this</span>-&gt;firstName = <span class="php-var">$firstName</span>;
        <span class="php-var">$this</span>-&gt;lastName = <span class="php-var">$lastName</span>;
        <span class="php-var">$this</span>-&gt;role = <span class="php-var">$role</span>;
        <span class="php-var">$this</span>-&gt;isActive = <span class="php-keyword">true</span>;
        <span class="php-var">$this</span>-&gt;createdAt = <span class="php-keyword">new</span> <span class="php-class">DateTime</span>();
    }
    
    <span class="php-comment">// Getters</span>
    <span class="php-keyword">public function</span> <span class="php-function">getId</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;id; }
    <span class="php-keyword">public function</span> <span class="php-function">getEmail</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;email; }
    <span class="php-keyword">public function</span> <span class="php-function">getFirstName</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;firstName; }
    <span class="php-keyword">public function</span> <span class="php-function">getLastName</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;lastName; }
    <span class="php-keyword">public function</span> <span class="php-function">getRole</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;role; }
    <span class="php-keyword">public function</span> <span class="php-function">isActive</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;isActive; }
    <span class="php-keyword">public function</span> <span class="php-function">getCreatedAt</span>() { <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;createdAt; }
    
    <span class="php-comment">// Setters avec validation</span>
    <span class="php-keyword">public function</span> <span class="php-function">setEmail</span>(<span class="php-var">$email</span>) {
        <span class="php-keyword">if</span> (!<span class="php-function">filter_var</span>(<span class="php-var">$email</span>, <span class="php-constant">FILTER_VALIDATE_EMAIL</span>)) {
            <span class="php-keyword">throw new</span> <span class="php-class">InvalidArgumentException</span>(<span class="php-string">"Email invalide"</span>);
        }
        <span class="php-var">$this</span>-&gt;email = <span class="php-var">$email</span>;
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">setPassword</span>(<span class="php-var">$password</span>) {
        <span class="php-keyword">if</span> (<span class="php-function">strlen</span>(<span class="php-var">$password</span>) &lt; <span class="php-number">8</span>) {
            <span class="php-keyword">throw new</span> <span class="php-class">InvalidArgumentException</span>(<span class="php-string">"Le mot de passe doit faire au moins 8 caractères"</span>);
        }
        <span class="php-var">$this</span>-&gt;password = <span class="php-function">password_hash</span>(<span class="php-var">$password</span>, <span class="php-constant">PASSWORD_DEFAULT</span>);
    }
    
    <span class="php-comment">// Méthodes métier</span>
    <span class="php-keyword">public function</span> <span class="php-function">verifyPassword</span>(<span class="php-var">$password</span>) {
        <span class="php-keyword">return</span> <span class="php-function">password_verify</span>(<span class="php-var">$password</span>, <span class="php-var">$this</span>-&gt;password);
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">activate</span>() {
        <span class="php-var">$this</span>-&gt;isActive = <span class="php-keyword">true</span>;
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">deactivate</span>() {
        <span class="php-var">$this</span>-&gt;isActive = <span class="php-keyword">false</span>;
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Repository Utilisateur avec PDO -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Repository Utilisateur avec PDO</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Implémentation concrète</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">UserRepository</span> <span class="php-keyword">implements</span> <span class="php-class">UserRepositoryInterface</span> {
    <span class="php-keyword">private</span> <span class="php-var">$connection</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-class">PDO</span> <span class="php-var">$connection</span>) {
        <span class="php-var">$this</span>-&gt;connection = <span class="php-var">$connection</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">find</span>(<span class="php-var">$id</span>) {
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">prepare</span>(
            <span class="php-string">"SELECT * FROM users WHERE id = :id"</span>
        );
        <span class="php-var">$statement</span>-&gt;<span class="php-function">execute</span>([<span class="php-string">'id'</span> =&gt; <span class="php-var">$id</span>]);
        <span class="php-var">$data</span> = <span class="php-var">$statement</span>-&gt;<span class="php-function">fetch</span>(<span class="php-constant">PDO</span>::<span class="php-constant">FETCH_ASSOC</span>);
        
        <span class="php-keyword">if</span> (!<span class="php-var">$data</span>) {
            <span class="php-keyword">return</span> <span class="php-keyword">null</span>;
        }
        
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;<span class="php-function">hydrate</span>(<span class="php-var">$data</span>);
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findAll</span>() {
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">query</span>(<span class="php-string">"SELECT * FROM users ORDER BY created_at DESC"</span>);
        <span class="php-var">$users</span> = [];
        
        <span class="php-keyword">while</span> (<span class="php-var">$data</span> = <span class="php-var">$statement</span>-&gt;<span class="php-function">fetch</span>(<span class="php-constant">PDO</span>::<span class="php-constant">FETCH_ASSOC</span>)) {
            <span class="php-var">$users</span>[] = <span class="php-var">$this</span>-&gt;<span class="php-function">hydrate</span>(<span class="php-var">$data</span>);
        }
        
        <span class="php-keyword">return</span> <span class="php-var">$users</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findBy</span>(<span class="php-keyword">array</span> <span class="php-var">$criteria</span>, <span class="php-keyword">array</span> <span class="php-var">$orderBy</span> = <span class="php-keyword">null</span>, <span class="php-var">$limit</span> = <span class="php-keyword">null</span>, <span class="php-var">$offset</span> = <span class="php-keyword">null</span>) {
        <span class="php-var">$sql</span> = <span class="php-string">"SELECT * FROM users WHERE "</span>;
        <span class="php-var">$conditions</span> = [];
        <span class="php-var">$parameters</span> = [];
        
        <span class="php-keyword">foreach</span> (<span class="php-var">$criteria</span> <span class="php-keyword">as</span> <span class="php-var">$field</span> =&gt; <span class="php-var">$value</span>) {
            <span class="php-var">$conditions</span>[] = <span class="php-string">"</span><span class="php-var">$field</span><span class="php-string"> = :</span><span class="php-var">$field</span><span class="php-string">"</span>;
            <span class="php-var">$parameters</span>[<span class="php-var">$field</span>] = <span class="php-var">$value</span>;
        }
        
        <span class="php-var">$sql</span> .= <span class="php-function">implode</span>(<span class="php-string">' AND '</span>, <span class="php-var">$conditions</span>);
        
        <span class="php-keyword">if</span> (<span class="php-var">$orderBy</span>) {
            <span class="php-var">$sql</span> .= <span class="php-string">' ORDER BY '</span>;
            <span class="php-var">$orderConditions</span> = [];
            <span class="php-keyword">foreach</span> (<span class="php-var">$orderBy</span> <span class="php-keyword">as</span> <span class="php-var">$field</span> =&gt; <span class="php-var">$direction</span>) {
                <span class="php-var">$orderConditions</span>[] = <span class="php-string">"</span><span class="php-var">$field</span><span class="php-string"> </span><span class="php-var">$direction</span><span class="php-string">"</span>;
            }
            <span class="php-var">$sql</span> .= <span class="php-function">implode</span>(<span class="php-string">', '</span>, <span class="php-var">$orderConditions</span>);
        }
        
        <span class="php-keyword">if</span> (<span class="php-var">$limit</span>) {
            <span class="php-var">$sql</span> .= <span class="php-string">" LIMIT </span><span class="php-var">$limit</span><span class="php-string">"</span>;
        }
        
        <span class="php-keyword">if</span> (<span class="php-var">$offset</span>) {
            <span class="php-var">$sql</span> .= <span class="php-string">" OFFSET </span><span class="php-var">$offset</span><span class="php-string">"</span>;
        }
        
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">prepare</span>(<span class="php-var">$sql</span>);
        <span class="php-var">$statement</span>-&gt;<span class="php-function">execute</span>(<span class="php-var">$parameters</span>);
        
        <span class="php-var">$users</span> = [];
        <span class="php-keyword">while</span> (<span class="php-var">$data</span> = <span class="php-var">$statement</span>-&gt;<span class="php-function">fetch</span>(<span class="php-constant">PDO</span>::<span class="php-constant">FETCH_ASSOC</span>)) {
            <span class="php-var">$users</span>[] = <span class="php-var">$this</span>-&gt;<span class="php-function">hydrate</span>(<span class="php-var">$data</span>);
        }
        
        <span class="php-keyword">return</span> <span class="php-var">$users</span>;
    }
    
    <span class="php-comment">// Méthodes spécifiques à User</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findByEmail</span>(<span class="php-var">$email</span>) {
        <span class="php-var">$users</span> = <span class="php-var">$this</span>-&gt;<span class="php-function">findBy</span>([<span class="php-string">'email'</span> =&gt; <span class="php-var">$email</span>]);
        <span class="php-keyword">return</span> <span class="php-function">count</span>(<span class="php-var">$users</span>) &gt; <span class="php-number">0</span> ? <span class="php-var">$users</span>[<span class="php-number">0</span>] : <span class="php-keyword">null</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findActiveUsers</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;<span class="php-function">findBy</span>([<span class="php-string">'is_active'</span> =&gt; <span class="php-keyword">true</span>], [<span class="php-string">'created_at'</span> =&gt; <span class="php-string">'DESC'</span>]);
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">countByRole</span>(<span class="php-var">$role</span>) {
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">prepare</span>(
            <span class="php-string">"SELECT COUNT(*) FROM users WHERE role = :role"</span>
        );
        <span class="php-var">$statement</span>-&gt;<span class="php-function">execute</span>([<span class="php-string">'role'</span> =&gt; <span class="php-var">$role</span>]);
        <span class="php-keyword">return</span> (<span class="php-keyword">int</span>)<span class="php-var">$statement</span>-&gt;<span class="php-function">fetchColumn</span>();
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">save</span>(<span class="php-var">$user</span>) {
        <span class="php-keyword">if</span> (!<span class="php-var">$user</span> <span class="php-keyword">instanceof</span> <span class="php-class">User</span>) {
            <span class="php-keyword">throw new</span> <span class="php-class">InvalidArgumentException</span>(<span class="php-string">"Expected User instance"</span>);
        }
        
        <span class="php-keyword">if</span> (<span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>()) {
            <span class="php-comment">// UPDATE</span>
            <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;<span class="php-function">update</span>(<span class="php-var">$user</span>);
        } <span class="php-keyword">else</span> {
            <span class="php-comment">// INSERT</span>
            <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;<span class="php-function">insert</span>(<span class="php-var">$user</span>);
        }
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">delete</span>(<span class="php-var">$user</span>) {
        <span class="php-keyword">if</span> (!<span class="php-var">$user</span> <span class="php-keyword">instanceof</span> <span class="php-class">User</span>) {
            <span class="php-keyword">throw new</span> <span class="php-class">InvalidArgumentException</span>(<span class="php-string">"Expected User instance"</span>);
        }
        
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">prepare</span>(
            <span class="php-string">"DELETE FROM users WHERE id = :id"</span>
        );
        <span class="php-keyword">return</span> <span class="php-var">$statement</span>-&gt;<span class="php-function">execute</span>([<span class="php-string">'id'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>()]);
    }
    
    <span class="php-keyword">private</span> <span class="php-keyword">function</span> <span class="php-function">insert</span>(<span class="php-class">User</span> <span class="php-var">$user</span>) {
        <span class="php-var">$sql</span> = <span class="php-string">"INSERT INTO users (email, password, first_name, last_name, role, is_active, created_at) 
                VALUES (:email, :password, :first_name, :last_name, :role, :is_active, :created_at)"</span>;
        
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">prepare</span>(<span class="php-var">$sql</span>);
        <span class="php-var">$statement</span>-&gt;<span class="php-function">execute</span>([
            <span class="php-string">'email'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>(),
            <span class="php-string">'password'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getPassword</span>(),
            <span class="php-string">'first_name'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getFirstName</span>(),
            <span class="php-string">'last_name'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getLastName</span>(),
            <span class="php-string">'role'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getRole</span>(),
            <span class="php-string">'is_active'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">isActive</span>() ? <span class="php-number">1</span> : <span class="php-number">0</span>,
            <span class="php-string">'created_at'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getCreatedAt</span>()-&gt;<span class="php-function">format</span>(<span class="php-string">'Y-m-d H:i:s'</span>)
        ]);
        
        <span class="php-var">$user</span>-&gt;id = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">lastInsertId</span>();
        <span class="php-keyword">return</span> <span class="php-keyword">true</span>;
    }
    
    <span class="php-keyword">private</span> <span class="php-keyword">function</span> <span class="php-function">update</span>(<span class="php-class">User</span> <span class="php-var">$user</span>) {
        <span class="php-var">$sql</span> = <span class="php-string">"UPDATE users SET 
                email = :email, 
                password = :password, 
                first_name = :first_name, 
                last_name = :last_name, 
                role = :role, 
                is_active = :is_active 
                WHERE id = :id"</span>;
        
        <span class="php-var">$statement</span> = <span class="php-var">$this</span>-&gt;connection-&gt;<span class="php-function">prepare</span>(<span class="php-var">$sql</span>);
        <span class="php-keyword">return</span> <span class="php-var">$statement</span>-&gt;<span class="php-function">execute</span>([
            <span class="php-string">'email'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>(),
            <span class="php-string">'password'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getPassword</span>(),
            <span class="php-string">'first_name'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getFirstName</span>(),
            <span class="php-string">'last_name'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getLastName</span>(),
            <span class="php-string">'role'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getRole</span>(),
            <span class="php-string">'is_active'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">isActive</span>() ? <span class="php-number">1</span> : <span class="php-number">0</span>,
            <span class="php-string">'id'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>()
        ]);
    }
    
    <span class="php-keyword">private</span> <span class="php-keyword">function</span> <span class="php-function">hydrate</span>(<span class="php-keyword">array</span> <span class="php-var">$data</span>) {
        <span class="php-var">$user</span> = <span class="php-keyword">new</span> <span class="php-class">User</span>(
            <span class="php-var">$data</span>[<span class="php-string">'email'</span>],
            <span class="php-string">''</span>, <span class="php-comment">// Mot de passe non utilisé pour l'hydratation</span>
            <span class="php-var">$data</span>[<span class="php-string">'first_name'</span>],
            <span class="php-var">$data</span>[<span class="php-string">'last_name'</span>],
            <span class="php-var">$data</span>[<span class="php-string">'role'</span>]
        );
        
        <span class="php-comment">// Utiliser la réflexion pour définir les propriétés privées</span>
        <span class="php-var">$reflection</span> = <span class="php-keyword">new</span> <span class="php-class">ReflectionClass</span>(<span class="php-class">User</span>);
        
        <span class="php-var">$idProperty</span> = <span class="php-var">$reflection</span>-&gt;<span class="php-function">getProperty</span>(<span class="php-string">'id'</span>);
        <span class="php-var">$idProperty</span>-&gt;<span class="php-function">setAccessible</span>(<span class="php-keyword">true</span>);
        <span class="php-var">$idProperty</span>-&gt;<span class="php-function">setValue</span>(<span class="php-var">$user</span>, (<span class="php-keyword">int</span>)<span class="php-var">$data</span>[<span class="php-string">'id'</span>]);
        
        <span class="php-var">$passwordProperty</span> = <span class="php-var">$reflection</span>-&gt;<span class="php-function">getProperty</span>(<span class="php-string">'password'</span>);
        <span class="php-var">$passwordProperty</span>-&gt;<span class="php-function">setAccessible</span>(<span class="php-keyword">true</span>);
        <span class="php-var">$passwordProperty</span>-&gt;<span class="php-function">setValue</span>(<span class="php-var">$user</span>, <span class="php-var">$data</span>[<span class="php-string">'password'</span>]);
        
        <span class="php-var">$isActiveProperty</span> = <span class="php-var">$reflection</span>-&gt;<span class="php-function">getProperty</span>(<span class="php-string">'isActive'</span>);
        <span class="php-var">$isActiveProperty</span>-&gt;<span class="php-function">setAccessible</span>(<span class="php-keyword">true</span>);
        <span class="php-var">$isActiveProperty</span>-&gt;<span class="php-function">setValue</span>(<span class="php-var">$user</span>, (<span class="php-keyword">bool</span>)<span class="php-var">$data</span>[<span class="php-string">'is_active'</span>]);
        
        <span class="php-var">$createdAtProperty</span> = <span class="php-var">$reflection</span>-&gt;<span class="php-function">getProperty</span>(<span class="php-string">'createdAt'</span>);
        <span class="php-var">$createdAtProperty</span>-&gt;<span class="php-function">setAccessible</span>(<span class="php-keyword">true</span>);
        <span class="php-var">$createdAtProperty</span>-&gt;<span class="php-function">setValue</span>(<span class="php-var">$user</span>, <span class="php-keyword">new</span> <span class="php-class">DateTime</span>(<span class="php-var">$data</span>[<span class="php-string">'created_at'</span>]));
        
        <span class="php-keyword">return</span> <span class="php-var">$user</span>;
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Service et Controller -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Service et Controller</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Service UserService</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">UserService</span> {
    <span class="php-keyword">private</span> <span class="php-var">$userRepository</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-class">UserRepositoryInterface</span> <span class="php-var">$userRepository</span>) {
        <span class="php-var">$this</span>-&gt;userRepository = <span class="php-var">$userRepository</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">registerUser</span>(<span class="php-var">$email</span>, <span class="php-var">$password</span>, <span class="php-var">$firstName</span>, <span class="php-var">$lastName</span>) {
        <span class="php-comment">// Vérifier si l'email existe déjà</span>
        <span class="php-keyword">if</span> (<span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">findByEmail</span>(<span class="php-var">$email</span>)) {
            <span class="php-keyword">throw new</span> <span class="php-class">Exception</span>(<span class="php-string">"Un utilisateur avec cet email existe déjà"</span>);
        }
        
        <span class="php-comment">// Créer l'utilisateur</span>
        <span class="php-var">$user</span> = <span class="php-keyword">new</span> <span class="php-class">User</span>(<span class="php-var">$email</span>, <span class="php-var">$password</span>, <span class="php-var">$firstName</span>, <span class="php-var">$lastName</span>);
        
        <span class="php-comment">// Sauvegarder</span>
        <span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">save</span>(<span class="php-var">$user</span>);
        
        <span class="php-keyword">return</span> <span class="php-var">$user</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">authenticateUser</span>(<span class="php-var">$email</span>, <span class="php-var">$password</span>) {
        <span class="php-var">$user</span> = <span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">findByEmail</span>(<span class="php-var">$email</span>);
        
        <span class="php-keyword">if</span> (!<span class="php-var">$user</span> || !<span class="php-var">$user</span>-&gt;<span class="php-function">isActive</span>()) {
            <span class="php-keyword">return</span> <span class="php-keyword">false</span>;
        }
        
        <span class="php-keyword">if</span> (!<span class="php-var">$user</span>-&gt;<span class="php-function">verifyPassword</span>(<span class="php-var">$password</span>)) {
            <span class="php-keyword">return</span> <span class="php-keyword">false</span>;
        }
        
        <span class="php-keyword">return</span> <span class="php-var">$user</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getUserStats</span>() {
        <span class="php-keyword">return</span> [
            <span class="php-string">'total'</span> =&gt; <span class="php-function">count</span>(<span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">findAll</span>()),
            <span class="php-string">'active'</span> =&gt; <span class="php-function">count</span>(<span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">findActiveUsers</span>()),
            <span class="php-string">'admins'</span> =&gt; <span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">countByRole</span>(<span class="php-string">'admin'</span>),
            <span class="php-string">'users'</span> =&gt; <span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">countByRole</span>(<span class="php-string">'user'</span>)
        ];
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">deactivateUser</span>(<span class="php-var">$userId</span>) {
        <span class="php-var">$user</span> = <span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">find</span>(<span class="php-var">$userId</span>);
        
        <span class="php-keyword">if</span> (!<span class="php-var">$user</span>) {
            <span class="php-keyword">throw new</span> <span class="php-class">Exception</span>(<span class="php-string">"Utilisateur non trouvé"</span>);
        }
        
        <span class="php-var">$user</span>-&gt;<span class="php-function">deactivate</span>();
        <span class="php-var">$this</span>-&gt;userRepository-&gt;<span class="php-function">save</span>(<span class="php-var">$user</span>);
        
        <span class="php-keyword">return</span> <span class="php-keyword">true</span>;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Controller UserController</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">UserController</span> {
    <span class="php-keyword">private</span> <span class="php-var">$userService</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-class">UserService</span> <span class="php-var">$userService</span>) {
        <span class="php-var">$this</span>-&gt;userService = <span class="php-var">$userService</span>;
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">register</span>(<span class="php-keyword">array</span> <span class="php-var">$requestData</span>) {
        <span class="php-keyword">try</span> {
            <span class="php-var">$user</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">registerUser</span>(
                <span class="php-var">$requestData</span>[<span class="php-string">'email'</span>] ?? <span class="php-keyword">null</span>,
                <span class="php-var">$requestData</span>[<span class="php-string">'password'</span>] ?? <span class="php-keyword">null</span>,
                <span class="php-var">$requestData</span>[<span class="php-string">'first_name'</span>] ?? <span class="php-keyword">null</span>,
                <span class="php-var">$requestData</span>[<span class="php-string">'last_name'</span>] ?? <span class="php-keyword">null</span>
            );
            
            <span class="php-keyword">return</span> [
                <span class="php-string">'success'</span> =&gt; <span class="php-keyword">true</span>,
                <span class="php-string">'message'</span> =&gt; <span class="php-string">'Utilisateur créé avec succès'</span>,
                <span class="php-string">'user'</span> =&gt; [
                    <span class="php-string">'id'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>(),
                    <span class="php-string">'email'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>(),
                    <span class="php-string">'name'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getFirstName</span>() . <span class="php-string">' '</span> . <span class="php-var">$user</span>-&gt;<span class="php-function">getLastName</span>()
                ]
            ];
            
        } <span class="php-keyword">catch</span> (<span class="php-class">Exception</span> <span class="php-var">$e</span>) {
            <span class="php-keyword">return</span> [
                <span class="php-string">'success'</span> =&gt; <span class="php-keyword">false</span>,
                <span class="php-string">'message'</span> =&gt; <span class="php-var">$e</span>-&gt;<span class="php-function">getMessage</span>()
            ];
        }
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">login</span>(<span class="php-keyword">array</span> <span class="php-var">$requestData</span>) {
        <span class="php-var">$user</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">authenticateUser</span>(
            <span class="php-var">$requestData</span>[<span class="php-string">'email'</span>] ?? <span class="php-keyword">null</span>,
            <span class="php-var">$requestData</span>[<span class="php-string">'password'</span>] ?? <span class="php-keyword">null</span>
        );
        
        <span class="php-keyword">if</span> (<span class="php-var">$user</span>) {
            <span class="php-comment">// Démarrer la session, créer un token, etc.</span>
            <span class="php-keyword">return</span> [
                <span class="php-string">'success'</span> =&gt; <span class="php-keyword">true</span>,
                <span class="php-string">'message'</span> =&gt; <span class="php-string">'Connexion réussie'</span>,
                <span class="php-string">'user'</span> =&gt; [
                    <span class="php-string">'id'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>(),
                    <span class="php-string">'email'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>(),
                    <span class="php-string">'name'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getFirstName</span>() . <span class="php-string">' '</span> . <span class="php-var">$user</span>-&gt;<span class="php-function">getLastName</span>(),
                    <span class="php-string">'role'</span> =&gt; <span class="php-var">$user</span>-&gt;<span class="php-function">getRole</span>()
                ]
            ];
        } <span class="php-keyword">else</span> {
            <span class="php-keyword">return</span> [
                <span class="php-string">'success'</span> =&gt; <span class="php-keyword">false</span>,
                <span class="php-string">'message'</span> =&gt; <span class="php-string">'Email ou mot de passe incorrect'</span>
            ];
        }
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">stats</span>() {
        <span class="php-var">$stats</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">getUserStats</span>();
        
        <span class="php-keyword">return</span> [
            <span class="php-string">'success'</span> =&gt; <span class="php-keyword">true</span>,
            <span class="php-string">'stats'</span> =&gt; <span class="php-var">$stats</span>
        ];
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Configuration et Injection de Dépendances -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Configuration et Injection de Dépendances</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Container de Dépendances Simple</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">Container</span> {
    <span class="php-keyword">private</span> <span class="php-var">$instances</span> = [];
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>() {
        <span class="php-comment">// Configuration de la base de données</span>
        <span class="php-var">$this</span>-&gt;instances[<span class="php-class">PDO</span>::class] = <span class="php-keyword">function</span>() {
            <span class="php-keyword">return</span> <span class="php-keyword">new</span> <span class="php-class">PDO</span>(
                <span class="php-string">'mysql:host=localhost;dbname=myapp;charset=utf8'</span>,
                <span class="php-string">'username'</span>,
                <span class="php-string">'password'</span>,
                [
                    <span class="php-constant">PDO</span>::<span class="php-constant">ATTR_ERRMODE</span> =&gt; <span class="php-constant">PDO</span>::<span class="php-constant">ERRMODE_EXCEPTION</span>,
                    <span class="php-constant">PDO</span>::<span class="php-constant">ATTR_DEFAULT_FETCH_MODE</span> =&gt; <span class="php-constant">PDO</span>::<span class="php-constant">FETCH_ASSOC</span>
                ]
            );
        };
        
        <span class="php-comment">// Configuration des repositories</span>
        <span class="php-var">$this</span>-&gt;instances[<span class="php-class">UserRepositoryInterface</span>::class] = <span class="php-keyword">function</span>(<span class="php-var">$container</span>) {
            <span class="php-keyword">return</span> <span class="php-keyword">new</span> <span class="php-class">UserRepository</span>(<span class="php-var">$container</span>-&gt;<span class="php-function">get</span>(<span class="php-class">PDO</span>::class));
        };
        
        <span class="php-comment">// Configuration des services</span>
        <span class="php-var">$this</span>-&gt;instances[<span class="php-class">UserService</span>::class] = <span class="php-keyword">function</span>(<span class="php-var">$container</span>) {
            <span class="php-keyword">return</span> <span class="php-keyword">new</span> <span class="php-class">UserService</span>(<span class="php-var">$container</span>-&gt;<span class="php-function">get</span>(<span class="php-class">UserRepositoryInterface</span>::class));
        };
        
        <span class="php-comment">// Configuration des controllers</span>
        <span class="php-var">$this</span>-&gt;instances[<span class="php-class">UserController</span>::class] = <span class="php-keyword">function</span>(<span class="php-var">$container</span>) {
            <span class="php-keyword">return</span> <span class="php-keyword">new</span> <span class="php-class">UserController</span>(<span class="php-var">$container</span>-&gt;<span class="php-function">get</span>(<span class="php-class">UserService</span>::class));
        };
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">get</span>(<span class="php-var">$className</span>) {
        <span class="php-keyword">if</span> (!<span class="php-function">isset</span>(<span class="php-var">$this</span>-&gt;instances[<span class="php-var">$className</span>])) {
            <span class="php-keyword">throw new</span> <span class="php-class">Exception</span>(<span class="php-string">"Class </span><span class="php-var">$className</span><span class="php-string"> not found in container"</span>);
        }
        
        <span class="php-keyword">if</span> (<span class="php-function">is_callable</span>(<span class="php-var">$this</span>-&gt;instances[<span class="php-var">$className</span>])) {
            <span class="php-var">$this</span>-&gt;instances[<span class="php-var">$className</span>] = <span class="php-var">$this</span>-&gt;instances[<span class="php-var">$className</span>](<span class="php-var">$this</span>);
        }
        
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;instances[<span class="php-var">$className</span>];
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Point d'entrée de l'application</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// index.php</span>
<span class="php-keyword">require_once</span> <span class="php-string">'Container.php'</span>;
<span class="php-keyword">require_once</span> <span class="php-string">'src/Entities/User.php'</span>;
<span class="php-keyword">require_once</span> <span class="php-string">'src/Repositories/UserRepository.php'</span>;
<span class="php-keyword">require_once</span> <span class="php-string">'src/Services/UserService.php'</span>;
<span class="php-keyword">require_once</span> <span class="php-string">'src/Controllers/UserController.php'</span>;

<span class="php-comment">// Initialiser le container</span>
<span class="php-var">$container</span> = <span class="php-keyword">new</span> <span class="php-class">Container</span>();

<span class="php-comment">// Router simple</span>
<span class="php-var">$route</span> = <span class="php-var">$_GET</span>[<span class="php-string">'route'</span>] ?? <span class="php-string">'home'</span>;
<span class="php-var">$method</span> = <span class="php-var">$_SERVER</span>[<span class="php-string">'REQUEST_METHOD'</span>];

<span class="php-keyword">try</span> {
    <span class="php-keyword">switch</span> (<span class="php-var">$route</span>) {
        <span class="php-keyword">case</span> <span class="php-string">'register'</span>:
            <span class="php-keyword">if</span> (<span class="php-var">$method</span> === <span class="php-string">'POST'</span>) {
                <span class="php-var">$controller</span> = <span class="php-var">$container</span>-&gt;<span class="php-function">get</span>(<span class="php-class">UserController</span>::class);
                <span class="php-var">$response</span> = <span class="php-var">$controller</span>-&gt;<span class="php-function">register</span>(<span class="php-var">$_POST</span>);
                <span class="php-function">echo</span> <span class="php-function">json_encode</span>(<span class="php-var">$response</span>);
            }
            <span class="php-keyword">break</span>;
            
        <span class="php-keyword">case</span> <span class="php-string">'login'</span>:
            <span class="php-keyword">if</span> (<span class="php-var">$method</span> === <span class="php-string">'POST'</span>) {
                <span class="php-var">$controller</span> = <span class="php-var">$container</span>-&gt;<span class="php-function">get</span>(<span class="php-class">UserController</span>::class);
                <span class="php-var">$response</span> = <span class="php-var">$controller</span>-&gt;<span class="php-function">login</span>(<span class="php-var">$_POST</span>);
                <span class="php-function">echo</span> <span class="php-function">json_encode</span>(<span class="php-var">$response</span>);
            }
            <span class="php-keyword">break</span>;
            
        <span class="php-keyword">case</span> <span class="php-string">'stats'</span>:
            <span class="php-keyword">if</span> (<span class="php-var">$method</span> === <span class="php-string">'GET'</span>) {
                <span class="php-var">$controller</span> = <span class="php-var">$container</span>-&gt;<span class="php-function">get</span>(<span class="php-class">UserController</span>::class);
                <span class="php-var">$response</span> = <span class="php-var">$controller</span>-&gt;<span class="php-function">stats</span>();
                <span class="php-function">echo</span> <span class="php-function">json_encode</span>(<span class="php-var">$response</span>);
            }
            <span class="php-keyword">break</span>;
            
        <span class="php-keyword">default</span>:
            <span class="php-function">echo</span> <span class="php-function">json_encode</span>([<span class="php-string">'message'</span> =&gt; <span class="php-string">'Bienvenue sur l API'</span>]);
    }
    
} <span class="php-keyword">catch</span> (<span class="php-class">Exception</span> <span class="php-var">$e</span>) {
    <span class="php-function">http_response_code</span>(<span class="php-number">500</span>);
    <span class="php-function">echo</span> <span class="php-function">json_encode</span>([
        <span class="php-string">'success'</span> =&gt; <span class="php-keyword">false</span>,
        <span class="php-string">'message'</span> =&gt; <span class="php-var">$e</span>-&gt;<span class="php-function">getMessage</span>()
    ]);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Tests Unitaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Tests Unitaires avec Repository</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Repository Mock pour les tests</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">MockUserRepository</span> <span class="php-keyword">implements</span> <span class="php-class">UserRepositoryInterface</span> {
    <span class="php-keyword">private</span> <span class="php-var">$users</span> = [];
    <span class="php-keyword">private</span> <span class="php-var">$nextId</span> = <span class="php-number">1</span>;
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">find</span>(<span class="php-var">$id</span>) {
        <span class="php-keyword">foreach</span> (<span class="php-var">$this</span>-&gt;users <span class="php-keyword">as</span> <span class="php-var">$user</span>) {
            <span class="php-keyword">if</span> (<span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>() == <span class="php-var">$id</span>) {
                <span class="php-keyword">return</span> <span class="php-var">$user</span>;
            }
        }
        <span class="php-keyword">return</span> <span class="php-keyword">null</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findAll</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;users;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findBy</span>(<span class="php-keyword">array</span> <span class="php-var">$criteria</span>, <span class="php-keyword">array</span> <span class="php-var">$orderBy</span> = <span class="php-keyword">null</span>, <span class="php-var">$limit</span> = <span class="php-keyword">null</span>, <span class="php-var">$offset</span> = <span class="php-keyword">null</span>) {
        <span class="php-comment">// Implémentation simplifiée pour les tests</span>
        <span class="php-keyword">return</span> <span class="php-function">array_filter</span>(<span class="php-var">$this</span>-&gt;users, <span class="php-keyword">function</span>(<span class="php-var">$user</span>) <span class="php-keyword">use</span> (<span class="php-var">$criteria</span>) {
            <span class="php-keyword">foreach</span> (<span class="php-var">$criteria</span> <span class="php-keyword">as</span> <span class="php-var">$field</span> =&gt; <span class="php-var">$value</span>) {
                <span class="php-keyword">if</span> (<span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>() === <span class="php-var">$value</span>) {
                    <span class="php-keyword">return</span> <span class="php-keyword">true</span>;
                }
            }
            <span class="php-keyword">return</span> <span class="php-keyword">false</span>;
        });
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findByEmail</span>(<span class="php-var">$email</span>) {
        <span class="php-keyword">foreach</span> (<span class="php-var">$this</span>-&gt;users <span class="php-keyword">as</span> <span class="php-var">$user</span>) {
            <span class="php-keyword">if</span> (<span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>() === <span class="php-var">$email</span>) {
                <span class="php-keyword">return</span> <span class="php-var">$user</span>;
            }
        }
        <span class="php-keyword">return</span> <span class="php-keyword">null</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findActiveUsers</span>() {
        <span class="php-keyword">return</span> <span class="php-function">array_filter</span>(<span class="php-var">$this</span>-&gt;users, <span class="php-keyword">function</span>(<span class="php-var">$user</span>) {
            <span class="php-keyword">return</span> <span class="php-var">$user</span>-&gt;<span class="php-function">isActive</span>();
        });
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">countByRole</span>(<span class="php-var">$role</span>) {
        <span class="php-keyword">return</span> <span class="php-function">count</span>(<span class="php-function">array_filter</span>(<span class="php-var">$this</span>-&gt;users, <span class="php-keyword">function</span>(<span class="php-var">$user</span>) <span class="php-keyword">use</span> (<span class="php-var">$role</span>) {
            <span class="php-keyword">return</span> <span class="php-var">$user</span>-&gt;<span class="php-function">getRole</span>() === <span class="php-var">$role</span>;
        }));
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">save</span>(<span class="php-var">$user</span>) {
        <span class="php-keyword">if</span> (!<span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>()) {
            <span class="php-comment">// Utiliser la réflexion pour définir l'ID</span>
            <span class="php-var">$reflection</span> = <span class="php-keyword">new</span> <span class="php-class">ReflectionClass</span>(<span class="php-class">User</span>);
            <span class="php-var">$idProperty</span> = <span class="php-var">$reflection</span>-&gt;<span class="php-function">getProperty</span>(<span class="php-string">'id'</span>);
            <span class="php-var">$idProperty</span>-&gt;<span class="php-function">setAccessible</span>(<span class="php-keyword">true</span>);
            <span class="php-var">$idProperty</span>-&gt;<span class="php-function">setValue</span>(<span class="php-var">$user</span>, <span class="php-var">$this</span>-&gt;nextId++);
        }
        
        <span class="php-comment">// Remplacer l'utilisateur existant ou ajouter le nouveau</span>
        <span class="php-var">$this</span>-&gt;users = <span class="php-function">array_filter</span>(<span class="php-var">$this</span>-&gt;users, <span class="php-keyword">function</span>(<span class="php-var">$existingUser</span>) <span class="php-keyword">use</span> (<span class="php-var">$user</span>) {
            <span class="php-keyword">return</span> <span class="php-var">$existingUser</span>-&gt;<span class="php-function">getId</span>() !== <span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>();
        });
        
        <span class="php-var">$this</span>-&gt;users[] = <span class="php-var">$user</span>;
        <span class="php-keyword">return</span> <span class="php-keyword">true</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">delete</span>(<span class="php-var">$user</span>) {
        <span class="php-var">$this</span>-&gt;users = <span class="php-function">array_filter</span>(<span class="php-var">$this</span>-&gt;users, <span class="php-keyword">function</span>(<span class="php-var">$existingUser</span>) <span class="php-keyword">use</span> (<span class="php-var">$user</span>) {
            <span class="php-keyword">return</span> <span class="php-var">$existingUser</span>-&gt;<span class="php-function">getId</span>() !== <span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>();
        });
        <span class="php-keyword">return</span> <span class="php-keyword">true</span>;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Tests PHPUnit</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">class</span> <span class="php-class">UserServiceTest</span> <span class="php-keyword">extends</span> <span class="php-class">TestCase</span> {
    <span class="php-keyword">private</span> <span class="php-var">$userService</span>;
    <span class="php-keyword">private</span> <span class="php-var">$mockRepository</span>;
    
    <span class="php-keyword">protected function</span> <span class="php-function">setUp</span>(): <span class="php-keyword">void</span> {
        <span class="php-var">$this</span>-&gt;mockRepository = <span class="php-keyword">new</span> <span class="php-class">MockUserRepository</span>();
        <span class="php-var">$this</span>-&gt;userService = <span class="php-keyword">new</span> <span class="php-class">UserService</span>(<span class="php-var">$this</span>-&gt;mockRepository);
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">testRegisterUser</span>() {
        <span class="php-var">$user</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">registerUser</span>(
            <span class="php-string">'test@example.com'</span>,
            <span class="php-string">'password123'</span>,
            <span class="php-string">'John'</span>,
            <span class="php-string">'Doe'</span>
        );
        
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertInstanceOf</span>(<span class="php-class">User</span>::class, <span class="php-var">$user</span>);
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertEquals</span>(<span class="php-string">'test@example.com'</span>, <span class="php-var">$user</span>-&gt;<span class="php-function">getEmail</span>());
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertEquals</span>(<span class="php-string">'John'</span>, <span class="php-var">$user</span>-&gt;<span class="php-function">getFirstName</span>());
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertTrue</span>(<span class="php-var">$user</span>-&gt;<span class="php-function">isActive</span>());
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">testRegisterUserWithExistingEmail</span>() {
        <span class="php-comment">// D'abord créer un utilisateur</span>
        <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">registerUser</span>(
            <span class="php-string">'test@example.com'</span>,
            <span class="php-string">'password123'</span>,
            <span class="php-string">'John'</span>,
            <span class="php-string">'Doe'</span>
        );
        
        <span class="php-comment">// Essayer de créer un autre utilisateur avec le même email</span>
        <span class="php-var">$this</span>-&gt;<span class="php-function">expectException</span>(<span class="php-class">Exception</span>::class);
        <span class="php-var">$this</span>-&gt;<span class="php-function">expectExceptionMessage</span>(<span class="php-string">'Un utilisateur avec cet email existe déjà'</span>);
        
        <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">registerUser</span>(
            <span class="php-string">'test@example.com'</span>,
            <span class="php-string">'differentpassword'</span>,
            <span class="php-string">'Jane'</span>,
            <span class="php-string">'Smith'</span>
        );
    }
    
    <span class="php-keyword">public function</span> <span class="php-function">testAuthenticateUser</span>() {
        <span class="php-comment">// Créer un utilisateur</span>
        <span class="php-var">$user</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">registerUser</span>(
            <span class="php-string">'test@example.com'</span>,
            <span class="php-string">'password123'</span>,
            <span class="php-string">'John'</span>,
            <span class="php-string">'Doe'</span>
        );
        
        <span class="php-comment">// Tester l'authentification réussie</span>
        <span class="php-var">$authenticatedUser</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">authenticateUser</span>(
            <span class="php-string">'test@example.com'</span>,
            <span class="php-string">'password123'</span>
        );
        
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertInstanceOf</span>(<span class="php-class">User</span>::class, <span class="php-var">$authenticatedUser</span>);
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertEquals</span>(<span class="php-var">$user</span>-&gt;<span class="php-function">getId</span>(), <span class="php-var">$authenticatedUser</span>-&gt;<span class="php-function">getId</span>());
        
        <span class="php-comment">// Tester l'authentification échouée</span>
        <span class="php-var">$failedAuth</span> = <span class="php-var">$this</span>-&gt;userService-&gt;<span class="php-function">authenticateUser</span>(
            <span class="php-string">'test@example.com'</span>,
            <span class="php-string">'wrongpassword'</span>
        );
        
        <span class="php-var">$this</span>-&gt;<span class="php-function">assertFalse</span>(<span class="php-var">$failedAuth</span>);
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Avantages et Bonnes Pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages et Bonnes Pratiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Avantages du Pattern Repository</h3>
                    <ul>
                        <li><strong>Découplage</strong> : La logique métier ne dépend pas de la source de données</li>
                        <li><strong>Testabilité</strong> : Facile à mock pour les tests unitaires</li>
                        <li><strong>Maintenabilité</strong> : Changements de base de données localisés</li>
                        <li><strong>Réutilisabilité</strong> : Même interface pour différentes sources</li>
                        <li><strong>Sécurité</strong> : Centralisation des requêtes SQL</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes Pratiques</h3>
                    <ul>
                        <li><strong>Utiliser des interfaces</strong> pour les repositories</li>
                        <li><strong>Une repository par entité</strong> (sauf cas particuliers)</li>
                        <li><strong>Injecter les dépendances</strong> via le constructeur</li>
                        <li><strong>Centraliser les requêtes complexes</strong> dans les repositories</li>
                        <li><strong>Utiliser l'injection de dépendances</strong> pour la configuration</li>
                        <li><strong>Créer des repositories mock</strong> pour les tests</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Structure de dossiers recommandée</h3>
                    <div class="code-example">
                        <pre><code>src/
├── Controllers/
│   ├── UserController.php
│   └── ProductController.php
├── Entities/
│   ├── User.php
│   └── Product.php
├── Repositories/
│   ├── Interfaces/
│   │   ├── UserRepositoryInterface.php
│   │   └── ProductRepositoryInterface.php
│   ├── UserRepository.php
│   └── ProductRepository.php
├── Services/
│   ├── UserService.php
│   └── ProductService.php
└── Infrastructure/
    ├── Database/
    │   └── Connection.php
    └── DI/
        └── Container.php</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Récapitulatif</h3>
                    <ul>
                        <li><strong>Repository Pattern</strong> : Abstraction de l'accès aux données</li>
                        <li><strong>Separation of Concerns</strong> : Logique métier ≠ Accès données</li>
                        <li><strong>Test-Driven Development</strong> : Facilité de testing avec des mocks</li>
                        <li><strong>Dependency Injection</strong> : Gestion propre des dépendances</li>
                        <li><strong>Interface Segregation</strong> : Contrats clairs entre les couches</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Prochaines Étapes</h3>
                    <p>
                        Pour aller plus loin avec les repositories :
                    </p>
                    <ul>
                        <li><strong>Repository Generic</strong> avec des classes abstraites</li>
                        <li><strong>Pattern Unit of Work</strong> pour gérer les transactions</li>
                        <li><strong>ORM Integration</strong> avec Doctrine ou Eloquent</li>
                        <li><strong>CQRS Pattern</strong> pour séparer lecture/écriture</li>
                        <li><strong>Repository Caching</strong> pour les performances</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Checklist de mise en œuvre</h3>
                    <ul>
                        <li>✅ <strong>Définir les interfaces</strong> de repository</li>
                        <li>✅ <strong>Implémenter les repositories</strong> concrets</li>
                        <li>✅ <strong>Créer les services</strong> métier</li>
                        <li>✅ <strong>Configurer l'injection</strong> de dépendances</li>
                        <li>✅ <strong>Écrire les tests</strong> unitaires</li>
                        <li>✅ <strong>Structurer le projet</strong> de manière cohérente</li>
                    </ul>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'RepositoryPatternLesson'
}
</script>

<style scoped>
/* Les styles restent identiques aux leçons précédentes */
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
    word-wrap: break-word;
    word-break: break-word;
}

pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* COULEURS PHP */
.php-keyword {
    color: #FF6B8B !important;
    font-weight: bold;
}

.php-class {
    color: #4EC9B0 !important;
}

.php-function {
    color: #DCDCAA !important;
}

.php-var {
    color: #9CDCFE !important;
}

.php-string {
    color: #CE9178 !important;
}

.php-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.php-number {
    color: #B5CEA8 !important;
}

.php-constant {
    color: #569CD6 !important;
}

.php-escape {
    color: #D7BA7D !important;
}

.warning-text {
    color: #d63031;
    font-weight: bold;
    margin-top: 0.5rem;
}

.success-text {
    color: #00b894;
    font-weight: bold;
    margin-top: 0.5rem;
}

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

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* Responsive */
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
</style>