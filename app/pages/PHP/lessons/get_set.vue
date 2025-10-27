<template>
  <div class="lesson-container">
    <div class="lesson-content">
      
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Getters et Setters en POO PHP</h1>
        <p class="lesson-meta text-white">Encapsulation et Contrôle d'Accès - Programmation Orientée Objet</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p>Les getters et setters sont des méthodes spéciales qui permettent de contrôler l'accès aux attributs d'une classe. Ils sont au cœur du principe d'encapsulation en programmation orientée objet.</p>
        <p>Dans cette leçon, nous allons découvrir pourquoi et comment utiliser les getters et setters pour protéger l'intégrité de nos objets.</p>
      </section>

      <!-- Pourquoi utiliser les getters/setters -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi utiliser les getters et setters ?</h2>
        <p>L'encapsulation est un principe fondamental de la POO qui consiste à cacher l'état interne d'un objet et à n'autoriser son accès que via des méthodes contrôlées.</p>
        
        <div class="code-comparison">
          <div class="code-block">
            <h3 class="text-purple">❌ Sans encapsulation</h3>
            <pre><code>&lt;?php
class <span class="class-name">Personne</span> {
    <span class="keyword">public</span> <span class="variable">$age</span>;
}

<span class="variable">$personne</span> = <span class="keyword">new</span> <span class="class-name">Personne</span>();
<span class="variable">$personne</span>->age = -<span class="number">5</span>; <span class="comment">// Âge invalide ! Aucun contrôle</span></code></pre>
          </div>
          
          <div class="code-block">
            <h3 class="text-purple">✅ Avec encapsulation</h3>
            <pre><code>&lt;?php
class <span class="class-name">Personne</span> {
    <span class="keyword">private</span> <span class="variable">$age</span>;
    
    <span class="keyword">public</span> <span class="function">setAge</span>(<span class="variable">$age</span>) {
        <span class="keyword">if</span> (<span class="variable">$age</span> >= <span class="number">0</span> <span class="operator">&amp;&amp;</span> <span class="variable">$age</span> <= <span class="number">150</span>) {
            <span class="variable">$this</span>->age = <span class="variable">$age</span>;
        }
    }
}</code></pre>
          </div>
        </div>
        
        <div class="textExemple">
          <h3 class="text-purple">Avantages des getters/setters :</h3>
          <ul>
            <li><strong>Contrôle de validation</strong> : Vérifier la validité des données</li>
            <li><strong>Sécurité</strong> : Protéger les données sensibles</li>
            <li><strong>Flexibilité</strong> : Modifier l'implémentation interne sans affecter le code externe</li>
            <li><strong>Journalisation</strong> : Tracker les accès aux données</li>
          </ul>
        </div>
      </section>

      <!-- Les Getters -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les Getters (Accesseurs)</h2>
        <p>Les getters sont des méthodes qui permettent de <strong>lire</strong> la valeur d'un attribut privé ou protégé.</p>
        
        <div class="code-example">
          <h3 class="text-purple">Convention de nommage</h3>
          <p>En PHP, on utilise généralement le préfixe "get" suivi du nom de l'attribut :</p>
          <pre><code>&lt;?php
class <span class="class-name">Produit</span> {
    <span class="keyword">private</span> <span class="variable">$prix</span>;
    <span class="keyword">private</span> <span class="variable">$nom</span>;
    
    <span class="comment">// Getter pour l'attribut $prix</span>
    <span class="keyword">public</span> <span class="function">getPrix</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->prix;
    }
    
    <span class="comment">// Getter pour l'attribut $nom</span>
    <span class="keyword">public</span> <span class="function">getNom</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->nom;
    }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Getters avec transformation de données</h3>
          <p>Les getters peuvent aussi formater ou transformer les données avant de les retourner :</p>
          <pre><code>&lt;?php
class <span class="class-name">Utilisateur</span> {
    <span class="keyword">private</span> <span class="variable">$prenom</span>;
    <span class="keyword">private</span> <span class="variable">$nom</span>;
    
