<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Contrôle d'accès avec IsGranted</h1>
                <p class="lesson-meta text-white">Symfony • Security • Voter • Access Control</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que IsGranted ?</h2>
                <p class="textExemple">
                    Le composant Security de Symfony fournit un système de contrôle d'accès flexible et puissant. 
                    La fonction <code>isGranted()</code> (ou son équivalent Twig <code>is_granted()</code>) est le point d'entrée 
                    pour vérifier si l'utilisateur actuel possède une certaine permission, un rôle, ou si un voter personnalisé 
                    accorde l'accès.
                </p>
                <p class="textExemple">
                    Elle permet de sécuriser vos routes, vos actions de contrôleur, vos éléments Twig et même votre logique métier 
                    de manière déclarative, en découplant les règles d'accès de la logique applicative.
                </p>
            </section>

            <!-- Principes fondamentaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Principes fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Les 3 piliers de la sécurité Symfony</h3>
                    <ul>
                        <li><strong>Rôles</strong> : chaînes simples (ex: <code>ROLE_ADMIN</code>, <code>ROLE_USER</code>) hiérarchisables</li>
                        <li><strong>Attributs</strong> : chaînes arbitraires (ex: <code>edit</code>, <code>view</code>) qui représentent une action</li>
                        <li><strong>Voters</strong> : classes PHP contenant la logique métier d'autorisation (ex: "seul l'auteur peut modifier")</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Contrôleur / Twig
       │
       │ isGranted('edit', $article)
       ▼
Access Decision Manager
       │
       ├─▶ Vérification des rôles simples (ROLE_ADMIN)
       │
       └─▶ Parcours des Voters enregistrés
                │
                ├─ Voter 1 : supporte l'attribut 'edit' et la classe Article ?
                ├─ Voter 2 : supporte ...
                └─ Voter 3 : ...
                     │
                     └─ Réponse finale (ACCÈS / REFUS)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Installation et configuration -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et configuration de base</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Prérequis</h3>
                    <p>Le bundle Security fait partie du standard Symfony. Vérifiez qu'il est bien installé :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require symfony/security-bundle</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configuration minimale (security.yaml)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/security.yaml
security:
    providers:
        app_user_provider:
            entity:
                class: App\Entity\User
                property: email

    firewalls:
        main:
            lazy: true
            provider: app_user_provider
            form_login:
                login_path: login
                check_path: login
            logout:
                path: logout

    access_control:
        - { path: ^/admin, roles: ROLE_ADMIN }
        - { path: ^/profile, roles: ROLE_USER }

    role_hierarchy:
        ROLE_ADMIN: ROLE_USER
        ROLE_SUPER_ADMIN: ROLE_ADMIN</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utilisation dans les Contrôleurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">IsGranted dans les Contrôleurs</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. L'attribut #[IsGranted] (recommandé)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/ArticleController.php
use Symfony\Component\Security\Http\Attribute\IsGranted;

class ArticleController extends AbstractController
{
    // Seuls les utilisateurs avec ROLE_ADMIN peuvent créer un article
    #[Route('/article/new', name: 'article_new')]
    #[IsGranted('ROLE_ADMIN')]
    public function new(): Response
    {
        // ...
    }

    // Seul l'auteur (via un Voter 'edit') peut modifier l'article
    #[Route('/article/{id}/edit', name: 'article_edit')]
    #[IsGranted('edit', subject: 'article')]
    public function edit(Article $article): Response
    {
        // ...
    }

    // Combinaison de conditions (ET logique)
    #[Route('/article/{id}/publish', name: 'article_publish')]
    #[IsGranted('ROLE_EDITOR')]
    #[IsGranted('publish', subject: 'article')]
    public function publish(Article $article): Response
    {
        // ...
    }

