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
                    <pre v-pre><code class="language-bash">composer require symfony/asset-mapper</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">2. Configuration de base</h4>
                    <pre v-pre><code class="language-yaml"># config/packages/asset_mapper.yaml
asset_mapper:
    paths:
        'assets/': '/assets'
    
    # Exclure certains fichiers
    excluded_patterns:
        - '*.scss'
        - '*.ts'
    
    # CDN pour les packages npm
    importmap_script_attributes:
        crossorigin: 'anonymous'</code></pre>
                </div>
            </section>

            <!-- Structure des assets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure des Assets</h2>

                <div class="code-example">
                    <h4 class="text-purple">Organisation recommandée</h4>
                    <pre v-pre><code class="language-plaintext">assets/
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
                    <pre v-pre><code class="language-javascript">// assets/app.js
import './styles/app.css';
import { Alert } from './components/alert.js';
import { Modal } from './components/modal.js';

// Initialisation
document.addEventListener('DOMContentLoaded', () => {
    // Code d'initialisation
    console.log('Application initialisée');
});</code></pre>
                </div>
            </section>

            <!-- Import Map -->
            <section class="lesson-section border-purple">
                <h2 class="text-purple">Utilisation d'Import Map</h2>

                <div class="code-example">
                    <h4 class="text-purple">1. Générer l'Import Map</h4>
                    <pre v-pre><code class="language-bash"># Ajouter un package npm
php bin/console importmap:require lodash

# Voir tous les packages installés
php bin/console importmap:json</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">2. Utilisation dans Twig</h4>
                    <pre v-pre><code class="language-twig">{# base.html.twig #}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;title&gt;{{ title }}&lt;/title&gt;
    {{ importmap() }}
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="app"&gt;&lt;/div&gt;
    &lt;script type="module" src="{{ asset('app.js') }}"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">3. Utiliser des packages npm</h4>
                    <pre v-pre><code class="language-javascript">// assets/app.js
import _ from 'lodash';
import $ from 'jquery';

// Utilisation
const users = _.groupBy(usersList, 'department');
$('#button').click(() => {
    console.log('Click!');
});</code></pre>
                </div>
            </section>

            <!-- Comparaison avec Webpack Encore -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comparaison avec Webpack Encore</h2>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Asset Mapper</h4>
                        <pre v-pre><code class="language-yaml"># Simple configuration
asset_mapper:
    paths:
        'assets/': '/assets'</code></pre>
                        <p class="textExemple">
                            <strong>Avantages :</strong><br>
                            Pas de build step nécessaire<br>
                            Modules ES6 natifs<br>
                            Configuration minimale
                        </p>
                    </div>

                    <div>
                        <h4 class="text-purple">Webpack Encore</h4>
                        <pre v-pre><code class="language-javascript">// Configuration complexe
const Encore = require('@symfony/webpack-encore');

Encore
    .setOutputPath('public/build/')
    .setPublicPath('/build')
    .addEntry('app', './assets/app.js')
    .enableSingleRuntimeChunk()
    .cleanupOutputBeforeBuild()
    .enableBuildNotifications();</code></pre>
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
                    <pre v-pre><code class="language-javascript">// assets/components/Notification.js
export default class Notification {
    constructor(message, type = 'info') {
        this.message = message;
        this.type = type;
    }

    show() {
        // Afficher la notification
    }
}

// Utilisation
import Notification from './components/Notification.js';
const notif = new Notification('Succès !', 'success');
notif.show();</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">2. Gestion du CSS</h4>
                    <pre v-pre><code class="language-css">/* assets/styles/app.css */
@import './base.css';
@import './components/buttons.css';
@import './components/forms.css';

/* CSS personnalisé */
:root {
    --primary-color: #8B5FBF;
    --secondary-color: #6A3093;
}</code></pre>
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
                            <pre v-pre><code class="language-bash">php bin/console importmap:require bootstrap</code></pre>
                        </div>

                        <div class="code-example">
                            <h5>2. Créer le composant Notification</h5>
                            <pre v-pre><code class="language-javascript">// assets/components/Notification.js
export default class Notification {
    constructor(message, type = 'primary') {
        this.message = message;
        this.type = type;
    }

    show(container = 'body') {
        const alert = document.createElement('div');
        alert.className = `alert alert-${this.type} alert-dismissible fade show`;
        alert.role = 'alert';
        alert.innerHTML = `
            ${this.message}
            &lt;button type="button" class="btn-close" data-bs-dismiss="alert"&gt;&lt;/button&gt;
        `;
        
        document.querySelector(container).appendChild(alert);
    }
}</code></pre>
                        </div>

                        <div class="code-example">
                            <h5>3. Fichier app.js principal</h5>
                            <pre v-pre><code class="language-javascript">// assets/app.js
import 'bootstrap/dist/css/bootstrap.min.css';
import 'bootstrap';
import Notification from './components/Notification.js';

document.addEventListener('DOMContentLoaded', () => {
    const form = document.querySelector('#contact-form');
    
    form.addEventListener('submit', (e) => {
        e.preventDefault();
        
        const notif = new Notification(
            'Formulaire envoyé avec succès !',
            'success'
        );
        notif.show();
    });
});</code></pre>
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

/* Couleurs VS Code - version simplifiée */
pre code {
    color: #d4d4d4;
}
/* Pour Bash */
pre code.language-bash {
    color: #9cdcfe;
}

/* Pour YAML */
pre code.language-yaml {
    color: #9cdcfe;
}

pre code.language-yaml .string {
    color: #ce9178 !important;
}

pre code.language-yaml .number {
    color: #b5cea8 !important;
}

/* Pour JavaScript */
pre code.language-javascript {
    color: #9cdcfe;
}

pre code.language-javascript .string {
    color: #ce9178 !important;
}

pre code.language-javascript .keyword {
    color: #c586c0 !important;
}

pre code.language-javascript .comment {
    color: #6a9955 !important;
}

/* Pour CSS */
pre code.language-css {
    color: #9cdcfe;
}

pre code.language-css .property {
    color: #9cdcfe !important;
}

pre code.language-css .keyword {
    color: #c586c0 !important;
}

/* Pour Twig */
pre code.language-twig {
    color: #9cdcfe;
}

/* Pour Plaintext */
pre code.language-plaintext {
    color: #d4d4d4;
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