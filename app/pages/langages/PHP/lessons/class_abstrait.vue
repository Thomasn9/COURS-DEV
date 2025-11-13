<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les Classes Abstraites en PHP</h1>
                <p class="lesson-meta text-white">PHP • Programmation Orientée Objet • Abstraction • Héritage • Design Patterns</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Classes Abstraites</h2>
                <p class="textExemple">
                    Les <strong>classes abstraites</strong> en PHP sont des classes qui ne peuvent pas être instanciées directement.
                    Elles servent de modèles de base pour d'autres classes et permettent de définir une structure commune
                    que les classes enfants doivent implémenter.
                </p>
                <p class="textExemple">
                    L'abstraction est l'un des concepts fondamentaux de la Programmation Orientée Objet (POO)
                    qui favorise la réutilisabilité, la maintenance et l'organisation du code.
                </p>
            </section>

            <!-- Concepts de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts de Base</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Qu'est-ce qu'une classe abstraite ?</h3>
                    <ul>
                        <li><strong>Ne peut pas être instanciée</strong> : On ne peut pas créer d'objet directement à partir d'elle</li>
                        <li><strong>Doit être étendue</strong> : Une classe enfant doit hériter de la classe abstraite</li>
                        <li><strong>Peut contenir des méthodes abstraites</strong> : Méthodes sans implémentation que les enfants doivent définir</li>
                        <li><strong>Peut contenir des méthodes concrètes</strong> : Méthodes avec implémentation héritée par les enfants</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe de base</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">NomDeLaClasseAbstraite</span> {
    <span class="php-comment">// Propriétés</span>
    <span class="php-keyword">protected</span> <span class="php-var">$propriete</span>;
    
    <span class="php-comment">// Méthode abstraite (sans implémentation)</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">methodeAbstraite</span>();
    
    <span class="php-comment">// Méthode concrète (avec implémentation)</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">methodeConcrete</span>() {
        <span class="php-comment">// Implémentation</span>
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Première classe abstraite -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Premier Exemple : Forme Géométrique</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Classe abstraite Forme</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">Forme</span> {
    <span class="php-keyword">protected</span> <span class="php-var">$couleur</span>;
    
    <span class="php-comment">// Constructeur</span>
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$couleur</span>) {
        <span class="php-var">$this</span>-&gt;couleur = <span class="php-var">$couleur</span>;
    }
    
    <span class="php-comment">// Méthode abstraite - doit être implémentée par les enfants</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">calculerAire</span>();
    
    <span class="php-comment">// Méthode concrète - héritée par les enfants</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getCouleur</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;couleur;
    }
    
    <span class="php-comment">// Méthode concrète</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">setCouleur</span>(<span class="php-var">$couleur</span>) {
        <span class="php-var">$this</span>-&gt;couleur = <span class="php-var">$couleur</span>;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Classes enfants concrètes</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Classe Cercle</h5>
                            <div class="code-example">
                                <pre><code><span class="php-keyword">class</span> <span class="php-class">Cercle</span> <span class="php-keyword">extends</span> <span class="php-class">Forme</span> {
    <span class="php-keyword">private</span> <span class="php-var">$rayon</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$couleur</span>, <span class="php-var">$rayon</span>) {
        <span class="php-var">parent</span>::<span class="php-function">__construct</span>(<span class="php-var">$couleur</span>);
        <span class="php-var">$this</span>-&gt;rayon = <span class="php-var">$rayon</span>;
    }
    
    <span class="php-comment">// Implémentation de la méthode abstraite</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">calculerAire</span>() {
        <span class="php-keyword">return</span> <span class="php-constant">M_PI</span> * <span class="php-var">$this</span>-&gt;rayon * <span class="php-var">$this</span>-&gt;rayon;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getRayon</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;rayon;
    }
}</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>Classe Rectangle</h5>
                            <div class="code-example">
                                <pre><code><span class="php-keyword">class</span> <span class="php-class">Rectangle</span> <span class="php-keyword">extends</span> <span class="php-class">Forme</span> {
    <span class="php-keyword">private</span> <span class="php-var">$largeur</span>;
    <span class="php-keyword">private</span> <span class="php-var">$hauteur</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$couleur</span>, <span class="php-var">$largeur</span>, <span class="php-var">$hauteur</span>) {
        <span class="php-var">parent</span>::<span class="php-function">__construct</span>(<span class="php-var">$couleur</span>);
        <span class="php-var">$this</span>-&gt;largeur = <span class="php-var">$largeur</span>;
        <span class="php-var">$this</span>-&gt;hauteur = <span class="php-var">$hauteur</span>;
    }
    
    <span class="php-comment">// Implémentation de la méthode abstraite</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">calculerAire</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;largeur * <span class="php-var">$this</span>-&gt;hauteur;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getLargeur</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;largeur;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getHauteur</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;hauteur;
    }
}</code></pre>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Utilisation pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation Pratique</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Instanciation et utilisation</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// ❌ IMPOSSIBLE : Instanciation d'une classe abstraite</span>
<span class="php-comment">// $forme = new Forme("rouge"); // Erreur fatale</span>

