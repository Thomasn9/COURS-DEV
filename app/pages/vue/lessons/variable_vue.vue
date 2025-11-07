<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les Variables en Vue.js</h1>
                <p class="lesson-meta text-white">Déclaration, utilisation et réactivité des données</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Variables Réactives</h2>
                <p class="textExemple">
                    En Vue.js, les variables ne sont pas de simples conteneurs de données. Grâce au système de
                    réactivité,
                    lorsque vous modifiez une variable, l'interface utilisateur se met automatiquement à jour.
                    Cette leçon couvre les différentes façons de déclarer et d'utiliser des variables dans Vue 3.
                </p>
            </section>

            <!-- Déclaration avec ref() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Déclaration avec <code>ref()</code></h2>
                <p class="textExemple">
                    <code>ref()</code> est utilisé pour créer des variables réactives avec des valeurs
                    primitives
                    (string, number, boolean) ou des objets. Pour accéder à la valeur, on utilise la propriété
                    <code>.value</code>.
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-javascript">&lt;!-- Template --&gt;
&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;Nom: {{ nom }}&lt;/p&gt;
    &lt;p&gt;Âge: {{ age }}&lt;/p&gt;
    &lt;button @click="incrementerAge"&gt;+1 an&lt;/button&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;!-- Script --&gt;
&lt;script setup&gt;
<span class="keyword">import</span> { <span class="variable">ref</span> } <span class="keyword">from</span> <span class="string">'vue'</span>

<span class="comment">// Déclaration de variables réactives</span>
<span class="keyword">const</span> <span class="variable">nom</span> = <span class="function">ref</span>(<span class="string">'Jean Dupont'</span>)
<span class="keyword">const</span> <span class="variable">age</span> = <span class="function">ref</span>(<span class="number">25</span>)
<span class="keyword">const</span> <span class="variable">estActif</span> = <span class="function">ref</span>(<span class="keyword">true</span>)

<span class="comment">// Fonction pour modifier une variable réactive</span>
<span class="keyword">const</span> <span class="function">incrementerAge</span> = () <span class="operator">=></span> {
  <span class="variable">age</span>.<span class="property">value</span><span class="operator">++</span>  <span class="comment">// Note: on utilise .value dans le script</span>
}
&lt;/script&gt;</code></pre>
                </div>

                <div class="code-comparison">
                    <div class="code-example" v-pre>
                        <h4 class="text-purple">✅ Dans le Template</h4>
                        <pre><code class="language-javascript"><span class="comment">// Pas besoin de .value</span>
{{ <span class="variable">nom</span> }}
{{ <span class="variable">age</span> }}</code></pre>
                    </div>

                    <div class="code-example" v-pre>
                        <h4 class="text-purple">✅ Dans le Script</h4>
                        <pre><code class="language-javascript"><span class="comment">// Toujours utiliser .value</span>
<span class="variable">nom</span>.<span class="property">value</span> <span class="operator">=</span> <span class="string">'Nouveau nom'</span>
<span class="variable">age</span>.<span class="property">value</span><span class="operator">++</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Déclaration avec reactive() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Déclaration avec <code>reactive()</code></h2>
                <p class="textExemple">
                    <code>reactive()</code> est optimisé pour les objets et les tableaux. Contrairement
                    à <code>ref()</code>,
                    on accède directement aux propriétés sans utiliser <code>.value</code>.
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-javascript">&lt;script setup&gt;
<span class="keyword">import</span> { <span class="variable">reactive</span> } <span class="keyword">from</span> <span class="string">'vue'</span>

<span class="comment">// Objet réactif</span>
<span class="keyword">const</span> <span class="variable">utilisateur</span> = <span class="function">reactive</span>({
  <span class="property">nom</span>: <span class="string">'Marie'</span>,
  <span class="property">age</span>: <span class="number">30</span>,
  <span class="property">email</span>: <span class="string">'marie@example.com'</span>
})

