<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Architecture Hexagonale avec Symfony</h1>
                <p class="lesson-meta text-white">Symfony • Architecture Hexagonale • Ports & Adaptateurs • DDD</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que l'Architecture Hexagonale ?</h2>
                <p class="textExemple">
                    L'architecture hexagonale, également connue sous le nom de <strong>"Ports and Adapters Pattern"</strong>, est une méthode de conception de logiciels qui vise à créer des applications <strong>indépendantes de toute technologie spécifique</strong>, rendant ainsi le code plus maintenable et adaptable[reference:0].
                </p>
                <p class="textExemple">
                    Inventée par Alistair Cockburn en 2005, son objectif principal est d'isoler le cœur de l'application (la logique métier) des éléments externes tels que les bases de données, les interfaces utilisateur ou les services web. Cela permet de changer de framework, de base de données ou d'infrastructure sans impacter la logique métier, tout en rendant l'application bien plus facile à tester[reference:1][reference:2].
                </p>
            </section>

            <!-- Architecture -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 3 Couches de l'Architecture Hexagonale</h2>
                <p class="textExemple">
                    L'architecture hexagonale repose sur trois couches principales, organisées de manière concentrique autour du cœur métier[reference:3].
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">1. La couche « Domaine » (Le Cœur)</h3>
                    <ul>
                        <li>C'est le <strong>cœur de l'application</strong> qui contient toute la logique métier.</li>
                        <li>Elle est totalement indépendante de toute technologie spécifique (framework, base de données...).</li>
                        <li>Elle ne sait rien des couches extérieures et n'a aucune dépendance vers l'extérieur.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. La couche « Application »</h3>
                    <ul>
                        <li>Cette couche orchestre le flux de données entre la couche « Domaine » et les ports.</li>
                        <li>Elle contient la <strong>logique d'application</strong> qui n'est pas purement métier (ex: gestion des transactions).</li>
                        <li>C'est ici que l'on va implémenter les cas d'utilisation (Use Cases).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. La couche « Infrastructure »</h3>
                    <ul>
                        <li>C'est la couche externe qui interagit avec le monde extérieur (BDD, services web, système de fichiers...).</li>
                        <li>Elle <strong>implémente les ports</strong> définis dans les couches internes.</li>
                        <li>C'est le point d'entrée et de sortie de l'application (contrôleurs, repositories Doctrine...).</li>
                    </ul>
                </div>
            </section>

            <!-- Principe des Ports et Adaptateurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le Principe des Ports et Adaptateurs</h2>
                <p class="textExemple">
                    La clé de l'architecture hexagonale réside dans la séparation stricte via les concepts de <strong>Ports</strong> et d'<strong>Adaptateurs</strong>[reference:4].
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Les Ports</h3>
                    <p>Ce sont des <strong>interfaces (contrats)</strong> qui définissent comment le cœur de l'application interagit avec le monde extérieur. Il existe deux types de ports :</p>
                    <ul>
                        <li><strong>Ports primaires (driving ports)</strong> : Ils définissent les fonctionnalités <strong>fournies</strong> par le cœur de l'application. Exemple : une interface `UserRegistrationUseCase` pour créer un utilisateur.</li>
                        <li><strong>Ports secondaires (driven ports)</strong> : Ils définissent les fonctionnalités <strong>attendues</strong> par le cœur de l'application, mais implémentées à l'extérieur. Exemple : une interface `UserRepositoryInterface` pour accéder à la base de données.</li>
                    </ul>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Les Adaptateurs</h3>
                    <p>Ce sont les <strong>implémentations concrètes des ports</strong>. Ils "adaptent" les technologies externes pour qu'elles puissent communiquer avec le cœur de l'application.</p>
                    <ul>
                        <li><strong>Adaptateurs primaires</strong> : Ils reçoivent des requêtes du monde extérieur (ex: un contrôleur Symfony) et les transmettent au cœur via un port primaire.</li>
                        <li><strong>Adaptateurs secondaires</strong> : Ils implémentent les ports secondaires pour communiquer avec les systèmes externes. Exemple : `DoctrineUserRepository` qui implémente `UserRepositoryInterface`[reference:5].</li>
                    </ul>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Exemple d'un Port secondaire (interface dans le Domaine)
// src/Domain/Port/UserRepositoryInterface.php

namespace App\Domain\Port;

use App\Domain\Entity\User;

interface UserRepositoryInterface
{
    public function findById(int $id): ?User;
    public function save(User $user): void;
}</code></pre>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Exemple d'un Adaptateur secondaire (implémentation dans l'Infrastructure)
// src/Infrastructure/Persistence/DoctrineUserRepository.php

namespace App\Infrastructure\Persistence;

