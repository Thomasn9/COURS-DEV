<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Le fichier security.yaml dans Symfony</h1>
                <p class="lesson-meta text-white">Symfony • Security • Configuration • Firewalls • Access Control</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à security.yaml</h2>
                <p class="textExemple">
                    Le fichier <code>config/packages/security.yaml</code> est le cœur de la sécurité dans Symfony.
                    Il définit comment les utilisateurs sont authentifiés, comment leurs mots de passe sont hachés,
                    quelles parties de l'application sont protégées, et comment les accès sont contrôlés.
                </p>
                <p class="textExemple">
                    Ce fichier est automatiquement créé avec le bundle Security. Sa maîtrise est essentielle pour
                    construire des applications sécurisées et gérer finement les permissions.
                </p>
            </section>

            <!-- Structure générale -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure générale du fichier</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/security.yaml
security:
    # Configuration des hashages de mots de passe
    password_hashers:
        App\Entity\User: 'auto'

    # Définition des sources d'utilisateurs
    providers:
        app_user_provider:
            entity:
                class: App\Entity\User
                property: email

    # Règles de pare-feu (firewalls)
    firewalls:
        dev:
            pattern: ^/(_(profiler|wdt)|css|images|js)/
            security: false
        main:
            lazy: true
            provider: app_user_provider
            custom_authenticator: App\Security\LoginFormAuthenticator
            logout:
                path: app_logout
                target: app_login

    # Contrôle d'accès (URLs protégées)
    access_control:
        - { path: ^/login, roles: PUBLIC_ACCESS }
        - { path: ^/admin, roles: ROLE_ADMIN }
        - { path: ^/profile, roles: ROLE_USER }

    # Rôles hiérarchiques (optionnel)
    role_hierarchy:
        ROLE_ADMIN: ROLE_USER
        ROLE_SUPER_ADMIN: [ROLE_ADMIN, ROLE_ALLOWED_TO_SWITCH]</code></pre>
                    </div>
                </div>
            </section>

            <!-- password_hashers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">password_hashers : Hachage des mots de passe</h2>

                <div class="textExemple">
                    <p>La section <code>password_hashers</code> définit l'algorithme utilisé pour hacher les mots de passe de chaque classe d'utilisateur.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">password_hashers:
    # Hachage automatique (bcrypt ou argon2i selon disponibilité)
    App\Entity\User: 'auto'

    # Hachage avec configuration personnalisée
    App\Entity\Admin:
        algorithm: 'auto'
        cost: 12          # Pour bcrypt (4-31)
        memory_cost: 1<<17 # Pour argon2i
        time_cost: 4       # Pour argon2i

    # Utiliser un hasher différent pour plusieurs classes
    App\Entity\LegacyUser:
        algorithm: 'sha256'
        encode_as_base64: false
        iterations: 5000

    # Hasher global par défaut (si classe non spécifiée)
    Symfony\Component\Security\Core\User\PasswordAuthenticatedUserInterface: 'auto'</code></pre>
                    </div>
                    <p><strong>Algorithmes disponibles :</strong> <code>auto</code>, <code>bcrypt</code>, <code>argon2i</code>, <code>argon2id</code>, <code>native</code>, <code>sodium</code>.</p>
                </div>
            </section>

            <!-- providers -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">providers : Sources d'utilisateurs</h2>

                <div class="textExemple">
                    <p>Les providers indiquent à Symfony où trouver les utilisateurs (base de données, mémoire, LDAP, etc.).</p>

                    <h3 class="text-purple">Provider Doctrine (entité)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">providers:
    users_db:
        entity:
            class: App\Entity\User
            property: email   # champ utilisé pour l'authentification
            # manager_name: 'default' # si plusieurs entity managers</code></pre>
                    </div>

                    <h3 class="text-purple">Provider mémoire (pour tests)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">providers:
    in_memory:
        memory:
            users:
                admin:
                    password: '$2y$13$...'  # mot de passe haché
                    roles: ['ROLE_ADMIN']
                user:
                    password: 'hashed_password'
                    roles: ['ROLE_USER']</code></pre>
                    </div>

                    <h3 class="text-purple">Provider chaîné (plusieurs sources)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">providers:
    chain_provider:
        chain:
            providers: ['users_db', 'in_memory']</code></pre>
                    </div>

                    <h3 class="text-purple">Provider personnalisé (service)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">providers:
    custom:
        id: App\Security\CustomUserProvider</code></pre>
                    </div>
                </div>
            </section>

            <!-- firewalls -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">firewalls : Les pare-feu</h2>

                <div class="textExemple">
                    <p>
                        Chaque requête entre dans un firewall. Le premier dont le <code>pattern</code> correspond est utilisé.
                        Le firewall <code>dev</code> est préconfiguré pour désactiver la sécurité sur les profiler et assets.
                    </p>

                    <h3 class="text-purple">Firewall principal (main)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">firewalls:
    main:
        # Rend le firewall actif pour toutes les URLs (pattern par défaut: ^/)
        lazy: true
        provider: users_db

        # Authentification par formulaire (ancienne méthode, dépréciée)
        form_login:
            login_path: login
            check_path: login
            default_target_path: home

        # Ou authentificateur personnalisé (recommandé)
        custom_authenticator: App\Security\LoginFormAuthenticator

        # Gestion de la déconnexion
        logout:
            path: app_logout
            target: app_login
            invalidate_session: true

        # "Se souvenir de moi"
        remember_me:
            secret: '%kernel.secret%'
            lifetime: 604800   # 1 semaine
            path: /
            always_remember_me: true

        # Connexion via JSON (API)
        json_login:
            check_path: api_login
            username_path: email
            password_path: password

        # Authentification HTTP basic
        http_basic:
            realm: 'Secured Area'

        # Activation du contexte (partage de session entre firewalls)
        context: primary_context

        # Limitation des tentatives de connexion (Symfony 6.2+)
        login_throttling:
            max_attempts: 5
            interval: '15 minutes'

        # Two-factor authentication (nécessite bundle)
        two_factor:
            auth_form_path: 2fa_login
            check_path: 2fa_login_check

        # Accès anonyme (ROLE_PUBLIC_ACCESS)
        security: true   # false pour désactiver complètement la sécurité</code></pre>
                    </div>

                    <h3 class="text-purple">Plusieurs firewalls (ex: API + interface web)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">firewalls:
    api:
        pattern: ^/api
        stateless: true
        json_login:
            check_path: /api/login
    main:
        lazy: true
        provider: users_db
        form_login:
            login_path: login
            check_path: login</code></pre>
                    </div>
                </div>
            </section>

            <!-- access_control -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">access_control : Contrôle d'accès par URL</h2>

                <div class="textExemple">
                    <p>
                        La section <code>access_control</code> définit des règles d'accès basées sur l'URL, la méthode HTTP,
                        l'IP, ou l'hôte. Les règles sont évaluées dans l'ordre, la première correspondante est appliquée.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">access_control:
    # Accès public à la page de login
    - { path: ^/login, roles: PUBLIC_ACCESS }

    # Zone admin réservée aux ROLE_ADMIN
    - { path: ^/admin, roles: ROLE_ADMIN }

    # Profil utilisateur : ROLE_USER ou mieux
    - { path: ^/profile, roles: ROLE_USER }

    # API publique en lecture, authentification requise pour écriture
    - { path: ^/api/posts, methods: [GET], roles: PUBLIC_ACCESS }
    - { path: ^/api/posts, roles: ROLE_USER }

    # Restriction par IP
    - { path: ^/internal, roles: PUBLIC_ACCESS, ips: [127.0.0.1, ::1] }
    - { path: ^/internal, roles: ROLE_ADMIN }  # autre IP → admin

    # Correspondance par hôte
    - { path: ^/secure, host: admin\.example\.com, roles: ROLE_ADMIN }

    # Exiger HTTPS
    - { path: ^/checkout, requires_channel: https }

    # Utiliser un service personnalisé (voter)
    - { path: ^/documents, allow_if: "'ROLE_USER' in roles and user.isVerified()" }

    # Désactiver l'accès (renvoie 404)
    - { path: ^/secret, roles: ROLE_NO_ACCESS }</code></pre>
                    </div>
                    <p><strong>Rôles spéciaux :</strong></p>
                    <ul>
                        <li><code>PUBLIC_ACCESS</code> : accès public (même non authentifié)</li>
                        <li><code>IS_AUTHENTICATED_FULLY</code> : utilisateur authentifié (pas de remember me)</li>
                        <li><code>IS_AUTHENTICATED_REMEMBERED</code> : authentifié ou remember me</li>
                        <li><code>IS_AUTHENTICATED_ANONYMOUSLY</code> : utilisateur anonyme</li>
                        <li><code>ROLE_ALLOWED_TO_SWITCH</code> : peut utiliser le switch user</li>
                        <li><code>ROLE_PREVIOUS_ADMIN</code> : utilisé lors du switch user</li>
                    </ul>
                </div>
            </section>

            <!-- role_hierarchy -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">role_hierarchy : Hiérarchie des rôles</h2>

                <div class="textExemple">
                    <p>
                        La hiérarchie permet d'hériter des rôles. Un rôle peut inclure d'autres rôles,
                        simplifiant la gestion des permissions.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">role_hierarchy:
    ROLE_MODERATOR: ROLE_USER
    ROLE_ADMIN: [ROLE_USER, ROLE_MODERATOR]
    ROLE_SUPER_ADMIN: [ROLE_ADMIN, ROLE_ALLOWED_TO_SWITCH]</code></pre>
                    </div>
                    <p>
                        Avec cette configuration, un utilisateur avec <code>ROLE_ADMIN</code> possède automatiquement
                        <code>ROLE_USER</code> et <code>ROLE_MODERATOR</code>.
                    </p>
                </div>
            </section>

            <!-- Access Decision Manager -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Access Decision Manager (ADM)</h2>

                <div class="textExemple">
                    <p>L'ADM décide si un utilisateur a accès à une ressource selon une stratégie.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">access_decision_manager:
    # 'affirmative' : un seul vote positif suffit
    # 'consensus'   : majorité (positif vs négatif)
    # 'unanimous'   : tous les votes positifs (défaut)
    strategy: unanimous
    allow_if_all_abstain: false   # Si tous s'abstiennent, refuser
    allow_if_equal_granted_denied: false</code></pre>
                    </div>
                </div>
            </section>

            <!-- Authenticators multiples -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Authenticators multiples (chaînage)</h2>

                <div class="textExemple">
                    <p>
                        Un firewall peut utiliser plusieurs authenticators qui sont essayés tour à tour.
                        Utile pour accepter à la fois un formulaire et un token JWT.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">firewalls:
    main:
        custom_authenticators:
            - App\Security\JwtAuthenticator
            - App\Security\LoginFormAuthenticator
        entry_point: App\Security\JwtAuthenticator  # authenticator par défaut</code></pre>
                    </div>
                </div>
            </section>

            <!-- Switch User (impersonnation) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Switch User : Devenir un autre utilisateur</h2>

                <div class="textExemple">
                    <p>Fonctionnalité permettant à un admin de se connecter en tant qu'un autre utilisateur (debug).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">firewalls:
    main:
        switch_user:
            provider: users_db
            role: ROLE_ALLOWED_TO_SWITCH
            parameter: _switch_user   # paramètre GET</code></pre>
                    </div>
                    <p>Pour l'utiliser : <code>/some-url?_switch_user=email@example.com</code>.</p>
                    <p>Pour revenir : <code>/some-url?_switch_user=_exit</code>.</p>
                </div>
            </section>

            <!-- Configuration avancée -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Configuration avancée</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Gestion des sessions</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">firewalls:
    main:
        session:
            name: MYSESSIONID
            cookie_secure: true
            cookie_httponly: true
            cookie_samesite: lax
            gc_maxlifetime: 3600</code></pre>
                    </div>

                    <h3 class="text-purple">Désactiver la sécurité pour certaines routes</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">firewalls:
    main:
        pattern: ^/
        security: true
        # Pour exclure des routes, utilisez access_control avec PUBLIC_ACCESS</code></pre>
                    </div>

                    <h3 class="text-purple">Utiliser des expressions (allow_if)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">access_control:
    - { path: ^/document/.*, allow_if: "'ROLE_ADMIN' in roles or user and user.getDepartment() == 'sales'" }</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques de sécurité</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Utilisez <code>auto</code> pour password_hashers</strong> : Symfony choisit l'algorithme le plus sécurisé disponible.</li>
                        <li><strong>Protégez toujours <code>/admin</code> et <code>/profile</code></strong> avec des rôles explicites.</li>
                        <li><strong>Activez <code>login_throttling</code></strong> pour limiter les attaques par brute force.</li>
                        <li><strong>En production, forcez HTTPS</strong> via <code>requires_channel: https</code> ou via serveur web.</li>
                        <li><strong>Ne laissez jamais de firewall sans authentification</strong> sauf pour <code>dev</code> et les assets publics.</li>
                        <li><strong>Utilisez <code>PUBLIC_ACCESS</code> plutôt que <code>IS_AUTHENTICATED_ANONYMOUSLY</code></strong> (plus clair).</li>
                        <li><strong>Stockez le secret (kernel.secret) dans .env</strong>, ne le versionnez pas.</li>
                        <li><strong>Testez toujours vos règles d'accès</strong> avec des tests fonctionnels.</li>
                    </ul>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Configurer une zone admin</h3>
                    <p>
                        Ajoutez un firewall pour l'API (<code>/api</code>) sans état (stateless) avec authentification JSON,
                        et un firewall web classique. Protégez l'administration (<code>/admin</code>) avec <code>ROLE_ADMIN</code>.
                    </p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-yaml">security:
    firewalls:
        api:
            pattern: ^/api
            stateless: true
            json_login:
                check_path: /api/login
        main:
            lazy: true
            provider: users_db
            form_login:
                login_path: login
                check_path: login
            logout: ~
    access_control:
        - { path: ^/admin, roles: ROLE_ADMIN }
        - { path: ^/api, roles: IS_AUTHENTICATED_FULLY }</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Hiérarchie des rôles et accès conditionnel</h3>
                    <p>
                        Créez une hiérarchie où <code>ROLE_EDITOR</code> hérite de <code>ROLE_USER</code>, et <code>ROLE_ADMIN</code>
                        hérite de <code>ROLE_EDITOR</code>. Protégez <code>/blog/edit</code> pour les éditeurs et <code>/blog/publish</code>
                        pour les admins.
                    </p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-yaml">role_hierarchy:
    ROLE_EDITOR: ROLE_USER
    ROLE_ADMIN: ROLE_EDITOR

