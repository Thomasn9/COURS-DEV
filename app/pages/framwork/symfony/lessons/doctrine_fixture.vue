<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Doctrine Fixtures dans Symfony</h1>
                <p class="lesson-meta text-white">PHP • Symfony • Doctrine • Fixtures • Faker</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Fixtures</h2>
                <p class="textExemple">
                    Les fixtures (ou données de test) sont un moyen d’insérer des données factices dans votre base de données
                    à des fins de développement ou de tests. Elles permettent de disposer d’un jeu de données cohérent et reproductible,
                    que ce soit pour démarrer un projet, effectuer des tests fonctionnels ou démonstrations.
                </p>
                <p class="textExemple">
                    Symfony intègre via le bundle <strong>DoctrineFixturesBundle</strong> un système puissant pour définir et charger
                    ces données de manière orientée objet, avec la possibilité de gérer les dépendances entre les différentes entités.
                </p>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et configuration</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Installer le bundle de fixtures</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer DoctrineFixturesBundle (toujours en --dev)
composer require --dev doctrine/doctrine-fixtures-bundle

# Installer FakerPHP pour générer des données réalistes (optionnel mais recommandé)
composer require --dev fakerphp/faker</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Vérification de l’installation</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Lister les commandes disponibles
php bin/console list doctrine:fixtures

# Devrait afficher :
# doctrine:fixtures:load   Load data fixtures to your database</code></pre>
                    </div>
                    <p>Le bundle est automatiquement activé. Aucune configuration supplémentaire n’est requise dans la plupart des cas.</p>
                </div>
            </section>

            <!-- Création d’une fixture simple -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer une première fixture</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Structure d’une classe de fixture</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/DataFixtures/ArticleFixtures.php
namespace App\DataFixtures;

use App\Entity\Article;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;