use App\Domain\Entity\User;
use App\Domain\Port\UserRepositoryInterface;
use Doctrine\ORM\EntityManagerInterface;

class DoctrineUserRepository implements UserRepositoryInterface
{
    public function __construct(private EntityManagerInterface $em) {}

    public function findById(int $id): ?User
    {
        return $this->em->getRepository(User::class)->find($id);
    }

    public function save(User $user): void
    {
        $this->em->persist($user);
        $this->em->flush();
    }
}</code></pre>
                </div>
            </section>

            <!-- Structure de dossiers recommandée -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure de Dossiers dans Symfony</h2>
                <p class="textExemple">
                    Pour implémenter cette architecture, la structure de dossiers reflète la séparation des responsabilités. L'idée est de créer des répertoires distincts pour les trois couches.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash">├── config/                     # Configuration Symfony
├── src/
│   ├── Domain/                 # Couche Domaine (Cœur métier)
│   │   ├── Entity/             # Entités métier (ex: Article, User)
│   │   ├── ValueObject/        # Objets de valeur (ex: Email, Money)
│   │   ├── Exception/          # Exceptions métier
│   │   ├── Port/               # Interfaces (Ports)
│   │   │   ├── UserRepositoryInterface.php
│   │   │   └── ...
│   │   └── Event/              # Événements de domaine
│   ├── Application/            # Couche Application (Use Cases)
│   │   ├── Command/            # Commandes CQRS
│   │   ├── Query/              # Requêtes CQRS
│   │   ├── Handler/            # Handlers associés
│   │   └── DTO/                # Objets de transfert de données
│   └── Infrastructure/         # Couche Infrastructure
│       ├── Persistence/        # Implémentation des repositories (Doctrine)
│       │   ├── DoctrineUserRepository.php
│       │   └── ...
│       ├── Api/                # Clients d'API externes
│       ├── Symfony/            # Adaptateurs spécifiques à Symfony
│       │   ├── Controller/     # Contrôleurs (Adaptateurs primaires)
│       │   ├── Security/       # Adaptateurs pour l'authentification
│       │   └── ...
│       └── Bus/                # Configuration des bus de messages
├── tests/                      # Tests (unitaires, fonctionnels...)
└── ...</code></pre>
                </div>
            </section>

            <!-- Implémentation Concrète avec CQRS -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Implémentation Concrète : Gestion d'Articles</h2>
                <p class="textExemple">
                    Prenons l'exemple d'une application de gestion d'articles, en nous basant sur l'article d'Adimeo. Nous allons créer un cas d'utilisation pour <strong>créer un nouvel article</strong>.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">1. Le Domaine (Article)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Domain/Entity/Article.php
namespace App\Domain\Entity;

class Article
{
    private ?int $id = null;
    private string $title;
    private string $content;

    public function __construct(string $title, string $content)
    {
        $this->setTitle($title);
        $this->setContent($content);
    }

    // Getters et setters avec logique métier
    public function setTitle(string $title): void
    {
        if (strlen($title) < 5) {
            throw new \InvalidArgumentException('Title must be at least 5 characters');
        }
        $this->title = $title;
    }

