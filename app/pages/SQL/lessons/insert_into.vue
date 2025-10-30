<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">INSERT INTO en SQL</h1>
                <p class="lesson-meta text-white">SQL • MySQL • Insertion de données • CRUD</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à INSERT INTO</h2>
                <p class="textExemple">
                    La commande <strong>INSERT INTO</strong> est utilisée pour ajouter de nouveaux enregistrements
                    dans une table de base de données. C'est l'une des opérations fondamentales du CRUD (Create, Read,
                    Update, Delete).
                </p>
                <p class="textExemple">
                    Elle permet de peupler les tables avec des données et est essentielle pour toute application
                    qui nécessite un stockage persistant d'informations.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de Base</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe générale</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">nom_table</span> (<span class="sql-identifier">colonne1</span>, <span class="sql-identifier">colonne2</span>, <span class="sql-identifier">colonne3</span>, ...)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'valeur1'</span>, <span class="sql-string">'valeur2'</span>, <span class="sql-string">'valeur3'</span>, ...);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple concret</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Insertion d'un nouveau client</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">email</span>,
  <span class="sql-identifier">telephone</span>,
  <span class="sql-identifier">date_inscription</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Dupont'</span>,
  <span class="sql-string">'Marie'</span>,
  <span class="sql-string">'marie.dupont@email.com'</span>,
  <span class="sql-string">'0123456789'</span>,
  <span class="sql-string">'2024-01-15'</span>
);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes d'insertion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Différentes Méthodes d'Insertion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Insertion avec toutes les colonnes</h3>
                    <p>Si vous fournissez des valeurs pour toutes les colonnes, vous pouvez omettre les noms de colonnes
                        :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Table clients avec 5 colonnes dans l'ordre: id, nom, prenom, email, date_inscription</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">VALUES</span> (
  <span class="sql-number">NULL</span>,
  <span class="sql-string">'Martin'</span>,
  <span class="sql-string">'Pierre'</span>,
  <span class="sql-string">'pierre.martin@email.com'</span>,
  <span class="sql-string">'2024-01-16'</span>
);</code></pre>
                    </div>
                    <p class="warning-text">⚠️ Attention : L'ordre des valeurs doit correspondre exactement à l'ordre
                        des colonnes dans la table.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Insertion partielle</h3>
                    <p>Vous pouvez n'insérer que certaines colonnes (les autres prennent leurs valeurs par défaut ou
                        NULL) :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Insertion avec seulement le nom et l'email</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">email</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Bernard'</span>,
  <span class="sql-string">'jacques.bernard@email.com'</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Insertion multiple</h3>
                    <p>Insérer plusieurs enregistrements en une seule requête :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">email</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-string">'Moreau'</span>, <span class="sql-string">'Sophie'</span>, <span class="sql-string">'sophie.moreau@email.com'</span>),
  (<span class="sql-string">'Petit'</span>, <span class="sql-string">'Luc'</span>, <span class="sql-string">'luc.petit@email.com'</span>),
  (<span class="sql-string">'Roux'</span>, <span class="sql-string">'Isabelle'</span>, <span class="sql-string">'isabelle.roux@email.com'</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Types de données -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des Différents Types de Données</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Chaînes de caractères</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">produits</span> (
  <span class="sql-identifier">nom_produit</span>,
  <span class="sql-identifier">description</span>,
  <span class="sql-identifier">categorie</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Ordinateur Portable'</span>,
  <span class="sql-string">'PC portable 15 pouces, 8GB RAM, 512GB SSD'</span>,
  <span class="sql-string">'Informatique'</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Nombres et valeurs numériques</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">produits</span> (
  <span class="sql-identifier">nom_produit</span>,
  <span class="sql-identifier">prix</span>,
  <span class="sql-identifier">quantite_stock</span>,
  <span class="sql-identifier">taux_tva</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Smartphone'</span>,
  <span class="sql-number">599.99</span>,
  <span class="sql-number">50</span>,
  <span class="sql-number">20.0</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Dates et heures</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">heure_commande</span>,
  <span class="sql-identifier">date_livraison_prevue</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-number">1</span>,
  <span class="sql-string">'2024-01-20'</span>,
  <span class="sql-string">'14:30:00'</span>,
  <span class="sql-string">'2024-01-25'</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Valeurs NULL et DEFAULT</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">employes</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">date_embauche</span>,
  <span class="sql-identifier">salaire</span>,
  <span class="sql-identifier">departement_id</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Lefebvre'</span>,
  <span class="sql-string">'Thomas'</span>,
  <span class="sql-reserved">NULL</span>,
  <span class="sql-reserved">DEFAULT</span>,
  <span class="sql-reserved">NULL</span>
);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Insertion avec SELECT -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Insertion avec SELECT</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Copie de données entre tables</h3>
                    <p>Insérer des données provenant d'une requête SELECT :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Copier tous les clients français dans une nouvelle table</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients_france</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">email</span>
)
<span class="sql-reserved">SELECT</span>
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">email</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">pays</span> <span class="sql-operator">=</span> <span class="sql-string">'France'</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Archivage des anciennes commandes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Archiver les commandes de plus d'un an</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes_archivees</span> (
  <span class="sql-identifier">commande_id</span>,
  <span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">montant</span>
)
<span class="sql-reserved">SELECT</span>
  <span class="sql-identifier">commande_id</span>,
  <span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">montant</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">date_commande</span> <span class="sql-operator">&lt;</span> <span class="sql-string">'2023-01-01'</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Création de statistiques</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Insérer des statistiques mensuelles</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">statistiques_ventes</span> (
  <span class="sql-identifier">mois</span>,
  <span class="sql-identifier">annee</span>,
  <span class="sql-identifier">nombre_commandes</span>,
  <span class="sql-identifier">chiffre_affaires</span>
)
<span class="sql-reserved">SELECT</span>
  <span class="sql-function">MONTH</span>(<span class="sql-identifier">date_commande</span>),
  <span class="sql-function">YEAR</span>(<span class="sql-identifier">date_commande</span>),
  <span class="sql-function">COUNT</span>(<span class="sql-operator">*</span>),
  <span class="sql-function">SUM</span>(<span class="sql-identifier">montant</span>)
