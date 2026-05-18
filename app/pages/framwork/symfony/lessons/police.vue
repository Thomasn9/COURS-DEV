<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Polices d'écriture dans Symfony</h1>
                <p class="lesson-meta text-white">Symfony • AssetMapper • Webpack Encore • Google Fonts • Typographie</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux polices web</h2>
                <p class="textExemple">
                    L'intégration de polices d'écriture personnalisées est essentielle pour l'identité visuelle d'un projet.
                    Symfony, via son système d'assets (AssetMapper ou Webpack Encore), permet d'intégrer facilement des polices
                    locales ou distantes tout en gérant les versions et la performance.
                </p>
                <p class="textExemple">
                    Deux approches principales s'offrent à vous : l'utilisation de services externes comme Google Fonts,
                    ou l'hébergement local des fichiers de polices (pour la conformité RGPD ou le travail hors ligne).
                </p>
            </section>

            <!-- Architecture des assets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture des assets dans Symfony</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Où placer les polices ?</h3>
                    <ul>
                        <li><strong>AssetMapper (Symfony 6.3+)</strong> : les polices vont dans <code>assets/styles/</code> ou <code>assets/fonts/</code></li>
                        <li><strong>Webpack Encore</strong> : les polices sont généralement dans <code>assets/fonts/</code> et importées via CSS/JS</li>
                        <li><strong>public/</strong> : approche traditionnelle (non recommandée avec les bundles modernes)</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement (AssetMapper)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">assets/
├── styles/
│   ├── app.css         # @import des polices locales
│   └── fonts.css       # Déclaration des @font-face
├── fonts/
│   ├── OpenSans-Regular.woff2
│   └── OpenSans-Bold.woff2
└── app.js              # Point d'entrée qui importe app.css

# Commande pour installer AssetMapper (si pas déjà fait)
composer require symfony/asset-mapper</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthode 1 : Google Fonts -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 1 : Google Fonts (CDN externe)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Intégration simple dans Twig</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;head&gt;
    &lt;link href="https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,400;0,500;0,700;1,400&amp;display=swap" rel="stylesheet"&gt;
&lt;/head&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Avec préconnexion (meilleure performance)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;head&gt;
    &lt;link rel="preconnect" href="https://fonts.googleapis.com"&gt;
    &lt;link rel="preconnect" href="https://fonts.gstatic.com" crossorigin&gt;
    &lt;link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&amp;display=swap" rel="stylesheet"&gt;
&lt;/head&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Application en CSS</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-css">body {
    font-family: 'Inter', sans-serif;
}
h1, h2, h3 {
    font-weight: 700;
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthode 2 : Polices locales -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthode 2 : Polices hébergées localement</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Téléchargement et placement des fichiers</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">mkdir -p assets/fonts
# Placer les fichiers .woff2 dans assets/fonts/</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Déclaration @font-face dans CSS</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-css">@font-face {
    font-family: 'Open Sans';
    src: url('../fonts/open-sans-400.woff2') format('woff2');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}
body {
    font-family: 'Open Sans', sans-serif;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Import du CSS (AssetMapper)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// assets/app.js
import './styles/fonts.css';
import './styles/app.css';</code></pre>
                    </div>
                </div>
            </section>

            <!-- Optimisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Optimisation et bonnes pratiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Utiliser WOFF2</h3>
                    <p>Meilleure compression, supporté par tous les navigateurs modernes.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. font-display: swap</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-css">@font-face {
    font-display: swap;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Limiter les graisses</h3>
                    <p>Ne charger que les poids utilisés (400, 500, 700 par exemple).</p>
                </div>
            </section>

            <!-- Exercices -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Google Fonts "Poppins"</h3>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-twig">&lt;link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&amp;display=swap" rel="stylesheet"&gt;
&lt;style&gt;body { font-family: 'Poppins', sans-serif; }&lt;/style&gt;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Police locale "Roboto"</h3>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-css">@font-face {
    font-family: 'Roboto';
    src: url('../fonts/Roboto-Regular.woff2') format('woff2');
    font-weight: 400;
}
body { font-family: 'Roboto', sans-serif; }</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Résumé et bonnes pratiques</h2>
                <ul>
                    <li>✓ Utiliser WOFF2</li>
                    <li>✓ <code>font-display: swap</code></li>
                    <li>✓ Précharger les polices critiques</li>
                    <li>✓ Polices locales pour le RGPD</li>
                </ul>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'WebfontLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const languages = ['css', 'twig', 'bash', 'php', 'javascript', 'plaintext'];
                    let loaded = 0;
                    languages.forEach(lang => {
                        const langScript = document.createElement('script');
                        langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`;
                        langScript.onload = () => {
                            loaded++;
                            if (loaded === languages.length) resolve();
                        };
                        document.head.appendChild(langScript);
                    });
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
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
    top: 0; left: 0; right: 0; bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
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
    animation: fadeInUp 0.6s ease forwards;
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

.bg-light-purple { background-color: #f8f6ff; }
.border-purple { border: 2px solid #e0d6ff; transition: all 0.3s ease; }
.text-purple { color: #6A3093 !important; }
.text-white { color: white !important; }

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

.code-example {
    margin: 1.5rem 0;
    width: 100%;
    box-sizing: border-box;
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
    width: 100%;
    box-sizing: border-box;
    white-space: pre;
    margin: 0;
}

pre code {
    display: block;
    white-space: pre;
    width: 100%;
}

.exercise { margin: 2rem 0; }
.solution { margin: 1rem 0; }
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
    .lesson-container { padding: 1rem; }
    .lesson-header { padding: 2rem 1rem; }
    .lesson-header h1 { font-size: 2rem; }
    .lesson-section { padding: 1.5rem; }
    pre { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section { padding: 1rem; }
    .lesson-header { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
}
</style>