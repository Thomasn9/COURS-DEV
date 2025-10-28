<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">ALTER TABLE en SQL</h1>
                <p class="lesson-meta text-white">SQL • MySQL • Modification de tables • Maintenance de base de données
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à ALTER TABLE</h2>
                <p class="textExemple">
                    La commande ALTER TABLE est essentielle pour modifier la structure d'une table existante sans avoir
                    à la supprimer et la recréer.
                </p>
                <p class="textExemple">
                    Elle permet d'ajouter, modifier ou supprimer des colonnes, de changer des types de données,
                    d'ajouter des contraintes et bien plus encore, tout en préservant les données existantes.
                </p>
            </section>

            <!-- Pourquoi éviter les modifications directes en production -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Dangers des ALTER TABLE en Production</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Les risques des modifications directes</h3>
                    <p>
                        Bien qu'ALTER TABLE soit puissant, son utilisation inconsidérée en production peut causer
                        des <strong>problèmes graves</strong> de disponibilité et d'intégrité des données.
                    </p>

                    <div class="warning-section">
                        <h4 class="text-purple"> Modification directe sans précaution</h4>
                        <div class="code-comparison">
                            <div>
                                <h5>Mauvaise pratique</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-comment">--  Modification directe pendant les heures de pointe</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">date_naissance</span> <span class="sql-type">DATE</span>,
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">320</span>);
<span class="sql-comment">--  Bloque la table pendant l'exécution!</span></code></pre>
                                </div>
                                <p class="warning-text"> Bloquer la table peut interrompre l'application</p>
                            </div>
                            <div>
                                <h5>Bonne pratique</h5>
                                <div class="code-example">
                                    <pre><code><span class="sql-comment">-- Planification et utilisation d'outils adaptés</span>
<span class="sql-comment">-- 1. Exécuter pendant une fenêtre de maintenance</span>
<span class="sql-comment">-- 2. Utiliser pt-online-schema-change (Percona)</span>
<span class="sql-comment">-- 3. Tester d'abord en environnement de dev/staging</span>
<span class="sql-comment">-- 4. Avoir un plan de rollback</span>

<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">date_naissance</span> <span class="sql-type">DATE</span>,
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">320</span>);</code></pre>
                                </div>
                                <p class="success-text">Modifications planifiées et sécurisées</p>
                            </div>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple"> Problèmes courants avec ALTER TABLE</h4>
                        <ul>
                            <li><strong>Blocage de table</strong> : La table devient inaccessible pendant l'exécution
                            </li>
                            <li><strong>Perte de données</strong> : Suppression accidentelle de colonnes importantes
                            </li>
                            <li><strong>Incompatibilité</strong> : Changements qui cassent l'application</li>
                            <li><strong>Performance</strong> : Reconstruction d'index sur de grandes tables</li>
                            <li><strong>Réplication</strong> : Problèmes avec les slaves en réplication</li>
                        </ul>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">🔧 Exemple de catastrophe réelle</h4>
                        <div class="code-example">
                            <pre><code><span class="sql-comment">--  SCÉNARIO CATASTROPHE</span>
<span class="sql-comment">-- Développeur exécute en production sans test préalable</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">client_id</span>;
<span class="sql-comment">--  OUBLI de la condition WHERE dans une requête DELETE!</span>

<span class="sql-comment">-- Résultat:</span>
<span class="sql-comment">-- • Toutes les commandes perdues</span>
<span class="sql-comment">-- • Application cassée</span>
<span class="sql-comment">-- • Restauration depuis backup = 4 heures d'indisponibilité</span>
<span class="sql-comment">-- • Perte de données entre backup et incident</span></code></pre>
                        </div>
                    </div>

                    <div class="textExemple">
                        <h4 class="text-purple">🛡️ Bonnes pratiques pour ALTER TABLE</h4>
                        <ul>
                            <li><strong>Toujours tester</strong> en environnement de développement d'abord</li>
                            <li><strong>Planifier</strong> pendant les fenêtres de maintenance</li>
                            <li><strong>Sauvegarder</strong> les données avant toute modification</li>
                            <li><strong>Utiliser des outils</strong> comme pt-online-schema-change pour les grosses
                                tables</li>
                            <li><strong>Documenter</strong> les changements de schéma</li>
                            <li><strong>Prévoir un rollback</strong> en cas de problème</li>
                        </ul>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Quand utiliser ALTER TABLE directement </h3>
                    <ul>
                        <li>Environnements de développement et test</li>
                        <li>Petites tables avec peu d'impact</li>
                        <li>Fenêtres de maintenance planifiées</li>
                        <li>Modifications non-bloquantes (ajout de colonne NULLable)</li>
                    </ul>
                    <p><strong>En production, planifiez et testez TOUJOURS vos ALTER TABLE !</strong></p>
                </div>
            </section>

            <!-- Ajout de colonnes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Ajout de Colonnes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe de base</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">nom_table</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">nom_colonne</span> <span class="sql-type">type_donnees</span> [<span class="sql-keyword">contraintes</span>];</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples pratiques</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Ajout d'une colonne simple</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">telephone</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">20</span>);

