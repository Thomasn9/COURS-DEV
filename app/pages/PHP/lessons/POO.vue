<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Programmation Orientée Objet en PHP</h1>
                <p class="lesson-meta text-white">POO • Classes • Objets • Héritage • PHP</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à la POO</h2>
                <p class="textExemple">
                    La Programmation Orientée Objet (POO) est un paradigme de programmation qui organise le code autour
                    des concepts d'<strong>objets</strong> et de <strong>classes</strong>.
                    Contrairement à la programmation procédurale, la POO permet de modéliser des entités du monde réel
                    avec leurs propriétés et comportements.
                </p>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Programmation Procédurale</h3>
                        <pre><code class="language-php">&lt;?php
<span class="comment">// Données séparées des fonctions</span>
<span class="variable">$userName</span> = <span class="string">"John"</span>;
<span class="variable">$userEmail</span> = <span class="string">"john@example.com"</span>;

<span class="keyword">function</span> <span class="function">displayUser</span>(<span class="variable">$name</span>, <span class="variable">$email</span>) {
    <span class="keyword">echo</span> <span class="string">"Nom: "</span> . <span class="variable">$name</span> . <span class="string">", Email: "</span> . <span class="variable">$email</span>;
}

<span class="function">displayUser</span>(<span class="variable">$userName</span>, <span class="variable">$userEmail</span>);
?&gt;</code></pre>
                    </div>

                    <div>
                        <h3 class="text-purple">Programmation Orientée Objet</h3>
                        <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">User</span> {
    <span class="keyword">private</span> <span class="variable">$name</span>;
    <span class="keyword">private</span> <span class="variable">$email</span>;

    <span class="keyword">public function</span> <span class="function">display</span>() {
        <span class="keyword">echo</span> <span class="string">"Nom: "</span> . <span class="variable">$this</span>-&gt;name . <span class="string">", Email: "</span> . <span class="variable">$this</span>-&gt;email;
    }
}

<span class="variable">$user</span> = <span class="keyword">new</span> <span class="class-name">User</span>(<span class="string">"John"</span>, <span class="string">"john@example.com"</span>);
<span class="variable">$user</span>-&gt;<span class="function">display</span>();
?&gt;</code></pre>
                    </div>
                </div>
            </div>

            <!-- Concepts Fondamentaux -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts Fondamentaux de la POO</h2>

                <div class="code-example">
                    <h3 class="text-purple">1. Classes et Objets</h3>
                    <p class="textExemple">
                        Une <strong>classe</strong> est un plan de construction, un <strong>objet</strong> est une
                        instance de cette classe.
                    </p>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Définition d'une classe</span>
<span class="keyword">class</span> <span class="class-name">Voiture</span> {
    <span class="comment">// Propriétés (attributs)</span>
    <span class="keyword">public</span> <span class="variable">$marque</span>;
    <span class="keyword">public</span> <span class="variable">$couleur</span>;
    <span class="keyword">private</span> <span class="variable">$vitesse</span> = <span class="number">0</span>;

    <span class="comment">// Constructeur</span>
    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$marque</span>, <span class="variable">$couleur</span>) {
        <span class="variable">$this</span>-&gt;marque = <span class="variable">$marque</span>;
        <span class="variable">$this</span>-&gt;couleur = <span class="variable">$couleur</span>;
    }

    <span class="comment">// Méthodes</span>
    <span class="keyword">public function</span> <span class="function">accelerer</span>(<span class="variable">$increment</span>) {
        <span class="variable">$this</span>-&gt;vitesse += <span class="variable">$increment</span>;
    }

    <span class="keyword">public function</span> <span class="function">getVitesse</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;vitesse;
    }
}

<span class="comment">// Création d'objets</span>
<span class="variable">$maVoiture</span> = <span class="keyword">new</span> <span class="class-name">Voiture</span>(<span class="string">"Renault"</span>, <span class="string">"rouge"</span>);
<span class="variable">$taVoiture</span> = <span class="keyword">new</span> <span class="class-name">Voiture</span>(<span class="string">"Peugeot"</span>, <span class="string">"bleue"</span>);

