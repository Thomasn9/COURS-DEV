<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">LEFT JOIN et RIGHT JOIN en SQL</h1>
                <p class="lesson-meta text-white">SQL • MySQL • Jointures externes • Données optionnelles</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Jointures Externes</h2>
                <p class="textExemple">
                    Les LEFT JOIN et RIGHT JOIN sont des jointures externes qui permettent d'inclure toutes les lignes
                    d'une table,
                    même si elles n'ont pas de correspondance dans l'autre table. Elles sont essentielles pour analyser
                    des données incomplètes.
                </p>
                <p class="textExemple">
                    Contrairement aux INNER JOIN qui retournent uniquement les correspondances, les jointures externes
                    préservent
                    toutes les lignes d'une table "principale" et ajoutent les données correspondantes de l'autre table.
                </p>
            </section>

            <!-- Concepts fondamentaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts Fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Comment fonctionnent les jointures externes</h3>
                    <ul>
                        <li><strong>LEFT JOIN</strong> : Toutes les lignes de la table de gauche + correspondances de
                            droite</li>
                        <li><strong>RIGHT JOIN</strong> : Toutes les lignes de la table de droite + correspondances de
                            gauche</li>
                        <li><strong>Valeurs NULL</strong> : Les colonnes sans correspondance contiennent NULL</li>
                        <li><strong>Table principale</strong> : La table dont toutes les lignes sont conservées</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement LEFT JOIN</h3>
                    <div class="code-example">
                        <pre><code>Table A (clients)     LEFT JOIN     Table B (commandes)
┌─────────────┐                     ┌──────────────┐
│ id │ nom    │                     │ id │ client_id │
├─────────────┤                     ├──────────────┤
│ 1  │ Alice  │ ────────┐           │ 101│ 1         │
│ 2  │ Bob    │         │ ┌───────→ │ 102│ 1         │
│ 3  │ Charlie│ ────┐   │ │         │ 103│ 4         │
│ 4  │ David  │     │   │ │         └──────────────┘
└─────────────┘     │   │ │
                    │   │ │
Résultat LEFT JOIN  │   │ │
┌─────────────────────────┐ │ │
│ nom    │ commande_id    │ │ │
├─────────────────────────┤ │ │
│ Alice  │ 101            │←┘ │
│ Alice  │ 102            │←──┘
│ Bob    │ NULL           │←── Tous les clients conservés!
│ Charlie│ NULL           │
│ David  │ NULL           │
└─────────────────────────┘</code></pre>
                    </div>
                </div>
            </section>

            <!-- Pourquoi éviter RIGHT JOIN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple"> Pourquoi éviter RIGHT JOIN (mauvaise pratique)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Le problème avec RIGHT JOIN</h3>
                    <p>
                        Bien que RIGHT JOIN soit fonctionnellement équivalent à LEFT JOIN, son utilisation est
                        considérée comme une
                        <strong>mauvaise pratique</strong> pour des raisons de lisibilité et de maintenance.
                    </p>

                    <div class="warning-section">
                        <h4 class="text-purple"> RIGHT JOIN - Déconseillé</h4>
                        <div class="code-comparison">
                            <div>
                                <h5>Mauvaise pratique (RIGHT JOIN)</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-comment">-- Difficile à lire: quelle est la table principale?</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span>
<span class="sql-reserved">RIGHT JOIN</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>;
<span class="sql-comment">-- La table principale est à droite, contre-intuitif!</span></code></pre>
                                </div>
                                <p class="warning-text"> Lecture contre-intuitive, difficile à maintenir</p>
                            </div>
                            <div>
                                <h5>Bonne pratique (LEFT JOIN équivalent)</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-comment">-- Clair: clients est la table principale</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>;
