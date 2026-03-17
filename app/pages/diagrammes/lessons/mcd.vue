<template>
  <div class="lesson-container">
    <div class="lesson-content">

      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Modèles Conceptuels de Données (MCD)</h1>
        <p class="lesson-meta text-white">Conception de bases de données - Mérise</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p>Le Modèle Conceptuel de Données (MCD) est une représentation graphique qui permet de décrire les données d'un système d'information et les liens qui existent entre elles, <strong>indépendamment de toute considération technique</strong>.</p>
        <p>Issu de la méthode Merise, le MCD répond à la question : <em>« Quelles informations le système doit-il mémoriser ? »</em>. Il constitue la première étape incontournable avant de concevoir une base de données relationnelle.</p>
      </section>

      <!-- Concepts fondamentaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les concepts fondamentaux</h2>
        <p>Un MCD repose sur trois éléments principaux : les <strong>entités</strong>, les <strong>associations</strong> et les <strong>propriétés</strong>.</p>

        <div class="code-comparison">
          <div class="code-block">
            <h3 class="text-purple">🟦 L'entité</h3>
            <p>Une entité représente un objet concret ou abstrait du monde réel sur lequel on veut mémoriser des informations. Elle regroupe des individus partageant les mêmes caractéristiques.</p>
            <pre><code><span class="comment">-- Exemples d'entités</span>
<span class="class-name">CLIENT</span>
<span class="class-name">PRODUIT</span>
<span class="class-name">COMMANDE</span>
<span class="class-name">EMPLOYE</span>

<span class="comment">-- Chaque entité possède un identifiant</span>
<span class="comment">-- unique (souligné dans le schéma)</span>
<span class="class-name">CLIENT</span>
├── <span class="keyword">idClient</span> <span class="comment">(identifiant)</span>
├── <span class="variable">nom</span>
├── <span class="variable">prenom</span>
└── <span class="variable">email</span></code></pre>
          </div>

          <div class="code-block">
            <h3 class="text-purple">🔗 L'association</h3>
            <p>Une association exprime un lien sémantique entre deux ou plusieurs entités. Elle représente un fait du monde réel qui met en relation ces entités.</p>
            <pre><code><span class="comment">-- Exemples d'associations</span>
<span class="class-name">CLIENT</span> <span class="function">PASSE</span> <span class="class-name">COMMANDE</span>
<span class="class-name">COMMANDE</span> <span class="function">CONTIENT</span> <span class="class-name">PRODUIT</span>
<span class="class-name">EMPLOYE</span> <span class="function">TRAVAILLE DANS</span> <span class="class-name">SERVICE</span>

<span class="comment">-- Une association peut avoir</span>
<span class="comment">-- des propriétés propres</span>
<span class="function">CONTIENT</span>
└── <span class="variable">quantite</span>
└── <span class="variable">prixUnitaire</span></code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">📌 La propriété</h3>
          <p>Une propriété (ou attribut) est une donnée élémentaire qui caractérise une entité ou une association. Elle doit être <strong>atomique</strong> (non décomposable) et <strong>non redondante</strong>.</p>
          <pre><code><span class="comment">-- Propriétés de l'entité PRODUIT</span>
<span class="class-name">PRODUIT</span>
├── <span class="keyword">idProduit</span>        <span class="comment">← Identifiant unique</span>
├── <span class="variable">libelle</span>          <span class="comment">← Nom du produit</span>
├── <span class="variable">description</span>      <span class="comment">← Description textuelle</span>
├── <span class="number">prix</span>             <span class="comment">← Prix unitaire HT</span>
└── <span class="variable">categorie</span>        <span class="comment">← Catégorie du produit</span>

<span class="comment">-- RÈGLE : une propriété ne doit pas</span>
<span class="comment">-- être calculable depuis d'autres propriétés</span>
<span class="comment">-- Ex: "age" est à éviter → préférer "dateNaissance"</span></code></pre>
        </div>
      </section>

      <!-- Les cardinalités -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les cardinalités</h2>
        <p>Les cardinalités indiquent le <strong>nombre minimum et maximum de fois</strong> qu'une occurrence d'une entité peut participer à une association. Elles se notent sous la forme <code>min,max</code> de chaque côté de l'association.</p>

        <div class="code-example">
          <h3 class="text-purple">Notation des cardinalités</h3>
          <pre><code><span class="comment">-- Cardinalités possibles</span>