<span class="sql-reserved">FROM</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">date_commande</span> <span class="sql-operator">>=</span> <span class="sql-string">'2024-01-01'</span>
<span class="sql-reserved">GROUP BY</span> <span class="sql-function">YEAR</span>(<span class="sql-identifier">date_commande</span>), <span class="sql-function">MONTH</span>(<span class="sql-identifier">date_commande</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des clés auto-incrémentées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des Clés Auto-incrémentées</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Clés primaires auto-incrémentées</h3>
                    <p>Pour les colonnes auto-incrémentées, utilisez NULL ou DEFAULT :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- La colonne client_id est auto-incrémentée</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-reserved">NULL</span>,
  <span class="sql-string">'Garcia'</span>,
  <span class="sql-string">'Ana'</span>
);

<span class="sql-comment">-- Ou plus simplement, ne pas mentionner la colonne auto-incrémentée</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Garcia'</span>,
  <span class="sql-string">'Ana'</span>
);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Récupération de l'ID inséré</h3>
                    <p>Dans la plupart des SGBD, vous pouvez récupérer le dernier ID auto-généré :</p>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- MySQL</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Dubois'</span>, <span class="sql-string">'Michel'</span>);

<span class="sql-reserved">SELECT</span> <span class="sql-function">LAST_INSERT_ID</span>(); <span class="sql-comment">-- Retourne l'ID du dernier client inséré</span>

<span class="sql-comment">-- PostgreSQL</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Dubois'</span>, <span class="sql-string">'Michel'</span>)
<span class="sql-reserved">RETURNING</span> <span class="sql-identifier">client_id</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Contraintes et validation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Contraintes et Validation des Données</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Gestion des contraintes NOT NULL</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ ERREUR : La colonne 'nom' ne peut pas être NULL</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-reserved">NULL</span>, <span class="sql-string">'test@email.com'</span>);

