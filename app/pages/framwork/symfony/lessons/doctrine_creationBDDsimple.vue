<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Créer et utiliser une base de données avec Doctrine</h1>
                <p class="lesson-meta text-white">PHP • Symfony • Doctrine ORM • Migrations • SQL</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi Doctrine ?</h2>
                <p class="textExemple">
                    <strong>Doctrine</strong> est l'ORM (Object Relational Mapper) standard de Symfony.
                    Il permet de manipuler votre base de données via des objets PHP, sans écrire de SQL manuel.
                    Doctrine gère la persistance, les relations, les migrations et bien plus encore.
                </p>
                <p class="textExemple">
                    Dans cette leçon, nous allons voir comment installer et configurer Doctrine, créer des entités,
                    générer des migrations, et interroger la base avec des méthodes simples et le QueryBuilder.
                    Aucune donnée factice n'est utilisée ici : nous construisons la structure de base.
                </p>
            </section>

            <!-- Installation et configuration -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et configuration</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Installer Doctrine dans un projet Symfony</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer l'ORM Pack (Doctrine + migrations + MakerBundle)
composer require symfony/orm-pack
composer require --dev symfony/maker-bundle</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configurer la connexion à la base de données</h3>
                    <p>Modifiez le fichier <code>.env</code> à la racine du projet :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Pour MySQL / MariaDB
DATABASE_URL="mysql://root:password@127.0.0.1:3306/mon_projet?serverVersion=8.0"

# Pour SQLite (simple pour le développement)
DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"

# Pour PostgreSQL
DATABASE_URL="postgresql://app:!ChangeMe@127.0.0.1:5432/app?serverVersion=15&charset=utf8"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer la base de données</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Créer la base de données (si elle n'existe pas)
php bin/console doctrine:database:create

# Vérifier la connexion
php bin/console doctrine:query:sql "SELECT 1"</code></pre>
                    </div>
                </div>
            </section>

            <!-- Créer une entité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer une entité (modèle)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Générer une entité avec MakerBundle</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Créer l'entité Article (mode interactif)
php bin/console make:entity Article

# Répondez aux questions :
# > titre (string, 255)
# > contenu (text)
# > dateCreation (datetime)
# > slug (string, 255, nullable)  [optionnel]
# Appuyez sur Entrée pour terminer</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple d'entité Article générée</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Article.php
namespace App\Entity;

use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity]
class Article
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 255)]
    private ?string $titre = null;

    #[ORM\Column(type: 'text')]
    private ?string $contenu = null;

    #[ORM\Column(type: 'datetime')]
    private ?\DateTimeInterface $dateCreation = null;

    #[ORM\Column(length: 255, nullable: true)]
    private ?string $slug = null;

    // Getters et setters...
    public function getId(): ?int { return $this->id; }
    public function getTitre(): ?string { return $this->titre; }
    public function setTitre(string $titre): self { $this->titre = $titre; return $this; }
    public function getContenu(): ?string { return $this->contenu; }
    public function setContenu(string $contenu): self { $this->contenu = $contenu; return $this; }
    public function getDateCreation(): ?\DateTimeInterface { return $this->dateCreation; }
    public function setDateCreation(\DateTimeInterface $dateCreation): self { $this->dateCreation = $dateCreation; return $this; }
    public function getSlug(): ?string { return $this->slug; }
    public function setSlug(?string $slug): self { $this->slug = $slug; return $this; }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ajouter un champ après création</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity Article
# Ajoutez un champ "vues" (integer, non nullable)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Migrations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Migrations – synchroniser la base</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Générer une migration</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Compare les entités avec la base et crée une migration
php bin/console make:migration</code></pre>
                    </div>
                    <p>Un fichier PHP est créé dans <code>migrations/VersionXXXXXXXX.php</code>.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple de migration</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// migrations/Version20250408120000.php
declare(strict_types=1);

namespace DoctrineMigrations;

use Doctrine\DBAL\Schema\Schema;
use Doctrine\Migrations\AbstractMigration;