<span class="variable">$maVoiture</span>-&gt;<span class="function">accelerer</span>(<span class="number">50</span>);
<span class="keyword">echo</span> <span class="variable">$maVoiture</span>-&gt;<span class="function">getVitesse</span>(); <span class="comment">// Affiche 50</span>
?&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">2. Encapsulation et Modificateurs d'Accès</h3>
                    <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">CompteBancaire</span> {
    <span class="comment">// public: accessible de partout</span>
    <span class="keyword">public</span> <span class="variable">$titulaire</span>;
    
    <span class="comment">// private: accessible seulement dans la classe</span>
    <span class="keyword">private</span> <span class="variable">$solde</span>;
    
    <span class="comment">// protected: accessible dans la classe et ses enfants</span>
    <span class="keyword">protected</span> <span class="variable">$numeroCompte</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$titulaire</span>, <span class="variable">$soldeInitial</span>) {
        <span class="variable">$this</span>-&gt;titulaire = <span class="variable">$titulaire</span>;
        <span class="variable">$this</span>-&gt;solde = <span class="variable">$soldeInitial</span>;
    }

    <span class="comment">// Getters (accesseurs)</span>
    <span class="keyword">public function</span> <span class="function">getSolde</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;solde;
    }

    <span class="comment">// Setters (mutateurs) avec validation</span>
    <span class="keyword">public function</span> <span class="function">deposer</span>(<span class="variable">$montant</span>) {
        <span class="keyword">if</span>(<span class="variable">$montant</span> &gt; <span class="number">0</span>) {
            <span class="variable">$this</span>-&gt;solde += <span class="variable">$montant</span>;
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }

    <span class="keyword">public function</span> <span class="function">retirer</span>(<span class="variable">$montant</span>) {
        <span class="keyword">if</span>(<span class="variable">$montant</span> &gt; <span class="number">0</span> <span class="operator">&amp;&amp;</span> <span class="variable">$montant</span> &lt;= <span class="variable">$this</span>-&gt;solde) {
            <span class="variable">$this</span>-&gt;solde -= <span class="variable">$montant</span>;
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }
}

<span class="variable">$compte</span> = <span class="keyword">new</span> <span class="class-name">CompteBancaire</span>(<span class="string">"Alice"</span>, <span class="number">1000</span>);
<span class="variable">$compte</span>-&gt;<span class="function">deposer</span>(<span class="number">500</span>);
<span class="variable">$compte</span>-&gt;<span class="function">retirer</span>(<span class="number">200</span>);
<span class="keyword">echo</span> <span class="variable">$compte</span>-&gt;<span class="function">getSolde</span>(); <span class="comment">// Affiche 1300</span>

<span class="comment">// Erreur: propriété privée inaccessible</span>
<span class="comment">// echo $compte-&gt;solde;</span>
?&gt;</code></pre>
                </div>
            </div>

            <!-- Héritage et Polymorphisme -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Héritage et Polymorphisme</h2>

                <div class="code-example">
                    <h3 class="text-purple">3. Héritage</h3>
                    <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">Animal</span> {
    <span class="keyword">protected</span> <span class="variable">$nom</span>;
    <span class="keyword">protected</span> <span class="variable">$age</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$nom</span>, <span class="variable">$age</span>) {
        <span class="variable">$this</span>-&gt;nom = <span class="variable">$nom</span>;
        <span class="variable">$this</span>-&gt;age = <span class="variable">$age</span>;
    }

    <span class="keyword">public function</span> <span class="function">manger</span>() {
        <span class="keyword">echo</span> <span class="variable">$this</span>-&gt;nom . <span class="string">" mange."</span>;
    }

    <span class="keyword">public function</span> <span class="function">dormir</span>() {
        <span class="keyword">echo</span> <span class="variable">$this</span>-&gt;nom . <span class="string">" dort."</span>;
    }
}

