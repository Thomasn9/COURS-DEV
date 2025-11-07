<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Documentation Technique & Lisibilité du Code</h1>
                <p class="lesson-meta text-white">Best practices pour un code maintenable et auditable</p>
            </header>

            <!-- Section 1: Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi la documentation et la lisibilité sont cruciales</h2>
                <p class="textExemple">
                    Dans un contexte d'audit, la qualité du code ne se mesure pas seulement à sa fonctionnalité,
                    mais aussi à sa capacité à être compris, maintenu et audité par d'autres développeurs.
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ Code bien documenté</h4>
                        <ul class="textExemple">
                            <li>Facilite la maintenance</li>
                            <li>Réduit le temps d'onboarding</li>
                            <li>Permet un audit efficace</li>
                            <li>Diminue les risques d'erreurs</li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="text-purple">❌ Code non documenté</h4>
                        <ul class="textExemple">
                            <li>Coûts de maintenance élevés</li>
                            <li>Dépendance aux développeurs initiaux</li>
                            <li>Difficulté d'audit</li>
                            <li>Risques de régression</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Section 2: Types de documentation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les différents types de documentation</h2>
                <p class="textExemple">
                    Une documentation complète couvre plusieurs niveaux :
                </p>
                <div class="code-example">
                    <pre><code><span class="comment">// 1. Documentation de code (inline)</span>
<span class="comment">// 2. Documentation technique (API, architecture)</span>
<span class="comment">// 3. Documentation utilisateur (manuels, guides)</span>
<span class="comment">// 4. Documentation de projet (README, setup)</span></code></pre>
                </div>

                <h3 class="text-purple">Niveaux de documentation</h3>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Documentation Interne</h4>
                        <pre><code><span class="comment">/**
 * Calcule le prix TTC d'un produit
 * @param float $prixHT Prix hors taxes
 * @param float $tauxTVA Taux de TVA (ex: 0.2 pour 20%)
 * @return float Prix TTC arrondi à 2 décimales
 */</span>
