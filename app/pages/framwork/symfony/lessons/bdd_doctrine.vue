<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Créer et Utiliser une Base de Données avec Doctrine dans Symfony avec données factice </h1>
                <p class="lesson-meta text-white">Maîtrisez les entités, les migrations et les fixtures pour persister vos données</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Doctrine ORM</h2>
                <p class="textExemple">
                    Doctrine est l'ORM (Object-Relational Mapping) par défaut de Symfony. Il vous permet de travailler avec des bases de données 
                    relationnelles en utilisant des objets PHP plutôt que d'écrire du SQL directement.
                </p>
                <p class="textExemple">
                    Cette leçon vous guidera à travers les étapes essentielles : création de base de données, entités, migrations et peuplement avec des fixtures.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Flux de travail complet Doctrine</span>
Configuration → Entités → Migrations → Fixtures → Application fonctionnelle</code></pre>
                </div>
            </div>

            <!-- Les 4 étapes fondamentales -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 4 étapes fondamentales avec Doctrine</h2>
                <p class="textExemple">
                    Pour créer et utiliser une base de données dans Symfony, suivez ces quatre étapes essentielles :
                </p>
                <ol class="textExemple">
                    <li><strong>Créer la base de données</strong> avec <code>doctrine:database:create</code></li>
                    <li><strong>Générer les migrations</strong> avec <code>make:migration</code></li>
                    <li><strong>Exécuter les migrations</strong> avec <code>doctrine:migrations:migrate</code></li>
                    <li><strong>Peupler avec des fixtures</strong> avec <code>doctrine:fixtures:load</code></li>
                </ol>
            </div>

            <!-- Préparation initiale -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Préparation : Configuration et Installation</h2>
                
                <h3 class="text-purple">1. Installation des dépendances nécessaires</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Installer Doctrine ORM</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require symfony/orm-pack</span>

<span class="bash-comment"># Installer le Maker Bundle pour les commandes de génération</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev symfony/maker-bundle</span>

<span class="bash-comment"># Installer ORM-Fixtures pour les données de test</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev orm-fixtures</span>

<span class="bash-comment"># Installer FakerPHP pour générer des données réalistes</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev fakerphp/faker</span></code></pre>
                </div>

                <h3 class="text-purple">2. Configuration de la base de données</h3>
                <p class="textExemple">
                    Configurez votre connexion dans le fichier <code>.env</code> :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># .env - Exemple pour MySQL</span>
<span class="bash-highlight">DATABASE_URL="mysql://root:password@127.0.0.1:3306/mon_projet?serverVersion=8.0&charset=utf8mb4"</span>

<span class="bash-comment"># .env - Exemple pour SQLite (plus simple pour débuter)</span>
<span class="bash-comment"># DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"</span></code></pre>
                </div>
            </div>

            <!-- ÉTAPE 1 : Création de la base de données -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : Créer la base de données</h2>
                <p class="textExemple">
                    La première étape consiste à créer physiquement la base de données sur votre serveur.
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Commande pour créer la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Exécution de la commande :</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>

<span class="bash-success">Création de la base de données 'mon_projet' réussie</span>
<span class="bash-success">✓ Connexion établie avec succès</span>

<span class="bash-comment"># Vérifier que la base a été créée</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SHOW DATABASES"</span>

<span class="bash-comment"># Sortie attendue :</span>
<span class="bash-string">+--------------------+</span>
<span class="bash-string">| Database           |</span>
<span class="bash-string">+--------------------+</span>
<span class="bash-string">| information_schema |</span>
<span class="bash-string">| mon_projet         |</span>  <span class="bash-comment">← Votre base est là !</span>
<span class="bash-string">| mysql              |</span>
<span class="bash-string">| performance_schema |</span>
<span class="bash-string">| sys                |</span>
<span class="bash-string">+--------------------+</span></code></pre>
                </div>

                <h3 class="text-purple">Commandes associées utiles</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Supprimer la base de données (attention !)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:drop --force</span>

<span class="bash-comment"># Créer la base si elle n'existe pas déjà</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create --if-not-exists</span>

<span class="bash-comment"># Tester la connexion</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT 1"</span></code></pre>
                </div>

                <div class="code-example tip">
                    <h4 class="text-purple">Conseil pratique</h4>
                    <p class="textExemple">
                        Si vous obtenez une erreur de connexion, vérifiez :
                    </p>
                    <ul class="textExemple">
                        <li>Que votre serveur MySQL/MariaDB est démarré</li>
                        <li>Que les identifiants dans <code>.env</code> sont corrects</li>
                        <li>Que le port spécifié correspond à celui de votre serveur</li>
                    </ul>
                </div>
            </div>

            <!-- Création des entités -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pré-requis : Créer vos entités</h2>
                <p class="textExemple">
                    Avant de générer des migrations, vous devez créer vos entités (modèles de données).
                </p>

                <h3 class="text-purple">Création d'une entité Article</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Générer une nouvelle entité</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:entity</span>

