<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">OWASP Top 10 – Le classement des vulnérabilités web</h1>
                <p class="lesson-meta text-white">Sécurité • OWASP • Risques • Bonnes pratiques</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que l'OWASP ?</h2>
                <p class="textExemple">
                    L’<strong>Open Web Application Security Project (OWASP)</strong> est une communauté internationale à but non lucratif
                    dédiée à l’amélioration de la sécurité des logiciels. Elle produit des ressources gratuites et ouvertes :
                    guides, outils, normes, et le célèbre <strong>OWASP Top 10</strong>.
                </p>
                <p class="textExemple">
                    Le <strong>Top 10</strong> est un rapport régulièrement mis à jour qui liste les dix risques de sécurité les plus critiques
                    pour les applications web. Il sert de référence mondiale pour les développeurs, les architectes,
                    les auditeurs et les responsables sécurité.
                </p>
                <div class="warning-section">
                    <h4 class="text-purple">📅 Dernière version</h4>
                    <p><strong>OWASP Top 10 2021</strong> – La précédente version datait de 2017. La prochaine version est attendue vers 2025.</p>
                </div>
            </section>

            <!-- Pourquoi ce classement est important -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser l'OWASP Top 10 ?</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Prendre conscience des risques majeurs</strong> : la plupart des attaques exploitent ces vulnérabilités.</li>
                        <li><strong>Prioriser les actions de sécurisation</strong> : on commence par corriger les failles les plus critiques.</li>
                        <li><strong>Disposer d’un langage commun</strong> entre développeurs, RSSI, auditeurs.</li>
                        <li><strong>Se conformer aux exigences normatives</strong> (PCI‑DSS, ISO 27001, etc.).</li>
                        <li><strong>Évaluer la maturité d’une application</strong> via des tests automatiques ou manuels.</li>
                    </ul>
                </div>
            </section>

            <!-- Présentation des 10 risques (2021) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">OWASP Top 10 (2021) – Les 10 risques critiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">A01 – Contrôle d’accès défaillant</h3>
                    <p>Les restrictions sur les utilisateurs authentifiés ne sont pas correctement appliquées.
                    Exemples : accès aux données d’un autre utilisateur, modification de son propre rôle, élévation de privilèges.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A02 – Échecs cryptographiques</h3>
                    <p>Données sensibles en clair, algorithmes de chiffrement obsolètes (MD5, SHA1), utilisation de clés faibles,
                    absence de HTTPS, stockage de mots de passe en clair.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A03 – Injections</h3>
                    <p>SQL, NoSQL, LDAP, OS command, etc. L’attaquant envoie des données malveillantes qui sont interprétées
                    comme des commandes par le système. C’est l’une des plus dangereuses (cf. leçon sur les injections SQL).</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A04 – Conception non sécurisée</h3>
                    <p>Faille au niveau de la conception (threat modeling manquant). Exemple : un site e‑commerce qui ne limite pas
                    la quantité d’un produit acheté, ou une API sans rate‑limiting.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A05 – Mauvaise configuration de sécurité</h3>
                    <p>Services inutiles activés, comptes par défaut, pages de debug exposées, en‑têtes HTTP manquants,
                    permissions trop larges sur les fichiers.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A06 – Composants vulnérables</h3>
                    <p>Utilisation de bibliothèques, frameworks ou modules tiers avec des vulnérabilités connues.
                    Exemple : Log4Shell, Heartbleed.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A07 – Échecs d’identification et d’authentification</h3>
                    <p>Gestion faible des mots de passe, absence de MFA, session fixation, fuite de credentials via URL,
                    temps de session trop longs.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A08 – Faille de traitement des données (intégrité)</h3>
                    <p>Absence de vérification de l’intégrité des données (ex: sérialisation non signée, confiance excessive
                    dans les données provenant du client).</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A09 – Monitoring et logging insuffisants</h3>
                    <p>Impossible de détecter une intrusion ou de comprendre une attaque a posteriori par manque de logs
                    ou d’alertes. Les attaquants effacent leurs traces.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">A10 – SSRF (Server-Side Request Forgery)</h3>
                    <p>Le serveur peut être amené à effectuer des requêtes HTTP non contrôlées, pouvant interagir avec des
                    services internes (métadonnées cloud, API internes, etc.).</p>
                </div>
            </section>

            <!-- Méthodologie de calcul du risque -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comment OWASP évalue-t-il les risques ?</h2>
                <div class="textExemple">
                    <p>OWASP utilise une formule simple :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Risque = Probabilité × Impact</code></pre>
                    </div>
                    <ul>
                        <li><strong>Probabilité</strong> : facilité d’exploitation, détectabilité, prévalence.</li>
                        <li><strong>Impact</strong> : technique (perte de confidentialité, d’intégrité, de disponibilité) et business.</li>
                    </ul>
                    <p>Le Top 10 est établi à partir de données réelles (rapports d’audit, outils de scan, bug bounty).</p>
                </div>
            </section>

            <!-- Comment utiliser OWASP dans un projet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Intégrer OWASP dans votre cycle de développement</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Phase de conception</strong> : réaliser un threat modeling avec les risques OWASP.</li>
                        <li><strong>Développement</strong> : se former aux 10 vulnérabilités, utiliser des bibliothèques sécurisées (OWASP ESAPI, CSRFGuard, etc.).</li>
                        <li><strong>Tests</strong> : utiliser des scanners comme OWASP ZAP, Dependency‑Check, ou des tests d’intrusion manuels.</li>
                        <li><strong>Exploitation</strong> : mettre en place du logging et monitoring (A09) et un plan de réponse à incident.</li>
                    </ul>
                </div>
            </section>

            <!-- Outils OWASP utiles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils OWASP phares</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>ZAP (Zed Attack Proxy)</strong> : scanner de vulnérabilités web, très utilisé pour les tests d’intrusion.</li>
                        <li><strong>Dependency‑Check</strong> : détecte les composants vulnérables (A06).</li>
                        <li><strong>ESAPI (Enterprise Security API)</strong> : bibliothèque de fonctions de sécurité (encodage, validation, etc.).</li>
                        <li><strong>CSRFGuard</strong> : protection contre les CSRF.</li>
                        <li><strong>Cheat Sheets</strong> : fiches de bonnes pratiques pour chaque langage/framework.</li>
                        <li><strong>Juice Shop</strong> : application volontairement vulnérable pour s’entraîner (CTF).</li>
                    </ul>
                </div>
            </section>

            <!-- Exemple de vulnérabilité typique (A03) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple concret : Injection SQL (A03)</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Code vulnérable
