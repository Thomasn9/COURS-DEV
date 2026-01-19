<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- Header avec gradient -->
            <header class="lesson-header text-white">
                <h1>Asset Mapper dans Symfony</h1>
                <p class="lesson-meta">
                    Gestion moderne des assets sans Webpack Encore • Symfony 6.3+
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Asset Mapper</h2>
                <p class="textExemple">
                    Asset Mapper est une nouvelle fonctionnalité introduite dans Symfony 6.3 qui permet de gérer
                    les assets (CSS, JavaScript, images) sans avoir besoin d'outils de build complexes comme
                    Webpack Encore. Il utilise l'importation native des modules ES6 du navigateur.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Pourquoi Asset Mapper ?</h4>
                    <ul>
                        <li><strong>Simplicité</strong> : Pas de configuration Webpack/Encore complexe</li>
                        <li><strong>Performance</strong> : Le navigateur gère lui-même les dépendances</li>
                        <li><strong>Modernité</strong> : Utilisation des modules ES6 natifs</li>
                        <li><strong>DX amélioré</strong> : Meilleure expérience développeur</li>
                    </ul>
                </div>
            </section>

            <!-- Installation et configuration -->
            <section class="lesson-section border-purple">
                <h2 class="text-purple">Installation et Configuration</h2>

                <div class="code-example">
                    <h4 class="text-purple">1. Installation du composant</h4>
                    <pre v-pre><code class="bash">composer require symfony/asset-mapper</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">2. Configuration de base</h4>
                    <pre v-pre><code class="yaml"><span class="comment"># config/packages/asset_mapper.yaml</span>
<span class="property">asset_mapper</span><span class="punctuation">:</span>
    <span class="property">paths</span><span class="punctuation">:</span>
        <span class="string">'assets/'</span><span class="punctuation">:</span> <span class="string">'/assets'</span>
    
    <span class="comment"># Exclure certains fichiers</span>
    <span class="property">excluded_patterns</span><span class="punctuation">:</span>
        <span class="punctuation">-</span> <span class="string">'*.scss'</span>
        <span class="punctuation">-</span> <span class="string">'*.ts'</span>
    
    <span class="comment"># CDN pour les packages npm</span>
    <span class="property">importmap_script_attributes</span><span class="punctuation">:</span>
        <span class="property">crossorigin</span><span class="punctuation">:</span> <span class="string">'anonymous'</span></code></pre>
                </div>
            </section>

            <!-- Structure des assets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure des Assets</h2>

                <div class="code-example">
                    <h4 class="text-purple">Organisation recommandée</h4>
                    <pre v-pre><code class="plaintext">assets/
├── app.js                    # Point d'entrée principal
├── styles/
│   ├── app.css              # CSS principal
│   └── components/          # CSS des composants
├── components/              # Composants JavaScript
│   ├── alert.js
│   └── modal.js
├── lib/                     # Bibliothèques tierces
└── images/                  # Images</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Fichier d'entrée principal (app.js)</h4>
                    <pre v-pre><code class="javascript"><span class="comment">// assets/app.js</span>
<span class="keyword">import</span> <span class="string">'./styles/app.css'</span><span class="punctuation">;</span>
<span class="keyword">import</span> <span class="punctuation">{</span> <span class="class-name">Alert</span> <span class="punctuation">}</span> <span class="keyword">from</span> <span class="string">'./components/alert.js'</span><span class="punctuation">;</span>
<span class="keyword">import</span> <span class="punctuation">{</span> <span class="class-name">Modal</span> <span class="punctuation">}</span> <span class="keyword">from</span> <span class="string">'./components/modal.js'</span><span class="punctuation">;</span>

<span class="comment">// Initialisation</span>
<span class="function">document</span><span class="punctuation">.</span><span class="function">addEventListener</span><span class="punctuation">(</span><span class="string">'DOMContentLoaded'</span><span class="punctuation">,</span> <span class="punctuation">()</span> <span class="punctuation">=&gt;</span> <span class="punctuation">{</span>
    <span class="comment">// Code d'initialisation</span>
    <span class="function">console</span><span class="punctuation">.</span><span class="function">log</span><span class="punctuation">(</span><span class="string">'Application initialisée'</span><span class="punctuation">);</span>
<span class="punctuation">}</span><span class="punctuation">)</span><span class="punctuation">;</span></code></pre>
                </div>
            </section>

            <!-- Import Map -->
            <section class="lesson-section border-purple">
                <h2 class="text-purple">Utilisation d'Import Map</h2>

                <div class="code-example">
                    <h4 class="text-purple">1. Générer l'Import Map</h4>
                    <pre v-pre><code class="bash"># Ajouter un package npm