final class Version20250408120000 extends AbstractMigration
{
    public function getDescription(): string
    {
        return 'Crée la table article';
    }

    public function up(Schema $schema): void
    {
        $this->addSql('CREATE TABLE article (
            id INT AUTO_INCREMENT NOT NULL,
            titre VARCHAR(255) NOT NULL,
            contenu LONGTEXT NOT NULL,
            date_creation DATETIME NOT NULL,
            slug VARCHAR(255) DEFAULT NULL,
            vues INT NOT NULL,
            PRIMARY KEY(id)
        ) DEFAULT CHARACTER SET utf8mb4');
    }

    public function down(Schema $schema): void
    {
        $this->addSql('DROP TABLE article');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exécuter les migrations</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Appliquer toutes les migrations en attente
php bin/console doctrine:migrations:migrate

# Voir le statut
php bin/console doctrine:migrations:status

# Annuler la dernière migration (downgrade)
php bin/console doctrine:migrations:migrate prev</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utilisation de base : persister et lire -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Opérations CRUD de base</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Créer (persister) un article</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/ArticleController.php
use App\Entity\Article;
use Doctrine\ORM\EntityManagerInterface;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class ArticleController extends AbstractController
{
    #[Route('/article/creer')]
    public function creer(EntityManagerInterface $em): Response
    {
        $article = new Article();
        $article->setTitre('Mon premier article');
        $article->setContenu('Ceci est le contenu.');
        $article->setDateCreation(new \DateTime());
        $article->setVues(0);

        // Doctrine "persist" prépare l'insertion
        $em->persist($article);
        // "flush" exécute la requête INSERT
        $em->flush();

        return new Response('Article créé avec l\'id '.$article->getId());
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Lire des articles (Repository)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use App\Repository\ArticleRepository;

#[Route('/articles')]
public function liste(ArticleRepository $repo): Response
{
    // Récupérer tous les articles
    $articles = $repo->findAll();

    // Récupérer un article par son id
    $article = $repo->find(1);

    // Récupérer un article par un critère (ex: titre)
    $article = $repo->findOneBy(['titre' => 'Mon premier article']);

    // Récupérer plusieurs articles avec critères
    $articlesRecents = $repo->findBy(
        ['vues' => 0],           // critères
        ['dateCreation' => 'DESC'], // tri
        10                         // limite
    );

    return $this->render('article/liste.html.twig', [
        'articles' => $articles,
    ]);
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Mettre à jour un article</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/article/modifier/{id}')]
public function modifier(int $id, ArticleRepository $repo, EntityManagerInterface $em): Response
{
    $article = $repo->find($id);
    if (!$article) {
        throw $this->createNotFoundException('Article inexistant');
    }

    $article->setTitre('Nouveau titre');
    $article->setContenu('Contenu mis à jour');
    // Pas besoin de persist() car l'entité est déjà gérée par Doctrine
    $em->flush();

    return new Response('Article modifié');
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Supprimer un article</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/article/supprimer/{id}')]
public function supprimer(int $id, ArticleRepository $repo, EntityManagerInterface $em): Response
{
    $article = $repo->find($id);
    if ($article) {
        $em->remove($article);
        $em->flush();
    }
    return new Response('Article supprimé');
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Requêtes avancées avec QueryBuilder -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Requêtes avancées : QueryBuilder</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Créer une méthode personnalisée dans le Repository</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Repository/ArticleRepository.php
namespace App\Repository;

use App\Entity\Article;
use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
use Doctrine\Persistence\ManagerRegistry;

class ArticleRepository extends ServiceEntityRepository
{
    public function __construct(ManagerRegistry $registry)
    {
        parent::__construct($registry, Article::class);
    }

    public function findArticlesRecents(int $limite = 5): array
    {
        return $this->createQueryBuilder('a')
            ->orderBy('a.dateCreation', 'DESC')
            ->setMaxResults($limite)
            ->getQuery()
            ->getResult();
    }

    public function findArticlesAvecPlusDeVues(int $minVues): array
    {
        return $this->createQueryBuilder('a')
            ->where('a.vues >= :min')
            ->setParameter('min', $minVues)
            ->orderBy('a.vues', 'DESC')
            ->getQuery()
            ->getResult();
    }

    public function searchByTitre(string $terme): array
    {
        return $this->createQueryBuilder('a')
            ->where('a.titre LIKE :terme')
            ->setParameter('terme', '%' . $terme . '%')
            ->getQuery()
            ->getResult();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser ces méthodes dans un controller</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/articles/recent')]
public function recents(ArticleRepository $repo): Response
{
    $articles = $repo->findArticlesRecents(3);
    // ...
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Relations entre entités -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Relations entre tables</h2>

                <div class="textExemple">
                    <h3 class="text-purple">ManyToOne : un article appartient à une catégorie</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity Categorie
# Ajoutez : nom (string, 100)

php bin/console make:entity Article
# Ajoutez un champ "categorie" (relation ManyToOne, cible Categorie)</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans Article.php (extrait)
#[ORM\ManyToOne(inversedBy: 'articles')]
#[ORM\JoinColumn(nullable: false)]
private ?Categorie $categorie = null;

// Dans Categorie.php
#[ORM\OneToMany(mappedBy: 'categorie', targetEntity: Article::class)]
private Collection $articles;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">ManyToMany : articles et tags</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity Tag
# Ajoutez : nom (string, 50)

php bin/console make:entity Article
# Ajoutez un champ "tags" (relation ManyToMany, cible Tag)</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Générer les migrations pour les relations</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:migration
php bin/console doctrine:migrations:migrate</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec Doctrine</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Utilisez les repositories</strong> : centralisez toutes les requêtes personnalisées.</li>
                        <li><strong>Évitez le chargement excessif (N+1)</strong> : utilisez les jointures dans QueryBuilder.</li>
                        <li><strong>Flush après plusieurs persist</strong> : un seul flush est plus performant.</li>
                        <li><strong>Validez les entités</strong> avec le composant Validator avant de persister.</li>
                        <li><strong>Utilisez des transactions</strong> pour les opérations critiques.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple de transaction</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$em->beginTransaction();
try {
    $article = new Article();
    $em->persist($article);
    $commentaire = new Commentaire();
    $em->persist($commentaire);
    $em->flush();
    $em->commit();
} catch (\Exception $e) {
    $em->rollback();
    throw $e;
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Créer une entité "Produit"</h3>
                    <p>Créez l'entité <code>Produit</code> avec les champs :</p>
                    <ul>
                        <li>nom (string, 100)</li>
                        <li>prix (decimal, 10,2)</li>
                        <li>stock (integer)</li>
                        <li>dateCreation (datetime)</li>
                    </ul>
                    <p>Générez la migration et exécutez-la.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:entity Produit
# nom (string, 100)
# prix (decimal, 10,2)
# stock (integer)
# dateCreation (datetime)

php bin/console make:migration
php bin/console doctrine:migrations:migrate</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Requêtes sur Produit</h3>
                    <p>Dans le repository <code>ProduitRepository</code>, écrivez une méthode <code>findProduitsEnStock()</code> qui retourne les produits avec stock > 0.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">public function findProduitsEnStock(): array
{
    return $this->createQueryBuilder('p')
        ->where('p.stock > 0')
        ->orderBy('p.nom', 'ASC')
        ->getQuery()
        ->getResult();
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <p>
                        Doctrine ORM vous permet de créer et d'interagir avec votre base de données
                        de manière objet, sans écrire de SQL. Grâce aux entités, migrations et repositories,
                        vous gérez proprement le schéma et les données.
                    </p>
                    <p>
                        Prochaines étapes : explorer les relations plus complexes, les événements de cycle de vie,
                        et l'optimisation des performances.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'DoctrineDatabaseLesson',

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
                        const bashScript = document.createElement('script');
                        bashScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/bash.min.js';
                        bashScript.onload = resolve;
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