<span class="keyword">0,1</span>  <span class="comment">→ zéro ou une fois (optionnel, unique)</span>
<span class="keyword">1,1</span>  <span class="comment">→ exactement une fois (obligatoire, unique)</span>
<span class="keyword">0,N</span>  <span class="comment">→ zéro ou plusieurs fois (optionnel, multiple)</span>
<span class="keyword">1,N</span>  <span class="comment">→ une ou plusieurs fois (obligatoire, multiple)</span>

<span class="comment">---------------------------------------------------</span>
<span class="comment">-- Exemple de lecture</span>
<span class="comment">---------------------------------------------------</span>

<span class="class-name">CLIENT</span> <span class="keyword">1,N</span> ——— <span class="function">PASSE</span> ——— <span class="keyword">1,1</span> <span class="class-name">COMMANDE</span>

<span class="comment">→ Un CLIENT passe entre 1 et N commandes</span>
<span class="comment">→ Une COMMANDE est passée par exactement 1 client</span></code></pre>
        </div>

        <div class="code-comparison">
          <div class="code-block">
            <h3 class="text-purple">Relation 1-1 (un à un)</h3>
            <p>Chaque occurrence d'une entité est liée à au plus une occurrence de l'autre entité.</p>
            <pre><code><span class="class-name">PERSONNE</span> <span class="keyword">1,1</span> — <span class="function">POSSEDE</span> — <span class="keyword">0,1</span> <span class="class-name">PASSEPORT</span>

<span class="comment">→ Une personne possède</span>
<span class="comment">  au plus un passeport</span>
<span class="comment">→ Un passeport appartient</span>
<span class="comment">  à une seule personne</span></code></pre>
          </div>

          <div class="code-block">
            <h3 class="text-purple">Relation 1-N (un à plusieurs)</h3>
            <p>Une occurrence d'une entité est liée à plusieurs occurrences de l'autre entité.</p>
            <pre><code><span class="class-name">CATEGORIE</span> <span class="keyword">1,1</span> — <span class="function">CLASSE</span> — <span class="keyword">1,N</span> <span class="class-name">PRODUIT</span>

<span class="comment">→ Un produit appartient</span>
<span class="comment">  à une seule catégorie</span>
<span class="comment">→ Une catégorie contient</span>
<span class="comment">  plusieurs produits</span></code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Relation N-N (plusieurs à plusieurs)</h3>
          <p>Plusieurs occurrences d'une entité peuvent être liées à plusieurs occurrences de l'autre entité. Ce type de relation génère une <strong>table intermédiaire</strong> lors du passage au MLD.</p>
          <pre><code><span class="class-name">COMMANDE</span> <span class="keyword">1,N</span> ——— <span class="function">CONTIENT</span> ——— <span class="keyword">1,N</span> <span class="class-name">PRODUIT</span>
                        |
                        └── <span class="variable">quantite</span>
                        └── <span class="variable">prixUnitaire</span>

<span class="comment">→ Une commande contient un ou plusieurs produits</span>
<span class="comment">→ Un produit figure dans une ou plusieurs commandes</span>
<span class="comment">→ L'association "CONTIENT" porte ses propres propriétés</span></code></pre>
        </div>
      </section>

      <!-- Exemple complet de MCD -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple complet : Système de commandes</h2>
        <p>Voici un MCD complet modélisant un système de gestion de commandes en ligne, avec toutes ses entités, associations et cardinalités.</p>

        <div class="code-example">
          <h3 class="text-purple">Représentation textuelle du MCD</h3>
          <pre><code><span class="comment">╔══════════════╗         ╔══════════════════╗         ╔═════════════╗</span>
