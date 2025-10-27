<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">La fonction json_encode() en PHP</h1>
        <p class="lesson-meta text-white">Manipulation et conversion de données en JSON</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p class="textExemple">
          La fonction <code>json_encode()</code> est l'une des fonctions les plus utiles en PHP pour la manipulation de données. 
          Elle permet de convertir une variable PHP en une chaîne de caractères au format JSON (JavaScript Object Notation). 
          Cette fonction est essentielle pour l'échange de données entre un serveur PHP et des applications clientes (JavaScript, applications mobiles, etc.).
        </p>
      </section>

      <!-- Syntaxe de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de base</h2>
        <p class="textExemple">
          La syntaxe de la fonction <code>json_encode()</code> est simple :
        </p>
        <div class="code-example">
          <pre><code><span class="function">json_encode</span>(<span class="variable">$value</span>[, <span class="variable">$options</span> = <span class="number">0</span>[, <span class="variable">$depth</span> = <span class="number">512</span>]]) : <span class="keyword">string</span>|<span class="keyword">false</span></code></pre>
        </div>
        <p class="textExemple">
          <strong>Paramètres :</strong>
        </p>
        <ul class="textExemple">
          <li><code><span class="variable">$value</span></code> : La valeur à encoder (tableau, objet, chaîne, etc.)</li>
          <li><code><span class="variable">$options</span></code> : Options de codage (optionnel)</li>
          <li><code><span class="variable">$depth</span></code> : Profondeur maximale d'encodage (optionnel)</li>
        </ul>
        <p class="textExemple">
          <strong>Valeur de retour :</strong> Une chaîne JSON encodée ou <code><span class="keyword">false</span></code> en cas d'échec.
        </p>
      </section>

      <!-- Exemples d'utilisation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples d'utilisation</h2>
        
        <h3 class="text-purple">1. Encoder un tableau associatif</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="variable">$data</span> = [
    <span class="string">"nom"</span> => <span class="string">"Dupont"</span>,
    <span class="string">"prenom"</span> => <span class="string">"Jean"</span>,
    <span class="string">"age"</span> => <span class="number">30</span>,
    <span class="string">"ville"</span> => <span class="string">"Paris"</span>
];

<span class="variable">$json</span> = <span class="function">json_encode</span>(<span class="variable">$data</span>);
<span class="function">echo</span> <span class="variable">$json</span>;</code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Résultat JSON</h4>
            <pre><code>{
    <span class="string">"nom"</span>: <span class="string">"Dupont"</span>,
    <span class="string">"prenom"</span>: <span class="string">"Jean"</span>,
    <span class="string">"age"</span>: <span class="number">30</span>,
    <span class="string">"ville"</span>: <span class="string">"Paris"</span>
}</code></pre>
          </div>
        </div>

        <h3 class="text-purple">2. Encoder un tableau indexé</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="variable">$fruits</span> = [<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>];
<span class="variable">$json</span> = <span class="function">json_encode</span>(<span class="variable">$fruits</span>);
<span class="function">echo</span> <span class="variable">$json</span>;</code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Résultat JSON</h4>
            <pre><code>[<span class="string">"pomme"</span>, <span class="string">"banane"</span>, <span class="string">"orange"</span>]</code></pre>
          </div>
        </div>

        <h3 class="text-purple">3. Encoder un objet</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="keyword">class</span> <span class="class-name">Utilisateur</span> {
    <span class="keyword">public</span> <span class="variable">$nom</span> = <span class="string">"Martin"</span>;
    <span class="keyword">public</span> <span class="variable">$age</span> = <span class="number">25</span>;
    <span class="keyword">private</span> <span class="variable">$email</span> = <span class="string">"martin@example.com"</span>;
}

