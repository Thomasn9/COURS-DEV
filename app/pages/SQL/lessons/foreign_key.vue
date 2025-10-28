<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Clés Étrangères (Foreign Keys) en SQL</h1>
        <p class="lesson-meta text-white">SQL • MySQL • Intégrité référentielle • Relations entre tables</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Clés Étrangères</h2>
        <p class="textExemple">
          Les clés étrangères (Foreign Keys) sont un concept fondamental des bases de données relationnelles 
          qui permet de créer des liens entre les tables et de maintenir l'intégrité référentielle des données.
        </p>
        <p class="textExemple">
          Une clé étrangère établit une relation entre une colonne (ou un ensemble de colonnes) d'une table 
          et la clé primaire d'une autre table, garantissant ainsi la cohérence des données.
        </p>
      </section>

      <!-- Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Concepts Fondamentaux</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Définitions importantes</h3>
          <ul>
            <li><strong>Clé étrangère</strong> : Colonne(s) qui référence(nt) la clé primaire d'une autre table</li>
            <li><strong>Table parent</strong> : Table contenant la clé primaire référencée</li>
            <li><strong>Table enfant</strong> : Table contenant la clé étrangère</li>
            <li><strong>Intégrité référentielle</strong> : Assurance que les relations entre tables restent cohérentes</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Exemple de relation</h3>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Table parent (référencée)</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>)
);

<span class="sql-comment">-- Table enfant (qui référence)</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">PRIMARY KEY</span>,
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>)
);</code></pre>
          </div>
        </div>
      </section>

      <!-- Pourquoi les Foreign Keys sont essentielles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">⚠️ Pourquoi les Foreign Keys sont Essentielles</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Le problème sans Foreign Keys</h3>
          <p>
            Sans contraintes de clés étrangères, votre base de données peut contenir des données incohérentes 
            et des références brisées, ce qui constitue une <strong>mauvaise pratique</strong> dangereuse.
          </p>
          
          <div class="warning-section">
            <h4 class="text-purple">🚫 Problèmes sans Foreign Keys</h4>
            <div class="code-comparison">
              <div>
                <h5>Mauvaise pratique</h5>
                <div class="code-example">
                  <pre><code><span class="sql-comment">-- Sans FOREIGN KEY</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span> <span class="sql-comment">-- Pas de contrainte!</span>
);

<span class="sql-comment">-- Insertion possible d'une commande</span>
<span class="sql-comment">-- pour un client qui n'existe pas! 😱</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> <span class="sql-reserved">VALUES</span> (<span class="sql-number">1</span>, <span class="sql-number">999</span>);</code></pre>
                </div>
                <p class="warning-text">➡️ Données incohérentes et références brisées</p>
              </div>
              <div>
                <h5>Bonne pratique</h5>
                <div class="code-example">
                  <pre><code><span class="sql-comment">-- Avec FOREIGN KEY</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>)
);

<span class="sql-comment">-- Insertion bloquée si client_id=999</span>
<span class="sql-comment">-- n'existe pas dans la table clients ✅</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> <span class="sql-reserved">VALUES</span> (<span class="sql-number">1</span>, <span class="sql-number">999</span>);</code></pre>
                </div>
                <p class="success-text">➡️ Intégrité des données garantie</p>
              </div>
            </div>
          </div>

          <div class="textExemple">
            <h4 class="text-purple">📊 Conséquences de l'absence de Foreign Keys</h4>
            <ul>
              <li><strong>Données orphelines</strong> : Enregistrements qui référencent des données inexistantes</li>
              <li><strong>Incohérences métier</strong> : Commandes sans clients, employés sans département, etc.</li>
              <li><strong>Difficulté d'analyse</strong> : Résultats de requêtes incorrects ou incomplets</li>
              <li><strong>Problèmes de suppression</strong> : Impossible de nettoyer proprement les données</li>
            </ul>
          </div>

          <div class="textExemple">
            <h4 class="text-purple">🔧 Impact sur la maintenance</h4>
            <div class="code-example">
              <pre><code><span class="sql-comment">-- Sans FK, difficile de savoir quelles données nettoyer</span>
<span class="sql-reserved">DELETE FROM</span> <span class="sql-identifier">clients</span> <span class="sql-reserved">WHERE</span> <span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-number">123</span>;

