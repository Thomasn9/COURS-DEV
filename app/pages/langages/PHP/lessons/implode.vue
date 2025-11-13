<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">La Fonction implode() en PHP</h1>
                <p class="lesson-meta text-white">Tableaux • Chaînes • Manipulation • PHP</p>
                <p class="lesson-meta text-white">
                    <span>Niveau : Intermédiaire</span>
                </p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à implode()</h2>
                <div class="textExemple">
                    <p>
                        La fonction <strong class="text-purple">implode()</strong> représente l'un des piliers
                        fondamentaux de la manipulation de données en PHP.
                        Bien plus qu'une simple fonction de concaténation, elle incarne un <strong>principe de
                            transformation structurelle</strong> qui permet
                        de convertir une structure de données complexe (un tableau) en une représentation linéaire et
                        sérialisée (une chaîne de caractères).
                    </p>
                </div>
                <div class="code-example">
                    <h3 class="text-purple">Syntaxe de base</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Syntaxe avec séparateur en premier paramètre</span>
<span class="variable">$chaine</span> = <span class="function">implode</span>(<span class="variable">$separateur</span>, <span class="variable">$tableau</span>);

<span class="comment">// Syntaxe alternative avec tableau en premier paramètre</span>
<span class="variable">$chaine</span> = <span class="function">implode</span>(<span class="variable">$tableau</span>, <span class="variable">$separateur</span>); <span class="comment">// Dépréciée, à éviter</span>
?&gt;</code></pre>
                </div>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Avant implode()</h3>
                        <pre><code class="language-php">&lt;?php
<span class="variable">$fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];
<span class="variable">$resultat</span> = <span class="string">""</span>;

<span class="keyword">foreach</span>(<span class="variable">$fruits</span> <span class="keyword">as</span> <span class="variable">$index</span> =&gt; <span class="variable">$fruit</span>) {
    <span class="variable">$resultat</span> .= <span class="variable">$fruit</span>;
    <span class="keyword">if</span>(<span class="variable">$index</span> &lt; <span class="function">count</span>(<span class="variable">$fruits</span>) - <span class="number">1</span>) {
        <span class="variable">$resultat</span> .= <span class="string">", "</span>;
    }
}

<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "pomme, banane, orange"</span>
?&gt;</code></pre>
                    </div>

                    <div>
                        <h3 class="text-purple">Avec implode()</h3>
                        <pre><code class="language-php">&lt;?php
<span class="variable">$fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$fruits</span>);

<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "pomme, banane, orange"</span>
?&gt;</code></pre>
                    </div>
                </div>
            </div>

            <!-- Utilisation Basique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation Basique de implode()</h2>

                <div class="code-example">
                    <h3 class="text-purple">Exemples fondamentaux</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Exemple 1: Séparation par des virgules</span>
<span class="variable">$noms</span> = [<span class="string">"Alice"</span>, <span class="string">"Bob"</span>, <span class="string">"Charlie"</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$noms</span>); 
<span class="comment">// Résultat: "Alice, Bob, Charlie"</span>