<span class="keyword">class</span> <span class="class-name">Chien</span> <span class="keyword">extends</span> <span class="class-name">Animal</span> {
    <span class="keyword">private</span> <span class="variable">$race</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$nom</span>, <span class="variable">$age</span>, <span class="variable">$race</span>) {
        <span class="keyword">parent</span>::<span class="function">__construct</span>(<span class="variable">$nom</span>, <span class="variable">$age</span>);
        <span class="variable">$this</span>-&gt;race = <span class="variable">$race</span>;
    }

    <span class="comment">// Surcharge de méthode (override)</span>
    <span class="keyword">public function</span> <span class="function">manger</span>() {
        <span class="keyword">echo</span> <span class="variable">$this</span>-&gt;nom . <span class="string">" mange des croquettes."</span>;
    }

    <span class="comment">// Méthode spécifique à la classe Chien</span>
    <span class="keyword">public function</span> <span class="function">aboyer</span>() {
        <span class="keyword">echo</span> <span class="string">"Woof! Woof!"</span>;
    }
}

<span class="keyword">class</span> <span class="class-name">Chat</span> <span class="keyword">extends</span> <span class="class-name">Animal</span> {
    <span class="keyword">public function</span> <span class="function">manger</span>() {
        <span class="keyword">echo</span> <span class="variable">$this</span>-&gt;nom . <span class="string">" mange du poisson."</span>;
    }

    <span class="keyword">public function</span> <span class="function">ronronner</span>() {
        <span class="keyword">echo</span> <span class="string">"Ronron..."</span>;
    }
}

<span class="variable">$rex</span> = <span class="keyword">new</span> <span class="class-name">Chien</span>(<span class="string">"Rex"</span>, <span class="number">3</span>, <span class="string">"Berger Allemand"</span>);
<span class="variable">$felix</span> = <span class="keyword">new</span> <span class="class-name">Chat</span>(<span class="string">"Félix"</span>, <span class="number">2</span>);

<span class="variable">$rex</span>-&gt;<span class="function">manger</span>();    <span class="comment">// "Rex mange des croquettes."</span>
<span class="variable">$felix</span>-&gt;<span class="function">manger</span>();  <span class="comment">// "Félix mange du poisson."</span>
<span class="variable">$rex</span>-&gt;<span class="function">aboyer</span>();    <span class="comment">// "Woof! Woof!"</span>
?&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">4. Polymorphisme</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Le polymorphisme permet de traiter différents objets de manière uniforme</span>
<span class="keyword">function</span> <span class="function">nourrirAnimal</span>(<span class="class-name">Animal</span> <span class="variable">$animal</span>) {
    <span class="variable">$animal</span>-&gt;<span class="function">manger</span>();
}

<span class="variable">$animaux</span> = [
    <span class="keyword">new</span> <span class="class-name">Chien</span>(<span class="string">"Medor"</span>, <span class="number">4</span>, <span class="string">"Labrador"</span>),
    <span class="keyword">new</span> <span class="class-name">Chat</span>(<span class="string">"Minou"</span>, <span class="number">2</span>),
    <span class="keyword">new</span> <span class="class-name">Chien</span>(<span class="string">"Lassie"</span>, <span class="number">5</span>, <span class="string">"Colley"</span>)
];

<span class="keyword">foreach</span>(<span class="variable">$animaux</span> <span class="keyword">as</span> <span class="variable">$animal</span>) {
    <span class="function">nourrirAnimal</span>(<span class="variable">$animal</span>); <span class="comment">// Appelle la méthode manger() appropriée</span>
    <span class="keyword">echo</span> <span class="string">"&lt;br&gt;"</span>;
}
?&gt;</code></pre>
                </div>
            </div>

            <!-- Classes Abstraites et Interfaces -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Classes Abstraites et Interfaces</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Classes Abstraites</h3>
                        <pre><code class="language-php">&lt;?php
<span class="keyword">abstract class</span> <span class="class-name">Forme</span> {
    <span class="keyword">protected</span> <span class="variable">$couleur</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$couleur</span>) {
        <span class="variable">$this</span>-&gt;couleur = <span class="variable">$couleur</span>;
    }

    <span class="comment">// Méthode concrète (implémentée)</span>
    <span class="keyword">public function</span> <span class="function">getCouleur</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;couleur;
    }

    <span class="comment">// Méthodes abstraites (doivent être implémentées par les enfants)</span>
    <span class="keyword">abstract public function</span> <span class="function">calculerAire</span>();
    <span class="keyword">abstract public function</span> <span class="function">calculerPerimetre</span>();
}

