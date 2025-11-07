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
                <h2 class="text-purple">Déclaration avec <code class="variable">ref()</code></h2>
                <p class="textExemple">
                    <code class="variable">ref()</code> est utilisé pour créer des variables réactives avec des valeurs
                    primitives
                    (string, number, boolean) ou des objets. Pour accéder à la valeur, on utilise la propriété <code
                        class="variable">.value</code>.
                </p>

                <div class="code-example" v-pre>
                    <pre>&lt;!-- Template --&gt;
&lt;template&gt;
  &lt;div&gt;
    &lt;p&gt;Nom: {{ nom }}&lt;/p&gt;
    &lt;p&gt;Âge: {{ age }}&lt;/p&gt;
    &lt;button @click="incrementerAge"&gt;+1 an&lt;/button&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;!-- Script --&gt;
&lt;script setup&gt;
import { ref } from 'vue'

// Déclaration de variables réactives
const nom = ref('Jean Dupont')
const age = ref(25)
const estActif = ref(true)

// Fonction pour modifier une variable réactive
const incrementerAge = () =&gt; {
  age.value++  // Note: on utilise .value dans le script
}
&lt;/script&gt;</pre>
                </div>

                <div class="code-comparison">
                    <div class="code-example" v-pre>
                        <h4 class="text-purple">✅ Dans le Template</h4>
                        <pre>// Pas besoin de .value
{{ nom }}
{{ age }}</pre>
                    </div>

                    <div class="code-example" v-pre>
                        <h4 class="text-purple">✅ Dans le Script</h4>
                        <pre>// Toujours utiliser .value
nom.value = 'Nouveau nom'
age.value++</pre>
                    </div>
                </div>
            </section>

            <!-- Déclaration avec reactive() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Déclaration avec <code class="variable">reactive()</code></h2>
                <p class="textExemple">
                    <code class="variable">reactive()</code> est optimisé pour les objets et les tableaux. Contrairement
                    à <code class="variable">ref()</code>,
                    on accède directement aux propriétés sans utiliser <code class="variable">.value</code>.
                </p>

                <div class="code-example" v-pre>
                    <pre>&lt;script setup&gt;
import { reactive } from 'vue'

// Objet réactif
const utilisateur = reactive({
  nom: 'Marie',
  age: 30,
  email: 'marie@example.com'
})

// Tableau réactif
const listeCourses = reactive(['Lait', 'Œufs', 'Pain'])

// Modification directe sans .value
utilisateur.age = 31
listeCourses.push('Fruits')
&lt;/script&gt;

&lt;!-- Dans le template --&gt;
&lt;p&gt;Utilisateur: {{ utilisateur.nom }}&lt;/p&gt;
&lt;p&gt;Courses: {{ listeCourses.join(', ') }}&lt;/p&gt;</pre>
                </div>
            </section>

            <!-- Comparaison ref() vs reactive() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Quand utiliser <code class="variable">ref()</code> vs <code
                        class="variable">reactive()</code> ?</h2>

                <div class="code-comparison">
                    <div class="code-example" v-pre>
                        <h4 class="text-purple">📌 Utiliser <code class="variable">ref()</code> pour :</h4>
                        <ul class="textExemple">
                            <li>Variables primitives (string, number, boolean)</li>
                            <li>Quand vous avez besoin de réaffecter toute la variable</li>
                            <li>Variables simples avec peu de propriétés</li>
                        </ul>
                        <pre>const count = ref(0)
const message = ref('Hello')
const isLoading = ref(false)</pre>
                    </div>

                    <div class="code-example" v-pre>
                        <h4 class="text-purple">📦 Utiliser <code class="variable">reactive()</code> pour :</h4>
                        <ul class="textExemple">
                            <li>Objets avec plusieurs propriétés</li>
                            <li>Tableaux et structures de données complexes</li>
                            <li>Quand les propriétés sont liées logiquement</li>
                        </ul>
                        <pre>const user = reactive({
  name: 'John',
  age: 25,
  address: {
    street: '123 Main St',
    city: 'Paris'
  }
})</pre>
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
                    <pre>&lt;script setup&gt;
import { ref, computed } from 'vue'

const prenom = ref('Jean')
const nom = ref('Dupont')
const prix = ref(100)
const quantite = ref(2)

// Computed property
const nomComplet = computed(() =&gt; {
  return `${prenom.value} ${nom.value}`
})

const total = computed(() =&gt; {
  return prix.value * quantite.value
})

const messageBienvenue = computed(() =&gt; {
  return `Bonjour ${nomComplet.value}, votre total est de ${total.value}€`
})
&lt;/script&gt;

&lt;!-- Utilisation dans le template --&gt;
&lt;p&gt;{{ nomComplet }}&lt;/p&gt;
&lt;p&gt;Total: {{ total }}€&lt;/p&gt;
&lt;p&gt;{{ messageBienvenue }}&lt;/p&gt;</pre>
                </div>
            </section>

            <!-- Variables avec watch -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Surveillance avec <code class="variable">watch()</code></h2>
                <p class="textExemple">
                    <code class="variable">watch()</code> permet d'exécuter du code lorsqu'une variable réactive change.
                    C'est utile pour les effets de bord, les appels API, ou la persistance des données.
                </p>

                <div class="code-example" v-pre>
                    <pre>&lt;script setup&gt;