<span class="bash-string">Comment voulez-vous nommer votre entité ?</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">Article</span>

<span class="bash-string">Voulez-vous ajouter de nouveaux champs ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Ajout des champs interactivement :</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">title</span>
<span class="bash-string">Type [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">string</span>
<span class="bash-string">Longueur [255] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">200</span>
<span class="bash-string">Nullable ? [no] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">no</span>

<span class="bash-string">Ajouter un autre champ ? [oui] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>
<span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">content</span>
<span class="bash-string">Type [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">text</span>

<span class="bash-string">Ajouter un autre champ ? [oui] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>
<span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">publishedAt</span>
<span class="bash-string">Type [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">datetime_immutable</span>
<span class="bash-string">Nullable ? [no] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Ajouter un autre champ ? [oui] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">non</span>

<span class="bash-success">Entité Article créée avec succès !</span>
<span class="bash-success">✓ Fichier : src/Entity/Article.php</span>
<span class="bash-success">✓ Repository : src/Repository/ArticleRepository.php</span></code></pre>
                </div>

                <h3 class="text-purple">Structure de l'entité générée</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// src/Entity/Article.php - Généré automatiquement</span>
<span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Entity</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Repository</span>\<span class="php-class">ArticleRepository</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">ORM</span>\<span class="php-class">Mapping</span> <span class="php-keyword">as</span> <span class="php-class">ORM</span>;

#[<span class="php-class">ORM</span>\<span class="php-function">Entity</span>(<span class="php-variable">repositoryClass</span>: <span class="php-class">ArticleRepository</span>::<span class="php-keyword">class</span>)]
<span class="php-keyword">class</span> <span class="php-class">Article</span>
{
    #[<span class="php-class">ORM</span>\<span class="php-function">Id</span>]
    #[<span class="php-class">ORM</span>\<span class="php-function">GeneratedValue</span>]
    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>]
    <span class="php-keyword">private</span> ?<span class="php-keyword">int</span> <span class="php-variable">$id</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">length</span>: <span class="php-number">200</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$title</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">type</span>: <span class="php-string">'text'</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$content</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">type</span>: <span class="php-string">'datetime_immutable'</span>, <span class="php-variable">nullable</span>: <span class="php-keyword">true</span>)]
    <span class="php-keyword">private</span> ?\<span class="php-class">DateTimeImmutable</span> <span class="php-variable">$publishedAt</span> = <span class="php-keyword">null</span>;

    <span class="php-comment">// Getters et setters générés automatiquement...</span>
}</code></pre>
                </div>
            </div>

            <!-- ÉTAPE 2 : Génération des migrations -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Générer les migrations</h2>
                <p class="textExemple">
                    Les migrations sont des fichiers qui décrivent les modifications à apporter à votre schéma de base de données.
                    Elles permettent de versionner et de répliquer votre structure de base de données.
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Commande pour générer une migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Exécution de la commande :</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration</span>

<span class="bash-success">Migration générée avec succès</span>
<span class="bash-success">✓ Fichier : migrations/Version20240115120000.php</span>

<span class="bash-comment"># Voir le SQL qui sera exécuté</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:diff --dry-run</span>

<span class="bash-comment"># Sortie :</span>
<span class="bash-string">-- CREATE TABLE article (id INT AUTO_INCREMENT NOT NULL, title VARCHAR(200) NOT NULL, ...)</span></code></pre>
                </div>

                <h3 class="text-purple">Contenu du fichier de migration généré</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">declare</span>(<span class="php-variable">strict_types</span>=<span class="php-number">1</span>);

<span class="php-keyword">namespace</span> DoctrineMigrations;

<span class="php-keyword">use</span> Doctrine\<span class="php-class">DBAL</span>\<span class="php-class">Schema</span>\<span class="php-class">Schema</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Migrations</span>\<span class="php-class">AbstractMigration</span>;

<span class="php-comment">/**
 * Auto-generated Migration
 */</span>
<span class="php-keyword">final</span> <span class="php-keyword">class</span> <span class="php-class">Version20240115120000</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractMigration</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getDescription</span>(): <span class="php-keyword">string</span>
    {
        <span class="php-keyword">return</span> <span class="php-string">'Create article table'</span>;
    }

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">up</span>(<span class="php-class">Schema</span> <span class="php-variable">$schema</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// Code pour appliquer la migration</span>
        <span class="php-variable">$this</span>-&gt;<span class="php-function">addSql</span>(<span class="php-string">'
            CREATE TABLE article (
                id INT AUTO_INCREMENT NOT NULL,
                title VARCHAR(200) NOT NULL,
                content LONGTEXT NOT NULL,
                published_at DATETIME DEFAULT NULL,
                PRIMARY KEY(id)
            ) DEFAULT CHARACTER SET utf8mb4 COLLATE `utf8mb4_unicode_ci` ENGINE = InnoDB
        '</span>);
    }

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">down</span>(<span class="php-class">Schema</span> <span class="php-variable">$schema</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// Code pour annuler la migration</span>
        <span class="php-variable">$this</span>-&gt;<span class="php-function">addSql</span>(<span class="php-string">'DROP TABLE article'</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Options avancées de génération</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Générer une migration vide (pour modifications manuelles)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration --empty</span>

<span class="bash-comment"># Voir les différences avant de générer</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:update --dump-sql</span>

<span class="bash-comment"># Valider le mapping des entités</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:validate</span></code></pre>
                </div>

                <div class="code-example tip">
                    <h4 class="text-purple">Bonne pratique</h4>
                    <p class="textExemple">
                        Toujours vérifier le contenu de votre migration avant de l'exécuter, surtout en production.
                        Vous pouvez ouvrir le fichier généré dans <code>migrations/</code> pour voir le SQL qui sera exécuté.
                    </p>
                </div>
            </div>

            <!-- ÉTAPE 3 : Exécution des migrations -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Exécuter les migrations</h2>
                <p class="textExemple">
                    Une fois la migration générée, il faut l'exécuter pour appliquer les changements à votre base de données.
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Commande pour exécuter les migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Exécution interactive :</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-comment"># Symfony vous demande confirmation</span>
<span class="bash-string">WARNING! You are about to execute a database migration
that could result in schema changes and data loss.
Are you sure you wish to continue? (yes/no) [yes]:</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">yes</span>

<span class="bash-success">✓ Migrating from 0 to 20240115120000</span>
<span class="bash-success">✓ 1 migration executed</span>
<span class="bash-success">✓ 1 sql query</span>
<span class="bash-success">Migrations completed successfully</span>

<span class="bash-comment"># Vérifier les tables créées</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SHOW TABLES"</span>

<span class="bash-comment"># Sortie :</span>
<span class="bash-string">+----------------------+</span>
<span class="bash-string">| Tables_in_mon_projet |</span>
<span class="bash-string">+----------------------+</span>
<span class="bash-string">| article              |</span>  <span class="bash-comment">← Table créée !</span>
<span class="bash-string">| doctrine_migration   |</span>  <span class="bash-comment">← Table des migrations</span>
<span class="bash-string">+----------------------+</span></code></pre>
                </div>

                <h3 class="text-purple">Commandes de gestion des migrations</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Voir l'état des migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:status</span>

<span class="bash-comment"># Sortie :</span>
<span class="bash-string">+----------------------+----------------------+</span>
<span class="bash-string">| Configuration        | Value                |</span>
<span class="bash-string">+----------------------+----------------------+</span>
<span class="bash-string">| Storage              | Table                |</span>
<span class="bash-string">| Database Driver      | pdo_mysql            |</span>
<span class="bash-string">| Database Name        | mon_projet           |</span>
<span class="bash-string">| Version              | 20240115120000       |</span>  <span class="bash-comment">← Version actuelle</span>
<span class="bash-string">| Migrations Count     | 1                    |</span>
<span class="bash-string">| Executed Migrations  | 1                    |</span>
<span class="bash-string">| Available Migrations | 1                    |</span>
<span class="bash-string">+----------------------+----------------------+</span>

<span class="bash-comment"># Lister toutes les migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:list</span>

<span class="bash-comment"># Annuler la dernière migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate prev</span>

<span class="bash-comment"># Exécuter une migration spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:execute --up '20240115120000'</span>

<span class="bash-comment"># Exécuter jusqu'à une version spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate '20240115120000'</span></code></pre>
                </div>

                <h3 class="text-purple">Cycle de vie complet d'une migration</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># 1. Modifier votre entité (ajouter un champ)</span>
<span class="bash-comment"># 2. Générer la migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration</span>

<span class="bash-comment"># 3. Vérifier le fichier généré</span>
<span class="bash-prompt">$</span> <span class="bash-command">cat migrations/Version20240115130000.php</span>

<span class="bash-comment"># 4. Exécuter la nouvelle migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-comment"># 5. Vérifier que le champ a été ajouté</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "DESCRIBE article"</span></code></pre>
                </div>
            </div>

            <!-- Création de fixtures -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Préparation : Créer des fixtures avec ORM-Fixtures et FakerPHP</h2>
                <p class="textExemple">
                    Les fixtures permettent de peupler votre base de données avec des données de test.
                    Nous utiliserons ORM-Fixtures pour la structure et FakerPHP pour générer des données réalistes.
                </p>

                <h3 class="text-purple">1. Créer une classe de fixtures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Générer une classe de fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:fixtures</span>

<span class="bash-string">Comment voulez-vous nommer la classe de fixtures ?</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">ArticleFixtures</span>

<span class="bash-success">Fixtures créées avec succès</span>
<span class="bash-success">✓ Fichier : src/DataFixtures/ArticleFixtures.php</span></code></pre>
                </div>

                <h3 class="text-purple">2. Structure de base des fixtures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">DataFixtures</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Article</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Bundle</span>\<span class="php-class">FixturesBundle</span>\<span class="php-class">Fixture</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Persistence</span>\<span class="php-class">ObjectManager</span>;

<span class="php-keyword">class</span> <span class="php-class">ArticleFixtures</span> <span class="php-keyword">extends</span> <span class="php-class">Fixture</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">load</span>(<span class="php-class">ObjectManager</span> <span class="php-variable">$manager</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// $product = new Product();</span>
        <span class="php-comment">// $manager->persist($product);</span>

        <span class="php-variable">$manager</span>-&gt;<span class="php-function">flush</span>();
    }
}</code></pre>
                </div>

                <h3 class="text-purple">3. Utilisation de FakerPHP dans les fixtures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">DataFixtures</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Article</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Bundle</span>\<span class="php-class">FixturesBundle</span>\<span class="php-class">Fixture</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Persistence</span>\<span class="php-class">ObjectManager</span>;

<span class="php-keyword">class</span> <span class="php-class">ArticleFixtures</span> <span class="php-keyword">extends</span> <span class="php-class">Fixture</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">load</span>(<span class="php-class">ObjectManager</span> <span class="php-variable">$manager</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// Initialiser Faker en français</span>
        <span class="php-variable">$faker</span> = \<span class="php-class">Faker</span>\<span class="php-class">Factory</span>::<span class="php-function">create</span>(<span class="php-string">'fr_FR'</span>);

        <span class="php-comment">// Créer 50 articles</span>
        <span class="php-keyword">for</span> (<span class="php-variable">$i</span> = <span class="php-number">0</span>; <span class="php-variable">$i</span> &lt; <span class="php-number">50</span>; <span class="php-variable">$i</span>++) {
            <span class="php-variable">$article</span> = <span class="php-keyword">new</span> <span class="php-class">Article</span>();
            
            <span class="php-comment">// Générer un titre réaliste avec Faker</span>
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setTitle</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">sentence</span>(<span class="php-number">6</span>));
            
            <span class="php-comment">// Générer un contenu réaliste</span>
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setContent</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">paragraphs</span>(<span class="php-number">3</span>, <span class="php-keyword">true</span>));
            
            <span class="php-comment">// 80% des articles sont publiés, 20% en brouillon (null)</span>
            <span class="php-keyword">if</span> (<span class="php-variable">$faker</span>-&gt;<span class="php-function">boolean</span>(<span class="php-number">80</span>)) {
                <span class="php-variable">$article</span>-&gt;<span class="php-function">setPublishedAt</span>(
                    <span class="php-variable">$faker</span>-&gt;<span class="php-function">dateTimeBetween</span>(<span class="php-string">'-1 year'</span>, <span class="php-string">'now'</span>)
                );
            }
            
            <span class="php-variable">$manager</span>-&gt;<span class="php-function">persist</span>(<span class="php-variable">$article</span>);
            
            <span class="php-comment">// Ajouter une référence pour usage ultérieur</span>
            <span class="php-variable">$this</span>-&gt;<span class="php-function">addReference</span>(<span class="php-string">'article_'</span> . <span class="php-variable">$i</span>, <span class="php-variable">$article</span>);
        }

        <span class="php-variable">$manager</span>-&gt;<span class="php-function">flush</span>();
    }
}</code></pre>
                </div>

                <h3 class="text-purple">4. Méthodes utiles de FakerPHP</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Texte</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">sentence</span>(<span class="php-number">6</span>);              <span class="php-comment">// "Lorem ipsum dolor sit amet."</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">paragraphs</span>(<span class="php-number">3</span>, <span class="php-keyword">true</span>);     <span class="php-comment">// 3 paragraphes concaténés</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">text</span>(<span class="php-number">200</span>);               <span class="php-comment">// Texte de 200 caractères</span>

