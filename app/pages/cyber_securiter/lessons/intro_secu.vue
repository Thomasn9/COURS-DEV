<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Introduction à la sécurité web</h1>
                <p class="lesson-meta text-white">Sécurité • OWASP • Cyberattaques • Bonnes pratiques</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi la sécurité web est‑elle cruciale ?</h2>
                <p class="textExemple">
                    Aujourd’hui, les applications web sont partout : banque, santé, e‑commerce, réseaux sociaux.
                    Chaque jour, des données sensibles (identifiants, numéros de carte bancaire, dossiers médicaux)
                    circulent sur le web. La <strong>sécurité</strong> n’est plus une option, c’est une nécessité absolue.
                </p>
                <p class="textExemple">
                    Une faille de sécurité peut coûter des millions d’euros, détruire la réputation d’une entreprise
                    et compromettre la vie privée des utilisateurs. Pourtant, beaucoup de développeurs sous‑estiment
                    les risques ou pensent que « cela n’arrive qu’aux autres ».
                </p>
                <div class="warning-section">
                    <h4 class="text-purple">📊 Chiffres clés</h4>
                    <ul>
                        <li>Selon Verizon, <strong>43% des cyberattaques</strong> visent les petites entreprises.</li>
                        <li>Le coût moyen d’une violation de données en 2024 : <strong>4,88 millions de dollars</strong> (IBM).</li>
                        <li>Les vulnérabilités web (XSS, injections SQL, etc.) représentent <strong>plus des deux tiers</strong> des failles exploitées.</li>
                    </ul>
                </div>
            </section>

            <!-- Conséquences d’une faille -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conséquences d’une sécurité négligée</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Impact business</h3>
                    <ul>
                        <li><strong>Pertes financières directes</strong> : vol, rançons, amendes (RGPD, PCI‑DSS).</li>
                        <li><strong>Perte de confiance des clients</strong> : 65% des clients quittent une entreprise après une fuite de données.</li>
                        <li><strong>Arrêt de service</strong> (DDoS, ransomware) → perte de chiffre d’affaires.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Impact juridique et réglementaire</h3>
                    <ul>
                        <li>RGPD (Europe) : amende pouvant atteindre 20 M€ ou 4% du CA mondial.</li>
                        <li>Loi de programmation militaire (LPM) en France, HIPAA (USA), etc.</li>
                        <li>Obligation de notification des violations aux autorités et aux utilisateurs.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Impact humain</h3>
                    <ul>
                        <li>Usurpation d’identité, harcèlement, chantage.</li>
                        <li>Vol de données médicales ou financières.</li>
                        <li>Mise en danger physique (objets connectés, infrastructures critiques).</li>
                    </ul>
                </div>
            </section>

            <!-- Les piliers de la sécurité : CIA -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les trois piliers : Confidentialité, Intégrité, Disponibilité</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Confidentialité   →  Seules les personnes autorisées accèdent aux données.
