<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Connexion à MySQL en PHP avec Architecture MVC</h1>
                <p class="lesson-meta text-white">Apprenez à structurer votre application PHP avec le pattern MVC et à
                    interagir avec une base de données MySQL</p>
                <p class="lesson-meta text-white">
                    <span>Niveau : Intermédiaire</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>Dans cette leçon, nous allons découvrir comment connecter une application PHP à une base de données
                    MySQL en utilisant l'architecture MVC (Modèle-Vue-Contrôleur). Cette architecture permet de séparer
                    les préoccupations de votre application pour une meilleure maintenabilité et évolutivité.</p>

                <div class="textExemple">
                    <h3 class="text-purple">Objectifs d'apprentissage</h3>
                    <ul>
                        <li>Comprendre l'architecture MVC et ses avantages</li>
                        <li>Configurer une connexion à MySQL en PHP</li>
                        <li>Créer un modèle pour interagir avec la base de données</li>
                        <li>Implémenter un contrôleur pour gérer la logique métier</li>
                        <li>Afficher les données dans une vue</li>
                    </ul>
                </div>
            </section>

            <!-- Section 1: Architecture MVC -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">1. Comprendre l'Architecture MVC</h2>
                <p>L'architecture MVC sépare votre application en trois composants distincts :</p>

                <div class="code-example">
                    <h3 class="text-purple">Structure MVC</h3>
                    <pre><code class="language-php"><span class="comment">// Structure de dossiers MVC typique</span>
<span class="variable">app</span>/
├── <span class="variable">controllers</span>/    <span class="comment"># Contrôleurs - Logique métier</span>
├── <span class="variable">models</span>/         <span class="comment"># Modèles - Interaction avec la base de données</span>
├── <span class="variable">views</span>/          <span class="comment"># Vues - Présentation des données</span>
└── <span class="variable">config</span>/         <span class="comment"># Configuration (connexion DB, etc.)</span></code></pre>
                </div>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Rôle de chaque composant</h4>
                        <ul>
                            <li><strong>Modèle (Model)</strong> : Gère les données et la logique métier</li>
                            <li><strong>Vue (View)</strong> : Présente les données à l'utilisateur</li>
                            <li><strong>Contrôleur (Controller)</strong> : Reçoit les entrées utilisateur et coordonne
                                modèle et vue</li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="text-purple">Avantages du MVC</h4>
                        <ul>
                            <li>Séparation des préoccupations</li>
                            <li>Code plus maintenable et réutilisable</li>
                            <li>Facilite le travail d'équipe</li>
                            <li>Meilleure testabilité</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Section 2: Configuration de la connexion MySQL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">2. Configuration de la Connexion MySQL</h2>
                <p>Commençons par configurer la connexion à notre base de données MySQL.</p>

                <div class="code-example">
                    <h3 class="text-purple">Fichier de configuration de la base de données</h3>
                    <pre><code class="language-php"><span class="keyword">&lt;?php</span>
<span class="comment">// app/config/Database.php</span>