<span class="php-comment">// Dates</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">dateTime</span>();                 <span class="php-comment">// Date aléatoire</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">dateTimeBetween</span>(<span class="php-string">'-1 year'</span>, <span class="php-string">'now'</span>); <span class="php-comment">// Dernière année</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">dateTimeThisYear</span>();        <span class="php-comment">// Cette année</span>

<span class="php-comment">// Nombres et booléens</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">numberBetween</span>(<span class="php-number">1</span>, <span class="php-number">100</span>);     <span class="php-comment">// Nombre entre 1 et 100</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">randomFloat</span>(<span class="php-number">2</span>, <span class="php-number">0</span>, <span class="php-number">1000</span>);  <span class="php-comment">// Nombre décimal</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">boolean</span>(<span class="php-number">70</span>);              <span class="php-comment">// 70% de chance d'être true</span>

<span class="php-comment">// Noms et emails</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">name</span>();                     <span class="php-comment">// "Jean Dupont"</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">email</span>();                    <span class="php-comment">// "jean.dupont@example.com"</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">firstName</span>();               <span class="php-comment">// "Marie"</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">lastName</span>();                <span class="php-comment">// "Martin"</span>

<span class="php-comment">// Adresses</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">address</span>();                  <span class="php-comment">// Adresse complète</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">city</span>();                     <span class="php-comment">// "Paris"</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">postcode</span>();                 <span class="php-comment">// "75001"</span>