<span class="keyword">class</span> <span class="class-name">Cercle</span> <span class="keyword">extends</span> <span class="class-name">Forme</span> {
    <span class="keyword">private</span> <span class="variable">$rayon</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$rayon</span>, <span class="variable">$couleur</span>) {
        <span class="keyword">parent</span>::<span class="function">__construct</span>(<span class="variable">$couleur</span>);
        <span class="variable">$this</span>-&gt;rayon = <span class="variable">$rayon</span>;
    }

    <span class="keyword">public function</span> <span class="function">calculerAire</span>() {
        <span class="keyword">return</span> pi() * <span class="function">pow</span>(<span class="variable">$this</span>-&gt;rayon, <span class="number">2</span>);
    }

    <span class="keyword">public function</span> <span class="function">calculerPerimetre</span>() {
        <span class="keyword">return</span> <span class="number">2</span> * pi() * <span class="variable">$this</span>-&gt;rayon;
    }
}

<span class="comment">// Impossible d'instancier une classe abstraite</span>
<span class="comment">// $forme = new Forme("rouge"); // Erreur!</span>

<span class="variable">$cercle</span> = <span class="keyword">new</span> <span class="class-name">Cercle</span>(<span class="number">5</span>, <span class="string">"bleu"</span>);
<span class="keyword">echo</span> <span class="string">"Aire: "</span> . <span class="variable">$cercle</span>-&gt;<span class="function">calculerAire</span>(); <span class="comment">// Aire: 78.539816339745</span>
?&gt;</code></pre>
                    </div>

                    <div>
                        <h3 class="text-purple">Interfaces</h3>
                        <pre><code class="language-php">&lt;?php
<span class="keyword">interface</span> <span class="class-name">Volant</span> {
    <span class="keyword">public function</span> <span class="function">decoller</span>();
    <span class="keyword">public function</span> <span class="function">atterrir</span>();
}

<span class="keyword">interface</span> <span class="class-name">Transport</span> {
    <span class="keyword">public function</span> <span class="function">charger</span>(<span class="variable">$passagers</span>);
    <span class="keyword">public function</span> <span class="function">decharger</span>();
}

<span class="keyword">class</span> <span class="class-name">Avion</span> <span class="keyword">implements</span> <span class="class-name">Volant</span>, <span class="class-name">Transport</span> {
    <span class="keyword">private</span> <span class="variable">$passagers</span> = [];

    <span class="keyword">public function</span> <span class="function">decoller</span>() {
        <span class="keyword">echo</span> <span class="string">"L'avion décolle!"</span>;
    }

    <span class="keyword">public function</span> <span class="function">atterrir</span>() {
        <span class="keyword">echo</span> <span class="string">"L'avion atterrit!"</span>;
    }

    <span class="keyword">public function</span> <span class="function">charger</span>(<span class="variable">$passagers</span>) {
        <span class="variable">$this</span>-&gt;passagers = <span class="variable">$passagers</span>;
        <span class="keyword">echo</span> <span class="string">"Passagers chargés: "</span> . <span class="function">count</span>(<span class="variable">$passagers</span>);
    }

    <span class="keyword">public function</span> <span class="function">decharger</span>() {
        <span class="variable">$this</span>-&gt;passagers = [];
        <span class="keyword">echo</span> <span class="string">"Passagers déchargés"</span>;
    }
}

<span class="keyword">class</span> <span class="class-name">Oiseau</span> <span class="keyword">implements</span> <span class="class-name">Volant</span> {
    <span class="keyword">public function</span> <span class="function">decoller</span>() {
        <span class="keyword">echo</span> <span class="string">"L'oiseau s'envole!"</span>;
    }

    <span class="keyword">public function</span> <span class="function">atterrir</span>() {
        <span class="keyword">echo</span> <span class="string">"L'oiseau se pose!"</span>;
    }
}

<span class="variable">$avion</span> = <span class="keyword">new</span> <span class="class-name">Avion</span>();
<span class="variable">$oiseau</span> = <span class="keyword">new</span> <span class="class-name">Oiseau</span>();

<span class="function">faireVoler</span>(<span class="variable">$avion</span>);   <span class="comment">// "L'avion décolle!"</span>
<span class="function">faireVoler</span>(<span class="variable">$oiseau</span>);  <span class="comment">// "L'oiseau s'envole!"</span>