Intégrité         →  Les données ne sont pas altérées sans autorisation.
Disponibilité     →  Le service est accessible quand les utilisateurs en ont besoin.</code></pre>
                    </div>
                    <p>
                        Une attaque peut viser un ou plusieurs de ces piliers :
                    </p>
                    <ul>
                        <li><strong>Violation de confidentialité</strong> : vol de mots de passe, exfiltration de données.</li>
                        <li><strong>Atteinte à l’intégrité</strong> : modification frauduleuse d’un virement, défacement de site.</li>
                        <li><strong>Attaque sur la disponibilité</strong> : déni de service (DDoS), ransomware.</li>
                    </ul>
                </div>
            </section>

            <!-- OWASP Top 10 – les vulnérabilités les plus critiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">OWASP Top 10 – Le référentiel mondial</h2>

                <p class="textExemple">
                    L’<strong>Open Web Application Security Project (OWASP)</strong> publie tous les 3-4 ans le classement
                    des 10 vulnérabilités web les plus critiques. Voici un aperçu (édition 2021) :
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-plaintext">1. Contrôle d’accès défaillant
2. Échecs cryptographiques
3. Injections (SQL, NoSQL, OS command, etc.)
4. Conception non sécurisée
5. Mauvaise configuration de sécurité
6. Composants vulnérables
7. Échecs d’identification et d’authentification
8. Faille de traitement des données (intégrité)
9. Monitoring et logging insuffisants
10. SSRF (Server-Side Request Forgery)</code></pre>
                </div>

                <p class="textExemple">
                    Dans les leçons suivantes, nous détaillerons plusieurs de ces risques :
                    XSS, injections SQL, CSRF, etc.
                </p>
            </section>

            <!-- Les attaques web les plus fréquentes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Aperçu des attaques web courantes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Injection SQL</h3>
                    <p>L’attaquant insère du code SQL dans une entrée utilisateur pour lire, modifier ou supprimer des données.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">' OR '1'='1' --</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Cross-Site Scripting (XSS)</h3>
                    <p>Injection de scripts JavaScript malveillants dans des pages vues par d’autres utilisateurs.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Cross-Site Request Forgery (CSRF)</h3>
                    <p>Forcer le navigateur d’un utilisateur authentifié à exécuter une action non souhaitée sur un site.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Déni de service (DDoS)</h3>
                    <p>Saturation du serveur par un flot de requêtes pour rendre le service indisponible.</p>
                </div>
            </section>

            <!-- Les principes fondamentaux de la sécurité web -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Principes fondamentaux à adopter</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Ne jamais faire confiance aux entrées utilisateur</strong> (validation, échappement, assainissement).</li>
                        <li><strong>Défense en profondeur</strong> : multiplier les couches de sécurité.</li>
                        <li><strong>Principe du moindre privilège</strong> : donner le minimum d’autorisations nécessaires.</li>
                        <li><strong>Garder les composants à jour</strong> (framework, bibliothèques, serveur).</li>
                        <li><strong>Sécuriser par défaut</strong> : configurer les options les plus restrictives.</li>
                        <li><strong>Ne pas inventer sa propre crypto</strong> : utiliser des bibliothèques standard.</li>
                        <li><strong>Journaliser et surveiller</strong> les événements suspects.</li>
                    </ul>
                </div>
            </section>

            <!-- Sécurité dans le cycle de développement (DevSecOps) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Intégrer la sécurité dès la conception</h2>

                <p class="textExemple">
                    La sécurité ne doit pas être une « couche » ajoutée à la fin. Elle doit faire partie intégrante
                    du cycle de développement (Shift Left).
                </p>
                <ul>
                    <li><strong>Analyse des risques</strong> en amont (threat modeling).</li>
                    <li><strong>Revues de code</strong> orientées sécurité.</li>
                    <li><strong>Tests automatisés</strong> (SAST, DAST, fuzzing).</li>
                    <li><strong>Formation continue</strong> des développeurs aux bonnes pratiques.</li>
                    <li><strong>Plan de réponse à incident</strong>.</li>
                </ul>
            </section>

            <!-- Mythes et idées reçues -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Idées reçues sur la sécurité web</h2>

                <div class="warning-section">
                    <ul>
                        <li><strong>« Mon site est petit, personne ne va m’attaquer »</strong> → Les attaques sont automatisées, la taille n’est pas un bouclier.</li>
                        <li><strong>« J’utilise HTTPS, je suis en sécurité »</strong> → HTTPS protège le transport, pas les vulnérabilités applicatives.</li>
                        <li><strong>« Un firewall suffit »</strong> → Les firewalls ne bloquent pas les injections SQL ou XSS.</li>
                        <li><strong>« La sécurité, c’est le travail d’un expert »</strong> → Tout développeur doit connaître les bases pour ne pas créer de failles.</li>
                    </ul>
                </div>
            </section>

            <!-- Exercice de sensibilisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice : Évaluer votre propre niveau de sécurité</h2>

                <div class="exercise">
                    <h3 class="text-purple">Questionnaire (réfléchissez avant de regarder la solution)</h3>
                    <ol>
                        <li>Votre application échappe‑t‑elle systématiquement les données affichées ?</li>
                        <li>Utilisez‑vous des requêtes paramétrées pour interagir avec la base de données ?</li>
                        <li>Avez‑vous activé les en‑têtes de sécurité (CSP, HSTS, X‑Frame‑Options) ?</li>
                        <li>Les sessions utilisateur expirent‑elles après un délai d’inactivité ?</li>
                        <li>Testez‑vous régulièrement votre application contre les vulnérabilités courantes ?</li>
                    </ol>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir les bonnes pratiques correspondantes</summary>
                        <div class="solution-content">
                            <ul>
                                <li>1 → Échappement automatique (Twig, blazor, React) ou manuel (<code>htmlspecialchars</code>).</li>
                                <li>2 → Utilisation de requêtes préparées (PDO, Doctrine, etc.).</li>
                                <li>3 → Configurer les en‑têtes HTTP via le serveur ou le framework.</li>
                                <li>4 → Configurer la durée de vie des sessions et un garbage collector.</li>
                                <li>5 → Mettre en place des outils comme OWASP ZAP, audit régulier.</li>
                            </ul>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion : la sécurité est une culture</h2>

                <div class="textExemple">
                    <p>
                        La sécurité web n’est pas une liste de cases à cocher, c’est un <strong>état d’esprit</strong>.
                        Chaque ligne de code peut être une porte d’entrée pour un attaquant. En adoptant les bonnes pratiques
                        dès maintenant, vous protégez vos utilisateurs, votre entreprise et vous‑même.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous détaillerons les vulnérabilités les plus dangereuses
                        (XSS, injections SQL, CSRF, etc.) et vous apprendrez à les prévenir efficacement.
                    </p>
                    <p>
                        <strong>Rappel :</strong> la sécurité est un processus continu. Restez informé, formez‑vous,
                        et n’hésitez jamais à remettre en question la robustesse de votre code.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SecurityIntroLesson',

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
                    const sqlScript = document.createElement('script');
                    sqlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/sql.min.js';
                    sqlScript.onload = resolve;
                    document.head.appendChild(sqlScript);
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