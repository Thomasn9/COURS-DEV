<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- Header -->
            <header class="lesson-header">
                <h1 class="text-white">Les Mocks dans les Tests Unitaires</h1>
                <p class="lesson-meta text-white">Comprendre et utiliser les mocks pour tester efficacement votre code
                    JavaScript</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Mocks</h2>
                <p>Les <strong>mocks</strong> (ou "simulacres" en français) sont des objets qui simulent le comportement
                    de composants réels dans un environnement de test. Ils permettent d'isoler le code testé de ses
                    dépendances externes.</p>

                <div class="textExemple">
                    <h3 class="text-purple">Pourquoi utiliser des mocks ?</h3>
                    <ul>
                        <li><strong>Isoler le code testé</strong> : Éviter les effets de bord des dépendances</li>
                        <li><strong>Contrôler l'environnement de test</strong> : Simuler différents scénarios</li>
                        <li><strong>Accélérer les tests</strong> : Éviter les appels réseau ou bases de données</li>
                        <li><strong>Tester des cas d'erreur</strong> : Simuler facilement des erreurs</li>
                    </ul>
                </div>
            </section>

            <!-- Création du projet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : Création et initialisation du projet</h2>

                <div class="textExemple">
                    <p>Commençons par créer un nouveau projet et l'initialiser avec npm :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment"># Créer un nouveau dossier pour votre projet</span>
<span class="variable">mkdir</span> mon-projet-tests
<span class="variable">cd</span> mon-projet-tests

<span class="comment"># Initialiser le projet avec npm</span>
<span class="variable">npm</span> init -y

<span class="comment"># Installer les dépendances de test (Vitest dans cet exemple)</span>
<span class="variable">npm</span> install -D vitest</code></pre>
                </div>

                <div class="textExemple">
                    <p>Modifiez le fichier <code>package.json</code> pour ajouter un script de test :</p>
                </div>

                <div class="code-block">
                    <pre><code>{
  <span class="string">"name"</span>: <span class="string">"mon-projet-tests"</span>,
  <span class="string">"version"</span>: <span class="string">"1.0.0"</span>,
  <span class="string">"scripts"</span>: {
    <span class="string">"test"</span>: <span class="string">"vitest"</span>,
    <span class="string">"test:run"</span>: <span class="string">"vitest run"</span>
  },
  <span class="string">"devDependencies"</span>: {
    <span class="string">"vitest"</span>: <span class="string">"^0.34.0"</span>
  }
}</code></pre>
                </div>
            </section>

            <!-- Création du fichier à tester -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Création du fichier à tester "OrderService.js"</h2>

                <div class="textExemple">
                    <p>Créez un fichier <code>OrderService.js</code> qui contient notre classe à tester :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="keyword">export</span> <span class="keyword">class</span> <span class="class-name">OrderService</span> {
  <span class="function">constructor</span>(<span class="variable">repo</span>) { 
    <span class="keyword">this</span>.<span class="variable">repo</span> = <span class="variable">repo</span>; 
  }
  
  <span class="keyword">async</span> <span class="function">totalPrice</span>(<span class="variable">orderId</span>) {
    <span class="keyword">const</span> <span class="variable">order</span> = <span class="keyword">await</span> <span class="keyword">this</span>.<span class="variable">repo</span>.<span class="function">get</span>(<span class="variable">orderId</span>);
    <span class="keyword">return</span> <span class="variable">order</span>.<span class="variable">items</span>.<span class="function">reduce</span>((<span class="variable">sum</span>, <span class="variable">it</span>) =<span class="operator">&gt;</span> <span class="variable">sum</span> + <span class="variable">it</span>.<span class="variable">price</span> * <span class="variable">it</span>.<span class="variable">qty</span>, <span class="number">0</span>);
  }
}</code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Explication du code :</h3>
                    <ul>
                        <li>La classe <code>OrderService</code> dépend d'un repository (<code>repo</code>) qui fournit
                            l'accès aux données</li>
                        <li>La méthode <code>totalPrice</code> :
                            <ul>
                                <li>Récupère une commande via <code>this.repo.get(orderId)</code></li>
                                <li>Calcule le prix total en additionnant <code>price * qty</code> pour chaque article
                                </li>
                            </ul>
                        </li>
                        <li>Le problème : nous ne voulons pas dépendre d'une vraie base de données pendant les tests
                        </li>
                    </ul>
                </div>
            </section>

            <!-- Création du fichier de test - DÉTAILLÉ -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Création du fichier de test "order.service.test.js"</h2>

                <div class="textExemple">
                    <p>Créez un fichier de test qui utilise un mock pour simuler le repository. Décomposons chaque étape
                        :</p>
                </div>

                <!-- Sous-étape 3.1 -->
                <div class="textExemple">
                    <h3 class="text-purple">3.1 Import des dépendances</h3>
                    <p>On commence par importer les outils de test et la classe à tester :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment">// order.service.test.js</span>