<span class="sql-comment">-- Les commandes du client 123 deviennent orphelines</span>
<span class="sql-comment">-- Personne ne sait qui a passé ces commandes! 😵</span></code></pre>
            </div>
            <p>
              Avec les Foreign Keys, la base de données vous protège automatiquement contre ce type de problème.
            </p>
          </div>

          <div class="textExemple">
            <h4 class="text-purple">🛡️ Avantages des Foreign Keys</h4>
            <ul>
              <li><strong>Intégrité des données</strong> : Garantie que toutes les références sont valides</li>
              <li><strong>Documentation automatique</strong> : Les relations entre tables sont explicites</li>
              <li><strong>Meilleures performances</strong> : Optimisation des jointures par le SGBD</li>
              <li><strong>Maintenance simplifiée</strong> : Nettoyage et mise à jour cohérents des données</li>
            </ul>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">✅ Quand éviter les Foreign Keys (cas rares)</h3>
          <ul>
            <li>Tables de logging ou d'audit à très haute fréquence d'écriture</li>
            <li>Bases de données distribuées complexes</li>
            <li>Scénarios de chargement de données massives temporaires</li>
            <li>Tables de configuration statiques sans relations complexes</li>
          </ul>
          <p><strong>En production, utilisez toujours les Foreign Keys pour les relations importantes !</strong></p>
        </div>
      </section>

      <!-- Syntaxe de création -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de Création des Foreign Keys</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Méthode 1 : Directement dans CREATE TABLE</h3>
          <div class="code-example">
            <pre><code><span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">nom_table</span> (
  <span class="sql-identifier">colonne1</span> <span class="sql-type">type_donnees</span>,
  <span class="sql-identifier">colonne2</span> <span class="sql-type">type_donnees</span>,
  ...
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">colonne_etrangere</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">table_parent</span>(<span class="sql-identifier">colonne_primaire</span>)
);</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Méthode 2 : Avec ALTER TABLE</h3>
          <div class="code-example">
            <pre><code><span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">nom_table</span>
<span class="sql-reserved">ADD CONSTRAINT</span> <span class="sql-identifier">nom_contrainte</span>
<span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">colonne_etrangere</span>) 
<span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">table_parent</span>(<span class="sql-identifier">colonne_primaire</span>);</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Exemple complet</h3>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Tables parentes</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">UNIQUE</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">produits</span> (
  <span class="sql-identifier">produit_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">prix</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>)
);

<span class="sql-comment">-- Table enfant avec multiples Foreign Keys</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">produit_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">quantite</span> <span class="sql-type">INT</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-number">1</span>,
  <span class="sql-identifier">date_commande</span> <span class="sql-type">DATETIME</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-function">CURRENT_TIMESTAMP</span>,
  
  <span class="sql-comment">-- Foreign Keys définies inline</span>
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">produit_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">produits</span>(<span class="sql-identifier">produit_id</span>)
);</code></pre>
          </div>
        </div>
      </section>

      <!-- Actions référentielles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Actions Référentielles (ON DELETE / ON UPDATE)</h2>
        
        <div class="textExemple">
          <p>Les actions référentielles définissent le comportement lors de la suppression ou modification des données parentes :</p>
          <div class="code-example">
            <pre><code><span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">colonne</span>) 
<span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">table_parent</span>(<span class="sql-identifier">colonne_primaire</span>)
<span class="sql-reserved">ON DELETE</span> <span class="sql-identifier">action</span>
<span class="sql-reserved">ON UPDATE</span> <span class="sql-identifier">action</span>;</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Options ON DELETE</h3>
          <div class="code-comparison">
            <div>
              <h4>RESTRICT (Défaut)</h4>
              <div class="code-example">
                <pre><code><span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">RESTRICT</span></code></pre>
              </div>
              <p>Empêche la suppression si des enregistrements enfants existent</p>
            </div>
            <div>
              <h4>CASCADE</h4>
              <div class="code-example">
                <pre><code><span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">CASCADE</span></code></pre>
              </div>
              <p>Supprime automatiquement les enregistrements enfants</p>
            </div>
          </div>

          <div class="code-comparison">
            <div>
              <h4>SET NULL</h4>
              <div class="code-example">
                <pre><code><span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">SET NULL</span></code></pre>
              </div>
              <p>Met la clé étrangère à NULL chez les enfants</p>
            </div>
            <div>
              <h4>NO ACTION</h4>
              <div class="code-example">
                <pre><code><span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">NO ACTION</span></code></pre>
              </div>
              <p>Similaire à RESTRICT (vérification différée)</p>
            </div>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Exemples pratiques</h3>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Suppression en cascade pour les relations fortes</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">details_commande</span> (
  <span class="sql-identifier">detail_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">PRIMARY KEY</span>,
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">commande_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">commandes</span>(<span class="sql-identifier">commande_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">CASCADE</span>
);

