<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Requêtes SELECT en SQL</h1>
                <p class="lesson-meta text-white">SQL • MySQL • Interrogation de données</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Requêtes SELECT</h2>
                <p class="textExemple">
                    La commande SELECT est la pierre angulaire de SQL. Elle permet d'interroger une base de données
                    pour récupérer des données spécifiques à partir d'une ou plusieurs tables.
                </p>
                <p class="textExemple">
                    SELECT est utilisé dans la majorité des opérations de lecture et constitue l'outil principal
                    pour extraire et analyser les informations stockées.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de Base</h2>

                <div class="textExemple">
                    <p>La structure fondamentale d'une requête SELECT est :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">SELECT</span> <span class="sql-identifier">colonne1</span>, <span class="sql-identifier">colonne2</span>, ...
<span class="sql-reserved">FROM</span> <span class="sql-identifier">nom_table</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples simples</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ À éviter : sélectionner toutes les colonnes</span>
<span class="sql-comment">-- SELECT * FROM clients;</span>

<span class="sql-comment">-- ✅ Bonne pratique : sélectionner des colonnes spécifiques</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">email</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>;

<span class="sql-comment">-- ✅ Sélectionner avec un alias</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Nom du client'</span>,
  <span class="sql-identifier">prenom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Prénom'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>;</code></pre>
                    </div>
                </div>
            </section>


            <!-- Clause WHERE -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Filtrer les Résultats avec WHERE</h2>

                <div class="textExemple">
                    <p>La clause WHERE permet de filtrer les enregistrements selon des conditions spécifiques :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">SELECT</span> <span class="sql-identifier">colonne1</span>, <span class="sql-identifier">colonne2</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">table</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">condition</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Opérateurs de comparaison</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Égalité</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> 
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">prix</span> <span class="sql-operator">=</span> <span class="sql-number">19.99</span>;

<span class="sql-comment">-- Inégalité</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> 
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">prix</span> <span class="sql-operator">!=</span> <span class="sql-number">0</span>;

<span class="sql-comment">-- Supérieur à</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">salaire</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span> 
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">salaire</span> <span class="sql-operator">></span> <span class="sql-number">30000</span>;

<span class="sql-comment">-- Entre deux valeurs</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> 
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">prix</span> <span class="sql-reserved">BETWEEN</span> <span class="sql-number">10</span> <span class="sql-reserved">AND</span> <span class="sql-number">50</span>;

<span class="sql-comment">-- Liste de valeurs</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">ville</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> 
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">ville</span> <span class="sql-reserved">IN</span> (<span class="sql-string">'Paris'</span>, <span class="sql-string">'Lyon'</span>, <span class="sql-string">'Marseille'</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Opérateurs logiques</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ET logique</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">date_commande</span>, <span class="sql-identifier">montant</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">statut</span> <span class="sql-operator">=</span> <span class="sql-string">'livrée'</span> 
  <span class="sql-reserved">AND</span> <span class="sql-identifier">montant</span> <span class="sql-operator">></span> <span class="sql-number">100</span>;

<span class="sql-comment">-- OU logique</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">pays</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">pays</span> <span class="sql-operator">=</span> <span class="sql-string">'France'</span> 
  <span class="sql-reserved">OR</span> <span class="sql-identifier">pays</span> <span class="sql-operator">=</span> <span class="sql-string">'Belgique'</span>;

<span class="sql-comment">-- Négation</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>, <span class="sql-identifier">disponible</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">WHERE</span> <span class="sql-reserved">NOT</span> <span class="sql-identifier">disponible</span> <span class="sql-operator">=</span> <span class="sql-constant">TRUE</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Pourquoi éviter SELECT * -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">⚠️ Pourquoi éviter SELECT *</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Le problème avec SELECT *</h3>
                    <p>
                        Bien que <code>SELECT *</code> soit pratique pour les tests rapides, son utilisation en
                        production
                        est considérée comme une <strong>mauvaise pratique</strong> pour plusieurs raisons :
                    </p>

                    <div class="warning-section">
                        <h4 class="text-purple">🚫 Inefficacité des performances</h4>
                        <div class="code-comparison">
                            <div>
                                <h5>Mauvaise pratique</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-reserved">SELECT</span> <span class="sql-keyword">*</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">ville</span> <span class="sql-operator">=</span> <span class="sql-string">'Paris'</span>;</code></pre>
                                </div>
                                <p class="warning-text">➡️ Transfère toutes les colonnes inutilement</p>
                            </div>
                            <div>
                                <h5>Bonne pratique</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">email</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">ville</span> <span class="sql-operator">=</span> <span class="sql-string">'Paris'</span>;</code></pre>
                                </div>
                                <p class="success-text">➡️ Transfère uniquement les colonnes nécessaires</p>
                            </div>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">📊 Impact sur les performances</h4>
                        <ul>
                            <li><strong>Réseau</strong> : Transfert de données inutiles entre la base de données et
                                l'application</li>
                            <li><strong>Mémoire</strong> : Consommation mémoire accrue pour stocker des colonnes non
                                utilisées</li>
                            <li><strong>Index</strong> : Impossible d'utiliser les index covering quand on sélectionne
                                toutes les colonnes</li>
                            <li><strong>Cache</strong> : Réduction de l'efficacité du cache de requêtes</li>
                        </ul>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">🔧 Problèmes de maintenance</h4>
                        <div class="code-example">
                            <pre><code><span class="sql-comment">-- Table originale</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">utilisateurs</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>),
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>)
);