    <span class="keyword">public</span> <span class="function">getNomComplet</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->prenom . <span class="string">" "</span> . <span class="variable">$this</span>->nom;
    }
    
    <span class="keyword">public</span> <span class="function">getInitiales</span>() {
        <span class="keyword">return</span> <span class="function">strtoupper</span>(<span class="variable">$this</span>->prenom[<span class="number">0</span>] . <span class="variable">$this</span>->nom[<span class="number">0</span>]);
    }
}

<span class="variable">$user</span> = <span class="keyword">new</span> <span class="class-name">Utilisateur</span>();
<span class="function">echo</span> <span class="variable">$user</span>->getNomComplet(); <span class="comment">// "John Doe"</span>
<span class="function">echo</span> <span class="variable">$user</span>->getInitiales();   <span class="comment">// "JD"</span></code></pre>
        </div>
      </section>

      <!-- Les Setters -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les Setters (Mutateurs)</h2>
        <p>Les setters sont des méthodes qui permettent de <strong>modifier</strong> la valeur d'un attribut privé ou protégé avec validation.</p>
        
        <div class="code-example">
          <h3 class="text-purple">Convention de nommage</h3>
          <p>On utilise généralement le préfixe "set" suivi du nom de l'attribut :</p>
          <pre><code>&lt;?php
class <span class="class-name">CompteBancaire</span> {
    <span class="keyword">private</span> <span class="variable">$solde</span> = <span class="number">0</span>;
    
    <span class="comment">// Setter avec validation</span>
    <span class="keyword">public</span> <span class="function">setSolde</span>(<span class="variable">$montant</span>) {
        <span class="keyword">if</span> (<span class="variable">$montant</span> >= <span class="number">0</span>) {
            <span class="variable">$this</span>->solde = <span class="variable">$montant</span>;
        } <span class="keyword">else</span> {
            <span class="function">throw new</span> <span class="class-name">Exception</span>(<span class="string">"Le solde ne peut pas être négatif"</span>);
        }
    }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h3 class="text-purple">Setters avec transformation de données</h3>
          <pre><code>&lt;?php
class <span class="class-name">Email</span> {
    <span class="keyword">private</span> <span class="variable">$adresse</span>;
    
    <span class="keyword">public</span> <span class="function">setAdresse</span>(<span class="variable">$email</span>) {
        <span class="comment">// Nettoyer et valider l'email</span>
        <span class="variable">$email</span> = <span class="function">trim</span>(<span class="function">strtolower</span>(<span class="variable">$email</span>));
        
        <span class="keyword">if</span> (<span class="function">filter_var</span>(<span class="variable">$email</span>, FILTER_VALIDATE_EMAIL)) {
            <span class="variable">$this</span>->adresse = <span class="variable">$email</span>;
        } <span class="keyword">else</span> {
            <span class="function">throw new</span> <span class="class-name">Exception</span>(<span class="string">"Adresse email invalide"</span>);
        }
    }
}</code></pre>
        </div>
      </section>

      <!-- Exemple complet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple complet</h2>
        <p>Voici une implémentation complète avec getters et setters :</p>
        
        <div class="code-example">
          <pre><code>&lt;?php
class <span class="class-name">Etudiant</span> {
    <span class="keyword">private</span> <span class="variable">$nom</span>;
    <span class="keyword">private</span> <span class="variable">$notes</span> = [];
    <span class="keyword">private</span> <span class="variable">$dateNaissance</span>;
    
    <span class="comment">// GETTERS</span>
    <span class="keyword">public</span> <span class="function">getNom</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->nom;
    }
    