<span class="sql-comment">-- SET NULL pour les relations optionnelles</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">employes</span> (
  <span class="sql-identifier">employe_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">PRIMARY KEY</span>,
  <span class="sql-identifier">manager_id</span> <span class="sql-type">INT</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">manager_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">employes</span>(<span class="sql-identifier">employe_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">SET NULL</span>
);</code></pre>
          </div>
        </div>
      </section>

      <!-- Contraintes nommées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Contraintes Nommées et Bonnes Pratiques</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Nommer les contraintes Foreign Key</h3>
          <p>Il est recommandé de nommer explicitement les contraintes pour une meilleure maintenance :</p>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Avec ALTER TABLE</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">ADD CONSTRAINT</span> <span class="sql-identifier">fk_commandes_client</span>
<span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) 
<span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>);

<span class="sql-comment">-- Dans CREATE TABLE</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">PRIMARY KEY</span>,
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span>,
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_commandes_client</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>)
);</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Conventions de nommage</h3>
          <ul>
            <li><code>fk_enfant_parent</code> - Format recommandé</li>
            <li><code>fk_tableenfant_tableparent_colonne</code> - Plus explicite</li>
            <li>Soyez cohérent dans toute la base de données</li>
          </ul>
        </div>
      </section>

      <!-- Gestion des erreurs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Gestion des Erreurs et Contraintes</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Erreurs courantes avec les Foreign Keys</h3>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- ❌ Erreur : Violation de contrainte FK</span>
<span class="sql-reserved">INSERT INTO</span> <span class="sql-identifier">commandes</span> (<span class="sql-identifier">client_id</span>, <span class="sql-identifier">produit_id</span>) 
<span class="sql-reserved">VALUES</span> (<span class="sql-number">999</span>, <span class="sql-number">1</span>);
<span class="sql-comment">-- ERROR 1452: Cannot add or update a child row: a foreign key constraint fails</span>

<span class="sql-comment">-- ❌ Erreur : Suppression bloquée par RESTRICT</span>
<span class="sql-reserved">DELETE FROM</span> <span class="sql-identifier">clients</span> <span class="sql-reserved">WHERE</span> <span class="sql-identifier">client_id</span> <span class="sql-operator">=</span> <span class="sql-number">1</span>;
<span class="sql-comment">-- ERROR 1451: Cannot delete or update a parent row: a foreign key constraint fails</span></code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Vérification et suppression des contraintes</h3>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Voir toutes les Foreign Keys d'une table</span>
<span class="sql-reserved">SELECT</span> 
  <span class="sql-identifier">TABLE_NAME</span>,
  <span class="sql-identifier">COLUMN_NAME</span>,
  <span class="sql-identifier">CONSTRAINT_NAME</span>,
  <span class="sql-identifier">REFERENCED_TABLE_NAME</span>,
  <span class="sql-identifier">REFERENCED_COLUMN_NAME</span>
<span class="sql-reserved">FROM</span> <span class="sql-identifier">information_schema</span>.<span class="sql-identifier">KEY_COLUMN_USAGE</span>
<span class="sql-reserved">WHERE</span> <span class="sql-identifier">REFERENCED_TABLE_SCHEMA</span> <span class="sql-operator">=</span> <span class="sql-string">'ma_base'</span>
  <span class="sql-reserved">AND</span> <span class="sql-identifier">REFERENCED_TABLE_NAME</span> <span class="sql-operator">=</span> <span class="sql-string">'clients'</span>;