<span class="php-comment">// ✅ CORRECT : Instanciation des classes enfants</span>
<span class="php-var">$cercle</span> = <span class="php-keyword">new</span> <span class="php-class">Cercle</span>(<span class="php-string">"bleu"</span>, <span class="php-number">5</span>);
<span class="php-var">$rectangle</span> = <span class="php-keyword">new</span> <span class="php-class">Rectangle</span>(<span class="php-string">"vert"</span>, <span class="php-number">4</span>, <span class="php-number">6</span>);

<span class="php-comment">// Utilisation des méthodes</span>
<span class="php-function">echo</span> <span class="php-string">"Aire du cercle: "</span> . <span class="php-var">$cercle</span>-&gt;<span class="php-function">calculerAire</span>() . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;
<span class="php-function">echo</span> <span class="php-string">"Aire du rectangle: "</span> . <span class="php-var">$rectangle</span>-&gt;<span class="php-function">calculerAire</span>() . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;

<span class="php-comment">// Utilisation des méthodes héritées</span>
<span class="php-function">echo</span> <span class="php-string">"Couleur du cercle: "</span> . <span class="php-var">$cercle</span>-&gt;<span class="php-function">getCouleur</span>() . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;
<span class="php-var">$rectangle</span>-&gt;<span class="php-function">setCouleur</span>(<span class="php-string">"jaune"</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Polymorphisme avec classes abstraites</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">function</span> <span class="php-function">afficherInformationsForme</span>(<span class="php-class">Forme</span> <span class="php-var">$forme</span>) {
    <span class="php-function">echo</span> <span class="php-string">"Type: "</span> . <span class="php-function">get_class</span>(<span class="php-var">$forme</span>) . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;
    <span class="php-function">echo</span> <span class="php-string">"Couleur: "</span> . <span class="php-var">$forme</span>-&gt;<span class="php-function">getCouleur</span>() . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;
    <span class="php-function">echo</span> <span class="php-string">"Aire: "</span> . <span class="php-var">$forme</span>-&gt;<span class="php-function">calculerAire</span>() . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;
    <span class="php-function">echo</span> <span class="php-string">"------------------------</span><span class="php-escape">\n</span><span class="php-string">"</span>;
}

