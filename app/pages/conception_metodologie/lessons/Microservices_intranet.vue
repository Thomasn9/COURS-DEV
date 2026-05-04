<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Microservices sécurisés sur intranet</h1>
                <p class="lesson-meta text-white">Architecture • API Gateway • mTLS • JWT • RBAC • Docker</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi une architecture microservices ?</h2>
                <p class="textExemple">
                    Dans un environnement intranet, les applications monolithiques deviennent difficilement maintenables 
                    et évolutives à mesure que l’organisation grandit. L’approche microservices permet de découper 
                    le système en petits services indépendants, chacun responsable d’un domaine métier spécifique.
                </p>
                <p class="textExemple">
                    Sur un intranet, la <strong>sécurité</strong> est primordiale : authentification unique (SSO), 
                    chiffrement des flux internes, isolation réseau et contrôle d’accès granulaire. Cette leçon présente 
                    une architecture de référence pour déployer des microservices robustes et sécurisés au sein d’un réseau 
                    interne d’entreprise.
                </p>
            </section>

            <!-- Architecture générale -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture de référence</h2>
                <div class="textExemple">
                    <p>Une architecture microservices typique sur intranet comprend les blocs suivants :</p>
                    <ul>
                        <li><strong>API Gateway</strong> – point d’entrée unique, reverse proxy, gestion des tokens.</li>
                        <li><strong>Service Discovery</strong> (Consul / etcd / Eureka) – localisation dynamique des services.</li>
                        <li><strong>Service de configuration</strong> – centralisation des secrets et paramètres.</li>
                        <li><strong>Service d’authentification</strong> (IAM) – délivre et valide les JWT, gère les identités.</li>
                        <li><strong>Services métier</strong> – chacun expose une API REST gRPC, avec son propre stockage.</li>
                        <li><strong>Observabilité</strong> – logs centralisés, métriques (Prometheus), tracing (Jaeger).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de flux sécurisé</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Client Intranet                API Gateway                Service Auth              Service Métier
     │                              │                           │                           │
     │ ───── POST /login (LDAP) ───→│                           │                           │
     │                              │ ──── vérification ───────→│                           │
     │                              │ ←───── JWT (signed) ──────│                           │
     │ ←───── JWT (cookie) ─────────│                           │                           │
     │                              │                           │                           │
     │ ─── GET /orders (JWT) ──────→│                           │                           │
     │                              │ ──── validate JWT ───────→│ (optionnel : introspection)│
     │                              │                           │                           │
     │                              │ ──── forward + JWT ───────────────────────────────────→│
     │                              │                           │                           │
     │ ←───────── orders JSON (mTLS)─────────────────────────────────────────────────────────│</code></pre>
                    </div>
                </div>
            </section>

            <!-- Composants clés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Composants clés de la sécurité intranet</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. API Gateway – point d’entrée et sécurité en périmètre</h3>
                    <p>L’API Gateway (NGINX, Traefik, Kong, Ocelot) joue un rôle central :</p>
                    <ul>
                        <li><strong>Terminaison TLS</strong> – déchiffrement mTLS pour services internes.</li>
                        <li><strong>Validation JWT</strong> – vérifie les tokens avant de router.</li>
                        <li><strong>Rate limiting & IP whitelisting</strong> – protège les services exposés.</li>
                        <li><strong>Transformation de requêtes</strong> – ajoute les en-têtes d’identité.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-nginx"># Extrait NGINX comme API Gateway avec validation JWT