    <span class="keyword">public</span> <span class="function">getNotes</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->notes;
    }
    
    <span class="keyword">public</span> <span class="function">getMoyenne</span>() {
        <span class="keyword">if</span> (<span class="function">empty</span>(<span class="variable">$this</span>->notes)) {
            <span class="keyword">return</span> <span class="number">0</span>;
        }
        <span class="keyword">return</span> <span class="function">array_sum</span>(<span class="variable">$this</span>->notes) / <span class="function">count</span>(<span class="variable">$this</span>->notes);
    }
    
    <span class="keyword">public</span> <span class="function">getAge</span>() {
        <span class="variable">$aujourdhui</span> = <span class="keyword">new</span> <span class="class-name">DateTime</span>();
        <span class="variable">$naissance</span> = <span class="keyword">new</span> <span class="class-name">DateTime</span>(<span class="variable">$this</span>->dateNaissance);
        <span class="keyword">return</span> <span class="variable">$naissance</span>-><span class="function">diff</span>(<span class="variable">$aujourdhui</span>)->y;
    }
    
    <span class="comment">// SETTERS</span>
    <span class="keyword">public</span> <span class="function">setNom</span>(<span class="variable">$nom</span>) {
        <span class="keyword">if</span> (<span class="function">strlen</span>(<span class="variable">$nom</span>) >= <span class="number">2</span>) {
            <span class="variable">$this</span>->nom = <span class="function">ucwords</span>(<span class="function">trim</span>(<span class="variable">$nom</span>));
        } <span class="keyword">else</span> {
            <span class="function">throw new</span> <span class="class-name">Exception</span>(<span class="string">"Le nom doit contenir au moins 2 caractères"</span>);
        }
    }
    
    <span class="keyword">public</span> <span class="function">ajouterNote</span>(<span class="variable">$note</span>) {
        <span class="keyword">if</span> (<span class="variable">$note</span> >= <span class="number">0</span> <span class="operator">&amp;&amp;</span> <span class="variable">$note</span> <= <span class="number">20</span>) {
            <span class="variable">$this</span>->notes[] = <span class="variable">$note</span>;
        } <span class="keyword">else</span> {
            <span class="function">throw new</span> <span class="class-name">Exception</span>(<span class="string">"La note doit être entre 0 et 20"</span>);
        }
    }
    
    <span class="keyword">public</span> <span class="function">setDateNaissance</span>(<span class="variable">$date</span>) {
        <span class="variable">$dateTime</span> = <span class="function">DateTime</span>::<span class="function">createFromFormat</span>(<span class="string">'Y-m-d'</span>, <span class="variable">$date</span>);
        <span class="keyword">if</span> (<span class="variable">$dateTime</span> <span class="operator">&amp;&amp;</span> <span class="variable">$dateTime</span>-><span class="function">format</span>(<span class="string">'Y-m-d'</span>) === <span class="variable">$date</span>) {
            <span class="variable">$this</span>->dateNaissance = <span class="variable">$date</span>;
        } <span class="keyword">else</span> {
            <span class="function">throw new</span> <span class="class-name">Exception</span>(<span class="string">"Format de date invalide (YYYY-MM-DD)"</span>);
        }
    }
}

<span class="comment">// Utilisation</span>
<span class="variable">$etudiant</span> = <span class="keyword">new</span> <span class="class-name">Etudiant</span>();
<span class="variable">$etudiant</span>-><span class="function">setNom</span>(<span class="string">"marie dupont"</span>);
<span class="variable">$etudiant</span>-><span class="function">setDateNaissance</span>(<span class="string">"2000-05-15"</span>);
<span class="variable">$etudiant</span>-><span class="function">ajouterNote</span>(<span class="number">15</span>);
<span class="variable">$etudiant</span>-><span class="function">ajouterNote</span>(<span class="number">18</span>);

<span class="function">echo</span> <span class="variable">$etudiant</span>-><span class="function">getNom</span>();       <span class="comment">// "Marie Dupont"</span>
<span class="function">echo</span> <span class="variable">$etudiant</span>-><span class="function">getMoyenne</span>();  <span class="comment">// 16.5</span>
<span class="function">echo</span> <span class="variable">$etudiant</span>-><span class="function">getAge</span>();      <span class="comment">// 23 (selon la date actuelle)</span></code></pre>
        </div>
      </section>

      <!-- Méthodes magiques __get et __set -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Méthodes magiques __get et __set</h2>
        <p>PHP offre des méthodes magiques pour intercepter l'accès aux attributs non définis ou inaccessibles.</p>
        
        <div class="code-example">
          <h3 class="text-purple">Utilisation de __get et __set</h3>
          <pre><code>&lt;?php
