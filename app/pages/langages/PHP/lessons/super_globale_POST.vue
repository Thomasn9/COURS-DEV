<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">La superglobale $_POST en PHP</h1>
        <p class="lesson-meta text-white">Traiter les données de formulaires en toute sécurité</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p class="textExemple">
          La superglobale <code>$_POST</code> est essentielle en PHP pour récupérer les données envoyées via des formulaires HTML avec la méthode POST. Contrairement à <code>$_GET</code>, les données de <code>$_POST</code> ne sont pas visibles dans l'URL, ce qui les rend idéales pour les informations sensibles.
        </p>
      </section>

      <!-- Qu'est-ce que $_POST -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Qu'est-ce que la superglobale $_POST ?</h2>
        <p class="textExemple">
          <code>$_POST</code> est un tableau associatif qui contient toutes les variables envoyées via un formulaire HTML avec la méthode POST. Les données sont envoyées dans le corps de la requête HTTP, ce qui les rend invisibles dans l'URL.
        </p>
        
        <div class="code-example">
          <pre><code><span class="token comment">// Exemple de formulaire HTML</span>
<span class="token delimiter">&lt;?</span><span class="token variable">form</span> <span class="token variable">method</span><span class="token operator">=</span><span class="token string">"POST"</span> <span class="token variable">action</span><span class="token operator">=</span><span class="token string">"traitement.php"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"text"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"nom"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"email"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"email"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"password"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"mot_de_passe"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">button</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"submit"</span><span class="token delimiter">?></span>Envoyer<span class="token delimiter">&lt;?/</span><span class="token variable">button</span><span class="token delimiter">?></span>
<span class="token delimiter">&lt;?/</span><span class="token variable">form</span><span class="token delimiter">?></span>

<span class="token comment">// Dans traitement.php, $_POST contiendra :</span>
<span class="token variable">$_POST</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
    <span class="token string">'nom'</span>          <span class="token operator">=></span> <span class="token string">'Alice Dupont'</span><span class="token punctuation">,</span>
    <span class="token string">'email'</span>        <span class="token operator">=></span> <span class="token string">'alice@example.com'</span><span class="token punctuation">,</span>
    <span class="token string">'mot_de_passe'</span> <span class="token operator">=></span> <span class="token string">'mon_mot_de_passe_secret'</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span></code></pre>
        </div>
      </section>

      <!-- Syntaxe de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Syntaxe de base</h2>
        <p class="textExemple">
          Pour accéder aux valeurs de <code>$_POST</code>, on utilise la même syntaxe que pour <code>$_GET</code> :
        </p>
        
        <div class="code-example">
          <pre><code><span class="token comment">// Récupérer une valeur simple</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token comment">// Récupérer avec une valeur par défaut</span>
<span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token punctuation">:</span> <span class="token string">''</span><span class="token punctuation">;</span>

