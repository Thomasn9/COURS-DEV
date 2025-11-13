<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Création de Bases de Données avec MySQL</h1>
        <p class="lesson-meta text-white">SQL • MySQL • Bases de données relationnelles</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Bases de Données MySQL</h2>
        <p class="textExemple">
          MySQL est un système de gestion de bases de données relationnelles (SGBDR) open source très populaire. 
          Dans cette leçon, nous allons apprendre les concepts fondamentaux de la création et de la gestion 
          de bases de données avec MySQL.
        </p>
        <p class="textExemple">
          Une base de données est une collection organisée de données structurées, généralement stockées électroniquement 
          dans un système informatique. MySQL utilise le langage SQL (Structured Query Language) pour gérer ces données.
        </p>
      </section>

      <!-- Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Concepts Fondamentaux</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">1. Bases de données et tables</h3>
          <p>Dans MySQL :</p>
          <ul>
            <li>Une <strong>base de données</strong> est un conteneur qui regroupe des tables et d'autres objets</li>
            <li>Une <strong>table</strong> est une structure qui organise les données en lignes et colonnes</li>
            <li>Les <strong>colonnes</strong> définissent le type de données stockées</li>
            <li>Les <strong>lignes</strong> représentent des enregistrements individuels</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">2. Types de données courants</h3>
          <div class="code-comparison">
            <div>
              <h4>Types numériques</h4>
              <ul>
                <li><code>INT</code> - Entiers</li>
                <li><code>DECIMAL</code> - Nombres décimaux</li>
                <li><code>FLOAT</code> - Nombres à virgule flottante</li>
              </ul>
            </div>
            <div>
              <h4>Types texte</h4>
              <ul>
                <li><code>VARCHAR(n)</code> - Chaîne de longueur variable</li>
                <li><code>CHAR(n)</code> - Chaîne de longueur fixe</li>
                <li><code>TEXT</code> - Texte long</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- Création de base de données -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Création d'une Base de Données</h2>
        
        <div class="textExemple">
          <p>La commande de base pour créer une base de données est :</p>
          <div class="code-example">
            <pre><code><span class="sql-reserved">CREATE DATABASE</span> <span class="sql-identifier">nom_de_la_base</span>;</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Exemple pratique</h3>
          <p>Créons une base de données pour une bibliothèque :</p>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Création de la base de données "bibliotheque"</span>
<span class="sql-reserved">CREATE DATABASE</span> <span class="sql-identifier">bibliotheque</span>;

<span class="sql-comment">-- Sélectionner la base de données pour l'utiliser</span>
<span class="sql-reserved">USE</span> <span class="sql-identifier">bibliotheque</span>;</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Options avancées</h3>
          <p>Vous pouvez spécifier l'encodage des caractères :</p>
          <div class="code-example">
            <pre><code><span class="sql-reserved">CREATE DATABASE</span> <span class="sql-identifier">bibliotheque</span>
<span class="sql-reserved">CHARACTER SET</span> utf8mb4
<span class="sql-reserved">COLLATE</span> utf8mb4_unicode_ci;</code></pre>
          </div>
        </div>
      </section>

      <!-- Création de tables -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Création de Tables</h2>
        
        <div class="textExemple">
          <p>La syntaxe générale pour créer une table est :</p>
          <div class="code-example">
            <pre><code><span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">nom_table</span> (
  <span class="sql-identifier">colonne1</span> <span class="sql-type">type_donnees</span> <span class="sql-keyword">contraintes</span>,
  <span class="sql-identifier">colonne2</span> <span class="sql-type">type_donnees</span> <span class="sql-keyword">contraintes</span>,
  ...
);</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Exemple : Table "livres"</h3>
          <div class="code-example">
            <pre><code><span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">livres</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">titre</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">auteur</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">annee_publication</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">isbn</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">13</span>) <span class="sql-keyword">UNIQUE</span>,
  <span class="sql-identifier">date_ajout</span> <span class="sql-type">TIMESTAMP</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-function">CURRENT_TIMESTAMP</span>
);</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Contraintes courantes</h3>
          <div class="code-comparison">
            <div>
              <h4>Contraintes de base</h4>
              <ul>
                <li><code>PRIMARY KEY</code> - Clé primaire</li>
                <li><code>FOREIGN KEY</code> - Clé étrangère</li>
                <li><code>UNIQUE</code> - Valeurs uniques</li>
              </ul>
            </div>
            <div>
              <h4>Contraintes d'intégrité</h4>
              <ul>
                <li><code>NOT NULL</code> - Ne peut pas être vide</li>
                <li><code>DEFAULT</code> - Valeur par défaut</li>
                <li><code>CHECK</code> - Validation de données</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- Exemple complet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple Complet : Système de Bibliothèque</h2>
        
        <div class="textExemple">
          <p>Créons un système complet pour notre bibliothèque avec plusieurs tables :</p>
          <div class="code-example">
            <pre><code><span class="sql-comment">-- Table des livres</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">livres</span> (
  <span class="sql-identifier">livre_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">titre</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">auteur_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">genre</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>),
  <span class="sql-identifier">annee_publication</span> <span class="sql-type">YEAR</span>,
  <span class="sql-identifier">disponible</span> <span class="sql-type">BOOLEAN</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-constant">TRUE</span>
);