class <span class="class-name">Personne</span> {
    <span class="keyword">private</span> <span class="variable">$data</span> = [];
    
    <span class="keyword">public</span> <span class="function">__get</span>(<span class="variable">$name</span>) {
        <span class="keyword">if</span> (<span class="function">array_key_exists</span>(<span class="variable">$name</span>, <span class="variable">$this</span>->data)) {
            <span class="keyword">return</span> <span class="variable">$this</span>->data[<span class="variable">$name</span>];
        }
        <span class="function">trigger_error</span>(<span class="string">"Propriété undefined: </span><span class="variable">$name</span><span class="string">"</span>, E_USER_NOTICE);
    }
    
    <span class="keyword">public</span> <span class="function">__set</span>(<span class="variable">$name</span>, <span class="variable">$value</span>) {
        <span class="comment">// Validation selon la propriété</span>
        <span class="keyword">switch</span> (<span class="variable">$name</span>) {
            <span class="keyword">case</span> <span class="string">'age'</span>:
                <span class="keyword">if</span> (<span class="variable">$value</span> >= <span class="number">0</span>) {
                    <span class="variable">$this</span>->data[<span class="variable">$name</span>] = <span class="variable">$value</span>;
                }
                <span class="keyword">break</span>;
            <span class="keyword">case</span> <span class="string">'email'</span>:
                <span class="keyword">if</span> (<span class="function">filter_var</span>(<span class="variable">$value</span>, FILTER_VALIDATE_EMAIL)) {
                    <span class="variable">$this</span>->data[<span class="variable">$name</span>] = <span class="variable">$value</span>;
                }
                <span class="keyword">break</span>;
            <span class="keyword">default</span>:
                <span class="variable">$this</span>->data[<span class="variable">$name</span>] = <span class="variable">$value</span>;
        }
    }
}

<span class="variable">$p</span> = <span class="keyword">new</span> <span class="class-name">Personne</span>();
<span class="variable">$p</span>->age = <span class="number">25</span>;    <span class="comment">// Appelle __set('age', 25)</span>
<span class="variable">$p</span>->email = <span class="string">"test@example.com"</span>; <span class="comment">// Appelle __set('email', 'test@example.com')</span>
<span class="function">echo</span> <span class="variable">$p</span>->age;     <span class="comment">// Appelle __get('age')</span></code></pre>
        </div>
        
        <div class="textExemple">
          <h3 class="text-purple">⚠️ Attention :</h3>
          <p>Les méthodes magiques sont pratiques mais peuvent rendre le code moins explicite. Utilisez-les avec parcimonie et préférez les getters/setters explicites pour la plupart des cas.</p>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        <div class="exercise">
          <h3 class="text-purple">Création d'une classe "Voiture" avec encapsulation</h3>
          <p>Créez une classe <code>Voiture</code> avec les attributs suivants :</p>
          <ul>
            <li><code>marque</code> (privé)</li>
            <li><code>modele</code> (privé)</li>
            <li><code>vitesse</code> (privé, toujours entre 0 et 200 km/h)</li>
            <li><code>kilometrage</code> (privé, toujours positif)</li>
          </ul>
          <p>Implémentez les getters et setters appropriés avec validation :</p>
          <ul>
            <li>Les marque et modèle ne doivent pas être vides</li>
            <li>La vitesse doit rester entre 0 et 200 km/h</li>
            <li>Le kilométrage ne peut qu'augmenter</li>
            <li>Ajoutez des méthodes <code>accelerer()</code> et <code>ralentir()</code></li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code>&lt;?php