<span class="comment">║   CLIENT     ║         ║     COMMANDE     ║         ║   PRODUIT   ║</span>
<span class="comment">╠══════════════╣         ╠══════════════════╣         ╠═════════════╣</span>
<span class="keyword">║ #idClient    ║</span>         <span class="keyword">║ #idCommande      ║</span>         <span class="keyword">║ #idProduit  ║</span>
<span class="variable">║ nom          ║</span>         <span class="variable">║ dateCommande     ║</span>         <span class="variable">║ libelle     ║</span>
<span class="variable">║ prenom       ║</span>         <span class="variable">║ statut           ║</span>         <span class="number">║ prix        ║</span>
<span class="variable">║ email        ║</span>         <span class="variable">║ adresseLivraison ║</span>         <span class="variable">║ stock       ║</span>
<span class="variable">║ telephone    ║</span>         <span class="comment">╚══════════════════╝</span>         <span class="comment">╚═════════════╝</span>
<span class="comment">╚══════════════╝</span>
       |                        |                           |
     <span class="keyword">1,N</span>                      <span class="keyword">1,1</span>                         <span class="keyword">1,N</span>
       |                        |                           |
    <span class="function">PASSE</span>                  (clé FK)                    <span class="function">CONTIENT</span>
       |                                                    |
     <span class="keyword">0,N</span>                                                 <span class="keyword">1,N</span>
                                               (quantite, prixUnitaire)

<span class="comment">-- Entité CATEGORIE reliée à PRODUIT</span>
<span class="comment">╔══════════════╗</span>
<span class="comment">║  CATEGORIE   ║</span>
<span class="comment">╠══════════════╣</span>
<span class="keyword">║ #idCategorie ║</span>
<span class="variable">║ nomCategorie ║</span>
<span class="variable">║ description  ║</span>
<span class="comment">╚══════════════╝</span>
       |
     <span class="keyword">1,1</span>
       |
  <span class="function">APPARTIENT</span>
       |
     <span class="keyword">1,N</span>
       |
  <span class="class-name">PRODUIT</span></code></pre>
        </div>
      </section>

      <!-- Du MCD au MLD -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Du MCD au MLD : les règles de transformation</h2>
        <p>Le Modèle Logique de Données (MLD) est la traduction du MCD en tables relationnelles. Les règles de transformation sont les suivantes :</p>

        <div class="code-example">
          <h3 class="text-purple">Règle 1 — Entité → Table</h3>
          <p>Chaque entité devient une table. Son identifiant devient la <strong>clé primaire (PK)</strong>.</p>
          <pre><code><span class="comment">-- MCD</span>