<span class="comment">// Exemple 2: Séparation par des tirets</span>
<span class="variable">$dates</span> = [<span class="string">"2024"</span>, <span class="string">"01"</span>, <span class="string">"15"</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">"-"</span>, <span class="variable">$dates</span>);
<span class="comment">// Résultat: "2024-01-15"</span>

<span class="comment">// Exemple 3: Séparation par des espaces</span>
<span class="variable">$mots</span> = [<span class="string">"Bonjour"</span>, <span class="string">"le"</span>, <span class="string">"monde"</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">" "</span>, <span class="variable">$mots</span>);
<span class="comment">// Résultat: "Bonjour le monde"</span>

<span class="comment">// Exemple 4: Séparation par des retours à la ligne</span>
<span class="variable">$lignes</span> = [<span class="string">"Ligne 1"</span>, <span class="string">"Ligne 2"</span>, <span class="string">"Ligne 3"</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">"\n"</span>, <span class="variable">$lignes</span>);
<span class="comment">// Résultat: 
// Ligne 1
// Ligne 2
// Ligne 3</span>
?&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Cas particuliers</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Tableau vide</span>
<span class="variable">$tableauVide</span> = [];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$tableauVide</span>); 
<span class="comment">// Résultat: "" (chaîne vide)</span>

<span class="comment">// Tableau avec un seul élément</span>
<span class="variable">$seulElement</span> = [<span class="string">"Unique"</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$seulElement</span>);
<span class="comment">// Résultat: "Unique" (pas de séparateur ajouté)</span>

<span class="comment">// Séparateur vide</span>
<span class="variable">$lettres</span> = [<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">""</span>, <span class="variable">$lettres</span>);
<span class="comment">// Résultat: "abc"</span>

<span class="comment">// Tableau avec valeurs numériques</span>
<span class="variable">$nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>];
<span class="keyword">echo</span> <span class="function">implode</span>(<span class="string">" + "</span>, <span class="variable">$nombres</span>);
<span class="comment">// Résultat: "1 + 2 + 3"</span>
?&gt;</code></pre>
                </div>
            </div>

            <!-- Cas d'Utilisation Avancés -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas d'Utilisation Avancés</h2>

                <div class="code-example">
                    <h3 class="text-purple">1. Génération de requêtes SQL</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Génération de clause IN pour SQL</span>
<span class="variable">$ids</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];
<span class="variable">$placeholders</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="function">array_fill</span>(<span class="number">0</span>, <span class="function">count</span>(<span class="variable">$ids</span>), <span class="string">"?"</span>));

<span class="variable">$requete</span> = <span class="string">"SELECT * FROM users WHERE id IN ("</span> . <span class="variable">$placeholders</span> . <span class="string">")"</span>;
<span class="keyword">echo</span> <span class="variable">$requete</span>;
<span class="comment">// Résultat: "SELECT * FROM users WHERE id IN (?, ?, ?, ?, ?)"</span>

<span class="comment">// Alternative avec implode direct sur les IDs</span>
<span class="variable">$requete2</span> = <span class="string">"SELECT * FROM users WHERE id IN ("</span> . <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$ids</span>) . <span class="string">")"</span>;
<span class="keyword">echo</span> <span class="variable">$requete2</span>;
<span class="comment">// Résultat: "SELECT * FROM users WHERE id IN (1, 2, 3, 4, 5)"</span>
?&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">2. Construction d'URL et chemins</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Construction d'URL avec paramètres</span>
<span class="variable">$parametres</span> = [
    <span class="string">"page"</span> =&gt; <span class="string">"profil"</span>,
    <span class="string">"id"</span> =&gt; <span class="number">123</span>,
    <span class="string">"lang"</span> =&gt; <span class="string">"fr"</span>
];

<span class="variable">$queryString</span> = <span class="function">implode</span>(<span class="string">"&amp;"</span>, <span class="function">array_map</span>(
    <span class="keyword">function</span>(<span class="variable">$key</span>, <span class="variable">$value</span>) {
        <span class="keyword">return</span> <span class="variable">$key</span> . <span class="string">"="</span> . <span class="variable">$value</span>;
    }, 
    <span class="function">array_keys</span>(<span class="variable">$parametres</span>), 
    <span class="variable">$parametres</span>
));

<span class="keyword">echo</span> <span class="string">"https://example.com?"</span> . <span class="variable">$queryString</span>;
<span class="comment">// Résultat: "https://example.com?page=profil&amp;id=123&amp;lang=fr"</span>