server {
    listen 443 ssl;
    server_name api.intranet.local;

    ssl_certificate     /etc/nginx/certs/gateway.crt;
    ssl_certificate_key /etc/nginx/certs/gateway.key;
    ssl_client_certificate /etc/nginx/certs/ca.crt;
    ssl_verify_client on;               # mTLS obligatoire

    location /auth/ {
        proxy_pass http://auth-service:8080;
    }

    location /orders/ {
        # Vérification JWT avant routage
        auth_jwt "intranet" token=$cookie_jwt;
        auth_jwt_key_file /etc/nginx/jwt.pub;

        proxy_pass http://orders-service:3000;
        proxy_set_header X-User-Id $jwt_claim_sub;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. mTLS – chiffrement et authentification mutuelle</h3>
                    <p>
                        En intranet, le trafic entre services doit être chiffré et authentifié. 
                        <strong>mTLS</strong> (mutual TLS) garantit que seul un service possédant un certificat valide 
                        peut appeler un autre service. On utilise généralement une autorité de certification interne.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Génération de certificats pour un service (avec openssl)
openssl req -new -newkey rsa:4096 -days 365 -nodes -x509 \
    -subj "/CN=orders-service.intra" \
    -keyout orders.key -out orders.crt

# Signature par la CA interne
openssl x509 -req -in orders.csr -CA ca.crt -CAkey ca.key -out orders.crt</code></pre>
                    </div>
                    <p>Dans Docker Compose, on monte ces certificats et on configure le client HTTP (ex: Node.js avec <code>https.Agent</code>).</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Authentification centralisée – JWT & OAuth2</h3>
                    <p>
                        Un service IAM (Identity and Access Management) délivre des JWT après authentification 
                        (LDAP, Active Directory, base interne). Les services métier ne vérifient plus le mot de passe, 
                        seulement la signature et les claims du JWT.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Service d’authentification (Node.js + express) – génération JWT
const jwt = require('jsonwebtoken');

app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    // Vérification LDAP ou AD (simplifié)
    if (await authenticateIntranetUser(username, password)) {
        const token = jwt.sign(
            { sub: username, roles: ['employee', 'finance'] },
            process.env.JWT_PRIVATE_KEY,
            { algorithm: 'RS256', expiresIn: '8h' }
        );
        res.cookie('jwt', token, { httpOnly: true, secure: true, sameSite: 'strict' });
        res.json({ success: true });
    } else {
        res.status(401).json({ error: 'Invalid credentials' });
    }
});</code></pre>
                    </div>
                    <p>Validation du JWT dans un service métier (sans appel réseau externe) :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-python"># Service Orders (Python + Flask) – validation JWT locale
import jwt
from flask import request, jsonify

def verify_jwt(token):
    try:
        payload = jwt.decode(
            token, 
            open('public_key.pem').read(), 
            algorithms=['RS256'],
            audience='intranet'
        )
        return payload
    except jwt.InvalidTokenError:
        return None

@app.route('/api/orders')
def get_orders():
    token = request.cookies.get('jwt')
    user = verify_jwt(token)
    if not user or 'finance' not in user.get('roles', []):
        return jsonify({'error': 'Forbidden'}), 403
    orders = fetch_orders_for_user(user['sub'])
    return jsonify(orders)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Mise en œuvre concrète -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Mise en œuvre avec Docker Compose</h2>
                <div class="textExemple">
                    <p>Exemple de <code>docker-compose.yml</code> décrivant trois services : auth, orders, gateway (Traefik).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">version: '3.8'

services:
  auth-service:
    build: ./auth
    environment:
      - JWT_PRIVATE_KEY=/run/secrets/jwt_private
      - LDAP_SERVER=ldap.intra
    secrets:
      - jwt_private
    networks:
      - intra-net

  orders-service:
    build: ./orders
    environment:
      - JWT_PUBLIC_KEY=/run/secrets/jwt_public
    secrets:
      - jwt_public
    networks:
      - intra-net

  traefik:
    image: traefik:v2.10
    command:
      - "--providers.docker"
      - "--entrypoints.websecure.address=:443"
      - "--entrypoints.web.http.redirections.entrypoint.to=websecure"
      - "--serversTransport.insecureSkipVerify=true" # seulement pour démo
      - "--certificatesresolvers.intra.acme.tlsChallenge=true"
    ports:
      - "443:443"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
      - "./certs:/certs"
    networks:
      - intra-net

networks:
  intra-net:
    driver: overlay   # pour Swarm, isolation réseau

secrets:
  jwt_private:
    file: ./secrets/jwt-private.pem
  jwt_public:
    file: ./secrets/jwt-public.pem</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Communication inter-services sécurisée</h3>
                    <p>Chaque service doit appeler un autre service uniquement via HTTPS avec validation mTLS. On utilise des certificats spécifiques.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-go">// Exemple en Go : client HTTP avec mTLS
func callService(url string) (*http.Response, error) {
    caCert, _ := ioutil.ReadFile("/certs/ca.crt")
    caCertPool := x509.NewCertPool()
    caCertPool.AppendCertsFromPEM(caCert)

    cert, _ := tls.LoadX509KeyPair("/certs/client.crt", "/certs/client.key")
    tlsConfig := &tls.Config{
        Certificates: []tls.Certificate{cert},
        RootCAs:      caCertPool,
    }
    transport := &http.Transport{TLSClientConfig: tlsConfig}
    client := &http.Client{Transport: transport}
    return client.Get(url)
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Sécurité réseau et RBAC -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Sécurité réseau et contrôle d’accès (RBAC)</h2>
                <div class="textExemple">
                    <p>
                        Dans un intranet, on peut utiliser des <strong>network policies</strong> (Kubernetes) 
                        ou des <strong>overlay networks</strong> (Docker Swarm) pour isoler les services. 
                        Seul l’API Gateway et certains services autorisés communiquent entre eux.
                    </p>
                    <p>
                        Le <strong>RBAC</strong> (Role-Based Access Control) se met en œuvre via les claims JWT. 
                        Exemple de politique d’accès :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-json">{
  "roles": ["finance", "rh", "it"],
  "resources": {
    "/api/invoices": ["finance"],
    "/api/employees": ["rh"],
    "/api/servers": ["it"]
  }
}</code></pre>
                    </div>
                    <p>Middleware de vérification dans l’API Gateway :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-js">// Middleware Express dans l’API Gateway