<span class="sql-comment">-- Lecture naturelle de gauche à droite</span></code></pre>
                                </div>
                                <p class="success-text">Logique claire, facile à comprendre</p>
                            </div>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple"> Problèmes avec RIGHT JOIN</h4>
                        <ul>
                            <li><strong>Lisibilité réduite</strong> : La lecture de gauche à droite est naturelle, RIGHT
                                JOIN inverse cette logique</li>
                            <li><strong>Maintenance difficile</strong> : Les développeurs doivent "inverser mentalement"
                                la logique</li>
                            <li><strong>Inconsistance</strong> : Mélanger LEFT et RIGHT JOIN dans une même requête crée
                                de la confusion</li>
                            <li><strong>Standard industriel</strong> : La communauté SQL préfère largement LEFT JOIN
                            </li>
                        </ul>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple"> Exemple de confusion avec RIGHT JOIN</h4>
                        <div class="code-example">
                            <pre><code><span class="sql-comment">--  Requête complexe avec RIGHT JOIN - Difficile à comprendre</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom_produit</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span>
<span class="sql-reserved">RIGHT JOIN</span> <span class="sql-identifier">details_commande</span> <span class="sql-identifier">dc</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">produit_id</span>
<span class="sql-reserved">RIGHT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">commande_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span>;
<span class="sql-comment">--  Quelle est la table principale? Difficile à suivre!</span>

<span class="sql-comment">-- Version équivalente avec LEFT JOIN - Beaucoup plus claire</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom_produit</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">details_commande</span> <span class="sql-identifier">dc</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">commande_id</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span>;
<span class="sql-comment">-- Logique claire: commandes est la table principale</span></code></pre>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">Avantages des LEFT JOIN</h4>
                        <ul>
                            <li><strong>Lisibilité optimale</strong> : Lecture naturelle de gauche à droite</li>
                            <li><strong>Consistance</strong> : Toutes les jointures suivent la même logique</li>
                            <li><strong>Maintenance facilitée</strong> : Les développeurs comprennent rapidement la
                                logique</li>
                            <li><strong>Standard industriel</strong> : Adopté par la majorité des équipes SQL</li>
                        </ul>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Cas d'usage très rares pour RIGHT JOIN</h3>
                    <ul>
                        <li>Migration d'ancien code legacy qu'on ne peut pas modifier</li>
                        <li>Requêtes très spécifiques où la logique RIGHT est plus naturelle (rare)</li>
                        <li>Environnements avec des conventions d'équipe spécifiques</li>
                    </ul>
                    <p><strong>En pratique, utilisez TOUJOURS LEFT JOIN à la place de RIGHT JOIN !</strong></p>
                </div>
            </section>

            <!-- Syntaxe LEFT JOIN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe et Utilisation de LEFT JOIN</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe de base</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">SELECT</span> <span class="sql-identifier">colonnes</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">table_principale</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">table_secondaire</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">table_principale</span>.<span class="sql-identifier">colonne</span> <span class="sql-operator">=</span> <span class="sql-identifier">table_secondaire</span>.<span class="sql-identifier">colonne</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple fondamental</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Tous les clients, même ceux sans commande</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Résultat typique</h3>
                    <div class="code-example">
                        <pre><code>┌───────────┬──────────┬──────────┬─────────────┬──────────────┬─────────┐
│ client_id │ nom      │ prenom   │ commande_id │ date_commande│ montant │
├───────────┼──────────┼──────────┼─────────────┼──────────────┼─────────┤
│ 1         │ Dupont   │ Jean     │ 101         │ 2024-01-15   │ 150.00  │
│ 1         │ Dupont   │ Jean     │ 102         │ 2024-02-20   │ 200.00  │
│ 2         │ Martin   │ Marie    │ NULL        │ NULL         │ NULL    │ ← Client sans commande
│ 3         │ Bernard  │ Pierre   │ 103         │ 2024-01-10   │ 75.50   │
│ 4         │ Dubois   │ Anne     │ NULL        │ NULL         │ NULL    │ ← Client sans commande
└───────────┴──────────┴──────────┴─────────────┴──────────────┴─────────┘</code></pre>
                    </div>
                </div>
            </section>

            <!-- Cas d'usage LEFT JOIN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas d'Usage Pratiques de LEFT JOIN</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Analyse des clients inactifs</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Clients qui n'ont jamais passé commande</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">email</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">date_inscription</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span> <span class="sql-keyword">IS NULL</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Produits jamais vendus</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Produits qui n'ont jamais été commandés</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">prix</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">stock</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">details_commande</span> <span class="sql-identifier">dc</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">produit_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">detail_id</span> <span class="sql-keyword">IS NULL</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Employés sans manager (hiérarchie plate)</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Employés qui n'ont pas de manager (top de la hiérarchie)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">e</span>.<span class="sql-identifier">employe_id</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">poste</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">e</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">m</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">manager_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">m</span>.<span class="sql-identifier">employe_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">m</span>.<span class="sql-identifier">employe_id</span> <span class="sql-keyword">IS NULL</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- LEFT JOIN multiples -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">LEFT JOIN Multiples</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Chaînage de LEFT JOIN</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Tous les clients avec leurs commandes et produits (si existants)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom_produit</span>,
  <span class="sql-identifier">dc</span>.<span class="sql-identifier">quantite</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">details_commande</span> <span class="sql-identifier">dc</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">commande_id</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de relations</h3>
                    <div class="code-example">
                        <pre><code>clients (tous) ────┐
                   │ LEFT JOIN
