<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les Variables en PHP</h1>
                <p class="lesson-meta text-white">Apprenez à déclarer, utiliser et manipuler les variables en PHP</p>
            </header>

            <!-- Section 1: Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'une variable ?</h2>
                <p class="textExemple">
                    Une variable en PHP est un conteneur qui permet de stocker des données temporairement en mémoire.
                    Elle fonctionne comme une boîte étiquetée où vous pouvez ranger des informations et les réutiliser
                    plus tard dans votre code.
                </p>
                <p class="textExemple">
                    Les variables sont essentielles pour créer des applications dynamiques et interactives.
                </p>
            </section>

            <!-- Section 2: Déclaration des variables -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Déclarer une variable</h2>
                <p class="textExemple">
                    En PHP, les variables commencent toujours par le signe dollar <strong>$</strong> suivi du nom de la
                    variable.
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Déclaration de variables</span>
<span class="variable">$nom</span> = <span class="string">"Jean"</span>;
<span class="variable">$age</span> = <span class="number">25</span>;
<span class="variable">$estEtudiant</span> = <span class="keyword">true</span>;
<span class="variable">$prix</span> = <span class="number">19.99</span>;

<span class="comment">// Affichage des variables</span>
<span class="function">echo</span> <span class="string">"Bonjour "</span> . <span class="variable">$nom</span> . <span class="string">", vous avez "</span> . <span class="variable">$age</span> . <span class="string">" ans."</span>;
<span class="keyword">?&gt;</span></code></pre>
                </div>
                <p class="textExemple">
                    <strong>Résultat :</strong> "Bonjour Jean, vous avez 25 ans."
                </p>
            </section>

            <!-- Section 3: Règles de nommage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Règles de nommage des variables</h2>
                <p class="textExemple">
                    Les noms de variables doivent respecter certaines règles :
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ Valides</h4>
                        <pre><code><span class="variable">$nom</span>
<span class="variable">$age_utilisateur</span>
<span class="variable">$prixTotal</span>
<span class="variable">$user123</span>
<span class="variable">$_variable</span></code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">❌ Non valides</h4>
                        <pre><code><span class="variable">$123user</span>      <span class="comment">// Ne peut pas commencer par un chiffre</span>
<span class="variable">$age-utilisateur</span> <span class="comment">// Tirets non autorisés</span>
<span class="variable">$prix total</span>    <span class="comment">// Espaces interdits</span>
<span class="variable">$nom@mail</span>      <span class="comment">// Caractères spéciaux interdits</span></code></pre>
                    </div>
                </div>
                <p class="textExemple">
                    <strong>Conseil :</strong> Utilisez des noms descriptifs en camelCase ou snake_case pour une
                    meilleure lisibilité.
                </p>
            </section>

            <!-- Section 4: Types de variables -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les types de données en PHP</h2>
                <p class="textExemple">
                    PHP supporte plusieurs types de données :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Chaîne de caractères (String)</span>
<span class="variable">$prenom</span> = <span class="string">"Marie"</span>;
<span class="variable">$message</span> = <span class="string">'Bonjour le monde'</span>;

<span class="comment">// Entier (Integer)</span>
<span class="variable">$age</span> = <span class="number">30</span>;
<span class="variable">$quantite</span> = <span class="number">-5</span>;

<span class="comment">// Nombre décimal (Float/Double)</span>
<span class="variable">$prix</span> = <span class="number">19.99</span>;
<span class="variable">$temperature</span> = <span class="number">-3.5</span>;

<span class="comment">// Booléen (Boolean)</span>
<span class="variable">$estActif</span> = <span class="keyword">true</span>;
<span class="variable">$estVide</span> = <span class="keyword">false</span>;

<span class="comment">// Tableau (Array)</span>
<span class="variable">$couleurs</span> = [<span class="string">"rouge"</span>, <span class="string">"vert"</span>, <span class="string">"bleu"</span>];
<span class="variable">$personne</span> = [
    <span class="string">"nom"</span> =&gt; <span class="string">"Dupont"</span>,
    <span class="string">"age"</span> =&gt; <span class="number">25</span>
];

<span class="comment">// Null</span>
<span class="variable">$variableVide</span> = <span class="keyword">null</span>;
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 5: Concaténation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concaténation de variables</h2>
                <p class="textExemple">
                    Pour combiner des variables avec du texte, utilisez l'opérateur de concaténation <strong>.</strong>
                    (point) :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="variable">$prenom</span> = <span class="string">"Alice"</span>;
<span class="variable">$metier</span> = <span class="string">"développeuse"</span>;
<span class="variable">$salaire</span> = <span class="number">35000</span>;