<span class="sql-comment">-- ✅ CORRECT</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Durand'</span>, <span class="sql-string">'test@email.com'</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes UNIQUE</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ ERREUR : L'email doit être unique</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Laurent'</span>, <span class="sql-string">'marie.dupont@email.com'</span>); <span class="sql-comment">-- Email déjà existant</span>

<span class="sql-comment">-- ✅ CORRECT : Email unique</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Laurent'</span>, <span class="sql-string">'laurent.nouveau@email.com'</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Clés étrangères</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ ERREUR : Le client_id 999 n'existe pas</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> (<span class="sql-identifier">client_id</span>, <span class="sql-identifier">date_commande</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-number">999</span>, <span class="sql-string">'2024-01-20'</span>);

<span class="sql-comment">-- ✅ CORRECT : Le client_id existe</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> (<span class="sql-identifier">client_id</span>, <span class="sql-identifier">date_commande</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-number">1</span>, <span class="sql-string">'2024-01-20'</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurité et injections SQL</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>❌ Mauvaise pratique (vulnérable aux injections)</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-comment">-- NE JAMAIS FAIRE ÇA !</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'$nom'</span>, <span class="sql-string">'$email'</span>);</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>✅ Bonne pratique (requêtes préparées)</h5>
                            <div class="code-example">
                                <pre><code><span class="sql-comment">-- Utiliser des requêtes préparées</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (?, ?);

<span class="sql-comment">-- Ou avec des paramètres nommés</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (:nom, :email);</code></pre>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Validation des données</h3>
                    <ul>
                        <li><strong>Toujours valider les données</strong> avant insertion</li>
                        <li><strong>Utiliser les contraintes de la base de données</strong> (NOT NULL, UNIQUE, CHECK)
                        </li>
                        <li><strong>Échapper les caractères spéciaux</strong> dans les chaînes de caractères</li>
                        <li><strong>Vérifier les formats de dates</strong> et nombres</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance</h3>
                    <ul>
                        <li><strong>Préférer les insertions multiples</strong> pour plusieurs enregistrements</li>
                        <li><strong>Utiliser les transactions</strong> pour des insertions groupées</li>
                        <li><strong>Désactiver les index temporairement</strong> lors de gros imports</li>
                        <li><strong>Utiliser LOAD DATA INFILE</strong> pour les imports massifs (MySQL)</li>
                    </ul>
                </div>
            </section>

            <!-- Exemples pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples Pratiques Complets</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Système de blog</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Insertion d'un nouvel article</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">articles</span> (
  <span class="sql-identifier">titre</span>,
  <span class="sql-identifier">contenu</span>,
  <span class="sql-identifier">auteur_id</span>,
  <span class="sql-identifier">date_publication</span>,
  <span class="sql-identifier">est_publie</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-string">'Introduction à SQL'</span>,
  <span class="sql-string">'SQL est un langage de programmation utilisé pour gérer les bases de données...'</span>,
  <span class="sql-number">1</span>,
  <span class="sql-function">NOW</span>(),
  <span class="sql-number">1</span>
);

<span class="sql-comment">-- Insertion de tags pour l'article</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">article_tags</span> (
  <span class="sql-identifier">article_id</span>,
  <span class="sql-identifier">tag_id</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-function">LAST_INSERT_ID</span>(), <span class="sql-number">1</span>),
  (<span class="sql-function">LAST_INSERT_ID</span>(), <span class="sql-number">3</span>),
  (<span class="sql-function">LAST_INSERT_ID</span>(), <span class="sql-number">5</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Système e-commerce</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Création d'une nouvelle commande</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">date_commande</span>,
  <span class="sql-identifier">statut</span>,
  <span class="sql-identifier">montant_total</span>
)
<span class="sql-reserved">VALUES</span> (
  <span class="sql-number">123</span>,
  <span class="sql-function">NOW</span>(),
  <span class="sql-string">'en_attente'</span>,
  <span class="sql-number">149.99</span>
);