class ArticleFixtures extends Fixture
{
    public function load(ObjectManager $manager): void
    {
        // Créer 10 articles factices
        for ($i = 1; $i <= 10; $i++) {
            $article = new Article();
            $article->setTitre("Article n°$i");
            $article->setContenu("Ceci est le contenu de l'article $i.");
            $article->setPublishedAt(new \DateTimeImmutable("-$i days"));

            $manager->persist($article);
        }

        $manager->flush();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Générer une fixture via la console (MakerBundle)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer MakerBundle si ce n’est pas déjà fait
composer require --dev symfony/maker-bundle

# Générer une fixture pour une entité
php bin/console make:fixture ArticleFixtures

# Le fichier est créé dans src/DataFixtures/ArticleFixtures.php</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utiliser Faker pour des données réalistes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Générer des données réalistes avec Faker</h2>

                <div class="textExemple">
                    <p>
                        <strong>Faker</strong> est une bibliothèque qui génère des données factices de manière réaliste :
                        noms, adresses, paragraphes, emails, dates, etc. Elle est parfaitement adaptée aux fixtures.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/DataFixtures/ArticleFixtures.php
namespace App\DataFixtures;

use App\Entity\Article;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;
use Faker\Factory;

class ArticleFixtures extends Fixture
{
    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR'); // Localisation française

        for ($i = 0; $i < 20; $i++) {
            $article = new Article();
            $article->setTitre($faker->sentence(5));
            $article->setContenu($faker->paragraphs(3, true));
            $article->setPublishedAt($faker->dateTimeBetween('-6 months', 'now'));
            $article->setEmail($faker->email());

            $manager->persist($article);
        }

        $manager->flush();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples de données générées par Faker</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->name();               // "Jean Dupont"
$faker->firstName();          // "Sophie"
$faker->lastName();           // "Martin"
$faker->email();              // "dupont@example.org"
$faker->sentence(3);          // "Incidunt ut necessitatibus."
$faker->paragraph(2);         // Paragraphe de deux phrases
$faker->numberBetween(0, 100); // 42
$faker->imageUrl(640, 480);   // "https://picsum.photos/id/1/640/480"
$faker->dateTimeBetween('-1 year', 'now'); // Objet DateTime
$faker->boolean(70);          // true avec 70% de chance
$faker->unique()->email;      // Évite les doublons</code></pre>
                    </div>
                </div>
            </section>

            <!-- Relations entre entités -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gérer les relations entre entités</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Fixture avec référence et dépendance</h3>
                    <p>
                        Lorsqu’une entité possède une relation (ManyToOne, ManyToMany), il faut référencer d’autres fixtures.
                        DoctrineFixturesBundle offre un système de <strong>références</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/DataFixtures/CategorieFixtures.php
namespace App\DataFixtures;

use App\Entity\Categorie;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;

class CategorieFixtures extends Fixture
{
    public function load(ObjectManager $manager): void
    {
        $categories = ['Technologie', 'Santé', 'Sport', 'Politique'];

        foreach ($categories as $index => $nom) {
            $categorie = new Categorie();
            $categorie->setNom($nom);
            $manager->persist($categorie);

            // Enregistrer une référence pour l'utiliser ailleurs
            $this->addReference('categorie_' . $index, $categorie);
        }

        $manager->flush();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/DataFixtures/ArticleFixtures.php
namespace App\DataFixtures;

use App\Entity\Article;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Common\DataFixtures\DependentFixtureInterface;
use Doctrine\Persistence\ObjectManager;
use Faker\Factory;

class ArticleFixtures extends Fixture implements DependentFixtureInterface
{
    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR');

        for ($i = 0; $i < 50; $i++) {
            $article = new Article();

            // Récupérer une catégorie aléatoire parmi celles enregistrées
            $randomCategorie = $this->getReference('categorie_' . rand(0, 3));
            $article->setCategorie($randomCategorie);

            // ... autres setters
            $manager->persist($article);
        }

        $manager->flush();
    }

    // Indique que cette fixture dépend de CategorieFixtures
    public function getDependencies(): array
    {
        return [CategorieFixtures::class];
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Relation ManyToMany avec références multiples</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Ajouter des tags à un article
$tag1 = $this->getReference('tag_1');
$tag2 = $this->getReference('tag_2');
$article->addTag($tag1);
$article->addTag($tag2);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Chargement des fixtures -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Charger les fixtures</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Commande de base</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Charge toutes les fixtures (purge la base avant)
php bin/console doctrine:fixtures:load

# ATTENTION : Cette opération efface toutes les données existantes !
# Confirmation interactive : tapez "yes"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Options importantes</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Ne pas purger la base (ajouter les fixtures aux données existantes)
php bin/console doctrine:fixtures:load --append

# Exécuter uniquement certaines fixtures (grâce aux groupes)
php bin/console doctrine:fixtures:load --group=dev
php bin/console doctrine:fixtures:load --group=test

# Désactiver la confirmation interactive
php bin/console doctrine:fixtures:load --no-interaction

# Spécifier un gestionnaire d’entité particulier (pour plusieurs connexions)
php bin/console doctrine:fixtures:load --em=default</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser les groupes dans les fixtures</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans la classe de fixture
public static function getGroups(): array
{
    return ['dev', 'test']; // Cette fixture sera chargée uniquement pour ces groupes
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Purge personnalisée -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Contrôler la purge des données</h2>

                <div class="textExemple">
                    <p>
                        Par défaut, <code>doctrine:fixtures:load</code> supprime toutes les lignes de toutes les tables.
                        Vous pouvez personnaliser ce comportement via l’option <code>--purge-with-truncate</code> ou en implémentant
                        une stratégie de purge.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Utiliser TRUNCATE au lieu de DELETE (plus rapide mais réinitialise les auto-incréments)
php bin/console doctrine:fixtures:load --purge-with-truncate</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exclure certaines tables de la purge</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/doctrine_fixtures.yaml
doctrine_fixtures:
    purge_with_truncate: true
    fixtures:
        - App\DataFixtures\DevFixtures
    groups:
        dev: [App\DataFixtures\DevFixtures]
    exclude_tables: [migration_versions, user_log]</code></pre>
                    </div>
                </div>
            </section>

            <!-- Fixtures dans l’environnement de test -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fixtures pour les tests fonctionnels</h2>

                <div class="textExemple">
                    <p>
                        Dans un contexte de test (PHPUnit), les fixtures permettent de préparer un état initial connu.
                        Symfony fournit une <strong>trait</strong> pour charger les fixtures directement depuis un test.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// tests/Controller/ArticleControllerTest.php
namespace App\Tests\Controller;

use Symfony\Bundle\FrameworkBundle\Test\WebTestCase;
use Doctrine\Common\DataFixtures\Executor\ORMExecutor;
use Doctrine\Common\DataFixtures\Purger\ORMPurger;
use Doctrine\Common\DataFixtures\Loader;
use App\DataFixtures\ArticleFixtures;

class ArticleControllerTest extends WebTestCase
{
    protected function setUp(): void
    {
        parent::setUp();
        $this->loadFixtures();
    }

    private function loadFixtures(): void
    {
        $em = self::getContainer()->get('doctrine')->getManager();

        $loader = new Loader();
        $loader->addFixture(new ArticleFixtures());

        $purger = new ORMPurger($em);
        $executor = new ORMExecutor($em, $purger);
        $executor->execute($loader->getFixtures());
    }

    public function testArticleIndex(): void
    {
        $client = static::createClient();
        $crawler = $client->request('GET', '/articles');

        $this->assertResponseIsSuccessful();
        $this->assertSelectorTextContains('h1', 'Liste des articles');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Trait <code>FixtureTrait</code> (plus simple)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Bundle\FrameworkBundle\Test\KernelTestCase;
use Doctrine\Common\DataFixtures\Purger\ORMPurger;
use Liip\TestFixturesBundle\Services\DatabaseToolCollection; // Avec LiipTestFixturesBundle

// Installation recommandée pour les tests : 
composer require --dev liip/test-fixtures-bundle

// Dans le test
public function testWithFixtures(): void
{
    $databaseTool = $this->getContainer()->get(DatabaseToolCollection::class)->get();
    $databaseTool->loadFixtures([ArticleFixtures::class]);

    // Votre test...
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques et conseils</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Séparer les fixtures par environnement</strong> : utilisez les groupes (<code>dev</code>, <code>test</code>, <code>prod</code>).</li>
                        <li><strong>Ne jamais charger de fixtures en production</strong> : le bundle est installé en <code>--dev</code> et ne devrait pas être présent sur l'environnement de production.</li>
                        <li><strong>Utiliser Faker systématiquement</strong> : cela rend les données plus réalistes et évite les biais.</li>
                        <li><strong>Gérer les dépendances explicitement</strong> : implémentez <code>DependentFixtureInterface</code> pour assurer l’ordre de chargement.</li>
                        <li><strong>Réinitialiser les séquences / auto-incréments</strong> : utilisez <code>--purge-with-truncate</code> en développement.</li>
                        <li><strong>Ne pas hardcoder d’IDs</strong> : utilisez les références (<code>addReference()</code> / <code>getReference()</code>).</li>
                        <li><strong>Fixtures volumineuses</strong> : pour plus de 1000 entités, utilisez <code>batchSize</code> ou le pattern "chunk" pour éviter l’épuisement mémoire.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple avec batch (optimisation mémoire)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">for ($i = 0; $i < 10000; $i++) {
    $article = new Article();
    // ... set data
    $manager->persist($article);

    if ($i % 500 === 0) {
        $manager->flush();
        $manager->clear(); // Détache tous les objets persistés
    }
}
$manager->flush();</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Fixtures pour un blog</h3>
                    <p>Créez les fixtures suivantes pour un blog Symfony :</p>
                    <ul>
                        <li>10 catégories (noms uniques)</li>
                        <li>50 articles, chacun avec une catégorie aléatoire</li>
                        <li>20 tags (ex : "PHP", "Symfony", "Doctrine", etc.)</li>
                        <li>Chaque article possède entre 1 et 4 tags aléatoires (relation ManyToMany)</li>
                        <li>Utilisez Faker pour générer les titres, contenus, dates de publication</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/DataFixtures/TagFixtures.php
namespace App\DataFixtures;

use App\Entity\Tag;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;

class TagFixtures extends Fixture
{
    public function load(ObjectManager $manager): void
    {
        $tags = ['PHP', 'Symfony', 'Doctrine', 'JavaScript', 'React', 'Vue', 'CSS', 'SQL', 'Docker', 'Kubernetes'];

        foreach ($tags as $index => $nom) {
            $tag = new Tag();
            $tag->setNom($nom);
            $manager->persist($tag);
            $this->addReference('tag_' . $index, $tag);
        }

        $manager->flush();
    }
}

// src/DataFixtures/ArticleFixtures.php
namespace App\DataFixtures;

use App\Entity\Article;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Common\DataFixtures\DependentFixtureInterface;
use Doctrine\Persistence\ObjectManager;
use Faker\Factory;

class ArticleFixtures extends Fixture implements DependentFixtureInterface
{
    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR');
        $categories = [];
        for ($i = 0; $i < 10; $i++) {
            $categories[] = $this->getReference('categorie_' . $i);
        }

        $tags = [];
        for ($i = 0; $i < 20; $i++) {
            $tags[] = $this->getReference('tag_' . $i);
        }

        for ($i = 0; $i < 50; $i++) {
            $article = new Article();
            $article->setTitre($faker->sentence(6));
            $article->setContenu($faker->paragraphs(4, true));
            $article->setPublishedAt($faker->dateTimeBetween('-1 year', 'now'));
            $article->setCategorie($faker->randomElement($categories));

            // Tags aléatoires (entre 1 et 4)
            $randomTags = $faker->randomElements($tags, $faker->numberBetween(1, 4));
            foreach ($randomTags as $tag) {
                $article->addTag($tag);
            }

            $manager->persist($article);
        }

        $manager->flush();
    }

    public function getDependencies(): array
    {
        return [CategorieFixtures::class, TagFixtures::class];
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Fixtures pour un système d'utilisateurs</h3>
                    <p>Réalisez un jeu de fixtures pour gérer des utilisateurs avec profils :</p>
                    <ul>
                        <li>Créez 10 utilisateurs (nom, email, mot de passe hashé via <code>UserPasswordHasherInterface</code>)</li>
                        <li>Attribuez des rôles (<code>ROLE_USER</code>, <code>ROLE_ADMIN</code>) à certains utilisateurs</li>
                        <li>Chaque utilisateur possède entre 0 et 5 articles (relation OneToMany)</li>
                        <li>Utilisez une référence pour réutiliser l’utilisateur admin dans d’autres fixtures</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/DataFixtures/UserFixtures.php
namespace App\DataFixtures;

use App\Entity\User;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;
use Symfony\Component\PasswordHasher\Hasher\UserPasswordHasherInterface;
use Faker\Factory;

class UserFixtures extends Fixture
{
    private $passwordHasher;

    public function __construct(UserPasswordHasherInterface $passwordHasher)
    {
        $this->passwordHasher = $passwordHasher;
    }

    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR');

        // Admin
        $admin = new User();
        $admin->setEmail('admin@example.com');
        $admin->setRoles(['ROLE_ADMIN']);
        $admin->setPassword($this->passwordHasher->hashPassword($admin, 'admin123'));
        $manager->persist($admin);
        $this->addReference('user_admin', $admin);

        // Utilisateurs normaux
        for ($i = 0; $i < 9; $i++) {
            $user = new User();
            $user->setEmail($faker->unique()->email());
            $user->setRoles(['ROLE_USER']);
            $user->setPassword($this->passwordHasher->hashPassword($user, 'password'));
            $manager->persist($user);
            $this->addReference('user_' . $i, $user);
        }

        $manager->flush();
    }
}

// src/DataFixtures/ArticleWithUserFixtures.php
namespace App\DataFixtures;

use App\Entity\Article;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Common\DataFixtures\DependentFixtureInterface;
use Doctrine\Persistence\ObjectManager;
use Faker\Factory;

class ArticleWithUserFixtures extends Fixture implements DependentFixtureInterface
{
    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR');
        $users = [];

        // Récupérer tous les utilisateurs (admin inclus)
        for ($i = 0; $i < 10; $i++) {
            $users[] = $this->getReference($i === 0 ? 'user_admin' : 'user_' . ($i - 1));
        }

        for ($i = 0; $i < 30; $i++) {
            $article = new Article();
            $article->setTitre($faker->sentence(5));
            $article->setContenu($faker->paragraphs(2, true));
            $article->setPublishedAt($faker->dateTimeBetween('-6 months', 'now'));
            $article->setAuteur($faker->randomElement($users));

            $manager->persist($article);
        }

        $manager->flush();
    }

    public function getDependencies(): array
    {
        return [UserFixtures::class];
    }
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
                        Les fixtures sont un outil indispensable pour tout développeur Symfony. Elles permettent de :
                    </p>
                    <ul>
                        <li>Disposer rapidement d’un environnement de développement réaliste,</li>
                        <li>Écrire des tests fonctionnels fiables et reproductibles,</li>
                        <li>Démontrer des fonctionnalités sans polluer la base de production.</li>
                    </ul>
                    <p>
                        En combinant <strong>DoctrineFixturesBundle</strong> et <strong>Faker</strong>, vous gagnez un temps précieux
                        et évitez les saisies manuelles fastidieuses.
                    </p>
                    <p>
                        <strong>Prochaines étapes</strong> : Découvrez comment utiliser les fixtures avec <strong>AliceBundle</strong>
                        (définition en YAML) ou intégrez les fixtures dans votre pipeline d’intégration continue.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyFixturesLesson',

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
                    // Charger les langages PHP, Twig et Bash
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const twigScript = document.createElement('script');
                        twigScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/twig.min.js';
                        twigScript.onload = () => {
                            const bashScript = document.createElement('script');
                            bashScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/bash.min.js';
                            bashScript.onload = resolve;
                            document.head.appendChild(bashScript);
                        };
                        document.head.appendChild(twigScript);
                    };
                    document.head.appendChild(phpScript);
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