<span class="sql-comment">-- Plus tard, ajout d'une colonne LOB (Large Object)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">ADD</span> <span class="sql-identifier">photo</span> <span class="sql-type">LONGBLOB</span>;</code></pre>
                        </div>
                        <p>
                            Si votre application utilise <code>SELECT *</code>, elle recevra automatiquement la colonne
                            <code>photo</code>
                            (potentiellement plusieurs Mo) même si elle n'en a pas besoin !
                        </p>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">🛡️ Problèmes de sécurité</h4>
                        <ul>
                            <li>Exposition accidentelle de données sensibles (mots de passe hashés, informations
                                personnelles)</li>
                            <li>Violation du principe de moindre privilège</li>
                            <li>Difficulté à auditer quelles données sont réellement utilisées</li>
                        </ul>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">✅ Quand utiliser SELECT * (rarement)</h3>
                    <ul>
                        <li>Débogage rapide pendant le développement</li>
                        <li>Requêtes ad-hoc pour exploration des données</li>
                        <li>Dans des sous-requêtes EXISTS où les colonnes ne sont pas importantes</li>
                    </ul>
                    <p><strong>En production, toujours spécifier les colonnes explicitement !</strong></p>
                </div>
            </section>

            <!-- Tri et limitation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Trier et Limiter les Résultats</h2>

                <div class="textExemple">
                    <h3 class="text-purple">ORDER BY - Trier les résultats</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Tri ascendant (par défaut)</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">salaire</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">salaire</span> <span class="sql-reserved">ASC</span>;

<span class="sql-comment">-- Tri descendant</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">salaire</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">salaire</span> <span class="sql-reserved">DESC</span>;

<span class="sql-comment">-- Tri multiple</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">ville</span>, <span class="sql-identifier">salaire</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">ville</span> <span class="sql-reserved">ASC</span>, <span class="sql-identifier">salaire</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">LIMIT - Limiter le nombre de résultats</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- 10 premiers résultats</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">LIMIT</span> <span class="sql-number">10</span>;

<span class="sql-comment">-- Pagination (5 résultats à partir du 11ème)</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">LIMIT</span> <span class="sql-number">10</span>, <span class="sql-number">5</span>;

<span class="sql-comment">-- Top 5 des produits les plus chers</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">prix</span> <span class="sql-reserved">DESC</span>
<span class="sql-reserved">LIMIT</span> <span class="sql-number">5</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Jointures -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Jointures entre Tables</h2>

                <div class="textExemple">
                    <p>Les jointures permettent de combiner des données de plusieurs tables :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- INNER JOIN (jointure interne)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>, 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">prenom</span>, 
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Types de jointures</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- LEFT JOIN (jointure gauche)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">co</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>
<span class="sql-reserved">LEFT JOIN</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span> <span class="sql-operator">=</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span>;

<span class="sql-comment">-- RIGHT JOIN (jointure droite)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom_categorie</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span>
<span class="sql-reserved">RIGHT JOIN</span> <span class="sql-identifier">categories</span> <span class="sql-identifier">c</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">categorie_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>;

<span class="sql-comment">-- Multiple JOIN</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">cl</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">pr</span>.<span class="sql-identifier">nom_produit</span>,
  <span class="sql-identifier">cat</span>.<span class="sql-identifier">nom_categorie</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">cl</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">cl</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">details_commande</span> <span class="sql-identifier">dc</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">id</span> <span class="sql-operator">=</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">commande_id</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">pr</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">dc</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">pr</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">categories</span> <span class="sql-identifier">cat</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">pr</span>.<span class="sql-identifier">categorie_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">cat</span>.<span class="sql-identifier">id</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Agrégations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fonctions d'Agrégation</h2>

                <div class="textExemple">
                    <p>Les fonctions d'agrégation effectuent des calculs sur un ensemble de lignes :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- COUNT : compter le nombre d'enregistrements</span>