<span class="keyword">function</span> <span class="function">faireVoler</span>(<span class="class-name">Volant</span> <span class="variable">$volant</span>) {
    <span class="variable">$volant</span>-&gt;<span class="function">decoller</span>();
}
?&gt;</code></pre>
                    </div>
                </div>
            </div>

            <!-- Méthodes et Propriétés Statiques -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes et Propriétés Statiques</h2>

                <div class="code-example">
                    <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">MathUtils</span> {
    <span class="comment">// Propriété statique (partagée par toutes les instances)</span>
    <span class="keyword">public static</span> <span class="variable">$PI</span> = <span class="number">3.14159</span>;
    <span class="keyword">private static</span> <span class="variable">$compteur</span> = <span class="number">0</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>() {
        <span class="keyword">self</span>::<span class="variable">$compteur</span>++;
    }

    <span class="comment">// Méthode statique (appelée sans instanciation)</span>
    <span class="keyword">public static function</span> <span class="function">additionner</span>(<span class="variable">$a</span>, <span class="variable">$b</span>) {
        <span class="keyword">return</span> <span class="variable">$a</span> + <span class="variable">$b</span>;
    }

    <span class="keyword">public static function</span> <span class="function">calculerCirconference</span>(<span class="variable">$rayon</span>) {
        <span class="keyword">return</span> <span class="number">2</span> * <span class="keyword">self</span>::<span class="variable">$PI</span> * <span class="variable">$rayon</span>;
    }

    <span class="keyword">public static function</span> <span class="function">getCompteur</span>() {
        <span class="keyword">return</span> <span class="keyword">self</span>::<span class="variable">$compteur</span>;
    }
}

<span class="comment">// Utilisation sans instanciation</span>
<span class="keyword">echo</span> <span class="class-name">MathUtils</span>::<span class="function">additionner</span>(<span class="number">5</span>, <span class="number">3</span>); <span class="comment">// 8</span>
<span class="keyword">echo</span> <span class="class-name">MathUtils</span>::<span class="function">calculerCirconference</span>(<span class="number">10</span>); <span class="comment">// 62.8318</span>
<span class="keyword">echo</span> <span class="class-name">MathUtils</span>::<span class="variable">$PI</span>; <span class="comment">// 3.14159</span>

<span class="comment">// Modification de la propriété statique</span>
<span class="class-name">MathUtils</span>::<span class="variable">$PI</span> = <span class="number">3.14</span>;

<span class="variable">$math1</span> = <span class="keyword">new</span> <span class="class-name">MathUtils</span>();
<span class="variable">$math2</span> = <span class="keyword">new</span> <span class="class-name">MathUtils</span>();
<span class="keyword">echo</span> <span class="class-name">MathUtils</span>::<span class="function">getCompteur</span>(); <span class="comment">// 2</span>
?&gt;</code></pre>
                </div>
            </div>

            <!-- Exercice Pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Créez un système de gestion de bibliothèque avec les classes suivantes :
                    </p>
                    <ul>
                        <li><strong>Livre</strong> : avec titre, auteur, année de publication, et statut
                            (disponible/emprunté)</li>
                        <li><strong>Membre</strong> : avec nom, email, et liste des livres empruntés</li>
                        <li><strong>Bibliotheque</strong> : qui gère les livres et les membres</li>
                    </ul>
                    <p class="textExemple">
                        Implémentez les fonctionnalités suivantes :
                    </p>
                    <ul>
                        <li>Ajouter/supprimer des livres et des membres</li>
                        <li>Emprunter et retourner des livres</li>
                        <li>Rechercher des livres par titre ou auteur</li>
                        <li>Afficher les livres empruntés par un membre</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution Complète</h4>
                            <pre><code class="language-php">&lt;?php