<span class="php-comment">// Utilisation polymorphe</span>
<span class="php-function">afficherInformationsForme</span>(<span class="php-var">$cercle</span>);
<span class="php-function">afficherInformationsForme</span>(<span class="php-var">$rectangle</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes abstraites -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes Abstraites</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Règles des méthodes abstraites</h3>
                    <ul>
                        <li><strong>Déclarées sans implémentation</strong> : Pas de corps de méthode {}</li>
                        <li><strong>Doivent être public ou protected</strong> : Ne peuvent pas être private</li>
                        <li><strong>Doivent être implémentées</strong> par toutes les classes enfants concrètes</li>
                        <li><strong>Signature doit être respectée</strong> : Même visibilité et paramètres</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple détaillé</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>❌ Incorrect</h5>
                            <div class="code-example">
                                <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">Animal</span> {
    <span class="php-comment">// ❌ private interdit</span>
    <span class="php-keyword">abstract private</span> <span class="php-keyword">function</span> <span class="php-function">dormir</span>();
    
    <span class="php-comment">// ❌ Implémentation interdite</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">manger</span>() {
        <span class="php-function">echo</span> <span class="php-string">"Je mange"</span>;
    }
}</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>✅ Correct</h5>
                            <div class="code-example">
                                <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">Animal</span> {
    <span class="php-comment">// ✅ public ou protected</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">dormir</span>();
    
    <span class="php-comment">// ✅ Pas d'implémentation</span>
    <span class="php-keyword">abstract protected</span> <span class="php-keyword">function</span> <span class="php-function">manger</span>();
    
    <span class="php-comment">// ✅ Méthode concrète</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">respirer</span>() {
        <span class="php-function">echo</span> <span class="php-string">"Je respire"</span>;
    }
}</code></pre>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Exemple système de paiement -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple Réel : Système de Paiement</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Classe abstraite Paiement</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">Paiement</span> {
    <span class="php-keyword">protected</span> <span class="php-var">$montant</span>;
    <span class="php-keyword">protected</span> <span class="php-var">$devise</span>;
    <span class="php-keyword">protected</span> <span class="php-var">$datePaiement</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$montant</span>, <span class="php-var">$devise</span> = <span class="php-string">'EUR'</span>) {
        <span class="php-var">$this</span>-&gt;montant = <span class="php-var">$montant</span>;
        <span class="php-var">$this</span>-&gt;devise = <span class="php-var">$devise</span>;
        <span class="php-var">$this</span>-&gt;datePaiement = <span class="php-keyword">new</span> <span class="php-class">DateTime</span>();
    }
    
    <span class="php-comment">// Méthodes abstraites</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">traiterPaiement</span>();
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">obtenirDetails</span>();
    
    <span class="php-comment">// Méthodes concrètes</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getMontant</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;montant . <span class="php-string">' '</span> . <span class="php-var">$this</span>-&gt;devise;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getDatePaiement</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;datePaiement-&gt;<span class="php-function">format</span>(<span class="php-string">'Y-m-d H:i:s'</span>);
    }
    
    <span class="php-comment">// Méthode concrète avec implémentation par défaut</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">verifierSolde</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;montant &gt; <span class="php-number">0</span>;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Implémentations concrètes</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Paiement Carte Bancaire</h5>
                            <div class="code-example">
                                <pre><code><span class="php-keyword">class</span> <span class="php-class">PaiementCarte</span> <span class="php-keyword">extends</span> <span class="php-class">Paiement</span> {
    <span class="php-keyword">private</span> <span class="php-var">$numeroCarte</span>;
    <span class="php-keyword">private</span> <span class="php-var">$titulaire</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$montant</span>, <span class="php-var">$numeroCarte</span>, <span class="php-var">$titulaire</span>) {
        <span class="php-var">parent</span>::<span class="php-function">__construct</span>(<span class="php-var">$montant</span>);
        <span class="php-var">$this</span>-&gt;numeroCarte = <span class="php-var">$numeroCarte</span>;
        <span class="php-var">$this</span>-&gt;titulaire = <span class="php-var">$titulaire</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">traiterPaiement</span>() {
        <span class="php-comment">// Simulation traitement carte</span>
        <span class="php-keyword">return</span> <span class="php-string">"Paiement carte traité pour "</span> . <span class="php-var">$this</span>-&gt;titulaire;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">obtenirDetails</span>() {
        <span class="php-keyword">return</span> [
            <span class="php-string">'type'</span> =&gt; <span class="php-string">'Carte bancaire'</span>,
            <span class="php-string">'titulaire'</span> =&gt; <span class="php-var">$this</span>-&gt;titulaire,
            <span class="php-string">'montant'</span> =&gt; <span class="php-var">$this</span>-&gt;<span class="php-function">getMontant</span>(),
            <span class="php-string">'date'</span> =&gt; <span class="php-var">$this</span>-&gt;<span class="php-function">getDatePaiement</span>()
        ];
    }
}</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>Paiement PayPal</h5>
                            <div class="code-example">
                                <pre><code><span class="php-keyword">class</span> <span class="php-class">PaiementPayPal</span> <span class="php-keyword">extends</span> <span class="php-class">Paiement</span> {
    <span class="php-keyword">private</span> <span class="php-var">$email</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$montant</span>, <span class="php-var">$email</span>) {
        <span class="php-var">parent</span>::<span class="php-function">__construct</span>(<span class="php-var">$montant</span>, <span class="php-string">'USD'</span>);
        <span class="php-var">$this</span>-&gt;email = <span class="php-var">$email</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">traiterPaiement</span>() {
        <span class="php-comment">// Simulation traitement PayPal</span>
        <span class="php-keyword">return</span> <span class="php-string">"Paiement PayPal traité pour "</span> . <span class="php-var">$this</span>-&gt;email;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">obtenirDetails</span>() {
        <span class="php-keyword">return</span> [
            <span class="php-string">'type'</span> =&gt; <span class="php-string">'PayPal'</span>,
            <span class="php-string">'email'</span> =&gt; <span class="php-var">$this</span>-&gt;email,
            <span class="php-string">'montant'</span> =&gt; <span class="php-var">$this</span>-&gt;<span class="php-function">getMontant</span>(),
            <span class="php-string">'date'</span> =&gt; <span class="php-var">$this</span>-&gt;<span class="php-function">getDatePaiement</span>()
        ];
    }
}</code></pre>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Avantages et utilisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages des Classes Abstraites</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Pourquoi utiliser des classes abstraites ?</h3>
                    <ul>
                        <li><strong>Forcer l'implémentation</strong> : Garantir que certaines méthodes existent</li>
                        <li><strong>Réutiliser du code</strong> : Éviter la duplication avec des méthodes concrètes</li>
                        <li><strong>Contrat clair</strong> : Définir une interface commune pour un groupe de classes</li>
                        <li><strong>Polymorphisme</strong> : Traiter différents objets de manière uniforme</li>
                        <li><strong>Maintenance</strong> : Modifications centralisées dans la classe parente</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple d'utilisation polymorphe</h3>
                    <div class="code-example">
                        <pre><code><span class="php-keyword">function</span> <span class="php-function">processerPaiements</span>(<span class="php-class">Paiement</span> <span class="php-var">$paiement</span>) {
    <span class="php-keyword">if</span> (!<span class="php-var">$paiement</span>-&gt;<span class="php-function">verifierSolde</span>()) {
        <span class="php-keyword">throw new</span> <span class="php-class">Exception</span>(<span class="php-string">"Solde insuffisant"</span>);
    }
    
    <span class="php-var">$resultat</span> = <span class="php-var">$paiement</span>-&gt;<span class="php-function">traiterPaiement</span>();
    <span class="php-var">$details</span> = <span class="php-var">$paiement</span>-&gt;<span class="php-function">obtenirDetails</span>();
    
    <span class="php-keyword">return</span> [
        <span class="php-string">'resultat'</span> =&gt; <span class="php-var">$resultat</span>,
        <span class="php-string">'details'</span> =&gt; <span class="php-var">$details</span>
    ];
}

