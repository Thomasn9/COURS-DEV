<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Symfony Profiler</h1>
                <p class="lesson-meta text-white">Symfony • Debug • Performance • Web Profiler • Toolbar</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le Symfony Profiler ?</h2>
                <p class="textExemple">
                    Le Symfony Profiler (ou Web Debug Toolbar) est un outil de développement intégré au framework Symfony.
                    Il fournit en temps réel une multitude d'informations sur la requête HTTP en cours : temps d'exécution,
                    mémoire consommée, requêtes SQL, logs, événements, routes, etc.
                </p>
                <p class="textExemple">
                    Accessible via une barre d'outils en bas de page (en environnement de développement), il permet de diagnostiquer
                    rapidement les problèmes de performance, de comprendre le flux d'exécution et d'analyser les interactions
                    avec la base de données ou le cache.
                </p>
            </section>

            <!-- Installation et activation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et activation</h2>
                <div class="textExemple">
                    <p>
                        Le Profiler fait partie du <strong>Web Profiler Bundle</strong>, généralement inclus par défaut
                        dans l'environnement de développement. Pour l'installer :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installation du bundle (si absent)
composer require symfony/profiler-pack --dev</code></pre>
                    </div>
                    <p>
                        La configuration par défaut dans <code>config/packages/dev/web_profiler.yaml</code> :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/dev/web_profiler.yaml
web_profiler:
    toolbar: true
    intercept_redirects: false

framework:
    profiler:
        only_exceptions: false
        collect_serializer_data: true</code></pre>
                    </div>
                    <p>
                        Pour désactiver le profiler (par exemple en production), assurez-vous que la configuration
                        dans <code>config/packages/prod/web_profiler.yaml</code> désactive la barre :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">web_profiler:
    toolbar: false
    intercept_redirects: false

framework:
    profiler: false</code></pre>
                    </div>
                </div>
            </section>

            <!-- La barre d'outils (Toolbar) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La barre d'outils (Debug Toolbar)</h2>
                <p class="textExemple">
                    Une fois activée, une barre horizontale apparaît en bas de chaque page (sauf les redirections et les pages Ajax).
                    Elle affiche des indicateurs synthétiques :
                </p>
                <ul>
                    <li><strong>Statut HTTP</strong> (200, 404, 500, etc.)</li>
                    <li><strong>Temps d'exécution</strong> (en ms)</li>
                    <li><strong>Mémoire consommée</strong> (en Mo)</li>
                    <li><strong>Nombre de requêtes SQL</strong> et temps total</li>
                    <li><strong>Nombre d'événements</strong> (dispatcher)</li>
                    <li><strong>Utilisateur authentifié</strong> (si oui, son nom)</li>
                    <li><strong>Environnement</strong> (dev, test, prod)</li>
                    <li><strong>Version Symfony</strong></li>
                </ul>
                <p class="textExemple">
                    En cliquant sur chaque section, on accède au Profiler complet avec des détails exhaustifs.
                </p>
                <div class="warning-section">
                    <p class="warning-text">
                        ⚠️ Le profiler ne doit <strong>jamais</strong> être activé en production, car il expose
                        des informations sensibles (requêtes SQL, configuration, logs, etc.) et dégrade les performances.
                    </p>
                </div>
            </section>

            <!-- Le Profiler complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le Profiler : interface détaillée</h2>
                <p class="textExemple">
                    En cliquant sur la barre d'outils ou en accédant à l'URL <code>/_profiler</code>, vous arrivez sur
                    une page listant toutes les requêtes récentes. Vous pouvez en sélectionner une pour voir le détail.
                </p>
                <p class="textExemple">
                    Le Profiler est organisé en plusieurs onglets (panels) :
                </p>

                <h3 class="text-purple">Panel Summary</h3>
                <p>Résumé global : méthode HTTP, statut, URI, IP client, version Symfony, environnement, etc.</p>

                <h3 class="text-purple">Panel Request / Response</h3>
                <p>
                    Détail des en-têtes (headers) de la requête et de la réponse, paramètres GET/POST, attributs de route,
                    session, cookies, contenu brut.
                </p>

                <h3 class="text-purple">Panel Controller</h3>
                <p>
                    Nom du contrôleur et de la méthode exécutée, arguments passés, type de retour (Response, JsonResponse, etc.).
                </p>

                <h3 class="text-purple">Panel Routing</h3>
                <p>
                    Route correspondante, nom de la route, paramètres, conditions (scheme, host, methods), et liste de toutes
                    les routes de l'application.
                </p>

                <h3 class="text-purple">Panel Database (Doctrine)</h3>
                <p>
                    Liste de toutes les requêtes SQL exécutées, leur durée, leur stack trace, la possibilité d'expliquer
                    le plan d'exécution (EXPLAIN). Permet d'identifier les requêtes lentes ou redondantes.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-sql">-- Exemple de requête affichée dans le profiler