<span class="sql-reserved">SELECT</span> <span class="sql-function">COUNT</span>(<span class="sql-keyword">*</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre de clients'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>;

<span class="sql-comment">-- SUM : somme des valeurs</span>
<span class="sql-reserved">SELECT</span> <span class="sql-function">SUM</span>(<span class="sql-identifier">montant</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Chiffre d affaires total'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>;

<span class="sql-comment">-- AVG : moyenne</span>
<span class="sql-reserved">SELECT</span> <span class="sql-function">AVG</span>(<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Prix moyen'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>;

<span class="sql-comment">-- MIN et MAX</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-function">MIN</span>(<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Prix minimum'</span>,
  <span class="sql-function">MAX</span>(<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Prix maximum'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">GROUP BY - Regroupement</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Nombre de commandes par client</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">client_id</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-keyword">*</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre de commandes'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">client_id</span>;

<span class="sql-comment">-- Chiffre d'affaires par ville</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">ville</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">co</span>.<span class="sql-identifier">montant</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'CA total'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">ville</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">HAVING - Filtre sur agrégation</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Clients avec plus de 5 commandes</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">client_id</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-keyword">*</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'nb_commandes'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">client_id</span>
<span class="sql-reserved">HAVING</span> <span class="sql-function">COUNT</span>(<span class="sql-keyword">*</span>) <span class="sql-operator">></span> <span class="sql-number">5</span>;

<span class="sql-comment">-- Villes avec un CA supérieur à 10 000€</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">ville</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">montant</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'CA_total'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">ville</span>
<span class="sql-reserved">HAVING</span> <span class="sql-function">SUM</span>(<span class="sql-identifier">montant</span>) <span class="sql-operator">></span> <span class="sql-number">10000</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Sous-requêtes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Sous-requêtes (Subqueries)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Sous-requêtes dans WHERE</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Produits plus chers que la moyenne</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prix</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">prix</span> <span class="sql-operator">></span> (
  <span class="sql-reserved">SELECT</span> <span class="sql-function">AVG</span>(<span class="sql-identifier">prix</span>) 
  <span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
);

<span class="sql-comment">-- Clients ayant passé commande ce mois-ci</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">id</span> <span class="sql-reserved">IN</span> (
  <span class="sql-reserved">SELECT</span> <span class="sql-reserved">DISTINCT</span> <span class="sql-identifier">client_id</span>
  <span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>
  <span class="sql-reserved">WHERE</span> <span class="sql-function">YEAR</span>(<span class="sql-identifier">date_commande</span>) <span class="sql-operator">=</span> <span class="sql-function">YEAR</span>(<span class="sql-function">CURDATE</span>())
  <span class="sql-reserved">AND</span> <span class="sql-function">MONTH</span>(<span class="sql-identifier">date_commande</span>) <span class="sql-operator">=</span> <span class="sql-function">MONTH</span>(<span class="sql-function">CURDATE</span>())
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sous-requêtes dans SELECT</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Nombre de commandes à côté de chaque client</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  (
    <span class="sql-reserved">SELECT</span> <span class="sql-function">COUNT</span>(<span class="sql-keyword">*</span>) 
    <span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span> <span class="sql-identifier">co</span>
    <span class="sql-reserved">WHERE</span> <span class="sql-identifier">co</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>
  ) <span class="sql-reserved">AS</span> <span class="sql-string">'nb_commandes'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">c</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Requêtes basiques</h3>
                    <p>Sur la table "employes" avec colonnes : id, nom, prenom, salaire, departement, date_embauche</p>
                    <ul>
                        <li>Sélectionner tous les employés du département "Ventes"</li>
                        <li>Afficher nom, prénom et salaire des employés gagnant plus de 40 000€</li>
                        <li>Trier les employés par date d'embauche (plus récents en premier)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Employés du département Ventes</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">departement</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">departement</span> <span class="sql-operator">=</span> <span class="sql-string">'Ventes'</span>;

<span class="sql-comment">-- Employés avec salaire > 40 000€</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">salaire</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">salaire</span> <span class="sql-operator">></span> <span class="sql-number">40000</span>;

<span class="sql-comment">-- Employés triés par date d'embauche</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">date_embauche</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">date_embauche</span> <span class="sql-reserved">DESC</span>;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Agrégations et jointures</h3>
                    <p>Avec les tables : produits (id, nom, prix, categorie_id), categories (id, nom), ventes (id,
                        produit_id, quantite, date_vente)</p>
                    <ul>
                        <li>Calculer le chiffre d'affaires total par catégorie</li>
                        <li>Trouver les 3 produits les plus vendus</li>
                        <li>Afficher les catégories avec une moyenne de prix supérieure à 50€</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- CA par catégorie</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'catégorie'</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">p</span>.<span class="sql-identifier">prix</span> <span class="sql-operator">*</span> <span class="sql-identifier">v</span>.<span class="sql-identifier">quantite</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'chiffre_affaires'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">ventes</span> <span class="sql-identifier">v</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">v</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">categories</span> <span class="sql-identifier">c</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">categorie_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>;

<span class="sql-comment">-- Top 3 des produits les plus vendus</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">p</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">v</span>.<span class="sql-identifier">quantite</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'total_vendu'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">ventes</span> <span class="sql-identifier">v</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">v</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">id</span>, <span class="sql-identifier">p</span>.<span class="sql-identifier">nom</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-string">'total_vendu'</span> <span class="sql-reserved">DESC</span>
<span class="sql-reserved">LIMIT</span> <span class="sql-number">3</span>;

<span class="sql-comment">-- Catégories avec prix moyen > 50€</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-function">AVG</span>(<span class="sql-identifier">p</span>.<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'prix_moyen'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span> <span class="sql-identifier">p</span>
<span class="sql-reserved">JOIN</span> <span class="sql-identifier">categories</span> <span class="sql-identifier">c</span> <span class="sql-reserved">ON</span> <span class="sql-identifier">p</span>.<span class="sql-identifier">categorie_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">c</span>.<span class="sql-identifier">id</span>, <span class="sql-identifier">c</span>.<span class="sql-identifier">nom</span>
<span class="sql-reserved">HAVING</span> <span class="sql-function">AVG</span>(<span class="sql-identifier">p</span>.<span class="sql-identifier">prix</span>) <span class="sql-operator">></span> <span class="sql-number">50</span>;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Optimisation des requêtes</h3>
                    <ul>
                        <li><strong>Évitez SELECT *</strong> : Spécifiez toujours les colonnes explicitement</li>
                        <li>Indexez les colonnes fréquemment utilisées dans les clauses WHERE et JOIN</li>
                        <li>Évitez les fonctions sur les colonnes indexées dans les conditions WHERE</li>
                        <li>Utilisez LIMIT pour limiter les résultats quand c'est possible</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Lisibilité et maintenance</h3>
                    <ul>
                        <li>Utilisez des alias explicites pour les colonnes et tables</li>
                        <li>Formatez vos requêtes avec des sauts de ligne logiques</li>
                        <li>Commentez les requêtes complexes</li>
                        <li>Utilisez des jointures explicites (INNER JOIN, LEFT JOIN) plutôt que des jointures
                            implicites</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurité</h3>
                    <ul>
                        <li>Validez et échappez les entrées utilisateur pour éviter les injections SQL</li>
                        <li>Utilisez des requêtes paramétrées quand c'est possible</li>
                        <li>Limitez les privilèges des utilisateurs de la base de données</li>
                        <li><strong>Ne jamais utiliser SELECT *</strong> pour éviter d'exposer des données sensibles
                        </li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        La maîtrise de la commande SELECT est essentielle pour exploiter pleinement une base de données
                        SQL.
                        Des requêtes bien structurées permettent d'extraire des informations précieuses et de prendre
                        des décisions éclairées.
                    </p>
                    <p>
                        <strong>Rappel important</strong> : Privilégiez toujours la spécification explicite des colonnes
                        plutôt que
                        l'utilisation de <code>SELECT *</code> pour des raisons de performance, de maintenance et de
                        sécurité.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous aborderons les commandes de modification des données
                        (INSERT, UPDATE, DELETE) ainsi que des concepts avancés comme les vues et les procédures
                        stockées.
                    </p>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'LessonSelectSQL',
    data() {
        return {
            lessonTitle: 'Requêtes SELECT en SQL'
        }
    },
    head() {
        return {
            title: this.lessonTitle,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Apprenez à maîtriser les requêtes SELECT en SQL avec cette leçon complète incluant syntaxe, exemples pratiques et exercices.'
                }
            ]
        }
    }
}
</script>

<style scoped>
/* Les styles précédents restent identiques */
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

/* Styles pour la section d'avertissement SELECT * */
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