<span class="php-comment">// Utilisation avec différents types de paiement</span>
<span class="php-var">$paiementCarte</span> = <span class="php-keyword">new</span> <span class="php-class">PaiementCarte</span>(<span class="php-number">100</span>, <span class="php-string">'1234-5678-9012-3456'</span>, <span class="php-string">'John Doe'</span>);
<span class="php-var">$paiementPayPal</span> = <span class="php-keyword">new</span> <span class="php-class">PaiementPayPal</span>(<span class="php-number">50</span>, <span class="php-string">'john@example.com'</span>);

<span class="php-var">$resultat1</span> = <span class="php-function">processerPaiements</span>(<span class="php-var">$paiementCarte</span>);
<span class="php-var">$resultat2</span> = <span class="php-function">processerPaiements</span>(<span class="php-var">$paiementPayPal</span>);

<span class="php-function">print_r</span>(<span class="php-var">$resultat1</span>);
<span class="php-function">print_r</span>(<span class="php-var">$resultat2</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Différence avec les interfaces -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Classes Abstraites vs Interfaces</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Comparaison</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Classe Abstraite</h5>
                            <ul>
                                <li><strong>Peut contenir des méthodes concrètes</strong></li>
                                <li><strong>Peut avoir des propriétés</strong></li>
                                <li><strong>Peut avoir un constructeur</strong></li>
                                <li><strong>Héritage simple uniquement</strong></li>
                                <li><strong>Représente un "est-un"</strong></li>
                                <li><strong>Code partagé entre classes apparentées</strong></li>
                            </ul>
                        </div>
                        <div>
                            <h5>Interface</h5>
                            <ul>
                                <li><strong>Uniquement des méthodes abstraites</strong></li>
                                <li><strong>Pas de propriétés (constantes uniquement)</strong></li>
                                <li><strong>Pas de constructeur</strong></li>
                                <li><strong>Implémentation multiple possible</strong></li>
                                <li><strong>Représente un "peut-faire"</strong></li>
                                <li><strong>Contrat pour fonctionnalités</strong></li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Quand utiliser laquelle ?</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// ✅ Classe abstraite quand :</span>
<span class="php-comment">// - Les classes partagent du code commun</span>
<span class="php-comment">// - Il y a une relation "est-un" forte</span>
<span class="php-comment">// - Besoin de propriétés communes</span>
<span class="php-keyword">abstract class</span> <span class="php-class">Vehicule</span> {
    <span class="php-keyword">protected</span> <span class="php-var">$vitesse</span>;
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">avancer</span>() { ... }
}

<span class="php-comment">// ✅ Interface quand :</span>
<span class="php-comment">// - Définir un contrat de comportement</span>
<span class="php-comment">// - Classes non apparentées partagent des capacités</span>
<span class="php-comment">// - Besoin d'implémentation multiple</span>
<span class="php-keyword">interface</span> <span class="php-class">Volant</span> {
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">decoller</span>();
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">atterrir</span>();
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Conception des classes abstraites</h3>
                    <ul>
                        <li><strong>Nommage explicite</strong> : Utiliser des noms qui reflètent le concept abstrait</li>
                        <li><strong>Minimiser les méthodes abstraites</strong> : Ne rendre abstrait que le nécessaire</li>
                        <li><strong>Documentation</strong> : Expliquer le contrat que les enfants doivent respecter</li>
                        <li><strong>Visibilité appropriée</strong> : Utiliser protected pour les méthodes internes</li>
                        <li><strong>Constructeur protégé</strong> : Si la classe ne doit jamais être instanciée</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple de conception solide</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">/**
 * Classe abstraite représentant un employé
 * Définit le contrat de base pour tous les types d'employés
 */</span>
<span class="php-keyword">abstract class</span> <span class="php-class">Employe</span> {
    <span class="php-keyword">protected</span> <span class="php-var">$nom</span>;
    <span class="php-keyword">protected</span> <span class="php-var">$salaireBase</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$nom</span>, <span class="php-var">$salaireBase</span>) {
        <span class="php-var">$this</span>-&gt;nom = <span class="php-var">$nom</span>;
        <span class="php-var">$this</span>-&gt;salaireBase = <span class="php-var">$salaireBase</span>;
    }
    
    <span class="php-comment">// Méthode abstraite - chaque type d'employé calcule son salaire différemment</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">calculerSalaire</span>();
    
    <span class="php-comment">// Méthode concrète - commune à tous les employés</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getNom</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;nom;
    }
    
    <span class="php-comment">// Méthode concrète avec implémentation par défaut</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getSalaireBase</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;salaireBase;
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Système de Notifications</h3>
                    <p>Créez un système de notifications avec :</p>
                    <ul>
                        <li>Une classe abstraite Notification</li>
                        <li>Des classes EmailNotification et SMSNotification</li>
                        <li>Méthodes abstraites : envoyer(), getType()</li>
                        <li>Méthodes concrètes : formatMessage(), logger()</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">Notification</span> {
    <span class="php-keyword">protected</span> <span class="php-var">$message</span>;
    <span class="php-keyword">protected</span> <span class="php-var">$destinataire</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$message</span>, <span class="php-var">$destinataire</span>) {
        <span class="php-var">$this</span>-&gt;message = <span class="php-var">$message</span>;
        <span class="php-var">$this</span>-&gt;destinataire = <span class="php-var">$destinataire</span>;
    }
    
    <span class="php-comment">// Méthodes abstraites</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">envoyer</span>();
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">getType</span>();
    
    <span class="php-comment">// Méthodes concrètes</span>
    <span class="php-keyword">protected</span> <span class="php-keyword">function</span> <span class="php-function">formatMessage</span>() {
        <span class="php-keyword">return</span> <span class="php-string">"["</span> . <span class="php-function">date</span>(<span class="php-string">'Y-m-d H:i:s'</span>) . <span class="php-string">"] "</span> . <span class="php-var">$this</span>-&gt;message;
    }
    
    <span class="php-keyword">protected</span> <span class="php-keyword">function</span> <span class="php-function">logger</span>(<span class="php-var">$action</span>) {
        <span class="php-function">echo</span> <span class="php-string">"Log: </span><span class="php-var">$action</span><span class="php-string"> pour </span><span class="php-var">{$this-&gt;destinataire}</span><span class="php-string">"</span> . <span class="php-string">"</span><span class="php-escape">\n</span><span class="php-string">"</span>;
    }
}