<span class="comment">// Tableau réactif</span>
<span class="keyword">const</span> <span class="variable">listeCourses</span> = <span class="function">reactive</span>([<span class="string">'Lait'</span>, <span class="string">'Œufs'</span>, <span class="string">'Pain'</span>])

<span class="comment">// Modification directe sans .value</span>
<span class="variable">utilisateur</span>.<span class="property">age</span> <span class="operator">=</span> <span class="number">31</span>
<span class="variable">listeCourses</span>.<span class="function">push</span>(<span class="string">'Fruits'</span>)
&lt;/script&gt;

&lt;!-- Dans le template --&gt;
&lt;p&gt;Utilisateur: {{ <span class="variable">utilisateur</span>.<span class="property">nom</span> }}&lt;/p&gt;
&lt;p&gt;Courses: {{ <span class="variable">listeCourses</span>.<span class="function">join</span>(<span class="string">', '</span>) }}&lt;/p&gt;</code></pre>
                </div>
            </section>

            <!-- Comparaison ref() vs reactive() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Quand utiliser <code>ref()</code> vs <code>reactive()</code> ?</h2>

                <div class="code-comparison">
                    <div class="code-example" v-pre>
                        <h4 class="text-purple">📌 Utiliser <code>ref()</code> pour :</h4>
                        <ul class="textExemple">
                            <li>Variables primitives (string, number, boolean)</li>
                            <li>Quand vous avez besoin de réaffecter toute la variable</li>
                            <li>Variables simples avec peu de propriétés</li>
                        </ul>
                        <pre><code class="language-javascript"><span class="keyword">const</span> <span class="variable">count</span> = <span class="function">ref</span>(<span class="number">0</span>)
<span class="keyword">const</span> <span class="variable">message</span> = <span class="function">ref</span>(<span class="string">'Hello'</span>)
<span class="keyword">const</span> <span class="variable">isLoading</span> = <span class="function">ref</span>(<span class="keyword">false</span>)</code></pre>
                    </div>

                    <div class="code-example" v-pre>
                        <h4 class="text-purple">📦 Utiliser <code>reactive()</code> pour :</h4>
                        <ul class="textExemple">
                            <li>Objets avec plusieurs propriétés</li>
                            <li>Tableaux et structures de données complexes</li>
                            <li>Quand les propriétés sont liées logiquement</li>
                        </ul>
                        <pre><code class="language-javascript"><span class="keyword">const</span> <span class="variable">user</span> = <span class="function">reactive</span>({
  <span class="property">name</span>: <span class="string">'John'</span>,
  <span class="property">age</span>: <span class="number">25</span>,
  <span class="property">address</span>: {
    <span class="property">street</span>: <span class="string">'123 Main St'</span>,
    <span class="property">city</span>: <span class="string">'Paris'</span>
  }
})</code></pre>
                    </div>
                </div>
            </section>

            <!-- Variables Computed -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Variables Computed (Calculées)</h2>
                <p class="textExemple">
                    Les propriétés computed sont des variables qui sont automatiquement recalculées
                    lorsque leurs dépendances changent. Elles sont en lecture seule par défaut.
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-javascript">&lt;script setup&gt;
<span class="keyword">import</span> { <span class="variable">ref</span>, <span class="variable">computed</span> } <span class="keyword">from</span> <span class="string">'vue'</span>

<span class="keyword">const</span> <span class="variable">prenom</span> = <span class="function">ref</span>(<span class="string">'Jean'</span>)
<span class="keyword">const</span> <span class="variable">nom</span> = <span class="function">ref</span>(<span class="string">'Dupont'</span>)
<span class="keyword">const</span> <span class="variable">prix</span> = <span class="function">ref</span>(<span class="number">100</span>)
<span class="keyword">const</span> <span class="variable">quantite</span> = <span class="function">ref</span>(<span class="number">2</span>)