<span class="keyword">class</span> <span class="class-name">Database</span> {
    <span class="keyword">private</span> <span class="variable">$host</span> = <span class="string">'localhost'</span>;
    <span class="keyword">private</span> <span class="variable">$db_name</span> = <span class="string">'mon_application'</span>;
    <span class="keyword">private</span> <span class="variable">$username</span> = <span class="string">'root'</span>;
    <span class="keyword">private</span> <span class="variable">$password</span> = <span class="string">''</span>;
    <span class="keyword">private</span> <span class="variable">$conn</span>;

    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">connect</span>() {
        <span class="variable">$this</span>-&gt;conn = <span class="keyword">null</span>;

        <span class="keyword">try</span> {
            <span class="variable">$this</span>-&gt;conn = <span class="keyword">new</span> <span class="class-name">PDO</span>(
                <span class="string">"mysql:host="</span> . <span class="variable">$this</span>-&gt;host . <span class="string">";dbname="</span> . <span class="variable">$this</span>-&gt;db_name,
                <span class="variable">$this</span>-&gt;username,
                <span class="variable">$this</span>-&gt;password
            );
            <span class="variable">$this</span>-&gt;conn-&gt;<span class="function">setAttribute</span>(PDO::<span class="constant">ATTR_ERRMODE</span>, PDO::<span class="constant">ERRMODE_EXCEPTION</span>);
            <span class="variable">$this</span>-&gt;conn-&gt;<span class="function">setAttribute</span>(PDO::<span class="constant">ATTR_DEFAULT_FETCH_MODE</span>, PDO::<span class="constant">FETCH_ASSOC</span>);
        } <span class="keyword">catch</span>(PDOException <span class="variable">$e</span>) {
            <span class="keyword">echo</span> <span class="string">"Erreur de connexion: "</span> . <span class="variable">$e</span>-&gt;<span class="function">getMessage</span>();
        }

        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;conn;
    }
}
<span class="keyword">?&gt;</span></code></pre>
                </div>

                <div class="textExemple">
                    <h4 class="text-purple">Explications</h4>
                    <ul>
                        <li>Nous utilisons PDO (PHP Data Objects) pour une connexion sécurisée</li>
                        <li>PDO::ATTR_ERRMODE permet de gérer les erreurs de manière appropriée</li>
                        <li>PDO::FETCH_ASSOC retourne les résultats sous forme de tableau associatif</li>
                        <li>Le bloc try/catch permet de capturer les exceptions PDO</li>
                    </ul>
                </div>
            </section>

            <!-- Section 3: Création du Modèle -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">3. Création d'un Modèle</h2>
                <p>Le modèle représente les données et la logique métier de notre application.</p>

                <div class="code-example">
                    <h3 class="text-purple">Modèle Utilisateur</h3>
                    <pre><code class="language-php"><span class="keyword">&lt;?php</span>
<span class="comment">// app/models/User.php</span>

<span class="keyword">class</span> <span class="class-name">User</span> {
    <span class="keyword">private</span> <span class="variable">$conn</span>;
    <span class="keyword">private</span> <span class="variable">$table</span> = <span class="string">'users'</span>;

    <span class="keyword">public</span> <span class="variable">$id</span>;
    <span class="keyword">public</span> <span class="variable">$name</span>;
    <span class="keyword">public</span> <span class="variable">$email</span>;
    <span class="keyword">public</span> <span class="variable">$created_at</span>;

    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">__construct</span>(<span class="variable">$db</span>) {
        <span class="variable">$this</span>-&gt;conn = <span class="variable">$db</span>;
    }

    <span class="comment">// Lire tous les utilisateurs</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">read</span>() {
        <span class="variable">$query</span> = <span class="string">'SELECT * FROM '</span> . <span class="variable">$this</span>-&gt;table . <span class="string">' ORDER BY created_at DESC'</span>;
        
        <span class="variable">$stmt</span> = <span class="variable">$this</span>-&gt;conn-&gt;<span class="function">prepare</span>(<span class="variable">$query</span>);
        <span class="variable">$stmt</span>-&gt;<span class="function">execute</span>();
        
        <span class="keyword">return</span> <span class="variable">$stmt</span>;
    }

    <span class="comment">// Lire un seul utilisateur</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">read_single</span>() {
        <span class="variable">$query</span> = <span class="string">'SELECT * FROM '</span> . <span class="variable">$this</span>-&gt;table . <span class="string">' WHERE id = ? LIMIT 0,1'</span>;
        
        <span class="variable">$stmt</span> = <span class="variable">$this</span>-&gt;conn-&gt;<span class="function">prepare</span>(<span class="variable">$query</span>);
        <span class="variable">$stmt</span>-&gt;<span class="function">bindParam</span>(<span class="number">1</span>, <span class="variable">$this</span>-&gt;id);
        <span class="variable">$stmt</span>-&gt;<span class="function">execute</span>();
        
        <span class="variable">$row</span> = <span class="variable">$stmt</span>-&gt;<span class="function">fetch</span>(PDO::<span class="constant">FETCH_ASSOC</span>);
        
        <span class="variable">$this</span>-&gt;name = <span class="variable">$row</span>[<span class="string">'name'</span>];
        <span class="variable">$this</span>-&gt;email = <span class="variable">$row</span>[<span class="string">'email'</span>];
        <span class="variable">$this</span>-&gt;created_at = <span class="variable">$row</span>[<span class="string">'created_at'</span>];
    }

    <span class="comment">// Créer un utilisateur</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">create</span>() {
        <span class="variable">$query</span> = <span class="string">'INSERT INTO '</span> . <span class="variable">$this</span>-&gt;table . <span class="string">' 
                  SET name = :name, email = :email'</span>;
        
        <span class="variable">$stmt</span> = <span class="variable">$this</span>-&gt;conn-&gt;<span class="function">prepare</span>(<span class="variable">$query</span>);
        
        <span class="comment">// Nettoyer les données</span>
        <span class="variable">$this</span>-&gt;name = <span class="function">htmlspecialchars</span>(<span class="function">strip_tags</span>(<span class="variable">$this</span>-&gt;name));
        <span class="variable">$this</span>-&gt;email = <span class="function">htmlspecialchars</span>(<span class="function">strip_tags</span>(<span class="variable">$this</span>-&gt;email));
        
        <span class="comment">// Lier les données</span>
        <span class="variable">$stmt</span>-&gt;<span class="function">bindParam</span>(<span class="string">':name'</span>, <span class="variable">$this</span>-&gt;name);
        <span class="variable">$stmt</span>-&gt;<span class="function">bindParam</span>(<span class="string">':email'</span>, <span class="variable">$this</span>-&gt;email);
        
        <span class="keyword">if</span>(<span class="variable">$stmt</span>-&gt;<span class="function">execute</span>()) {
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        
        <span class="function">printf</span>(<span class="string">"Erreur: %s.\n"</span>, <span class="variable">$stmt</span>-&gt;error);
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }
}
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 4: Création du Contrôleur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">4. Création d'un Contrôleur</h2>
                <p>Le contrôleur gère la logique de l'application et coordonne les interactions entre le modèle et la
                    vue.</p>

                <div class="code-example">
                    <h3 class="text-purple">Contrôleur Utilisateur</h3>
                    <pre><code class="language-php"><span class="keyword">&lt;?php</span>
