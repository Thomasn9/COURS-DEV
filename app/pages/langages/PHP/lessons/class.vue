<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Les Classes dans le Modèle MVC en PHP</h1>
                <p class="lesson-meta text-white">Architecture • POO • PHP • MVC</p>
                <p class="lesson-meta text-white">
                    <span>Niveau : Débutant / Intermédiaire</span>
                </p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction au Modèle MVC</h2>
                <p class="textExemple">
                    Le modèle MVC (Modèle-Vue-Contrôleur) est un pattern d'architecture logicielle qui sépare une
                    application en trois composants principaux :
                </p>
                <ul>
                    <li><strong>Modèle</strong> : Gère les données et la logique métier</li>
                    <li><strong>Vue</strong> : Présente les données à l'utilisateur</li>
                    <li><strong>Contrôleur</strong> : Traite les entrées utilisateur et coordonne Modèle et Vue</li>
                </ul>
                <p class="textExemple">
                    Dans cette leçon, nous allons nous concentrer sur les classes qui composent la partie
                    <strong>Modèle</strong> de l'architecture MVC.
                </p>
            </div>

            <!-- Qu'est-ce qu'une classe dans le Modèle MVC -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le Rôle des Classes dans le Modèle</h2>
                <p class="textExemple">
                    Dans le contexte MVC, les classes du modèle représentent les entités métier de votre application.
                    Elles sont responsables de :
                </p>
                <ul>
                    <li>La représentation des données</li>
                    <li>La validation des données</li>
                    <li>Les interactions avec la base de données</li>
                    <li>L'application des règles métier</li>
                </ul>

                <div class="code-example">
                    <h3 class="text-purple">Exemple de classe Modèle simple</h3>
                    <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">User</span> {
    <span class="comment">// Propriétés (attributs)</span>
    <span class="keyword">private</span> <span class="variable">$id</span>;
    <span class="keyword">private</span> <span class="variable">$username</span>;
    <span class="keyword">private</span> <span class="variable">$email</span>;
    <span class="keyword">private</span> <span class="variable">$password</span>;

    <span class="comment">// Constructeur</span>
    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$username</span>, <span class="variable">$email</span>, <span class="variable">$password</span>) {
        <span class="variable">$this</span>-&gt;username = <span class="variable">$username</span>;
        <span class="variable">$this</span>-&gt;email = <span class="variable">$email</span>;
        <span class="variable">$this</span>-&gt;password = <span class="function">password_hash</span>(<span class="variable">$password</span>, PASSWORD_DEFAULT);
    }

    <span class="comment">// Getters (accesseurs)</span>
    <span class="keyword">public function</span> <span class="function">getId</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;id;
    }

    <span class="keyword">public function</span> <span class="function">getUsername</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;username;
    }

    <span class="comment">// Setters (mutateurs)</span>
    <span class="keyword">public function</span> <span class="function">setUsername</span>(<span class="variable">$username</span>) {
        <span class="variable">$this</span>-&gt;username = <span class="variable">$username</span>;
    }

    <span class="comment">// Méthodes métier</span>
    <span class="keyword">public function</span> <span class="function">verifyPassword</span>(<span class="variable">$password</span>) {
        <span class="keyword">return</span> <span class="function">password_verify</span>(<span class="variable">$password</span>, <span class="variable">$this</span>-&gt;password);
    }
}
?&gt;</code></pre>
                </div>
            </div>

            <!-- Classes du Modèle et Base de Données -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Classes Modèle et Interaction avec la Base de Données</h2>
                <p class="textExemple">
                    Les classes du modèle interagissent généralement avec une base de données. Il existe plusieurs
                    approches pour cela :
                </p>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Approche Active Record</h3>
                        <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">User</span> <span class="keyword">extends</span> <span class="class-name">Model</span> {
    <span class="keyword">protected</span> <span class="variable">$table</span> = <span class="string">'users'</span>;

    <span class="keyword">public static function</span> <span class="function">find</span>(<span class="variable">$id</span>) {
        <span class="variable">$db</span> = <span class="class-name">Database</span>::<span class="function">getInstance</span>();
        <span class="variable">$stmt</span> = <span class="variable">$db</span>-&gt;<span class="function">prepare</span>(<span class="string">"SELECT * FROM users WHERE id = ?"</span>);
        <span class="variable">$stmt</span>-&gt;<span class="function">execute</span>([<span class="variable">$id</span>]);
        <span class="keyword">return</span> <span class="variable">$stmt</span>-&gt;<span class="function">fetchObject</span>(<span class="class-name">self</span>::<span class="keyword">class</span>);
    }

    <span class="keyword">public function</span> <span class="function">save</span>() {
        <span class="keyword">if</span>(<span class="variable">$this</span>-&gt;id) {
            <span class="comment">// Mise à jour</span>
            <span class="variable">$this</span>-&gt;<span class="function">update</span>();
        } <span class="keyword">else</span> {
            <span class="comment">// Insertion</span>
            <span class="variable">$this</span>-&gt;<span class="function">insert</span>();
        }
    }
}
?&gt;</code></pre>
                    </div>

                    <div>
                        <h3 class="text-purple">Approche Data Mapper</h3>
                        <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">UserMapper</span> {
    <span class="keyword">private</span> <span class="variable">$db</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="class-name">Database</span> <span class="variable">$db</span>) {
        <span class="variable">$this</span>-&gt;db = <span class="variable">$db</span>;
    }

    <span class="keyword">public function</span> <span class="function">findById</span>(<span class="variable">$id</span>) {
        <span class="variable">$stmt</span> = <span class="variable">$this</span>-&gt;db-&gt;<span class="function">prepare</span>(<span class="string">"SELECT * FROM users WHERE id = ?"</span>);
        <span class="variable">$stmt</span>-&gt;<span class="function">execute</span>([<span class="variable">$id</span>]);
        <span class="variable">$data</span> = <span class="variable">$stmt</span>-&gt;<span class="function">fetch</span>();

        <span class="keyword">if</span>(!<span class="variable">$data</span>) {
            <span class="keyword">return</span> <span class="keyword">null</span>;
        }

        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;<span class="function">mapToUser</span>(<span class="variable">$data</span>);
    }

    <span class="keyword">private function</span> <span class="function">mapToUser</span>(<span class="variable">$data</span>) {
        <span class="variable">$user</span> = <span class="keyword">new</span> <span class="class-name">User</span>();
        <span class="variable">$user</span>-&gt;<span class="function">setId</span>(<span class="variable">$data</span>[<span class="string">'id'</span>]);
        <span class="variable">$user</span>-&gt;<span class="function">setUsername</span>(<span class="variable">$data</span>[<span class="string">'username'</span>]);
        <span class="comment">// ... autres propriétés</span>
        <span class="keyword">return</span> <span class="variable">$user</span>;
    }
}
?&gt;</code></pre>
                    </div>
                </div>
            </div>

            <!-- Relations entre Classes Modèle -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Relations entre Classes Modèle</h2>
                <p class="textExemple">
                    Dans une application réelle, les classes du modèle ont souvent des relations entre elles. Voici
                    comment représenter ces relations :
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Relations One-to-Many</h3>
                    <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">User</span> {
    <span class="comment">// ... autres propriétés et méthodes</span>

    <span class="keyword">private</span> <span class="variable">$posts</span> = [];

    <span class="comment">// Relation One-to-Many: Un utilisateur a plusieurs articles</span>
    <span class="keyword">public function</span> <span class="function">getPosts</span>() {
        <span class="keyword">if</span>(<span class="function">empty</span>(<span class="variable">$this</span>-&gt;posts)) {
            <span class="variable">$postMapper</span> = <span class="keyword">new</span> <span class="class-name">PostMapper</span>();
            <span class="variable">$this</span>-&gt;posts = <span class="variable">$postMapper</span>-&gt;<span class="function">findByUserId</span>(<span class="variable">$this</span>-&gt;id);
        }
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;posts;
    }

    <span class="keyword">public function</span> <span class="function">addPost</span>(<span class="class-name">Post</span> <span class="variable">$post</span>) {
        <span class="variable">$post</span>-&gt;<span class="function">setUserId</span>(<span class="variable">$this</span>-&gt;id);
        <span class="variable">$this</span>-&gt;posts[] = <span class="variable">$post</span>;
    }
}