<span class="sql-comment">-- Ajout avec contraintes</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">date_creation</span> <span class="sql-type">DATETIME</span> <span class="sql-keyword">NOT NULL DEFAULT</span> <span class="sql-function">CURRENT_TIMESTAMP</span>;

<span class="sql-comment">-- Ajout avec valeur par défaut</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">statut</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">20</span>) <span class="sql-keyword">DEFAULT</span> <span class="sql-string">'en attente'</span>;

<span class="sql-comment">-- Ajout de plusieurs colonnes en une commande</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">employes</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">date_embauche</span> <span class="sql-type">DATE</span>,
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">salaire</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>),
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">departement_id</span> <span class="sql-type">INT</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Positionnement de la colonne</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Ajouter en première position</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">id_temp</span> <span class="sql-type">INT</span> <span class="sql-keyword">FIRST</span>;

<span class="sql-comment">-- Ajouter après une colonne spécifique</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">prenom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>) <span class="sql-keyword">AFTER</span> <span class="sql-identifier">nom</span>;

<span class="sql-comment">-- Ajouter en dernière position (par défaut)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">notes</span> <span class="sql-type">TEXT</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Modification de colonnes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Modification de Colonnes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Changer le type de données</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Modifier le type (attention aux données existantes!)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">prix</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>);

<span class="sql-comment">-- Augmenter la taille d'une colonne VARCHAR</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>);

<span class="sql-comment">-- Changer les contraintes</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">montant</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>) <span class="sql-keyword">NOT NULL</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Changer le nom d'une colonne</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Renommer une colonne (syntaxe MySQL)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">CHANGE COLUMN</span> <span class="sql-identifier">ancien_nom</span> <span class="sql-identifier">nouveau_nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>);

<span class="sql-comment">-- Renommer avec changement de type</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">CHANGE COLUMN</span> <span class="sql-identifier">prix_ht</span> <span class="sql-identifier">prix_ttc</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>);

<span class="sql-comment">-- Syntaxe standard (autres SGBD)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">RENAME COLUMN</span> <span class="sql-identifier">ancien_nom</span> <span class="sql-reserved">TO</span> <span class="sql-identifier">nouveau_nom</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Suppression de colonnes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Suppression de Colonnes et Contraintes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Supprimer des colonnes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Supprimer une colonne (DANGEREUX!)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">colonne_inutile</span>;

<span class="sql-comment">-- Supprimer plusieurs colonnes</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ancienne_structure</span>
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">col1</span>,
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">col2</span>,
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">col3</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Gestion des contraintes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Ajouter une clé primaire</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD PRIMARY KEY</span> (<span class="sql-identifier">client_id</span>);

<span class="sql-comment">-- Ajouter une clé étrangère</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD CONSTRAINT</span> <span class="sql-identifier">fk_commandes_client</span>
<span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>);

<span class="sql-comment">-- Supprimer une clé étrangère</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">DROP FOREIGN KEY</span> <span class="sql-identifier">fk_commandes_client</span>;

<span class="sql-comment">-- Ajouter un index</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_nom</span> (<span class="sql-identifier">nom</span>);

<span class="sql-comment">-- Supprimer un index</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">DROP INDEX</span> <span class="sql-identifier">idx_nom</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Changement de nom et structure -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Changement de Nom et Structure</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Renommer une table</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Renommer une table</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ancien_nom</span>
<span class="sql-reserved">RENAME TO</span> <span class="sql-identifier">nouveau_nom</span>;