<span class="keyword">import</span> { <span class="variable">describe</span>, <span class="variable">test</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">"vitest"</span>;
<span class="keyword">import</span> { <span class="class-name">OrderService</span> } <span class="keyword">from</span> <span class="string">"./OrderService"</span>;</code></pre>
                </div>

                <!-- Sous-étape 3.2 -->
                <div class="textExemple">
                    <h3 class="text-purple">3.2 Structure du test avec describe et test</h3>
                    <p>On organise notre test avec les fonctions <code>describe</code> et <code>test</code> :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="function">describe</span>(<span class="string">"test de la methode totalPrice de la class OrderService"</span>, () =<span class="operator">&gt;</span> {
  <span class="function">test</span>(<span class="string">"test de la methode totalPrice"</span>, <span class="keyword">async</span> () =<span class="operator">&gt;</span> {
    <span class="comment">// Le code de test va ici</span>
  });
});</code></pre>
                </div>

                <div class="textExemple">
                    <p><strong>Explication :</strong></p>
                    <ul>
                        <li><code>describe</code> : Regroupe plusieurs tests liés, crée un contexte</li>
                        <li><code>test</code> : Définit un test individuel avec une description</li>
                        <li><code>async</code> : Notre test est asynchrone car <code>totalPrice</code> est async</li>
                    </ul>
                </div>

                <!-- Sous-étape 3.3 -->
                <div class="textExemple">
                    <h3 class="text-purple">3.3 Création du Mock du Repository</h3>
                    <p>On crée un objet mock qui simule le comportement du repository réel :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment">// Construction du Mock</span>
<span class="keyword">const</span> <span class="variable">repoMock</span> = {
  <span class="function">get</span>: (<span class="variable">orderId</span>) =<span class="operator">&gt;</span> {
    <span class="comment">// Vérification que la méthode est appelée avec le bon paramètre</span>
    <span class="function">expect</span>(<span class="variable">orderId</span>).<span class="function">toBe</span>(<span class="string">"order-001"</span>);

    <span class="comment">// Simulation de la réponse du repository</span>
    <span class="keyword">return</span> <span class="class-name">Promise</span>.<span class="function">resolve</span>({
      <span class="variable">items</span>: [
        { <span class="variable">price</span>: <span class="number">10</span>, <span class="variable">qty</span>: <span class="number">2</span> },
        { <span class="variable">price</span>: <span class="number">5</span>, <span class="variable">qty</span>: <span class="number">1</span> },
      ],
    });
  },
};</code></pre>
                </div>

                <div class="textExemple">
                    <p><strong>Analyse détaillée du mock :</strong></p>
                    <ul>
                        <li><code>repoMock</code> : Objet qui simule le repository</li>
                        <li><code>get</code> : Méthode mockée qui remplace <code>repo.get()</code></li>
                        <li><code>expect(orderId).toBe("order-001")</code> : Vérifie que l'ID passé est correct</li>
                        <li><code>Promise.resolve()</code> : Simule une réponse asynchrone réussie</li>
                        <li>Les données retournées sont <strong>contrôlées et prévisibles</strong></li>
                    </ul>
                </div>

                <!-- Sous-étape 3.4 -->
                <div class="textExemple">
                    <h3 class="text-purple">3.4 Instanciation du Service avec le Mock</h3>
                    <p>On crée une instance de OrderService en injectant le mock :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment">// On instancie la classe avec le mock</span>
<span class="keyword">const</span> <span class="variable">orderService</span> = <span class="keyword">new</span> <span class="class-name">OrderService</span>(<span class="variable">repoMock</span>);</code></pre>
                </div>

                <div class="textExemple">
                    <p><strong>Point important :</strong> Le service utilise maintenant notre mock au lieu d'un vrai
                        repository.
                        Il ne sait pas que c'est un mock - il utilise l'interface définie par le contrat.</p>
                </div>

                <!-- Sous-étape 3.5 -->
                <div class="textExemple">
                    <h3 class="text-purple">3.5 Appel de la méthode à tester</h3>
                    <p>On appelle la méthode <code>totalPrice</code> avec un ID spécifique :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment">// On appelle totalPrice avec un ID spécifique</span>
<span class="keyword">const</span> <span class="variable">total</span> = <span class="keyword">await</span> <span class="variable">orderService</span>.<span class="function">totalPrice</span>(<span class="string">"order-001"</span>);</code></pre>
                </div>

                <div class="textExemple">
                    <p><strong>Ce qui se passe pendant cet appel :</strong></p>
                    <ol>
                        <li><code>orderService.totalPrice("order-001")</code> est appelé</li>
                        <li>La méthode appelle <code>this.repo.get("order-001")</code></li>
                        <li>Notre mock <code>repoMock.get()</code> est exécuté à la place du vrai repository</li>
                        <li>Le mock vérifie que l'ID est "order-001"</li>
                        <li>Le mock retourne les données de test prédéfinies</li>
                        <li>La méthode calcule le total : (10 × 2) + (5 × 1) = 25</li>
                    </ol>
                </div>

                <!-- Sous-étape 3.6 -->
                <div class="textExemple">
                    <h3 class="text-purple">3.6 Vérification du résultat</h3>
                    <p>On vérifie que le résultat correspond à ce qu'on attend :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment">// Vérification du résultat</span>
<span class="function">expect</span>(<span class="variable">total</span>).<span class="function">toBe</span>(<span class="number">25</span>); <span class="comment">// (10 * 2) + (5 * 1) = 25</span></code></pre>
                </div>

                <!-- Code complet -->
                <div class="textExemple">
                    <h3 class="text-purple">Code complet du test</h3>
                    <p>Voici le fichier de test complet :</p>
                </div>

                <div class="code-block">
                    <pre><code><span class="comment">// order.service.test.js</span>
<span class="keyword">import</span> { <span class="variable">describe</span>, <span class="variable">test</span>, <span class="variable">expect</span> } <span class="keyword">from</span> <span class="string">"vitest"</span>;
<span class="keyword">import</span> { <span class="class-name">OrderService</span> } <span class="keyword">from</span> <span class="string">"./OrderService"</span>;

<span class="function">describe</span>(<span class="string">"test de la methode totalPrice de la class OrderService"</span>, () =<span class="operator">&gt;</span> {
  <span class="function">test</span>(<span class="string">"test de la methode totalPrice"</span>, <span class="keyword">async</span> () =<span class="operator">&gt;</span> {
    <span class="comment">// Construction du Mock</span>
    <span class="keyword">const</span> <span class="variable">repoMock</span> = {
      <span class="function">get</span>: (<span class="variable">orderId</span>) =<span class="operator">&gt;</span> {
        <span class="function">expect</span>(<span class="variable">orderId</span>).<span class="function">toBe</span>(<span class="string">"order-001"</span>);

        <span class="comment">// Le test vérifie que la dépendance est appelée correctement</span>
        <span class="keyword">return</span> <span class="class-name">Promise</span>.<span class="function">resolve</span>({
          <span class="variable">items</span>: [
            { <span class="variable">price</span>: <span class="number">10</span>, <span class="variable">qty</span>: <span class="number">2</span> },
            { <span class="variable">price</span>: <span class="number">5</span>, <span class="variable">qty</span>: <span class="number">1</span> },
          ],
        });
      },
    };

    <span class="comment">// On instancie la classe avec le mock</span>
    <span class="keyword">const</span> <span class="variable">orderService</span> = <span class="keyword">new</span> <span class="class-name">OrderService</span>(<span class="variable">repoMock</span>);
    
    <span class="comment">// On appelle totalPrice avec un ID spécifique</span>
    <span class="keyword">const</span> <span class="variable">total</span> = <span class="keyword">await</span> <span class="variable">orderService</span>.<span class="function">totalPrice</span>(<span class="string">"order-001"</span>);
    
    <span class="comment">// Vérification du résultat</span>
    <span class="function">expect</span>(<span class="variable">total</span>).<span class="function">toBe</span>(<span class="number">25</span>); <span class="comment">// (10 * 2) + (5 * 1) = 25</span>
  });
});</code></pre>
                </div>
            </section>

            <!-- Explication des mocks -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comprendre les Mocks en Détail</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Qu'est-ce qu'un mock exactement ?</h3>
                    <p>Un <strong>mock</strong> est un objet qui simule le comportement d'un composant réel. Il permet
                        de :</p>
                    <ul>
                        <li>Remplacer des dépendances externes (bases de données, APIs, services)</li>
                        <li>Contrôler les données retournées par ces dépendances</li>
                        <li>Vérifier comment votre code interagit avec ces dépendances</li>
                    </ul>
                </div>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Sans Mock</h4>
                        <pre><code><span class="comment">// Problèmes :</span>
<span class="comment">// - Dépend d'une base de données réelle</span>
<span class="comment">// - Données non contrôlables</span>
<span class="comment">// - Tests lents et fragiles</span>
<span class="keyword">const</span> <span class="variable">realRepo</span> = <span class="keyword">new</span> <span class="class-name">DatabaseRepository</span>();
<span class="keyword">const</span> <span class="variable">service</span> = <span class="keyword">new</span> <span class="class-name">OrderService</span>(<span class="variable">realRepo</span>);</code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Avec Mock</h4>
                        <pre><code><span class="comment">// Avantages :</span>
<span class="comment">// - Isolation complète</span>
<span class="comment">// - Données contrôlées</span>
<span class="comment">// - Tests rapides et fiables</span>
<span class="keyword">const</span> <span class="variable">repoMock</span> = {
  <span class="function">get</span>: (<span class="variable">id</span>) =<span class="operator">&gt;</span> <span class="class-name">Promise</span>.<span class="function">resolve</span>(<span class="variable">testData</span>)
};
<span class="keyword">const</span> <span class="variable">service</span> = <span class="keyword">new</span> <span class="class-name">OrderService</span>(<span class="variable">repoMock</span>);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Types de mocks courants :</h3>
                    <ul>
                        <li><strong>Stubs</strong> : Fournissent des réponses prédéfinies</li>
                        <li><strong>Spies</strong> : Enregistrent les appels de fonction</li>
                        <li><strong>Mocks complets</strong> : Combinent stubs et spies avec vérifications</li>
                    </ul>
                </div>
            </section>

            <!-- Avantages et bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages et Bonnes Pratiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Avantages des mocks :</h3>
                    <ul>
                        <li><strong>Tests plus rapides</strong> : Pas d'appels réseau ou de bases de données</li>
                        <li><strong>Tests plus fiables</strong> : Pas de dépendance à des services externes</li>
                        <li><strong>Meilleure couverture</strong> : Possibilité de tester des cas limites difficiles à
                            reproduire</li>
                        <li><strong>Isolation des bugs</strong> : Si un test échoue, le problème vient du code testé,
                            pas des dépendances</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques :</h3>
                    <ul>
                        <li><strong>Mockez seulement ce qui est nécessaire</strong> : Ne pas tout mocker "juste parce
                            que"</li>
                        <li><strong>Gardez les mocks simples</strong> : Un mock complexe peut introduire ses propres
                            bugs</li>
                        <li><strong>Testez les interactions</strong> : Vérifiez que votre code appelle bien les
                            dépendances avec les bons paramètres</li>
                        <li><strong>Documentez vos mocks</strong> : Expliquez pourquoi vous mockez certaines dépendances
                        </li>
                    </ul>
                </div>

            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <p>Les mocks sont des outils essentiels pour écrire des tests unitaires efficaces. Ils permettent
                        d'isoler le code testé et de créer des environnements de test contrôlables et reproductibles.
                    </p>

                    <p>Dans cette leçon, nous avons vu :</p>
                    <ul>
                        <li>Comment créer un projet de test avec Vitest</li>
                        <li>Comment écrire une classe avec des dépendances externes</li>
                        <li>Comment créer des mocks pour simuler ces dépendances</li>
                        <li>Comment écrire des tests qui vérifient à la fois le comportement et les interactions</li>
                    </ul>

                    <p>Les mocks vous aideront à écrire des tests plus rapides, plus fiables et plus complets. Pratiquez
                        régulièrement pour maîtriser cet outil puissant !</p>
                </div>
            </section>
        </div>
    </div>
</template>

<script setup>
// Vous pouvez ajouter ici des données réactives si nécessaire
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

/* Couleurs VS Code pour la syntaxe JavaScript */
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