function rbacMiddleware(allowedRoles) {
    return (req, res, next) => {
        const token = req.cookies.jwt;
        const decoded = jwt.verify(token, publicKey);
        const hasRole = allowedRoles.some(role => decoded.roles.includes(role));
        if (!hasRole) return res.status(403).send('Access Denied');
        next();
    };
}

app.get('/api/invoices', rbacMiddleware(['finance']), proxyToInvoices);
app.get('/api/employees', rbacMiddleware(['rh']), proxyToHR);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques & conclusion</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Sécurité par défaut</strong> : tous les services exigent mTLS et JWT ; pas de réseau ouvert.</li>
                        <li><strong>Rotation des secrets</strong> : utiliser Vault ou un gestionnaire de secrets (K8s secrets, Docker secrets).</li>
                        <li><strong>Journalisation centralisée</strong> : chaque service envoie ses logs (ELK, Loki) pour détecter les intrusions.</li>
                        <li><strong>Rate limiting et circuit breaker</strong> pour éviter les effets domino en cas d’attaque.</li>
                        <li><strong>Déploiement immuable</strong> : images Docker signées, scan de vulnérabilités.</li>
                    </ul>
                    <p>
                        L’architecture microservices sur intranet offre agilité et scalabilité, mais la sécurité doit être intégrée 
                        dès la conception. L’usage conjoint de mTLS, d’un API Gateway et de JWT permet d’obtenir un système 
                        robuste et adapté aux exigences internes.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous verrons comment orchestrer ces services avec Kubernetes, 
                        mettre en place un Service Mesh (Istio) et automatiser la délivrance des certificats via SPIRE.
                    </p>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>
                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Mise en place d’une Gateway avec NGINX et validation JWT</h3>
                    <p>À partir d’un fichier docker-compose simple (auth + echo service), configurez NGINX pour :</p>
                    <ul>
                        <li>Terminer le TLS (générer un certificat auto-signé).</li>
                        <li>Vérifier la présence d’un JWT valide dans l’en-tête <code>Authorization: Bearer</code>.</li>
                        <li>Rejeter les requêtes sans token valide.</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir un extrait de solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-nginx">server {
    listen 443 ssl;
    ssl_certificate /etc/nginx/certs/server.crt;
    ssl_certificate_key /etc/nginx/certs/server.key;

    location / {
        auth_jwt "MyApp" token=$http_authorization;
        auth_jwt_key_file /etc/nginx/jwt.pub;
        proxy_pass http://echo-service:3000;
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Implémenter un middleware JWT en Python ou Node.js</h3>
                    <p>Créez un service métier fictif qui lit le JWT (clé publique) et n’autorise que les utilisateurs ayant le rôle <code>admin</code>. Renvoyez une erreur 403 sinon.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution (Node.js)</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-javascript">const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();

const publicKey = `-----BEGIN PUBLIC KEY-----
...
-----END PUBLIC KEY-----`;

const requireAdmin = (req, res, next) => {
    const token = req.headers.authorization?.split(' ')[1];
    if (!token) return res.status(401).json({error: 'Missing token'});
    try {
        const decoded = jwt.verify(token, publicKey, {algorithms: ['RS256']});
        if (!decoded.roles || !decoded.roles.includes('admin')) {
            return res.status(403).json({error: 'Admin role required'});
        }
        req.user = decoded;
        next();
    } catch(e) {
        res.status(401).json({error: 'Invalid token'});
    }
};

app.get('/admin-only', requireAdmin, (req, res) => {
    res.json({message: `Welcome admin ${req.user.sub}`});
});

app.listen(3000);</code></pre>
                        </div>
                    </details>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MicroservicesSecurityLesson',

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
                    const languages = ['nginx', 'yaml', 'javascript', 'python', 'go', 'json', 'bash'];
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
/* === Copie exacte du style de la leçon Symfony === */
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

.code-example {
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

.success-text {
    color: #00b894;
    font-weight: bold;
    margin-top: 0.5rem;
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
    .code-comparison   { grid-template-columns: 1fr; gap: 1rem; }
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