<span class="variable">$user</span> = <span class="keyword">new</span> <span class="class-name">Utilisateur</span>();
<span class="variable">$json</span> = <span class="function">json_encode</span>(<span class="variable">$user</span>);
<span class="function">echo</span> <span class="variable">$json</span>;</code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Résultat JSON</h4>
            <pre><code>{
    <span class="string">"nom"</span>: <span class="string">"Martin"</span>,
    <span class="string">"age"</span>: <span class="number">25</span>
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Options d'encodage -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Options d'encodage</h2>
        <p class="textExemple">
          Le deuxième paramètre de <code>json_encode()</code> permet de spécifier des options pour personnaliser l'encodage.
          Voici les principales options :
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">JSON_PRETTY_PRINT</h3>
          <p class="textExemple">Formate le JSON avec une indentation pour une meilleure lisibilité :</p>
          <pre><code><span class="variable">$data</span> = [<span class="string">"a"</span> => <span class="number">1</span>, <span class="string">"b"</span> => <span class="number">2</span>, <span class="string">"c"</span> => <span class="number">3</span>];
<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$data</span>, <span class="constant">JSON_PRETTY_PRINT</span>);</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">JSON_UNESCAPED_UNICODE</h3>
          <p class="textExemple">Encode les caractères Unicode sans les échapper :</p>
          <pre><code><span class="variable">$data</span> = [<span class="string">"message"</span> => <span class="string">"Bonjour à tous!"</span>];
<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$data</span>, <span class="constant">JSON_UNESCAPED_UNICODE</span>);</code></pre>
        </div>

        <div class="code-example">
          <h3 class="text-purple">JSON_NUMERIC_CHECK</h3>
          <p class="textExemple">Convertit les chaînes numériques en nombres :</p>
          <pre><code><span class="variable">$data</span> = [<span class="string">"age"</span> => <span class="string">"30"</span>, <span class="string">"score"</span> => <span class="string">"95.5"</span>];
<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$data</span>, <span class="constant">JSON_NUMERIC_CHECK</span>);</code></pre>
        </div>

        <p class="textExemple">
          <strong>Note :</strong> Vous pouvez combiner plusieurs options avec l'opérateur | (OR bit à bit) :
        </p>
        <pre><code><span class="function">json_encode</span>(<span class="variable">$data</span>, <span class="constant">JSON_PRETTY_PRINT</span> | <span class="constant">JSON_UNESCAPED_UNICODE</span>);</code></pre>
      </section>

      <!-- Gestion des erreurs -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Gestion des erreurs</h2>
        <p class="textExemple">
          Il est important de vérifier si l'encodage a réussi, car <code>json_encode()</code> peut retourner <code><span class="keyword">false</span></code> en cas d'échec.
        </p>
        <div class="code-example">
          <pre><code><span class="variable">$data</span> = [<span class="string">"nom"</span> => <span class="string">"Dupont"</span>, <span class="string">"age"</span> => <span class="number">30</span>];

<span class="variable">$json</span> = <span class="function">json_encode</span>(<span class="variable">$data</span>);

<span class="keyword">if</span> (<span class="variable">$json</span> === <span class="keyword">false</span>) {
    <span class="comment">// Gérer l'erreur</span>
    <span class="function">echo</span> <span class="string">"Erreur d'encodage JSON: "</span> . <span class="function">json_last_error_msg</span>();
} <span class="keyword">else</span> {
    <span class="function">echo</span> <span class="variable">$json</span>;
}</code></pre>
        </div>
        <p class="textExemple">
          La fonction <code>json_last_error_msg()</code> retourne un message décrivant la dernière erreur survenue.
        </p>
      </section>

      <!-- Cas d'utilisation courants -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Cas d'utilisation courants</h2>
        
        <h3 class="text-purple">1. API REST</h3>
        <p class="textExemple">
          <code>json_encode()</code> est essentiel pour créer des API REST qui renvoient des données au format JSON :
        </p>
        <div class="code-example">
          <pre><code><span class="comment">// Récupérer des données depuis la base de données</span>
<span class="variable">$users</span> = [
    [<span class="string">"id"</span> => <span class="number">1</span>, <span class="string">"nom"</span> => <span class="string">"Dupont"</span>, <span class="string">"email"</span> => <span class="string">"dupont@example.com"</span>],
    [<span class="string">"id"</span> => <span class="number">2</span>, <span class="string">"nom"</span> => <span class="string">"Martin"</span>, <span class="string">"email"</span> => <span class="string">"martin@example.com"</span>]
];

<span class="comment">// Définir l'en-tête HTTP</span>
<span class="function">header</span>(<span class="string">'Content-Type: application/json'</span>);