<span class="sql-comment">-- Ajout des produits à la commande</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">details_commande</span> (
  <span class="sql-identifier">commande_id</span>,
  <span class="sql-identifier">produit_id</span>,
  <span class="sql-identifier">quantite</span>,
  <span class="sql-identifier">prix_unitaire</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-function">LAST_INSERT_ID</span>(), <span class="sql-number">45</span>, <span class="sql-number">1</span>, <span class="sql-number">99.99</span>),
  (<span class="sql-function">LAST_INSERT_ID</span>(), <span class="sql-number">78</span>, <span class="sql-number">2</span>, <span class="sql-number">25.00</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des erreurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des Erreurs Courantes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Erreurs de syntaxe</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ Oubli des parenthèses</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> <span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span> <span class="sql-reserved">VALUES</span> <span class="sql-string">'Dupont'</span>, <span class="sql-string">'Jean'</span>;

<span class="sql-comment">-- ✅ Syntaxe correcte</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>) <span class="sql-reserved">VALUES</span> (<span class="sql-string">'Dupont'</span>, <span class="sql-string">'Jean'</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Nombre de valeurs incorrect</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ 3 colonnes mais 2 valeurs</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Dupont'</span>, <span class="sql-string">'Jean'</span>);

<span class="sql-comment">-- ✅ Nombre de valeurs correspondant</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">prenom</span>, <span class="sql-identifier">email</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Dupont'</span>, <span class="sql-string">'Jean'</span>, <span class="sql-string">'jean.dupont@email.com'</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Types de données incompatibles</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- ❌ La colonne 'age' attend un nombre</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">age</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Martin'</span>, <span class="sql-string">'trente'</span>);

<span class="sql-comment">-- ✅ Type correct</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">clients</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">age</span>)
<span class="sql-reserved">VALUES</span> (<span class="sql-string">'Martin'</span>, <span class="sql-number">30</span>);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Gestion des étudiants</h3>
                    <p>Tables : etudiants, cours, inscriptions</p>
                    <ul>
                        <li>Insérer 3 nouveaux étudiants</li>
                        <li>Insérer 2 nouveaux cours</li>
                        <li>Inscrire les étudiants aux cours</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Insertion des étudiants</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">etudiants</span> (
  <span class="sql-identifier">nom</span>,
  <span class="sql-identifier">prenom</span>,
  <span class="sql-identifier">email</span>,
  <span class="sql-identifier">date_naissance</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-string">'Bernard'</span>, <span class="sql-string">'Alice'</span>, <span class="sql-string">'alice.bernard@email.com'</span>, <span class="sql-string">'2000-05-15'</span>),
  (<span class="sql-string">'Moreau'</span>, <span class="sql-string">'Bruno'</span>, <span class="sql-string">'bruno.moreau@email.com'</span>, <span class="sql-string">'1999-08-22'</span>),
  (<span class="sql-string">'Petit'</span>, <span class="sql-string">'Clara'</span>, <span class="sql-string">'clara.petit@email.com'</span>, <span class="sql-string">'2001-03-10'</span>);

<span class="sql-comment">-- Insertion des cours</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">cours</span> (
  <span class="sql-identifier">titre</span>,
  <span class="sql-identifier">description</span>,
  <span class="sql-identifier">credits</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-string">'Base de données'</span>, <span class="sql-string">'Introduction aux SGBD et SQL'</span>, <span class="sql-number">4</span>),
  (<span class="sql-string">'Programmation Web'</span>, <span class="sql-string">'Développement front-end et back-end'</span>, <span class="sql-number">5</span>);