<span class="sql-comment">-- Syntaxe alternative</span>
<span class="sql-reserved">RENAME TABLE</span> <span class="sql-identifier">ancien_nom</span> <span class="sql-reserved">TO</span> <span class="sql-identifier">nouveau_nom</span>;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Changer le moteur de stockage</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Changer de InnoDB à MyISAM (déconseillé)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ma_table</span>
<span class="sql-reserved">ENGINE</span> <span class="sql-operator">=</span> <span class="sql-keyword">MyISAM</span>;

<span class="sql-comment">-- Changer vers InnoDB (recommandé)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ma_table</span>
<span class="sql-reserved">ENGINE</span> <span class="sql-operator">=</span> <span class="sql-keyword">InnoDB</span>;

<span class="sql-comment">-- Changer le charset et collation</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">CONVERT TO CHARACTER SET</span> utf8mb4
<span class="sql-reserved">COLLATE</span> utf8mb4_unicode_ci;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des index -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion Avancée des Index</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Types d'index</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Index unique</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">ADD UNIQUE INDEX</span> <span class="sql-identifier">uq_email</span> (<span class="sql-identifier">email</span>);

<span class="sql-comment">-- Index composite</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_client_date</span> (<span class="sql-identifier">client_id</span>, <span class="sql-identifier">date_commande</span>);

<span class="sql-comment">-- Index fulltext (pour la recherche)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">articles</span>
<span class="sql-reserved">ADD FULLTEXT</span> <span class="sql-identifier">ft_contenu</span> (<span class="sql-identifier">titre</span>, <span class="sql-identifier">contenu</span>);

<span class="sql-comment">-- Index spatial</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">localisations</span>
<span class="sql-reserved">ADD SPATIAL INDEX</span> <span class="sql-identifier">sp_position</span> (<span class="sql-identifier">coordonnees</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Optimisation des index</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Vérifier les index existants</span>
<span class="sql-reserved">SHOW INDEX FROM</span> <span class="sql-identifier">ma_table</span>;

<span class="sql-comment">-- Reconstruire un index (optimisation)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ma_table</span>
<span class="sql-reserved">DROP INDEX</span> <span class="sql-identifier">idx_nom</span>,
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_nom</span> (<span class="sql-identifier">nom</span>);

<span class="sql-comment">-- Désactiver les index temporairement</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ma_table</span>
<span class="sql-reserved">DISABLE KEYS</span>;
<span class="sql-comment">-- Opérations de chargement de données...</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ma_table</span>
<span class="sql-reserved">ENABLE KEYS</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Scénarios pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Scénarios Pratiques Réels</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Migration de schéma</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Scénario: Ajout d'un système de soft delete</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">deleted_at</span> <span class="sql-type">TIMESTAMP</span> <span class="sql-keyword">NULL DEFAULT NULL</span>,
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">deleted_by</span> <span class="sql-type">INT</span> <span class="sql-keyword">NULL DEFAULT NULL</span>,
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_deleted_at</span> (<span class="sql-identifier">deleted_at</span>);

<span class="sql-comment">-- Scénario: Normalisation de la base</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">adresse_livraison_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">NULL</span>,
<span class="sql-reserved">ADD CONSTRAINT</span> <span class="sql-identifier">fk_commandes_adresse</span>
<span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">adresse_livraison_id</span>) 
<span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">adresses</span>(<span class="sql-identifier">adresse_id</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Optimisation de performance</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Ajout d'index pour les requêtes fréquentes</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">logs</span>
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_date_niveau</span> (<span class="sql-identifier">date_creation</span>, <span class="sql-identifier">niveau</span>),
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_utilisateur_action</span> (<span class="sql-identifier">utilisateur_id</span>, <span class="sql-identifier">action</span>);

<span class="sql-comment">-- Partitionnement d'une grande table</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">ventes</span>
<span class="sql-reserved">PARTITION BY RANGE</span> (<span class="sql-function">YEAR</span>(<span class="sql-identifier">date_vente</span>)) (
  <span class="sql-reserved">PARTITION</span> <span class="sql-identifier">p2022</span> <span class="sql-reserved">VALUES LESS THAN</span> (<span class="sql-number">2023</span>),
  <span class="sql-reserved">PARTITION</span> <span class="sql-identifier">p2023</span> <span class="sql-reserved">VALUES LESS THAN</span> (<span class="sql-number">2024</span>),
  <span class="sql-reserved">PARTITION</span> <span class="sql-identifier">p2024</span> <span class="sql-reserved">VALUES LESS THAN</span> (<span class="sql-number">2025</span>)
);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des erreurs et sécurité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des Erreurs et Sécurité</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Erreurs courantes</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">--  Erreur: Colonne n'existe pas</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">colonne_inexistante</span>;
<span class="sql-comment">-- ERROR 1091: Can't DROP 'colonne_inexistante'; check that it exists</span>

<span class="sql-comment">--  Erreur: Violation de contrainte</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">client_id</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>);
<span class="sql-comment">-- ERROR 3780: Referencing column 'client_id' and referenced column...</span>

<span class="sql-comment">--  Erreur: Données incompatibles</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">produits</span>
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">prix</span> <span class="sql-type">INT</span>;
<span class="sql-comment">-- ERROR 1366: Incorrect integer value: '19.99' for column 'prix'</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques de sécurité</h3>
                    <div class="code-example">
                        <pre><code><span class="sql-comment">-- Utiliser des transactions quand possible</span>
<span class="sql-reserved">START TRANSACTION</span>;

<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">clients</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">nouvelle_colonne</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>);

