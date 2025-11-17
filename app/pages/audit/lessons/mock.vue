<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Mocks dans le Testing</h1>
        <p class="lesson-meta text-white">Maîtrisez l'art de simuler des dépendances pour des tests plus efficaces</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Mocks</h2>
        <p class="textExemple">
          Les mocks sont des objets simulés qui imitent le comportement de composants réels dans un environnement contrôlé. 
          Ils sont essentiels pour isoler le code testé de ses dépendances externes.
        </p>
        <p class="textExemple">
          Dans cette leçon, nous explorerons pourquoi et comment utiliser les mocks, les différents types de mocks, 
          et les bonnes pratiques pour les implémenter efficacement.
        </p>
      </section>

      <!-- Pourquoi utiliser les mocks -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Pourquoi utiliser des Mocks ?</h2>
        <div class="textExemple">
          <p>Les mocks sont particulièrement utiles pour :</p>
          <ul>
            <li>Isoler le code testé de ses dépendances externes</li>
            <li>Rendre les tests plus rapides en évitant les appels réseau ou bases de données</li>
            <li>Simuler des scénarios difficiles à reproduire (erreurs réseau, timeout, etc.)</li>
            <li>Vérifier que certaines méthodes sont appelées avec les bons paramètres</li>
            <li>Rendre les tests plus fiables et reproductibles</li>
          </ul>
        </div>
      </section>

      <!-- Types de mocks -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types de Mocks</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">1. Stubs</h3>
          <p>Fournissent des réponses prédéfinies aux appels de méthodes.</p>
          
          <div class="code-example">
            <pre><code class="javascript">// Exemple de stub avec Jest
<span class="keyword">const</span> <span class="variable">apiStub</span> = {
  <span class="variable">getUser</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockReturnValue</span>({
    <span class="variable">id</span>: <span class="number">1</span>,
    <span class="variable">name</span>: <span class="string">'John Doe'</span>,
    <span class="variable">email</span>: <span class="string">'john@example.com'</span>
  })
};</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">2. Spies</h3>
          <p>Enregistrent les informations sur les appels de fonctions sans modifier leur comportement.</p>
          
          <div class="code-example">
            <pre><code class="javascript">// Exemple de spy avec Jest
<span class="keyword">const</span> <span class="variable">userService</span> = {
  <span class="variable">sendEmail</span>: <span class="function">jest</span>.<span class="variable">fn</span>()
};

<span class="comment">// Le spy enregistrera les appels à sendEmail</span>
<span class="variable">userService</span>.<span class="variable">sendEmail</span>.<span class="function">mockImplementation</span>((<span class="variable">email</span>, <span class="variable">message</span>) <span class="operator">=></span> {
  <span class="comment">// Implémentation personnalisée si nécessaire</span>
  <span class="keyword">return</span> <span class="keyword">true</span>;
});</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">3. Mocks complets</h3>
          <p>Simulent entièrement un module ou une dépendance externe.</p>
          
          <div class="code-example">
            <pre><code class="javascript">// Mock d'un module externe avec Jest
<span class="function">jest</span>.<span class="function">mock</span>(<span class="string">'../api/userApi'</span>, () <span class="operator">=></span> ({
  <span class="variable">fetchUser</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>({
    <span class="variable">id</span>: <span class="number">123</span>,
    <span class="variable">name</span>: <span class="string">'Mock User'</span>
  }),
  <span class="variable">updateUser</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>(<span class="keyword">true</span>)
}));</code></pre>
          </div>
        </div>
      </section>

      <!-- Exemple pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exemple Pratique</h2>
        
        <div class="textExemple">
          <p>Imaginons un service qui récupère des utilisateurs et envoie des notifications :</p>
          
          <div class="code-example">
            <pre><code class="javascript"><span class="comment">// Code à tester</span>