commandes (optionnel) ────┐
                          │ LEFT JOIN
details_commande (optionnel) ────┐
                                 │ LEFT JOIN
produits (optionnel)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conditions avec LEFT JOIN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conditions Avancées avec LEFT JOIN</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Filtrage des résultats</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Clients avec commandes récentes OU aucun historique</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span> <span class="sql-operator">>=</span> <span class="sql-string">'2024-01-01'</span>  <span class="sql-comment">-- Filtre dans le JOIN</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">ville</span> <span class="sql-operator">=</span> <span class="sql-string">'Paris'</span>;</code></pre>
                    </div>
                    <p><strong>Attention</strong> : Le filtre dans ON vs WHERE donne des résultats différents!</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Différence ON vs WHERE</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Filtre dans ON</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span> <span class="sql-operator">></span> <span class="sql-number">100</span></code></pre>
                            </div>
                            <p>→ Tous les clients + seulement leurs commandes > 100€</p>
                        </div>
                        <div>
                            <h5>Filtre dans WHERE</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span> <span class="sql-operator">></span> <span class="sql-number">100</span>
  <span class="sql-reserved">OR</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span> <span class="sql-keyword">IS NULL</span></code></pre>
                            </div>
                            <p>→ Clients avec commandes > 100€ OU sans commandes</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Agrégations avec LEFT JOIN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Agrégations avec LEFT JOIN</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Calculs incluant les données manquantes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- CA par client (incluant les clients sans commande)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'nb_commandes'</span>,
  <span class="sql-function">COALESCE</span>(<span class="sql-function">SUM</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>), <span class="sql-number">0</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'chiffre_affaires'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-string">'chiffre_affaires'</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation de COALESCE</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Statistiques produits avec remplacement des NULL</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span>,
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-function">COALESCE</span>(<span class="sql-function">SUM</span>(<span class="sql-identifier">dc</span>.<span class="sql-identifier">quantite</span>), <span class="sql-number">0</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'quantite_vendue'</span>,
  <span class="sql-function">COALESCE</span>(<span class="sql-function">COUNT</span>(<span class="sql-identifier">dc</span>.<span class="sql-identifier">detail_id</span>), <span class="sql-number">0</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'nb_ventes'</span>,
  <span class="sql-function">CASE</span> 
    <span class="sql-reserved">WHEN</span> <span class="sql-function">SUM</span>(<span class="sql-identifier">dc</span>.<span class="sql-identifier">quantite</span>) <span class="sql-keyword">IS NULL</span> <span class="sql-reserved">THEN</span> <span class="sql-string">'Non vendu'</span>
    <span class="sql-reserved">ELSE</span> <span class="sql-string">'Vendu'</span>
  <span class="sql-reserved">END</span> <span class="sql-reserved">AS</span> <span class="sql-string">'statut'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">details_commande</span> <span class="sql-identifier">dc</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">produit_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">produit_id</span>, <span class="sql-identifier">p</span>.<span class="sql-identifier">nom</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exemple complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple Complet : Analyse Commerciale</h2>

                <div class="textExemple">
                    <p>Requête complète d'analyse commerciale avec LEFT JOIN :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Analyse complète des clients et leur comportement d'achat</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">ville</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">date_inscription</span>,
  
  <span class="sql-comment">-- Statistiques commandes</span>
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'total_commandes'</span>,
  <span class="sql-function">COALESCE</span>(<span class="sql-function">SUM</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>), <span class="sql-number">0</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'chiffre_affaires'</span>,
  <span class="sql-function">COALESCE</span>(<span class="sql-function">AVG</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>), <span class="sql-number">0</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'panier_moyen'</span>,
  
  <span class="sql-comment">-- Dernière commande</span>
  <span class="sql-function">MAX</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'derniere_commande'</span>,
  
  <span class="sql-comment">-- Catégorie client</span>
  <span class="sql-function">CASE</span> 
    <span class="sql-reserved">WHEN</span> <span class="sql-function">COUNT</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span>) <span class="sql-operator">=</span> <span class="sql-number">0</span> <span class="sql-reserved">THEN</span> <span class="sql-string">'Prospect'</span>
    <span class="sql-reserved">WHEN</span> <span class="sql-function">COUNT</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">commande_id</span>) <span class="sql-operator">=</span> <span class="sql-number">1</span> <span class="sql-reserved">THEN</span> <span class="sql-string">'Nouveau'</span>
    <span class="sql-reserved">WHEN</span> <span class="sql-function">SUM</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>) <span class="sql-operator">></span> <span class="sql-number">1000</span> <span class="sql-reserved">THEN</span> <span class="sql-string">'VIP'</span>
    <span class="sql-reserved">ELSE</span> <span class="sql-string">'Régulier'</span>
  <span class="sql-reserved">END</span> <span class="sql-reserved">AS</span> <span class="sql-string">'categorie_client'</span>