<span class="php-keyword">class</span> <span class="php-class">EmailNotification</span> <span class="php-keyword">extends</span> <span class="php-class">Notification</span> {
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">envoyer</span>() {
        <span class="php-var">$messageFormate</span> = <span class="php-var">$this</span>-&gt;<span class="php-function">formatMessage</span>();
        <span class="php-var">$this</span>-&gt;<span class="php-function">logger</span>(<span class="php-string">"Email envoyé"</span>);
        <span class="php-keyword">return</span> <span class="php-string">"Email envoyé à </span><span class="php-var">{$this-&gt;destinataire}</span><span class="php-string">: </span><span class="php-var">$messageFormate</span><span class="php-string">"</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getType</span>() {
        <span class="php-keyword">return</span> <span class="php-string">"Email"</span>;
    }
}

<span class="php-keyword">class</span> <span class="php-class">SMSNotification</span> <span class="php-keyword">extends</span> <span class="php-class">Notification</span> {
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">envoyer</span>() {
        <span class="php-var">$messageFormate</span> = <span class="php-var">$this</span>-&gt;<span class="php-function">formatMessage</span>();
        <span class="php-var">$this</span>-&gt;<span class="php-function">logger</span>(<span class="php-string">"SMS envoyé"</span>);
        <span class="php-keyword">return</span> <span class="php-string">"SMS envoyé à </span><span class="php-var">{$this-&gt;destinataire}</span><span class="php-string">: </span><span class="php-var">$messageFormate</span><span class="php-string">"</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getType</span>() {
        <span class="php-keyword">return</span> <span class="php-string">"SMS"</span>;
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Gestion des Employés</h3>
                    <p>Implémentez un système de gestion d'employés avec différents types de salaires :</p>
                    <ul>
                        <li>EmployeTempsPlein (salaire fixe)</li>
                        <li>EmployeTempsPartiel (salaire horaire)</li>
                        <li>EmployeCommission (salaire + commission)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="php-keyword">abstract class</span> <span class="php-class">Employe</span> {
    <span class="php-keyword">protected</span> <span class="php-var">$nom</span>;
    <span class="php-keyword">protected</span> <span class="php-var">$prenom</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$nom</span>, <span class="php-var">$prenom</span>) {
        <span class="php-var">$this</span>-&gt;nom = <span class="php-var">$nom</span>;
        <span class="php-var">$this</span>-&gt;prenom = <span class="php-var">$prenom</span>;
    }
    
    <span class="php-comment">// Méthode abstraite</span>
    <span class="php-keyword">abstract public</span> <span class="php-keyword">function</span> <span class="php-function">calculerSalaire</span>();
    
    <span class="php-comment">// Méthodes concrètes</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getNomComplet</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;prenom . <span class="php-string">' '</span> . <span class="php-var">$this</span>-&gt;nom;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getInformations</span>() {
        <span class="php-keyword">return</span> [
            <span class="php-string">'nom'</span> =&gt; <span class="php-var">$this</span>-&gt;<span class="php-function">getNomComplet</span>(),
            <span class="php-string">'type'</span> =&gt; <span class="php-function">get_class</span>(<span class="php-var">$this</span>),
            <span class="php-string">'salaire'</span> =&gt; <span class="php-var">$this</span>-&gt;<span class="php-function">calculerSalaire</span>()
        ];
    }
}