<span class="keyword">class</span> <span class="class-name">Livre</span> {
    <span class="keyword">private</span> <span class="variable">$titre</span>;
    <span class="keyword">private</span> <span class="variable">$auteur</span>;
    <span class="keyword">private</span> <span class="variable">$annee</span>;
    <span class="keyword">private</span> <span class="variable">$disponible</span>;

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$titre</span>, <span class="variable">$auteur</span>, <span class="variable">$annee</span>) {
        <span class="variable">$this</span>-&gt;titre = <span class="variable">$titre</span>;
        <span class="variable">$this</span>-&gt;auteur = <span class="variable">$auteur</span>;
        <span class="variable">$this</span>-&gt;annee = <span class="variable">$annee</span>;
        <span class="variable">$this</span>-&gt;disponible = <span class="keyword">true</span>;
    }

    <span class="keyword">public function</span> <span class="function">emprunter</span>() {
        <span class="keyword">if</span>(<span class="variable">$this</span>-&gt;disponible) {
            <span class="variable">$this</span>-&gt;disponible = <span class="keyword">false</span>;
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }

    <span class="keyword">public function</span> <span class="function">retourner</span>() {
        <span class="variable">$this</span>-&gt;disponible = <span class="keyword">true</span>;
    }

    <span class="comment">// Getters</span>
    <span class="keyword">public function</span> <span class="function">getTitre</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;titre; }
    <span class="keyword">public function</span> <span class="function">getAuteur</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;auteur; }
    <span class="keyword">public function</span> <span class="function">getAnnee</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;annee; }
    <span class="keyword">public function</span> <span class="function">estDisponible</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;disponible; }
}

<span class="keyword">class</span> <span class="class-name">Membre</span> {
    <span class="keyword">private</span> <span class="variable">$nom</span>;
    <span class="keyword">private</span> <span class="variable">$email</span>;
    <span class="keyword">private</span> <span class="variable">$livresEmpruntes</span> = [];

    <span class="keyword">public function</span> <span class="function">__construct</span>(<span class="variable">$nom</span>, <span class="variable">$email</span>) {
        <span class="variable">$this</span>-&gt;nom = <span class="variable">$nom</span>;
        <span class="variable">$this</span>-&gt;email = <span class="variable">$email</span>;
    }

    <span class="keyword">public function</span> <span class="function">emprunterLivre</span>(<span class="class-name">Livre</span> <span class="variable">$livre</span>) {
        <span class="keyword">if</span>(<span class="variable">$livre</span>-&gt;<span class="function">estDisponible</span>()) {
            <span class="variable">$livre</span>-&gt;<span class="function">emprunter</span>();
            <span class="variable">$this</span>-&gt;livresEmpruntes[] = <span class="variable">$livre</span>;
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }

    <span class="keyword">public function</span> <span class="function">retournerLivre</span>(<span class="class-name">Livre</span> <span class="variable">$livre</span>) {
        <span class="variable">$key</span> = <span class="function">array_search</span>(<span class="variable">$livre</span>, <span class="variable">$this</span>-&gt;livresEmpruntes, <span class="keyword">true</span>);
        <span class="keyword">if</span>(<span class="variable">$key</span> <span class="operator">!==</span> <span class="keyword">false</span>) {
            <span class="variable">$livre</span>-&gt;<span class="function">retourner</span>();
            <span class="function">array_splice</span>(<span class="variable">$this</span>-&gt;livresEmpruntes, <span class="variable">$key</span>, <span class="number">1</span>);
            <span class="keyword">return</span> <span class="keyword">true</span>;
        }
        <span class="keyword">return</span> <span class="keyword">false</span>;
    }

    <span class="keyword">public function</span> <span class="function">getLivresEmpruntes</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>-&gt;livresEmpruntes;
    }

    <span class="comment">// Getters</span>
    <span class="keyword">public function</span> <span class="function">getNom</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;nom; }
    <span class="keyword">public function</span> <span class="function">getEmail</span>() { <span class="keyword">return</span> <span class="variable">$this</span>-&gt;email; }
}