php bin/console importmap:require lodash

# Voir tous les packages installés
php bin/console importmap:json</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">2. Utilisation dans Twig</h4>
                    <pre v-pre><code class="twig"><span class="comment">{# base.html.twig #}</span>
&lt;<span class="tag">!DOCTYPE html</span>&gt;
&lt;<span class="tag">html</span>&gt;
&lt;<span class="tag">head</span>&gt;
    &lt;<span class="tag">title</span>&gt;{{ <span class="variable">title</span> }}&lt;/<span class="tag">title</span>&gt;
    {{ <span class="function">importmap</span>() }}
&lt;/<span class="tag">head</span>&gt;
&lt;<span class="tag">body</span>&gt;
    &lt;<span class="tag">div</span> <span class="attribute">id</span>=<span class="string">"app"</span>&gt;&lt;/<span class="tag">div</span>&gt;
    &lt;<span class="tag">script</span> <span class="attribute">type</span>=<span class="string">"module"</span> <span class="attribute">src</span>="{{ <span class="function">asset</span>(<span class="string">'app.js'</span>) }}"&gt;&lt;/<span class="tag">script</span>&gt;
&lt;/<span class="tag">body</span>&gt;
&lt;/<span class="tag">html</span>&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">3. Utiliser des packages npm</h4>
                    <pre v-pre><code class="javascript"><span class="comment">// assets/app.js</span>
<span class="keyword">import</span> <span class="variable">_</span> <span class="keyword">from</span> <span class="string">'lodash'</span><span class="punctuation">;</span>
<span class="keyword">import</span> <span class="variable">$</span> <span class="keyword">from</span> <span class="string">'jquery'</span><span class="punctuation">;</span>

<span class="comment">// Utilisation</span>
<span class="keyword">const</span> <span class="variable">users</span> <span class="operator">=</span> <span class="function">_</span><span class="punctuation">.</span><span class="function">groupBy</span><span class="punctuation">(</span><span class="variable">usersList</span><span class="punctuation">,</span> <span class="string">'department'</span><span class="punctuation">)</span><span class="punctuation">;</span>
<span class="function">$</span><span class="punctuation">(</span><span class="string">'#button'</span><span class="punctuation">)</span><span class="punctuation">.</span><span class="function">click</span><span class="punctuation">(()</span> <span class="punctuation">=&gt;</span> <span class="punctuation">{</span>
    <span class="function">console</span><span class="punctuation">.</span><span class="function">log</span><span class="punctuation">(</span><span class="string">'Click!'</span><span class="punctuation">)</span><span class="punctuation">;</span>
<span class="punctuation">}</span><span class="punctuation">)</span><span class="punctuation">;</span></code></pre>
                </div>
            </section>

            <!-- Comparaison avec Webpack Encore -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comparaison avec Webpack Encore</h2>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Asset Mapper</h4>
                        <pre v-pre><code class="yaml"><span class="comment"># Simple configuration</span>
<span class="property">asset_mapper</span><span class="punctuation">:</span>
    <span class="property">paths</span><span class="punctuation">:</span>
        <span class="string">'assets/'</span><span class="punctuation">:</span> <span class="string">'/assets'</span></code></pre>
                        <p class="textExemple">
                            <strong>Avantages :</strong><br>
                            Pas de build step nécessaire<br>
                            Modules ES6 natifs<br>
                            Configuration minimale
                        </p>
                    </div>

                    <div>
                        <h4 class="text-purple">Webpack Encore</h4>
                        <pre v-pre><code class="javascript"><span class="comment">// Configuration complexe</span>
<span class="keyword">const</span> <span class="class-name">Encore</span> <span class="operator">=</span> <span class="function">require</span><span class="punctuation">(</span><span class="string">'@symfony/webpack-encore'</span><span class="punctuation">)</span><span class="punctuation">;</span>

<span class="class-name">Encore</span>
    <span class="punctuation">.</span><span class="function">setOutputPath</span><span class="punctuation">(</span><span class="string">'public/build/'</span><span class="punctuation">)</span>
    <span class="punctuation">.</span><span class="function">setPublicPath</span><span class="punctuation">(</span><span class="string">'/build'</span><span class="punctuation">)</span>
    <span class="punctuation">.</span><span class="function">addEntry</span><span class="punctuation">(</span><span class="string">'app'</span><span class="punctuation">,</span> <span class="string">'./assets/app.js'</span><span class="punctuation">)</span>
    <span class="punctuation">.</span><span class="function">enableSingleRuntimeChunk</span><span class="punctuation">(</span><span class="punctuation">)</span>
    <span class="punctuation">.</span><span class="function">cleanupOutputBeforeBuild</span><span class="punctuation">(</span><span class="punctuation">)</span>
    <span class="punctuation">.</span><span class="function">enableBuildNotifications</span><span class="punctuation">(</span><span class="punctuation">)</span><span class="punctuation">;</span></code></pre>
                        <p class="textExemple">
                            <strong>Inconvénients :</strong><br>
                            Build step requis<br>
                            Configuration complexe<br>
                            Dépend à Node.js
                        </p>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section border-purple">
                <h2 class="text-purple">Bonnes Pratiques</h2>

                <div class="code-example">
                    <h4 class="text-purple">1. Organisation des composants</h4>
                    <pre v-pre><code class="javascript"><span class="comment">// assets/components/Notification.js</span>
<span class="keyword">export</span> <span class="keyword">default</span> <span class="keyword">class</span> <span class="class-name">Notification</span> <span class="punctuation">{</span>
    <span class="function">constructor</span><span class="punctuation">(</span><span class="parameter">message</span><span class="punctuation">,</span> <span class="parameter">type</span> <span class="operator">=</span> <span class="string">'info'</span><span class="punctuation">)</span> <span class="punctuation">{</span>
        <span class="keyword">this</span><span class="punctuation">.</span><span class="property">message</span> <span class="operator">=</span> <span class="variable">message</span><span class="punctuation">;</span>
        <span class="keyword">this</span><span class="punctuation">.</span><span class="property">type</span> <span class="operator">=</span> <span class="variable">type</span><span class="punctuation">;</span>
    <span class="punctuation">}</span>

    <span class="function">show</span><span class="punctuation">(</span><span class="punctuation">)</span> <span class="punctuation">{</span>
        <span class="comment">// Afficher la notification</span>
    <span class="punctuation">}</span>
<span class="punctuation">}</span>

<span class="comment">// Utilisation</span>
<span class="keyword">import</span> <span class="class-name">Notification</span> <span class="keyword">from</span> <span class="string">'./components/Notification.js'</span><span class="punctuation">;</span>
<span class="keyword">const</span> <span class="variable">notif</span> <span class="operator">=</span> <span class="keyword">new</span> <span class="class-name">Notification</span><span class="punctuation">(</span><span class="string">'Succès !'</span><span class="punctuation">,</span> <span class="string">'success'</span><span class="punctuation">)</span><span class="punctuation">;</span>
<span class="variable">notif</span><span class="punctuation">.</span><span class="function">show</span><span class="punctuation">(</span><span class="punctuation">)</span><span class="punctuation">;</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">2. Gestion du CSS</h4>
                    <pre v-pre><code class="css"><span class="comment">/* assets/styles/app.css */</span>
<span class="keyword">@import</span> <span class="string">'./base.css'</span><span class="punctuation">;</span>
<span class="keyword">@import</span> <span class="string">'./components/buttons.css'</span><span class="punctuation">;</span>
<span class="keyword">@import</span> <span class="string">'./components/forms.css'</span><span class="punctuation">;</span>

<span class="comment">/* CSS personnalisé */</span>
<span class="selector">:root</span> <span class="punctuation">{</span>
    <span class="property">--primary-color</span><span class="punctuation">:</span> <span class="value">#8B5FBF</span><span class="punctuation">;</span>
    <span class="property">--secondary-color</span><span class="punctuation">:</span> <span class="value">#6A3093</span><span class="punctuation">;</span>
<span class="punctuation">}</span></code></pre>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>

                <div class="exercise">
                    <h4 class="text-purple">Objectif : Créer une application simple avec Asset Mapper</h4>
                    <p class="textExemple">
                        Créez une petite application qui :
                    </p>
                    <ol>
                        <li>Utilise Bootstrap via CDN dans l'import map</li>
                        <li>Importe un composant JavaScript personnalisé</li>
                        <li>Gère un formulaire avec validation</li>
                        <li>Affiche des notifications</li>
                    </ol>

                    <button class="btn-purple btn-hover" @click="toggleSolution">
                        {{ showSolution ? 'Masquer' : 'Afficher' }} la solution
                    </button>

                    <div v-if="showSolution" class="solution-content">
                        <h4 class="text-purple">Solution :</h4>

                        <div class="code-example">
                            <h5>1. Ajouter Bootstrap</h5>
                            <pre v-pre><code class="bash">php bin/console importmap:require bootstrap</code></pre>
                        </div>

                        <div class="code-example">
                            <h5>2. Créer le composant Notification</h5>
                            <pre v-pre><code class="javascript"><span class="comment">// assets/components/Notification.js</span>
<span class="keyword">export</span> <span class="keyword">default</span> <span class="keyword">class</span> <span class="class-name">Notification</span> <span class="punctuation">{</span>
    <span class="function">constructor</span><span class="punctuation">(</span><span class="parameter">message</span><span class="punctuation">,</span> <span class="parameter">type</span> <span class="operator">=</span> <span class="string">'primary'</span><span class="punctuation">)</span> <span class="punctuation">{</span>
        <span class="keyword">this</span><span class="punctuation">.</span><span class="property">message</span> <span class="operator">=</span> <span class="variable">message</span><span class="punctuation">;</span>
        <span class="keyword">this</span><span class="punctuation">.</span><span class="property">type</span> <span class="operator">=</span> <span class="variable">type</span><span class="punctuation">;</span>
    <span class="punctuation">}</span>

    <span class="function">show</span><span class="punctuation">(</span><span class="parameter">container</span> <span class="operator">=</span> <span class="string">'body'</span><span class="punctuation">)</span> <span class="punctuation">{</span>
        <span class="keyword">const</span> <span class="variable">alert</span> <span class="operator">=</span> <span class="function">document</span><span class="punctuation">.</span><span class="function">createElement</span><span class="punctuation">(</span><span class="string">'div'</span><span class="punctuation">)</span><span class="punctuation">;</span>
        <span class="variable">alert</span><span class="punctuation">.</span><span class="property">className</span> <span class="operator">=</span> <span class="string">`alert alert-</span><span class="substitution">${<span class="keyword">this</span><span class="punctuation">.</span><span class="property">type</span>}</span><span class="string"> alert-dismissible fade show`</span><span class="punctuation">;</span>
        <span class="variable">alert</span><span class="punctuation">.</span><span class="property">role</span> <span class="operator">=</span> <span class="string">'alert'</span><span class="punctuation">;</span>
        <span class="variable">alert</span><span class="punctuation">.</span><span class="property">innerHTML</span> <span class="operator">=</span> <span class="string">`
            </span><span class="substitution">${<span class="keyword">this</span><span class="punctuation">.</span><span class="property">message</span>}</span><span class="string">
            &lt;button type="button" class="btn-close" data-bs-dismiss="alert"&gt;&lt;/button&gt;
        `</span><span class="punctuation">;</span>
        
        <span class="function">document</span><span class="punctuation">.</span><span class="function">querySelector</span><span class="punctuation">(</span><span class="variable">container</span><span class="punctuation">)</span><span class="punctuation">.</span><span class="function">appendChild</span><span class="punctuation">(</span><span class="variable">alert</span><span class="punctuation">)</span><span class="punctuation">;</span>
    <span class="punctuation">}</span>
<span class="punctuation">}</span></code></pre>
                        </div>

                        <div class="code-example">
                            <h5>3. Fichier app.js principal</h5>
                            <pre v-pre><code class="javascript"><span class="comment">// assets/app.js</span>
<span class="keyword">import</span> <span class="string">'bootstrap/dist/css/bootstrap.min.css'</span><span class="punctuation">;</span>
<span class="keyword">import</span> <span class="string">'bootstrap'</span><span class="punctuation">;</span>
<span class="keyword">import</span> <span class="class-name">Notification</span> <span class="keyword">from</span> <span class="string">'./components/Notification.js'</span><span class="punctuation">;</span>

<span class="function">document</span><span class="punctuation">.</span><span class="function">addEventListener</span><span class="punctuation">(</span><span class="string">'DOMContentLoaded'</span><span class="punctuation">,</span> <span class="punctuation">()</span> <span class="punctuation">=&gt;</span> <span class="punctuation">{</span>
    <span class="keyword">const</span> <span class="variable">form</span> <span class="operator">=</span> <span class="function">document</span><span class="punctuation">.</span><span class="function">querySelector</span><span class="punctuation">(</span><span class="string">'#contact-form'</span><span class="punctuation">)</span><span class="punctuation">;</span>
    
    <span class="variable">form</span><span class="punctuation">.</span><span class="function">addEventListener</span><span class="punctuation">(</span><span class="string">'submit'</span><span class="punctuation">,</span> <span class="punctuation">(</span><span class="parameter">e</span><span class="punctuation">)</span> <span class="punctuation">=&gt;</span> <span class="punctuation">{</span>
        <span class="variable">e</span><span class="punctuation">.</span><span class="function">preventDefault</span><span class="punctuation">(</span><span class="punctuation">)</span><span class="punctuation">;</span>
        
        <span class="keyword">const</span> <span class="variable">notif</span> <span class="operator">=</span> <span class="keyword">new</span> <span class="class-name">Notification</span><span class="punctuation">(</span>
            <span class="string">'Formulaire envoyé avec succès !'</span><span class="punctuation">,</span>
            <span class="string">'success'</span>
        <span class="punctuation">)</span><span class="punctuation">;</span>
        <span class="variable">notif</span><span class="punctuation">.</span><span class="function">show</span><span class="punctuation">(</span><span class="punctuation">)</span><span class="punctuation">;</span>
    <span class="punctuation">}</span><span class="punctuation">)</span><span class="punctuation">;</span>
<span class="punctuation">}</span><span class="punctuation">)</span><span class="punctuation">;</span></code></pre>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-gradient-primary text-white">
                <h2>Conclusion</h2>
                <p class="textExemple">
                    Asset Mapper représente l'avenir de la gestion des assets dans Symfony. Il offre une alternative
                    moderne et simplifiée à Webpack Encore, particulièrement adaptée aux petites et moyennes
                    applications.
                    Bien qu'il ne remplace pas entièrement Webpack pour les projets complexes nécessitant du
                    tree-shaking
                    avancé ou du code splitting, il est parfait pour la majorité des applications Symfony.
                </p>
            </section>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const showSolution = ref(false)

const toggleSolution = () => {
    showSolution.value = !showSolution.value
}
</script>

<style scoped>
/* Le même CSS que vous avez fourni */
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

/* COULEURS VS CODE PURE CSS - PAS DE LIBRAIRIE */
pre code {
    color: #d4d4d4; /* Couleur par défaut */
}

/* Commentaires - vert VS Code */
pre code .comment {
    color: #6A9955 !important;
    font-style: italic;
}

/* Chaînes de caractères - orange VS Code */
pre code .string {
    color: #CE9178 !important;
}

/* Nombres - vert clair VS Code */
pre code .number {
    color: #B5CEA8 !important;
}

/* Mots-clés - violet VS Code */
pre code .keyword {
    color: #C586C0 !important;
    font-weight: bold;
}

/* Fonctions - jaune VS Code */
pre code .function {
    color: #DCDCAA !important;
}

/* Classes - turquoise VS Code */
pre code .class-name {
    color: #4EC9B0 !important;
}

/* Variables - bleu clair VS Code */
pre code .variable {
    color: #9CDCFE !important;
}

/* Opérateurs - gris clair */
pre code .operator {
    color: #D4D4D4 !important;
}

/* Ponctuation - gris clair */
pre code .punctuation {
    color: #D4D4D4 !important;
}

/* Propriétés (YAML, CSS) - bleu VS Code */
pre code .property {
    color: #9CDCFE !important;
}

/* Valeurs (CSS) - orange VS Code */
pre code .value {
    color: #CE9178 !important;
}

/* Sélecteurs (CSS) - jaune VS Code */
pre code .selector {
    color: #D7BA7D !important;
}

/* Tags HTML/Twig - bleu VS Code */
pre code .tag {
    color: #569CD6 !important;
}

/* Attributs HTML/Twig - vert VS Code */
pre code .attribute {
    color: #9CDCFE !important;
}

/* Variables Twig - bleu VS Code */
pre code .twig-variable {
    color: #9CDCFE !important;
}

/* Substitution dans les templates strings */
pre code .substitution {
    color: #DCDCAA !important;
}

/* Paramètres de fonctions */
pre code .parameter {
    color: #9CDCFE !important;
}

/* Styles spécifiques pour Bash */
pre code.bash {
    color: #9CDCFE !important;
}

/* Styles spécifiques pour Plaintext */
pre code.plaintext {
    color: #D4D4D4 !important;
}

/* Pour les commentaires en Bash (commençant par #) */
pre code.bash:before {
    content: "$ ";
    color: #D4D4D4;
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