<span class="keyword">function</span> <span class="function">calculerPrixTTC</span>(<span class="variable">$prixHT</span>, <span class="variable">$tauxTVA</span> = <span class="number">0.2</span>) {
    <span class="keyword">return</span> <span class="function">round</span>(<span class="variable">$prixHT</span> * (<span class="number">1</span> + <span class="variable">$tauxTVA</span>), <span class="number">2</span>);
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Documentation Externe</h4>
                        <pre><code><span class="comment"># API - Endpoint Utilisateurs
## GET /api/users/{id}
- **Description**: Récupère les infos d'un utilisateur
- **Paramètres**: id (integer, required)
- **Réponse**: 
  - 200: User object
  - 404: User not found
- **Exemple**: 
  ```json
  {
    "id": 123,
    "name": "John Doe",
    "email": "john@example.com"
  }
  ```</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Section 3: Bonnes pratiques de commentaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques des commentaires</h2>
                <p class="textExemple">
                    Les commentaires doivent expliquer le "pourquoi" plutôt que le "comment".
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ Commentaires utiles</h4>
                        <pre><code><span class="comment">// Conversion nécessaire car l'API externe 
// retourne les prix en cents</span>
<span class="variable">$prixEnEuros</span> = <span class="variable">$prixEnCents</span> / <span class="number">100</span>;

<span class="comment">// Contournement temporaire pour le bug #1234
// de la librairie de paiement</span>
<span class="keyword">if</span> (<span class="variable">$montant</span> &gt; <span class="number">1000</span>) {
    <span class="function">logger</span>(<span class="string">"Transaction suspecte détectée"</span>);
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">❌ Commentaires inutiles</h4>
                        <pre><code><span class="comment">// Incrémente i de 1</span>
<span class="variable">$i</span>++;

<span class="comment">// Ajoute nom à la liste</span>
<span class="variable">$liste</span>[] = <span class="variable">$nom</span>;

<span class="comment">// Si l'utilisateur est admin</span>
<span class="keyword">if</span> (<span class="variable">$user</span>-&gt;isAdmin()) {
    <span class="comment">// Faire quelque chose</span>
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Section 4: Standards de documentation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Standards de documentation</h2>
                <p class="textExemple">
                    Utilisez des standards reconnus comme PHPDoc pour une documentation cohérente.
                </p>
                <div class="code-example">
                    <pre><code><span class="comment">/**
 * Gère l'authentification des utilisateurs
 * 
 * @package    Auth
 * @author     John Doe &lt;john@example.com&gt;
 * @version    1.2.0
 * @since      2020-01-01
 */</span>
<span class="keyword">class</span> <span class="class-name">Authenticator</span> {
    
    <span class="comment">/**
     * Vérifie les credentials utilisateur
     *
     * @param string $email Email de l'utilisateur
     * @param string $password Mot de passe en clair
     * @param bool $remember Se souvenir de la connexion
     * 
     * @return User|false Utilisateur ou false si échec
     * 
     * @throws AuthenticationException Si erreur technique
     * @throws RateLimitException Si trop de tentatives
     * 
     * @example
     * $user = $auth->login('test@example.com', 'password');
     */</span>
    <span class="keyword">public</span> <span class="keyword">function</span> <span class="function">login</span>(<span class="variable">$email</span>, <span class="variable">$password</span>, <span class="variable">$remember</span> = <span class="keyword">false</span>) {
        <span class="comment">// Implémentation...</span>
    }
}</code></pre>
                </div>
            </section>

            <!-- Section 5: Lisibilité du code -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Principes de lisibilité</h2>
                <p class="textExemple">
                    Un code lisible est un code qui se comprend de lui-même.
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ Code expressif</h4>
                        <pre><code><span class="keyword">public</span> <span class="keyword">function</span> <span class="function">calculateOrderTotal</span>(<span class="class-name">Order</span> <span class="variable">$order</span>) {
    <span class="variable">$subtotal</span> = <span class="variable">$order</span>-&gt;<span class="function">getSubtotal</span>();
    <span class="variable">$shipping</span> = <span class="variable">$order</span>-&gt;<span class="function">getShippingCost</span>();
    <span class="variable">$discount</span> = <span class="variable">$order</span>-&gt;<span class="function">getDiscountAmount</span>();
    
    <span class="keyword">return</span> <span class="variable">$subtotal</span> + <span class="variable">$shipping</span> - <span class="variable">$discount</span>;
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">❌ Code cryptique</h4>
                        <pre><code><span class="keyword">public</span> <span class="keyword">function</span> <span class="function">calc</span>(<span class="class-name">Order</span> <span class="variable">$o</span>) {
    <span class="variable">$a</span> = <span class="variable">$o</span>-&gt;<span class="function">s</span>();
    <span class="variable">$b</span> = <span class="variable">$o</span>-&gt;<span class="function">sc</span>();
    <span class="variable">$c</span> = <span class="variable">$o</span>-&gt;<span class="function">da</span>();
    
    <span class="keyword">return</span> <span class="variable">$a</span> + <span class="variable">$b</span> - <span class="variable">$c</span>;
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Section 6: Complexité cyclomatique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gérer la complexité</h2>
                <p class="textExemple">
                    La complexité cyclomatique mesure la difficulté de compréhension d'une fonction.
                </p>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">✅ Complexité maîtrisée</h4>
                        <pre><code><span class="keyword">public</span> <span class="keyword">function</span> <span class="function">processPayment</span>(<span class="class-name">Payment</span> <span class="variable">$payment</span>) {
    <span class="keyword">if</span> (!<span class="variable">$payment</span>-&gt;<span class="function">isValid</span>()) {
        <span class="keyword">throw new</span> <span class="class-name">InvalidPaymentException</span>();
    }
    
    <span class="variable">$this</span>-&gt;<span class="function">validateAmount</span>(<span class="variable">$payment</span>);
    <span class="variable">$this</span>-&gt;<span class="function">processWithGateway</span>(<span class="variable">$payment</span>);
    
    <span class="keyword">return</span> <span class="variable">$this</span>-&gt;<span class="function">createReceipt</span>(<span class="variable">$payment</span>);
}</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">❌ Complexité élevée</h4>
                        <pre><code><span class="keyword">public</span> <span class="keyword">function</span> <span class="function">processPayment</span>(<span class="class-name">Payment</span> <span class="variable">$p</span>) {
    <span class="keyword">if</span> (<span class="variable">$p</span>-&gt;<span class="function">v</span>() &amp;&amp; <span class="variable">$p</span>-&gt;<span class="function">a</span>() &gt; <span class="number">0</span> &amp;&amp; 
        <span class="variable">$p</span>-&gt;<span class="function">c</span>() != <span class="keyword">null</span> &amp;&amp; 
        !<span class="variable">$p</span>-&gt;<span class="function">e</span>()) {
        <span class="keyword">try</span> {
            <span class="comment">// 50 lignes de code...</span>
        } <span class="keyword">catch</span> (<span class="class-name">Exception1</span> <span class="variable">$e1</span>) {
            <span class="comment">// Gestion...</span>
        } <span class="keyword">catch</span> (<span class="class-name">Exception2</span> <span class="variable">$e2</span>) {
            <span class="comment">// Gestion...</span>
        }
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Section 7: Outils d'analyse -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils d'analyse de code</h2>
                <p class="textExemple">
                    Utilisez des outils automatisés pour mesurer la qualité du code.
                </p>
                <div class="code-example">
                    <pre><code><span class="comment"># PHPStan - Analyse statique</span>
vendor/bin/phpstan analyse src --level=8

<span class="comment"># PHPCodeSniffer - Standards de code</span>
vendor/bin/phpcs src --standard=PSR12

<span class="comment"># PHPMD - Détection des mauvaises pratiques</span>
vendor/bin/phpmd src text cleancode,codesize,design

<span class="comment"># PHPCPD - Détection de code dupliqué</span>
vendor/bin/phpcpd src

<span class="comment"># SonarQube - Analyse complète</span>
sonar-scanner -Dsonar.projectKey=mon-projet</code></pre>
                </div>

                <h3 class="text-purple">Métriques importantes</h3>
                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Qualité</h4>
                        <ul class="textExemple">
                            <li><strong>Complexité cyclomatique</strong> : &lt; 10 par fonction</li>
                            <li><strong>Maintenability Index</strong> : &gt; 80</li>
                            <li><strong>Couverture de tests</strong> : &gt; 80%</li>
                            <li><strong>Dette technique</strong> : &lt; 5%</li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="text-purple">Documentation</h4>
                        <ul class="textExemple">
                            <li><strong>Commentaires</strong> : 20-30% du code</li>
                            <li><strong>Fonctions documentées</strong> : 100%</li>
                            <li><strong>Classes documentées</strong> : 100%</li>
                            <li><strong>README à jour</strong> : Obligatoire</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Section 8: Checklist d'audit -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Checklist d'audit de documentation</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Points à vérifier lors d'un audit de code :
                    </p>
                    <div class="code-comparison">
                        <div>
                            <h4 class="text-purple">Documentation</h4>
                            <ul class="textExemple">
                                <li>✅ README.md complet et à jour</li>
                                <li>✅ Guide d'installation et setup</li>
                                <li>✅ Documentation d'API à jour</li>
                                <li>✅ Commentaires PHPDoc sur toutes les méthodes publiques</li>
                                <li>✅ Explications des décisions techniques complexes</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-purple">Lisibilité</h4>
                            <ul class="textExemple">
                                <li>✅ Noms de variables explicites</li>
                                <li>✅ Fonctions courtes et spécialisées</li>
                                <li>✅ Absence de code commenté inutile</li>
                                <li>✅ Structure cohérente du projet</li>
                                <li>✅ Respect des conventions de codage</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Section 9: Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        Améliorez la documentation et la lisibilité de ce code :
                    </p>
                    <pre><code><span class="keyword">function</span> <span class="function">p</span>(<span class="variable">$a</span>, <span class="variable">$b</span>, <span class="variable">$c</span>) {
    <span class="variable">$x</span> = <span class="number">0</span>;
    <span class="keyword">for</span> (<span class="variable">$i</span> = <span class="number">0</span>; <span class="variable">$i</span> &lt; <span class="function">count</span>(<span class="variable">$a</span>); <span class="variable">$i</span>++) {
        <span class="keyword">if</span> (<span class="variable">$a</span>[<span class="variable">$i</span>][<span class="string">'s'</span>] &gt; <span class="variable">$b</span> &amp;&amp; <span class="variable">$a</span>[<span class="variable">$i</span>][<span class="string">'t'</span>] == <span class="variable">$c</span>) {
            <span class="variable">$x</span> += <span class="variable">$a</span>[<span class="variable">$i</span>][<span class="string">'p'</span>];
        }
    }
    <span class="keyword">return</span> <span class="variable">$x</span>;
}</code></pre>
                    <details>
                        <summary class="btn-purple btn-hover">Voir la solution améliorée</summary>
                        <div class="solution-content">
                            <h4 class="text-purple">Solution refactorisée :</h4>
                            <pre><code><span class="comment">/**
 * Calcule le prix total des produits filtrés
 * 
 * @param array $products Liste des produits
 * @param float $minStock Stock minimum requis
 * @param string $productType Type de produit à filtrer
 * 
 * @return float Prix total des produits correspondants
 * 
 * @throws InvalidArgumentException Si $products n'est pas un tableau
 */</span>
<span class="keyword">function</span> <span class="function">calculateTotalPriceForProducts</span>(
    <span class="variable">$products</span>, 
    <span class="variable">$minStock</span>, 
    <span class="variable">$productType</span>
) {
    <span class="comment">// Validation des paramètres d'entrée</span>
    <span class="keyword">if</span> (!<span class="function">is_array</span>(<span class="variable">$products</span>)) {
        <span class="keyword">throw new</span> <span class="class-name">InvalidArgumentException</span>(
            <span class="string">'Le paramètre products doit être un tableau'</span>
        );
    }
    
    <span class="variable">$totalPrice</span> = <span class="number">0.0</span>;
    
    <span class="keyword">foreach</span> (<span class="variable">$products</span> <span class="keyword">as</span> <span class="variable">$product</span>) {
        <span class="keyword">if</span> (<span class="variable">$this</span>-&gt;<span class="function">isProductMatchingCriteria</span>(<span class="variable">$product</span>, <span class="variable">$minStock</span>, <span class="variable">$productType</span>)) {
            <span class="variable">$totalPrice</span> += <span class="variable">$product</span>[<span class="string">'price'</span>];
        }
    }
    
    <span class="keyword">return</span> <span class="variable">$totalPrice</span>;
}

<span class="comment">/**
 * Vérifie si un produit correspond aux critères de filtrage
 */</span>
<span class="keyword">private</span> <span class="keyword">function</span> <span class="function">isProductMatchingCriteria</span>(<span class="variable">$product</span>, <span class="variable">$minStock</span>, <span class="variable">$productType</span>) {
    <span class="keyword">return</span> <span class="variable">$product</span>[<span class="string">'stock'</span>] &gt; <span class="variable">$minStock</span> 
        &amp;&amp; <span class="variable">$product</span>[<span class="string">'type'</span>] === <span class="variable">$productType</span>;
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Section 10: Conclusion -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white">Points clés à retenir</h2>
                <div class="text-center">
                    <div class="code-comparison">
                        <div>
                            <h4 class="text-white">📝 Documentation</h4>
                            <ul class="text-white">
                                <li>Documentez le "pourquoi" pas le "comment"</li>
                                <li>Utilisez des standards (PHPDoc)</li>
                                <li>Maintenez la documentation à jour</li>
                                <li>Couverture complète des APIs</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-white">👁️ Lisibilité</h4>
                            <ul class="text-white">
                                <li>Noms explicites et cohérents</li>
                                <li>Fonctions courtes et spécialisées</li>
                                <li>Complexité cyclomatique maîtrisée</li>
                                <li>Respect des conventions</li>
                            </ul>
                        </div>
                    </div>
                    <p class="text-white">
                        Un code bien documenté et lisible n'est pas un luxe, mais une nécessité pour la maintenabilité
                        et l'auditabilité de vos projets.
                    </p>
                </div>
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