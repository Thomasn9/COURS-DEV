<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Faker – Générateur de données factices</h1>
                <p class="lesson-meta text-white">PHP • Faker • Données de test • Fixtures Symfony</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que Faker ?</h2>
                <p class="textExemple">
                    <strong>Faker</strong> est une bibliothèque PHP qui génère des données factices réalistes : noms, adresses, textes, emails, dates,
                    numéros de téléphone, etc. Elle est essentielle pour peupler vos bases de données de développement,
                    écrire des tests fonctionnels ou créer des démonstrations sans avoir à saisir manuellement des données.
                </p>
                <p class="textExemple">
                    Dans l'écosystème Symfony, Faker est souvent utilisé avec <strong>DoctrineFixturesBundle</strong>
                    pour produire des jeux de données cohérents et variés, en quelques lignes de code.
                </p>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Via Composer</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installation classique (généralement en --dev)
composer require --dev fakerphp/faker

# Ou pour une utilisation en production (rare)
composer require fakerphp/faker</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Installation avec Symfony (recommandée)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Créer un projet Symfony
symfony new mon-projet --webapp

# Ajouter Faker et les fixtures
composer require --dev doctrine/doctrine-fixtures-bundle
composer require --dev fakerphp/faker</code></pre>
                    </div>
                    <p>Faker est automatiquement disponible dans vos classes de fixtures.</p>
                </div>
            </section>

            <!-- Premiers pas -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Premiers pas avec Faker</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation basique</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">require_once 'vendor/autoload.php';

use Faker\Factory;

$faker = Factory::create('fr_FR'); // Localisation française

echo $faker->name();           // "Sophie Martin"
echo $faker->email();          // "dupont@example.org"
echo $faker->sentence();       // "Incidunt ut necessitatibus."
echo $faker->numberBetween(1, 100); // 42</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les localisations disponibles</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Français
$faker = Factory::create('fr_FR');
$faker->name();    // "Jean Dupont"

// Anglais US
$faker = Factory::create('en_US');
$faker->name();    // "John Smith"

// Allemand
$faker = Factory::create('de_DE');

// Espagnol
$faker = Factory::create('es_ES');

// Liste complète : https://github.com/fzaninotto/Faker#localization</code></pre>
                    </div>
                </div>
            </section>

            <!-- Formateurs (formatters) essentiels -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les formateurs (formatters) essentiels</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Textes et chaînes</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->word();                 // "molestiae"
$faker->words(3);               // ["porro", "sed", "magni"]
$faker->sentence($nbWords = 6); // "Amet et laboriosam magnam."
$faker->sentences(3);           // Tableau de 3 phrases
$faker->paragraph($nbSentences = 3); // Paragraphe
$faker->paragraphs(2);          // Tableau de 2 paragraphes
$faker->text($maxNbChars = 200); // Texte court</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Noms et identités</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->firstName();            // "Julie"
$faker->lastName();             // "Bernard"
$faker->name();                 // "Julie Bernard"
$faker->title();                // "Dr."
$faker->titleFemale();          // "Mme" (fr_FR)</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Coordonnées</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->email();                // "lefevre@example.com"
$faker->safeEmail();            // "sophie.martin@example.org"
$faker->phoneNumber();          // "06 12 34 56 78"
$faker->address();              // "47 rue du Faubourg, 75010 Paris"
$faker->city();                 // "Lyon"
$faker->postcode();             // "75001"
$faker->country();              // "France"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Dates et heures</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->date();                 // "2023-05-12"
$faker->dateTime();             // DateTime (maintenant)
$faker->dateTimeBetween('-1 year', 'now'); // Entre -1 an et aujourd'hui
$faker->dateTimeThisYear();     // Dans l'année courante
$faker->dateTimeThisMonth();    // Dans le mois courant
$faker->time();                 // "14:32:45"
$faker->unixTime();             // 1683895742</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Nombres et booléens</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->randomNumber(3);        // 3 chiffres (ex: 542)
$faker->numberBetween(10, 20);  // Entier entre 10 et 20
$faker->randomFloat(2, 0, 100); // Flottant avec 2 décimales (ex: 34.56)
$faker->boolean(70);            // true avec 70% de chance
$faker->randomDigit();          // 0-9
$faker->randomDigitNotNull();   // 1-9</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Médias et fichiers</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->imageUrl(640, 480);     // "https://picsum.photos/id/1/640/480"
$faker->image('public/uploads', 640, 480, null, false);
// Télécharge une vraie image et la sauvegarde