    // ... autres getters/setters
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">2. Le Port Secondaire (Repository)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Domain/Port/ArticleRepositoryInterface.php
namespace App\Domain\Port;

use App\Domain\Entity\Article;

interface ArticleRepositoryInterface
{
    public function save(Article $article): void;
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">3. La Couche Application (Use Case & Handler)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Application/Command/CreateArticleCommand.php
namespace App\Application\Command;

final readonly class CreateArticleCommand
{
    public function __construct(
        public string $title,
        public string $content
    ) {}
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Application/Handler/CreateArticleHandler.php
namespace App\Application\Handler;

use App\Domain\Entity\Article;
use App\Domain\Port\ArticleRepositoryInterface;
use App\Application\Command\CreateArticleCommand;

class CreateArticleHandler
{
    public function __construct(
        private ArticleRepositoryInterface $articleRepository
    ) {}

    public function __invoke(CreateArticleCommand $command): void
    {
        $article = new Article($command->title, $command->content);
        $this->articleRepository->save($article);
    }
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">4. L'Adaptateur Primaire (Contrôleur Symfony)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Infrastructure/Symfony/Controller/ArticleController.php
namespace App\Infrastructure\Symfony\Controller;

use App\Application\Command\CreateArticleCommand;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Messenger\MessageBusInterface;
use Symfony\Component\Routing\Attribute\Route;

class ArticleController extends AbstractController
{
    #[Route('/article', name: 'create_article', methods: ['POST'])]
    public function create(Request $request, MessageBusInterface $commandBus): Response
    {
        $data = json_decode($request->getContent(), true);
        $command = new CreateArticleCommand($data['title'], $data['content']);
        $commandBus->dispatch($command);

        return $this->json(['status' => 'Article created'], Response::HTTP_CREATED);
    }
}</code></pre>
                    </div>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">5. L'Adaptateur Secondaire (Repository Doctrine)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Infrastructure/Persistence/DoctrineArticleRepository.php
namespace App\Infrastructure\Persistence;

use App\Domain\Entity\Article;
use App\Domain\Port\ArticleRepositoryInterface;
use Doctrine\ORM\EntityManagerInterface;

class DoctrineArticleRepository implements ArticleRepositoryInterface
{
    public function __construct(private EntityManagerInterface $em) {}

    public function save(Article $article): void
    {
        $this->em->persist($article);
        $this->em->flush();
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utilisation de Symfony Messenger -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Aller plus loin : Le Message Bus (CQRS)</h2>
                <p class="textExemple">
                    Pour découpler encore plus les couches, on peut utiliser le composant <strong>Symfony Messenger</strong>. Il ne sert pas uniquement à faire de l'asynchrone, mais il implémente le pattern <strong>Message Bus</strong>, ce qui est parfait pour une architecture hexagonale[reference:6].
                </p>
                <div class="textExemple">
                    <h3 class="text-purple">Configuration de 3 Bus distincts</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/messenger.yaml
framework:
    messenger:
        default_bus: command.bus
        buses:
            command.bus: ~
            query.bus: ~
            event.bus:
                default_middleware: allow_no_handlers: true</code></pre>
                    </div>
                    <ul>
                        <li><strong>Command Bus</strong> : Pour les opérations d'écriture (mutations). Une commande ne retourne rien et ne doit avoir qu'un seul handler.</li>
                        <li><strong>Query Bus</strong> : Pour les opérations de lecture. Une requête retourne toujours une donnée.</li>
                        <li><strong>Event Bus</strong> : Pour notifier que quelque chose s'est passé. Un événement peut avoir plusieurs handlers.</li>
                    </ul>
                </div>
            </section>

            <!-- Bonnes pratiques et avantages -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages & Inconvénients</h2>
                <div class="textExemple">
                    <h3 class="text-purple">✅ Les Avantages</h3>
                    <ul>
                        <li><strong>Testabilité maximale</strong> : Le domaine et l'application peuvent être testés unitairement sans aucune dépendance externe (base de données, framework).</li>
                        <li><strong>Indépendance technologique</strong> : Changer de framework (Symfony vers Laravel) ou de base de données (MySQL vers PostgreSQL) devient un jeu d'enfant, sans toucher au cœur métier.</li>
                        <li><strong>Code plus maintenable</strong> : La séparation stricte des responsabilités rend le code plus propre, plus lisible et plus facile à faire évoluer.</li>
                        <li><strong>Focalisation sur le métier</strong> : Les développeurs passent plus de temps sur la logique métier, là où se trouve la valeur ajoutée.</li>
                    </ul>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">⚠️ Les Inconvénients / Défis</h3>
                    <ul>
                        <li><strong>Complexité initiale</strong> : L'architecture est plus complexe à mettre en place qu'une architecture MVC classique, ce qui peut être surdimensionné pour des petits projets.</li>
                        <li><strong>Courbe d'apprentissage</strong> : L'équipe doit maîtriser les concepts de DDD, CQRS, et Ports/Adapters.</li>
                        <li><strong>Nombre de fichiers</strong> : Le nombre de classes et d'interfaces augmente, ce qui peut rendre le projet plus verbeux.</li>
                    </ul>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        L'architecture hexagonale est un choix judicieux pour les projets Symfony complexes et amenés à évoluer dans la durée. Elle permet de créer un code robuste, découplé et hautement testable.
                    </p>
                    <p>
                        Bien que sa mise en place demande plus d'investissement initial, elle protège l'essentiel de votre application : votre logique métier. Symfony, avec ses composants (Dependency Injection, Messenger, Maker), offre un terrain de jeu idéal pour implémenter ce type d'architecture.
                    </p>
                    <p>
                        Pour aller plus loin, vous pouvez explorer les concepts de <strong>Domain-Driven Design (DDD)</strong> et utiliser des bundles comme <strong>hexagonal-maker-bundle</strong> pour générer automatiquement la structure de vos modules[reference:7].
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'HexagonalArchitectureLesson',

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
                    // Charger les langages PHP, Bash et YAML
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const bashScript = document.createElement('script');
                        bashScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/bash.min.js';
                        bashScript.onload = () => {
                            const yamlScript = document.createElement('script');
                            yamlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/yaml.min.js';
                            yamlScript.onload = resolve;
                            document.head.appendChild(yamlScript);
                        };
                        document.head.appendChild(bashScript);
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