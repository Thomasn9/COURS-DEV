<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">INNER JOIN en SQL</h1>
                <p class="lesson-meta text-white">SQL • MySQL • Jointures • Relations entre tables</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux INNER JOIN</h2>
                <p class="textExemple">
                    Les INNER JOIN (jointures internes) sont l'un des types de jointures les plus utilisés en SQL.
                    Elles permettent de combiner des données de plusieurs tables en se basant sur une condition de
                    correspondance.
                </p>
                <p class="textExemple">
                    Une INNER JOIN retourne uniquement les enregistrements qui ont des correspondances dans les deux
                    tables jointes,
                    formant ainsi l'intersection des datasets.
                </p>
            </section>

            <!-- Concepts fondamentaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts Fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Comment fonctionne INNER JOIN</h3>
                    <ul>
                        <li><strong>Intersection</strong> : Seules les lignes avec correspondance dans les deux tables
                            sont retournées</li>
                        <li><strong>Condition de jointure</strong> : Spécifie comment les tables sont reliées
                            (généralement via des clés primaires/étrangères)</li>
                        <li><strong>Syntaxe claire</strong> : Permettent une écriture explicite des requêtes</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement</h3>
                    <div class="code-example">
                        <pre><code>Table A          INNER JOIN         Table B
┌─────────┐                     ┌─────────┐
│ id │ nom │                     │ id │ age │
├─────────┤                     ├─────────┤
│ 1  │ A   │ ────────┐          │ 1  │ 20  │
│ 2  │ B   │         │ ┌──────→ │ 3  │ 25  │
│ 3  │ C   │ ────┐   │ │        │ 4  │ 30  │
│ 4  │ D   │     │   │ │        └─────────┘
└─────────┘     │   │ │
                │   │ │
Résultat INNER JOIN │ │
┌─────────────────┐ │ │
│ id │ nom │ age  │ │ │
├─────────────────┤ │ │
│ 1  │ A   │ 20   │←┘ │
│ 3  │ C   │ 25   │←──┘
└─────────────────┘</code></pre>
                    </div>
                </div>
            </section>

            <!-- Pourquoi éviter les jointures implicites -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple"> Pourquoi éviter les Jointures Implicites (ancienne syntaxe)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Le problème avec les jointures WHERE</h3>
                    <p>
                        L'ancienne syntaxe de jointure utilisant la clause WHERE est considérée comme une
                        <strong>mauvaise pratique</strong> pour plusieurs raisons importantes.
                    </p>

                    <div class="warning-section">
                        <h4 class="text-purple"> Ancienne syntaxe dépréciée</h4>
                        <div class="code-comparison">
                            <div>
                                <h5>Mauvaise pratique (jointure implicite)</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-comment">-- Syntaxe WHERE (dépréciée)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>, 
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>, <span class="sql-identifier">commandes</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>;</code></pre>
                                </div>
                                <p class="warning-text">Syntaxe ambiguë et moins lisible</p>
                            </div>
                            <div>
                                <h5>Bonne pratique (INNER JOIN explicite)</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-comment">-- Syntaxe INNER JOIN (moderne)</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>, 
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>;</code></pre>
                                </div>
                                <p class="success-text">Syntaxe claire et explicite</p>
                            </div>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">Problèmes avec les jointures implicites</h4>
                        <ul>
                            <li><strong>Ambiguïté</strong> : Difficile de distinguer les conditions de jointure des
                                conditions de filtrage</li>
                            <li><strong>Oubli accidentel</strong> : Risque d'oublier la condition WHERE, créant un
                                produit cartésien</li>
                            <li><strong>Maintenance difficile</strong> : Requêtes complexes deviennent illisibles</li>
                            <li><strong>Support limité</strong> : Impossible d'utiliser des jointures externes
                                (LEFT/RIGHT JOIN)</li>
                        </ul>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple"> Exemple de catastrophe avec jointure implicite</h4>
                        <div class="code-example">
                            <pre><code><span class="sql-comment">-- OUBLI de la condition WHERE = CATASTROPHE!</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>, <span class="sql-identifier">commandes</span>;
<span class="sql-comment">-- Produit cartésien: 100 clients × 1000 commandes = 100,000 lignes!</span>

