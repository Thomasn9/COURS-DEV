<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">La superglobale $_GET en PHP</h1>
        <p class="lesson-meta text-white">Récupérer et traiter les données des URLs</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p class="textExemple">
          La superglobale <code>$_GET</code> est l'une des variables les plus importantes en PHP pour la communication entre les pages web. Elle permet de récupérer les données envoyées via l'URL, ce qui est essentiel pour créer des applications web dynamiques et interactives.
        </p>
      </section>

      <!-- Qu'est-ce que $_GET -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que la superglobale $_GET ?</h2>
        <p class="textExemple">
          <code>$_GET</code> est un tableau associatif prédéfini en PHP qui contient toutes les variables passées dans l'URL via la méthode GET. C'est une "superglobale", ce qui signifie qu'elle est accessible partout dans le script sans avoir besoin d'utiliser <code>global</code>.
        </p>
        
        <div class="code-example">
          <pre><code><span class="token comment">// Exemple d'URL avec paramètres GET</span>
<span class="token constant">http</span><span class="token punctuation">:</span><span class="token comment">//monsite.com/page.php?nom=Alice&amp;age=25&amp;ville=Paris</span>

<span class="token comment">// Dans page.php, $_GET contiendra :</span>
<span class="token variable">$_GET</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
    <span class="token string">'nom'</span>   <span class="token operator">=></span> <span class="token string">'Alice'</span><span class="token punctuation">,</span>
    <span class="token string">'age'</span>   <span class="token operator">=></span> <span class="token string">'25'</span><span class="token punctuation">,</span>
    <span class="token string">'ville'</span> <span class="token operator">=></span> <span class="token string">'Paris'</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span></code></pre>
        </div>
      </section>

      <!-- Syntaxe de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de base</h2>
        <p class="textExemple">
          Pour accéder aux valeurs de <code>$_GET</code>, on utilise la syntaxe des tableaux associatifs :
        </p>
        
        <div class="code-example">
          <pre><code><span class="token comment">// Récupérer une valeur simple</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token comment">// Récupérer avec une valeur par défaut</span>
<span class="token variable">$age</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'age'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'age'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>

<span class="token comment">// Vérifier si un paramètre existe</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'ville'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$ville</span> <span class="token operator">=</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'ville'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Exemples pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples pratiques</h2>
        
        <h3 class="text-purple">Exemple 1 : Page de profil utilisateur</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// URL : profile.php?id=123&amp;nom=Alice</span>

<span class="token variable">$id</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">intval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">htmlspecialchars</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token string">'Invité'</span><span class="token punctuation">;</span>

<span class="token keyword">echo</span> <span class="token string">"&lt;h1>Profil de </span><span class="token variable">$nom</span><span class="token string">&lt;/h1>"</span><span class="token punctuation">;</span>
<span class="token keyword">echo</span> <span class="token string">"&lt;p>ID : </span><span class="token variable">$id</span><span class="token string">&lt;/p>"</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">Exemple 2 : Système de recherche</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// URL : search.php?q=php+tutorial&amp;category=web&amp;page=2</span>

<span class="token variable">$recherche</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'q'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'q'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token string">''</span><span class="token punctuation">;</span>
<span class="token variable">$categorie</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'category'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'category'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'all'</span><span class="token punctuation">;</span>
<span class="token variable">$page</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'page'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token function">intval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'page'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">;</span>

<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$recherche</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">"&lt;h2>Résultats pour : "</span> <span class="token operator">.</span> <span class="token function">htmlspecialchars</span><span class="token punctuation">(</span><span class="token variable">$recherche</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">"&lt;/h2>"</span><span class="token punctuation">;</span>
    <span class="token keyword">echo</span> <span class="token string">"&lt;p>Catégorie : </span><span class="token variable">$categorie</span><span class="token string"> - Page : </span><span class="token variable">$page</span><span class="token string">&lt;/p>"</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">"&lt;p>Veuillez entrer un terme de recherche&lt;/p>"</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
        </div>
        
        <h3 class="text-purple">Exemple 3 : Filtrage de produits</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// URL : products.php?category=electronics&amp;min_price=100&amp;max_price=500&amp;sort=price</span>