<span class="comment">// Construction de chemin de fichier</span>
<span class="variable">$partiesChemin</span> = [<span class="string">"var"</span>, <span class="string">"www"</span>, <span class="string">"html"</span>, <span class="string">"mon-projet"</span>];
<span class="variable">$cheminComplet</span> = <span class="string">"/"</span> . <span class="function">implode</span>(<span class="string">"/"</span>, <span class="variable">$partiesChemin</span>);
<span class="keyword">echo</span> <span class="variable">$cheminComplet</span>;
<span class="comment">// Résultat: "/var/www/html/mon-projet"</span>
?&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">3. Génération de HTML et listes</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Génération de liste HTML</span>
<span class="variable">$items</span> = [<span class="string">"Accueil"</span>, <span class="string">"À propos"</span>, <span class="string">"Services"</span>, <span class="string">"Contact"</span>];
<span class="variable">$listeHTML</span> = <span class="string">"&lt;ul&gt;\n"</span> . 
               <span class="function">implode</span>(<span class="string">"\n"</span>, <span class="function">array_map</span>(
                   <span class="keyword">function</span>(<span class="variable">$item</span>) {
                       <span class="keyword">return</span> <span class="string">"  &lt;li&gt;"</span> . <span class="variable">$item</span> . <span class="string">"&lt;/li&gt;"</span>;
                   }, 
                   <span class="variable">$items</span>
               )) . 
               <span class="string">"\n&lt;/ul&gt;"</span>;

<span class="keyword">echo</span> <span class="variable">$listeHTML</span>;
<span class="comment">// Résultat:
// &lt;ul&gt;
//   &lt;li&gt;Accueil&lt;/li&gt;
//   &lt;li&gt;À propos&lt;/li&gt;
//   &lt;li&gt;Services&lt;/li&gt;
//   &lt;li&gt;Contact&lt;/li&gt;
// &lt;/ul&gt;</span>

<span class="comment">// Génération d'options de select</span>
<span class="variable">$options</span> = [
    <span class="string">"fr"</span> =&gt; <span class="string">"Français"</span>,
    <span class="string">"en"</span> =&gt; <span class="string">"Anglais"</span>,
    <span class="string">"es"</span> =&gt; <span class="string">"Espagnol"</span>
];

<span class="variable">$optionsHTML</span> = <span class="function">implode</span>(<span class="string">"\n"</span>, <span class="function">array_map</span>(
    <span class="keyword">function</span>(<span class="variable">$valeur</span>, <span class="variable">$texte</span>) {
        <span class="keyword">return</span> <span class="string">"&lt;option value='"</span> . <span class="variable">$valeur</span> . <span class="string">"'&gt;"</span> . <span class="variable">$texte</span> . <span class="string">"&lt;/option&gt;"</span>;
    }, 
    <span class="function">array_keys</span>(<span class="variable">$options</span>), 
    <span class="variable">$options</span>
));

<span class="keyword">echo</span> <span class="string">"&lt;select&gt;\n"</span> . <span class="variable">$optionsHTML</span> . <span class="string">"\n&lt;/select&gt;"</span>;
?&gt;</code></pre>
                </div>
            </div>

            <!-- Combinaison avec d'autres fonctions -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Combinaison avec d'autres Fonctions</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Avec array_map()</h3>
                        <pre><code class="language-php">&lt;?php
<span class="comment">// Transformation puis assemblage</span>
<span class="variable">$nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>];
<span class="variable">$carres</span> = <span class="function">array_map</span>(
    <span class="keyword">function</span>(<span class="variable">$n</span>) { 
        <span class="keyword">return</span> <span class="variable">$n</span> * <span class="variable">$n</span>; 
    }, 
    <span class="variable">$nombres</span>
);

<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$carres</span>);
<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "1, 4, 9, 16"</span>

<span class="comment">// Version en une ligne</span>
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="function">array_map</span>(
    <span class="keyword">function</span>(<span class="variable">$n</span>) { <span class="keyword">return</span> <span class="variable">$n</span> * <span class="variable">$n</span>; }, 
    <span class="variable">$nombres</span>
));
?&gt;</code></pre>
                    </div>

                    <div>
                        <h3 class="text-purple">Avec array_filter()</h3>
                        <pre><code class="language-php">&lt;?php
<span class="comment">// Filtrage puis assemblage</span>
<span class="variable">$nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>, <span class="number">6</span>];
<span class="variable">$pairs</span> = <span class="function">array_filter</span>(
    <span class="variable">$nombres</span>, 
    <span class="keyword">function</span>(<span class="variable">$n</span>) { 
        <span class="keyword">return</span> <span class="variable">$n</span> % <span class="number">2</span> == <span class="number">0</span>; 
    }
);