<span class="comment">// Computed property</span>
<span class="keyword">const</span> <span class="variable">nomComplet</span> = <span class="function">computed</span>(() <span class="operator">=></span> {
  <span class="keyword">return</span> <span class="string">`</span><span class="variable">${prenom.value}</span> <span class="variable">${nom.value}</span><span class="string">`</span>
})

<span class="keyword">const</span> <span class="variable">total</span> = <span class="function">computed</span>(() <span class="operator">=></span> {
  <span class="keyword">return</span> <span class="variable">prix</span>.<span class="property">value</span> <span class="operator">*</span> <span class="variable">quantite</span>.<span class="property">value</span>
})

<span class="keyword">const</span> <span class="variable">messageBienvenue</span> = <span class="function">computed</span>(() <span class="operator">=></span> {
  <span class="keyword">return</span> <span class="string">`Bonjour </span><span class="variable">${nomComplet.value}</span><span class="string">, votre total est de </span><span class="variable">${total.value}</span><span class="string">€`</span>
})
&lt;/script&gt;

&lt;!-- Utilisation dans le template --&gt;
&lt;p&gt;{{ <span class="variable">nomComplet</span> }}&lt;/p&gt;
&lt;p&gt;Total: {{ <span class="variable">total</span> }}€&lt;/p&gt;
&lt;p&gt;{{ <span class="variable">messageBienvenue</span> }}&lt;/p&gt;</code></pre>
                </div>
            </section>

            <!-- Variables avec watch -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Surveillance avec <code>watch()</code></h2>
                <p class="textExemple">
                    <code class="variable">watch()</code> permet d'exécuter du code lorsqu'une variable réactive change.
                    C'est utile pour les effets de bord, les appels API, ou la persistance des données.
                </p>

                <div class="code-example" v-pre>
                    <pre><code class="language-javascript">&lt;script setup&gt;
<span class="keyword">import</span> { <span class="variable">ref</span>, <span class="variable">watch</span> } <span class="keyword">from</span> <span class="string">'vue'</span>

<span class="keyword">const</span> <span class="variable">recherche</span> = <span class="function">ref</span>(<span class="string">''</span>)
<span class="keyword">const</span> <span class="variable">resultats</span> = <span class="function">ref</span>([])
<span class="keyword">const</span> <span class="variable">chargement</span> = <span class="function">ref</span>(<span class="keyword">false</span>)

<span class="comment">// Surveiller les changements de 'recherche'</span>
<span class="function">watch</span>(<span class="variable">recherche</span>, <span class="keyword">async</span> (<span class="variable">nouvelleValeur</span>, <span class="variable">ancienneValeur</span>) <span class="operator">=></span> {
  <span class="keyword">if</span> (<span class="variable">nouvelleValeur</span>.<span class="property">length</span> <span class="operator"><</span> <span class="number">3</span>) {
    <span class="variable">resultats</span>.<span class="property">value</span> <span class="operator">=</span> []
    <span class="keyword">return</span>
  }
  
  <span class="variable">chargement</span>.<span class="property">value</span> <span class="operator">=</span> <span class="keyword">true</span>
  
  <span class="comment">// Simuler un appel API</span>
  <span class="keyword">try</span> {
    <span class="keyword">const</span> <span class="variable">response</span> <span class="operator">=</span> <span class="keyword">await</span> <span class="function">fetch</span>(<span class="string">`/api/search?q=</span><span class="variable">${nouvelleValeur}</span><span class="string">`</span>)
    <span class="variable">resultats</span>.<span class="property">value</span> <span class="operator">=</span> <span class="keyword">await</span> <span class="variable">response</span>.<span class="function">json</span>()
  } <span class="keyword">catch</span> (<span class="variable">error</span>) {
    <span class="function">console</span>.<span class="function">error</span>(<span class="string">'Erreur de recherche:'</span>, <span class="variable">error</span>)
  } <span class="keyword">finally</span> {
    <span class="variable">chargement</span>.<span class="property">value</span> <span class="operator">=</span> <span class="keyword">false</span>
  }
})