<span class="sql-comment">-- Avec INNER JOIN, impossible d'oublier la condition ON</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>;
<span class="sql-comment">-- Seulement les commandes avec clients correspondants</span></code></pre>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">Avantages des INNER JOIN explicites</h4>
                        <ul>
                            <li><strong>Lisibilité</strong> : La logique de jointure est séparée du filtrage</li>
                            <li><strong>Sécurité</strong> : Impossible de créer accidentellement un produit cartésien
                            </li>
                            <li><strong>Maintenabilité</strong> : Plus facile à comprendre et modifier</li>
                            <li><strong>Compatibilité</strong> : Supporte tous les types de jointures (LEFT, RIGHT,
                                FULL)</li>
                        </ul>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Quand utiliser l'ancienne syntaxe (très rare)</h3>
                    <ul>
                        <li>Maintenance d'anciens systèmes legacy</li>
                        <li>Requêtes très simples à des fins éducatives</li>
                        <li>Environnements avec contraintes techniques spécifiques</li>
                    </ul>
                    <p><strong>En production, utilisez toujours la syntaxe INNER JOIN explicite !</strong></p>
                </div>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de Base des INNER JOIN</h2>

                <div class="textExemple">
                    <p>La structure fondamentale d'une INNER JOIN est :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">SELECT</span> <span class="sql-identifier">colonnes</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">table1</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">table2</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">table1</span>.<span class="sql-identifier">colonne</span> <span class="sql-operator">=</span> <span class="sql-identifier">table2</span>.<span class="sql-identifier">colonne</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple simple avec deux tables</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Clients et leurs commandes</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">montant</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Avec conditions supplémentaires</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Commandes récentes de clients français</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Nom client'</span>,
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">prenom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Prénom'</span>,
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Date commande'</span>,
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">montant</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Montant'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">pays</span> <span class="sql-operator">=</span> <span class="sql-string">'France'</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span> <span class="sql-operator">>=</span> <span class="sql-string">'2024-01-01'</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Jointures multiples -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Jointures Multiples</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Joindre plusieurs tables</h3>
                    <p>Vous pouvez enchaîner plusieurs INNER JOIN pour relier plusieurs tables :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Clients, commandes et produits</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">produits</span>.<span class="sql-identifier">nom_produit</span>,
  <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">quantite</span>,
  <span class="sql-identifier">produits</span>.<span class="sql-identifier">prix</span> <span class="sql-operator">*</span> <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">quantite</span> <span class="sql-reserved">AS</span> <span class="sql-string">'sous_total'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">details_commande</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">commande_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">commande_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">produits</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">produit_id</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de relations multiples</h3>
                    <div class="code-example">
                        <pre><code>clients ───── commandes ───── details_commande ───── produits
   │              │                  │                  │