<span class="sql-comment">-- Supprimer une Foreign Key</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">commandes</span>
<span class="sql-reserved">DROP FOREIGN KEY</span> <span class="sql-identifier">fk_commandes_client</span>;</code></pre>
          </div>
        </div>
      </section>

      <!-- Exemple complet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple Complet : Système de Gestion d'École</h2>
        
        <div class="textExemple">
          <p>Création d'un système complet avec multiples relations :</p>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Tables de référence</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">etudiants</span> (
  <span class="sql-identifier">etudiant_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">prenom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">date_naissance</span> <span class="sql-type">DATE</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">cours</span> (
  <span class="sql-identifier">cours_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">titre</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">credits</span> <span class="sql-type">INT</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-number">3</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">professeurs</span> (
  <span class="sql-identifier">professeur_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">specialite</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>)
);

<span class="sql-comment">-- Tables de relation avec Foreign Keys</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">inscriptions</span> (
  <span class="sql-identifier">inscription_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">etudiant_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">cours_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">date_inscription</span> <span class="sql-type">DATE</span> <span class="sql-keyword">DEFAULT</span> (<span class="sql-function">CURDATE</span>()),
  <span class="sql-identifier">note</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">4</span>, <span class="sql-number">2</span>),
  
  <span class="sql-comment">-- Contraintes nommées avec actions</span>
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_inscriptions_etudiant</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">etudiant_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">etudiants</span>(<span class="sql-identifier">etudiant_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">CASCADE</span>,
    
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_inscriptions_cours</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">cours_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">cours</span>(<span class="sql-identifier">cours_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">RESTRICT</span>,
    
  <span class="sql-comment">-- Clé unique composite</span>
  <span class="sql-reserved">UNIQUE KEY</span> <span class="sql-identifier">uk_etudiant_cours</span> (<span class="sql-identifier">etudiant_id</span>, <span class="sql-identifier">cours_id</span>)
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">cours_professeurs</span> (
  <span class="sql-identifier">cours_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">professeur_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">annee</span> <span class="sql-type">YEAR</span>,
  
  <span class="sql-reserved">PRIMARY KEY</span> (<span class="sql-identifier">cours_id</span>, <span class="sql-identifier">professeur_id</span>, <span class="sql-identifier">annee</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">cours_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">cours</span>(<span class="sql-identifier">cours_id</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">professeur_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">professeurs</span>(<span class="sql-identifier">professeur_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">SET NULL</span>
);</code></pre>
          </div>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices Pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Système de Bibliothèque</h3>
          <p>Créez les tables suivantes avec les Foreign Keys appropriées :</p>
          <ul>
            <li><strong>livres</strong> : livre_id (PK), titre, auteur_id, categorie_id</li>
            <li><strong>auteurs</strong> : auteur_id (PK), nom, pays</li>
            <li><strong>categories</strong> : categorie_id (PK), nom_categorie</li>
            <li><strong>emprunts</strong> : emprunt_id (PK), livre_id, membre_id, date_emprunt</li>
            <li><strong>membres</strong> : membre_id (PK), nom, email</li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">auteurs</span> (
  <span class="sql-identifier">auteur_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">pays</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>)
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">categories</span> (
  <span class="sql-identifier">categorie_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom_categorie</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">membres</span> (
  <span class="sql-identifier">membre_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">UNIQUE</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">livres</span> (
  <span class="sql-identifier">livre_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">titre</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">auteur_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">categorie_id</span> <span class="sql-type">INT</span>,
  
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_livres_auteur</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">auteur_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">auteurs</span>(<span class="sql-identifier">auteur_id</span>),
    
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_livres_categorie</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">categorie_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">categories</span>(<span class="sql-identifier">categorie_id</span>)
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">emprunts</span> (
  <span class="sql-identifier">emprunt_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">livre_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">membre_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date_emprunt</span> <span class="sql-type">DATE</span> <span class="sql-keyword">DEFAULT</span> (<span class="sql-function">CURDATE</span>()),
  <span class="sql-identifier">date_retour</span> <span class="sql-type">DATE</span>,
  
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_emprunts_livre</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">livre_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">livres</span>(<span class="sql-identifier">livre_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">RESTRICT</span>,
    
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_emprunts_membre</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">membre_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">membres</span>(<span class="sql-identifier">membre_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">CASCADE</span>
);</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Gestion de Projet</h3>
          <p>Créez un système de gestion de projet avec les relations suivantes :</p>
          <ul>
            <li>Un projet a un chef de projet (employé)</li>
            <li>Un employé peut travailler sur plusieurs projets</li>
            <li>Un projet a plusieurs tâches</li>
            <li>Une tâche est assignée à un employé</li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">employes</span> (
  <span class="sql-identifier">employe_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">poste</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>)
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">projets</span> (
  <span class="sql-identifier">projet_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom_projet</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">chef_projet_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date_debut</span> <span class="sql-type">DATE</span>,
  <span class="sql-identifier">date_fin</span> <span class="sql-type">DATE</span>,
  
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_projets_chef</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">chef_projet_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">employes</span>(<span class="sql-identifier">employe_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">SET NULL</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">taches</span> (
  <span class="sql-identifier">tache_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">projet_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">employe_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">description</span> <span class="sql-type">TEXT</span>,
  <span class="sql-identifier">statut</span> <span class="sql-type">ENUM</span>(<span class="sql-string">'en attente'</span>, <span class="sql-string">'en cours'</span>, <span class="sql-string">'terminée'</span>),
  
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_taches_projet</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">projet_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">projets</span>(<span class="sql-identifier">projet_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">CASCADE</span>,
    
  <span class="sql-reserved">CONSTRAINT</span> <span class="sql-identifier">fk_taches_employe</span>
    <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">employe_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">employes</span>(<span class="sql-identifier">employe_id</span>)
    <span class="sql-reserved">ON DELETE</span> <span class="sql-keyword">SET NULL</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">employes_projets</span> (
  <span class="sql-identifier">employe_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">projet_id</span> <span class="sql-type">INT</span>,
  
  <span class="sql-reserved">PRIMARY KEY</span> (<span class="sql-identifier">employe_id</span>, <span class="sql-identifier">projet_id</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">employe_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">employes</span>(<span class="sql-identifier">employe_id</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">projet_id</span>) 
    <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">projets</span>(<span class="sql-identifier">projet_id</span>)
);</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Bonnes pratiques et conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Conception des relations</h3>
          <ul>
            <li><strong>Toujours utiliser des Foreign Keys</strong> pour les relations importantes</li>
            <li>Choisir les actions ON DELETE/ON UPDATE appropriées au métier</li>
            <li>Nommer systématiquement les contraintes pour faciliter la maintenance</li>
            <li>Vérifier la cohérence des types de données entre clés primaires et étrangères</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Performance et maintenance</h3>
          <ul>
            <li>Indexer les colonnes de clés étrangères pour optimiser les jointures</li>
            <li>Utiliser CASCADE avec prudence (peut supprimer beaucoup de données)</li>
            <li>Documenter les relations complexes dans un schéma de base de données</li>
            <li>Vérifier régulièrement l'intégrité référentielle avec des requêtes de validation</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Sécurité et robustesse</h3>
          <ul>
            <li>Les Foreign Keys protègent contre les données incohérentes</li>
            <li>Elles documentent automatiquement la structure des données</li>
            <li>Elles améliorent la qualité des données et la confiance dans le système</li>
            <li>Elles facilitent les opérations de nettoyage et d'archivage</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Conclusion</h3>
          <p>
            Les clés étrangères sont un pilier fondamental des bases de données relationnelles. 
            Elles garantissent l'intégrité des données, documentent les relations entre tables 
            et améliorent la qualité globale du système.
          </p>
          <p>
            <strong>Rappel important</strong> : Ne négligez jamais les Foreign Keys dans vos conceptions. 
            Le temps gagné en les omettant sera largement perdu en débogage et correction de données corrompues.
          </p>
          <p>
            Dans les prochaines leçons, nous aborderons les index, les vues et les procédures stockées 
            pour compléter votre maîtrise des bases de données SQL.
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

/* COULEURS MYSQL WORKBENCH POUR SQL */
.sql-reserved { color: #FF6B8B !important; font-weight: bold; } /* Mots réservés */
.sql-keyword { color: #4FC1FF !important; } /* Mots-clés */
.sql-identifier { color: #9CDCFE !important; } /* Identifiants */
.sql-type { color: #4EC9B0 !important; } /* Types de données */
.sql-string { color: #CE9178 !important; } /* Chaînes de caractères */
.sql-comment { color: #6A9955 !important; font-style: italic; } /* Commentaires */
.sql-function { color: #DCDCAA !important; } /* Fonctions SQL */
.sql-number { color: #B5CEA8 !important; } /* Nombres */
.sql-constant { color: #569CD6 !important; } /* Constantes */
.sql-operator { color: #D4D4D4 !important; } /* Opérateurs */

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