$faker->fileExtension();        // "jpg"
$faker->mimeType();             // "image/jpeg"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Identifiants uniques</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->uuid();                 // UUID v4
$faker->md5();                  // MD5 hash
$faker->sha1();                 // SHA1 hash
$faker->unique()->email;        // Évite les doublons</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utilisation avancée -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation avancée</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Générer des valeurs uniques</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Méthode unique() garantit qu'une valeur ne sera pas répétée
for ($i = 0; $i < 10; $i++) {
    echo $faker->unique()->email . "\n";
}
// 10 emails distincts

// Réinitialiser l'unicité
$faker->unique($reset = true);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Prendre un élément aléatoire dans un tableau</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$statuses = ['pending', 'approved', 'rejected'];
$status = $faker->randomElement($statuses);

// Plusieurs éléments aléatoires
$tags = ['php', 'symfony', 'doctrine', 'twig'];
$randomTags = $faker->randomElements($tags, 2); // 2 tags aléatoires</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Formater une chaîne selon un motif</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Remplacer '#' par un chiffre, '?' par une lettre
$faker->numerify('###-###-###'); // "123-456-789"
$faker->lexify('????');          // "abcd"
$faker->bothify('##??');         // "12ab"</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer ses propres formateurs</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$faker->addProvider(new class($faker) extends \Faker\Provider\Base {
    public function productName(): string
    {
        $products = ['Smartphone', 'Laptop', 'Tablet', 'Monitor'];
        return $this->generator->randomElement($products);
    }
});

