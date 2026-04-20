<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Authentification Symfony avec make:auth</h1>
                <p class="lesson-meta text-white">Symfony • Security • make:auth • Authenticator • Login</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à make:auth</h2>
                <p class="textExemple">
                    La commande <code>make:auth</code> du MakerBundle génère automatiquement tout le système d'authentification
                    de Symfony : formulaire de connexion, entité User, authentificateur, contrôleur, templates et configuration.
                </p>
                <p class="textExemple">
                    Elle implémente le <strong>Authenticator system</strong> de Symfony (Security component 5.4+), une approche moderne
                    et flexible qui remplace l'ancien système basé sur des providers et listeners.
                </p>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis et installation</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Installer les bundles nécessaires</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># MakerBundle (pour la génération de code)
composer require symfony/maker-bundle --dev

# Security pack (inclut security-core, password-hasher, etc.)
composer require symfony/security-bundle

# Twig pour les templates (si pas déjà fait)
composer require symfony/twig-bundle

# Optionnel : pour la gestion des formulaires de login
composer require symfony/form</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Vérifier la configuration de security.yaml</h3>
                    <p>Le fichier <code>config/packages/security.yaml</code> doit exister. Sinon, créez-le :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console debug:config security</code></pre>
                    </div>
                </div>
            </section>

            <!-- Lancer make:auth -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Générer l'authentification</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Commande interactive</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:auth</code></pre>
                    </div>
                    <p>Le générateur propose deux choix :</p>
                    <ul>
                        <li><strong>Empty authenticator</strong> : squelette minimal, idéal pour une API ou une authentification personnalisée.</li>
                        <li><strong>Login form authenticator</strong> : génère un formulaire de connexion complet (recommandé pour les applications web classiques).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Déroulement typique (formulaire de connexion)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-text">$ php bin/console make:auth

 What style of authentication do you want? (Empty authenticator, Login form authenticator)
 > Login form authenticator

 The class name of the authenticator to create (e.g. AppLoginFormAuthenticator):
 > AppLoginFormAuthenticator

 Choose a name for the login route (e.g. app_login):
 > app_login

 Do you want to generate a '/logout' route? (yes/no) [yes]:
 > yes

 Do you want to generate an entity class to store user data? (yes/no) [yes]:
 > yes

 Enter the class name of the user entity (e.g. User):
 > User

 Do you want to persist user data via Doctrine? (yes/no) [yes]:
 > yes</code></pre>
                    </div>
                </div>
            </section>

            <!-- Fichiers générés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fichiers générés par make:auth</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>src/Security/AppLoginFormAuthenticator.php</strong> – La logique d'authentification</li>
                        <li><strong>src/Controller/SecurityController.php</strong> – Contrôleur pour login/logout</li>
                        <li><strong>templates/security/login.html.twig</strong> – Formulaire de connexion</li>
                        <li><strong>src/Entity/User.php</strong> (si absent) – Entité utilisateur avec champs email, password, roles</li>
                        <li><strong>src/Repository/UserRepository.php</strong> – Repository Doctrine</li>
                        <li><strong>config/routes/security.yaml</strong> – Route de déconnexion (si demandée)</li>
                        <li><strong>config/packages/security.yaml</strong> – Configuration mise à jour (providers, encoders, firewalls, access_control)</li>
                    </ul>
                </div>
            </section>

            <!-- Explication de l'authenticator -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comprendre l'Authenticator</h2>

                <div class="textExemple">
                    <p>La classe générée <code>AppLoginFormAuthenticator</code> implémente l'interface <code>AuthenticatorInterface</code>. Voici ses méthodes clés :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Security/AppLoginFormAuthenticator.php
class AppLoginFormAuthenticator extends AbstractLoginFormAuthenticator
{
    // Route du formulaire de login
    public const LOGIN_ROUTE = 'app_login';

    // 1. Indique si la requête doit être interceptée
    public function supports(Request $request): bool
    {
        return self::LOGIN_ROUTE === $request->attributes->get('_route')
            && $request->isMethod('POST');
    }

    // 2. Extrait les identifiants de la requête
    public function authenticate(Request $request): Passport
    {
        $email = $request->request->get('email', '');
        $password = $request->request->get('password', '');

        return new Passport(
            new UserBadge($email),
            new PasswordCredentials($password),
            [new CsrfTokenBadge('authenticate', $request->request->get('_csrf_token'))]
        );
    }

    // 3. En cas de succès : redirection
    public function onAuthenticationSuccess(Request $request, TokenInterface $token, string $firewallName): ?Response
    {
        return new RedirectResponse($this->urlGenerator->generate('app_home'));
    }