<span class="php-comment">// Internet</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">url</span>();                      <span class="php-comment">// "https://example.com"</span>
<span class="php-variable">$faker</span>-&gt;<span class="php-function">userName</span>();                 <span class="php-comment">// "jdupont23"</span></code></pre>
                </div>
            </div>

            <!-- ÉTAPE 4 : Chargement des fixtures -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4 : Charger les fixtures dans la base de données</h2>
                <p class="textExemple">
                    Une fois vos fixtures créées, vous pouvez les charger dans votre base de données pour peupler vos tables avec des données de test.
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Commande pour charger les fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span></code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Exécution interactive :</h4>
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span>

<span class="bash-comment"># Attention : Cette commande va PURGER votre base de données !</span>
<span class="bash-string">Careful, database "mon_projet" will be purged.
Do you want to continue? (yes/no) [no]:</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">yes</span>

<span class="bash-success">✓ Purging database</span>
<span class="bash-success">✓ Loading App\DataFixtures\ArticleFixtures</span>
<span class="bash-success">Fixtures loaded successfully!</span>

<span class="bash-comment"># Vérifier que les données ont été insérées</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT COUNT(*) FROM article"</span>

<span class="bash-comment"># Sortie :</span>
<span class="bash-string">+----------+</span>
<span class="bash-string">| COUNT(*) |</span>
<span class="bash-string">+----------+</span>
<span class="bash-string">|       50 |</span>  <span class="bash-comment">← 50 articles créés !</span>
<span class="bash-string">+----------+</span>