<span class="sql-comment">-- Table des auteurs</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">auteurs</span> (
  <span class="sql-identifier">auteur_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">pays</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>)
);

<span class="sql-comment">-- Table des membres</span>
<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">membres</span> (
  <span class="sql-identifier">membre_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">UNIQUE NOT NULL</span>,
  <span class="sql-identifier">date_inscription</span> <span class="sql-type">DATE</span> <span class="sql-keyword">DEFAULT</span> (<span class="sql-function">CURDATE</span>())
);

<span class="sql-comment">-- Ajout des clés étrangères</span>
<span class="sql-reserved">ALTER TABLE</span> <span class="sql-identifier">livres</span>
<span class="sql-reserved">ADD CONSTRAINT</span> <span class="sql-identifier">fk_livres_auteurs</span>
<span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">auteur_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">auteurs</span>(<span class="sql-identifier">auteur_id</span>);</code></pre>
          </div>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices Pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Création d'une base de données d'étudiants</h3>
          <p>Créez une base de données "universite" avec les tables suivantes :</p>
          <ul>
            <li><strong>etudiants</strong> : id, nom, prénom, email, date_naissance</li>
            <li><strong>cours</strong> : id, nom_cours, professeur, credits</li>
            <li><strong>inscriptions</strong> : id, etudiant_id, cours_id, date_inscription</li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="sql-reserved">CREATE DATABASE</span> <span class="sql-identifier">universite</span>;
<span class="sql-reserved">USE</span> <span class="sql-identifier">universite</span>;

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">etudiants</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">prenom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">50</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">UNIQUE</span>,
  <span class="sql-identifier">date_naissance</span> <span class="sql-type">DATE</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">cours</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom_cours</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">professeur</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>),
  <span class="sql-identifier">credits</span> <span class="sql-type">INT</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-number">3</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">inscriptions</span> (
  <span class="sql-identifier">id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">etudiant_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">cours_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date_inscription</span> <span class="sql-type">DATE</span> <span class="sql-keyword">DEFAULT</span> (<span class="sql-function">CURDATE</span>()),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">etudiant_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">etudiants</span>(<span class="sql-identifier">id</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">cours_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">cours</span>(<span class="sql-identifier">id</span>)
);</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Base de données e-commerce</h3>
          <p>Créez une base de données "boutique" avec au moins 3 tables liées pour gérer :</p>
          <ul>
            <li>Les produits</li>
            <li>Les clients</li>
            <li>Les commandes</li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="sql-reserved">CREATE DATABASE</span> <span class="sql-identifier">boutique</span>;
<span class="sql-reserved">USE</span> <span class="sql-identifier">boutique</span>;

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">clients</span> (
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">100</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">email</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">UNIQUE NOT NULL</span>,
  <span class="sql-identifier">telephone</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">20</span>),
  <span class="sql-identifier">adresse</span> <span class="sql-type">TEXT</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">produits</span> (
  <span class="sql-identifier">produit_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">nom</span> <span class="sql-type">VARCHAR</span>(<span class="sql-number">255</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">description</span> <span class="sql-type">TEXT</span>,
  <span class="sql-identifier">prix</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">stock</span> <span class="sql-type">INT</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-number">0</span>
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">commandes</span> (
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">client_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">date_commande</span> <span class="sql-type">DATETIME</span> <span class="sql-keyword">DEFAULT</span> <span class="sql-function">CURRENT_TIMESTAMP</span>,
  <span class="sql-identifier">statut</span> <span class="sql-type">ENUM</span>(<span class="sql-string">'en attente'</span>, <span class="sql-string">'confirmée'</span>, <span class="sql-string">'expédiée'</span>, <span class="sql-string">'livrée'</span>) <span class="sql-keyword">DEFAULT</span> <span class="sql-string">'en attente'</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">client_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">clients</span>(<span class="sql-identifier">client_id</span>)
);