<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$pairs</span>);
<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "2, 4, 6"</span>

<span class="comment">// Filtrage des valeurs vides</span>
<span class="variable">$donnees</span> = [<span class="string">"Alice"</span>, <span class="string">""</span>, <span class="string">"Bob"</span>, <span class="keyword">null</span>, <span class="string">"Charlie"</span>];
<span class="variable">$nettoyees</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="function">array_filter</span>(<span class="variable">$donnees</span>));
<span class="keyword">echo</span> <span class="variable">$nettoyees</span>; <span class="comment">// "Alice, Bob, Charlie"</span>
?&gt;</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Combinaisons complexes</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Transformation, filtrage et assemblage</span>
<span class="variable">$utilisateurs</span> = [
    [<span class="string">"nom"</span> =&gt; <span class="string">"Alice"</span>, <span class="string">"age"</span> =&gt; <span class="number">25</span>],
    [<span class="string">"nom"</span> =&gt; <span class="string">"Bob"</span>, <span class="string">"age"</span> =&gt; <span class="number">17</span>],
    [<span class="string">"nom"</span> =&gt; <span class="string">"Charlie"</span>, <span class="string">"age"</span> =&gt; <span class="number">30</span>],
    [<span class="string">"nom"</span> =&gt; <span class="string">"David"</span>, <span class="string">"age"</span> =&gt; <span class="number">16</span>]
];

<span class="comment">// Noms des utilisateurs majeurs, en majuscules</span>
<span class="variable">$nomsMajeurs</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="function">array_map</span>(
    <span class="keyword">function</span>(<span class="variable">$user</span>) {
        <span class="keyword">return</span> <span class="function">strtoupper</span>(<span class="variable">$user</span>[<span class="string">"nom"</span>]);
    },
    <span class="function">array_filter</span>(
        <span class="variable">$utilisateurs</span>,
        <span class="keyword">function</span>(<span class="variable">$user</span>) {
            <span class="keyword">return</span> <span class="variable">$user</span>[<span class="string">"age"</span>] &gt;= <span class="number">18</span>;
        }
    )
));

<span class="keyword">echo</span> <span class="variable">$nomsMajeurs</span>; <span class="comment">// "ALICE, CHARLIE"</span>

<span class="comment">// Version avec array_column pour plus de simplicité</span>
<span class="variable">$utilisateursMajeurs</span> = <span class="function">array_filter</span>(
    <span class="variable">$utilisateurs</span>, 
    <span class="keyword">function</span>(<span class="variable">$user</span>) { <span class="keyword">return</span> <span class="variable">$user</span>[<span class="string">"age"</span>] &gt;= <span class="number">18</span>; }
);
<span class="variable">$noms</span> = <span class="function">array_column</span>(<span class="variable">$utilisateursMajeurs</span>, <span class="string">"nom"</span>);
<span class="variable">$nomsMajeurs</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="function">array_map</span>(<span class="string">"strtoupper"</span>, <span class="variable">$noms</span>));
?&gt;</code></pre>
                </div>
            </div>

            <!-- Fonction inverse : explode() -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fonction Inverse : explode()</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">implode() → Tableau vers Chaîne</h3>
                        <pre><code class="language-php">&lt;?php
<span class="variable">$tableau</span> = [<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>];
<span class="variable">$chaine</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$tableau</span>);

<span class="keyword">echo</span> <span class="variable">$chaine</span>; <span class="comment">// "a, b, c"</span>
?&gt;</code></pre>
                    </div>

                    <div>
                        <h3 class="text-purple">explode() → Chaîne vers Tableau</h3>
                        <pre><code class="language-php">&lt;?php
<span class="variable">$chaine</span> = <span class="string">"a, b, c"</span>;
<span class="variable">$tableau</span> = <span class="function">explode</span>(<span class="string">", "</span>, <span class="variable">$chaine</span>);