<span class="class-name">CLIENT</span> (<span class="keyword">#idClient</span>, nom, prenom, email)

<span class="comment">-- MLD résultant</span>
<span class="function">CLIENT</span> (<span class="keyword">idClient</span> PK, nom, prenom, email)</code></pre>
        </div>

        <div class="code-comparison">
          <div class="code-block">
            <h3 class="text-purple">Règle 2 — Relation 1,N → Clé étrangère</h3>
            <p>L'entité côté <code>1,1</code> reçoit la clé primaire de l'entité côté <code>1,N</code> comme <strong>clé étrangère (FK)</strong>.</p>
            <pre><code><span class="comment">-- MCD</span>
<span class="class-name">CATEGORIE</span> <span class="keyword">1,1</span> — <span class="function">CLASSE</span> — <span class="keyword">1,N</span> <span class="class-name">PRODUIT</span>

<span class="comment">-- MLD</span>
<span class="function">CATEGORIE</span> (<span class="keyword">idCategorie</span> PK, nom)
<span class="function">PRODUIT</span> (
  <span class="keyword">idProduit</span> PK,
  libelle,
  prix,
  <span class="variable">idCategorie</span> <span class="string">FK</span>
)</code></pre>
          </div>

          <div class="code-block">
            <h3 class="text-purple">Règle 3 — Relation N,N → Table intermédiaire</h3>
            <p>Une relation N,N génère une nouvelle table avec les clés primaires des deux entités comme <strong>clé primaire composée</strong>.</p>
            <pre><code><span class="comment">-- MCD</span>
<span class="class-name">COMMANDE</span> <span class="keyword">1,N</span> — <span class="function">CONTIENT</span> — <span class="keyword">1,N</span> <span class="class-name">PRODUIT</span>
                     quantite

<span class="comment">-- MLD</span>
<span class="function">CONTENIR</span> (
  <span class="keyword">idCommande</span> PK FK,
  <span class="keyword">idProduit</span>  PK FK,
  <span class="variable">quantite</span>,
  <span class="variable">prixUnitaire</span>
)</code></pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">MLD complet du système de commandes</h3>
          <pre><code><span class="comment">-- Toutes les tables issues du MCD</span>

<span class="function">CLIENT</span>    (<span class="keyword">idClient</span>, nom, prenom, email, telephone)

<span class="function">CATEGORIE</span> (<span class="keyword">idCategorie</span>, nomCategorie, description)

<span class="function">PRODUIT</span>   (<span class="keyword">idProduit</span>, libelle, prix, stock, <span class="variable">#idCategorie</span>)

<span class="function">COMMANDE</span>  (<span class="keyword">idCommande</span>, dateCommande, statut,
            adresseLivraison, <span class="variable">#idClient</span>)

<span class="function">CONTENIR</span>  (<span class="keyword">#idCommande</span>, <span class="keyword">#idProduit</span>, quantite, prixUnitaire)

<span class="comment">-- Légende :</span>
<span class="comment">--   souligné  → Clé primaire (PK)</span>
<span class="comment">--   #         → Clé étrangère (FK)</span></code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice pratique</h2>
        <div class="exercise">
          <h3 class="text-purple">Modéliser un système de bibliothèque</h3>
          <p>Concevez le MCD d'une bibliothèque avec les règles suivantes :</p>
          <ul>
            <li>Des <strong>adhérents</strong> peuvent emprunter des <strong>livres</strong></li>
            <li>Un livre est écrit par un ou plusieurs <strong>auteurs</strong></li>
            <li>Un livre appartient à une seule <strong>catégorie</strong></li>
            <li>Un emprunt a une <strong>date de début</strong> et une <strong>date de retour prévue</strong></li>
            <li>Un adhérent peut emprunter plusieurs livres, un livre peut être emprunté plusieurs fois (successivement)</li>
          </ul>

          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="comment">-- ═══════════════════════════════════════</span>
<span class="comment">--              ENTITÉS</span>
<span class="comment">-- ═══════════════════════════════════════</span>

<span class="class-name">ADHERENT</span>  (<span class="keyword">#idAdherent</span>, nom, prenom, email, dateInscription)
<span class="class-name">LIVRE</span>     (<span class="keyword">#idLivre</span>, titre, isbn, anneePublication, disponible)
<span class="class-name">AUTEUR</span>    (<span class="keyword">#idAuteur</span>, nom, prenom, nationalite)
<span class="class-name">CATEGORIE</span> (<span class="keyword">#idCategorie</span>, libelle)

<span class="comment">-- ═══════════════════════════════════════</span>
<span class="comment">--              ASSOCIATIONS</span>
<span class="comment">-- ═══════════════════════════════════════</span>

<span class="comment">-- Un adhérent emprunte un livre (N-N avec propriétés)</span>
<span class="class-name">ADHERENT</span> <span class="keyword">1,N</span> ——— <span class="function">EMPRUNTE</span> ——— <span class="keyword">0,N</span> <span class="class-name">LIVRE</span>
                       |
                       ├── <span class="variable">dateDebut</span>
                       └── <span class="variable">dateRetourPrevue</span>

<span class="comment">-- Un livre est écrit par des auteurs (N-N)</span>
<span class="class-name">LIVRE</span> <span class="keyword">1,N</span> ——— <span class="function">ECRIT_PAR</span> ——— <span class="keyword">1,N</span> <span class="class-name">AUTEUR</span>

<span class="comment">-- Un livre appartient à une catégorie (1-N)</span>
<span class="class-name">CATEGORIE</span> <span class="keyword">1,1</span> ——— <span class="function">CLASSE</span> ——— <span class="keyword">1,N</span> <span class="class-name">LIVRE</span>

<span class="comment">-- ═══════════════════════════════════════</span>
<span class="comment">--              MLD RÉSULTANT</span>
<span class="comment">-- ═══════════════════════════════════════</span>

<span class="function">ADHERENT</span>  (<span class="keyword">idAdherent</span>, nom, prenom, email, dateInscription)

<span class="function">CATEGORIE</span> (<span class="keyword">idCategorie</span>, libelle)

<span class="function">LIVRE</span>     (<span class="keyword">idLivre</span>, titre, isbn, anneePublication,
            disponible, <span class="variable">#idCategorie</span>)

<span class="function">AUTEUR</span>    (<span class="keyword">idAuteur</span>, nom, prenom, nationalite)

<span class="function">ECRIRE</span>    (<span class="keyword">#idLivre</span>, <span class="keyword">#idAuteur</span>)

<span class="function">EMPRUNTER</span> (<span class="keyword">#idAdherent</span>, <span class="keyword">#idLivre</span>, <span class="keyword">dateDebut</span>,
            dateRetourPrevue)
<span class="comment">-- Note: la PK est composée de idAdherent + idLivre + dateDebut</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-gradient-primary text-white">
        <h2>Conclusion</h2>
        <div class="textExemple">
          <p>Dans cette leçon, nous avons couvert les fondamentaux de la modélisation conceptuelle des données :</p>
          <ul>
            <li>Le <strong>MCD</strong> est une représentation abstraite et indépendante de toute technologie</li>
            <li>Les <strong>entités</strong> représentent les objets du monde réel à mémoriser</li>
            <li>Les <strong>associations</strong> expriment les liens sémantiques entre entités</li>
            <li>Les <strong>cardinalités</strong> (0,1 / 1,1 / 0,N / 1,N) précisent les multiplicités des relations</li>
            <li>Les règles de transformation permettent de passer du MCD au <strong>MLD</strong> puis au <strong>SQL</strong></li>
          </ul>
          <p>La maîtrise du MCD est essentielle avant toute création de base de données. Un modèle bien conçu en amont évite des erreurs coûteuses à corriger en production et garantit un schéma cohérent, évolutif et performant.</p>
          <p>Ces bases vous permettront d'aborder ensuite les formes normales (1NF, 2NF, 3NF), la normalisation et l'optimisation des schémas relationnels.</p>
        </div>
      </section>

    </div>
  </div>
</template>

<script setup>
// Aucune logique nécessaire pour cette leçon statique
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

/* Classes utilitaires */
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

/* Blocs de code */
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

/* Couleurs syntaxiques style VS Code */
.keyword    { color: #c586c0 !important; }
.variable   { color: #9cdcfe !important; }
.string     { color: #ce9178 !important; }
.comment    { color: #6a9955 !important; }
.function   { color: #dcdcaa !important; }
.operator   { color: #d4d4d4 !important; }
.constant   { color: #4fc1ff !important; }
.number     { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }

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

details summary {
    cursor: pointer;
    outline: none;
}

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* RESPONSIVE */
@media (max-width: 768px) {
    .lesson-container { padding: 1rem; }
    .lesson-header    { padding: 2rem 1rem; }
    .lesson-header h1 { font-size: 2rem; }
    .lesson-section   { padding: 1.5rem; }
    .code-comparison  { grid-template-columns: 1fr; gap: 1rem; }
    pre               { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre               { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section   { padding: 1rem; }
    .lesson-header    { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@media (min-width: 1400px) {
    .lesson-content { max-width: 1300px; }
}

/* Animations */
@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}

.lesson-section                  { animation: fadeInUp 0.6s ease forwards; }
.lesson-section:nth-child(1)     { animation-delay: 0.1s; }
.lesson-section:nth-child(2)     { animation-delay: 0.2s; }
.lesson-section:nth-child(3)     { animation-delay: 0.3s; }
.lesson-section:nth-child(4)     { animation-delay: 0.4s; }
.lesson-section:nth-child(5)     { animation-delay: 0.5s; }
.lesson-section:nth-child(6)     { animation-delay: 0.6s; }
.lesson-section:nth-child(7)     { animation-delay: 0.7s; }
</style>