<span class="sql-comment">-- Inscription des étudiants aux cours</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">inscriptions</span> (
  <span class="sql-identifier">etudiant_id</span>,
  <span class="sql-identifier">cours_id</span>,
  <span class="sql-identifier">date_inscription</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-number">1</span>, <span class="sql-number">1</span>, <span class="sql-function">NOW</span>()),
  (<span class="sql-number">1</span>, <span class="sql-number">2</span>, <span class="sql-function">NOW</span>()),
  (<span class="sql-number">2</span>, <span class="sql-number">1</span>, <span class="sql-function">NOW</span>()),
  (<span class="sql-number">3</span>, <span class="sql-number">2</span>, <span class="sql-function">NOW</span>());</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Système de réservations</h3>
                    <p>Tables : clients, chambres, reservations</p>
                    <ul>
                        <li>Insérer de nouvelles chambres d'hôtel</li>
                        <li>Créer des réservations pour les clients</li>
                        <li>Gérer les dates de séjour</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Insertion des chambres</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">chambres</span> (
  <span class="sql-identifier">numero</span>,
  <span class="sql-identifier">type_chambre</span>,
  <span class="sql-identifier">prix_nuit</span>,
  <span class="sql-identifier">est_disponible</span>
)
<span class="sql-reserved">VALUES</span>
  (<span class="sql-string">'101'</span>, <span class="sql-string">'Simple'</span>, <span class="sql-number">80.00</span>, <span class="sql-number">1</span>),
  (<span class="sql-string">'102'</span>, <span class="sql-string">'Double'</span>, <span class="sql-number">120.00</span>, <span class="sql-number">1</span>),
  (<span class="sql-string">'201'</span>, <span class="sql-string">'Suite'</span>, <span class="sql-number">200.00</span>, <span class="sql-number">1</span>);

<span class="sql-comment">-- Création de réservations</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">reservations</span> (
  <span class="sql-identifier">client_id</span>,
  <span class="sql-identifier">chambre_id</span>,
  <span class="sql-identifier">date_arrivee</span>,
  <span class="sql-identifier">date_depart</span>,
  <span class="sql-identifier">nombre_personnes</span>,
  <span class="sql-identifier">prix_total</span>
)
<span class="sql-reserved">VALUES</span>
  (
    <span class="sql-number">1</span>,
    <span class="sql-number">2</span>,
    <span class="sql-string">'2024-02-01'</span>,
    <span class="sql-string">'2024-02-05'</span>,
    <span class="sql-number">2</span>,
    <span class="sql-number">480.00</span>
  ),
  (
    <span class="sql-number">2</span>,
    <span class="sql-number">3</span>,
    <span class="sql-string">'2024-02-10'</span>,
    <span class="sql-string">'2024-02-12'</span>,
    <span class="sql-number">2</span>,
    <span class="sql-number">400.00</span>
  );</code></pre>
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
                        <li><strong>INSERT INTO</strong> est la commande fondamentale pour ajouter des données</li>
                        <li>Plusieurs syntaxes disponibles selon les besoins</li>
                        <li>Respecter les contraintes et types de données</li>
                        <li>Privilégier la sécurité avec les requêtes préparées</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Prochaines étapes</h3>
                    <p>
                        Maintenant que vous maîtrisez l'insertion de données, les prochaines leçons couvriront :
                    </p>
                    <ul>
                        <li>La lecture de données avec <strong>SELECT</strong></li>
                        <li>La modification avec <strong>UPDATE</strong></li>
                        <li>La suppression avec <strong>DELETE</strong></li>
                        <li>Les transactions et la gestion d'erreurs</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques à retenir</h3>
                    <ul>
                        <li>✅ <strong>Toujours utiliser des requêtes préparées</strong></li>
                        <li>✅ <strong>Valider les données avant insertion</strong></li>
                        <li>✅ <strong>Respecter les contraintes de la base</strong></li>
                        <li>✅ <strong>Utiliser les insertions multiples quand possible</strong></li>
                        <li>❌ <strong>Ne jamais concaténer des variables directement</strong></li>
                    </ul>
                </div>
            </section>
        </div>
    </div>
</template>

<script>

</script>

<style scoped>
/* Les styles restent identiques à la leçon précédente */
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