<span class="bash-comment"># Voir un exemple d'article</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT id, title FROM article LIMIT 3"</span>

<span class="bash-comment"># Sortie :</span>
<span class="bash-string">+----+-----------------------------------------+</span>
<span class="bash-string">| id | title                                   |</span>
<span class="bash-string">+----+-----------------------------------------+</span>
<span class="bash-string">|  1 | Lorem ipsum dolor sit amet consectetur. |</span>
<span class="bash-string">|  2 | Adipisci velit sed quia non numquam.    |</span>
<span class="bash-string">|  3 | Eius modi tempora incidunt ut labore.   |</span>
<span class="bash-string">+----+-----------------------------------------+</span></code></pre>
                </div>

                <h3 class="text-purple">Options de chargement des fixtures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Charger sans confirmation (utile pour les scripts)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --no-interaction</span>

<span class="bash-comment"># Ajouter des données sans purger la base</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --append</span>

<span class="bash-comment"># Charger un groupe spécifique de fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --group=ArticleFixtures</span>

<span class="bash-comment"># Exclure certains groupes</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --exclude-group=AdminFixtures</span>

<span class="bash-comment"># Afficher les fixtures qui seront chargées</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --dry-run</span></code></pre>
                </div>

                <h3 class="text-purple">Gestion des dépendances entre fixtures</h3>
                <p class="textExemple">
                    Lorsque vous avez plusieurs fixtures avec des relations entre elles, vous pouvez gérer les dépendances :
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">DataFixtures</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Category</span>;
<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Article</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Bundle</span>\<span class="php-class">FixturesBundle</span>\<span class="php-class">Fixture</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Common</span>\<span class="php-class">DataFixtures</span>\<span class="php-class">DependentFixtureInterface</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Persistence</span>\<span class="php-class">ObjectManager</span>;