<span class="sql-reserved">CREATE TABLE</span> <span class="sql-identifier">details_commande</span> (
  <span class="sql-identifier">detail_id</span> <span class="sql-type">INT</span> <span class="sql-keyword">AUTO_INCREMENT PRIMARY KEY</span>,
  <span class="sql-identifier">commande_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">produit_id</span> <span class="sql-type">INT</span>,
  <span class="sql-identifier">quantite</span> <span class="sql-type">INT</span> <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-identifier">prix_unitaire</span> <span class="sql-type">DECIMAL</span>(<span class="sql-number">10</span>, <span class="sql-number">2</span>) <span class="sql-keyword">NOT NULL</span>,
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">commande_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">commandes</span>(<span class="sql-identifier">commande_id</span>),
  <span class="sql-reserved">FOREIGN KEY</span> (<span class="sql-identifier">produit_id</span>) <span class="sql-reserved">REFERENCES</span> <span class="sql-identifier">produits</span>(<span class="sql-identifier">produit_id</span>)
);</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Bonnes pratiques et conclusion regroupées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Conventions de nommage</h3>
          <ul>
            <li>Utilisez des noms significatifs et cohérents</li>
            <li>Préférez le snake_case (ex: date_naissance)</li>
            <li>Évitez les mots réservés SQL comme noms</li>
            <li>Soyez cohérent dans le pluriel/singulier</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Optimisation</h3>
          <ul>
            <li>Choisissez les types de données appropriés</li>
            <li>Utilisez des clés primaires sur toutes les tables</li>
            <li>Ajoutez des index sur les colonnes fréquemment interrogées</li>
            <li>Normalisez vos données pour éviter la redondance</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Sécurité</h3>
          <ul>
            <li>Utilisez des contraintes pour valider les données</li>
            <li>Limitez les privilèges des utilisateurs de la base</li>
            <li>Sauvegardez régulièrement vos bases de données</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Conclusion</h3>
          <p>
            Vous avez maintenant les bases pour créer des bases de données MySQL fonctionnelles. 
            La création de bases de données bien structurées est fondamentale pour le développement 
            d'applications robustes et performantes.
          </p>
          <p>
            Dans les prochaines leçons, nous aborderons l'insertion, la modification et l'interrogation 
            des données avec les commandes SELECT, INSERT, UPDATE et DELETE.
          </p>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonMySQL',
  data() {
    return {
      lessonTitle: 'Création de Bases de Données avec MySQL'
    }
  },
  head() {
    return {
      title: this.lessonTitle,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez à créer des bases de données MySQL avec cette leçon complète incluant syntaxe, exemples et exercices pratiques.'
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

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* COULEURS MYSQL WORKBENCH */
.sql-reserved { color: #FF6B8B !important; font-weight: bold; } /* Mots réservés (CREATE, DATABASE, TABLE, etc.) */
.sql-keyword { color: #4FC1FF !important; } /* Mots-clés (AUTO_INCREMENT, PRIMARY KEY, etc.) */
.sql-identifier { color: #9CDCFE !important; } /* Identifiants (noms de tables, colonnes) */
.sql-type { color: #4EC9B0 !important; } /* Types de données (INT, VARCHAR, etc.) */
.sql-string { color: #CE9178 !important; } /* Chaînes de caractères */
.sql-comment { color: #6A9955 !important; font-style: italic; } /* Commentaires */
.sql-function { color: #DCDCAA !important; } /* Fonctions SQL */
.sql-number { color: #B5CEA8 !important; } /* Nombres */
.sql-constant { color: #569CD6 !important; } /* Constantes (TRUE, FALSE, NULL) */

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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>