<span class="function">print_r</span>(<span class="variable">$tableau</span>); 
<span class="comment">// Résultat: Array ( [0] =&gt; a [1] =&gt; b [2] =&gt; c )</span>
?&gt;</code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Cycle complet implode/explode</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// Données initiales</span>
<span class="variable">$donneesInitiales</span> = [<span class="string">"Paris"</span>, <span class="string">"Londres"</span>, <span class="string">"Berlin"</span>];

<span class="comment">// Conversion en chaîne pour stockage</span>
<span class="variable">$chaineStockee</span> = <span class="function">implode</span>(<span class="string">"|"</span>, <span class="variable">$donneesInitiales</span>);
<span class="keyword">echo</span> <span class="string">"Chaîne stockée: "</span> . <span class="variable">$chaineStockee</span> . <span class="string">"\n"</span>;
<span class="comment">// Chaîne stockée: Paris|Londres|Berlin</span>

<span class="comment">// Conversion inverse pour utilisation</span>
<span class="variable">$donneesRestituees</span> = <span class="function">explode</span>(<span class="string">"|"</span>, <span class="variable">$chaineStockee</span>);
<span class="function">print_r</span>(<span class="variable">$donneesRestituees</span>);
<span class="comment">// Array ( [0] =&gt; Paris [1] =&gt; Londres [2] =&gt; Berlin )</span>

<span class="comment">// Vérification de l'égalité</span>
<span class="variable">$identique</span> = <span class="variable">$donneesInitiales</span> === <span class="variable">$donneesRestituees</span>;
<span class="keyword">echo</span> <span class="string">"Données identiques: "</span> . (<span class="variable">$identique</span> ? <span class="string">"OUI"</span> : <span class="string">"NON"</span>);
<span class="comment">// Données identiques: OUI</span>
?&gt;</code></pre>
                </div>
            </div>

            <!-- Bonnes Pratiques et Pièges -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Pièges à Éviter</h2>

                <div class="code-example">
                    <h3 class="text-purple">Pièges courants</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// PIÈGE 1: Tableau associatif</span>
<span class="variable">$associatif</span> = [<span class="string">"nom"</span> =&gt; <span class="string">"Alice"</span>, <span class="string">"age"</span> =&gt; <span class="number">25</span>];
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$associatif</span>);
<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "Alice, 25" (seules les valeurs sont utilisées)</span>

<span class="comment">// PIÈGE 2: Types mélangés</span>
<span class="variable">$mixte</span> = [<span class="number">1</span>, <span class="string">"deux"</span>, <span class="keyword">true</span>, <span class="keyword">null</span>];
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">" - "</span>, <span class="variable">$mixte</span>);
<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "1 - deux - 1 - " (true = "1", null = "")</span>

<span class="comment">// PIÈGE 3: Tableau multidimensionnel</span>
<span class="variable">$multidim</span> = [[<span class="string">"a"</span>, <span class="string">"b"</span>], [<span class="string">"c"</span>, <span class="string">"d"</span>]];
<span class="comment">// $resultat = implode(", ", $multidim); // Avertissement et résultat inattendu</span>

<span class="comment">// SOLUTION: Aplatir d'abord le tableau</span>
<span class="function">function</span> <span class="function">aplatirTableau</span>(<span class="variable">$tableau</span>) {
    <span class="variable">$resultat</span> = [];
    <span class="function">array_walk_recursive</span>(<span class="variable">$tableau</span>, <span class="keyword">function</span>(<span class="variable">$v</span>) <span class="keyword">use</span> (&amp;<span class="variable">$resultat</span>) {
        <span class="variable">$resultat</span>[] = <span class="variable">$v</span>;
    });
    <span class="keyword">return</span> <span class="variable">$resultat</span>;
}

<span class="variable">$aplati</span> = <span class="function">aplatirTableau</span>(<span class="variable">$multidim</span>);
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$aplati</span>);
<span class="keyword">echo</span> <span class="variable">$resultat</span>; <span class="comment">// "a, b, c, d"</span>
?&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Bonnes pratiques</h3>
                    <pre><code class="language-php">&lt;?php