client_id    commande_id        commande_id        produit_id
               client_id         produit_id</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conditions complexes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conditions de Jointure Complexes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Jointures sur plusieurs colonnes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Jointure sur clé composite</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">departements</span>.<span class="sql-identifier">nom_departement</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">departements</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">departement_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">departements</span>.<span class="sql-identifier">departement_id</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">region_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">departements</span>.<span class="sql-identifier">region_id</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Jointures avec opérateurs autres que =</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Produits et leurs promotions actives</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">produits</span>.<span class="sql-identifier">nom_produit</span>,
  <span class="sql-identifier">produits</span>.<span class="sql-identifier">prix</span>,
  <span class="sql-identifier">promotions</span>.<span class="sql-identifier">nom_promotion</span>,
  <span class="sql-identifier">promotions</span>.<span class="sql-identifier">pourcentage_remise</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">promotions</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">promotions</span>.<span class="sql-identifier">produit_id</span>
  <span class="sql-reserved">AND</span> <span class="sql-function">CURDATE</span>() <span class="sql-reserved">BETWEEN</span> <span class="sql-identifier">promotions</span>.<span class="sql-identifier">date_debut</span> <span class="sql-reserved">AND</span> <span class="sql-identifier">promotions</span>.<span class="sql-identifier">date_fin</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Auto-jointure (Self JOIN)</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Employés et leurs managers</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Employé'</span>,
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">prenom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Prénom employé'</span>,
  <span class="sql-identifier">managers</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Manager'</span>,
  <span class="sql-identifier">managers</span>.<span class="sql-identifier">prenom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Prénom manager'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">managers</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">manager_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">managers</span>.<span class="sql-identifier">employe_id</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Agrégations avec JOIN -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Agrégations avec INNER JOIN</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Calculs sur données jointes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Chiffre d'affaires par client</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">clients</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">commandes</span>.<span class="sql-identifier">commande_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre de commandes'</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">commandes</span>.<span class="sql-identifier">montant</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Chiffre d affaires total'</span>,
  <span class="sql-function">AVG</span>(<span class="sql-identifier">commandes</span>.<span class="sql-identifier">montant</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Montant moyen par commande'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span>, <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">clients</span>.<span class="sql-identifier">prenom</span>
<span class="sql-reserved">HAVING</span> <span class="sql-function">SUM</span>(<span class="sql-identifier">commandes</span>.<span class="sql-identifier">montant</span>) <span class="sql-operator">></span> <span class="sql-number">1000</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-string">'Chiffre d affaires total'</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Top produits par catégorie</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Produits les plus vendus par catégorie</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">categories</span>.<span class="sql-identifier">nom_categorie</span>,
  <span class="sql-identifier">produits</span>.<span class="sql-identifier">nom_produit</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">details_commande</span>.<span class="sql-identifier">quantite</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Quantité vendue'</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">details_commande</span>.<span class="sql-identifier">quantite</span> <span class="sql-operator">*</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Chiffre d affaires'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">categories</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">produits</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">categories</span>.<span class="sql-identifier">categorie_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">categorie_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">details_commande</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">produit_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">categories</span>.<span class="sql-identifier">categorie_id</span>, <span class="sql-identifier">categories</span>.<span class="sql-identifier">nom_categorie</span>, <span class="sql-identifier">produits</span>.<span class="sql-identifier">produit_id</span>, <span class="sql-identifier">produits</span>.<span class="sql-identifier">nom_produit</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">categories</span>.<span class="sql-identifier">nom_categorie</span>, <span class="sql-string">'Quantité vendue'</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Performance et optimisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Performance et Optimisation</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques pour les INNER JOIN</h3>
                    <ul>
                        <li><strong>Indexez les colonnes de jointure</strong> : Clés primaires et étrangères</li>
                        <li><strong>Utilisez WHERE pour filtrer tôt</strong> : Réduisez le dataset avant la jointure
                        </li>
                        <li><strong>Sélectionnez uniquement les colonnes nécessaires</strong> : Évitez SELECT *</li>
                        <li><strong>Limitez les résultats</strong> : Utilisez LIMIT pour les requêtes exploratoires</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple d'optimisation</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Moins efficace</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-comment">-- Jointure avant filtrage</span>
<span class="sql-reserved">SELECT</span> <span class="sql-keyword">*</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">ville</span> <span class="sql-operator">=</span> <span class="sql-string">'Paris'</span>;</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>Plus efficace</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-comment">-- Filtrage avant jointure (si possible)</span>
<span class="sql-reserved">SELECT</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">clients</span>.<span class="sql-identifier">prenom</span>, <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span>
<span class="sql-reserved">FROM</span> (
  <span class="sql-reserved">SELECT</span> <span class="sql-identifier">client_id</span>, <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>
  <span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
  <span class="sql-reserved">WHERE</span> <span class="sql-identifier">ville</span> <span class="sql-operator">=</span> <span class="sql-string">'Paris'</span>
) <span class="sql-identifier">clients</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>;</code></pre>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Exemple complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple Complet : Système E-commerce</h2>

                <div class="textExemple">
                    <p>Requête complète pour analyser les ventes d'un e-commerce :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Analyse des ventes par région et catégorie</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">regions</span>.<span class="sql-identifier">nom_region</span>,
  <span class="sql-identifier">categories</span>.<span class="sql-identifier">nom_categorie</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-reserved">DISTINCT</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">commande_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre de commandes'</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">details_commande</span>.<span class="sql-identifier">quantite</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Quantité vendue'</span>,
  <span class="sql-function">SUM</span>(<span class="sql-identifier">details_commande</span>.<span class="sql-identifier">quantite</span> <span class="sql-operator">*</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Chiffre d affaires'</span>,
  <span class="sql-function">AVG</span>(<span class="sql-identifier">produits</span>.<span class="sql-identifier">prix</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Prix moyen'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">regions</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">clients</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">regions</span>.<span class="sql-identifier">region_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">region_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">commandes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">clients</span>.<span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">client_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">details_commande</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">commande_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">commande_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">produits</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">details_commande</span>.<span class="sql-identifier">produit_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">produit_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">categories</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">produits</span>.<span class="sql-identifier">categorie_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">categories</span>.<span class="sql-identifier">categorie_id</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">date_commande</span> <span class="sql-operator">>=</span> <span class="sql-string">'2024-01-01'</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">commandes</span>.<span class="sql-identifier">statut</span> <span class="sql-operator">=</span> <span class="sql-string">'livrée'</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">regions</span>.<span class="sql-identifier">region_id</span>, <span class="sql-identifier">regions</span>.<span class="sql-identifier">nom_region</span>, <span class="sql-identifier">categories</span>.<span class="sql-identifier">categorie_id</span>, <span class="sql-identifier">categories</span>.<span class="sql-identifier">nom_categorie</span>
<span class="sql-reserved">HAVING</span> <span class="sql-string">'Chiffre d affaires'</span> <span class="sql-operator">></span> <span class="sql-number">5000</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-identifier">regions</span>.<span class="sql-identifier">nom_region</span>, <span class="sql-string">'Chiffre d affaires'</span> <span class="sql-reserved">DESC</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Système de Ressources Humaines</h3>
                    <p>Avec les tables : employes, departements, postes, salaries_historique</p>
                    <ul>
                        <li>Afficher tous les employés avec leur département et poste actuel</li>
                        <li>Calculer le salaire moyen par département</li>
                        <li>Trouver les managers et leurs équipes</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Employés avec département et poste</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">departements</span>.<span class="sql-identifier">nom_departement</span>,
  <span class="sql-identifier">postes</span>.<span class="sql-identifier">titre_poste</span>,
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">salaire</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">departements</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">departement_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">departements</span>.<span class="sql-identifier">departement_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">postes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">poste_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">postes</span>.<span class="sql-identifier">poste_id</span>;

<span class="sql-comment">-- Salaire moyen par département</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">departements</span>.<span class="sql-identifier">nom_departement</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">employes</span>.<span class="sql-identifier">employe_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre employés'</span>,
  <span class="sql-function">AVG</span>(<span class="sql-identifier">employes</span>.<span class="sql-identifier">salaire</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Salaire moyen'</span>,
  <span class="sql-function">MAX</span>(<span class="sql-identifier">employes</span>.<span class="sql-identifier">salaire</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Salaire maximum'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">departements</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">employes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">departements</span>.<span class="sql-identifier">departement_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">departement_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">departements</span>.<span class="sql-identifier">departement_id</span>, <span class="sql-identifier">departements</span>.<span class="sql-identifier">nom_departement</span>;

<span class="sql-comment">-- Managers et leurs équipes</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">managers</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Manager'</span>,
  <span class="sql-identifier">managers</span>.<span class="sql-identifier">prenom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Prénom manager'</span>,
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Employé'</span>,
  <span class="sql-identifier">employes</span>.<span class="sql-identifier">prenom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Prénom employé'</span>,
  <span class="sql-identifier">departements</span>.<span class="sql-identifier">nom_departement</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">employes</span> <span class="sql-identifier">managers</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">employes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">managers</span>.<span class="sql-identifier">employe_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">manager_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">departements</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">employes</span>.<span class="sql-identifier">departement_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">departements</span>.<span class="sql-identifier">departement_id</span>;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Système Académique</h3>
                    <p>Avec les tables : etudiants, cours, professeurs, inscriptions, notes</p>
                    <ul>
                        <li>Afficher les étudiants avec leurs cours et notes</li>
                        <li>Calculer la moyenne générale par étudiant</li>
                        <li>Trouver les cours les plus populaires</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Étudiants avec cours et notes</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">cours</span>.<span class="sql-identifier">titre_cours</span>,
  <span class="sql-identifier">professeurs</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Professeur'</span>,
  <span class="sql-identifier">notes</span>.<span class="sql-identifier">note</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">etudiants</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">inscriptions</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">etudiant_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">etudiant_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">cours</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">cours_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">cours</span>.<span class="sql-identifier">cours_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">professeurs</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">cours</span>.<span class="sql-identifier">professeur_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">professeurs</span>.<span class="sql-identifier">professeur_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">notes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">inscription_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">notes</span>.<span class="sql-identifier">inscription_id</span>;

<span class="sql-comment">-- Moyenne générale par étudiant</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">nom</span>,
  <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">prenom</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">notes</span>.<span class="sql-identifier">note_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre de notes'</span>,
  <span class="sql-function">AVG</span>(<span class="sql-identifier">notes</span>.<span class="sql-identifier">note</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Moyenne générale'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">etudiants</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">inscriptions</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">etudiant_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">etudiant_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">notes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">inscription_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">notes</span>.<span class="sql-identifier">inscription_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">etudiant_id</span>, <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">nom</span>, <span class="sql-identifier">etudiants</span>.<span class="sql-identifier">prenom</span>
<span class="sql-reserved">HAVING</span> <span class="sql-function">COUNT</span>(<span class="sql-identifier">notes</span>.<span class="sql-identifier">note_id</span>) <span class="sql-operator">>=</span> <span class="sql-number">3</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-string">'Moyenne générale'</span> <span class="sql-reserved">DESC</span>;

<span class="sql-comment">-- Cours les plus populaires</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">cours</span>.<span class="sql-identifier">titre_cours</span>,
  <span class="sql-identifier">professeurs</span>.<span class="sql-identifier">nom</span> <span class="sql-reserved">AS</span> <span class="sql-string">'Professeur'</span>,
  <span class="sql-function">COUNT</span>(<span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">etudiant_id</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Nombre d étudiants'</span>,
  <span class="sql-function">AVG</span>(<span class="sql-identifier">notes</span>.<span class="sql-identifier">note</span>) <span class="sql-reserved">AS</span> <span class="sql-string">'Note moyenne'</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">cours</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">professeurs</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">cours</span>.<span class="sql-identifier">professeur_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">professeurs</span>.<span class="sql-identifier">professeur_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">inscriptions</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">cours</span>.<span class="sql-identifier">cours_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">cours_id</span>
<span class="sql-reserved">INNER JOIN</span> <span class="sql-identifier">notes</span> 
  <span class="sql-reserved">ON</span> <span class="sql-identifier">inscriptions</span>.<span class="sql-identifier">inscription_id</span> <span class="sql-operator">=</span> <span class="sql-identifier">notes</span>.<span class="sql-identifier">inscription_id</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-identifier">cours</span>.<span class="sql-identifier">cours_id</span>, <span class="sql-identifier">cours</span>.<span class="sql-identifier">titre_cours</span>, <span class="sql-identifier">professeurs</span>.<span class="sql-identifier">nom</span>
<span class="sql-reserved">ORDER BY</span> <span class="sql-string">'Nombre d étudiants'</span> <span class="sql-reserved">DESC</span>
<span class="sql-reserved">LIMIT</span> <span class="sql-number">10</span>;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Conception des jointures</h3>
                    <ul>
                        <li><strong>Toujours utiliser INNER JOIN explicite</strong> plutôt que la syntaxe WHERE
                            dépréciée</li>
                        <li>Utiliser des noms de tables explicites pour plus de clarté</li>
                        <li>Utiliser des clés primaires et étrangères pour des jointures efficaces</li>
                        <li>Séparer la logique de jointure (ON) de la logique de filtrage (WHERE)</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance et optimisation</h3>
                    <ul>
                        <li>Indexer les colonnes utilisées dans les conditions ON</li>
                        <li>Filtrer les données tôt avec WHERE pour réduire les datasets</li>
                        <li>Éviter SELECT * et sélectionner uniquement les colonnes nécessaires</li>
                        <li>Utiliser LIMIT pour les requêtes exploratoires sur de grandes tables</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Lisibilité et maintenance</h3>
                    <ul>
                        <li>Formater les requêtes avec des indentations logiques</li>
                        <li>Utiliser des alias explicites pour les colonnes calculées</li>
                        <li>Commenter les jointures complexes</li>
                        <li>Organiser les jointures dans l'ordre logique des relations</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Les INNER JOIN sont un outil puissant pour combiner des données de multiples tables
                        et extraire des informations significatives de votre base de données.
                    </p>
                    <p>
                        <strong>Rappel crucial</strong> : Privilégiez toujours la syntaxe INNER JOIN explicite
                        pour éviter les produits cartésiens accidentels et améliorer la lisibilité de vos requêtes.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous aborderons les autres types de jointures
                        (LEFT JOIN, RIGHT JOIN, FULL JOIN) et les jointures avancées.
                    </p>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'InnerJoinLesson'
}
</script>

<style scoped>
/* Les styles restent identiques */
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