<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Installer un Projet Vue avec Vite</h1>
                <p class="lesson-meta text-white">Création d'environnements Vue.js modernes et performants</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Vite</h2>
                <p class="textExemple">
                    Vite est un outil de build rapide et léger qui améliore considérablement l'expérience de
                    développement.
                    Contrairement aux bundlers traditionnels, Vite utilise les modules natifs ES pour le développement,
                    ce qui permet un démarrage quasi instantané du serveur et un rechargement à chaud extrêmement
                    rapide.
                </p>
                <p class="textExemple">
                    Dans cette leçon, nous allons découvrir comment installer et configurer un projet Vue.js avec Vite,
                    explorer sa structure et comprendre les avantages de cet outil moderne.
                </p>
            </section>

            <!-- Prérequis -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis</h2>
                <p class="textExemple">
                    Avant de commencer, assurez-vous d'avoir installé les éléments suivants sur votre machine :
                </p>
                <div class="code-example">
                    <pre v-pre>// Vérifier la version de Node.js (version 14.18+ ou 16+ recommandée)
node --version

// Vérifier la version de npm
npm --version</pre>
                </div>
                <p class="textExemple">
                    Si Node.js n'est pas installé, téléchargez-le depuis le site officiel :
                    <a href="https://nodejs.org/" class="btn-purple btn-hover" target="_blank">Node.js</a>
                </p>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Création d'un Projet Vue avec Vite</h2>
                <p class="textExemple">
                    La création d'un projet Vue avec Vite est simple et rapide grâce à l'outil en ligne de commande.
                </p>

                <div class="code-example">
                    <pre v-pre>// Créer un nouveau projet Vue
npm create vite@latest mon-projet-vue -- --template vue

// Naviguer dans le dossier du projet
cd mon-projet-vue

// Installer les dépendances
npm install

// Démarrer le serveur de développement
npm run dev</pre>
                </div>

                <p class="textExemple">
                    Une fois ces commandes exécutées, votre application Vue sera accessible à l'adresse
                    <code class="string">http://localhost:5173</code> (ou un autre port si 5173 est déjà utilisé).
                </p>
            </section>

            <!-- Structure du projet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure du Projet</h2>
                <p class="textExemple">
                    Après avoir créé votre projet, vous obtiendrez une structure de fichiers organisée :
                </p>

                <div class="code-example">
                    <pre v-pre>mon-projet-vue/
├── node_modules/          # Dépendances du projet
├── public/                 # Fichiers statiques
├── src/                    # Code source de l'application
│   ├── assets/              # Ressources (images, styles)
│   ├── components/           # Composants Vue
│   ├── App.vue               # Composant racine
│   └── main.js              # Point d'entrée de l'application
├── index.html             # Page HTML principale
├── package.json           # Configuration du projet et dépendances
├── vite.config.js        # Configuration de Vite
└── README.md              # Documentation du projet</pre>
                </div>
            </section>

            <!-- Scripts disponibles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Scripts NPM Disponibles</h2>
                <p class="textExemple">
                    Vite fournit plusieurs scripts NPM prêts à l'emploi pour différentes phases de développement :
                </p>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">Développement</h4>
                        <pre v-pre>// Démarrer le serveur de développement
npm run dev</pre>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">Production</h4>
                        <pre v-pre>// Construire pour la production
npm run build

// Prévisualiser la build de production
npm run preview</pre>
                    </div>
                </div>
            </section>

            <!-- Configuration Vite -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Configuration de Vite</h2>
                <p class="textExemple">
                    Vous pouvez personnaliser le comportement de Vite en modifiant le fichier <code
                        class="variable">vite.config.js</code>.
                    Voici un exemple de configuration de base pour un projet Vue :
                </p>

                <div class="code-example">
                    <pre v-pre>// vite.config.js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  server: {
    port: 3000,  // Changer le port si nécessaire
    open: true     // Ouvrir automatiquement le navigateur
  },
  build: {
    outDir: 'dist',  // Dossier de sortie pour la build
    sourcemap: true  // Générer des source maps pour le débogage
  }
})</pre>
                </div>
            </section>

            <!-- Avantages de Vite -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages de Vite</h2>
                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">🚀 Rapidité</h4>
                        <p class="textExemple">
                            Vite utilise les modules ES natifs pour un démarrage instantané du serveur de développement,
                            même sur de grands projets.
                        </p>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">🔄 HMR Performant</h4>
                        <p class="textExemple">
                            Le Hot Module Replacement (HMR) est extrêmement rapide, préservant l'état de l'application
                            lors des modifications.
                        </p>
                    </div>
                </div>

                <div class="code-comparison">
                    <div class="code-example">
                        <h4 class="text-purple">📦 Optimisations</h4>
                        <p class="textExemple">
                            Vite pré-packette les dépendances avec esbuild (écrit en Go) pour des builds de production
                            optimisées.
                        </p>
                    </div>

                    <div class="code-example">
                        <h4 class="text-purple">🔧 Extensible</h4>
                        <p class="textExemple">
                            Architecture basée sur les plugins avec une API riche pour étendre les fonctionnalités.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer votre premier projet Vue avec Vite et le personnaliser.
                    </p>

                    <ol class="textExemple">
                        <li>Créez un nouveau projet Vue avec Vite en utilisant la commande vue précédente</li>
                        <li>Modifiez le composant <code class="variable">App.vue</code> pour ajouter votre nom</li>
                        <li>Créez un nouveau composant dans le dossier <code class="variable">components</code></li>
                        <li>Importez et utilisez ce composant dans <code class="variable">App.vue</code></li>
                        <li>Testez le rechargement à chaud en modifiant le style d'un composant</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Composant App.vue modifié</h4>
                        <pre v-pre>&lt;!-- App.vue --&gt;
&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;img alt="Vue logo" src="./assets/logo.png" /&gt;
    &lt;h1&gt;Bienvenue dans mon application Vue, {{ name }}!&lt;/h1&gt;
    &lt;MonComposant /&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
import { ref } from 'vue'
import MonComposant from './components/MonComposant.vue'

const name = ref('VotreNom')
&lt;/script&gt;</pre>

                        <h4 class="text-purple">Nouveau composant MonComposant.vue</h4>
                        <pre v-pre>&lt;!-- components/MonComposant.vue --&gt;
&lt;template&gt;
  &lt;div class="mon-composant"&gt;
    &lt;p&gt;Ceci est mon premier composant Vue!&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script setup&gt;
// La logique du composant va ici
&lt;/script&gt;

&lt;style scoped&gt;
.mon-composant {
  padding: 1rem;
  background-color: #f0f0f0;
  border-radius: 8px;
  margin-top: 1rem;
}
&lt;/style&gt;</pre>
                    </div>
                </details>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Félicitations ! Vous avez maintenant les bases pour créer et configurer un projet Vue.js moderne
                    avec Vite.
                </p>
                <p class="textExemple">
                    Vite offre une expérience de développement exceptionnellement rapide et fluide,
                    tout en produisant des builds de production optimisées.
                    C'est désormais l'outil recommandé pour le développement d'applications Vue.js.
                </p>
                <p class="textExemple">
                    Pour approfondir vos connaissances, consultez la
                    <a href="https://vitejs.dev/guide/" class="btn-purple btn-hover" target="_blank">documentation
                        officielle de Vite</a>.
                </p>
            </section>
        </div>
    </div>
</template>

<script setup>
// Le code JavaScript de la page leçon peut aller ici si nécessaire
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