<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Doctrine – Créer et utiliser une base de données</h1>
                <p class="lesson-meta text-white">PHP • Symfony • Doctrine ORM • Migrations • Repositories</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi Doctrine ?</h2>
                <p class="textExemple">
                    <strong>Doctrine</strong> est l'ORM (Object Relational Mapper) par défaut de Symfony.
                    Il permet de manipuler votre base de données via des objets PHP, sans écrire une ligne de SQL.
                    Doctrine gère la persistance, les relations, les migrations, et bien plus encore.
                </p>
                <p class="textExemple">
                    Dans cette leçon, nous allons voir comment installer et configurer Doctrine, créer des entités,
                    générer des migrations, interroger la base avec le QueryBuilder et les repositories,
                    et mettre en place des relations entre les tables.
                </p>
            </section>

            <!-- Installation et configuration -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et configuration</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Installer Doctrine</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Dans un projet Symfony (avec Symfony CLI)
composer require symfony/orm-pack
composer require --dev symfony/maker-bundle

# Le ORM Pack installe : doctrine/orm, doctrine/doctrine-bundle, doctrine/doctrine-migrations-bundle</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Configurer la connexion à la base de données</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Fichier .env (à la racine du projet)
DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name?serverVersion=8.0"

# Pour SQLite (parfait pour le développement)
DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"

# Pour PostgreSQL
DATABASE_URL="postgresql://db_user:db_password@127.0.0.1:5432/db_name"