SELECT t0.id AS id_1, t0.title AS title_2, t0.content AS content_3 FROM article t0 WHERE t0.published = 1
-- Durée : 2.34 ms</code></pre>
                </div>

                <h3 class="text-purple">Panel Cache</h3>
                <p>Opérations de cache (get, set, delete) et leurs temps d'exécution.</p>

                <h3 class="text-purple">Panel Logs</h3>
                <p>
                    Affiche tous les logs générés lors de la requête, avec leur niveau (info, warning, error, debug).
                    Utile pour tracer des erreurs ou des comportements inattendus.
                </p>

                <h3 class="text-purple">Panel Events (Event Dispatcher)</h3>
                <p>
                    Liste des événements déclenchés, les listeners appelés et leur durée d'exécution.
                    Permet de comprendre le flux du noyau Symfony.
                </p>

                <h3 class="text-purple">Panel Security</h3>
                <p>
                    Informations sur l'authentification : utilisateur courant, rôles, token, mécanisme d'authentification,
                    décisions d'accès (voters). Indique si l'accès à la ressource a été autorisé ou refusé.
                </p>

                <h3 class="text-purple">Panel Twig</h3>
                <p>
                    Templates Twig rendus, temps de compilation et d'exécution, blocs, extensions utilisées.
                    Aide à optimiser les vues.
                </p>

                <h3 class="text-purple">Panel Performance (Stopwatch)</h3>
                <p>
                    Chronométrage détaillé : temps passé dans le noyau, dans les listeners, dans le contrôleur, dans Twig.
                    Idéal pour identifier les goulots d'étranglement.
                </p>

                <h3 class="text-purple">Panel Mailer</h3>
                <p>
                    Si vous utilisez le composant Mailer, ce panel montre les e-mails envoyés, leur contenu,
                    et permet de les prévisualiser sans réel envoi (en environnement dev).
                </p>
            </section>

            <!-- Profiler pour les API / JSON -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Profiler pour les API et requêtes AJAX</h2>
                <p class="textExemple">
                    Pour les réponses non HTML (JSON, XML) ou les appels AJAX, la barre d'outils ne s'affiche pas.
                    Cependant, les données de profilage sont tout de même collectées. Vous pouvez les consulter
                    via l'interface <code>/_profiler</code> ou en ajoutant un en-tête spécifique :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Pour inclure le profiler dans une réponse JSON
curl -H "X-Debug-Token: 123456" https://mon-site.com/api/posts</code></pre>
                </div>
                <p>
                    Le token de profilage est disponible dans l'en-tête de réponse <code>X-Debug-Token</code>.
                    Vous pouvez ainsi récupérer le lien vers la page de profilage correspondante.
                </p>
            </section>

            <!-- Collecte de données personnalisées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Ajouter vos propres données au Profiler</h2>
                <p class="textExemple">
                    Vous pouvez créer un <strong>Data Collector</strong> personnalisé pour ajouter des informations
                    spécifiques à votre application dans le profiler.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/DataCollector/MyCustomCollector.php
namespace App\DataCollector;

use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\HttpKernel\DataCollector\DataCollector;

class MyCustomCollector extends DataCollector
{
    public function collect(Request $request, Response $response, \Throwable $exception = null): void
    {
        // Collecter des données
        $this->data = [
            'custom_value' => 42,
            'user_agent' => $request->headers->get('User-Agent'),
        ];
    }

    public function getName(): string
    {
        return 'app.my_custom_collector';
    }

    public function reset(): void
    {
        $this->data = [];
    }

    // Getter pour accéder aux données dans le template
    public function getCustomValue(): int
    {
        return $this->data['custom_value'];
    }

    public function getUserAgent(): ?string
    {
        return $this->data['user_agent'];
    }
}</code></pre>
                </div>
                <p>Ensuite, enregistrez-le comme service avec le tag <code>data_collector</code> :</p>
                <div class="code-example">
                    <pre v-pre><code class="language-yaml"># config/services.yaml