echo $faker->productName(); // "Laptop"</code></pre>
                    </div>
                </div>
            </section>

            <!-- Faker avec Doctrine Fixtures (Symfony) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Intégration avec Symfony et Doctrine Fixtures</h2>

                <div class="textExemple">
                    <p>
                        L'utilisation la plus courante de Faker dans Symfony est au sein des classes de fixtures.
                        Voici un exemple complet de fixtures pour une entité <code>Article</code>.
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
        $faker = Factory::create('fr_FR');

        for ($i = 0; $i < 50; $i++) {
            $article = new Article();
            $article->setTitre($faker->sentence(5));
            $article->setContenu($faker->paragraphs(3, true));
            $article->setPublishedAt($faker->dateTimeBetween('-6 months', 'now'));
            $article->setVues($faker->numberBetween(0, 1000));
            $article->setActif($faker->boolean(80));

            $manager->persist($article);
        }

        $manager->flush();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Fixtures avec relations (ManyToOne)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/DataFixtures/ArticleFixtures.php (avec dépendances)
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

        // Récupérer toutes les catégories créées par CategorieFixtures
        $categories = [];
        for ($i = 0; $i < 10; $i++) {
            $categories[] = $this->getReference('categorie_' . $i);
        }

        for ($i = 0; $i < 100; $i++) {
            $article = new Article();
            $article->setTitre($faker->sentence(6));
            $article->setContenu($faker->paragraphs(4, true));
            $article->setCategorie($faker->randomElement($categories));
            $article->setPublishedAt($faker->dateTimeBetween('-1 year', 'now'));

            $manager->persist($article);
        }

        $manager->flush();
    }

    public function getDependencies(): array
    {
        return [CategorieFixtures::class];
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Fixtures avec ManyToMany et tags</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Récupérer les tags
$tags = [];
for ($i = 0; $i < 20; $i++) {
    $tags[] = $this->getReference('tag_' . $i);
}

// Dans la boucle des articles
$article->setTitre($faker->sentence(5));
$randomTags = $faker->randomElements($tags, $faker->numberBetween(1, 4));
foreach ($randomTags as $tag) {
    $article->addTag($tag);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Utilisation en dehors des fixtures -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utiliser Faker ailleurs que dans les fixtures</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Dans un service Symfony</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Service/FakerService.php
namespace App\Service;

use Faker\Factory;
use Faker\Generator;

class FakerService
{
    private Generator $faker;

    public function __construct()
    {
        $this->faker = Factory::create('fr_FR');
    }

    public function generateRandomUserData(): array
    {
        return [
            'firstName' => $this->faker->firstName(),
            'lastName'  => $this->faker->lastName(),
            'email'     => $this->faker->email(),
            'phone'     => $this->faker->phoneNumber(),
        ];
    }

    // Autres méthodes...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Dans un test unitaire ou fonctionnel</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// tests/Entity/ArticleTest.php
use Faker\Factory;

class ArticleTest extends TestCase
{
    public function testArticleTitleIsValid(): void
    {
        $faker = Factory::create('fr_FR');
        $article = new Article();
        $article->setTitre($faker->sentence(5));

        $this->assertLessThanOrEqual(255, strlen($article->getTitre()));
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Commande Symfony personnalisée pour générer des utilisateurs</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Command/GenerateUsersCommand.php
namespace App\Command;

use App\Entity\User;
use Doctrine\ORM\EntityManagerInterface;
use Faker\Factory;
use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputArgument;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;

class GenerateUsersCommand extends Command
{
    protected static $defaultName = 'app:generate-users';

    private $em;

    public function __construct(EntityManagerInterface $em)
    {
        $this->em = $em;
        parent::__construct();
    }

    protected function configure(): void
    {
        $this->addArgument('count', InputArgument::REQUIRED, 'Number of users to generate');
    }

    protected function execute(InputInterface $input, OutputInterface $output): int
    {
        $count = $input->getArgument('count');
        $faker = Factory::create('fr_FR');

        for ($i = 0; $i < $count; $i++) {
            $user = new User();
            $user->setEmail($faker->unique()->email());
            $user->setFirstName($faker->firstName());
            $user->setLastName($faker->lastName());
            $this->em->persist($user);
        }

        $this->em->flush();
        $output->writeln("Generated $count users.");

        return Command::SUCCESS;
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Faker dans d'autres contextes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Faker sans Symfony (projet PHP pur)</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// script.php
require_once 'vendor/autoload.php';

use Faker\Factory;

$faker = Factory::create('fr_FR');

// Générer 100 faux profils et les exporter en CSV
$fp = fopen('fake_users.csv', 'w');
fputcsv($fp, ['Prénom', 'Nom', 'Email']);

for ($i = 0; $i < 100; $i++) {
    fputcsv($fp, [
        $faker->firstName(),
        $faker->lastName(),
        $faker->email()
    ]);
}
fclose($fp);

echo "CSV généré avec succès.\n";</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec Faker</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Localisez vos données</strong> : utilisez <code>Factory::create('fr_FR')</code> pour obtenir des noms, adresses français réalistes.</li>
                        <li><strong>Évitez les boucles trop grandes</strong> : au-delà de 1000 entités, utilisez <code>flush()</code> et <code>clear()</code> par lots pour ne pas saturer la mémoire.</li>
                        <li><strong>Utilisez <code>unique()</code> avec parcimonie</strong> : il maintient un historique des valeurs, ce qui peut ralentir les grosses générations.</li>
                        <li><strong>Ne stockez pas Faker en propriété de classe dans les fixtures</strong> : créez une instance locale dans <code>load()</code>.</li>
                        <li><strong>Pour des données plus complexes, combinez plusieurs formateurs</strong> : ex. <code>$faker->firstName() . ' ' . $faker->lastName()</code>.</li>
                        <li><strong>Utilisez <code>randomElement()</code> pour simuler des choix réalistes</strong> : statuts, catégories, tags, etc.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Optimisation mémoire dans les fixtures</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">for ($i = 0; $i < 5000; $i++) {
    $article = new Article();
    // ... remplir l'article
    $manager->persist($article);

    if ($i % 500 === 0) {
        $manager->flush();
        $manager->clear(); // Libère la mémoire
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
                    <h3 class="text-purple">Exercice 1 : Génération d'un catalogue produits</h3>
                    <p>Créez un script PHP utilisant Faker pour générer 200 produits factices. Chaque produit possède :</p>
                    <ul>
                        <li>Un nom (entre 2 et 5 mots)</li>
                        <li>Une description (2 à 4 paragraphes)</li>
                        <li>Un prix (décimal entre 5 et 500, avec 2 décimales)</li>
                        <li>Un code référence (lettres + chiffres, ex : "PROD-1234")</li>
                        <li>Une date d'ajout (entre -2 ans et maintenant)</li>
                        <li>Un booléen "en stock" (80% de chances d'être vrai)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">require_once 'vendor/autoload.php';

use Faker\Factory;

$faker = Factory::create('fr_FR');
$products = [];

for ($i = 0; $i < 200; $i++) {
    $products[] = [
        'name'        => $faker->words(rand(2, 5), true),
        'description' => $faker->paragraphs(rand(2, 4), true),
        'price'       => $faker->randomFloat(2, 5, 500),
        'reference'   => 'PROD-' . $faker->unique()->numerify('####'),
        'added_at'    => $faker->dateTimeBetween('-2 years', 'now')->format('Y-m-d H:i:s'),
        'in_stock'    => $faker->boolean(80),
    ];
}

// Export JSON
file_put_contents('products.json', json_encode($products, JSON_PRETTY_PRINT));
echo "200 produits générés dans products.json\n";</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Fixtures Symfony avec relations complexes</h3>
                    <p>En vous basant sur les entités suivantes, écrivez les fixtures nécessaires :</p>
                    <ul>
                        <li><strong>Client</strong> (nom, email, adresse, date d'inscription)</li>
                        <li><strong>Commande</strong> (client, date, montant total, statut)</li>
                        <li><strong>LigneCommande</strong> (commande, produit, quantité, prix unitaire)</li>
                        <li>Générez 50 clients, chacun ayant entre 1 et 5 commandes, chaque commande ayant entre 1 et 4 lignes.</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/DataFixtures/ClientFixtures.php
namespace App\DataFixtures;

use App\Entity\Client;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;
use Faker\Factory;

class ClientFixtures extends Fixture
{
    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR');

        for ($i = 0; $i < 50; $i++) {
            $client = new Client();
            $client->setNom($faker->lastName());
            $client->setEmail($faker->unique()->email());
            $client->setAdresse($faker->address());
            $client->setDateInscription($faker->dateTimeBetween('-2 years', 'now'));

            $manager->persist($client);
            $this->addReference('client_' . $i, $client);
        }

        $manager->flush();
    }
}

// src/DataFixtures/CommandeFixtures.php
namespace App\DataFixtures;

use App\Entity\Commande;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Common\DataFixtures\DependentFixtureInterface;
use Doctrine\Persistence\ObjectManager;
use Faker\Factory;

class CommandeFixtures extends Fixture implements DependentFixtureInterface
{
    public function load(ObjectManager $manager): void
    {
        $faker = Factory::create('fr_FR');
        $statuses = ['pending', 'paid', 'shipped', 'delivered', 'cancelled'];

        // Récupérer tous les clients
        $clients = [];
        for ($i = 0; $i < 50; $i++) {
            $clients[] = $this->getReference('client_' . $i);
        }

        foreach ($clients as $client) {
            $nbCommandes = $faker->numberBetween(1, 5);
            for ($j = 0; $j < $nbCommandes; $j++) {
                $commande = new Commande();
                $commande->setClient($client);
                $commande->setDate($faker->dateTimeBetween($client->getDateInscription(), 'now'));
                $commande->setStatut($faker->randomElement($statuses));
                // Le montant total sera calculé via les lignes de commande
                $manager->persist($commande);
                $this->addReference('commande_' . uniqid(), $commande);
            }
        }

        $manager->flush();
    }

    public function getDependencies(): array
    {
        return [ClientFixtures::class];
    }
}

// src/DataFixtures/LigneCommandeFixtures.php (similaire avec Produit)</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <p>
                        Faker est un outil incontournable pour tout développeur PHP, que vous utilisiez Symfony ou non.
                        Il permet de :
                    </p>
                    <ul>
                        <li>Gagner un temps considérable lors de la création de données de test,</li>
                        <li>Rendre vos fixtures plus réalistes et donc vos tests plus pertinents,</li>
                        <li>Faciliter les démonstrations et le développement local.</li>
                    </ul>
                    <p>
                        Associé à <strong>DoctrineFixturesBundle</strong>, il forme un duo redoutable pour préparer votre base
                        de données en quelques secondes. N'hésitez pas à explorer la <a href="https://fakerphp.github.io/" target="_blank" class="text-purple">documentation officielle</a>
                        pour découvrir tous les formateurs disponibles.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'FakerLesson',

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