<span class="comment">// Concaténation avec l'opérateur .</span>
<span class="variable">$message</span> = <span class="variable">$prenom</span> . <span class="string">" est "</span> . <span class="variable">$metier</span> . <span class="string">" et gagne "</span> . <span class="variable">$salaire</span> . <span class="string">"€ par an."</span>;
<span class="function">echo</span> <span class="variable">$message</span>;

<span class="comment">// Alternative avec les guillemets doubles</span>
<span class="function">echo</span> <span class="string">"</span><span class="variable">$prenom</span><span class="string"> est </span><span class="variable">$metier</span><span class="string"> et gagne </span><span class="variable">$salaire</span><span class="string">€ par an."</span>;
<span class="keyword">?&gt;</span></code></pre>
                </div>
                <p class="textExemple">
                    <strong>Résultat :</strong> "Alice est développeuse et gagne 35000€ par an."
                </p>
            </section>

            <!-- Section 6: Opérations sur les variables -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Opérations mathématiques</h2>
                <p class="textExemple">
                    Vous pouvez effectuer des calculs avec des variables numériques :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="variable">$a</span> = <span class="number">10</span>;
<span class="variable">$b</span> = <span class="number">3</span>;

<span class="comment">// Opérations de base</span>
<span class="variable">$somme</span> = <span class="variable">$a</span> + <span class="variable">$b</span>;        <span class="comment">// 13</span>
<span class="variable">$difference</span> = <span class="variable">$a</span> - <span class="variable">$b</span>;   <span class="comment">// 7</span>
<span class="variable">$produit</span> = <span class="variable">$a</span> * <span class="variable">$b</span>;      <span class="comment">// 30</span>
<span class="variable">$quotient</span> = <span class="variable">$a</span> / <span class="variable">$b</span>;     <span class="comment">// 3.333...</span>
<span class="variable">$reste</span> = <span class="variable">$a</span> % <span class="variable">$b</span>;        <span class="comment">// 1</span>

<span class="comment">// Opérations combinées</span>
<span class="variable">$total</span> = <span class="number">100</span>;
<span class="variable">$tva</span> = <span class="number">0.2</span>; <span class="comment">// 20%</span>
<span class="variable">$prixTTC</span> = <span class="variable">$total</span> + (<span class="variable">$total</span> * <span class="variable">$tva</span>); <span class="comment">// 120</span>

<span class="function">echo</span> <span class="string">"Prix TTC: "</span> . <span class="variable">$prixTTC</span> . <span class="string">"€"</span>;
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 7: Modification de variables -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Modification et réassignation</h2>
                <p class="textExemple">
                    Vous pouvez modifier la valeur d'une variable à tout moment :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Déclaration initiale</span>
<span class="variable">$compteur</span> = <span class="number">0</span>;
<span class="function">echo</span> <span class="string">"Compteur: "</span> . <span class="variable">$compteur</span>; <span class="comment">// 0</span>

<span class="comment">// Incrémentation</span>
<span class="variable">$compteur</span> = <span class="variable">$compteur</span> + <span class="number">1</span>;
<span class="variable">$compteur</span> += <span class="number">1</span>; <span class="comment">// Méthode raccourcie</span>
<span class="variable">$compteur</span>++;    <span class="comment">// Incrémentation de 1</span>

<span class="function">echo</span> <span class="string">"Compteur: "</span> . <span class="variable">$compteur</span>; <span class="comment">// 3</span>

<span class="comment">// Changement de type</span>
<span class="variable">$variable</span> = <span class="string">"123"</span>;   <span class="comment">// Chaîne de caractères</span>
<span class="variable">$variable</span> = <span class="number">123</span>;     <span class="comment">// Devient un entier</span>
<span class="variable">$variable</span> = <span class="keyword">true</span>;   <span class="comment">// Devient un booléen</span>
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 8: Variables variables -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Variables variables</h2>
                <p class="textExemple">
                    PHP supporte les "variables variables" - une variable dont le nom est stocké dans une autre variable
                    :
                </p>
                <div class="code-example">
                    <pre><code><span class="keyword">&lt;?php</span>
<span class="variable">$nomVariable</span> = <span class="string">"age"</span>;
<span class="variable">$$nomVariable</span> = <span class="number">25</span>; <span class="comment">// Crée $age = 25</span>

<span class="function">echo</span> <span class="variable">$age</span>; <span class="comment">// Affiche 25</span>

<span class="comment">// Exemple pratique</span>
<span class="variable">$langue</span> = <span class="string">"fr"</span>;
<span class="variable">$message_fr</span> = <span class="string">"Bonjour"</span>;
<span class="variable">$message_en</span> = <span class="string">"Hello"</span>;