<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span> <span class="sql-operator">>=</span> <span class="sql-function">DATE_SUB</span>(<span class="sql-function">CURDATE</span>(), <span class="sql-reserved">INTERVAL</span> <span class="sql-number">1</span> <span class="sql-keyword">YEAR</span>)
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">client_id</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">ville</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">date_inscription</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-string">'chiffre_affaires'</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Analyse des Relations</h3>
                    <p>Avec les tables : departements, employes, projets (employe_id = chef_projet)</p>
                    <ul>
                        <li>Lister tous les départements avec le nombre d'employés (même les départements vides)</li>
                        <li>Trouver les employés qui ne sont chefs d'aucun projet</li>
                        <li>Afficher les départements sans employés</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Départements avec nombre d'employés</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">d</span>.<span class="sql-identifier">nom_departement</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">e</span>.<span class="sql-identifier">employe_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'nb_employes'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">departements</span> <span class="sql-identifier">d</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">e</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">d</span>.<span class="sql-identifier">departement_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">departement_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">d</span>.<span class="sql-identifier">departement_id</span>, <span class="sql-identifier">d</span>.<span class="sql-identifier">nom_departement</span>;

<span class="sql-comment">-- Employés non chefs de projet</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">e</span>.<span class="sql-identifier">employe_id</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">poste</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">e</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">projets</span> <span class="sql-identifier">p</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">employe_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">chef_projet_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">projet_id</span> <span class="sql-keyword">IS NULL</span>;

<span class="sql-comment">-- Départements sans employés</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">d</span>.<span class="sql-identifier">departement_id</span>,
  <span class="sql-identifier">d</span>.<span class="sql-identifier">nom_departement</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">departements</span> <span class="sql-identifier">d</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">e</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">d</span>.<span class="sql-identifier">departement_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">departement_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">employe_id</span> <span class="sql-keyword">IS NULL</span>;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Système Académique</h3>
                    <p>Avec les tables : etudiants, cours, inscriptions, notes</p>
                    <ul>
                        <li>Lister tous les étudiants avec leurs cours et notes (même ceux non inscrits)</li>
                        <li>Trouver les cours sans aucun étudiant inscrit</li>
                        <li>Afficher la moyenne générale par étudiant (incluant ceux sans notes)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Étudiants avec cours et notes</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">e</span>.<span class="sql-identifier">etudiant_id</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">titre_cours</span>,
  <span class="sql-identifier">n</span>.<span class="sql-identifier">note</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">etudiants</span> <span class="sql-identifier">e</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">inscriptions</span> <span class="sql-identifier">i</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">etudiant_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">etudiant_id</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">cours</span> <span class="sql-identifier">c</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">cours_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">cours_id</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">notes</span> <span class="sql-identifier">n</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">inscription_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">n</span>.<span class="sql-identifier">inscription_id</span>;