import { ref, watch } from 'vue'

const recherche = ref('')
const resultats = ref([])
const chargement = ref(false)

// Surveiller les changements de 'recherche'
watch(recherche, async (nouvelleValeur, ancienneValeur) =&gt; {
  if (nouvelleValeur.length &lt; 3) {
    resultats.value = []
    return
  }
  
  chargement.value = true
  
  // Simuler un appel API
  try {
    const response = await fetch(`/api/search?q=${nouvelleValeur}`)
    resultats.value = await response.json()
  } catch (error) {
    console.error('Erreur de recherche:', error)
  } finally {
    chargement.value = false
  }
})

// Surveillance immédiate (exécuté au chargement)
watch(recherche, (nouvelleValeur) =&gt; {
  console.log('Recherche changée:', nouvelleValeur)
}, { immediate: true })
&lt;/script&gt;</pre>
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
                            <li>Utiliser <code class="variable">computed()</code> pour les valeurs dérivées</li>
                            <li>Typer vos variables avec TypeScript</li>
                        </ul>
                        <pre>// Bon
const utilisateurActif = ref(true)
const nombreArticles = ref(0)

// Déstructuration sécurisée
const { nom, age } = toRefs(utilisateur)</pre>
                    </div>

                    <div class="code-example" v-pre>
                        <h4 class="text-purple">❌ À Éviter</h4>
                        <ul class="textExemple">
                            <li>Modifier directement les computed properties</li>
                            <li>Oublier <code class="variable">.value</code> dans le script</li>
                            <li>Utiliser <code class="variable">reactive()</code> avec des primitives</li>
                            <li>Muter des tableaux de façon non-réactive</li>
                        </ul>
                        <pre>// Mauvais
nomComplet.value = 'Nouveau nom' // Erreur!

// Mauvais - perd la réactivité
const { nom, age } = utilisateur</pre>
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
                        <li>Créez un compteur avec <code class="variable">ref()</code> qui commence à 0</li>
                        <li>Ajoutez des boutons pour incrémenter et décrémenter</li>
                        <li>Créez une computed property pour afficher si le nombre est pair ou impair</li>
                        <li>Utilisez <code class="variable">reactive()</code> pour stocker l'historique des changements
                        </li>
                        <li>Surveillez le compteur pour limiter sa valeur entre -10 et 10</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Solution Complète</h4>
                        <div class="code-example" v-pre>
                            <pre>&lt;template&gt;
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
import { ref, reactive, computed, watch } from 'vue'

// Variables avec ref()
const compteur = ref(0)

// Computed property
const parite = computed(() =&gt; {
  return compteur.value % 2 === 0 ? 'pair' : 'impair'
})

// Objet réactif avec reactive()
const historique = reactive({
  actions: []
})

// Fonctions
const incrementer = () =&gt; {
  compteur.value++
  ajouterHistorique('incrément')
}

const decrementer = () =&gt; {
  compteur.value--
  ajouterHistorique('décrément')
}

const reinitialiser = () =&gt; {
  compteur.value = 0
  ajouterHistorique('reset')
}

const ajouterHistorique = (type) =&gt; {
  historique.actions.push({
    type,
    timestamp: new Date().toLocaleTimeString()
  })
}

// Surveillance avec watch()
watch(compteur, (nouvelleValeur) =&gt; {
  if (nouvelleValeur &gt; 10) {
    compteur.value = 10
  } else if (nouvelleValeur &lt; -10) {
    compteur.value = -10
  }
})
&lt;/script&gt;</pre>
                        </div>
                    </div>
                </details>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Les variables réactives sont au cœur de Vue.js. Maîtriser <code class="variable">ref()</code>, <code
                        class="variable">reactive()</code>,
                    <code class="variable">computed()</code> et <code class="variable">watch()</code> est essentiel pour
                    créer des applications interactives et performantes.
                </p>
                <p class="textExemple">
                    Pour approfondir, consultez la
                    <a href="https://vuejs.org/guide/essentials/reactivity-fundamentals.html"
                        class="btn-purple btn-hover" target="_blank">
                        documentation officielle sur la réactivité
                    </a>.
                </p>
            </section>
        </div>
    </div>
</template>

<script setup>
// Aucune logique nécessaire pour cette page de cours
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
    word-wrap: break-word;
    word-break: break-word;
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe */
.keyword {
    color: #c586c0 !important;
}

.variable {
    color: #9cdcfe !important;
}

.string {
    color: #ce9178 !important;
}

.comment {
    color: #6a9955 !important;
}

.function {
    color: #dcdcaa !important;
}

.operator {
    color: #d4d4d4 !important;
}

.constant {
    color: #4fc1ff !important;
}

.number {
    color: #b5cea8 !important;
}

.class-name {
    color: #4ec9b0 !important;
}

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