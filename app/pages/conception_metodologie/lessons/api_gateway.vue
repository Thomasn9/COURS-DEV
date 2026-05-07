<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">API Gateway : rôle et utilité</h1>
                <p class="lesson-meta text-white">Architecture • Reverse proxy • Centralisation • Sécurité • Microservices</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'une API Gateway ?</h2>
                <p class="textExemple">
                    Une <strong>API Gateway</strong> est un composant logiciel qui se place entre les clients (applications web, mobiles, services tiers) et l'ensemble des services d'un backend. Elle agit comme un <strong>point d'entrée unique</strong>.
                </p>
                <p class="textExemple">
                    Imaginez un immeuble avec une réception centrale : tous les visiteurs passent par l'accueil avant d'être orientés vers le bon service. L'API Gateway joue exactement ce rôle dans une architecture logicielle.
                </p>
            </section>

            <!-- Problème sans API Gateway -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi en a-t-on besoin ? (Le problème)</h2>
                <div class="textExemple">
                    <p>Dans une architecture microservices classique, sans API Gateway, chaque client doit :</p>
                    <ul>
                        <li>Connaître l'adresse (IP/port) de chaque service métier.</li>
                        <li>Gérer l'authentification et l'autorisation pour chaque service.</li>
                        <li>Implémenter la logique de récupération des tokens, la limitation de débit, etc.</li>
                        <li>Appeler plusieurs services séparément pour assembler une page complexe (ex: dashboard).</li>
                    </ul>
                    <p>Cela conduit à :</p>
                    <ul>
                        <li>Une forte dépendance des clients à l'infrastructure interne.</li>
                        <li>Une duplication de code (sécurité, rate limiting, logs).</li>
                        <li>Des difficultés à faire évoluer l'architecture (changer un endpoint oblige à mettre à jour tous les clients).</li>
                        <li>Une exposition dangereuse des services backend directement sur le réseau.</li>
                    </ul>
                </div>
            </section>

            <!-- Solution : API Gateway -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">La solution : une API Gateway</h2>
                <p class="textExemple">
                    L'API Gateway s'interpose et devient l'unique point de contact. Toutes les requêtes des clients passent par elle, qui se charge de :
                </p>
                <ul>
                    <li><strong>Router</strong> chaque requête vers le bon service (ex: <code>/users/*</code> → User Service, <code>/orders/*</code> → Order Service).</li>
                    <li><strong>Authentifier et autoriser</strong> (validation JWT, vérification des rôles).</li>
                    <li><strong>Limiter le débit</strong> (rate limiting) pour éviter les abus.</li>
                    <li><strong>Agréger</strong> les réponses de plusieurs services en un seul appel (pattern <em>API Composition</em>).</li>
                    <li><strong>Transformer</strong> les protocoles (REST ↔ gRPC, SOAP ↔ JSON).</li>
                    <li><strong>Collecter</strong> des métriques et logs centralisés.</li>
                </ul>
            </section>

            <!-- Schéma de fonctionnement -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Schéma de fonctionnement</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-plaintext">Client mobile / web / partenaire
         │
         ▼
   ┌─────────────┐
   │ API Gateway │  ← point d'entrée unique
   └─────────────┘
         │
         ├──────► Service Utilisateurs (port 3001)
         ├──────► Service Commandes   (port 3002)
         └──────► Service Paiements   (port 3003)

Avantages :
• Les clients ne connaissent qu'une URL (ex: https://api.intranet.local)
• La Gateway gère la sécurité centralisée
• Les services restent isolés et ne sont pas exposés directement</code></pre>
                </div>
            </section>

            <!-- Cas d'usage concrets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilité concrète – exemples</h2>
                <div class="textExemple">
                    <h3 class="text-purple">1. Authentification unique (SSO)</h3>
                    <p>La Gateway valide le token JWT une fois pour toutes. Les services backend n'ont pas à vérifier le token, ils reçoivent simplement les informations de l'utilisateur (X-User-Id, X-Roles).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-nginx"># Extrait NGINX : validation JWT avant routage
location /api/ {
    auth_jwt "API" token=$http_authorization;
    auth_jwt_key_file /etc/nginx/jwt.pub;
    proxy_set_header X-User-Id $jwt_claim_sub;
    proxy_set_header X-Roles $jwt_claim_roles;
    proxy_pass http://backend;
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">2. Agrégation de données (dashboard)</h3>
                    <p>Une page d'accueil d'application affiche les profils, commandes récentes et notifications. Sans Gateway, le client ferait 3 appels distincts. Avec Gateway, un seul appel <code>/dashboard</code> déclenche les appels parallèles en interne.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Exemple dans l'API Gateway (Node.js)
app.get('/dashboard', async (req, res) => {
    const [profile, orders, notifs] = await Promise.all([
        fetch('http://user-svc/users/me'),
        fetch('http://order-svc/orders?limit=5'),
        fetch('http://notif-svc/unread')
    ]);
    res.json({
        profile: await profile.json(),
        orders: await orders.json(),
        notifications: await notifs.json()
    });
});</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">3. Rate limiting (protection contre les abus)</h3>
                    <p>Limiter à 100 requêtes par minute par utilisateur pour éviter les attaques DoD ou les surcharges accidentelles.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># Configuration Kong Gateway
plugins:
- name: rate-limiting
  service: my-service
  config:
    minute: 100
    policy: local</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bénéfices clés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bénéfices clés pour une architecture interne</h2>
                <ul>
                    <li><strong>Sécurité renforcée</strong> : TLS/mTLS terminé à la Gateway, règles d'IP whitelisting, injection des en-têtes d'identité.</li>
                    <li><strong>Simplicité pour les clients</strong> : une seule URL, une seule politique de sécurité à intégrer.</li>
                    <li><strong>Découplage</strong> : on peut changer l'emplacement d'un service sans impacter les clients (la Gateway modifie sa configuration).</li>
                    <li><strong>Observabilité centralisée</strong> : tous les logs, métriques et traces passent par la Gateway.</li>
                    <li><strong>Transition facilitée</strong> : on peut router progressivement du trafic d'un ancien système vers un nouveau (blue/green, canary).</li>
                    <li><strong>Réduction de la charge des services</strong> : la Gateway gère la terminaison SSL, la compression, la mise en cache.</li>
                </ul>
            </section>

            <!-- Solutions existantes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Quelles solutions utiliser ?</h2>
                <div class="textExemple">
                    <p>Il existe de nombreuses implémentations, libres ou propriétaires :</p>
                    <ul>
                        <li><strong>Traefik</strong> – très simple avec Docker/Kubernetes, intégration Let's Encrypt.</li>
                        <li><strong>NGINX / NGINX Plus</strong> – haute performance, configuration flexible.</li>
                        <li><strong>Kong Gateway</strong> – riche écosystème de plugins (authentification, logs, transformation).</li>
                        <li><strong>Apache APISIX</strong> – dynamique, support gRPC, dashboard.</li>
                        <li><strong>Envoy + Gloo</strong> – souvent utilisé comme maillage de services.</li>
                        <li><strong>Spring Cloud Gateway</strong> – pour environnements Java.</li>
                        <li><strong>Ocelot</strong> – pour .NET.</li>
                    </ul>
                    <p>Pour un intranet avec Docker, Traefik ou NGINX sont d'excellents choix.</p>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Exemple Docker Compose avec Traefik</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">version: '3'
services:
  traefik:
    image: traefik:v2.10
    command:
      - "--providers.docker=true"
      - "--entrypoints.web.address=:80"
    ports:
      - "80:80"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"

  users-api:
    image: myapp/users
    labels:
      - "traefik.http.routers.users.rule=PathPrefix(`/users`)"
      - "traefik.http.services.users.loadbalancer.server.port=3000"

  orders-api:
    image: myapp/orders
    labels:
      - "traefik.http.routers.orders.rule=PathPrefix(`/orders`)"
      - "traefik.http.services.orders.loadbalancer.server.port=8080"</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li><strong>Gardez la Gateway sans logique métier</strong> – elle ne doit que router et appliquer des politiques transverses.</li>
                    <li><strong>Déployez plusieurs instances</strong> pour la haute disponibilité (utilisez un load balancer en amont).</li>
                    <li><strong>Utilisez des timeout et retries</strong> pour protéger les clients de l'indisponibilité d'un service.</li>
                    <li><strong>Activez les health checks</strong> pour ne pas router vers un service défaillant.</li>
                    <li><strong>Centralisez la configuration</strong> (git + rechargement dynamique) pour faciliter les mises à jour.</li>
                    <li><strong>Surveillez la Gateway elle-même</strong> (latence, taux d'erreur) – elle peut devenir un goulot d'étranglement.</li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        L'API Gateway est un élément <strong>fondamental</strong> dans toute architecture moderne orientée services (microservices, serverless). Elle apporte :
                    </p>
                    <ul>
                        <li>Un point d'entrée unique, simple et sécurisé.</li>
                        <li>Une réduction de la complexité pour les clients.</li>
                        <li>Une centralisation des préoccupations transverses (sécurité, observabilité, limitation).</li>
                        <li>Un découplage qui facilite l'évolution du backend.</li>
                    </ul>
                    <p>
                        Sans API Gateway, on se retrouve rapidement avec une architecture "point-à-point" difficile à maintenir et à sécuriser. Dans un contexte intranet, l'API Gateway est souvent la première brique à poser avant de passer aux microservices.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous verrons comment coupler l'API Gateway avec un Service Mesh (comme Istio) pour un contrôle plus fin des communications entre services.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'ApiGatewayUtilityLesson',

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
                    const languages = ['nginx', 'yaml', 'javascript', 'plaintext'];
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
/* Styles identiques à la leçon Symfony – copie exacte */
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