<span class="php-keyword">class</span> <span class="php-class">EmployeTempsPlein</span> <span class="php-keyword">extends</span> <span class="php-class">Employe</span> {
    <span class="php-keyword">private</span> <span class="php-var">$salaireMensuel</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$nom</span>, <span class="php-var">$prenom</span>, <span class="php-var">$salaireMensuel</span>) {
        <span class="php-var">parent</span>::<span class="php-function">__construct</span>(<span class="php-var">$nom</span>, <span class="php-var">$prenom</span>);
        <span class="php-var">$this</span>-&gt;salaireMensuel = <span class="php-var">$salaireMensuel</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">calculerSalaire</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;salaireMensuel;
    }
}

<span class="php-keyword">class</span> <span class="php-class">EmployeTempsPartiel</span> <span class="php-keyword">extends</span> <span class="php-class">Employe</span> {
    <span class="php-keyword">private</span> <span class="php-var">$tauxHoraire</span>;
    <span class="php-keyword">private</span> <span class="php-var">$heuresTravaillees</span>;
    
    <span class="php-keyword">public function</span> <span class="php-function">__construct</span>(<span class="php-var">$nom</span>, <span class="php-var">$prenom</span>, <span class="php-var">$tauxHoraire</span>, <span class="php-var">$heuresTravaillees</span>) {
        <span class="php-var">parent</span>::<span class="php-function">__construct</span>(<span class="php-var">$nom</span>, <span class="php-var">$prenom</span>);
        <span class="php-var">$this</span>-&gt;tauxHoraire = <span class="php-var">$tauxHoraire</span>;
        <span class="php-var">$this</span>-&gt;heuresTravaillees = <span class="php-var">$heuresTravaillees</span>;
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">calculerSalaire</span>() {
        <span class="php-keyword">return</span> <span class="php-var">$this</span>-&gt;tauxHoraire * <span class="php-var">$this</span>-&gt;heuresTravaillees;
    }
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Récapitulatif</h3>
                    <ul>
                        <li><strong>Classes abstraites</strong> : Modèles non instanciables pour l'héritage</li>
                        <li><strong>Méthodes abstraites</strong> : Contrat que les enfants doivent implémenter</li>
                        <li><strong>Méthodes concrètes</strong> : Code partagé entre les classes enfants</li>
                        <li><strong>Polymorphisme</strong> : Traitement uniforme d'objets différents</li>
                        <li><strong>Maintenance</strong> : Modifications centralisées</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques à retenir</h3>
                    <ul>
                        <li>✅ <strong>Utiliser l'abstraction</strong> pour les relations "est-un"</li>
                        <li>✅ <strong>Minimiser les méthodes abstraites</strong> au strict nécessaire</li>
                        <li>✅ <strong>Documenter le contrat</strong> que les enfants doivent respecter</li>
                        <li>✅ <strong>Utiliser le polymorphisme</strong> pour un code plus flexible</li>
                        <li>❌ <strong>Éviter l'héritage profond</strong> et les hiérarchies complexes</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Prochaines étapes</h3>
                    <p>
                        Après avoir maîtrisé les classes abstraites, explorez :
                    </p>
                    <ul>
                        <li>Les <strong>interfaces</strong> pour l'implémentation multiple</li>
                        <li>Les <strong>traits</strong> pour la composition</li>
                        <li>Les <strong>design patterns</strong> utilisant l'abstraction</li>
                        <li>La <strong>réflexion</strong> pour l'introspection des classes</li>
                    </ul>
                </div>
            </section>
        </div>
    </div>
</template>

<script>

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