<span class="token variable">$categorie</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'category'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'category'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'all'</span><span class="token punctuation">;</span>
<span class="token variable">$prixMin</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'min_price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">floatval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'min_price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token variable">$prixMax</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'max_price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">floatval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'max_price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">1000</span><span class="token punctuation">;</span>
<span class="token variable">$tri</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'sort'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'sort'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'name'</span><span class="token punctuation">;</span>

<span class="token comment">// Construction de la requête SQL (exemple simplifié)</span>
<span class="token variable">$where</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$categorie</span> <span class="token operator">!==</span> <span class="token string">'all'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$where</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"category = '"</span> <span class="token operator">.</span> <span class="token function">mysqli_real_escape_string</span><span class="token punctuation">(</span><span class="token variable">$conn</span><span class="token punctuation">,</span> <span class="token variable">$categorie</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">"'"</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token variable">$where</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"price BETWEEN </span><span class="token variable">$prixMin</span><span class="token string"> AND </span><span class="token variable">$prixMax</span><span class="token string">"</span><span class="token punctuation">;</span>

<span class="token variable">$requete</span> <span class="token operator">=</span> <span class="token string">"SELECT * FROM products WHERE "</span> <span class="token operator">.</span> <span class="token function">implode</span><span class="token punctuation">(</span><span class="token string">' AND '</span><span class="token punctuation">,</span> <span class="token variable">$where</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">" ORDER BY </span><span class="token variable">$tri</span><span class="token string">"</span><span class="token punctuation">;</span></code></pre>
        </div>
      </section>

      <!-- Sécurité avec $_GET -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Sécurité avec $_GET</h2>
        <p class="textExemple">
          Les données de <code>$_GET</code> proviennent directement des utilisateurs et doivent donc être traitées avec prudence pour éviter les vulnérabilités de sécurité.
        </p>
        
        <h3 class="text-purple">Bonnes pratiques de sécurité</h3>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">❌ Dangereux</h4>
            <pre><code><span class="token comment">// Injection SQL possible</span>
<span class="token variable">$id</span> <span class="token operator">=</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token variable">$requete</span> <span class="token operator">=</span> <span class="token string">"SELECT * FROM users WHERE id = </span><span class="token variable">$id</span><span class="token string">"</span><span class="token punctuation">;</span>

<span class="token comment">// XSS possible</span>
<span class="token keyword">echo</span> <span class="token string">"&lt;h1>Bonjour "</span> <span class="token operator">.</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">.</span> <span class="token string">"&lt;/h1>"</span><span class="token punctuation">;</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">✅ Sécurisé</h4>
            <pre><code><span class="token comment">// Protection contre l'injection SQL</span>
<span class="token variable">$id</span> <span class="token operator">=</span> <span class="token function">intval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$requete</span> <span class="token operator">=</span> <span class="token string">"SELECT * FROM users WHERE id = "</span> <span class="token operator">.</span> <span class="token function">mysqli_real_escape_string</span><span class="token punctuation">(</span><span class="token variable">$conn</span><span class="token punctuation">,</span> <span class="token variable">$id</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Protection contre XSS</span>
<span class="token keyword">echo</span> <span class="token string">"&lt;h1>Bonjour "</span> <span class="token operator">.</span> <span class="token function">htmlspecialchars</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">"&lt;/h1>"</span><span class="token punctuation">;</span></code></pre>
          </div>
        </div>
        
        <h3 class="text-purple">Fonctions de sécurisation importantes</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// Pour les nombres</span>
<span class="token variable">$id</span> <span class="token operator">=</span> <span class="token function">intval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$prix</span> <span class="token operator">=</span> <span class="token function">floatval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Pour le texte (affichage HTML)</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token function">htmlspecialchars</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'name'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Pour les URLs</span>
<span class="token variable">$url</span> <span class="token operator">=</span> <span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'url'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_URL</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Pour les emails</span>
<span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
        </div>
      </section>

      <!-- Différences avec $_POST -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Différences entre $_GET et $_POST</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">$_GET</h4>
            <ul class="textExemple">
              <li>✅ Données visibles dans l'URL</li>
              <li>✅ Limitée en taille (~2048 caractères)</li>
              <li>✅ Peut être mise en cache</li>
              <li>✅ Peut être bookmarkée</li>
              <li>✅ Idéal pour la recherche, filtres</li>
              <li>❌ Moins sécurisé</li>
            </ul>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">$_POST</h4>
            <ul class="textExemple">
              <li>✅ Données invisibles dans l'URL</li>
              <li>✅ Pas de limite de taille pratique</li>
              <li>✅ Non mis en cache par défaut</li>
              <li>✅ Ne peut pas être bookmarkée</li>
              <li>✅ Idéal pour les formulaires sensibles</li>
              <li>✅ Plus sécurisé</li>
            </ul>
          </div>
        </div>
        
        <h3 class="text-purple">Quand utiliser $_GET ?</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// ✅ Bon usage de GET</span>
<span class="token constant">http</span><span class="token punctuation">:</span><span class="token comment">//site.com/search?q=php</span>
<span class="token constant">http</span><span class="token punctuation">:</span><span class="token comment">//site.com/products?category=books</span>
<span class="token constant">http</span><span class="token punctuation">:</span><span class="token comment">//site.com/article?id=123</span>

<span class="token comment">// ❌ Mauvais usage de GET</span>
<span class="token constant">http</span><span class="token punctuation">:</span><span class="token comment">//site.com/login?username=admin&amp;password=1234</span>
<span class="token constant">http</span><span class="token punctuation">:</span><span class="token comment">//site.com/register?email=test@test.com</span></code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques avec $_GET</h2>
        
        <h3 class="text-purple">1. Toujours valider les données</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// ❌ Mauvaise pratique</span>
<span class="token variable">$page</span> <span class="token operator">=</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'page'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token comment">// ✅ Bonne pratique</span>
<span class="token variable">$page</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'page'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token function">intval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'page'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">2. Utiliser des valeurs par défaut</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// Valeurs par défaut pour éviter les erreurs</span>
<span class="token variable">$tri</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'sort'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'sort'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'date'</span><span class="token punctuation">;</span>
<span class="token variable">$ordre</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'order'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'order'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'desc'</span><span class="token punctuation">;</span>
<span class="token variable">$limite</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'limit'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">min</span><span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">,</span> <span class="token function">intval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'limit'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">10</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">3. Fonction utilitaire pour $_GET</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">get</span><span class="token punctuation">(</span><span class="token variable">$key</span><span class="token punctuation">,</span> <span class="token variable">$default</span> <span class="token operator">=</span> <span class="token constant">null</span><span class="token punctuation">,</span> <span class="token variable">$filter</span> <span class="token operator">=</span> <span class="token constant">FILTER_DEFAULT</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$value</span> <span class="token operator">=</span> <span class="token function">filter_input</span><span class="token punctuation">(</span><span class="token constant">INPUT_GET</span><span class="token punctuation">,</span> <span class="token variable">$key</span><span class="token punctuation">,</span> <span class="token variable">$filter</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token variable">$value</span> <span class="token operator">!==</span> <span class="token constant">null</span> <span class="token operator">?</span> <span class="token variable">$value</span> <span class="token punctuation">:</span> <span class="token variable">$default</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token variable">$id</span> <span class="token operator">=</span> <span class="token function">get</span><span class="token punctuation">(</span><span class="token string">'id'</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_INT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token function">get</span><span class="token punctuation">(</span><span class="token string">'nom'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_SANITIZE_STRING</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">get</span><span class="token punctuation">(</span><span class="token string">'email'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Calculateur simple</h3>
          <p class="textExemple">
            Créez une page qui accepte deux nombres et une opération via <code>$_GET</code> et affiche le résultat. L'URL devrait ressembler à : <code>calculateur.php?a=5&amp;b=3&amp;operation=add</code>
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="token variable">$a</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'a'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">floatval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'a'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token variable">$b</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'b'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token function">floatval</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'b'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token variable">$operation</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'operation'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'operation'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'add'</span><span class="token punctuation">;</span>

<span class="token variable">$resultat</span> <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token keyword">switch</span> <span class="token punctuation">(</span><span class="token variable">$operation</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">case</span> <span class="token string">'add'</span><span class="token punctuation">:</span>
        <span class="token variable">$resultat</span> <span class="token operator">=</span> <span class="token variable">$a</span> <span class="token operator">+</span> <span class="token variable">$b</span><span class="token punctuation">;</span>
        <span class="token keyword">break</span><span class="token punctuation">;</span>
    <span class="token keyword">case</span> <span class="token string">'subtract'</span><span class="token punctuation">:</span>
        <span class="token variable">$resultat</span> <span class="token operator">=</span> <span class="token variable">$a</span> <span class="token operator">-</span> <span class="token variable">$b</span><span class="token punctuation">;</span>
        <span class="token keyword">break</span><span class="token punctuation">;</span>
    <span class="token keyword">case</span> <span class="token string">'multiply'</span><span class="token punctuation">:</span>
        <span class="token variable">$resultat</span> <span class="token operator">=</span> <span class="token variable">$a</span> <span class="token operator">*</span> <span class="token variable">$b</span><span class="token punctuation">;</span>
        <span class="token keyword">break</span><span class="token punctuation">;</span>
    <span class="token keyword">case</span> <span class="token string">'divide'</span><span class="token punctuation">:</span>
        <span class="token variable">$resultat</span> <span class="token operator">=</span> <span class="token variable">$b</span> <span class="token operator">!=</span> <span class="token number">0</span> <span class="token operator">?</span> <span class="token variable">$a</span> <span class="token operator">/</span> <span class="token variable">$b</span> <span class="token punctuation">:</span> <span class="token string">'Erreur: division par zéro'</span><span class="token punctuation">;</span>
        <span class="token keyword">break</span><span class="token punctuation">;</span>
    <span class="token keyword">default</span><span class="token punctuation">:</span>
        <span class="token variable">$resultat</span> <span class="token operator">=</span> <span class="token string">'Opération non supportée'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">echo</span> <span class="token string">"&lt;h2>Résultat : </span><span class="token variable">$resultat</span><span class="token string">&lt;/h2>"</span><span class="token punctuation">;</span></code></pre>
            </div>
          </details>
        </div>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Gallery avec filtres</h3>
          <p class="textExemple">
            Créez une galerie d'images qui peut être filtrée par catégorie et triée par date ou popularité. Utilisez <code>$_GET</code> pour gérer les filtres.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="token variable">$categories</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'nature'</span><span class="token punctuation">,</span> <span class="token string">'portrait'</span><span class="token punctuation">,</span> <span class="token string">'urban'</span><span class="token punctuation">,</span> <span class="token string">'animal'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token variable">$categorie</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'category'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'category'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'all'</span><span class="token punctuation">;</span>
<span class="token variable">$tri</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'sort'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_GET</span><span class="token punctuation">[</span><span class="token string">'sort'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">'date'</span><span class="token punctuation">;</span>

<span class="token comment">// Validation des entrées</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$categorie</span> <span class="token operator">!==</span> <span class="token string">'all'</span> <span class="token operator">&amp;&amp;</span> <span class="token operator">!</span><span class="token function">in_array</span><span class="token punctuation">(</span><span class="token variable">$categorie</span><span class="token punctuation">,</span> <span class="token variable">$categories</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$categorie</span> <span class="token operator">=</span> <span class="token string">'all'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token variable">$ordreTri</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'date'</span><span class="token punctuation">,</span> <span class="token string">'popularity'</span><span class="token punctuation">,</span> <span class="token string">'name'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">in_array</span><span class="token punctuation">(</span><span class="token variable">$tri</span><span class="token punctuation">,</span> <span class="token variable">$ordreTri</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$tri</span> <span class="token operator">=</span> <span class="token string">'date'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Affichage des filtres</span>
<span class="token keyword">echo</span> <span class="token string">'&lt;div class="filters">'</span><span class="token punctuation">;</span>
<span class="token keyword">echo</span> <span class="token string">'&lt;a href="?category=all&amp;sort=</span><span class="token variable">$tri</span><span class="token string">" class="</span> <span class="token operator">.</span> <span class="token punctuation">(</span><span class="token variable">$categorie</span> <span class="token operator">===</span> <span class="token string">'all'</span> <span class="token operator">?</span> <span class="token string">'active'</span> <span class="token punctuation">:</span> <span class="token string">''</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">'">Tous&lt;/a>'</span><span class="token punctuation">;</span>
<span class="token keyword">foreach</span> <span class="token punctuation">(</span><span class="token variable">$categories</span> <span class="token keyword">as</span> <span class="token variable">$cat</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">'&lt;a href="?category='</span> <span class="token operator">.</span> <span class="token variable">$cat</span> <span class="token operator">.</span> <span class="token string">'&amp;sort=</span><span class="token variable">$tri</span><span class="token string">" class="</span> <span class="token operator">.</span> <span class="token punctuation">(</span><span class="token variable">$categorie</span> <span class="token operator">===</span> <span class="token variable">$cat</span> <span class="token operator">?</span> <span class="token string">'active'</span> <span class="token punctuation">:</span> <span class="token string">''</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">'">'</span> <span class="token operator">.</span> <span class="token function">ucfirst</span><span class="token punctuation">(</span><span class="token variable">$cat</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">'&lt;/a>'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token keyword">echo</span> <span class="token string">'&lt;/div>'</span><span class="token punctuation">;</span>

<span class="token comment">// Ici, vous récupéreriez les images de la base de données</span>
<span class="token comment">// en fonction des filtres $categorie et $tri</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          La superglobale <code>$_GET</code> est un outil fondamental en PHP pour créer des applications web interactives et dynamiques. Elle permet une communication simple entre les pages via l'URL.
        </p>
        <p class="textExemple">
          Points clés à retenir :
        </p>
        <ul class="textExemple">
          <li><code>$_GET</code> récupère les données passées dans l'URL</li>
          <li>Toujours valider et sécuriser les données de <code>$_GET</code></li>
          <li>Utiliser <code>$_GET</code> pour les données non sensibles et bookmarkables</li>
          <li>Préférer <code>$_POST</code> pour les données sensibles et les formulaires</li>
          <li>Les URLs avec paramètres GET doivent rester lisibles et compréhensibles</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonGetSuperglobal',
}
</script>

<style scoped>
/* Les styles sont identiques à votre leçon précédente */
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

.btn-hover {
    position: relative;
    overflow: hidden;
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

/* Couleurs VS Code pour la syntaxe PHP */
.token.keyword { color: #c586c0 !important; }
.token.variable { color: #9cdcfe !important; }
.token.string { color: #ce9178 !important; }
.token.comment { color: #6a9955 !important; }
.token.function { color: #dcdcaa !important; }
.token.operator { color: #d4d4d4 !important; }
.token.constant { color: #4fc1ff !important; }
.token.number { color: #b5cea8 !important; }
.token.punctuation { color: #d4d4d4 !important; }

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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>