services:
    App\DataCollector\MyCustomCollector:
        tags:
            - { name: data_collector, template: 'data_collector/my_custom_collector.html.twig', id: 'app.my_custom_collector' }</code></pre>
                </div>
            </section>

            <!-- Profiler en ligne de commande -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Profiler pour les commandes Console</h2>
                <p class="textExemple">
                    Le profiler peut également collecter des données lors de l'exécution de commandes Symfony.
                    Utilisez l'option <code>--profile</code> :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">php bin/console app:ma-commande --profile</code></pre>
                </div>
                <p>
                    Un token est généré et les données sont stockées. Vous pouvez les consulter via l'interface web
                    du profiler (l'URL est affichée dans la console). Utile pour déboguer des commandes longues.
                </p>
            </section>

            <!-- Gestion des tokens et purge -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des tokens et purge des données</h2>
                <p class="textExemple">
                    Chaque requête profilée génère un token unique. Les données sont stockées (par défaut dans le cache).
                    Pour éviter une accumulation excessive, Symfony limite la durée de conservation.
                </p>
                <p>Configuration dans <code>config/packages/dev/framework.yaml</code> :</p>
                <div class="code-example">
                    <pre v-pre><code class="language-yaml">framework:
    profiler:
        only_exceptions: false
        collect: true
        lifetime: 86400   # durée de vie en secondes (24h)</code></pre>
                </div>
                <p>Pour purger manuellement les profils :</p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">php bin/console profiler:clear</code></pre>
                </div>
            </section>

            <!-- Trucs et astuces -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Astuces d'utilisation</h2>
                <ul>
                    <li><strong>Forcer le profiler</strong> : ajoutez <code>?_profiler=true</code> à une URL pour activer le profiler même si la barre est désactivée (utile pour les réponses JSON).</li>
                    <li><strong>Intercepter les redirections</strong> : activez <code>intercept_redirects: true</code> dans <code>web_profiler.yaml</code> pour voir le profiler après une redirection.</li>
                    <li><strong>Chercher une requête</strong> : dans <code>/_profiler</code>, vous pouvez filtrer par méthode, IP, URL, statut, etc.</li>
                    <li><strong>Exporter un profil</strong> : chaque page de profilage a un bouton "Export" pour sauvegarder les données et les partager.</li>
                    <li><strong>Analyser les requêtes SQL lentes</strong> : le panel Doctrine trie par durée décroissante. Cliquez sur "Explain" pour voir le plan d'exécution.</li>
                </ul>
            </section>

            <!-- Problèmes courants -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Problèmes fréquents et solutions</h2>
                <div class="textExemple">
                    <h3 class="text-purple">La barre n'apparaît pas</h3>
                    <p>Vérifiez que :</p>
                    <ul>
                        <li>Vous êtes en environnement <code>dev</code> (ou <code>APP_ENV=dev</code>).</li>
                        <li>Le bundle <code>symfony/profiler-pack</code> est installé.</li>
                        <li>Le template de base inclut <code>&lt;/body&gt;</code> (la barre s'insère juste avant).</li>
                        <li>Pas de conflit avec un framework CSS qui cacherait la barre (z-index).</li>
                    </ul>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Erreur "Token not found"</h3>
                    <p>Le token a expiré ou a été purgé. Augmentez le <code>lifetime</code> ou purgez moins souvent.</p>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Le profiler ralentit l'application</h3>
                    <p>C'est normal en environnement de développement. Désactivez-le complètement en production.</p>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li><strong>Ne jamais activer le profiler en production</strong> (risque de fuite d'informations).</li>
                    <li><strong>Utilisez-le pour optimiser les requêtes SQL</strong> : repérez les N+1 queries.</li>
                    <li><strong>Surveillez le panel "Stopwatch"</strong> pour trouver les parties lentes de votre code.</li>
                    <li><strong>Créez des data collectors personnalisés</strong> pour des métriques spécifiques à votre domaine.</li>
                    <li><strong>En équipe, partagez un export de profil</strong> pour discuter d'un problème.</li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Le Symfony Profiler est un outil indispensable pour tout développeur Symfony. Il offre une visibilité
                    sans égale sur le fonctionnement interne de l'application et aide à diagnostiquer rapidement
                    les problèmes de performance, de logique ou de configuration.
                </p>
                <p class="textExemple">
                    Maîtriser le profiler permet de gagner un temps précieux en développement et d'optimiser
                    efficacement son code. Prenez le temps d'explorer chaque panel : vous y découvrirez toujours
                    des informations utiles.
                </p>
                <p class="textExemple">
                    Prochaines étapes : apprendre à utiliser le <strong>Stopwatch</strong> pour chronométrer des portions
                    de code personnalisées, ou créer des <strong>Data Collectors</strong> sur mesure pour des besoins avancés.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyProfilerLesson',

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
                    const languages = ['bash', 'yaml', 'php', 'sql'];
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
/* === Styles identiques aux leçons précédentes === */
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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
}

.warning-text {
    color: #d63031;
    font-weight: bold;
    margin-top: 0.5rem;
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