<span class="sql-comment">-- Vérifier que tout s'est bien passé</span>
<span class="sql-reserved">SELECT</span> <span class="sql-keyword">*</span> <span class="sql-reserved">FROM</span> <span class="sql-identifier">information_schema</span>.<span class="sql-identifier">COLUMNS</span> 
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">TABLE_NAME</span> <span class="sql-operator">=</span> <span class="sql-string">'clients'</span>;

<span class="sql-reserved">COMMIT</span>;
<span class="sql-comment">-- Ou ROLLBACK en cas de problème</span>

<span class="sql-comment">-- Sauvegarde avant modification risquée</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">clients_backup_2024</span> 
<span class="sql-reserved">SELECT</span> <span class="sql-keyword">*</span> <span class="sql-reserved">FROM</span> <span class="sql-identifier">clients</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Optimisation d'une table existante</h3>
                    <p>Sur la table "utilisateurs" avec les colonnes : id, nom, email, date_creation</p>
                    <ul>
                        <li>Ajouter une colonne "telephone" de type VARCHAR(20) après "email"</li>
                        <li>Modifier la colonne "email" pour qu'elle soit UNIQUE et NOT NULL</li>
                        <li>Ajouter un index sur "date_creation"</li>
                        <li>Renommer la colonne "nom" en "nom_complet"</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Solution complète</span>
<span class="sql-reserved">START TRANSACTION</span>;

<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">telephone</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">20</span>) <span class="sql-keyword">AFTER</span> <span class="sql-identifier">email</span>,
<span class="sql-reserved">MODIFY COLUMN</span> <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
<span class="sql-reserved">ADD UNIQUE INDEX</span> <span class="sql-identifier">uq_email</span> (<span class="sql-identifier">email</span>),
<span class="sql-reserved">ADD INDEX</span> <span class="sql-identifier">idx_date_creation</span> (<span class="sql-identifier">date_creation</span>);

<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">utilisateurs</span>
<span class="sql-reserved">CHANGE COLUMN</span> <span class="sql-identifier">nom</span> <span class="sql-identifier">nom_complet</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>;

<span class="sql-reserved">COMMIT</span>;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Refactoring de base de données</h3>
                    <p>Vous devez restructurer une table "commandes" pour ajouter un système de statuts avancé :</p>
                    <ul>
                        <li>Ajouter une colonne "statut_id" de type INT</li>
                        <li>Créer une table "statuts_commandes" avec id, nom, description</li>
                        <li>Ajouter une clé étrangère entre les deux tables</li>
                        <li>Supprimer l'ancienne colonne "statut" de type VARCHAR</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="sql-comment">-- Solution étape par étape</span>
<span class="sql-reserved">START TRANSACTION</span>;

<span class="sql-comment">-- 1. Créer la nouvelle table de statuts</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">statuts_commandes</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">description</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>)
);