<span class="variable">$variableMessage</span> = <span class="string">"message_"</span> . <span class="variable">$langue</span>;
<span class="function">echo</span> <span class="variable">$$variableMessage</span>; <span class="comment">// Affiche "Bonjour"</span>
<span class="keyword">?&gt;</span></code></pre>
                </div>
            </section>

            <!-- Section 9: Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Créez un script PHP qui :
                    </p>
                    <ol class="textExemple">
                        <li>Déclare des variables pour un produit (nom, prix, quantité en stock)</li>
                        <li>Calcule le prix total du stock (prix × quantité)</li>
                        <li>Affiche un message formaté avec toutes les informations</li>
                    </ol>
                    <details>
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution :</h4>
                            <pre><code><span class="keyword">&lt;?php</span>
<span class="comment">// Déclaration des variables</span>
<span class="variable">$nomProduit</span> = <span class="string">"Ordinateur portable"</span>;
<span class="variable">$prixUnitaire</span> = <span class="number">899.99</span>;
<span class="variable">$quantiteStock</span> = <span class="number">15</span>;

<span class="comment">// Calcul du prix total</span>
<span class="variable">$valeurStock</span> = <span class="variable">$prixUnitaire</span> * <span class="variable">$quantiteStock</span>;

<span class="comment">// Affichage des informations</span>
<span class="function">echo</span> <span class="string">"Produit: "</span> . <span class="variable">$nomProduit</span> . <span class="string">"&lt;br&gt;"</span>;
<span class="function">echo</span> <span class="string">"Prix unitaire: "</span> . <span class="variable">$prixUnitaire</span> . <span class="string">"€&lt;br&gt;"</span>;
<span class="function">echo</span> <span class="string">"Quantité en stock: "</span> . <span class="variable">$quantiteStock</span> . <span class="string">"&lt;br&gt;"</span>;
<span class="function">echo</span> <span class="string">"Valeur totale du stock: "</span> . <span class="variable">$valeurStock</span> . <span class="string">"€&lt;br&gt;"</span>;

<span class="comment">// Alternative avec une seule chaîne</span>
<span class="variable">$message</span> = <span class="string">"Le produit '</span><span class="variable">$nomProduit</span><span class="string">' coûte </span><span class="variable">$prixUnitaire</span><span class="string">€. "</span> .
            <span class="string">"Avec </span><span class="variable">$quantiteStock</span><span class="string"> unités en stock, la valeur totale est de </span><span class="variable">$valeurStock</span><span class="string">€."</span>;
<span class="function">echo</span> <span class="variable">$message</span>;
<span class="keyword">?&gt;</span></code></pre>

                            <h4 class="text-purple">Résultat attendu :</h4>
                            <pre><code>Produit: Ordinateur portable
Prix unitaire: 899.99€
Quantité en stock: 15
Valeur totale du stock: 13499.85€

Le produit 'Ordinateur portable' coûte 899.99€. Avec 15 unités en stock, la valeur totale est de 13499.85€.</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Section 10: Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ À faire</h4>
                        <pre><code><span class="comment">// Noms descriptifs</span>
<span class="variable">$nombreArticles</span> = <span class="number">5</span>;
<span class="variable">$adresseEmail</span> = <span class="string">"test@email.com"</span>;

<span class="comment">// Initialisation</span>
<span class="variable">$total</span> = <span class="number">0</span>;
<span class="variable">$listeUtilisateurs</span> = [];

<span class="comment">// Style cohérent</span>
<span class="variable">$prix_ht</span> = <span class="number">100</span>;
<span class="variable">$prix_ttc</span> = <span class="number">120</span>;</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">❌ À éviter</h4>
                        <pre><code><span class="comment">// Noms vagues</span>
<span class="variable">$a</span> = <span class="number">5</span>;
<span class="variable">$x</span> = <span class="string">"test@email.com"</span>;

<span class="comment">// Variables non initialisées</span>
<span class="variable">$total</span> = <span class="variable">$total</span> + <span class="variable">$prix</span>; <span class="comment">// Erreur si $prix n'existe pas</span>

<span class="comment">// Mélange de styles</span>
<span class="variable">$prix_ht</span> = <span class="number">100</span>;
<span class="variable">$prixTTC</span> = <span class="number">120</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Section 11: Conclusion -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Récapitulatif</h2>
                <p class="text-white">
                    Les variables sont les éléments de base de tout programme PHP. Vous savez maintenant comment :
                </p>
                <ul class="text-white">
                    <li>Déclarer et nommer correctement des variables</li>
                    <li>Utiliser les différents types de données</li>
                    <li>Effectuer des opérations et des concaténations</li>
                    <li>Modifier et réassigner des valeurs</li>
                    <li>Appliquer les bonnes pratiques de codage</li>
                </ul>
            </section>
        </div>
    </div>
</template>

<script>

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

/* Couleurs VS Code pour la syntaxe PHP */
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

.text-center {
    text-align: center;
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