<span class="php-keyword">class</span> <span class="php-class">ArticleFixtures</span> <span class="php-keyword">extends</span> <span class="php-class">Fixture</span> <span class="php-keyword">implements</span> <span class="php-class">DependentFixtureInterface</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">load</span>(<span class="php-class">ObjectManager</span> <span class="php-variable">$manager</span>): <span class="php-keyword">void</span>
    {
        <span class="php-variable">$faker</span> = \<span class="php-class">Faker</span>\<span class="php-class">Factory</span>::<span class="php-function">create</span>(<span class="php-string">'fr_FR'</span>);
        
        <span class="php-keyword">for</span> (<span class="php-variable">$i</span> = <span class="php-number">0</span>; <span class="php-variable">$i</span> &lt; <span class="php-number">50</span>; <span class="php-variable">$i</span>++) {
            <span class="php-variable">$article</span> = <span class="php-keyword">new</span> <span class="php-class">Article</span>();
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setTitle</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">sentence</span>());
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setContent</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">paragraphs</span>(<span class="php-number">3</span>, <span class="php-keyword">true</span>));
            
            <span class="php-comment">// Récupérer une catégorie aléatoire créée par CategoryFixtures</span>
            <span class="php-variable">$category</span> = <span class="php-variable">$this</span>-&gt;<span class="php-function">getReference</span>(
                <span class="php-string">'category_'</span> . <span class="php-variable">$faker</span>-&gt;<span class="php-function">numberBetween</span>(<span class="php-number">0</span>, <span class="php-number">4</span>)
            );
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setCategory</span>(<span class="php-variable">$category</span>);
            
            <span class="php-variable">$manager</span>-&gt;<span class="php-function">persist</span>(<span class="php-variable">$article</span>);
        }
        
        <span class="php-variable">$manager</span>-&gt;<span class="php-function">flush</span>();
    }
    
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getDependencies</span>(): <span class="php-class">array</span>
    {
        <span class="php-keyword">return</span> [
            <span class="php-class">CategoryFixtures</span>::<span class="php-keyword">class</span>,  <span class="php-comment">// S'exécute après CategoryFixtures</span>
        ];
    }
}</code></pre>
                </div>

                <div class="code-example tip">
                    <h4 class="text-purple">Cycle de développement typique</h4>
                    <p class="textExemple">
                        Lorsque vous développez, vous allez souvent répéter ce cycle :
                    </p>
                    <ol class="textExemple">
                        <li>Modifier une entité (ajouter/supprimer un champ)</li>
                        <li>Générer une migration : <code>make:migration</code></li>
                        <li>Exécuter la migration : <code>doctrine:migrations:migrate</code></li>
                        <li>Charger les fixtures : <code>doctrine:fixtures:load</code></li>
                        <li>Tester votre application</li>
                    </ol>
                </div>
            </div>

            <!-- Récapitulatif complet -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récapitulatif : Workflow complet Doctrine</h2>
                
                <h3 class="text-purple">Séquence complète des commandes</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># 1. INSTALLATION (une seule fois)</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require symfony/orm-pack</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev symfony/maker-bundle orm-fixtures fakerphp/faker</span>

<span class="bash-comment"># 2. CONFIGURATION (une seule fois)</span>
<span class="bash-comment"># Éditer le fichier .env et configurer DATABASE_URL</span>

<span class="bash-comment"># 3. CRÉATION DE LA BASE (étape 1)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>

<span class="bash-comment"># 4. CRÉATION DES ENTITÉS (pré-requis)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:entity NomEntite</span>

<span class="bash-comment"># 5. GÉNÉRATION DES MIGRATIONS (étape 2)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration</span>

<span class="bash-comment"># 6. EXÉCUTION DES MIGRATIONS (étape 3)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-comment"># 7. CRÉATION DES FIXTURES (pré-requis)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:fixtures</span>
<span class="bash-comment"># Éditer le fichier src/DataFixtures/*.php avec FakerPHP</span>

<span class="bash-comment"># 8. CHARGEMENT DES FIXTURES (étape 4)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span>

<span class="bash-comment"># 9. VÉRIFICATION</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT COUNT(*) FROM nom_table"</span></code></pre>
                </div>

                <h3 class="text-purple">Script bash pour automatiser le processus</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment">#!/bin/bash</span>
<span class="bash-comment"># script-doctrine.sh - Automatise le workflow Doctrine</span>

<span class="bash-keyword">echo</span> <span class="bash-string">"Début du workflow Doctrine..."</span>