<span class="sql-comment">-- Cours sans étudiants</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">cours_id</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">titre_cours</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">credits</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">cours</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">inscriptions</span> <span class="sql-identifier">i</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">cours_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">cours_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">inscription_id</span> <span class="sql-keyword">IS NULL</span>;

<span class="sql-comment">-- Moyenne générale par étudiant</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">e</span>.<span class="sql-identifier">etudiant_id</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">e</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-function">COALESCE</span>(<span class="sql-function">AVG</span>(<span class="sql-identifier">n</span>.<span class="sql-identifier">note</span>), <span class="sql-number">0</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'moyenne_generale'</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">n</span>.<span class="sql-identifier">note_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'nb_notes'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">etudiants</span> <span class="sql-identifier">e</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">inscriptions</span> <span class="sql-identifier">i</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">etudiant_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">etudiant_id</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">notes</span> <span class="sql-identifier">n</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">i</span>.<span class="sql-identifier">inscription_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">n</span>.<span class="sql-identifier">inscription_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">e</span>.<span class="sql-identifier">etudiant_id</span>, <span class="sql-identifier">e</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">e</span>.<span class="sql-identifier">prenom</span>;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation des LEFT JOIN</h3>
                    <ul>
                        <li><strong>Préférez LEFT JOIN à RIGHT JOIN</strong> pour une meilleure lisibilité</li>
                        <li><strong>Utilisez COALESCE</strong> pour gérer les valeurs NULL dans les agrégations</li>
                        <li><strong>Documentez la logique</strong> quand vous filtrez sur des colonnes NULL</li>
                        <li><strong>Testez les performances</strong> sur les grandes tables</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance et optimisation</h3>
                    <ul>
                        <li><strong>Indexez les colonnes de jointure</strong> pour améliorer les performances</li>
                        <li><strong>Évitez les LEFT JOIN inutiles</strong> si vous n'avez pas besoin des données
                            optionnelles</li>
                        <li><strong>Utilisez WHERE IS NULL avec prudence</strong> - cela peut être coûteux</li>
                        <li><strong>Limitez le dataset</strong> avec des conditions WHERE avant les LEFT JOIN</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Lisibilité et maintenance</h3>
                    <ul>
                        <li><strong>Organisez les LEFT JOIN</strong> dans l'ordre logique des relations</li>
                        <li><strong>Utilisez des alias explicites</strong> pour les tables</li>
                        <li><strong>Commentez les LEFT JOIN complexes</strong> pour expliquer la logique métier</li>
                        <li><strong>Évitez de mélanger LEFT et RIGHT JOIN</strong> dans la même requête</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Les LEFT JOIN sont des outils essentiels pour analyser des données incomplètes et comprendre
                        les relations optionnelles entre les tables. Ils permettent de conserver toutes les lignes
                        d'une table principale tout en ajoutant les données correspondantes de l'autre table.
                    </p>
                    <p>
                        <strong>Rappel crucial</strong> : Évitez les RIGHT JOIN et utilisez toujours LEFT JOIN
                        pour une meilleure lisibilité et maintenabilité de vos requêtes SQL.
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

/* COULEURS MYSQL WORKBENCH POUR SQL */
.sql-reserved {
    color: #FF6B8B !important;
    font-weight: bold;
}

/* Mots réservés */
.sql-keyword {
    color: #4FC1FF !important;
}

/* Mots-clés */
.sql-identifier {
    color: #9CDCFE !important;
}

/* Identifiants */
.sql-type {
    color: #4EC9B0 !important;
}

/* Types de données */
.sql-string {
    color: #CE9178 !important;
}

/* Chaînes de caractères */
.sql-comment {
    color: #6A9955 !important;
    font-style: italic;
}

/* Commentaires */
.sql-function {
    color: #DCDCAA !important;
}

/* Fonctions SQL */
.sql-number {
    color: #B5CEA8 !important;
}

/* Nombres */
.sql-constant {
    color: #569CD6 !important;
}

/* Constantes */
.sql-operator {
    color: #D4D4D4 !important;
}

/* Opérateurs */

/* Styles pour la section d'avertissement */
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