<span class="keyword">class</span> <span class="class-name">Post</span> {
    <span class="keyword">private</span> <span class="variable">$id</span>;
    <span class="keyword">private</span> <span class="variable">$title</span>;
    <span class="keyword">private</span> <span class="variable">$content</span>;
    <span class="keyword">private</span> <span class="variable">$userId</span>;

    <span class="comment">// Relation Many-to-One: Un article appartient à un utilisateur</span>
    <span class="keyword">public function</span> <span class="function">getUser</span>() {
        <span class="variable">$userMapper</span> = <span class="keyword">new</span> <span class="class-name">UserMapper</span>();
        <span class="keyword">return</span> <span class="variable">$userMapper</span>-&gt;<span class="function">findById</span>(<span class="variable">$this</span>-&gt;userId);
    }

    <span class="keyword">public function</span> <span class="function">setUserId</span>(<span class="variable">$userId</span>) {
        <span class="variable">$this</span>-&gt;userId = <span class="variable">$userId</span>;
    }
}
?&gt;</code></pre>
                </div>
            </div>

            <!-- Bonnes Pratiques -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques pour les Classes Modèle</h2>
                <ul>
                    <li><strong>SRP (Single Responsibility Principle)</strong> : Une classe modèle ne devrait avoir
                        qu'une seule raison de changer</li>
                    <li><strong>Encapsulation</strong> : Utilisez des propriétés privées/protégées et fournissez des
                        accesseurs/mutateurs</li>
                    <li><strong>Validation</strong> : Validez les données dans les setters et le constructeur</li>
                    <li><strong>Séparation des préoccupations</strong> : Ne mélangez pas la logique de présentation avec
                        la logique métier</li>
                    <li><strong>Injection de dépendances</strong> : Injectez les dépendances plutôt que de les créer
                        dans la classe</li>
                </ul>

                <div class="code-example">
                    <h3 class="text-purple">Exemple de classe Modèle bien structurée</h3>
                    <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">Product</span> {
    <span class="keyword">private</span> <span class="variable">$id</span>;
    <span class="keyword">private</span> <span class="variable">$name</span>;
    <span class="keyword">private</span> <span class="variable">$price</span>;
    <span class="keyword">private</span> <span class="variable">$category</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$name</span>, <span class="variable">$price</span>, <span class="class-name">Category</span> <span class="variable">$category</span>) {
        <span class="variable">$this</span>-&gt;<span class="function">setName</span>(<span class="variable">$name</span>);
        <span class="variable">$this</span>-&gt;<span class="function">setPrice</span>(<span class="variable">$price</span>);
        <span class="variable">$this</span>-&gt;<span class="function">setCategory</span>(<span class="variable">$category</span>);
    }

    <span class="keyword">public function</span> <span class="function">setName</span>(<span class="variable">$name</span>) {
        <span class="keyword">if</span>(<span class="function">empty</span>(<span class="variable">$name</span>) <span class="operator">||</span> <span class="function">strlen</span>(<span class="variable">$name</span>) &gt; <span class="number">255</span>) {
            <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"Le nom du produit est invalide"</span>);
        }
        <span class="variable">$this</span>-&gt;name = <span class="variable">$name</span>;
    }

    <span class="keyword">public function</span> <span class="function">setPrice</span>(<span class="variable">$price</span>) {
        <span class="keyword">if</span>(!<span class="function">is_numeric</span>(<span class="variable">$price</span>) <span class="operator">||</span> <span class="variable">$price</span> &lt; <span class="number">0</span>) {
            <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"Le prix doit être un nombre positif"</span>);
        }
        <span class="variable">$this</span>-&gt;price = <span class="function">floatval</span>(<span class="variable">$price</span>);
    }

    <span class="comment">// Méthodes métier</span>
    <span class="keyword">public function</span> <span class="function">applyDiscount</span>(<span class="variable">$percentage</span>) {
        <span class="keyword">if</span>(<span class="variable">$percentage</span> &lt; <span class="number">0</span> <span class="operator">||</span> <span class="variable">$percentage</span> &gt; <span class="number">100</span>) {
            <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"Le pourcentage de réduction doit être entre 0 et 100"</span>);
        }
        <span class="variable">$this</span>-&gt;price = <span class="variable">$this</span>-&gt;price * (<span class="number">1</span> - <span class="variable">$percentage</span> / <span class="number">100</span>);
    }

    <span class="keyword">public function</span> <span class="function">isExpensive</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;price &gt; <span class="number">100</span>;
    }
}
?&gt;</code></pre>
                </div>
            </div>

            <!-- Exercice Pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Créez une classe <code>Article</code> qui représente un article de blog avec les propriétés
                        suivantes :
                    </p>
                    <ul>
                        <li>id (entier)</li>
                        <li>titre (chaîne de caractères, maximum 255 caractères)</li>
                        <li>contenu (texte)</li>
                        <li>datePublication (DateTime)</li>
                        <li>auteur (instance de la classe User)</li>
                        <li>categories (tableau d'instances de la classe Category)</li>
                    </ul>
                    <p class="textExemple">
                        Implémentez les méthodes suivantes :
                    </p>
                    <ul>
                        <li>Un constructeur qui prend le titre, le contenu et l'auteur</li>
                        <li>Des getters et setters avec validation</li>
                        <li>Une méthode <code>publier()</code> qui définit la date de publication à maintenant</li>
                        <li>Une méthode <code>estPublic()</code> qui retourne true si l'article est publié</li>
                        <li>Des méthodes pour gérer les catégories (<code>ajouterCategorie()</code>,
                            <code>supprimerCategorie()</code>)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">Article</span> {
    <span class="keyword">private</span> <span class="variable">$id</span>;
    <span class="keyword">private</span> <span class="variable">$titre</span>;
    <span class="keyword">private</span> <span class="variable">$contenu</span>;
    <span class="keyword">private</span> <span class="variable">$datePublication</span>;
    <span class="keyword">private</span> <span class="variable">$auteur</span>;
    <span class="keyword">private</span> <span class="variable">$categories</span> = [];

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$titre</span>, <span class="variable">$contenu</span>, <span class="class-name">User</span> <span class="variable">$auteur</span>) {
        <span class="variable">$this</span>-&gt;<span class="function">setTitre</span>(<span class="variable">$titre</span>);
        <span class="variable">$this</span>-&gt;<span class="function">setContenu</span>(<span class="variable">$contenu</span>);
        <span class="variable">$this</span>-&gt;<span class="function">setAuteur</span>(<span class="variable">$auteur</span>);
    }

    <span class="keyword">public function</span> <span class="function">setTitre</span>(<span class="variable">$titre</span>) {
        <span class="keyword">if</span>(<span class="function">empty</span>(<span class="variable">$titre</span>) <span class="operator">||</span> <span class="function">strlen</span>(<span class="variable">$titre</span>) &gt; <span class="number">255</span>) {
            <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"Le titre est invalide"</span>);
        }
        <span class="variable">$this</span>-&gt;titre = <span class="variable">$titre</span>;
    }

    <span class="keyword">public function</span> <span class="function">setContenu</span>(<span class="variable">$contenu</span>) {
        <span class="keyword">if</span>(<span class="function">empty</span>(<span class="variable">$contenu</span>)) {
            <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(<span class="string">"Le contenu ne peut pas être vide"</span>);
        }
        <span class="variable">$this</span>-&gt;contenu = <span class="variable">$contenu</span>;
    }

    <span class="keyword">public function</span> <span class="function">publier</span>() {
        <span class="variable">$this</span>-&gt;datePublication = <span class="keyword">new</span> <span class="class-name">DateTime</span>();
    }

    <span class="keyword">public function</span> <span class="function">estPublic</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;datePublication <span class="operator">!==</span> <span class="keyword">null</span>;
    }

    <span class="keyword">public function</span> <span class="function">ajouterCategorie</span>(<span class="class-name">Category</span> <span class="variable">$categorie</span>) {
        <span class="variable">$this</span>-&gt;categories[] = <span class="variable">$categorie</span>;
    }

    <span class="keyword">public function</span> <span class="function">supprimerCategorie</span>(<span class="class-name">Category</span> <span class="variable">$categorie</span>) {
        <span class="variable">$key</span> = <span class="function">array_search</span>(<span class="variable">$categorie</span>, <span class="variable">$this</span>-&gt;categories, <span class="keyword">true</span>);
        <span class="keyword">if</span>(<span class="variable">$key</span> <span class="operator">!==</span> <span class="keyword">false</span>) {
            <span class="function">array_splice</span>(<span class="variable">$this</span>-&gt;categories, <span class="variable">$key</span>, <span class="number">1</span>);
        }
    }

    <span class="comment">// Getters</span>
    <span class="keyword">public function</span> <span class="function">getId</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;id; }
    <span class="keyword">public function</span> <span class="function">getTitre</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;titre; }
    <span class="keyword">public function</span> <span class="function">getContenu</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;contenu; }
    <span class="keyword">public function</span> <span class="function">getDatePublication</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;datePublication; }
    <span class="keyword">public function</span> <span class="function">getAuteur</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;auteur; }
    <span class="keyword">public function</span> <span class="function">getCategories</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;categories; }
}
?&gt;</code></pre>
                        </div>
                    </details>
                </div>
            </div>

            <!-- Conclusion -->
            <div class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Conclusion</h2>
                <p class="text-white">
                    Les classes dans le modèle MVC sont essentielles pour structurer votre application PHP de manière
                    maintenable et évolutive.
                    En respectant les principes de la POO et en séparant clairement les responsabilités, vous créerez
                    des applications robustes
                    et faciles à maintenir.
                </p>
                <p class="text-white">
                    N'oubliez pas que le modèle ne doit contenir que la logique métier et les données, tandis que la
                    logique de présentation
                    et la gestion des requêtes HTTP doivent être déléguées respectivement à la Vue et au Contrôleur.
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MVCModelClassesLesson',
    data() {
        return {
            lessonTitle: 'Les Classes dans le Modèle MVC en PHP'
        }
    },
    head() {
        return {
            title: this.lessonTitle,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Apprenez à créer et utiliser les classes dans le modèle MVC en PHP. Comprenez leur rôle, leurs relations et les bonnes pratiques.'
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