<span class="comment">// BONNE PRATIQUE 1: Toujours utiliser la syntaxe séparateur en premier</span>
<span class="variable">$bon</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$tableau</span>);      <span class="comment">// ✅ Recommandé</span>
<span class="comment">// $mauvais = implode($tableau, ", "); // ❌ Déprécié</span>

<span class="comment">// BONNE PRATIQUE 2: Vérifier le type des éléments</span>
<span class="variable">$donnees</span> = [<span class="number">1</span>, <span class="string">"texte"</span>, <span class="keyword">null</span>];
<span class="variable">$nettoyees</span> = <span class="function">array_map</span>(<span class="string">'strval'</span>, <span class="variable">$donnees</span>); <span class="comment">// Convertir en string</span>
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">" | "</span>, <span class="variable">$nettoyees</span>);

<span class="comment">// BONNE PRATIQUE 3: Utiliser des constantes pour les séparateurs réutilisables</span>
<span class="keyword">const</span> <span class="constant">SEPARATEUR_CSV</span> = <span class="string">","</span>;
<span class="keyword">const</span> <span class="constant">SEPARATEUR_URL</span> = <span class="string">"&amp;"</span>;

<span class="variable">$csv</span> = <span class="function">implode</span>(<span class="constant">SEPARATEUR_CSV</span>, <span class="variable">$donnees</span>);
<span class="variable">$url</span> = <span class="function">implode</span>(<span class="constant">SEPARATEUR_URL</span>, <span class="variable">$params</span>);

<span class="comment">// BONNE PRATIQUE 4: Gérer les tableaux vides</span>
<span class="variable">$tableau</span> = [];
<span class="variable">$resultat</span> = <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$tableau</span>);
<span class="keyword">if</span>(<span class="function">empty</span>(<span class="variable">$resultat</span>)) {
    <span class="variable">$resultat</span> = <span class="string">"Aucune donnée"</span>; <span class="comment">// Valeur par défaut</span>
}
?&gt;</code></pre>
                </div>
            </div>

            <!-- Exercice Pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Créez une fonction <code>formaterListe</code> qui prend un tableau d'éléments et retourne une
                        chaîne formatée selon ces règles :
                    </p>
                    <ul>
                        <li>Si le tableau est vide, retourner "Aucun élément"</li>
                        <li>Si le tableau a 1 élément, retourner cet élément</li>
                        <li>Si le tableau a 2 éléments, les séparer par " et "</li>
                        <li>Si le tableau a 3+ éléments, séparer tous par des virgules sauf les deux derniers par " et "
                        </li>
                    </ul>

                    <div class="code-example">
                        <h3 class="text-purple">Exemples attendus</h3>
                        <pre><code class="language-php">&lt;?php
<span class="function">formaterListe</span>([]);                    <span class="comment">// "Aucun élément"</span>
<span class="function">formaterListe</span>([<span class="string">"pomme"</span>]);            <span class="comment">// "pomme"</span>
<span class="function">formaterListe</span>([<span class="string">"pomme"</span>, <span class="string">"banane"</span>]); <span class="comment">// "pomme et banane"</span>
<span class="function">formaterListe</span>([<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>]); 
<span class="comment">// "pomme, banane et orange"</span>

<span class="function">formaterListe</span>([<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>, <span class="string">"d"</span>]);
<span class="comment">// "a, b, c et d"</span>
?&gt;</code></pre>
                    </div>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution Complète</h4>
                            <pre><code class="language-php">&lt;?php