<span class="comment">// app/controllers/UserController.php</span>

<span class="keyword">class</span> <span class="class-name">UserController</span> {
    <span class="keyword">private</span> <span class="variable">$userModel</span>;
    <span class="keyword">private</span> <span class="variable">$db</span>;

    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">__construct</span>() {
        <span class="variable">$this</span>-&gt;db = (<span class="keyword">new</span> <span class="class-name">Database</span>())-&gt;<span class="function">connect</span>();
        <span class="variable">$this</span>-&gt;userModel = <span class="keyword">new</span> <span class="class-name">User</span>(<span class="variable">$this</span>-&gt;db);
    }

    <span class="comment">// Afficher tous les utilisateurs</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">index</span>() {
        <span class="variable">$result</span> = <span class="variable">$this</span>-&gt;userModel-&gt;<span class="function">read</span>();
        <span class="variable">$num</span> = <span class="variable">$result</span>-&gt;<span class="function">rowCount</span>();

        <span class="keyword">if</span>(<span class="variable">$num</span> &gt; <span class="number">0</span>) {
            <span class="variable">$users_arr</span> = <span class="keyword">array</span>();
            <span class="variable">$users_arr</span>[<span class="string">'data'</span>] = <span class="keyword">array</span>();

            <span class="keyword">while</span>(<span class="variable">$row</span> = <span class="variable">$result</span>-&gt;<span class="function">fetch</span>(PDO::<span class="constant">FETCH_ASSOC</span>)) {
                <span class="function">extract</span>(<span class="variable">$row</span>);

                <span class="variable">$user_item</span> = <span class="keyword">array</span>(
                    <span class="string">'id'</span> =&gt; <span class="variable">$id</span>,
                    <span class="string">'name'</span> =&gt; <span class="variable">$name</span>,
                    <span class="string">'email'</span> =&gt; <span class="variable">$email</span>,
                    <span class="string">'created_at'</span> =&gt; <span class="variable">$created_at</span>
                );

                <span class="function">array_push</span>(<span class="variable">$users_arr</span>[<span class="string">'data'</span>], <span class="variable">$user_item</span>);
            }

            <span class="comment">// Afficher la vue</span>
            <span class="function">require_once</span> <span class="string">'app/views/users/index.php'</span>;
        } <span class="keyword">else</span> {
            <span class="keyword">echo</span> <span class="function">json_encode</span>(<span class="keyword">array</span>(<span class="string">'message'</span> =&gt; <span class="string">'Aucun utilisateur trouvé'</span>));
        }
    }

    <span class="comment">// Afficher un utilisateur</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">show</span>(<span class="variable">$id</span>) {
        <span class="variable">$this</span>-&gt;userModel-&gt;id = <span class="variable">$id</span>;
        <span class="variable">$this</span>-&gt;userModel-&gt;<span class="function">read_single</span>();

        <span class="variable">$user_arr</span> = <span class="keyword">array</span>(
            <span class="string">'id'</span> =&gt; <span class="variable">$this</span>-&gt;userModel-&gt;id,
            <span class="string">'name'</span> =&gt; <span class="variable">$this</span>-&gt;userModel-&gt;name,
            <span class="string">'email'</span> =&gt; <span class="variable">$this</span>-&gt;userModel-&gt;email,
            <span class="string">'created_at'</span> =&gt; <span class="variable">$this</span>-&gt;userModel-&gt;created_at
        );

        <span class="comment">// Afficher la vue</span>
        <span class="function">require_once</span> <span class="string">'app/views/users/show.php'</span>;
    }

    <span class="comment">// Créer un utilisateur</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">create</span>() {
        <span class="keyword">if</span>(<span class="variable">$_SERVER</span>[<span class="string">'REQUEST_METHOD'</span>] == <span class="string">'POST'</span>) {
            <span class="variable">$this</span>-&gt;userModel-&gt;name = <span class="variable">$_POST</span>[<span class="string">'name'</span>];
            <span class="variable">$this</span>-&gt;userModel-&gt;email = <span class="variable">$_POST</span>[<span class="string">'email'</span>];

            <span class="keyword">if</span>(<span class="variable">$this</span>-&gt;userModel-&gt;<span class="function">create</span>()) {
                <span class="function">header</span>(<span class="string">'Location: /users'</span>);
            } <span class="keyword">else</span> {
                <span class="keyword">echo</span> <span class="string">'Erreur lors de la création'</span>;
            }
        } <span class="keyword">else</span> {
            <span class="function">require_once</span> <span class="string">'app/views/users/create.php'</span>;
        }
    }
}
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 5: Création de la Vue -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">5. Création d'une Vue</h2>
                <p>La vue présente les données à l'utilisateur de manière formatée.</p>

                <div class="code-example">
                    <h3 class="text-purple">Vue pour afficher tous les utilisateurs</h3>
                    <pre><code class="language-php"><span class="keyword">&lt;!DOCTYPE</span> <span class="variable">html</span><span class="keyword">&gt;</span>