<span class="keyword">class</span> <span class="class-name">UserService</span> {
  <span class="function">constructor</span>(<span class="variable">userApi</span>, <span class="variable">notificationService</span>) {
    <span class="keyword">this</span>.<span class="variable">userApi</span> = <span class="variable">userApi</span>;
    <span class="keyword">this</span>.<span class="variable">notificationService</span> = <span class="variable">notificationService</span>;
  }

  <span class="keyword">async</span> <span class="function">sendWelcomeEmail</span>(<span class="variable">userId</span>) {
    <span class="keyword">const</span> <span class="variable">user</span> = <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">userApi</span>.<span class="function">getUser</span>(<span class="variable">userId</span>);
    <span class="keyword">const</span> <span class="variable">message</span> = <span class="string">`Bienvenue <span class="operator">${</span><span class="variable">user</span>.<span class="variable">name</span><span class="operator">}</span> !`</span>;
    <span class="keyword">return</span> <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">notificationService</span>.<span class="function">sendEmail</span>(<span class="variable">user</span>.<span class="variable">email</span>, <span class="variable">message</span>);
  }
}</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <p>Test avec mocks :</p>
          
          <div class="code-example">
            <pre><code class="javascript"><span class="comment">// Test avec Jest</span>
<span class="function">describe</span>(<span class="string">'UserService'</span>, () <span class="operator">=></span> {
  <span class="function">it</span>(<span class="string">'should send welcome email to user'</span>, <span class="keyword">async</span> () <span class="operator">=></span> {
    <span class="comment">// Arrange - Configuration des mocks</span>
    <span class="keyword">const</span> <span class="variable">mockUserApi</span> = {
      <span class="variable">getUser</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>({
        <span class="variable">id</span>: <span class="number">1</span>,
        <span class="variable">name</span>: <span class="string">'Alice'</span>,
        <span class="variable">email</span>: <span class="string">'alice@example.com'</span>
      })
    };

    <span class="keyword">const</span> <span class="variable">mockNotificationService</span> = {
      <span class="variable">sendEmail</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>(<span class="keyword">true</span>)
    };

    <span class="keyword">const</span> <span class="variable">userService</span> = <span class="keyword">new</span> <span class="class-name">UserService</span>(<span class="variable">mockUserApi</span>, <span class="variable">mockNotificationService</span>);

    <span class="comment">// Act - Exécution de la méthode testée</span>
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="keyword">await</span> <span class="variable">userService</span>.<span class="function">sendWelcomeEmail</span>(<span class="number">1</span>);

    <span class="comment">// Assert - Vérifications</span>
    <span class="function">expect</span>(<span class="variable">mockUserApi</span>.<span class="variable">getUser</span>).<span class="function">toHaveBeenCalledWith</span>(<span class="number">1</span>);
    <span class="function">expect</span>(<span class="variable">mockNotificationService</span>.<span class="variable">sendEmail</span>).<span class="function">toHaveBeenCalledWith</span>(
      <span class="string">'alice@example.com'</span>,
      <span class="string">'Bienvenue Alice !'</span>
    );
    <span class="function">expect</span>(<span class="variable">result</span>).<span class="function">toBe</span>(<span class="keyword">true</span>);
  });
});</code></pre>
          </div>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Bonnes Pratiques</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">À faire :</h3>
          <ul>
            <li>Mockez seulement ce qui est nécessaire pour le test</li>
            <li>Utilisez des mocks réalistes qui reflètent le comportement réel</li>
            <li>Vérifiez les interactions avec les mocks (appels, paramètres)</li>
            <li>Documentez pourquoi vous utilisez un mock particulier</li>
            <li>Nettoyez les mocks entre les tests pour éviter les interférences</li>
          </ul>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">À éviter :</h3>
          <ul>
            <li>Ne mockez pas excessivement - testez le code réel quand c'est possible</li>
            <li>Évitez les mocks trop complexes qui deviennent difficiles à maintenir</li>
            <li>Ne testez pas l'implémentation des mocks, testez le comportement</li>
            <li>N'utilisez pas de mocks pour cacher des problèmes de conception</li>
          </ul>
        </div>
      </section>

      <!-- Exercice -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice Pratique</h2>
        
        <div class="exercise">
          <p>Créez un test pour la fonction suivante en utilisant des mocks appropriés :</p>
          
          <div class="code-example">
            <pre><code class="javascript"><span class="keyword">async</span> <span class="function">processOrder</span>(<span class="variable">orderId</span>) {
  <span class="keyword">const</span> <span class="variable">order</span> = <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">orderRepository</span>.<span class="function">findById</span>(<span class="variable">orderId</span>);
  
  <span class="keyword">if</span> (!<span class="variable">order</span>) {
    <span class="keyword">throw new</span> <span class="class-name">Error</span>(<span class="string">'Order not found'</span>);
  }

  <span class="keyword">if</span> (<span class="variable">order</span>.<span class="variable">status</span> === <span class="string">'processed'</span>) {
    <span class="keyword">return</span> <span class="variable">order</span>;
  }

  <span class="keyword">const</span> <span class="variable">paymentResult</span> = <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">paymentService</span>.<span class="function">processPayment</span>(<span class="variable">order</span>.<span class="variable">total</span>);
  
  <span class="keyword">if</span> (<span class="variable">paymentResult</span>.<span class="variable">success</span>) {
    <span class="variable">order</span>.<span class="variable">status</span> = <span class="string">'processed'</span>;
    <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">orderRepository</span>.<span class="function">update</span>(<span class="variable">order</span>);
    <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">notificationService</span>.<span class="function">sendConfirmation</span>(<span class="variable">order</span>.<span class="variable">customerEmail</span>);
  }

  <span class="keyword">return</span> <span class="variable">order</span>;
}</code></pre>
          </div>

          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4>Solution proposée :</h4>
              <pre><code class="javascript"><span class="function">describe</span>(<span class="string">'processOrder'</span>, () <span class="operator">=></span> {
  <span class="function">it</span>(<span class="string">'should process order successfully when payment is approved'</span>, <span class="keyword">async</span> () <span class="operator">=></span> {
    <span class="comment">// Arrange</span>
    <span class="keyword">const</span> <span class="variable">mockOrder</span> = {
      <span class="variable">id</span>: <span class="number">123</span>,
      <span class="variable">status</span>: <span class="string">'pending'</span>,
      <span class="variable">total</span>: <span class="number">100</span>,
      <span class="variable">customerEmail</span>: <span class="string">'test@example.com'</span>
    };

    <span class="keyword">const</span> <span class="variable">mockOrderRepository</span> = {
      <span class="variable">findById</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>(<span class="variable">mockOrder</span>),
      <span class="variable">update</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>({ ...<span class="variable">mockOrder</span>, <span class="variable">status</span>: <span class="string">'processed'</span> })
    };

    <span class="keyword">const</span> <span class="variable">mockPaymentService</span> = {
      <span class="variable">processPayment</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>({ <span class="variable">success</span>: <span class="keyword">true</span> })
    };

    <span class="keyword">const</span> <span class="variable">mockNotificationService</span> = {
      <span class="variable">sendConfirmation</span>: <span class="function">jest</span>.<span class="variable">fn</span>().<span class="function">mockResolvedValue</span>(<span class="keyword">true</span>)
    };

    <span class="keyword">const</span> <span class="variable">orderProcessor</span> = <span class="keyword">new</span> <span class="class-name">OrderProcessor</span>(
      <span class="variable">mockOrderRepository</span>,
      <span class="variable">mockPaymentService</span>,
      <span class="variable">mockNotificationService</span>
    );

    <span class="comment">// Act</span>
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="keyword">await</span> <span class="variable">orderProcessor</span>.<span class="function">processOrder</span>(<span class="number">123</span>);

    <span class="comment">// Assert</span>
    <span class="function">expect</span>(<span class="variable">mockOrderRepository</span>.<span class="variable">findById</span>).<span class="function">toHaveBeenCalledWith</span>(<span class="number">123</span>);
    <span class="function">expect</span>(<span class="variable">mockPaymentService</span>.<span class="variable">processPayment</span>).<span class="function">toHaveBeenCalledWith</span>(<span class="number">100</span>);
    <span class="function">expect</span>(<span class="variable">mockOrderRepository</span>.<span class="variable">update</span>).<span class="function">toHaveBeenCalled</span>();
    <span class="function">expect</span>(<span class="variable">mockNotificationService</span>.<span class="variable">sendConfirmation</span>).<span class="function">toHaveBeenCalledWith</span>(<span class="string">'test@example.com'</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">status</span>).<span class="function">toBe</span>(<span class="string">'processed'</span>);
  });
});</code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <div class="textExemple">
          <p>
            Les mocks sont des outils puissants dans l'arsenal du développeur de tests. 
            Ils permettent d'isoler le code testé, de simuler des scénarios complexes, 
            et de rendre les tests plus rapides et fiables.
          </p>
          <p>
            Cependant, il est important de les utiliser judicieusement et de ne pas 
            tomber dans le piège du sur-mocking, qui peut masquer des problèmes de conception 
            et rendre les tests moins significatifs.
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

/* Couleurs VS Code pour la syntaxe JavaScript */
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