access_control:
    - { path: ^/blog/edit, roles: ROLE_EDITOR }
    - { path: ^/blog/publish, roles: ROLE_ADMIN }</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Sécuriser une API avec token JWT</h3>
                    <p>
                        Configurez un firewall <code>api</code> stateless avec un authenticator JWT personnalisé.
                        (On suppose que l'authenticator existe déjà).
                    </p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-yaml">firewalls:
    api:
        pattern: ^/api
        stateless: true
        custom_authenticator: App\Security\JwtAuthenticator
        provider: users_db
access_control:
    - { path: ^/api/login, roles: PUBLIC_ACCESS }
    - { path: ^/api, roles: IS_AUTHENTICATED_FULLY }</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Debug et vérification -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Vérifier et déboguer la configuration</h2>

                <div class="textExemple">
                    <p>Commandes utiles pour analyser votre configuration de sécurité :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Afficher la configuration effective (après fusion)
php bin/console debug:config security

# Vérifier les règles d'accès pour une URL
php bin/console security:check:access /admin

# Lister les rôles disponibles
php bin/console debug:autowiring --tag=security.voter

# Afficher les firewalls et leur pattern
php bin/console debug:firewall

# Tester l'encodage d'un mot de passe
php bin/console security:hash-password 'monMotDePasse'</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Le fichier <code>security.yaml</code> est la clé de voûte de la sécurité dans Symfony.
                        Une bonne compréhension de ses sections permet de construire des applications robustes,
                        que ce soit pour un site web classique ou une API moderne.
                    </p>
                    <ul>
                        <li><strong>password_hashers</strong> : sécurisez les mots de passe.</li>
                        <li><strong>providers</strong> : définissez où chercher les utilisateurs.</li>
                        <li><strong>firewalls</strong> : isolez et protégez les zones de l'application.</li>
                        <li><strong>access_control</strong> : contrôlez finement l'accès aux URLs.</li>
                        <li><strong>role_hierarchy</strong> : simplifiez la gestion des permissions.</li>
                    </ul>
                    <p>
                        Prochaines leçons : les Voters (système d'autorisation avancé), l'intégration de LDAP,
                        et la mise en place de l'authentification multi-facteurs (2FA).
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonySecurityYamlLesson',

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
                    const languages = ['bash', 'yaml'];
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
/* === STYLES IDENTIQUES AUX LEÇONS PRÉCÉDENTES === */
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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
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