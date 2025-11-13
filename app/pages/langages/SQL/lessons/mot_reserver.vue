<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Gérer les Mots Réservés SQL dans les Tables</h1>
                <p class="lesson-meta text-white">SQL • MySQL • Mots réservés • Bonnes pratiques • Conventions de nommage</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Mots Réservés SQL</h2>
                <p class="textExemple">
                    Les <strong>mots réservés SQL</strong> sont des termes qui ont une signification spéciale dans le langage SQL.
                    Ils ne peuvent pas être utilisés directement comme noms de tables, colonnes ou autres objets de base de données
                    sans une gestion appropriée.
                </p>
                <p class="textExemple">
                    Cette leçon vous apprendra à identifier, éviter et gérer correctement les mots réservés
                    lors de la conception de votre base de données.
                </p>
            </section>

            <!-- Problème des mots réservés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le Problème avec les Mots Réservés</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple d'erreur courante</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ ERREUR : 'group' est un mot réservé SQL</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">group</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">name</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>)
);

<span class="sql-comment">-- ❌ ERREUR : 'order' est un mot réservé SQL</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">order</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date</span> <span class="sql-type">DATE</span>
);</code></pre>
                    </div>
                    <p class="warning-text">Ces requêtes généreront des erreurs de syntaxe car GROUP et ORDER sont des mots réservés SQL.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Pourquoi c'est problématique ?</h3>
                    <ul>
                        <li><strong>Confusion du parseur SQL</strong> : Le moteur ne sait pas si vous faites référence à une table ou à une clause SQL</li>
                        <li><strong>Erreurs de compilation</strong> : La requête ne peut pas être exécutée</li>
                        <li><strong>Code illisible</strong> : Difficulté à distinguer les noms des commandes</li>
                        <li><strong>Portabilité réduite</strong> : Les mots réservés peuvent varier entre SGBD</li>
                    </ul>
                </div>
            </section>

            <!-- Solution : Les guillemets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Solution : Utiliser les Guillemets</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Guillemets avec MySQL</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ✅ CORRECT : Utilisation des backticks `</span>
<span class="sql-reserved">CREATE TABLE</span> `<span class="sql-identifier">group</span>` (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">name</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>)
);

<span class="sql-reserved">CREATE TABLE</span> `<span class="sql-identifier">order</span>` (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span>,
  `<span class="sql-identifier">date</span>` <span class="sql-type">DATE</span>,
  `<span class="sql-identifier">desc</span>` <span class="sql-type">TEXT</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Guillemets selon les SGBD</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>MySQL / MariaDB</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-reserved">CREATE TABLE</span> `<span class="sql-identifier">order</span>` (
  `<span class="sql-identifier">select</span>` <span class="sql-type">INT</span>,
  `<span class="sql-identifier">where</span>` <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>)
);</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>PostgreSQL</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-reserved">CREATE TABLE</span> "<span class="sql-identifier">order</span>" (
  "<span class="sql-identifier">select</span>" <span class="sql-type">INT</span>,
  "<span class="sql-identifier">where</span>" <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>)
);</code></pre>
                            </div>
                        </div>
                    </div>
                    <div class="code-comparison">
                        <div>
                            <h5>SQL Server</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-reserved">CREATE TABLE</span> [<span class="sql-identifier">order</span>] (
  [<span class="sql-identifier">select</span>] <span class="sql-type">INT</span>,
  [<span class="sql-identifier">where</span>] <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>)
);</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>Oracle</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-reserved">CREATE TABLE</span> "<span class="sql-identifier">order</span>" (
  "<span class="sql-identifier">select</span>" <span class="sql-type">NUMBER</span>,
  "<span class="sql-identifier">where</span>" <span class="sql-type">VARCHAR2</span>(<span class="sql-number">100</span>)
);</code></pre>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Mots réservés courants -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Mots Réservés Courants à Éviter</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Liste des mots réservés les plus problématiques</h3>
                    <div class="warning-section">
                        <h4 class="text-purple">🚨 Mots réservés très courants :</h4>
                        <div class="code-example">
                            <div style="columns: 3; column-gap: 2rem;">
                                <ul style="margin: 0; padding-left: 1.5rem;">
                                    <li>SELECT</li>
                                    <li>INSERT</li>
                                    <li>UPDATE</li>
                                    <li>DELETE</li>
                                    <li>CREATE</li>
                                    <li>DROP</li>
                                    <li>ALTER</li>
                                    <li>TABLE</li>
                                </ul>
                                <ul style="margin: 0; padding-left: 1.5rem;">
                                    <li>WHERE</li>
                                    <li>GROUP</li>
                                    <li>ORDER</li>
                                    <li>BY</li>
                                    <li>HAVING</li>
                                    <li>JOIN</li>
                                    <li>UNION</li>
                                    <li>VIEW</li>
                                </ul>
                                <ul style="margin: 0; padding-left: 1.5rem;">
                                    <li>INDEX</li>
                                    <li>PRIMARY</li>
                                    <li>KEY</li>
                                    <li>FOREIGN</li>
                                    <li>REFERENCES</li>
                                    <li>VALUES</li>
                                    <li>DEFAULT</li>
                                    <li>NULL</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples de conflits courants</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ PROBLÉMATIQUES :</span>
<span class="sql-identifier">user</span>       <span class="sql-comment">-- Réservé dans certains SGBD</span>
<span class="sql-identifier">group</span>      <span class="sql-comment">-- Clause GROUP BY</span>
<span class="sql-identifier">order</span>      <span class="sql-comment">-- Clause ORDER BY</span>
<span class="sql-identifier">date</span>       <span class="sql-comment">-- Type de données DATE</span>
<span class="sql-identifier">timestamp</span>  <span class="sql-comment">-- Type de données TIMESTAMP</span>
<span class="sql-identifier">desc</span>      <span class="sql-comment">-- Mot-clé DESC</span>
<span class="sql-identifier">key</span>       <span class="sql-comment">-- Mot-clé KEY</span>
<span class="sql-identifier">value</span>     <span class="sql-comment">-- Risque de confusion</span>
<span class="sql-identifier">check</span>     <span class="sql-comment">-- Contrainte CHECK</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques de nommage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques de Nommage</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Règles générales</h3>
                    <ul>
                        <li><strong>Utiliser des noms explicites</strong> plutôt que des mots génériques</li>
                        <li><strong>Préfixer les noms</strong> pour éviter les conflits</li>
                        <li><strong>Utiliser le pluriel</strong> pour les noms de tables</li>
                        <li><strong>Éviter les abréviations</strong> ambiguës</li>
                        <li><strong>Rester cohérent</strong> dans toute la base</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples de bonnes pratiques</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>❌ À éviter</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-identifier">user</span>
<span class="sql-identifier">group</span>
<span class="sql-identifier">order</span>
<span class="sql-identifier">date</span>
<span class="sql-identifier">desc</span>
<span class="sql-identifier">key</span>
<span class="sql-identifier">value</span></code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>✅ Recommandé</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-identifier">utilisateur</span>
<span class="sql-identifier">groupe_utilisateurs</span>
<span class="sql-identifier">commande</span>
<span class="sql-identifier">date_creation</span>
<span class="sql-identifier">description</span>
<span class="sql-identifier">cle_primaire</span>
<span class="sql-identifier">valeur_parametre</span></code></pre>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Exemples complets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples Complets avec Mots Réservés</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Création de tables avec mots réservés</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ✅ CORRECT : Avec guillemets (MySQL)</span>
<span class="sql-reserved">CREATE TABLE</span> `<span class="sql-identifier">order</span>` (
  `<span class="sql-identifier">id</span>` <span class="sql-type">INT</span> <span class="sql-reserved">PRIMARY KEY</span> <span class="sql-reserved">AUTO_INCREMENT</span>,
  `<span class="sql-identifier">date</span>` <span class="sql-type">DATE</span> <span class="sql-reserved">NOT NULL</span>,
  `<span class="sql-identifier">desc</span>` <span class="sql-type">TEXT</span>,
  `<span class="sql-identifier">group</span>` <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  `<span class="sql-identifier">check</span>` <span class="sql-type">BOOLEAN</span> <span class="sql-reserved">DEFAULT</span> <span class="sql-number">FALSE</span>
);

<span class="sql-comment">-- ✅ CORRECT : Sans mots réservés (MEILLEUR CHOIX)</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span> <span class="sql-reserved">PRIMARY KEY</span> <span class="sql-reserved">AUTO_INCREMENT</span>,
  <span class="sql-identifier">date_commande</span> <span class="sql-type">DATE</span> <span class="sql-reserved">NOT NULL</span>,
  <span class="sql-identifier">description</span> <span class="sql-type">TEXT</span>,
  <span class="sql-identifier">groupe_commande</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  <span class="sql-identifier">est_verifie</span> <span class="sql-type">BOOLEAN</span> <span class="sql-reserved">DEFAULT</span> <span class="sql-number">FALSE</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Requêtes avec tables contenant des mots réservés</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ✅ CORRECT : Utilisation cohérente des guillemets</span>
<span class="sql-reserved">INSERT INTO</span> `<span class="sql-identifier">order</span>` (
  `<span class="sql-identifier">date</span>`,
  `<span class="sql-identifier">desc</span>`,
  `<span class="sql-identifier">group</span>`,
  `<span class="sql-identifier">check</span>`
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'2024-01-20'</span>,
  <span class="sql-string">'Commande importante'</span>,
  <span class="sql-string">'VIP'</span>,
  <span class="sql-number">TRUE</span>
);

<span class="sql-reserved">SELECT</span> `<span class="sql-identifier">id</span>`, `<span class="sql-identifier">date</span>`, `<span class="sql-identifier">desc</span>`
<span class="sql-reserved">FROM</span> `<span class="sql-identifier">order</span>`
<span class="sql-reserved">WHERE</span> `<span class="sql-identifier">group</span>` <span class="sql-operator">=</span> <span class="sql-string">'VIP'</span>
<span class="sql-reserved">ORDER BY</span> `<span class="sql-identifier">date</span>` <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Solutions alternatives -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Solutions Alternatives Recommandées</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser des synonymes ou préfixes</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Mots réservés problématiques</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-identifier">user</span>
<span class="sql-identifier">group</span>
<span class="sql-identifier">order</span>
<span class="sql-identifier">key</span>
<span class="sql-identifier">value</span>
<span class="sql-identifier">date</span>
<span class="sql-identifier">desc</span>
<span class="sql-identifier">check</span></code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>Alternatives recommandées</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-identifier">utilisateur</span>, <span class="sql-identifier">membre</span>, <span class="sql-identifier">client</span>
<span class="sql-identifier">groupe</span>, <span class="sql-identifier">categorie</span>, <span class="sql-identifier">equipe</span>
<span class="sql-identifier">commande</span>, <span class="sql-identifier">achat</span>, <span class="sql-identifier">transaction</span>
<span class="sql-identifier">cle</span>, <span class="sql-identifier">identifiant</span>, <span class="sql-identifier">code</span>
<span class="sql-identifier">valeur</span>, <span class="sql-identifier">contenu</span>, <span class="sql-identifier">donnee</span>
<span class="sql-identifier">date_creation</span>, <span class="sql-identifier">date_debut</span>, <span class="sql-identifier">timestamp</span>
<span class="sql-identifier">description</span>, <span class="sql-identifier">commentaire</span>, <span class="sql-identifier">details</span>
<span class="sql-identifier">verification</span>, <span class="sql-identifier">controle</span>, <span class="sql-identifier">validation</span></code></pre>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple de schéma bien conçu</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ✅ SCHÉMA OPTIMAL : Aucun mot réservé</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">utilisateurs</span> (
  <span class="sql-identifier">utilisateur_id</span> <span class="sql-type">INT</span> <span class="sql-reserved">PRIMARY KEY</span> <span class="sql-reserved">AUTO_INCREMENT</span>,
  <span class="sql-identifier">nom_utilisateur</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>) <span class="sql-reserved">NOT NULL</span>,
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-reserved">UNIQUE</span>,
  <span class="sql-identifier">date_creation</span> <span class="sql-type">DATETIME</span> <span class="sql-reserved">DEFAULT</span> <span class="sql-function">CURRENT_TIMESTAMP</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span> <span class="sql-reserved">PRIMARY KEY</span> <span class="sql-reserved">AUTO_INCREMENT</span>,
  <span class="sql-identifier">utilisateur_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date_commande</span> <span class="sql-type">DATE</span> <span class="sql-reserved">NOT NULL</span>,
  <span class="sql-identifier">montant_total</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>),
  <span class="sql-identifier">statut_commande</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">20</span>) <span class="sql-reserved">DEFAULT</span> <span class="sql-string">'en_attente'</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">utilisateur_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">utilisateurs</span>(<span class="sql-identifier">utilisateur_id</span>)
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">produits</span> (
  <span class="sql-identifier">produit_id</span> <span class="sql-type">INT</span> <span class="sql-reserved">PRIMARY KEY</span> <span class="sql-reserved">AUTO_INCREMENT</span>,
  <span class="sql-identifier">nom_produit</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-reserved">NOT NULL</span>,
  <span class="sql-identifier">description_produit</span> <span class="sql-type">TEXT</span>,
  <span class="sql-identifier">prix_unitaire</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">8</span>, <span class="sql-number">2</span>),
  <span class="sql-identifier">categorie_id</span> <span class="sql-type">INT</span>
);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Détection et prévention -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Détection et Prévention</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Comment vérifier si un mot est réservé</h3>
                    <ul>
                        <li><strong>Consulter la documentation officielle</strong> de votre SGBD</li>
                        <li><strong>Utiliser des outils de validation</strong> de schéma</li>
                        <li><strong>Tester les noms</strong> dans une requête simple</li>
                        <li><strong>Vérifier les erreurs de syntaxe</strong> lors du développement</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Test rapide de validation</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Testez votre nom de table avec cette requête</span>
<span class="sql-reserved">SELECT</span> <span class="sql-number">1</span> <span class="sql-reserved">FROM</span> `<span class="sql-identifier">votre_nom_de_table</span>` <span class="sql-reserved">WHERE</span> <span class="sql-number">1</span> <span class="sql-operator">=</span> <span class="sql-number">0</span>;

<span class="sql-comment">-- Si cette requête échoue, le nom est probablement un mot réservé</span>
<span class="sql-comment">-- ou la table n'existe pas encore</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Outils de validation</h3>
                    <ul>
                        <li><strong>MySQL Workbench</strong> : Coloration syntaxique et validation</li>
                        <li><strong>phpMyAdmin</strong> : Détection d'erreurs lors de l'exécution</li>
                        <li><strong>Extensions IDE</strong> : Visual Studio Code, PHPStorm, etc.</li>
                        <li><strong>Validateurs en ligne</strong> : SQL Fiddle, DB Fiddle</li>
                    </ul>
                </div>
            </section>

            <!-- Cas pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas Pratiques et Migrations</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Migration d'une base existante</h3>
                    <p>Si vous héritez d'une base avec des mots réservés :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Ancienne table avec mots réservés</span>
<span class="sql-reserved">CREATE TABLE</span> `<span class="sql-identifier">user</span>` (
  `<span class="sql-identifier">id</span>` <span class="sql-type">INT</span>,
  `<span class="sql-identifier">group</span>` <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  `<span class="sql-identifier">desc</span>` <span class="sql-type">TEXT</span>
);

<span class="sql-comment">-- Migration vers de meilleurs noms</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">utilisateurs</span> (
  <span class="sql-identifier">utilisateur_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">groupe_utilisateur</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  <span class="sql-identifier">description</span> <span class="sql-type">TEXT</span>
);

<span class="sql-comment">-- Copie des données</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">utilisateurs</span> (
  <span class="sql-identifier">utilisateur_id</span>,
  <span class="sql-identifier">groupe_utilisateur</span>,
  <span class="sql-identifier">description</span>
)
<span class="sql-reserved">SELECT</span>
  `<span class="sql-identifier">id</span>`,
  `<span class="sql-identifier">group</span>`,
  `<span class="sql-identifier">desc</span>`
<span class="sql-reserved">FROM</span> `<span class="sql-identifier">user</span>`;

<span class="sql-comment">-- Suppression de l'ancienne table (après vérification)</span>
<span class="sql-reserved">DROP TABLE</span> `<span class="sql-identifier">user</span>`;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Correction de schéma</h3>
                    <p>Corrigez ce schéma problématique contenant des mots réservés :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Schéma à corriger :</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">user</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">group</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  <span class="sql-identifier">order</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date</span> <span class="sql-type">DATE</span>,
  <span class="sql-identifier">desc</span> <span class="sql-type">TEXT</span>,
  <span class="sql-identifier">check</span> <span class="sql-type">BOOLEAN</span>
);</code></pre>
                    </div>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- SOLUTION 1 : Avec guillemets (solution temporaire)</span>
<span class="sql-reserved">CREATE TABLE</span> `<span class="sql-identifier">user</span>` (
  `<span class="sql-identifier">id</span>` <span class="sql-type">INT</span>,
  `<span class="sql-identifier">group</span>` <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  `<span class="sql-identifier">order</span>` <span class="sql-type">INT</span>,
  `<span class="sql-identifier">date</span>` <span class="sql-type">DATE</span>,
  `<span class="sql-identifier">desc</span>` <span class="sql-type">TEXT</span>,
  `<span class="sql-identifier">check</span>` <span class="sql-type">BOOLEAN</span>
);

<span class="sql-comment">-- SOLUTION 2 : Meilleurs noms (recommandé)</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">utilisateurs</span> (
  <span class="sql-identifier">utilisateur_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">groupe_utilisateur</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  <span class="sql-identifier">ordre_affichage</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date_creation</span> <span class="sql-type">DATE</span>,
  <span class="sql-identifier">description</span> <span class="sql-type">TEXT</span>,
  <span class="sql-identifier">est_verifie</span> <span class="sql-type">BOOLEAN</span>
);</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Requêtes avec mots réservés</h3>
                    <p>Écrivez des requêtes pour une table "order" avec des colonnes "date" et "desc" :</p>
                    <ul>
                        <li>Sélectionner toutes les commandes</li>
                        <li>Insérer une nouvelle commande</li>
                        <li>Mettre à jour la description d'une commande</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Sélectionner toutes les commandes</span>
<span class="sql-reserved">SELECT</span> `<span class="sql-identifier">id</span>`, `<span class="sql-identifier">date</span>`, `<span class="sql-identifier">desc</span>`
<span class="sql-reserved">FROM</span> `<span class="sql-identifier">order</span>`
<span class="sql-reserved">ORDER BY</span> `<span class="sql-identifier">date</span>` <span class="sql-reserved">DESC</span>;

<span class="sql-comment">-- Insérer une nouvelle commande</span>
<span class="sql-reserved">INSERT INTO</span> `<span class="sql-identifier">order</span>` (
  `<span class="sql-identifier">date</span>`,
  `<span class="sql-identifier">desc</span>`
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'2024-01-20'</span>,
  <span class="sql-string">'Nouvelle commande client'</span>
);

<span class="sql-comment">-- Mettre à jour la description</span>
<span class="sql-reserved">UPDATE</span> `<span class="sql-identifier">order</span>`
<span class="sql-reserved">SET</span> `<span class="sql-identifier">desc</span>` <span class="sql-operator">=</span> <span class="sql-string">'Description mise à jour'</span>
<span class="sql-reserved">WHERE</span> `<span class="sql-identifier">id</span>` <span class="sql-operator">=</span> <span class="sql-number">1</span>;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Checklist et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Checklist et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Checklist de validation</h3>
                    <ul>
                        <li>✅ <strong>Vérifier</strong> que les noms ne sont pas des mots réservés</li>
                        <li>✅ <strong>Utiliser des guillemets</strong> si nécessaire (backticks pour MySQL)</li>
                        <li>✅ <strong>Préférer des noms explicites</strong> sans mots réservés</li>
                        <li>✅ <strong>Rester cohérent</strong> dans l'utilisation des guillemets</li>
                        <li>✅ <strong>Tester les requêtes</strong> avec les noms choisis</li>
                        <li>✅ <strong>Documenter les choix</strong> de nommage</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Recommandations finales</h3>
                    <ul>
                        <li><strong>Évitez complètement les mots réservés</strong> dans les nouveaux projets</li>
                        <li><strong>Utilisez des guillemets uniquement</strong> pour la maintenance d'anciennes bases</li>
                        <li><strong>Adoptez une convention de nommage</strong> cohérente</li>
                        <li><strong>Formez votre équipe</strong> aux bonnes pratiques</li>
                        <li><strong>Utilisez des outils de validation</strong> automatique</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">En résumé</h3>
                    <p>
                        Les mots réservés SQL peuvent causer des erreurs frustrantes, mais elles sont facilement évitables.
                        La meilleure pratique est de concevoir vos schémas avec des noms explicites qui n'utilisent pas
                        de mots réservés. Lorsque vous travaillez avec des bases existantes, utilisez les guillemets
                        appropriés à votre SGBD.
                    </p>
                    <p class="success-text">
                        <strong>Règle d'or : Préférez toujours "utilisateurs" à "user", "commandes" à "order", 
                        et "description" à "desc".</strong>
                    </p>
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

/* COULEURS SQL */
.sql-reserved {
    color: #FF6B8B !important;
    font-weight: bold;
}

.sql-keyword {
    color: #4FC1FF !important;
}

.sql-identifier {
    color: #9CDCFE !important;
}

.sql-type {
    color: #4EC9B0 !important;
}

.sql-string {
    color: #CE9178 !important;
}

.sql-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.sql-function {
    color: #DCDCAA !important;
}

.sql-number {
    color: #B5CEA8 !important;
}

.sql-constant {
    color: #569CD6 !important;
}

.sql-operator {
    color: #D4D4D4 !important;
}

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
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