<span class="comment">// Renvoyer les données en JSON</span>
<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$users</span>, <span class="constant">JSON_PRETTY_PRINT</span>);</code></pre>
        </div>

        <h3 class="text-purple">2. Communication avec JavaScript (AJAX)</h3>
        <p class="textExemple">
          Pour envoyer des données structurées à JavaScript via AJAX :
        </p>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">Code PHP</h4>
            <pre><code><span class="variable">$response</span> = [
    <span class="string">"success"</span> => <span class="keyword">true</span>,
    <span class="string">"message"</span> => <span class="string">"Opération réussie"</span>,
    <span class="string">"data"</span> => <span class="variable">$users</span>
];

<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$response</span>);</code></pre>
          </div>
          <div class="code-example">
            <h4 class="text-purple">Code JavaScript</h4>
            <pre><code><span class="function">fetch</span>(<span class="string">'api.php'</span>)
    .<span class="function">then</span>(<span class="variable">response</span> => <span class="variable">response</span>.<span class="function">json</span>())
    .<span class="function">then</span>(<span class="variable">data</span> => {
        <span class="keyword">if</span> (<span class="variable">data</span>.<span class="variable">success</span>) {
            <span class="variable">console</span>.<span class="function">log</span>(<span class="variable">data</span>.<span class="variable">message</span>);
            <span class="comment">// Traiter data.data</span>
        }
    });</code></pre>
          </div>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Encodage simple</h3>
          <p class="textExemple">
            Créez un tableau associatif contenant les informations d'un produit (nom, prix, catégorie) et encodez-le en JSON.
          </p>
          <details>
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="variable">$produit</span> = [
    <span class="string">"nom"</span> => <span class="string">"Smartphone"</span>,
    <span class="string">"prix"</span> => <span class="number">599.99</span>,
    <span class="string">"categorie"</span> => <span class="string">"Électronique"</span>
];

<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$produit</span>, <span class="constant">JSON_PRETTY_PRINT</span>);</code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Encodage avec options</h3>
          <p class="textExemple">
            Encodez un tableau contenant des caractères spéciaux et des nombres sous forme de chaînes, en utilisant les options appropriées pour :
          </p>
          <ul class="textExemple">
            <li>Ne pas échapper les caractères Unicode</li>
            <li>Convertir les chaînes numériques en nombres</li>
            <li>Afficher le résultat de façon lisible</li>
          </ul>
          <details>
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="variable">$data</span> = [
    <span class="string">"message"</span> => <span class="string">"Café & croissant 🥐"</span>,
    <span class="string">"prix"</span> => <span class="string">"12.50"</span>,
    <span class="string">"quantite"</span> => <span class="string">"5"</span>
];

<span class="function">echo</span> <span class="function">json_encode</span>(<span class="variable">$data</span>, <span class="constant">JSON_UNESCAPED_UNICODE</span> | <span class="constant">JSON_NUMERIC_CHECK</span> | <span class="constant">JSON_PRETTY_PRINT</span>);</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <ul class="textExemple">
          <li><code>json_encode()</code> convertit les tableaux et objets PHP en chaîne JSON</li>
          <li>Toujours vérifier le retour de la fonction avec une condition</li>
          <li>Utilisez <code>JSON_PRETTY_PRINT</code> pour le débogage et le développement</li>
          <li>Pour les API, définissez l'en-tête <code>Content-Type: application/json</code></li>
          <li>Les propriétés privées et protégées des objets ne sont pas encodées</li>
          <li>Les ressources (comme les connexions de base de données) ne peuvent pas être encodées</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JsonEncodeLesson',
  head() {
    return {
      title: 'json_encode() en PHP - Cours de programmation',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez à utiliser la fonction json_encode() en PHP pour convertir des données en format JSON. Exemples pratiques et bonnes pratiques.'
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
    white-space: pre-wrap; /* Permet le retour à la ligne */
    word-wrap: break-word; /* Casse les mots longs */
    word-break: break-word; /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap; /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe PHP et JavaScript */
.keyword { color: #c586c0 !important; } /* Mots-clés (for, while, if, function, etc.) */
.variable { color: #9cdcfe !important; } /* Variables et noms de fonctions */
.string { color: #ce9178 !important; } /* Chaînes de caractères */
.comment { color: #6a9955 !important; } /* Commentaires */
.function { color: #dcdcaa !important; } /* Noms de fonctions */
.operator { color: #d4d4d4 !important; } /* Opérateurs (+, -, =, =>, etc.) */
.constant { color: #4fc1ff !important; } /* Constantes */
.number { color: #b5cea8 !important; } /* Nombres */
.class-name { color: #4ec9b0 !important; } /* Noms de classes */

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