class <span class="class-name">Voiture</span> {
    <span class="keyword">private</span> <span class="variable">$marque</span>;
    <span class="keyword">private</span> <span class="variable">$modele</span>;
    <span class="keyword">private</span> <span class="variable">$vitesse</span> = <span class="number">0</span>;
    <span class="keyword">private</span> <span class="variable">$kilometrage</span> = <span class="number">0</span>;
    
    <span class="comment">// GETTERS</span>
    <span class="keyword">public</span> <span class="function">getMarque</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->marque;
    }
    
    <span class="keyword">public</span> <span class="function">getModele</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->modele;
    }
    
    <span class="keyword">public</span> <span class="function">getVitesse</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->vitesse;
    }
    
    <span class="keyword">public</span> <span class="function">getKilometrage</span>() {
        <span class="keyword">return</span> <span class="variable">$this</span>->kilometrage;
    }
    
    <span class="comment">// SETTERS</span>
    <span class="keyword">public</span> <span class="function">setMarque</span>(<span class="variable">$marque</span>) {
        <span class="keyword">if</span> (<span class="function">!empty</span>(<span class="function">trim</span>(<span class="variable">$marque</span>))) {
            <span class="variable">$this</span>->marque = <span class="variable">$marque</span>;
        }
    }
    
    <span class="keyword">public</span> <span class="function">setModele</span>(<span class="variable">$modele</span>) {
        <span class="keyword">if</span> (<span class="function">!empty</span>(<span class="function">trim</span>(<span class="variable">$modele</span>))) {
            <span class="variable">$this</span>->modele = <span class="variable">$modele</span>;
        }
    }
    
    <span class="keyword">public</span> <span class="function">setVitesse</span>(<span class="variable">$vitesse</span>) {
        <span class="keyword">if</span> (<span class="variable">$vitesse</span> >= <span class="number">0</span> <span class="operator">&amp;&amp;</span> <span class="variable">$vitesse</span> <= <span class="number">200</span>) {
            <span class="variable">$this</span>->vitesse = <span class="variable">$vitesse</span>;
        }
    }
    
    <span class="keyword">public</span> <span class="function">setKilometrage</span>(<span class="variable">$km</span>) {
        <span class="keyword">if</span> (<span class="variable">$km</span> >= <span class="variable">$this</span>->kilometrage) {
            <span class="variable">$this</span>->kilometrage = <span class="variable">$km</span>;
        }
    }
    
    <span class="comment">// MÉTHODES SPÉCIALES</span>
    <span class="keyword">public</span> <span class="function">accelerer</span>(<span class="variable">$increment</span>) {
        <span class="variable">$nouvelleVitesse</span> = <span class="variable">$this</span>->vitesse + <span class="variable">$increment</span>;
        <span class="variable">$this</span>-><span class="function">setVitesse</span>(<span class="variable">$nouvelleVitesse</span>);
    }
    
    <span class="keyword">public</span> <span class="function">ralentir</span>(<span class="variable">$decrement</span>) {
        <span class="variable">$nouvelleVitesse</span> = <span class="variable">$this</span>->vitesse - <span class="variable">$decrement</span>;
        <span class="variable">$this</span>-><span class="function">setVitesse</span>(<span class="variable">$nouvelleVitesse</span>);
    }
    
    <span class="keyword">public</span> <span class="function">rouler</span>(<span class="variable">$distance</span>) {
        <span class="keyword">if</span> (<span class="variable">$distance</span> > <span class="number">0</span>) {
            <span class="variable">$this</span>->kilometrage += <span class="variable">$distance</span>;
        }
    }
}

<span class="comment">// Utilisation</span>
<span class="variable">$maVoiture</span> = <span class="keyword">new</span> <span class="class-name">Voiture</span>();
<span class="variable">$maVoiture</span>-><span class="function">setMarque</span>(<span class="string">"Renault"</span>);
<span class="variable">$maVoiture</span>-><span class="function">setModele</span>(<span class="string">"Clio"</span>);
<span class="variable">$maVoiture</span>-><span class="function">accelerer</span>(<span class="number">50</span>);
<span class="variable">$maVoiture</span>-><span class="function">rouler</span>(<span class="number">100</span>);