<span class="keyword">function</span> <span class="function">formaterListe</span>(<span class="variable">$elements</span>) {
    <span class="variable">$count</span> = <span class="function">count</span>(<span class="variable">$elements</span>);
    
    <span class="keyword">switch</span>(<span class="variable">$count</span>) {
        <span class="keyword">case</span> <span class="number">0</span>:
            <span class="keyword">return</span> <span class="string">"Aucun élément"</span>;
            
        <span class="keyword">case</span> <span class="number">1</span>:
            <span class="keyword">return</span> <span class="variable">$elements</span>[<span class="number">0</span>];
            
        <span class="keyword">case</span> <span class="number">2</span>:
            <span class="keyword">return</span> <span class="function">implode</span>(<span class="string">" et "</span>, <span class="variable">$elements</span>);
            
        <span class="keyword">default</span>:
            <span class="variable">$premiers</span> = <span class="function">array_slice</span>(<span class="variable">$elements</span>, <span class="number">0</span>, <span class="variable">$count</span> - <span class="number">1</span>);
            <span class="variable">$derniers</span> = <span class="function">array_slice</span>(<span class="variable">$elements</span>, <span class="variable">$count</span> - <span class="number">2</span>);
            
            <span class="keyword">return</span> <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$premiers</span>) . <span class="string">" et "</span> . 
                   <span class="function">implode</span>(<span class="string">" et "</span>, <span class="variable">$derniers</span>);
    }
}

<span class="comment">// Tests</span>
<span class="keyword">echo</span> <span class="function">formaterListe</span>([]) . <span class="string">"\n"</span>;
<span class="keyword">echo</span> <span class="function">formaterListe</span>([<span class="string">"pomme"</span>]) . <span class="string">"\n"</span>;
<span class="keyword">echo</span> <span class="function">formaterListe</span>([<span class="string">"pomme"</span>, <span class="string">"banane"</span>]) . <span class="string">"\n"</span>;
<span class="keyword">echo</span> <span class="function">formaterListe</span>([<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>]) . <span class="string">"\n"</span>;
<span class="keyword">echo</span> <span class="function">formaterListe</span>([<span class="string">"a"</span>, <span class="string">"b"</span>, <span class="string">"c"</span>, <span class="string">"d"</span>]) . <span class="string">"\n"</span>;

<span class="comment">// Version alternative plus concise</span>
<span class="keyword">function</span> <span class="function">formaterListeConcise</span>(<span class="variable">$elements</span>) {
    <span class="variable">$count</span> = <span class="function">count</span>(<span class="variable">$elements</span>);
    
    <span class="keyword">if</span>(<span class="variable">$count</span> === <span class="number">0</span>) <span class="keyword">return</span> <span class="string">"Aucun élément"</span>;
    <span class="keyword">if</span>(<span class="variable">$count</span> === <span class="number">1</span>) <span class="keyword">return</span> <span class="variable">$elements</span>[<span class="number">0</span>];
    <span class="keyword">if</span>(<span class="variable">$count</span> === <span class="number">2</span>) <span class="keyword">return</span> <span class="function">implode</span>(<span class="string">" et "</span>, <span class="variable">$elements</span>);
    
    <span class="variable">$dernier</span> = <span class="function">array_pop</span>(<span class="variable">$elements</span>);
    <span class="keyword">return</span> <span class="function">implode</span>(<span class="string">", "</span>, <span class="variable">$elements</span>) . <span class="string">" et "</span> . <span class="variable">$dernier</span>;
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
                    La fonction <strong>implode()</strong> est un outil extrêmement utile en PHP pour transformer des
                    tableaux en chaînes de caractères formatées.
                    Sa simplicité d'utilisation et sa polyvalence en font une fonction incontournable pour de nombreuses
                    tâches courantes.
                </p>
                <p class="text-white">
                    En maîtrisant <strong>implode()</strong> et ses combinaisons avec d'autres fonctions comme
                    <strong>array_map()</strong> et <strong>array_filter()</strong>,
                    vous pouvez manipuler et formater des données complexes avec une grande efficacité.
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ImplodeFunctionLesson',
    data() {
        return {
            lessonTitle: 'La Fonction implode() en PHP'
        }
    },
    head() {
        return {
            title: this.lessonTitle,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Apprenez à utiliser la fonction implode() en PHP pour transformer des tableaux en chaînes de caractères. Cas d\'usage avancés et bonnes pratiques.'
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