# Pour SQL Server
DATABASE_URL="sqlsrv://sa:password@localhost:1433?database=db_name"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer la base de données</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Créer la base (si elle n'existe pas)
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
                    <h3 class="text-purple">Génération automatique avec MakerBundle</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Générer une entité Article avec des champs
php bin/console make:entity Article

# Le mode interactif pose des questions :
# > titre (string, 255)
# > contenu (text)
# > publishedAt (datetime)
# > slug (string, 255, nullable)
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
    private ?\DateTimeInterface $publishedAt = null;

    #[ORM\Column(length: 255, nullable: true)]
    private ?string $slug = null;

    // Getters et setters...
    public function getId(): ?int { return $this->id; }
    public function getTitre(): ?string { return $this->titre; }
    public function setTitre(string $titre): self { $this->titre = $titre; return $this; }
    // ...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ajouter/modifier des champs après création</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Ajouter un champ "vues" (integer)
php bin/console make:entity Article

# Choisissez "vues" comme nouveau champ, type integer, nullable false
# La commande met à jour l'entité et propose de créer une migration</code></pre>
                    </div>
                </div>
            </section>

            <!-- Migrations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Migrations – synchroniser le schéma</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Générer une migration</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Créer une migration à partir des différences entre entités et base
php bin/console make:migration

# Un fichier est créé dans migrations/VersionXXXXXXXX.php</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple de fichier de migration</h3>
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
        return 'Ajoute le champ vues à la table article';
    }

    public function up(Schema $schema): void
    {
        $this->addSql('ALTER TABLE article ADD vues INT NOT NULL DEFAULT 0');
    }

    public function down(Schema $schema): void
    {
        $this->addSql('ALTER TABLE article DROP vues');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exécuter les migrations</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Appliquer toutes les migrations non encore exécutées
php bin/console doctrine:migrations:migrate

# Voir le statut
php bin/console doctrine:migrations:status

# Rejouer une migration (attention en production)
php bin/console doctrine:migrations:execute --up Version20250408120000</code></pre>
                    </div>
                </div>
            </section>

            <!-- Persister et interroger -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Persister et interroger des données</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Créer (persister) un article</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/ArticleController.php
use App\Entity\Article;
use Doctrine\ORM\EntityManagerInterface;

#[Route('/article/new')]
public function new(EntityManagerInterface $em): Response
{
    $article = new Article();
    $article->setTitre('Mon premier article');
    $article->setContenu('Lorem ipsum...');
    $article->setPublishedAt(new \DateTimeImmutable());

    // Préparer la persistance
    $em->persist($article);
    // Exécuter la requête INSERT
    $em->flush();

    return new Response('Article créé avec l\'id '.$article->getId());
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Lire des articles (Repository)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un controller
use App\Repository\ArticleRepository;

#[Route('/articles')]
public function list(ArticleRepository $repo): Response
{
    // findAll() : SELECT * FROM article
    $articles = $repo->findAll();

    // find($id) : SELECT * WHERE id = ?
    $article = $repo->find(1);

    // findBy() : avec critères
    $recentArticles = $repo->findBy(
        ['publishedAt' => '2025-01-01'], 
        ['publishedAt' => 'DESC'], 
        10
    );

    // findOneBy() : un seul résultat
    $article = $repo->findOneBy(['titre' => 'Mon article']);
}
</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Mettre à jour et supprimer</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Mise à jour
$article = $repo->find(1);
$article->setTitre('Nouveau titre');
$em->flush(); // UPDATE automatique

// Suppression
$em->remove($article);
$em->flush();</code></pre>
                    </div>
                </div>
            </section>

            <!-- QueryBuilder et DQL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Requêtes avancées avec QueryBuilder</h2>

                <div class="textExemple">
                    <h3 class="text-purple">QueryBuilder dans un Repository personnalisé</h3>
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

    public function findRecentArticles(int $limit = 5): array
    {
        return $this->createQueryBuilder('a')
            ->where('a.publishedAt <= :now')
            ->setParameter('now', new \DateTime())
            ->orderBy('a.publishedAt', 'DESC')
            ->setMaxResults($limit)
            ->getQuery()
            ->getResult();
    }

    public function searchByTitre(string $searchTerm): array
    {
        return $this->createQueryBuilder('a')
            ->where('a.titre LIKE :term')
            ->setParameter('term', '%' . $searchTerm . '%')
            ->getQuery()
            ->getResult();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Requête avec jointure (relation ManyToOne)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">public function findArticlesByCategory(string $categoryName): array
{
    return $this->createQueryBuilder('a')
        ->innerJoin('a.categorie', 'c')
        ->where('c.nom = :nom')
        ->setParameter('nom', $categoryName)
        ->orderBy('a.publishedAt', 'DESC')
        ->getQuery()
        ->getResult();
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">DQL (Doctrine Query Language) – alternative SQL-like</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$query = $em->createQuery(
    'SELECT a FROM App\Entity\Article a WHERE a.vues > :min ORDER BY a.vues DESC'
)->setParameter('min', 100);

$popularArticles = $query->getResult();</code></pre>
                    </div>
                </div>
            </section>

            <!-- Relations entre entités -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Relations : ManyToOne, OneToMany, ManyToMany</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Relation ManyToOne (un article appartient à une catégorie)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Categorie.php
#[ORM\Entity]
class Categorie
{
    #[ORM\Id, ORM\GeneratedValue, ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 100)]
    private ?string $nom = null;

    // OneToMany : une catégorie a plusieurs articles
    #[ORM\OneToMany(mappedBy: 'categorie', targetEntity: Article::class, cascade: ['persist'])]
    private Collection $articles;

    public function __construct() {
        $this->articles = new ArrayCollection();
    }
    // getter/setter...
}

// src/Entity/Article.php
#[ORM\Entity]
class Article
{
    // ...

    #[ORM\ManyToOne(inversedBy: 'articles')]
    #[ORM\JoinColumn(nullable: false)]
    private ?Categorie $categorie = null;

    public function getCategorie(): ?Categorie { return $this->categorie; }
    public function setCategorie(?Categorie $categorie): self { $this->categorie = $categorie; return $this; }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Relation ManyToMany (articles et tags)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Tag.php
#[ORM\Entity]
class Tag
{
    #[ORM\Id, ORM\GeneratedValue, ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 50)]
    private ?string $nom = null;

    #[ORM\ManyToMany(targetEntity: Article::class, mappedBy: 'tags')]
    private Collection $articles;
}

// Dans Article.php
#[ORM\ManyToMany(targetEntity: Tag::class, inversedBy: 'articles')]
#[ORM\JoinTable(name: 'article_tag')]
private Collection $tags;

public function __construct() {
    $this->tags = new ArrayCollection();
}

public function addTag(Tag $tag): self {
    if (!$this->tags->contains($tag)) {
        $this->tags->add($tag);
    }
    return $this;
}
public function removeTag(Tag $tag): self { ... }</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Générer les migrations après ajout de relations</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:migration
php bin/console doctrine:migrations:migrate</code></pre>
                    </div>
                </div>
            </section>

            <!-- Événements de cycle de vie -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Événements de cycle de vie (Lifecycle Callbacks)</h2>

                <div class="textExemple">
                    <p>
                        Doctrine permet d'exécuter du code automatiquement avant ou après certaines actions
                        (persist, update, remove) grâce aux <strong>attributs</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity]
#[ORM\HasLifecycleCallbacks]  // Active les callbacks
class Article
{
    #[ORM\Column(type: 'datetime')]
    private ?\DateTimeInterface $createdAt = null;

    #[ORM\Column(type: 'datetime', nullable: true)]
    private ?\DateTimeInterface $updatedAt = null;

    #[ORM\PrePersist]
    public function setCreatedAtValue(): void
    {
        $this->createdAt = new \DateTimeImmutable();
    }

    #[ORM\PreUpdate]
    public function setUpdatedAtValue(): void
    {
        $this->updatedAt = new \DateTimeImmutable();
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Doctrine Extensions (Slug, Timestampable, etc.) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Extensions populaires : StofDoctrineExtensionsBundle</h2>

                <div class="textExemple">
                    <p>
                        Des fonctionnalités avancées (Slug, Timestampable, Tree, etc.) sont disponibles via l'extension
                        <strong>StofDoctrineExtensionsBundle</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require stof/doctrine-extensions-bundle</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/stof_doctrine_extensions.yaml
stof_doctrine_extensions:
    default_locale: fr_FR
    orm:
        default:
            timestampable: true
            sluggable: true</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Gedmo\Mapping\Annotation as Gedmo;

#[ORM\Entity]
class Article
{
    #[Gedmo\Slug(fields: ['titre'])]
    #[ORM\Column(length: 128, unique: true)]
    private ?string $slug = null;

    #[Gedmo\Timestampable(on: 'create')]
    #[ORM\Column(type: 'datetime')]
    private $createdAt;

    #[Gedmo\Timestampable(on: 'update')]
    #[ORM\Column(type: 'datetime')]
    private $updatedAt;
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec Doctrine</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Utilisez les repositories</strong> : centralisez la logique de requête dans les classes Repository.</li>
                        <li><strong>Évitez les requêtes N+1</strong> : utilisez <code>join</code> et <code>select</code> dans le QueryBuilder, ou l'index de jointure.</li>
                        <li><strong>Ne flush pas inutilement</strong> : un seul flush après plusieurs persist est plus performant.</li>
                        <li><strong>Validez les entités</strong> : utilisez le composant Validator de Symfony avant la persistance.</li>
                        <li><strong>Gérez les transactions</strong> : pour les opérations critiques, utilisez <code>$em->beginTransaction()</code>.</li>
                        <li><strong>Activez le cache de requêtes</strong> en production (doctrine cache).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Transaction explicite</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$em->beginTransaction();
try {
    $article = new Article();
    $em->persist($article);
    $comment = new Comment();
    $em->persist($comment);
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
                    <h3 class="text-purple">Exercice 1 : Création d'une entité "Produit"</h3>
                    <p>Créez une entité <code>Produit</code> avec les champs suivants :</p>
                    <ul>
                        <li>nom (string, 100, non null)</li>
                        <li>description (text, nullable)</li>
                        <li>prix (decimal, 10,2)</li>
                        <li>stock (integer)</li>
                        <li>createdAt (datetime, auto rempli au persist)</li>
                    </ul>
                    <p>Générez la migration et mettez à jour la base.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:entity Produit
# Suivre les instructions interactives
php bin/console make:migration
php bin/console doctrine:migrations:migrate</code></pre>
                            <pre v-pre><code class="language-php">// src/Entity/Produit.php (extrait)
#[ORM\Entity]
class Produit
{
    #[ORM\Column(length: 100)]
    private ?string $nom = null;

    #[ORM\Column(type: 'text', nullable: true)]
    private ?string $description = null;

    #[ORM\Column(type: 'decimal', precision: 10, scale: 2)]
    private ?string $prix = null;

    #[ORM\Column]
    private ?int $stock = null;

    #[ORM\Column(type: 'datetime')]
    private ?\DateTimeInterface $createdAt = null;

    #[ORM\PrePersist]
    public function setCreatedAtValue(): void
    {
        $this->createdAt = new \DateTime();
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Relation OneToMany / ManyToOne</h3>
                    <p>Ajoutez une entité <code>Categorie</code> (nom, description).</p>
                    <p>Reliez chaque produit à une catégorie (ManyToOne). Une catégorie peut avoir plusieurs produits.</p>
                    <p>Créez une méthode dans le repository <code>ProduitRepository</code> pour récupérer les produits d'une catégorie donnée.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Entity/Categorie.php
#[ORM\Entity]
class Categorie
{
    #[ORM\Id, ORM\GeneratedValue, ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 100)]
    private ?string $nom = null;

    #[ORM\OneToMany(mappedBy: 'categorie', targetEntity: Produit::class)]
    private Collection $produits;
}

// Dans Produit.php
#[ORM\ManyToOne(inversedBy: 'produits')]
#[ORM\JoinColumn(nullable: false)]
private ?Categorie $categorie = null;

// Dans ProduitRepository
public function findByCategorie(Categorie $categorie): array
{
    return $this->createQueryBuilder('p')
        ->where('p.categorie = :cat')
        ->setParameter('cat', $categorie)
        ->getQuery()
        ->getResult();
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Requête avancée avec QueryBuilder</h3>
                    <p>Créez une méthode <code>findProduitsEnStockEtPrixSuperieur($prixMin)</code> qui retourne les produits dont le stock > 0 et le prix >= $prixMin, triés par prix décroissant.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">public function findProduitsEnStockEtPrixSuperieur(float $prixMin): array
{
    return $this->createQueryBuilder('p')
        ->where('p.stock > 0')
        ->andWhere('p.prix >= :prix')
        ->setParameter('prix', $prixMin)
        ->orderBy('p.prix', 'DESC')
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
                        Doctrine ORM est un outil puissant qui vous permet de travailler avec votre base de données
                        de manière objet, en écrivant très peu de SQL. Avec les entités, les migrations, les repositories
                        et le QueryBuilder, vous maîtrisez l'intégralité du cycle de vie des données.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous approfondirons les <strong>événements Doctrine</strong>,
                        les <strong>types personnalisés</strong> et l'<strong>optimisation des performances</strong>
                        (cache, index, lazy loading).
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'DoctrineLesson',

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
                    // Charger les langages PHP, Twig, Bash, YAML
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