<span class="keyword">&lt;html</span> <span class="variable">lang</span>=<span class="string">"fr"</span><span class="keyword">&gt;</span>
<span class="keyword">&lt;head&gt;</span>
    <span class="keyword">&lt;meta</span> <span class="variable">charset</span>=<span class="string">"UTF-8"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;meta</span> <span class="variable">name</span>=<span class="string">"viewport"</span> <span class="variable">content</span>=<span class="string">"width=device-width, initial-scale=1.0"</span><span class="keyword">&gt;</span>
    <span class="keyword">&lt;title&gt;</span>Liste des Utilisateurs<span class="keyword">&lt;/title&gt;</span>
    <span class="keyword">&lt;link</span> <span class="variable">href</span>=<span class="string">"https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"</span> <span class="variable">rel</span>=<span class="string">"stylesheet"</span><span class="keyword">&gt;</span>
<span class="keyword">&lt;/head&gt;</span>
<span class="keyword">&lt;body&gt;</span>
    <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"container mt-5"</span><span class="keyword">&gt;</span>
        <span class="keyword">&lt;h1</span> <span class="variable">class</span>=<span class="string">"mb-4"</span><span class="keyword">&gt;</span>Liste des Utilisateurs<span class="keyword">&lt;/h1&gt;</span>
        
        <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"mb-3"</span><span class="keyword">&gt;</span>
            <span class="keyword">&lt;a</span> <span class="variable">href</span>=<span class="string">"/users/create"</span> <span class="variable">class</span>=<span class="string">"btn btn-primary"</span><span class="keyword">&gt;</span>Ajouter un utilisateur<span class="keyword">&lt;/a&gt;</span>
        <span class="keyword">&lt;/div&gt;</span>

        <span class="keyword">&lt;?php</span> <span class="keyword">if</span>(<span class="function">isset</span>(<span class="variable">$users_arr</span>[<span class="string">'data'</span>]) &amp;&amp; <span class="function">count</span>(<span class="variable">$users_arr</span>[<span class="string">'data'</span>]) &gt; <span class="number">0</span>): <span class="keyword">?&gt;</span>
            <span class="keyword">&lt;table</span> <span class="variable">class</span>=<span class="string">"table table-striped"</span><span class="keyword">&gt;</span>
                <span class="keyword">&lt;thead&gt;</span>
                    <span class="keyword">&lt;tr&gt;</span>
                        <span class="keyword">&lt;th&gt;</span>ID<span class="keyword">&lt;/th&gt;</span>
                        <span class="keyword">&lt;th&gt;</span>Nom<span class="keyword">&lt;/th&gt;</span>
                        <span class="keyword">&lt;th&gt;</span>Email<span class="keyword">&lt;/th&gt;</span>
                        <span class="keyword">&lt;th&gt;</span>Date de création<span class="keyword">&lt;/th&gt;</span>
                        <span class="keyword">&lt;th&gt;</span>Actions<span class="keyword">&lt;/th&gt;</span>
                    <span class="keyword">&lt;/tr&gt;</span>
                <span class="keyword">&lt;/thead&gt;</span>
                <span class="keyword">&lt;tbody&gt;</span>
                    <span class="keyword">&lt;?php</span> <span class="keyword">foreach</span>(<span class="variable">$users_arr</span>[<span class="string">'data'</span>] <span class="keyword">as</span> <span class="variable">$user</span>): <span class="keyword">?&gt;</span>
                        <span class="keyword">&lt;tr&gt;</span>
                            <span class="keyword">&lt;td&gt;</span><span class="keyword">&lt;?php</span> <span class="keyword">echo</span> <span class="variable">$user</span>[<span class="string">'id'</span>]; <span class="keyword">?&gt;</span><span class="keyword">&lt;/td&gt;</span>
                            <span class="keyword">&lt;td&gt;</span><span class="keyword">&lt;?php</span> <span class="keyword">echo</span> <span class="variable">$user</span>[<span class="string">'name'</span>]; <span class="keyword">?&gt;</span><span class="keyword">&lt;/td&gt;</span>
                            <span class="keyword">&lt;td&gt;</span><span class="keyword">&lt;?php</span> <span class="keyword">echo</span> <span class="variable">$user</span>[<span class="string">'email'</span>]; <span class="keyword">?&gt;</span><span class="keyword">&lt;/td&gt;</span>
                            <span class="keyword">&lt;td&gt;</span><span class="keyword">&lt;?php</span> <span class="keyword">echo</span> <span class="variable">$user</span>[<span class="string">'created_at'</span>]; <span class="keyword">?&gt;</span><span class="keyword">&lt;/td&gt;</span>
                            <span class="keyword">&lt;td&gt;</span>
                                <span class="keyword">&lt;a</span> <span class="variable">href</span>=<span class="string">"/users/&lt;?php</span> <span class="keyword">echo</span> <span class="variable">$user</span>[<span class="string">'id'</span>]; <span class="keyword">?&gt;"</span> <span class="variable">class</span>=<span class="string">"btn btn-info btn-sm"</span><span class="keyword">&gt;</span>Voir<span class="keyword">&lt;/a&gt;</span>
                            <span class="keyword">&lt;/td&gt;</span>
                        <span class="keyword">&lt;/tr&gt;</span>
                    <span class="keyword">&lt;?php</span> <span class="keyword">endforeach</span>; <span class="keyword">?&gt;</span>
                <span class="keyword">&lt;/tbody&gt;</span>
            <span class="keyword">&lt;/table&gt;</span>
        <span class="keyword">&lt;?php</span> <span class="keyword">else</span>: <span class="keyword">?&gt;</span>
            <span class="keyword">&lt;div</span> <span class="variable">class</span>=<span class="string">"alert alert-info"</span><span class="keyword">&gt;</span>Aucun utilisateur trouvé<span class="keyword">&lt;/div&gt;</span>
        <span class="keyword">&lt;?php</span> <span class="keyword">endif</span>; <span class="keyword">?&gt;</span>
    <span class="keyword">&lt;/div&gt;</span>