<span class="keyword">class</span> <span class="class-name">Bibliotheque</span> {
    <span class="keyword">private</span> <span class="variable">$livres</span> = [];
    <span class="keyword">private</span> <span class="variable">$membres</span> = [];

    <span class="keyword">public function</span> <span class="function">ajouterLivre</span>(<span class="class-name">Livre</span> <span class="variable">$livre</span>) {
        <span class="variable">$this</span>-&gt;livres[] = <span class="variable">$livre</span>;
    }

    <span class="keyword">public function</span> <span class="function">ajouterMembre</span>(<span class="class-name">Membre</span> <span class="variable">$membre</span>) {
        <span class="variable">$this</span>-&gt;membres[] = <span class="variable">$membre</span>;
    }

    <span class="keyword">public function</span> <span class="function">rechercherLivres</span>(<span class="variable">$terme</span>) {
        <span class="variable">$resultats</span> = [];
        <span class="keyword">foreach</span>(<span class="variable">$this</span>-&gt;livres <span class="keyword">as</span> <span class="variable">$livre</span>) {
            <span class="keyword">if</span>(<span class="function">stripos</span>(<span class="variable">$livre</span>-&gt;<span class="function">getTitre</span>(), <span class="variable">$terme</span>) <span class="operator">!==</span> <span class="keyword">false</span> <span class="operator">||</span> 
               <span class="function">stripos</span>(<span class="variable">$livre</span>-&gt;<span class="function">getAuteur</span>(), <span class="variable">$terme</span>) <span class="operator">!==</span> <span class="keyword">false</span>) {
                <span class="variable">$resultats</span>[] = <span class="variable">$livre</span>;
            }
        }
        <span class="keyword">return</span> <span class="variable">$resultats</span>;
    }

    <span class="keyword">public function</span> <span class="function">getLivresDisponibles</span>() {
        <span class="keyword">return</span> <span class="function">array_filter</span>(<span class="variable">$this</span>-&gt;livres, <span class="keyword">function</span>(<span class="variable">$livre</span>) {
            <span class="keyword">return</span> <span class="variable">$livre</span>-&gt;<span class="function">estDisponible</span>();
        });
    }
}

<span class="comment">// Utilisation du système</span>
<span class="variable">$bibliotheque</span> = <span class="keyword">new</span> <span class="class-name">Bibliotheque</span>();

<span class="comment">// Ajout de livres</span>
<span class="variable">$bibliotheque</span>-&gt;<span class="function">ajouterLivre</span>(<span class="keyword">new</span> <span class="class-name">Livre</span>(<span class="string">"Harry Potter"</span>, <span class="string">"J.K. Rowling"</span>, <span class="number">1997</span>));
<span class="variable">$bibliotheque</span>-&gt;<span class="function">ajouterLivre</span>(<span class="keyword">new</span> <span class="class-name">Livre</span>(<span class="string">"Le Seigneur des Anneaux"</span>, <span class="string">"J.R.R. Tolkien"</span>, <span class="number">1954</span>));

<span class="comment">// Ajout de membres</span>
<span class="variable">$alice</span> = <span class="keyword">new</span> <span class="class-name">Membre</span>(<span class="string">"Alice"</span>, <span class="string">"alice@email.com"</span>);
<span class="variable">$bibliotheque</span>-&gt;<span class="function">ajouterMembre</span>(<span class="variable">$alice</span>);

<span class="comment">// Emprunt d'un livre</span>
<span class="variable">$livres</span> = <span class="variable">$bibliotheque</span>-&gt;<span class="function">rechercherLivres</span>(<span class="string">"Harry Potter"</span>);
<span class="keyword">if</span>(!<span class="function">empty</span>(<span class="variable">$livres</span>)) {
    <span class="variable">$alice</span>-&gt;<span class="function">emprunterLivre</span>(<span class="variable">$livres</span>[<span class="number">0</span>]);
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
                    La Programmation Orientée Objet en PHP offre une manière puissante et organisée de structurer vos
                    applications.
                    En maîtrisant les concepts de classes, objets, héritage, encapsulation et polymorphisme, vous pouvez
                    créer des
                    systèmes complexes maintenables et extensibles.
                </p>
                <p class="text-white">
                    La POO favorise la réutilisation du code, la modularité et facilite la maintenance à long terme de
                    vos projets PHP.
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'POOPHPLesson',
    data() {
        return {
            lessonTitle: 'Programmation Orientée Objet en PHP'
        }
    },
    head() {
        return {
            title: this.lessonTitle,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Apprenez la Programmation Orientée Objet en PHP : classes, objets, héritage, encapsulation, polymorphisme, interfaces et bonnes pratiques.'
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