<span class="sql-comment">-- 2. Ajouter des statuts par défaut</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">statuts_commandes</span> (<span class="sql-identifier">nom</span>, <span class="sql-identifier">description</span>) <span class="sql-reserved">VALUES</span>
(<span class="sql-string">'en attente'</span>, <span class="sql-string">'Commande en attente de traitement'</span>),
(<span class="sql-string">'confirmée'</span>, <span class="sql-string">'Commande confirmée'</span>),
(<span class="sql-string">'expédiée'</span>, <span class="sql-string">'Commande expédiée'</span>),
(<span class="sql-string">'livrée'</span>, <span class="sql-string">'Commande livrée'</span>),
(<span class="sql-string">'annulée'</span>, <span class="sql-string">'Commande annulée'</span>);

<span class="sql-comment">-- 3. Ajouter la colonne statut_id à commandes</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD COLUMN</span> <span class="sql-identifier">statut_id</span> <span class="sql-type">INT</span>;

<span class="sql-comment">-- 4. Migrer les données existantes (exemple simplifié)</span>
<span class="sql-reserved">UPDATE</span> <span class="sql-identifier">commandes</span> <span class="sql-reserved">SET</span> <span class="sql-identifier">statut_id</span> <span class="sql-operator">=</span> <span class="sql-number">1</span> <span class="sql-reserved">WHERE</span> <span class="sql-identifier">statut</span> <span class="sql-operator">=</span> <span class="sql-string">'en attente'</span>;
<span class="sql-reserved">UPDATE</span> <span class="sql-identifier">commandes</span> <span class="sql-reserved">SET</span> <span class="sql-identifier">statut_id</span> <span class="sql-operator">=</span> <span class="sql-number">2</span> <span class="sql-reserved">WHERE</span> <span class="sql-identifier">statut</span> <span class="sql-operator">=</span> <span class="sql-string">'confirmée'</span>;
<span class="sql-comment">-- ... et ainsi de suite pour chaque statut</span>

<span class="sql-comment">-- 5. Ajouter la contrainte de clé étrangère</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD CONSTRAINT</span> <span class="sql-identifier">fk_commandes_statut</span>
<span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">statut_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">statuts_commandes</span>(<span class="sql-identifier">id</span>);

<span class="sql-comment">-- 6. Supprimer l'ancienne colonne (seulement après vérification)</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">DROP COLUMN</span> <span class="sql-identifier">statut</span>;

<span class="sql-reserved">COMMIT</span>;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Planification des modifications</h3>
                    <ul>
                        <li><strong>Toujours tester en dev</strong> avant la production</li>
                        <li><strong>Documenter les changements</strong> de schéma</li>
                        <li><strong>Utiliser des outils</strong> comme pt-online-schema-change pour les grosses tables
                        </li>
                        <li><strong>Planifier des fenêtres de maintenance</strong> pour les modifications bloquantes
                        </li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurité et rollback</h3>
                    <ul>
                        <li><strong>Sauvegarder les données</strong> avant toute modification risquée</li>
                        <li><strong>Utiliser des transactions</strong> quand c'est possible</li>
                        <li><strong>Prévoir un plan de rollback</strong> pour chaque modification</li>
                        <li><strong>Vérifier les dépendances</strong> (clés étrangères, vues, procédures)</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance</h3>
                    <ul>
                        <li><strong>Éviter les modifications inutiles</strong> sur de grosses tables</li>
                        <li><strong>Regrouper les ALTER TABLE</strong> en une seule commande quand possible</li>
                        <li><strong>Utiliser des index appropriés</strong> pour améliorer les performances</li>
                        <li><strong>Monitorer l'impact</strong> des modifications sur les performances</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        ALTER TABLE est un outil extrêmement puissant mais qui doit être utilisé avec prudence.
                        Une mauvaise utilisation peut causer des interruptions de service, des pertes de données
                        et des problèmes de performance.
                    </p>
                    <p>
                        <strong>Rappel crucial</strong> : En production, planifiez, testez et sauvegardez
                        toujours avant d'exécuter des commandes ALTER TABLE.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous aborderons les vues, les procédures stockées
                        et d'autres fonctionnalités avancées de MySQL.
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