<span class="function">echo</span> <span class="string">"Vitesse: "</span> . <span class="variable">$maVoiture</span>-><span class="function">getVitesse</span>(); <span class="comment">// 50</span>
<span class="function">echo</span> <span class="string">"Kilométrage: "</span> . <span class="variable">$maVoiture</span>-><span class="function">getKilometrage</span>(); <span class="comment">// 100</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques</h2>
        <div class="textExemple">
          <h3 class="text-purple">✅ À faire :</h3>
          <ul>
            <li><strong>Utilisez des noms explicites</strong> : <code>getNomComplet()</code> plutôt que <code>getNC()</code></li>
            <li><strong>Validez toujours les données</strong> dans les setters</li>
            <li><strong>Lancez des exceptions</strong> pour les erreurs de validation</li>
            <li><strong>Documentez vos méthodes</strong> avec des commentaires</li>
            <li><strong>Utilisez le typage</strong> PHP 7+ pour les paramètres et retours</li>
          </ul>
          
          <h3 class="text-purple">❌ À éviter :</h3>
          <ul>
            <li><strong>Ne créez pas de setters inutiles</strong> pour les attributs immuables</li>
            <li><strong>Évitez la logique métier complexe</strong> dans les getters</li>
            <li><strong>Ne retournez pas des références</strong> aux tableaux/objets internes</li>
            <li><strong>N'utilisez pas les méthodes magiques</strong> comme substitut à une bonne conception</li>
          </ul>
          
          <h3 class="text-purple">Exemple avec typage PHP 7+ :</h3>
          <pre><code>&lt;?php
class <span class="class-name">Produit</span> {
    <span class="keyword">private</span> <span class="variable">$prix</span>;
    
    <span class="keyword">public</span> <span class="function">setPrix</span>(<span class="keyword">float</span> <span class="variable">$prix</span>): <span class="keyword">void</span> {
        <span class="keyword">if</span> (<span class="variable">$prix</span> >= <span class="number">0</span>) {
            <span class="variable">$this</span>->prix = <span class="variable">$prix</span>;
        }
    }
    
    <span class="keyword">public</span> <span class="function">getPrix</span>(): <span class="keyword">float</span> {
        <span class="keyword">return</span> <span class="variable">$this</span>->prix;
    }
}</code></pre>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary text-white">
        <h2>Conclusion</h2>
        <div class="textExemple">
          <p>Les getters et setters sont des éléments fondamentaux de la programmation orientée objet en PHP :</p>
          <ul>
            <li>Ils permettent de <strong>protéger l'intégrité des données</strong> grâce à la validation</li>
            <li>Ils offrent un <strong>contrôle précis</strong> sur l'accès aux attributs</li>
            <li>Ils facilitent la <strong>maintenance et l'évolution</strong> du code</li>
            <li>Ils améliorent la <strong>sécurité</strong> en empêchant les modifications non autorisées</li>
          </ul>
          <p>En maîtrisant les getters et setters, vous appliquez correctement le principe d'encapsulation et créez des classes plus robustes, maintenables et sécurisées. Ces pratiques sont essentielles pour développer des applications PHP de qualité professionnelle.</p>
          <p>Rappelez-vous : une bonne encapsulation aujourd'hui évite de nombreux bugs demain !</p>
        </div>
      </section>

    </div>
  </div>
</template>

<script>
export default {
  name: 'PhpGettersSettersLesson',
  // Vous pouvez ajouter des données ou méthodes si nécessaire
}
</script>

<style scoped>
/* Le CSS reste identique à celui de la première leçon */
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

.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }

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

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

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

@media (min-width: 1400px) {
    .lesson-content {
        max-width: 1300px;
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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>