<span class="keyword">&lt;/body&gt;</span>
<span class="keyword">&lt;/html&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 6: Routage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">6. Système de Routage</h2>
                <p>Le routeur dirige les requêtes vers les contrôleurs appropriés.</p>

                <div class="code-example">
                    <h3 class="text-purple">Routeur simple</h3>
                    <pre><code class="language-php"><span class="keyword">&lt;?php</span>
<span class="comment">// index.php (point d'entrée de l'application)</span>

<span class="function">require_once</span> <span class="string">'app/config/Database.php'</span>;
<span class="function">require_once</span> <span class="string">'app/models/User.php'</span>;
<span class="function">require_once</span> <span class="string">'app/controllers/UserController.php'</span>;

<span class="variable">$request</span> = <span class="variable">$_SERVER</span>[<span class="string">'REQUEST_URI'</span>];
<span class="variable">$method</span> = <span class="variable">$_SERVER</span>[<span class="string">'REQUEST_METHOD'</span>];

<span class="keyword">switch</span> (<span class="variable">$request</span>) {
    <span class="keyword">case</span> <span class="string">'/'</span>:
        <span class="function">require</span> <span class="string">'app/views/home.php'</span>;
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">'/users'</span>:
        <span class="variable">$userController</span> = <span class="keyword">new</span> <span class="class-name">UserController</span>();
        <span class="variable">$userController</span>-&gt;<span class="function">index</span>();
        <span class="keyword">break</span>;
    <span class="keyword">case</span> <span class="string">'/users/create'</span>:
        <span class="variable">$userController</span> = <span class="keyword">new</span> <span class="class-name">UserController</span>();
        <span class="keyword">if</span>(<span class="variable">$method</span> == <span class="string">'POST'</span>) {
            <span class="variable">$userController</span>-&gt;<span class="function">create</span>();
        } <span class="keyword">else</span> {
            <span class="function">require</span> <span class="string">'app/views/users/create.php'</span>;
        }
        <span class="keyword">break</span>;
    <span class="keyword">case</span> (<span class="function">preg_match</span>(<span class="string">'/\/users\/(\d+)/'</span>, <span class="variable">$request</span>, <span class="variable">$matches</span>) ? <span class="keyword">true</span> : <span class="keyword">false</span>):
        <span class="variable">$userController</span> = <span class="keyword">new</span> <span class="class-name">UserController</span>();
        <span class="variable">$userController</span>-&gt;<span class="function">show</span>(<span class="variable">$matches</span>[<span class="number">1</span>]);
        <span class="keyword">break</span>;
    <span class="keyword">default</span>:
        <span class="function">http_response_code</span>(<span class="number">404</span>);
        <span class="function">require</span> <span class="string">'app/views/404.php'</span>;
        <span class="keyword">break</span>;
}
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 7: Exercice Pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">7. Exercice Pratique</h2>
                <p>Maintenant que nous avons vu les bases, essayez de mettre en pratique ces concepts.</p>

                <div class="exercise">
                    <h3 class="text-purple">Exercice : Système de Blog</h3>
                    <p>Créez un système de blog simple avec les fonctionnalités suivantes :</p>
                    <ul>
                        <li>Table "posts" avec les champs : id, title, content, author, created_at</li>
                        <li>Afficher la liste des articles</li>
                        <li>Afficher un article individuel</li>
                        <li>Créer un nouvel article</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Structure de la table posts</h4>
                            <pre><code class="language-sql"><span class="keyword">CREATE TABLE</span> <span class="variable">posts</span> (
    <span class="variable">id</span> <span class="class-name">INT</span> <span class="keyword">AUTO_INCREMENT PRIMARY KEY</span>,
    <span class="variable">title</span> <span class="class-name">VARCHAR</span>(<span class="number">255</span>) <span class="keyword">NOT NULL</span>,
    <span class="variable">content</span> <span class="class-name">TEXT</span> <span class="keyword">NOT NULL</span>,
    <span class="variable">author</span> <span class="class-name">VARCHAR</span>(<span class="number">100</span>) <span class="keyword">NOT NULL</span>,
    <span class="variable">created_at</span> <span class="class-name">TIMESTAMP</span> <span class="keyword">DEFAULT</span> <span class="function">CURRENT_TIMESTAMP</span>
);</code></pre>

                            <h4 class="text-purple">Modèle Post</h4>
                            <pre><code class="language-php"><span class="keyword">class</span> <span class="class-name">Post</span> {
    <span class="keyword">private</span> <span class="variable">$conn</span>;
    <span class="keyword">private</span> <span class="variable">$table</span> = <span class="string">'posts'</span>;

    <span class="keyword">public</span> <span class="variable">$id</span>;
    <span class="keyword">public</span> <span class="variable">$title</span>;
    <span class="keyword">public</span> <span class="variable">$content</span>;
    <span class="keyword">public</span> <span class="variable">$author</span>;
    <span class="keyword">public</span> <span class="variable">$created_at</span>;

    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">__construct</span>(<span class="variable">$db</span>) {
        <span class="variable">$this</span>-&gt;conn = <span class="variable">$db</span>;
    }

    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">read</span>() {
        <span class="variable">$query</span> = <span class="string">'SELECT * FROM '</span> . <span class="variable">$this</span>-&gt;table . <span class="string">' ORDER BY created_at DESC'</span>;
        <span class="variable">$stmt</span> = <span class="variable">$this</span>-&gt;conn-&gt;<span class="function">prepare</span>(<span class="variable">$query</span>);
        <span class="variable">$stmt</span>-&gt;<span class="function">execute</span>();
        <span class="keyword">return</span> <span class="variable">$stmt</span>;
    }

    <span class="comment">// Ajoutez les autres méthodes (read_single, create, etc.)</span>
}</code></pre>

                            <p>Continuez en créant le contrôleur PostController et les vues correspondantes en suivant
                                le même pattern que pour les utilisateurs.</p>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Section 8: Bonnes Pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">8. Bonnes Pratiques et Sécurité</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Sécurité</h3>
                        <ul>
                            <li>Toujours utiliser des requêtes préparées</li>
                            <li>Valider et échapper les entrées utilisateur</li>
                            <li>Utiliser des mots de passe forts pour la base de données</li>
                            <li>Ne pas exposer les informations de connexion</li>
                        </ul>
                    </div>
                    <div>
                        <h3 class="text-purple">Performance</h3>
                        <ul>
                            <li>Fermer les connexions à la base de données</li>
                            <li>Utiliser des index sur les colonnes fréquemment interrogées</li>
                            <li>Limiter les données récupérées avec SELECT</li>
                            <li>Mettre en cache les requêtes répétitives</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Section 9: Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p>Vous avez maintenant les bases pour créer une application PHP connectée à MySQL en utilisant
                    l'architecture MVC. Cette approche vous permettra de développer des applications plus structurées,
                    maintenables et évolutives.</p>

                <div class="textExemple">
                    <h3 class="text-purple">Prochaines étapes</h3>
                    <ul>
                        <li>Explorer des frameworks PHP comme Laravel ou Symfony qui implémentent MVC</li>
                        <li>Apprendre à gérer les relations entre tables</li>
                        <li>Découvrir l'authentification et les autorisations</li>
                        <li>Implémenter des tests unitaires pour vos modèles et contrôleurs</li>
                    </ul>
                </div>

                <a href="#" class="btn-purple btn-hover">Passer à la leçon suivante</a>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MySQLPHPLesson',
    data() {
        return {
            lessonTitle: 'Connexion à MySQL en PHP avec Architecture MVC'
        }
    },
    head() {
        return {
            title: this.lessonTitle,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Apprenez à connecter une application PHP à MySQL en utilisant l\'architecture MVC pour une meilleure structure et maintenabilité.'
                }
            ]
        }
    },
    mounted() {
        // Appliquer la coloration syntaxique après le rendu
        this.applySyntaxHighlighting();
    },
    methods: {
        applySyntaxHighlighting() {
            // Cette fonction applique les classes de coloration syntaxique
            // Dans un vrai projet, vous pourriez utiliser une bibliothèque comme Prism.js
            // Pour cet exemple, nous utilisons les classes CSS que nous avons définies

            // Les classes sont déjà appliquées dans le HTML via les spans
            // Cette méthode est principalement pour la démonstration
            console.log('Coloration syntaxique appliquée');
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

/* COULEURS VS CODE POUR LA SYNTAXE PHP ET SQL */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (class, function, if, etc.) */
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

/* Styles spécifiques pour SQL */
.language-sql .keyword {
    color: #569cd6 !important;
}

/* Mots-clés SQL */
.language-sql .variable {
    color: #9cdcfe !important;
}

/* Noms de tables/colonnes */
.language-sql .string {
    color: #ce9178 !important;
}

/* Chaînes SQL */
.language-sql .number {
    color: #b5cea8 !important;
}

/* Nombres SQL */
.language-sql .function {
    color: #dcdcaa !important;
}

/* Fonctions SQL */

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