<span class="token comment">// Vérifier si un champ existe</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'mot_de_passe'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$motDePasse</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'mot_de_passe'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Vérifier si le formulaire a été soumis</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Traiter le formulaire</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Exemples pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemples pratiques</h2>
        
        <h3 class="text-purple">Exemple 1 : Formulaire de contact</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// contact.php</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Récupération et validation des données</span>
    <span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$message</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    
    <span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$nom</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le nom est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token variable">$email</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email n'est pas valide"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$message</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le message ne peut pas être vide"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Si pas d'erreurs, traiter le formulaire</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Envoyer l'email ou sauvegarder en base</span>
        <span class="token variable">$succes</span> <span class="token operator">=</span> <span class="token string">"Votre message a été envoyé avec succès !"</span><span class="token punctuation">;</span>
        <span class="token comment">// Réinitialiser les champs</span>
        <span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token variable">$email</span> <span class="token operator">=</span> <span class="token variable">$message</span> <span class="token operator">=</span> <span class="token string">''</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
        </div>
        
        <h3 class="text-purple">Exemple 2 : Système d'inscription</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// register.php</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$username</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'username'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$password</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">;</span>
    <span class="token variable">$confirm_password</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'confirm_password'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">;</span>
    
    <span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$username</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token number">3</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'username'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le nom d'utilisateur doit faire au moins 3 caractères"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token variable">$email</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email n'est pas valide"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token number">8</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le mot de passe doit faire au moins 8 caractères"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$password</span> <span class="token operator">!==</span> <span class="token variable">$confirm_password</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'confirm_password'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Les mots de passe ne correspondent pas"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Vérifier si l'email existe déjà</span>
    <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"SELECT id FROM users WHERE email = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Cet email est déjà utilisé"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Si pas d'erreurs, créer l'utilisateur</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$password_hash</span> <span class="token operator">=</span> <span class="token function">password_hash</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token constant">PASSWORD_DEFAULT</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO users (username, email, password) VALUES (?, ?, ?)"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$username</span><span class="token punctuation">,</span> <span class="token variable">$email</span><span class="token punctuation">,</span> <span class="token variable">$password_hash</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token variable">$succes</span> <span class="token operator">=</span> <span class="token string">"Votre compte a été créé avec succès !"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
        </div>
        
        <h3 class="text-purple">Exemple 3 : Upload de fichier avec $_POST et $_FILES</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// upload.php - Formulaire avec enctype="multipart/form-data"</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$titre</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'titre'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$description</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'description'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$fichier</span> <span class="token operator">=</span> <span class="token variable">$_FILES</span><span class="token punctuation">[</span><span class="token string">'fichier'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token constant">null</span><span class="token punctuation">;</span>
    
    <span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation des champs POST</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$titre</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le titre est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Validation du fichier</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$fichier</span> <span class="token operator">&&</span> <span class="token variable">$fichier</span><span class="token punctuation">[</span><span class="token string">'error'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token constant">UPLOAD_ERR_OK</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$types_autorises</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'image/jpeg'</span><span class="token punctuation">,</span> <span class="token string">'image/png'</span><span class="token punctuation">,</span> <span class="token string">'image/gif'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token variable">$taille_max</span> <span class="token operator">=</span> <span class="token number">5</span> <span class="token operator">*</span> <span class="token number">1024</span> <span class="token operator">*</span> <span class="token number">1024</span><span class="token punctuation">;</span> <span class="token comment">// 5MB</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">in_array</span><span class="token punctuation">(</span><span class="token variable">$fichier</span><span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token variable">$types_autorises</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Type de fichier non autorisé"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$fichier</span><span class="token punctuation">[</span><span class="token string">'size'</span><span class="token punctuation">]</span> <span class="token operator">></span> <span class="token variable">$taille_max</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le fichier est trop volumineux"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Veuillez sélectionner un fichier"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Si pas d'erreurs, traiter l'upload</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$extension</span> <span class="token operator">=</span> <span class="token function">pathinfo</span><span class="token punctuation">(</span><span class="token variable">$fichier</span><span class="token punctuation">[</span><span class="token string">'name'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token constant">PATHINFO_EXTENSION</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$nom_fichier</span> <span class="token operator">=</span> <span class="token function">uniqid</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">'.'</span> <span class="token operator">.</span> <span class="token variable">$extension</span><span class="token punctuation">;</span>
        <span class="token variable">$destination</span> <span class="token operator">=</span> <span class="token string">"uploads/"</span> <span class="token operator">.</span> <span class="token variable">$nom_fichier</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">move_uploaded_file</span><span class="token punctuation">(</span><span class="token variable">$fichier</span><span class="token punctuation">[</span><span class="token string">'tmp_name'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token variable">$destination</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// Sauvegarder en base de données</span>
            <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO fichiers (titre, description, nom_fichier) VALUES (?, ?, ?)"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$titre</span><span class="token punctuation">,</span> <span class="token variable">$description</span><span class="token punctuation">,</span> <span class="token variable">$nom_fichier</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            
            <span class="token variable">$succes</span> <span class="token operator">=</span> <span class="token string">"Fichier uploadé avec succès !"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Erreur lors de l'upload du fichier"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Sécurité avec $_POST -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Sécurité avec $_POST</h2>
        <p class="textExemple">
          Bien que <code>$_POST</code> soit plus sécurisé que <code>$_GET</code> car les données ne sont pas visibles dans l'URL, il reste essentiel de valider et sécuriser toutes les données reçues.
        </p>
        
        <h3 class="text-purple">Protections essentielles</h3>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">❌ Non sécurisé</h4>
            <pre><code><span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token variable">$email</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token comment">// Injection SQL possible</span>
<span class="token variable">$requete</span> <span class="token operator">=</span> <span class="token string">"INSERT INTO users (nom, email) VALUES ('</span><span class="token variable">$nom</span><span class="token string">', '</span><span class="token variable">$email</span><span class="token string">')"</span><span class="token punctuation">;</span>

<span class="token comment">// XSS possible</span>
<span class="token keyword">echo</span> <span class="token string">"&lt;div>Bonjour </span><span class="token variable">$nom</span><span class="token string">&lt;/div>"</span><span class="token punctuation">;</span></code></pre>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">✅ Sécurisé</h4>
            <pre><code><span class="token comment">// Validation et nettoyage</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Protection contre l'injection SQL</span>
<span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO users (nom, email) VALUES (?, ?)"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$nom</span><span class="token punctuation">,</span> <span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Protection contre XSS</span>
<span class="token keyword">echo</span> <span class="token string">"&lt;div>Bonjour "</span> <span class="token operator">.</span> <span class="token function">htmlspecialchars</span><span class="token punctuation">(</span><span class="token variable">$nom</span><span class="token punctuation">)</span> <span class="token operator">.</span> <span class="token string">"&lt;/div>"</span><span class="token punctuation">;</span></code></pre>
          </div>
        </div>
        
        <h3 class="text-purple">CSRF Protection</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// Génération du token CSRF</span>
<span class="token keyword">function</span> <span class="token function">genererTokenCSRF</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token function">bin2hex</span><span class="token punctuation">(</span><span class="token function">random_bytes</span><span class="token punctuation">(</span><span class="token number">32</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Vérification du token CSRF</span>
<span class="token keyword">function</span> <span class="token function">verifierTokenCSRF</span><span class="token punctuation">(</span><span class="token variable">$token</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">&&</span> 
           <span class="token function">hash_equals</span><span class="token punctuation">(</span><span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token variable">$token</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Dans le formulaire</span>
<span class="token variable">$csrf_token</span> <span class="token operator">=</span> <span class="token function">genererTokenCSRF</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">echo</span> <span class="token string">'&lt;input type="hidden" name="csrf_token" value="'</span> <span class="token operator">.</span> <span class="token variable">$csrf_token</span> <span class="token operator">.</span> <span class="token string">'"&gt;'</span><span class="token punctuation">;</span>

<span class="token comment">// Lors du traitement</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$token</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">verifierTokenCSRF</span><span class="token punctuation">(</span><span class="token variable">$token</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">die</span><span class="token punctuation">(</span><span class="token string">"Token CSRF invalide"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token comment">// Traitement sécurisé...</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Différences avec $_GET -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Différences entre $_POST et $_GET</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h4 class="text-purple">$_POST</h4>
            <ul class="textExemple">
              <li>✅ Données dans le corps de la requête</li>
              <li>✅ Invisibles dans l'URL</li>
              <li>✅ Pas de limite pratique de taille</li>
              <li>✅ Non mis en cache</li>
              <li>✅ Idéal pour les données sensibles</li>
              <li>✅ Supporte les fichiers</li>
              <li>❌ Ne peut pas être bookmarké</li>
            </ul>
          </div>
          
          <div class="code-example">
            <h4 class="text-purple">$_GET</h4>
            <ul class="textExemple">
              <li>✅ Données dans l'URL</li>
              <li>✅ Visibles et modifiables</li>
              <li>✅ Limitée en taille (~2048 caractères)</li>
              <li>✅ Peut être mis en cache</li>
              <li>✅ Idéal pour la recherche et filtres</li>
              <li>❌ Ne supporte pas les fichiers</li>
              <li>✅ Peut être bookmarké</li>
            </ul>
          </div>
        </div>
        
        <h3 class="text-purple">Quand utiliser $_POST ?</h3>
        <div class="code-example">
          <pre><code><span class="token comment">// ✅ Bon usage de POST</span>
<span class="token delimiter">&lt;?</span><span class="token variable">form</span> <span class="token variable">method</span><span class="token operator">=</span><span class="token string">"POST"</span> <span class="token variable">action</span><span class="token operator">=</span><span class="token string">"login.php"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"email"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"email"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"password"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"password"</span><span class="token delimiter">?></span>
<span class="token delimiter">&lt;?/</span><span class="token variable">form</span><span class="token delimiter">?></span>

<span class="token delimiter">&lt;?</span><span class="token variable">form</span> <span class="token variable">method</span><span class="token operator">=</span><span class="token string">"POST"</span> <span class="token variable">action</span><span class="token operator">=</span><span class="token string">"register.php"</span> <span class="token variable">enctype</span><span class="token operator">=</span><span class="token string">"multipart/form-data"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"file"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"avatar"</span><span class="token delimiter">?></span>
<span class="token delimiter">&lt;?/</span><span class="token variable">form</span><span class="token delimiter">?></span>

<span class="token comment">// ❌ Mauvais usage de POST</span>
<span class="token delimiter">&lt;?</span><span class="token variable">form</span> <span class="token variable">method</span><span class="token operator">=</span><span class="token string">"POST"</span> <span class="token variable">action</span><span class="token operator">=</span><span class="token string">"search.php"</span><span class="token delimiter">?></span>
    <span class="token delimiter">&lt;?</span><span class="token variable">input</span> <span class="token variable">type</span><span class="token operator">=</span><span class="token string">"text"</span> <span class="token variable">name</span><span class="token operator">=</span><span class="token string">"q"</span><span class="token delimiter">?></span>
<span class="token delimiter">&lt;?/</span><span class="token variable">form</span><span class="token delimiter">?></span>
<span class="token comment">// => Mieux vaut utiliser GET pour la recherche</span></code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes pratiques avec $_POST</h2>
        
        <h3 class="text-purple">1. Validation complète des données</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">validerFormulaire</span><span class="token punctuation">(</span><span class="token variable">$data</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation du nom</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$data</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le nom est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">elseif</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$data</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token number">2</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le nom doit faire au moins 2 caractères"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Validation de l'email</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$data</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">elseif</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$data</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email n'est pas valide"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">return</span> <span class="token variable">$erreurs</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation</span>
<span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token function">validerFormulaire</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">2. Fonction utilitaire pour $_POST</h3>
        <div class="code-example">
          <pre><code><span class="token keyword">function</span> <span class="token function">post</span><span class="token punctuation">(</span><span class="token variable">$key</span><span class="token punctuation">,</span> <span class="token variable">$default</span> <span class="token operator">=</span> <span class="token constant">null</span><span class="token punctuation">,</span> <span class="token variable">$filter</span> <span class="token operator">=</span> <span class="token constant">FILTER_DEFAULT</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$value</span> <span class="token operator">=</span> <span class="token function">filter_input</span><span class="token punctuation">(</span><span class="token constant">INPUT_POST</span><span class="token punctuation">,</span> <span class="token variable">$key</span><span class="token punctuation">,</span> <span class="token variable">$filter</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token variable">$value</span> <span class="token operator">!==</span> <span class="token constant">null</span> <span class="token operator">?</span> <span class="token variable">$value</span> <span class="token punctuation">:</span> <span class="token variable">$default</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// Utilisation sécurisée</span>
<span class="token variable">$nom</span> <span class="token operator">=</span> <span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'nom'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_SANITIZE_STRING</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'email'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token variable">$age</span> <span class="token operator">=</span> <span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'age'</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_INT</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
        </div>
        
        <h3 class="text-purple">3. Pattern de traitement de formulaire</h3>
        <div class="code-example">
          <pre><code><span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token variable">$donnees</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Récupération des données</span>
    <span class="token variable">$donnees</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
        <span class="token string">'nom'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token string">'email'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token string">'message'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span>
    <span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le nom est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">elseif</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email n'est pas valide"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Si pas d'erreurs, traiter</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Traitement réussi</span>
        <span class="token variable">$succes</span> <span class="token operator">=</span> <span class="token string">"Formulaire traité avec succès"</span><span class="token punctuation">;</span>
        <span class="token comment">// Réinitialiser ou rediriger</span>
        <span class="token variable">$donnees</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span> <span class="token comment">// Réinitialiser les champs</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1 : Formulaire de contact sécurisé</h3>
          <p class="textExemple">
            Créez un formulaire de contact avec validation complète, protection CSRF et envoi d'email sécurisé.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="token comment">// contact_securise.php</span>
<span class="token function">session_start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">function</span> <span class="token function">genererTokenCSRF</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token function">bin2hex</span><span class="token punctuation">(</span><span class="token function">random_bytes</span><span class="token punctuation">(</span><span class="token number">32</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">return</span> <span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
<span class="token variable">$succes</span> <span class="token operator">=</span> <span class="token string">''</span><span class="token punctuation">;</span>
<span class="token variable">$donnees</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
    <span class="token string">'nom'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">,</span>
    <span class="token string">'email'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">,</span>
    <span class="token string">'sujet'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">,</span>
    <span class="token string">'message'</span> <span class="token operator">=></span> <span class="token string">''</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">// Vérification CSRF</span>
    <span class="token variable">$token</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">hash_equals</span><span class="token punctuation">(</span><span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'csrf_token'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token variable">$token</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Erreur de sécurité"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Récupération des données</span>
    <span class="token variable">$donnees</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
        <span class="token string">'nom'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token string">'email'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token string">'sujet'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'sujet'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
        <span class="token string">'message'</span> <span class="token operator">=></span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span>
    <span class="token punctuation">]</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le nom est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">elseif</span> <span class="token punctuation">(</span><span class="token operator">!</span><span class="token function">filter_var</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token constant">FILTER_VALIDATE_EMAIL</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email n'est pas valide"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le message est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">elseif</span> <span class="token punctuation">(</span><span class="token function">strlen</span><span class="token punctuation">(</span><span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator"><</span> <span class="token number">10</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le message doit faire au moins 10 caractères"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Si pas d'erreurs, envoyer l'email</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$destinataire</span> <span class="token operator">=</span> <span class="token string">"contact@monsite.com"</span><span class="token punctuation">;</span>
        <span class="token variable">$sujet</span> <span class="token operator">=</span> <span class="token string">"Contact: "</span> <span class="token operator">.</span> <span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'sujet'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token variable">$message</span> <span class="token operator">=</span> <span class="token string">"Nom: "</span> <span class="token operator">.</span> <span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'nom'</span><span class="token punctuation">]</span> <span class="token operator">.</span> <span class="token string">"\n"</span>
                  <span class="token operator">.</span> <span class="token string">"Email: "</span> <span class="token operator">.</span> <span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">.</span> <span class="token string">"\n"</span>
                  <span class="token operator">.</span> <span class="token string">"Message: "</span> <span class="token operator">.</span> <span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'message'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token variable">$headers</span> <span class="token operator">=</span> <span class="token string">"From: "</span> <span class="token operator">.</span> <span class="token variable">$donnees</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">mail</span><span class="token punctuation">(</span><span class="token variable">$destinataire</span><span class="token punctuation">,</span> <span class="token variable">$sujet</span><span class="token punctuation">,</span> <span class="token variable">$message</span><span class="token punctuation">,</span> <span class="token variable">$headers</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token variable">$succes</span> <span class="token operator">=</span> <span class="token string">"Votre message a été envoyé avec succès !"</span><span class="token punctuation">;</span>
            <span class="token variable">$donnees</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'nom'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token string">'email'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token string">'sujet'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">,</span> <span class="token string">'message'</span> <span class="token operator">=></span> <span class="token string">''</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Erreur lors de l'envoi du message"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token variable">$csrf_token</span> <span class="token operator">=</span> <span class="token function">genererTokenCSRF</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
            </div>
          </details>
        </div>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 2 : Système de connexion</h3>
          <p class="textExemple">
            Créez un système de connexion sécurisé avec vérification du mot de passe et gestion de session.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="token comment">// login.php</span>
<span class="token function">session_start</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Rediriger si déjà connecté</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">isset</span><span class="token punctuation">(</span><span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'user_id'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token function">header</span><span class="token punctuation">(</span><span class="token string">'Location: dashboard.php'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">exit</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token variable">$erreurs</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$_SERVER</span><span class="token punctuation">[</span><span class="token string">'REQUEST_METHOD'</span><span class="token punctuation">]</span> <span class="token operator">===</span> <span class="token string">'POST'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token variable">$email</span> <span class="token operator">=</span> <span class="token function">trim</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token variable">$password</span> <span class="token operator">=</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span> <span class="token operator">??</span> <span class="token string">''</span><span class="token punctuation">;</span>
    
    <span class="token comment">// Validation basique</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$email</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"L'email est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Le mot de passe est obligatoire"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token comment">// Si pas d'erreurs, vérifier les identifiants</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">empty</span><span class="token punctuation">(</span><span class="token variable">$erreurs</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Récupérer l'utilisateur depuis la base</span>
        <span class="token variable">$stmt</span> <span class="token operator">=</span> <span class="token variable">$pdo</span><span class="token operator">-></span><span class="token function">prepare</span><span class="token punctuation">(</span><span class="token string">"SELECT id, email, password FROM users WHERE email = ?"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">execute</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token variable">$email</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token variable">$user</span> <span class="token operator">=</span> <span class="token variable">$stmt</span><span class="token operator">-></span><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token variable">$user</span> <span class="token operator">&&</span> <span class="token function">password_verify</span><span class="token punctuation">(</span><span class="token variable">$password</span><span class="token punctuation">,</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'password'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// Connexion réussie</span>
            <span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'user_id'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'id'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
            <span class="token variable">$_SESSION</span><span class="token punctuation">[</span><span class="token string">'user_email'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token variable">$user</span><span class="token punctuation">[</span><span class="token string">'email'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
            
            <span class="token function">header</span><span class="token punctuation">(</span><span class="token string">'Location: dashboard.php'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token keyword">exit</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token variable">$erreurs</span><span class="token punctuation">[</span><span class="token string">'general'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"Email ou mot de passe incorrect"</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          La superglobale <code>$_POST</code> est indispensable pour traiter les données de formulaires en PHP de manière sécurisée. Elle permet de récupérer les informations envoyées par les utilisateurs tout en les protégeant contre diverses attaques.
        </p>
        <p class="textExemple">
          Points clés à retenir :
        </p>
        <ul class="textExemple">
          <li><code>$_POST</code> récupère les données du corps de la requête HTTP</li>
          <li>Idéal pour les données sensibles (mots de passe, informations personnelles)</li>
          <li>Toujours valider et nettoyer les données de <code>$_POST</code></li>
          <li>Utiliser la protection CSRF pour les formulaires critiques</li>
          <li>Préparer les requêtes SQL pour éviter les injections</li>
          <li>Échapper les sorties HTML avec <code>htmlspecialchars()</code></li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonPostSuperglobal',
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