    // Avec message d'erreur personnalisé
    #[Route('/article/{id}/delete', name: 'article_delete')]
    #[IsGranted('delete', subject: 'article', message: 'Vous ne pouvez pas supprimer cet article')]
    public function delete(Article $article): Response
    {
        // ...
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Méthode isGranted() dans l'action</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/article/{id}/edit', name: 'article_edit')]
public function edit(Article $article): Response
{
    // Vérification manuelle
    if (!$this->isGranted('ROLE_ADMIN')) {
        throw $this->createAccessDeniedException('Accès refusé');
    }

    // Ou avec un attribut personnalisé et un sujet
    if (!$this->isGranted('edit', $article)) {
        // Redirection ou affichage d'erreur
        $this->addFlash('error', 'Vous n\'êtes pas autorisé');
        return $this->redirectToRoute('article_list');
    }

    // ...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. denyAccessUnlessGranted() (raccourci)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/article/{id}/edit', name: 'article_edit')]
public function edit(Article $article): Response
{
    $this->denyAccessUnlessGranted('edit', $article, 'Vous n\'êtes pas l\'auteur');

    // Code exécuté uniquement si autorisé
    // ...
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- IsGranted dans Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">IsGranted dans les Templates Twig</h2>

                <div class="textExemple">
                    <p>
                        La fonction <code>is_granted()</code> permet d'adapter dynamiquement l'affichage selon les droits.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/article/show.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    <h1>{{ article.titre }}</h1>

    {% if is_granted('ROLE_ADMIN') %}
        <div class="admin-actions">
            <a href="{{ path('article_edit', {id: article.id}) }}">Éditer</a>
        </div>
    {% endif %}

    {# Vérification plus fine avec un voter #}
    {% if is_granted('edit', article) %}
        <a href="{{ path('article_edit', {id: article.id}) }}" class="btn btn-primary">
            Modifier l'article
        </a>
    {% endif %}

    {# Cacher un bouton si l'utilisateur n'est pas l'auteur #}
    {% if is_granted('delete', article) %}
        <button type="button" class="btn btn-danger">Supprimer</button>
    {% endif %}
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contrôle d'accès dans le menu de navigation</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig"><nav>
    <ul>
        <li><a href="{{ path('home') }}">Accueil</a></li>
        <li><a href="{{ path('article_list') }}">Articles</a></li>

        {% if is_granted('ROLE_USER') %}
            <li><a href="{{ path('profile') }}">Mon profil</a></li>
        {% endif %}

        {% if is_granted('ROLE_ADMIN') %}
            <li><a href="{{ path('admin_dashboard') }}">Administration</a></li>
        {% endif %}

        {% if is_granted('ROLE_USER') %}
            <li><a href="{{ path('app_logout') }}">Déconnexion</a></li>
        {% else %}
            <li><a href="{{ path('app_login') }}">Connexion</a></li>
        {% endif %}
    </ul>
</nav></code></pre>
                    </div>
                </div>
            </section>

            <!-- Voters personnalisés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Voters personnalisés : la logique métier de l'autorisation</h2>

                <div class="textExemple">
                    <p>
                        Les Voters sont le cœur des règles d'accès complexes. Une classe Voter implémente la logique pour un ensemble 
                        d'attributs (ex: <code>edit</code>, <code>view</code>) et de classes de sujets (ex: <code>Article::class</code>).
                    </p>

                    <h3 class="text-purple">Créer un Voter avec la commande Maker</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:voter ArticleVoter</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple : Voter pour les articles</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Security/Voter/ArticleVoter.php
namespace App\Security\Voter;

use App\Entity\Article;
use App\Entity\User;
use Symfony\Component\Security\Core\Authentication\Token\TokenInterface;
use Symfony\Component\Security\Core\Authorization\Voter\Voter;
use Symfony\Component\Security\Core\User\UserInterface;

class ArticleVoter extends Voter
{
    // Définition des attributs gérés par ce voter
    public const EDIT   = 'edit';
    public const DELETE = 'delete';
    public const PUBLISH = 'publish';

    protected function supports(string $attribute, $subject): bool
    {
        // Le voter ne supporte que les attributs déclarés et un sujet de type Article
        return in_array($attribute, [self::EDIT, self::DELETE, self::PUBLISH])
            && $subject instanceof Article;
    }

    protected function voteOnAttribute(string $attribute, $subject, TokenInterface $token): bool
    {
        $user = $token->getUser();

        // Si l'utilisateur n'est pas connecté, refuser
        if (!$user instanceof UserInterface) {
            return false;
        }

        /** @var Article $article */
        $article = $subject;

        return match ($attribute) {
            self::EDIT   => $this->canEdit($article, $user),
            self::DELETE => $this->canDelete($article, $user),
            self::PUBLISH => $this->canPublish($article, $user),
            default => false,
        };
    }

    private function canEdit(Article $article, UserInterface $user): bool
    {
        // L'auteur peut modifier ses articles
        if ($user === $article->getAuthor()) {
            return true;
        }

        // Un administrateur peut tout modifier
        if (in_array('ROLE_ADMIN', $user->getRoles())) {
            return true;
        }

        return false;
    }

    private function canDelete(Article $article, UserInterface $user): bool
    {
        // Seul l'auteur ou un admin peut supprimer
        return $user === $article->getAuthor() || in_array('ROLE_ADMIN', $user->getRoles());
    }

    private function canPublish(Article $article, UserInterface $user): bool
    {
        // Un éditeur peut publier, mais pas forcément modifier
        return in_array('ROLE_EDITOR', $user->getRoles());
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation du Voter</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un contrôleur
#[Route('/article/{id}/edit', name: 'article_edit')]
public function edit(Article $article): Response
{
    // Le voter ArticleVoter sera automatiquement appelé
    $this->denyAccessUnlessGranted('edit', $article);

    // ...
}

// Dans Twig
{% if is_granted('delete', article) %}
    <a href="{{ path('article_delete', {id: article.id}) }}">Supprimer</a>
{% endif %}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Attributs avancés et hiérarchie -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fonctionnalités avancées</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Hiérarchie des rôles</h3>
                    <p>
                        Définissez une hiérarchie dans <code>security.yaml</code> pour que certains rôles héritent d'autres :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">role_hierarchy:
    ROLE_CONTRIBUTOR: ROLE_USER
    ROLE_EDITOR:       ROLE_CONTRIBUTOR
    ROLE_ADMIN:        ROLE_EDITOR
    ROLE_SUPER_ADMIN:  ROLE_ADMIN</code></pre>
                    </div>
                    <p>
                        Un utilisateur avec <code>ROLE_EDITOR</code> aura automatiquement <code>ROLE_CONTRIBUTOR</code> et <code>ROLE_USER</code>.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">IsGranted avec expression (Security Expression Language)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\ExpressionLanguage\Expression;

#[Route('/article/{id}/report', name: 'article_report')]
#[IsGranted(new Expression(
    'is_authenticated() and user.getEmail() matches "/^admin/"'
))]
public function report(Article $article): Response
{
    // Seul un utilisateur authentifié avec email commençant par "admin" peut signaler
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Accès basé sur la méthode HTTP ou la route</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Restreindre à une méthode HTTP
#[Route('/api/article', methods: ['POST'])]
#[IsGranted('ROLE_API_USER')]
public function apiCreate(): Response { ... }

// Ou utiliser access_control dans security.yaml
access_control:
    - { path: ^/api, roles: ROLE_API_USER, methods: [POST, PUT] }</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Sécurisation d'un blog</h3>
                    <p>Créez un système d'autorisation pour un blog avec les règles suivantes :</p>
                    <ul>
                        <li>Tout le monde peut lire les articles (pas de restriction)</li>
                        <li>Seuls les utilisateurs connectés peuvent commenter</li>
                        <li>Seul l'auteur de l'article peut le modifier</li>
                        <li>Les administrateurs peuvent tout faire (modifier, supprimer, publier)</li>
                        <li>Les éditeurs peuvent publier des articles (mais pas les modifier)</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// ArticleVoter (extrait)
protected function voteOnAttribute(string $attribute, $subject, TokenInterface $token): bool
{
    $user = $token->getUser();

    // Admins ont tous les droits
    if (in_array('ROLE_ADMIN', $user->getRoles())) {
        return true;
    }

    return match ($attribute) {
        'edit' => $user === $subject->getAuthor(),
        'publish' => in_array('ROLE_EDITOR', $user->getRoles()),
        'comment' => $user instanceof UserInterface, // tout utilisateur connecté
        default => false,
    };
}

// Dans les contrôleurs
#[Route('/article/{id}/edit', name: 'article_edit')]
#[IsGranted('edit', subject: 'article')]
public function edit(Article $article): Response { ... }

#[Route('/article/{id}/comment', name: 'article_comment')]
#[IsGranted('comment')]
public function comment(Article $article, Request $request): Response { ... }</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Voter pour des fichiers</h3>
                    <p>Créez un Voter qui autorise le téléchargement d'un fichier uniquement si :</p>
                    <ul>
                        <li>Le fichier appartient à l'utilisateur connecté</li>
                        <li>OU le fichier est public (champ <code>isPublic</code> = true)</li>
                        <li>OU l'utilisateur a le rôle ROLE_ADMIN</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Security/Voter/FileVoter.php
class FileVoter extends Voter
{
    public const DOWNLOAD = 'download';

    protected function supports(string $attribute, $subject): bool
    {
        return self::DOWNLOAD === $attribute && $subject instanceof File;
    }

    protected function voteOnAttribute(string $attribute, $subject, TokenInterface $token): bool
    {
        $user = $token->getUser();
        /** @var File $file */
        $file = $subject;

        // Admin a toujours accès
        if ($user && in_array('ROLE_ADMIN', $user->getRoles())) {
            return true;
        }

        // Fichier public → accès pour tous (même non connecté)
        if ($file->isPublic()) {
            return true;
        }

        // Fichier privé : seul le propriétaire y a accès
        return $user && $user === $file->getOwner();
    }
}

// Utilisation dans un contrôleur
#[Route('/file/{id}/download', name: 'file_download')]
public function download(File $file): Response
{
    $this->denyAccessUnlessGranted(FileVoter::DOWNLOAD, $file);
    // ...
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques et conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Organisation et séparation</h3>
                    <ul>
                        <li><strong>Ne pas mélanger les rôles et la logique métier</strong> : un rôle est un niveau d'accès, pas une action.</li>
                        <li><strong>Utilisez des Voters pour toute logique complexe</strong> : cela garde vos contrôleurs légers et votre sécurité centralisée.</li>
                        <li><strong>Nommez clairement vos attributs</strong> : <code>edit</code>, <code>view</code>, <code>delete</code> plutôt que des chaînes arbitraires.</li>
                        <li><strong>Testez vos Voters</strong> : isolez-les avec des tests unitaires pour valider les règles d'accès.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurité</h3>
                    <ul>
                        <li>N'oubliez jamais de sécuriser vos routes avec <code>#[IsGranted]</code> ou <code>denyAccessUnlessGranted()</code>.</li>
                        <li>Évitez les conditions d'accès en dur dans les templates : utilisez <code>is_granted()</code> pour rester DRY.</li>
                        <li>La hiérarchie des rôles simplifie la gestion mais soyez vigilant aux héritages implicites.</li>
                        <li>Pensez à désactiver la protection CSRF pour les endpoints qui n'en ont pas besoin (API).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance</h3>
                    <ul>
                        <li>Les Voters sont appelés pour chaque vérification ; assurez-vous qu'ils sont légers.</li>
                        <li>Utilisez le cache des décisions d'accès si nécessaire (via <code>AccessDecisionManager</code>).</li>
                        <li>Préférez les attributs <code>#[IsGranted]</code> aux appels programmatiques pour une meilleure performance en production.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Le système <code>isGranted</code> est la pierre angulaire de la sécurité dans Symfony. 
                        Maîtriser les rôles, les attributs et surtout les Voters vous permettra de construire des applications 
                        robustes où chaque action est correctement autorisée, sans avoir à dupliquer la logique.
                    </p>
                    <p>
                        Prochaine étape : découvrez l'intégration avec API Platform, la sécurité basée sur les expressions 
                        et l'utilisation de <code>@Security</code> dans les contrôleurs pour des conditions encore plus fines.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyIsGrantedLesson',

    mounted() {
        // Charger highlight.js + thème VS Code Dark via CDN
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
                    // Charger les langages PHP, Twig, YAML et Bash
                    const langs = ['php', 'twig', 'yaml', 'bash'];
                    let loaded = 0;
                    langs.forEach(lang => {
                        const langScript = document.createElement('script');
                        langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`;
                        langScript.onload = () => {
                            loaded++;
                            if (loaded === langs.length) resolve();
                        };
                        document.head.appendChild(langScript);
                    });
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            // Appliquer la coloration sur tous les blocs de code
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
/* Les styles restent exactement les mêmes que ceux fournis dans le template original */
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