<span class="comment">// Surveillance immédiate (exécuté au chargement)</span>
<span class="function">watch</span>(<span class="variable">recherche</span>, (<span class="variable">nouvelleValeur</span>) <span class="operator">=></span> {
  <span class="function">console</span>.<span class="function">log</span>(<span class="string">'Recherche changée:'</span>, <span class="variable">nouvelleValeur</span>)
}, { <span class="property">immediate</span>: <span class="keyword">true</span> })
&lt;/script&gt;</code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques</h2>

                <div class="code-comparison">
                    <div class="code-example" v-pre>
                        <h4 class="text-purple">✅ À Faire</h4>
                        <ul class="textExemple">
                            <li>Utiliser des noms explicites pour les variables</li>
                            <li>Déstructurer les objets réactifs avec précaution</li>
                            <li>Utiliser <code>computed()</code> pour les valeurs dérivées</li>
                            <li>Typer vos variables avec TypeScript</li>
                        </ul>
                        <pre><code class="language-javascript"><span class="comment">// Bon</span>
<span class="keyword">const</span> <span class="variable">utilisateurActif</span> = <span class="function">ref</span>(<span class="keyword">true</span>)
<span class="keyword">const</span> <span class="variable">nombreArticles</span> = <span class="function">ref</span>(<span class="number">0</span>)

<span class="comment">// Déstructuration sécurisée</span>
<span class="keyword">const</span> { <span class="variable">nom</span>, <span class="variable">age</span> } = <span class="function">toRefs</span>(<span class="variable">utilisateur</span>)</code></pre>
                    </div>

                    <div class="code-example" v-pre>
                        <h4 class="text-purple">❌ À Éviter</h4>
                        <ul class="textExemple">
                            <li>Modifier directement les computed properties</li>
                            <li>Oublier <code>.value</code> dans le script</li>
                            <li>Utiliser <code>reactive()</code> avec des primitives</li>
                            <li>Muter des tableaux de façon non-réactive</li>
                        </ul>
                        <pre><code class="language-javascript"><span class="comment">// Mauvais</span>
<span class="variable">nomComplet</span>.<span class="property">value</span> <span class="operator">=</span> <span class="string">'Nouveau nom'</span> <span class="comment">// Erreur!</span>

<span class="comment">// Mauvais - perd la réactivité</span>
<span class="keyword">const</span> { <span class="variable">nom</span>, <span class="variable">age</span> } = <span class="variable">utilisateur</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer un compteur intelligent avec historique
                    </p>

                    <ol class="textExemple">
                        <li>Créez un compteur avec <code>ref()</code> qui commence à 0</li>
                        <li>Ajoutez des boutons pour incrémenter et décrémenter</li>
                        <li>Créez une computed property pour afficher si le nombre est pair ou impair</li>
                        <li>Utilisez <code>reactive()</code> pour stocker l'historique des changements
                        </li>
                        <li>Surveillez le compteur pour limiter sa valeur entre -10 et 10</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Solution Complète</h4>
                        <div class="code-example" v-pre>
                            <pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="compteur"&gt;
    &lt;h2&gt;Compteur: {{ compteur }}&lt;/h2&gt;
    &lt;p&gt;Le nombre est {{ parite }}&lt;/p&gt;
    
    &lt;div class="boutons"&gt;
      &lt;button @click="decrementer" :disabled="compteur &lt;= -10"&gt;-&lt;/button&gt;
      &lt;button @click="incrementer" :disabled="compteur &gt;= 10"&gt;+&lt;/button&gt;
      &lt;button @click="reinitialiser"&gt;Reset&lt;/button&gt;
    &lt;/div&gt;
    
    &lt;h3&gt;Historique ({{ historique.actions.length }} actions)&lt;/h3&gt;
    &lt;ul&gt;
      &lt;li v-for="(action, index) in historique.actions" :key="index"&gt;
        {{ action.type }} - {{ action.timestamp }}
      &lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
