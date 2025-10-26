<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">La fonction password_hash() en PHP</h1>
        <p class="lesson-meta text-white">Sécuriser les mots de passe de manière professionnelle</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p class="textExemple">
          La fonction <code>password_hash()</code> est l'une des fonctions les plus importantes en PHP pour la sécurité des applications web. Elle permet de hacher les mots de passe de manière sécurisée en utilisant des algorithmes robustes, rendant pratiquement impossible la récupération du mot de passe original.
        </p>
      </section>

      <!-- Pourquoi password_hash() -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi utiliser password_hash() ?</h2>
        <p class="textExemple">
          Avant <code>password_hash()</code>, les développeurs utilisaient des fonctions comme <code>md5()</code> ou <code>sha1()</code> pour hacher les mots de passe. Ces méthodes sont maintenant considérées comme obsolètes et dangereuses car vulnérables aux attaques par force brute.
        </p>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">❌ Anciennes méthodes dangereuses</h4>
            <pre><code><span class="token comment">// MD5 - Très vulnérable</span>
<span class="token variable">$password_hash</span> <span class="token operator">=</span> <span class="token function">md5</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// SHA1 - Également vulnérable</span>
<span class="token variable">$password_hash</span> <span class="token operator">=</span> <span class="token function">sha1</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Hash avec salt manuel - Complexe et risqué</span>
<span class="token variable">$salt</span> <span class="token operator">=</span> <span class="token string">'mon_salt_secret'</span><span class="token punctuation">;</span>
<span class="token variable">$password_hash</span> <span class="token operator">=</span> <span class="token function">md5</span><span class="token punctuation">(</span><span class="token variable">$password</span> <span class="token operator">.</span> <span class="token variable">$salt</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">✅ Nouvelle méthode sécurisée</h4>
            <pre><code><span class="token comment">// password_hash() - Sécurisé et simple</span>
<span class="token variable">$password_hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Le salt est généré automatiquement</span>
<span class="token comment">// L'algorithme est choisi automatiquement</span>
<span class="token comment">// Le coût est adapté au matériel actuel</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Syntaxe de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de base</h2>
        <p class="textExemple">
          La fonction <code>password_hash()</code> prend deux paramètres principaux et un paramètre optionnel :
        </p>
        
        <div class="code-example">
          <pre><code><span class="token keyword">string</span> <span class="token function">password_hash</span><span class="token punctuation">(</span>
    <span class="token keyword">string</span> <span class="token variable">$password</span><span class="token punctuation">,</span>
    <span class="token keyword">mixed</span> <span class="token variable">$algo</span><span class="token punctuation">,</span>
    <span class="token keyword">array</span> <span class="token variable">$options</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
<span class="token punctuation">)</span></code></pre>
        </div>
        
        <h3 class="text-purple">Paramètres</h3>
        <ul class="textExemple">
          <li><strong>$password</strong> : Le mot de passe en clair à hacher</li>
          <li><strong>$algo</strong> : L'algorithme de hachage à utiliser</li>
          <li><strong>$options</strong> : Tableau d'options (optionnel)</li>
        </ul>
        
        <h3 class="text-purple">Exemple simple</h3>
        <div class="code-example">
          <pre><code><span class="token variable">$password</span> <span class="token operator">=</span> <span class="token string">'mon_mot_de_passe_secret'</span><span class="token punctuation">;</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// $hash contiendra quelque chose comme :</span>
<span class="token comment">// '$2y$10$X5z8M9aBcDeFgHiJkLmNoOqRsTuVwXyZABCDEFGHIJKLMNOPQRSTUV'</span>

<span class="token function">var_dump</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">// string(60) "$2y$10$X5z8M9aBcDeFgHiJkLmNoOqRsTuVwXyZABCDEFGHIJKLMNOPQRSTUV"</span></code></pre>
        </div>
      </section>

      <!-- Algorithmes disponibles -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Algorithmes de hachage</h2>
        <p class="textExemple">
          PHP supporte plusieurs algorithmes pour le hachage de mots de passe. Il est recommandé d'utiliser <code>PASSWORD_DEFAULT</code> qui choisit automatiquement le meilleur algorithme disponible.
        </p>
        
        <div class="code-example">
          <pre><code><span class="token comment">// Algorithmes disponibles</span>
<span class="token constant">PASSWORD_DEFAULT</span>      <span class="token comment">// Utilise bcrypt (recommandé)</span>
<span class="token constant">PASSWORD_BCRYPT</span>       <span class="token comment">// Algorithme bcrypt</span>
<span class="token constant">PASSWORD_ARGON2I</span>      <span class="token comment">// Algorithme Argon2i (PHP 7.2+)</span>
<span class="token constant">PASSWORD_ARGON2ID</span>     <span class="token comment">// Algorithme Argon2id (PHP 7.3+)</span>

<span class="token comment">// Exemples d'utilisation</span>
<span class="token variable">$hash1</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$hash2</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_BCRYPT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$hash3</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_ARGON2I</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">Comparaison des algorithmes</h3>
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">PASSWORD_BCRYPT</h4>
            <ul class="textExemple">
              <li>✅ Algorithmes éprouvé et sécurisé</li>
              <li>✅ Supporté depuis PHP 5.5</li>
              <li>✅ Résistant aux attaques GPU</li>
              <li>✅ Limite à 72 caractères</li>
              <li>✅ Coût configurable</li>
            </ul>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">PASSWORD_ARGON2</h4>
            <ul class="textExemple">
              <li>✅ Gagnant du Password Hashing Competition</li>
              <li>✅ Plus résistant aux attaques hardware</li>
              <li>✅ Pas de limite de longueur</li>
              <li>❌ Nécessite PHP 7.2+</li>
              <li>✅ Plus de paramètres de configuration</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Options de configuration -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Options de configuration</h2>
        <p class="textExemple">
          Vous pouvez personnaliser le hachage en utilisant le troisième paramètre options. Les options les plus importantes sont le <strong>coût</strong> (cost) pour bcrypt et la <strong>mémoire</strong>, le <strong>temps</strong>, et les <strong>threads</strong> pour Argon2.
        </p>
        
        <h3 class="text-purple">Options pour BCRYPT</h3>
        <div class="code-example">
          <pre><code><span class="token variable">$options</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
    <span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token number">12</span><span class="token punctuation">,</span>  <span class="token comment">// Coût entre 4 et 31 (défaut: 10)</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_BCRYPT</span><span class="token punctuation">,</span> <span class="token variable">$options</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Le coût détermine le nombre d'itérations</span>
<span class="token comment">// Coût 10 = 2^10 = 1024 itérations</span>
<span class="token comment">// Coût 12 = 2^12 = 4096 itérations</span></code></pre>
        </div>
        
        <h3 class="text-purple">Options pour ARGON2</h3>
        <div class="code-example">
          <pre><code><span class="token variable">$options</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
    <span class="token string">'memory_cost'</span> <span class="token operator">=></span> <span class="token number">2048</span><span class="token punctuation">,</span>   <span class="token comment">// Mémoire en KiB (défaut: 65536)</span>
    <span class="token string">'time_cost'</span>   <span class="token operator">=></span> <span class="token number">4</span><span class="token punctuation">,</span>       <span class="token comment">// Nombre d'itérations (défaut: 4)</span>
    <span class="token string">'threads'</span>     <span class="token operator">=></span> <span class="token number">3</span><span class="token punctuation">,</span>       <span class="token comment">// Nombre de threads (défaut: 1)</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_ARGON2I</span><span class="token punctuation">,</span> <span class="token variable">$options</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">Déterminer le coût optimal</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// Fonction pour trouver le coût optimal</span>
<span class="token variable">$timeTarget</span> <span class="token operator">=</span> <span class="token number">0.05</span><span class="token punctuation">;</span> <span class="token comment">// 50 millisecondes</span>

<span class="token variable">$cost</span> <span class="token operator">=</span> <span class="token number">8</span><span class="token punctuation">;</span>
<span class="token keyword">do</span> <span class="token punctuation">{</span>
    <span class="token variable">$cost</span><span class="token operator">++</span><span class="token punctuation">;</span>
    <span class="token variable">$start</span> <span class="token operator">=</span> <span class="token function">microtime</span><span class="token punctuation">(</span><span class="token constant">true</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token string">"test"</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_BCRYPT</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">"cost"</span> <span class="token operator">=></span> <span class="token variable">$cost</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$end</span> <span class="token operator">=</span> <span class="token function">microtime</span><span class="token punctuation">(</span><span class="token constant">true</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span> <span class="token keyword">while</span> <span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token variable">$end</span> <span class="token operator">-</span> <span class="token variable">$start</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token variable">$timeTarget</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">echo</span> <span class="token string">"Coût optimal trouvé: "</span> <span class="token operator">.</span> <span class="token variable">$cost</span><span class="token punctuation">;</span>
<span class="token comment">// Résultat typique: 10-12 sur un serveur moderne</span></code></pre>
        </div>
      </section>

      <!-- Vérification des mots de passe -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Vérification avec password_verify()</h2>
        <p class="textExemple">
          Pour vérifier si un mot de passe correspond à un hash, utilisez la fonction <code>password_verify()</code>. Cette fonction est sécurisée contre les attaques temporelles.
        </p>
        
        <div class="code-example">
          <pre><code><span class="token comment">// Hachage du mot de passe (à l'inscription)</span>
<span class="token variable">$password</span> <span class="token operator">=</span> <span class="token string">'mon_mot_de_passe_secret'</span><span class="token punctuation">;</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Sauvegarde du hash en base de données</span>
<span class="token comment">// $hash = '$2y$10$X5z8M9aBcDeFgHiJkLmNoOqRsTuVwXyZABCDEFGHIJKLMNOPQRSTUV'</span>

<span class="token comment">// Vérification (à la connexion)</span>
<span class="token variable">$password_saisi</span> <span class="token operator">=</span> <span class="token string">'mon_mot_de_passe_secret'</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password_saisi</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">'Mot de passe correct !'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">'Mot de passe incorrect.'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
        </div>
        
        <h3 class="text-purple">Exemple complet d'authentification</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">inscrireUtilisateur</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    
    <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO users (email, password) VALUES (?, ?)"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">function</span> <span class="token function">verifierUtilisateur</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"SELECT id, email, password FROM users WHERE email = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$user</span> <span class="token operator">=</span> <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$user</span> <span class="token operator">&&</span> <span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token variable">$user</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">return</span> <span class="token constant">false</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token function">inscrireUtilisateur</span><span class="token punctuation">(</span><span class="token string">'alice@example.com'</span><span class="token punctuation">,</span> <span class="token string">'mot_de_passe_secret'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token variable">$user</span> <span class="token operator">=</span> <span class="token function">verifierUtilisateur</span><span class="token punctuation">(</span><span class="token string">'alice@example.com'</span><span class="token punctuation">,</span> <span class="token string">'mot_de_passe_secret'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$user</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">"Connexion réussie !"</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Réhachage des mots de passe -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Réhachage avec password_needs_rehash()</h2>
        <p class="textExemple">
          Lorsque les standards de sécurité évoluent ou que vous changez les options de hachage, vous pouvez utiliser <code>password_needs_rehash()</code> pour mettre à jour les anciens hash.
        </p>
        
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">verifierEtRehasher</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Vérifier d'abord le mot de passe</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Vérifier si le hash a besoin d'être mis à jour</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">password_needs_rehash</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// Créer un nouveau hash</span>
            <span class="token variable">$newHash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token comment">// Sauvegarder le nouveau hash en base de données</span>
            <span class="token function">mettreAJourHashUtilisateur</span><span class="token punctuation">(</span><span class="token variable">$userId</span><span class="token punctuation">,</span> <span class="token variable">$newHash</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token variable">$newHash</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">return</span> <span class="token constant">true</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">return</span> <span class="token constant">false</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Exemple d'utilisation avec des options spécifiques</span>
<span class="token variable">$options</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token number">12</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">password_needs_rehash</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token variable">$options</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Le hash a besoin d'être mis à jour avec un coût de 12</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques</h2>
        
        <h3 class="text-purple">1. Validation des mots de passe</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">validerMotDePasse</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Longueur minimale</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token number">8</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le mot de passe doit faire au moins 8 caractères"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Complexité</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[A-Z]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le mot de passe doit contenir au moins une majuscule"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[a-z]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le mot de passe doit contenir au moins une minuscule"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[0-9]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le mot de passe doit contenir au moins un chiffre"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">return</span> <span class="token variable">$erreurs</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token function">validerMotDePasse</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
        </div>
        
        <h3 class="text-purple">2. Gestion des erreurs</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">creerHashSecurise</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">try</span> <span class="token punctuation">{</span>
        <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$hash</span> <span class="token operator">===</span> <span class="token constant">false</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">Exception</span><span class="token punctuation">(</span><span class="token string">'Erreur lors de la création du hash'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token variable">$hash</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">Exception</span> <span class="token variable">$e</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token function">error_log</span><span class="token punctuation">(</span><span class="token string">"Erreur password_hash: "</span> <span class="token operator">.</span> <span class="token variable">$e</span><span class="token operator">-></span><span class="token function">getMessage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> <span class="token constant">false</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
        </div>
        
        <h3 class="text-purple">3. Classe utilitaire complète</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">class</span> <span class="token class-name">PasswordManager</span> <span class="token punctuation">{</span>
    <span class="token keyword">private</span> <span class="token variable">$options</span><span class="token punctuation">;</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">__construct</span><span class="token punctuation">(</span><span class="token variable">$cost</span> <span class="token operator">=</span> <span class="token number">12</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">options</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token variable">$cost</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">options</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">needsRehash</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">password_needs_rehash</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">options</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">validate</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$score</span> <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token operator">>=</span> <span class="token number">8</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token variable">$score</span><span class="token operator">++</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[A-Z]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token variable">$score</span><span class="token operator">++</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[a-z]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token variable">$score</span><span class="token operator">++</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[0-9]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token variable">$score</span><span class="token operator">++</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[^A-Za-z0-9]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token variable">$score</span><span class="token operator">++</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token variable">$score</span> <span class="token operator">>=</span> <span class="token number">4</span><span class="token punctuation">;</span> <span class="token comment">// Au moins 4 critères sur 5</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token variable">$pm</span> <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">PasswordManager</span><span class="token punctuation">(</span><span class="token number">12</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$pm</span><span class="token operator">-></span><span class="token function">validate</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token variable">$pm</span><span class="token operator">-></span><span class="token function">hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Pièges à éviter -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pièges à éviter</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">❌ À éviter</h4>
            <pre><code><span class="token comment">// Hash avec algorithme obsolète</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">md5</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Salt manuel (complexe et risqué)</span>
<span class="token variable">$salt</span> <span class="token operator">=</span> <span class="token string">'mon_salt_fixe'</span><span class="token punctuation">;</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">hash</span><span class="token punctuation">(</span><span class="token string">'sha256'</span><span class="token punctuation">,</span> <span class="token variable">$password</span> <span class="token operator">.</span> <span class="token variable">$salt</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Coût trop faible</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token number">4</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Stockage en clair (jamais !)</span>
<span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO users (password) VALUES (?)"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$password</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// DANGER !</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">✅ Bonnes pratiques</h4>
            <pre><code><span class="token comment">// Utilisation de password_hash()</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Coût adapté (10-12)</span>
<span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token number">12</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Vérification avec password_verify()</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$input</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Mot de passe correct</span>
<span class="token punctuation">}</span>

<span class="token comment">// Stockage sécurisé</span>
<span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO users (password) VALUES (?)"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$hash</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Système d'inscription sécurisé</h3>
          <p class="textExemple">
            Créez un système d'inscription complet avec validation du mot de passe, hachage sécurisé et gestion des erreurs.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="token keyword">class</span> <span class="token class-name">AuthSystem</span> <span class="token punctuation">{</span>
    <span class="token keyword">private</span> <span class="token variable">$pdo</span><span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token variable">$cost</span><span class="token punctuation">;</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">__construct</span><span class="token punctuation">(</span><span class="token constant">PDO</span> <span class="token variable">$pdo</span><span class="token punctuation">,</span> <span class="token variable">$cost</span> <span class="token operator">=</span> <span class="token number">12</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token punctuation">;</span>
        <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">cost</span> <span class="token operator">=</span> <span class="token variable">$cost</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">register</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Validation de l'email</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">InvalidArgumentException</span><span class="token punctuation">(</span><span class="token string">"Email invalide"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token comment">// Validation du mot de passe</span>
        <span class="token variable">$validation</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token function">validatePassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token variable">$validation</span><span class="token punctuation">[</span><span class="token string">'valid'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">InvalidArgumentException</span><span class="token punctuation">(</span><span class="token string">"Mot de passe invalide: "</span> <span class="token operator">.</span> <span class="token function">implode</span><span class="token punctuation">(</span><span class="token string">', '</span><span class="token punctuation">,</span> <span class="token variable">$validation</span><span class="token punctuation">[</span><span class="token string">'errors'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token comment">// Vérifier si l'email existe déjà</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"SELECT id FROM users WHERE email = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">Exception</span><span class="token punctuation">(</span><span class="token string">"Cet email est déjà utilisé"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token comment">// Hachage du mot de passe</span>
        <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token function">hashPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token comment">// Insertion en base</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO users (email, password, created_at) VALUES (?, ?, NOW())"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">return</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">lastInsertId</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">login</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"SELECT id, email, password FROM users WHERE email = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$user</span> <span class="token operator">=</span> <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token constant">PDO</span><span class="token operator">::</span><span class="token constant">FETCH_ASSOC</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token variable">$user</span> <span class="token operator">||</span> <span class="token operator">!</span><span class="token variable">$this</span><span class="token operator">-></span><span class="token function">verifyPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token constant">false</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token comment">// Vérifier si le hash a besoin d'être mis à jour</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$this</span><span class="token operator">-></span><span class="token function">needsRehash</span><span class="token punctuation">(</span><span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$newHash</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token function">hashPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token variable">$this</span><span class="token operator">-></span><span class="token function">updatePassword</span><span class="token punctuation">(</span><span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token variable">$newHash</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token variable">$user</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">private</span> <span class="token keyword">function</span> <span class="token function">hashPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">cost</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$hash</span> <span class="token operator">===</span> <span class="token constant">false</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">RuntimeException</span><span class="token punctuation">(</span><span class="token string">"Erreur lors du hachage du mot de passe"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token variable">$hash</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">private</span> <span class="token keyword">function</span> <span class="token function">verifyPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$hash</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">private</span> <span class="token keyword">function</span> <span class="token function">needsRehash</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">password_needs_rehash</span><span class="token punctuation">(</span><span class="token variable">$hash</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">'cost'</span> <span class="token operator">=></span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">cost</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">private</span> <span class="token keyword">function</span> <span class="token function">validatePassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$errors</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token number">8</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$errors</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Au moins 8 caractères"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[A-Z]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$errors</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Au moins une majuscule"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[a-z]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$errors</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Au moins une minuscule"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[0-9]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$errors</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Au moins un chiffre"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">preg_match</span><span class="token punctuation">(</span><span class="token string">'/[^A-Za-z0-9]/'</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$errors</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Au moins un caractère spécial"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token punctuation">[</span>
            <span class="token string">'valid'</span> <span class="token operator">=></span> <span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$errors</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
            <span class="token string">'errors'</span> <span class="token operator">=></span> <span class="token variable">$errors</span>
        <span class="token punctuation">]</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">private</span> <span class="token keyword">function</span> <span class="token function">updatePassword</span><span class="token punctuation">(</span><span class="token variable">$userId</span><span class="token punctuation">,</span> <span class="token variable">$newHash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"UPDATE users SET password = ? WHERE id = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$newHash</span><span class="token punctuation">,</span> <span class="token variable">$userId</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token keyword">try</span> <span class="token punctuation">{</span>
    <span class="token variable">$auth</span> <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">AuthSystem</span><span class="token punctuation">(</span><span class="token variable">$pdo</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$userId</span> <span class="token operator">=</span> <span class="token variable">$auth</span><span class="token operator">-></span><span class="token function">register</span><span class="token punctuation">(</span><span class="token string">'test@example.com'</span><span class="token punctuation">,</span> <span class="token string">'MonSuperMot2Passe!'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token function">var_dump</span><span class="token punctuation">(</span><span class="token string">"Utilisateur créé avec ID: "</span> <span class="token operator">.</span> <span class="token variable">$userId</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">Exception</span> <span class="token variable">$e</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token function">var_dump</span><span class="token punctuation">(</span><span class="token string">"Erreur: "</span> <span class="token operator">.</span> <span class="token variable">$e</span><span class="token operator">-></span><span class="token function">getMessage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
            </div>
          </details>
        </div>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Migration depuis ancien système</h3>
          <p class="textExemple">
            Créez un système qui peut migrer des mots de passe depuis un ancien système utilisant md5 vers password_hash().
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="token keyword">class</span> <span class="token class-name">PasswordMigrator</span> <span class="token punctuation">{</span>
    <span class="token keyword">private</span> <span class="token variable">$pdo</span><span class="token punctuation">;</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">__construct</span><span class="token punctuation">(</span><span class="token constant">PDO</span> <span class="token variable">$pdo</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">verifyLegacyPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$legacyHash</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Vérifier avec l'ancien système (md5)</span>
        <span class="token keyword">return</span> <span class="token function">md5</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token operator">===</span> <span class="token variable">$legacyHash</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">migrateUser</span><span class="token punctuation">(</span><span class="token variable">$userId</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Créer un nouveau hash sécurisé</span>
        <span class="token variable">$newHash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token comment">// Mettre à jour la base de données</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"UPDATE users SET password = ?, password_legacy = NULL WHERE id = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$newHash</span><span class="token punctuation">,</span> <span class="token variable">$userId</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">public</span> <span class="token keyword">function</span> <span class="token function">verifyAndMigrate</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Récupérer l'utilisateur</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token property">pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span>
            <span class="token string">"SELECT id, password, password_legacy FROM users WHERE email = ?"</span>
        <span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$user</span> <span class="token operator">=</span> <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token constant">PDO</span><span class="token operator">::</span><span class="token constant">FETCH_ASSOC</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token variable">$user</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token constant">false</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token comment">// Si le mot de passe est déjà en password_hash</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token variable">$user</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token comment">// Si le mot de passe est en legacy (md5) et correct</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password_legacy'</span><span class="token punctuation">]</span> <span class="token operator">&&</span> <span class="token variable">$this</span><span class="token operator">-></span><span class="token function">verifyLegacyPassword</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password_legacy'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// Migrer vers password_hash</span>
            <span class="token variable">$this</span><span class="token operator">-></span><span class="token function">migrateUser</span><span class="token punctuation">(</span><span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token keyword">return</span> <span class="token variable">$user</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token constant">false</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token variable">$migrator</span> <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">PasswordMigrator</span><span class="token punctuation">(</span><span class="token variable">$pdo</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$user</span> <span class="token operator">=</span> <span class="token variable">$migrator</span><span class="token operator">-></span><span class="token function">verifyAndMigrate</span><span class="token punctuation">(</span><span class="token string">'ancien@example.com'</span><span class="token punctuation">,</span> <span class="token string">'ancien_mot_de_passe'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$user</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">echo</span> <span class="token string">"Connexion réussie et mot de passe migré !"</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          La fonction <code>password_hash()</code> est la méthode recommandée pour sécuriser les mots de passe en PHP. Elle offre une sécurité robuste tout en restant simple à utiliser.
        </p>
        <p class="textExemple">
          Points clés à retenir :
        </p>
        <ul class="textExemple">
          <li>Utilisez toujours <code>PASSWORD_DEFAULT</code> pour l'algorithme</li>
          <li>Le coût (cost) doit être adapté à votre matériel (10-12 typiquement)</li>
          <li>Utilisez <code>password_verify()</code> pour vérifier les mots de passe</li>
          <li>Utilisez <code>password_needs_rehash()</code> pour mettre à jour les anciens hash</li>
          <li>Validez toujours la complexité des mots de passe</li>
          <li>Jamais de stockage en clair des mots de passe</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonPasswordHash',
}
</script>

<style scoped>
/* Les styles sont identiques aux leçons précédentes */
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