<span class="bash-comment"># 1. Créer la base de données</span>
<span class="bash-keyword">echo</span> <span class="bash-string">"Étape 1 : Création de la base de données"</span>
symfony console doctrine:database:create --if-not-exists

<span class="bash-comment"># 2. Générer les migrations</span>
<span class="bash-keyword">echo</span> <span class="bash-string">"Étape 2 : Génération des migrations"</span>
symfony console make:migration

<span class="bash-comment"># 3. Exécuter les migrations</span>
<span class="bash-keyword">echo</span> <span class="bash-string">"Étape 3 : Exécution des migrations"</span>
symfony console doctrine:migrations:migrate --no-interaction

<span class="bash-comment"># 4. Charger les fixtures</span>
<span class="bash-keyword">echo</span> <span class="bash-string">"Étape 4 : Chargement des fixtures"</span>
symfony console doctrine:fixtures:load --no-interaction

<span class="bash-keyword">echo</span> <span class="bash-string">"Workflow Doctrine terminé avec succès !"</span></code></pre>
                </div>

                <h3 class="text-purple">Commandes de débogage et vérification</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Vérifier l'état de la base</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SHOW TABLES"</span>

<span class="bash-comment"># Voir la structure d'une table</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "DESCRIBE article"</span>

<span class="bash-comment"># Compter les enregistrements</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT COUNT(*) FROM article"</span>

<span class="bash-comment"># Voir les données d'exemple</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT * FROM article LIMIT 5"</span>

<span class="bash-comment"># Vérifier l'état des migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:status</span>

<span class="bash-comment"># Valider le mapping</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:validate</span></code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique : Blog complet</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer un système de blog complet en suivant les 4 étapes Doctrine.
                    </p>
                    <ol class="textExemple">
                        <li><strong>Configuration</strong> : Installer les dépendances et configurer <code>.env</code></li>
                        <li><strong>Étape 1</strong> : Créer la base avec <code>doctrine:database:create</code></li>
                        <li><strong>Entités</strong> : Créer 3 entités : <code>Post</code>, <code>Category</code>, <code>Comment</code></li>
                        <li><strong>Étape 2</strong> : Générer les migrations avec <code>make:migration</code></li>
                        <li><strong>Étape 3</strong> : Exécuter les migrations avec <code>doctrine:migrations:migrate</code></li>
                        <li><strong>Fixtures</strong> : Créer des fixtures avec FakerPHP pour chaque entité</li>
                        <li><strong>Étape 4</strong> : Charger les fixtures avec <code>doctrine:fixtures:load</code></li>
                        <li><strong>Vérification</strong> : Vérifier que les données sont bien présentes</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution guidée</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Solution étape par étape :</h4>
                        
                        <div class="code-example">
                            <h5 class="text-purple">1. Installation et configuration</h5>
                            <pre v-pre><code class="language-bash"><span class="bash-comment"># Installation</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require symfony/orm-pack</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev symfony/maker-bundle orm-fixtures fakerphp/faker</span>

<span class="bash-comment"># Configuration de .env</span>
<span class="bash-highlight">DATABASE_URL="mysql://root:@127.0.0.1:3306/mon_blog?serverVersion=8.0"</span></code></pre>
                        </div>

                        <div class="code-example">
                            <h5 class="text-purple">2. Exécution des 4 étapes principales</h5>
                            <pre v-pre><code class="language-bash"><span class="bash-comment"># ÉTAPE 1 : Création de la base</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>

<span class="bash-comment"># Création des entités</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:entity Post</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:entity Category</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:entity Comment</span>

<span class="bash-comment"># ÉTAPE 2 : Génération des migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration</span>

<span class="bash-comment"># ÉTAPE 3 : Exécution des migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-comment"># Création des fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:fixtures CategoryFixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:fixtures PostFixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:fixtures CommentFixtures</span>

<span class="bash-comment"># ÉTAPE 4 : Chargement des fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span>

<span class="bash-comment"># Vérification</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT 'Categories', COUNT(*) FROM category"</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT 'Posts', COUNT(*) FROM post"</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT 'Comments', COUNT(*) FROM comment"</span></code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Vous maîtrisez maintenant le workflow complet pour gérer une base de données avec Doctrine dans Symfony !
                    Les 4 étapes clés sont désormais claires :
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># LES 4 ÉTAPES ESSENTIELLES</span>

<span class="bash-comment"># 1. Créer la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>

<span class="bash-comment"># 2. Générer les migrations (après création/modification d'entités)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console make:migration</span>