<span class="keyword">import</span> { <span class="variable">ref</span>, <span class="variable">reactive</span>, <span class="variable">computed</span>, <span class="variable">watch</span> } <span class="keyword">from</span> <span class="string">'vue'</span>

<span class="comment">// Variables avec ref()</span>
<span class="keyword">const</span> <span class="variable">compteur</span> = <span class="function">ref</span>(<span class="number">0</span>)

<span class="comment">// Computed property</span>
<span class="keyword">const</span> <span class="variable">parite</span> = <span class="function">computed</span>(() <span class="operator">=></span> {
  <span class="keyword">return</span> <span class="variable">compteur</span>.<span class="property">value</span> <span class="operator">%</span> <span class="number">2</span> <span class="operator">===</span> <span class="number">0</span> <span class="operator">?</span> <span class="string">'pair'</span> : <span class="string">'impair'</span>
})

<span class="comment">// Objet réactif avec reactive()</span>
<span class="keyword">const</span> <span class="variable">historique</span> = <span class="function">reactive</span>({
  <span class="property">actions</span>: []
})

<span class="comment">// Fonctions</span>
<span class="keyword">const</span> <span class="function">incrementer</span> = () <span class="operator">=></span> {
  <span class="variable">compteur</span>.<span class="property">value</span><span class="operator">++</span>
  <span class="function">ajouterHistorique</span>(<span class="string">'incrément'</span>)
}

<span class="keyword">const</span> <span class="function">decrementer</span> = () <span class="operator">=></span> {
  <span class="variable">compteur</span>.<span class="property">value</span><span class="operator">--</span>
  <span class="function">ajouterHistorique</span>(<span class="string">'décrément'</span>)
}

<span class="keyword">const</span> <span class="function">reinitialiser</span> = () <span class="operator">=></span> {
  <span class="variable">compteur</span>.<span class="property">value</span> <span class="operator">=</span> <span class="number">0</span>
  <span class="function">ajouterHistorique</span>(<span class="string">'reset'</span>)
}

<span class="keyword">const</span> <span class="function">ajouterHistorique</span> = (<span class="variable">type</span>) <span class="operator">=></span> {
  <span class="variable">historique</span>.<span class="property">actions</span>.<span class="function">push</span>({
    <span class="property">type</span>,
    <span class="property">timestamp</span>: <span class="keyword">new</span> <span class="class-name">Date</span>().<span class="function">toLocaleTimeString</span>()
  })
}

<span class="comment">// Surveillance avec watch()</span>
<span class="function">watch</span>(<span class="variable">compteur</span>, (<span class="variable">nouvelleValeur</span>) <span class="operator">=></span> {
  <span class="keyword">if</span> (<span class="variable">nouvelleValeur</span> <span class="operator">></span> <span class="number">10</span>) {
    <span class="variable">compteur</span>.<span class="property">value</span> <span class="operator">=</span> <span class="number">10</span>
  } <span class="keyword">else</span> <span class="keyword">if</span> (<span class="variable">nouvelleValeur</span> <span class="operator"><</span> <span class="operator">-</span><span class="number">10</span>) {
    <span class="variable">compteur</span>.<span class="property">value</span> <span class="operator">=</span> <span class="operator">-</span><span class="number">10</span>
  }
})
&lt;/script&gt;</code></pre>
                        </div>
                    </div>
                </details>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Les variables réactives sont au cœur de Vue.js. Maîtriser <code>ref()</code>,
                    <code>reactive()</code>,
                    <code>computed()</code> et <code>watch()</code> est essentiel pour
                    créer des applications interactives et performantes.
                </p>
                <p class="textExemple">
                    Pour approfondir, consultez la
                    <a href="https://vuejs.org/guide/essentials/reactivity-fundamentals.html"
                        class="btn btn-purple btn-hover mt-auto text-white text-decoration-none" target="_blank">
                        documentation officielle sur la réactivité
                    </a>
                </p>
            </section>
        </div>
    </div>
</template>

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