$id = $_GET['id'];
$sql = "SELECT * FROM users WHERE id = $id";
$result = $conn->query($sql);</code></pre>
                </div>
                <p>Correction avec requête préparée :</p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">$stmt = $conn->prepare("SELECT * FROM users WHERE id = ?");
$stmt->bind_param("i", $id);
$stmt->execute();</code></pre>
                </div>
                <p>Cette vulnérabilité est régulièrement en tête du Top 10 (A03 en 2021).</p>
            </section>

            <!-- Exercices -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Identifier la catégorie OWASP</h3>
                    <p>À quelle catégorie OWASP Top 10 appartiennent ces vulnérabilités ?</p>
                    <ol>
                        <li>Un développeur a laissé activé le mode debug d’un framework en production, exposant les variables d’environnement.</li>
                        <li>Un utilisateur peut voir la fiche d’un autre utilisateur en modifiant l’ID dans l’URL.</li>
                        <li>Les mots de passe sont stockés en clair dans la base de données.</li>
                        <li>Une bibliothèque jQuery obsolète avec une faille XSS connue est utilisée.</li>
                    </ol>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <ol>
                                <li><strong>A05 – Mauvaise configuration de sécurité</strong></li>
                                <li><strong>A01 – Contrôle d’accès défaillant</strong></li>
                                <li><strong>A02 – Échecs cryptographiques</strong></li>
                                <li><strong>A06 – Composants vulnérables</strong></li>
                            </ol>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Mise en place d’un plan d’action</h3>
                    <p>Vous reprenez une application existante. Quelles seraient vos premières actions basées sur l’OWASP Top 10 ?</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <ul>
                                <li>Scanner avec OWASP ZAP et Dependency‑Check.</li>
                                <li>Corriger les injections SQL (A03) et les contrôles d’accès (A01) en priorité.</li>
                                <li>Vérifier la configuration des en‑têtes de sécurité (CSP, HSTS, X‑Frame‑Options).</li>
                                <li>Mettre en place un chiffrement fort pour les données sensibles.</li>
                                <li>Mettre à jour tous les composants tiers (npm, composer, etc.).</li>
                                <li>Activer un système de logging centralisé et d’alertes.</li>
                            </ul>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        L’OWASP Top 10 est bien plus qu’une simple liste : c’est un outil stratégique pour toute organisation
                        souhaitant maîtriser les risques web. En connaissant ces dix catégories, vous pouvez prioriser vos
                        efforts de sécurisation, former vos équipes et choisir les bons outils.
                    </p>
                    <p>
                        Pour aller plus loin, consultez le site officiel <strong>owasp.org</strong>, les <strong>cheat sheets</strong>
                        et le projet <strong>OWASP ASVS</strong> (standard de vérification de la sécurité applicative).
                    </p>
                    <p>
                        Prochaine leçon : nous étudierons en détail les <strong>attaques CSRF</strong> (Cross‑Site Request Forgery)
                        et comment les prévenir dans vos frameworks favoris.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'OwaspLesson',

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
                        const sqlScript = document.createElement('script');
                        sqlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/sql.min.js';
                        sqlScript.onload = resolve;
                        document.head.appendChild(sqlScript);
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
.border-purple { border: 2px solid #e0d6ff; }
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