<span class="bash-comment"># 3. Exécuter les migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-comment"># 4. Peupler avec des fixtures (optionnel mais recommandé)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span></code></pre>
                </div>

                <h3 class="text-purple">Points clés à retenir :</h3>
                <ul class="textExemple">
                    <li><strong>Les migrations sont versionnées</strong> : Chaque modification génère un fichier que vous pouvez versionner avec Git</li>
                    <li><strong>Fixtures + FakerPHP</strong> : Combinaison puissante pour créer des données de test réalistes</li>
                    <li><strong>Toujours vérifier</strong> : Utilisez les commandes de vérification avant d'exécuter en production</li>
                    <li><strong>Cycle itératif</strong> : Modifiez vos entités → Générez une migration → Exécutez → Testez</li>
                </ul>

                <h3 class="text-purple">Prochaines étapes :</h3>
                <ul class="textExemple">
                    <li>Apprendre les relations entre entités (OneToMany, ManyToMany)</li>
                    <li>Découvrir les événements Doctrine (lifecycle callbacks)</li>
                    <li>Explorer les requêtes DQL (Doctrine Query Language)</li>
                    <li>Apprendre à optimiser les performances avec les index et le cache</li>
                </ul>

                <h3 class="text-purple">Ressources :</h3>
                <ul class="textExemple">
                    <li><a href="https://symfony.com/doc/current/doctrine.html" target="_blank" class="btn-purple btn-hover">Documentation officielle Doctrine</a></li>
                    <li><a href="https://github.com/doctrine/DoctrineMigrationsBundle" target="_blank" class="btn-purple btn-hover">Doctrine Migrations Bundle</a></li>
                    <li><a href="https://github.com/doctrine/DoctrineFixturesBundle" target="_blank" class="btn-purple btn-hover">Doctrine Fixtures Bundle</a></li>
                    <li><a href="https://fakerphp.github.io/" target="_blank" class="btn-purple btn-hover">Documentation FakerPHP</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DoctrineWorkflowLessonPage',
    
    mounted() {
        if (typeof Prism !== 'undefined') {
            Prism.highlightAll();
        }
    }
}
</script>

<style scoped>
/* Styles identiques à la leçon précédente */
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
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
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
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

.bg-light-purple {
    background-color: #f8f6ff;
    border-radius: 12px;
}

.border-purple {
    border: 2px solid #e0d6ff;
    border-radius: 15px;
    transition: all 0.3s ease;
}

.text-purple {
    color: #6A3093 !important;
}

.text-white {
    color: white !important;
}

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
    max-width: 100%;
    width: 100%;
    box-sizing: border-box;
    white-space: pre-wrap;
    word-wrap: break-word;
    word-break: break-word;
}

.bash-prompt {
    color: #2ECC71 !important;
    font-weight: bold;
}

.bash-command {
    color: #F1C40F !important;
}

.bash-comment {
    color: #7F8C8D !important;
    font-style: italic;
}

.bash-highlight {
    color: #FF9800 !important;
    font-weight: bold;
    background-color: rgba(255, 152, 0, 0.1);
    padding: 2px 4px;
    border-radius: 3px;
}

.bash-success {
    color: #2ECC71 !important;
    font-weight: bold;
}

.php-keyword {
    color: #569CD6 !important;
}

.php-function {
    color: #DCDCAA !important;
}

.php-class {
    color: #4EC9B0 !important;
}

.php-variable {
    color: #9CDCFE !important;
}

.php-string {
    color: #CE9178 !important;
}

.php-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.php-number {
    color: #B5CEA8 !important;
}

.tip {
    background: linear-gradient(135deg, rgba(139, 95, 191, 0.1) 0%, rgba(106, 48, 147, 0.1) 100%);
    border-left: 4px solid #8B5FBF;
    padding: 1.5rem;
    border-radius: 8px;
    margin: 1.5rem 0;
}

.tip h4 {
    color: #6A3093;
    margin-top: 0;
    display: flex;
    align-items: center;
    gap: 10px;
}


/* Responsive */
@media (max-width: 768px) {
    .lesson-container {
        padding: 1rem;
    }
    
    .lesson-header {
        padding: 2rem 1rem;
    }
    
    .lesson-header h1 {
        font-size: 2rem;
    }
    
    .lesson-section {
        padding: 1.5rem;
    }
    
    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
    }
}

@media (max-width: 480px) {
    pre {
        padding: 0.75rem !important;
        font-size: 0.8rem;
    }
    
    .lesson-container {
        padding: 0.5rem;
    }
    
    .lesson-section {
        padding: 1rem;
    }
    
    .lesson-header {
        padding: 1.5rem 1rem;
    }
    
    .lesson-header h1 {
        font-size: 1.75rem;
    }
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.lesson-section {
    animation: fadeInUp 0.6s ease forwards;
}

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>