    // 4. En cas d'échec : message d'erreur
    protected function getLoginUrl(Request $request): string
    {
        return $this->urlGenerator->generate(self::LOGIN_ROUTE);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Fonctionnement pas à pas</h3>
                    <ol>
                        <li><code>supports()</code> : vérifie que la requête est bien un POST sur la route <code>app_login</code>.</li>
                        <li><code>authenticate()</code> : construit un <code>Passport</code> avec l'email (UserBadge), le mot de passe et un token CSRF.</li>
                        <li>Symfony charge l'utilisateur via <code>UserProvider</code>, vérifie le mot de passe (auto).</li>
                        <li><code>onAuthenticationSuccess()</code> : redirige après connexion réussie.</li>
                        <li>En cas d'erreur, le système affiche le formulaire avec un message d'erreur (via <code>getLoginUrl()</code>).</li>
                    </ol>
                </div>
            </section>

            <!-- Entité User et sécurité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Entité User et encodage des mots de passe</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Structure de l'entité User générée</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/User.php
use Symfony\Component\Security\Core\User\PasswordAuthenticatedUserInterface;
use Symfony\Component\Security\Core\User\UserInterface;

#[ORM\Entity(repositoryClass: UserRepository::class)]
class User implements UserInterface, PasswordAuthenticatedUserInterface
{
    #[ORM\Id, ORM\GeneratedValue, ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 180, unique: true)]
    private ?string $email = null;

    #[ORM\Column]
    private array $roles = [];

    #[ORM\Column]
    private ?string $password = null;

    // Getters / setters...

    public function getPassword(): ?string
    {
        return $this->password;
    }

    public function getRoles(): array
    {
        $roles = $this->roles;
        $roles[] = 'ROLE_USER'; // garantit au moins un rôle
        return array_unique($roles);
    }

    // ...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configuration de l'encodage (security.yaml)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/security.yaml
security:
    password_hashers:
        App\Entity\User: 'auto'  # Symfony choisit bcrypt ou argon2i

    providers:
        app_user_provider:
            entity:
                class: App\Entity\User
                property: email   # champ utilisé pour l'authentification

    firewalls:
        main:
            lazy: true
            provider: app_user_provider
            custom_authenticator: App\Security\AppLoginFormAuthenticator
            logout:
                path: app_logout
                target: app_login

    access_control:
        - { path: ^/login, roles: PUBLIC_ACCESS }
        - { path: ^/admin, roles: ROLE_ADMIN }
        - { path: ^/profile, roles: ROLE_USER }</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Hacher un mot de passe (inscription)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un contrôleur d'inscription
use Symfony\Component\PasswordHasher\Hasher\UserPasswordHasherInterface;

public function register(Request $request, UserPasswordHasherInterface $passwordHasher, EntityManagerInterface $em): Response
{
    $user = new User();
    $plainPassword = $request->request->get('password');
    $hashedPassword = $passwordHasher->hashPassword($user, $plainPassword);
    $user->setPassword($hashedPassword);
    $em->persist($user);
    $em->flush();

    // ...
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Formulaire de connexion Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Template du formulaire de connexion</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/security/login.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    <form method="post">
        {% if error %}
            <div class="alert alert-danger">{{ error.messageKey|trans(error.messageData, 'security') }}</div>
        {% endif %}

        <input type="email" value="{{ last_username }}" name="email" id="inputEmail" required autofocus>
        <input type="password" name="password" id="inputPassword" required>

        <input type="hidden" name="_csrf_token" value="{{ csrf_token('authenticate') }}">

        <button type="submit">Se connecter</button>
    </form>
{% endblock %}</code></pre>
                    </div>
                    <p><strong>Remarques :</strong></p>
                    <ul>
                        <li>Le champ CSRF est automatiquement inclus par l'authenticator.</li>
                        <li><code>last_username</code> est fourni par la session.</li>
                        <li>L'erreur est passée via le formulaire (message générique "Invalid credentials").</li>
                    </ul>
                </div>
            </section>

            <!-- Déconnexion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gérer la déconnexion</h2>

                <div class="textExemple">
                    <p>La commande <code>make:auth</code> peut générer une route de déconnexion automatique :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/routes/security.yaml
app_logout:
    path: /logout
    methods: GET</code></pre>
                    </div>
                    <p>Il suffit ensuite d'ajouter un lien dans vos templates :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;a href="{{ path('app_logout') }}"&gt;Déconnexion&lt;/a&gt;</code></pre>
                    </div>
                    <p class="textExemple">
                        ⚠️ La déconnexion ne nécessite pas de méthode de contrôleur ; Symfony invalide automatiquement la session.
                        Le firewall doit contenir la configuration <code>logout</code>.
                    </p>
                </div>
            </section>

            <!-- Personnalisations avancées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Personnalisations courantes</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Redirection après connexion (par rôle)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">public function onAuthenticationSuccess(Request $request, TokenInterface $token, string $firewallName): ?Response
{
    $roles = $token->getRoleNames();
    if (in_array('ROLE_ADMIN', $roles)) {
        return new RedirectResponse($this->urlGenerator->generate('admin_dashboard'));
    }
    return new RedirectResponse($this->urlGenerator->generate('app_home'));
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser l'email ou le pseudo</h3>
                    <p>Modifiez la propriété dans <code>security.yaml</code> et l'entité User :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">providers:
    app_user_provider:
        entity:
            class: App\Entity\User
            property: username   # au lieu de email</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ajouter "Se souvenir de moi" (Remember Me)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># security.yaml (dans le firewall)
main:
    remember_me:
        secret:   '%kernel.secret%'
        lifetime: 604800  # 1 semaine
        path:     /
        always_remember_me: true</code></pre>
                    </div>
                    <p>Ajoutez une case à cocher dans <code>login.html.twig</code> :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;input type="checkbox" name="_remember_me" value="1"&gt; Se souvenir de moi</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Limiter les tentatives de connexion (rate limiting)</h3>
                    <p>Avec Symfony 6.2+ et le composant RateLimiter :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/security.yaml
main:
    login_throttling:
        max_attempts: 5   # 5 tentatives
        interval: '15 minutes'</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Premier système d'authentification</h3>
                    <p>Utilisez <code>make:auth</code> pour générer un système complet. Créez manuellement un utilisateur en BDD (avec un mot de passe haché) et testez la connexion.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:user    # crée User (si pas déjà fait)
php bin/console make:auth
# Choisir "Login form authenticator"
# Répondre "yes" pour l'entité et la route de logout

# Créer un utilisateur via fixture ou manuellement
php bin/console doctrine:query:sql "INSERT INTO user (email, password, roles) VALUES ('test@example.com', '$2y$13\$...', '[]')"</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Inscription des utilisateurs</h3>
                    <p>Créez un contrôleur d'inscription qui utilise <code>UserPasswordHasherInterface</code> pour hacher le mot de passe avant de persister l'utilisateur.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Controller/RegistrationController.php
#[Route('/register', name: 'app_register')]
public function register(Request $request, UserPasswordHasherInterface $passwordHasher, EntityManagerInterface $em): Response
{
    if ($request->isMethod('POST')) {
        $user = new User();
        $user->setEmail($request->request->get('email'));
        $hashed = $passwordHasher->hashPassword($user, $request->request->get('password'));
        $user->setPassword($hashed);
        $em->persist($user);
        $em->flush();
        return $this->redirectToRoute('app_login');
    }
    return $this->render('registration/register.html.twig');
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Rôles et accès</h3>
                    <p>Ajoutez un champ <code>roles</code> dans l'entité User (généré automatiquement). Créez une zone admin protégée par <code>ROLE_ADMIN</code> en configurant <code>access_control</code>.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-yaml"># security.yaml
access_control:
    - { path: ^/admin, roles: ROLE_ADMIN }
    - { path: ^/profile, roles: ROLE_USER }</code></pre>
                            <p>Dans un contrôleur :</p>
                            <pre v-pre><code class="language-php">$this->denyAccessUnlessGranted('ROLE_ADMIN');</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques de sécurité</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Ne jamais stocker de mot de passe en clair</strong> – utilisez toujours <code>UserPasswordHasherInterface</code>.</li>
                        <li><strong>Protection CSRF</strong> – l'authenticator génère un token, vérifiez qu'il est présent.</li>
                        <li><strong>Message d'erreur générique</strong> – "Identifiants invalides" plutôt que "Email inconnu".</li>
                        <li><strong>Utilisez HTTPS en production</strong> – les mots de passe voyagent en clair sinon.</li>
                        <li><strong>Limitez les tentatives de connexion</strong> (login_throttling) contre le brute force.</li>
                        <li><strong>Validez la force des mots de passe</strong> (avec des contraintes Assert dans l'entité).</li>
                        <li><strong>Déconnectez l'utilisateur après un certain temps d'inactivité</strong> via <code>session.gc_maxlifetime</code>.</li>
                    </ul>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        <code>make:auth</code> est un générateur puissant qui accélère considérablement la mise en place
                        d'un système d'authentification sécurisé et conforme aux standards Symfony.
                    </p>
                    <ul>
                        <li>Il génère un <strong>authenticator moderne</strong> (basé sur les passesports).</li>
                        <li>Il respecte les <strong>bonnes pratiques de sécurité</strong> (CSRF, password hashing, messages génériques).</li>
                        <li>Il est <strong>entièrement personnalisable</strong> (redirections, champs, rôles).</li>
                    </ul>
                    <p>
                        Prochaines leçons : l'API Authenticator pour les APIs (JWT, OAuth), l'utilisation de voter pour les permissions complexes,
                        et l'intégration de deux facteurs (2FA).
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyMakeAuthLesson',

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
                    const languages = ['bash', 'php', 'yaml', 'twig'];
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
/* === STYLES IDENTIQUES À LA LEÇON SUR LES FORMULAIRES === */
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