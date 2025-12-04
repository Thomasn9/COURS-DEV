<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Créer et Utiliser une Base de Données avec Doctrine dans Symfony</h1>
                <p class="lesson-meta text-white">Maîtrisez les entités, les migrations et les requêtes pour persister vos données</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Doctrine ORM</h2>
                <p class="textExemple">
                    Doctrine est l'ORM (Object-Relational Mapping) par défaut de Symfony. Il vous permet de travailler avec des bases de données 
                    relationnelles en utilisant des objets PHP plutôt que d'écrire du SQL directement.
                </p>
                <p class="textExemple">
                    Cette leçon vous guidera à travers l'ensemble du processus : de la configuration de la base de données 
                    à la création d'entités, en passant par les migrations et les requêtes.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Flux de travail Doctrine</span>
Configuration → Entités → Migrations → Requêtes → Persistance des données</code></pre>
                </div>
            </div>

            <!-- Les 5 étapes fondamentales -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 5 étapes fondamentales avec Doctrine</h2>
                <p class="textExemple">
                    Pour utiliser efficacement Doctrine dans Symfony, suivez ces cinq étapes :
                </p>
                <ol class="textExemple">
                    <li><strong>Configurer la connexion à la base de données</strong></li>
                    <li><strong>Créer des entités (modèles de données)</strong></li>
                    <li><strong>Générer et exécuter les migrations</strong></li>
                    <li><strong>Utiliser le Repository pour les requêtes</strong></li>
                    <li><strong>Persister les données avec l'EntityManager</strong></li>
                </ol>
            </div>

            <!-- Étape 1 : Configuration de la base de données -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : Configurer la connexion à la base de données</h2>
                <p class="textExemple">
                    Avant de commencer, vous devez configurer votre connexion à la base de données dans Symfony.
                </p>

                <h3 class="text-purple">1. Installation de Doctrine (si ce n'est pas déjà fait)</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Installation du bundle Doctrine</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require symfony/orm-pack</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev symfony/maker-bundle</span></code></pre>
                </div>

                <h3 class="text-purple">2. Configuration dans le fichier .env</h3>
                <p class="textExemple">
                    Symfony utilise le fichier <code>.env</code> pour la configuration de l'environnement. Configurez votre connexion :
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># .env</span>
<span class="bash-comment"># DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name?serverVersion=mariadb-10.11.4&charset=utf8mb4"</span>

<span class="bash-comment"># Pour MySQL/MariaDB :</span>
<span class="bash-highlight">DATABASE_URL="mysql://root:@127.0.0.1:3306/symfony_project?serverVersion=8.0&charset=utf8mb4"</span>

<span class="bash-comment"># Pour PostgreSQL :</span>
<span class="bash-comment"># DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=15&charset=utf8"</span>

<span class="bash-comment"># Pour SQLite :</span>
<span class="bash-comment"># DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"</span></code></pre>
                </div>

                <h3 class="text-purple">3. Créer la base de données</h3>
                <p class="textExemple">
                    Une fois la configuration terminée, créez la base de données avec Doctrine :
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>

<span class="bash-success">✅ Base de données 'symfony_project' créée avec succès</span>

<span class="bash-comment"># Vérifier la connexion</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT 1"</span>

<span class="bash-comment"># Supprimer la base de données (en cas de besoin)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:drop --force</span></code></pre>
                </div>

                <h3 class="text-purple">4. Commandes utiles pour la gestion des bases de données</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lister toutes les commandes Doctrine disponibles</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console list doctrine</span>

<span class="bash-comment"># Vérifier le mapping des entités</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:mapping:info</span>

<span class="bash-comment"># Vider complètement la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:drop --force</span></code></pre>
                </div>
            </div>

            <!-- Étape 2 : Création d'entités avec symfony make:entity -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Créer des entités avec symfony make:entity</h2>
                <p class="textExemple">
                    Les entités sont des classes PHP qui représentent vos tables de base de données. 
                    Utilisez <code>symfony make:entity</code> pour les créer facilement.
                </p>

                <h3 class="text-purple">1. Créer une première entité : Article</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity</span>

<span class="bash-string">Quel nom souhaitez-vous donner à votre entité ?</span>
<span class="bash-parameter">[ex: <span class="bash-keyword">Victorious</span>Penguin]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">Article</span>

<span class="bash-string">Voulez-vous ajouter une nouvelle propriété à votre entité ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span></code></pre>
                </div>

                <h3 class="text-purple">2. Ajouter les propriétés (champs) de l'entité</h3>
                <p class="textExemple">
                    Suivez les prompts interactifs pour ajouter chaque propriété :
                </p>

                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-string">Nom du champ (appuyez sur &lt;return&gt; pour arrêter l'ajout de champs) :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">title</span>

<span class="bash-string">Type de champ [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">string</span>

<span class="bash-string">Longueur du champ [255] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">255</span>

<span class="bash-string">Ce champ peut-il être nul (nullable) ? (oui/no) [no] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">no</span>

<span class="bash-string">Voulez-vous ajouter une nouvelle propriété à votre entité ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">content</span>

<span class="bash-string">Type de champ [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">text</span>

<span class="bash-string">Voulez-vous ajouter une nouvelle propriété ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">publishedAt</span>

<span class="bash-string">Type de champ [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">datetime_immutable</span>

<span class="bash-string">Ce champ peut-il être nul (nullable) ? (oui/no) [no] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Voulez-vous ajouter une nouvelle propriété ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">non</span>

<span class="bash-success">✅ Entité Article créée !</span>
<span class="bash-success">✓ src/Entity/Article.php</span>
<span class="bash-success">✓ src/Repository/ArticleRepository.php</span></code></pre>
                </div>

                <h3 class="text-purple">3. Structure de l'entité générée</h3>
                <div class="code-example">
                    <h4 class="text-purple">Fichier d'entité : src/Entity/Article.php</h4>
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Entity</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Repository</span>\<span class="php-class">ArticleRepository</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">DBAL</span>\<span class="php-class">Types</span>\<span class="php-class">Types</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">ORM</span>\<span class="php-class">Mapping</span> <span class="php-keyword">as</span> <span class="php-class">ORM</span>;

#[<span class="php-class">ORM</span>\<span class="php-function">Entity</span>(<span class="php-variable">repositoryClass</span>: <span class="php-class">ArticleRepository</span>::<span class="php-keyword">class</span>)]
<span class="php-keyword">class</span> <span class="php-class">Article</span>
{
    #[<span class="php-class">ORM</span>\<span class="php-function">Id</span>]
    #[<span class="php-class">ORM</span>\<span class="php-function">GeneratedValue</span>]
    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>]
    <span class="php-keyword">private</span> ?<span class="php-keyword">int</span> <span class="php-variable">$id</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">length</span>: <span class="php-number">255</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$title</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">type</span>: <span class="php-class">Types</span>::<span class="php-class">TEXT</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$content</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">type</span>: <span class="php-class">Types</span>::<span class="php-class">DATETIME_IMMUTABLE</span>, <span class="php-variable">nullable</span>: <span class="php-keyword">true</span>)]
    <span class="php-keyword">private</span> ?\<span class="php-class">DateTimeImmutable</span> <span class="php-variable">$publishedAt</span> = <span class="php-keyword">null</span>;

    <span class="php-comment">// Getters et Setters générés automatiquement</span>
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getId</span>(): ?<span class="php-keyword">int</span>
    {
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;id;
    }

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getTitle</span>(): ?<span class="php-keyword">string</span>
    {
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;title;
    }

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">setTitle</span>(<span class="php-keyword">string</span> <span class="php-variable">$title</span>): <span class="php-keyword">static</span>
    {
        <span class="php-variable">$this</span>-&gt;title = <span class="php-variable">$title</span>;
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>;
    }

    <span class="php-comment">// ... autres getters et setters</span>
}</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Fichier de repository : src/Repository/ArticleRepository.php</h4>
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Repository</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Article</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Bundle</span>\<span class="php-class">DoctrineBundle</span>\<span class="php-class">Repository</span>\<span class="php-class">ServiceEntityRepository</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Persistence</span>\<span class="php-class">ManagerRegistry</span>;

<span class="php-keyword">class</span> <span class="php-class">ArticleRepository</span> <span class="php-keyword">extends</span> <span class="php-class">ServiceEntityRepository</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> __construct(<span class="php-class">ManagerRegistry</span> <span class="php-variable">$registry</span>)
    {
        <span class="php-keyword">parent</span>::__construct(<span class="php-variable">$registry</span>, <span class="php-class">Article</span>::<span class="php-keyword">class</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">4. Types de champs disponibles</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Principaux types de champs Doctrine :</span>
<span class="bash-keyword">string</span>       <span class="bash-comment"># Chaîne de caractères (VARCHAR)</span>
<span class="bash-keyword">text</span>         <span class="bash-comment"># Texte long (TEXT)</span>
<span class="bash-keyword">integer</span>      <span class="bash-comment"># Entier (INT)</span>
<span class="bash-keyword">float</span>        <span class="bash-comment"># Nombre à virgule (FLOAT)</span>
<span class="bash-keyword">boolean</span>      <span class="bash-comment"># Booléen (TINYINT)</span>
<span class="bash-keyword">datetime</span>     <span class="bash-comment"># Date et heure (DATETIME)</span>
<span class="bash-keyword">date</span>         <span class="bash-comment"># Date seulement (DATE)</span>
<span class="bash-keyword">time</span>         <span class="bash-comment"># Heure seulement (TIME)</span>
<span class="bash-keyword">json</span>         <span class="bash-comment"># Données JSON (JSON)</span>
<span class="bash-keyword">array</span>        <span class="bash-comment"># Tableau sérialisé (LONGTEXT)</span>
<span class="bash-keyword">decimal</span>      <span class="bash-comment"># Nombre décimal précis (DECIMAL)</span></code></pre>
                </div>

                <h3 class="text-purple">5. Modifier une entité existante</h3>
                <p class="textExemple">
                    Pour ajouter ou modifier des champs dans une entité existante :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Lancer à nouveau make:entity avec le même nom</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Article</span>

<span class="bash-string">Votre entité Article existe déjà ! Voulez-vous la mettre à jour ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Nom du champ (appuyez sur &lt;return&gt; pour arrêter) :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">slug</span>

<span class="bash-string">Type de champ [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">string</span>

<span class="bash-string">Longueur du champ [255] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">100</span>

<span class="bash-string">Ce champ peut-il être nul (nullable) ? (oui/no) [no] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">no</span></code></pre>
                </div>
            </div>

            <!-- Étape 3 : Migrations avec symfony make:migration -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Générer et exécuter les migrations avec symfony make:migration</h2>
                <p class="textExemple">
                    Les migrations sont des fichiers qui permettent de versionner votre schéma de base de données.
                    Elles assurent que tous les environnements (dev, prod) ont le même schéma.
                </p>

                <h3 class="text-purple">1. Générer une migration</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Générer une migration basée sur les différences entre entités et base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:migration</span>

<span class="bash-success">✅ Migration générée avec succès !</span>
<span class="bash-success">✓ migrations/Version20240115143000.php</span>

<span class="bash-comment"># Voir le SQL qui sera exécuté</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:diff --dry-run</span></code></pre>
                </div>

                <h3 class="text-purple">2. Structure d'une migration générée</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">declare</span>(<span class="php-variable">strict_types</span>=<span class="php-number">1</span>);

<span class="php-keyword">namespace</span> DoctrineMigrations;

<span class="php-keyword">use</span> Doctrine\<span class="php-class">DBAL</span>\<span class="php-class">Schema</span>\<span class="php-class">Schema</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Migrations</span>\<span class="php-class">AbstractMigration</span>;

<span class="php-comment">/**
 * Auto-generated Migration: Please modify to your needs!
 */</span>
<span class="php-keyword">final</span> <span class="php-keyword">class</span> <span class="php-class">Version20240115143000</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractMigration</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getDescription</span>(): <span class="php-keyword">string</span>
    {
        <span class="php-keyword">return</span> <span class="php-string">'Création de la table article'</span>;
    }

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">up</span>(<span class="php-class">Schema</span> <span class="php-variable">$schema</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// this up() migration is auto-generated, please modify it to your needs</span>
        <span class="php-variable">$this</span>-&gt;<span class="php-function">addSql</span>(<span class="php-string">'
            CREATE TABLE article (
                id INT AUTO_INCREMENT NOT NULL,
                title VARCHAR(255) NOT NULL,
                content LONGTEXT NOT NULL,
                published_at DATETIME DEFAULT NULL,
                PRIMARY KEY(id)
            ) DEFAULT CHARACTER SET utf8mb4 COLLATE `utf8mb4_unicode_ci` ENGINE = InnoDB
        '</span>);
    }

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">down</span>(<span class="php-class">Schema</span> <span class="php-variable">$schema</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// this down() migration is auto-generated, please modify it to your needs</span>
        <span class="php-variable">$this</span>-&gt;<span class="php-function">addSql</span>(<span class="php-string">'DROP TABLE article'</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">3. Exécuter les migrations</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Exécuter toutes les migrations en attente</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-string">Voulez-vous exécuter ces migrations ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-success">✓ Migration Version20240115143000 exécutée</span>
<span class="bash-success">✅ Migrations exécutées avec succès</span>

<span class="bash-comment"># Exécuter une migration spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:execute --up '20240115143000'</span>

<span class="bash-comment"># Annuler la dernière migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate prev</span>

<span class="bash-comment"># Revenir à une version spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate '20240115143000'</span></code></pre>
                </div>

                <h3 class="text-purple">4. Gestion avancée des migrations</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Voir l'état des migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:status</span>

<span class="bash-comment"># Lister toutes les migrations disponibles</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:list</span>

<span class="bash-comment"># Générer une migration vide (pour modifications manuelles)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:migration --empty</span>

<span class="bash-comment"># Synchroniser la base de données sans migrations (DANGEREUX)</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:update --force</span></code></pre>
                </div>

                <div class="code-example tip">
                    <h4 class="text-purple">💡 Bonne pratique : Validation du schéma</h4>
                    <p class="textExemple">
                        Avant de générer une migration, vérifiez toujours que votre schéma est valide :
                    </p>
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Valider le mapping</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:validate</span>

<span class="bash-success">[OK] Le mapping est valide</span>

<span class="bash-comment"># Voir les différences entre entités et base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:update --dump-sql</span></code></pre>
                </div>
            </div>

            <!-- Étape 4 : Relations entre entités -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4 : Créer des relations entre entités</h2>
                <p class="textExemple">
                    Doctrine permet de créer des relations entre différentes entités, tout comme les clés étrangères en SQL.
                </p>

                <h3 class="text-purple">1. Créer une entité Category avec relation</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer l'entité Category</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Category</span>

<span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">name</span>

<span class="bash-string">Type de champ [string] :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">string</span>

<span class="bash-string">Voulez-vous ajouter une nouvelle propriété ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">non</span></code></pre>
                </div>

                <h3 class="text-purple">2. Ajouter une relation entre Article et Category</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Ajouter une relation à l'entité Article</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Article</span>

<span class="bash-string">Voulez-vous ajouter une nouvelle propriété ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Nom du champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">category</span>

<span class="bash-string">Type de champ :</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">relation</span>

<span class="bash-string">Quelle entité voulez-vous relier ?</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">Category</span>

<span class="bash-string">Type de relation :</span>
<span class="bash-comment"># ManyToOne : Un article appartient à une catégorie</span>
<span class="bash-comment"># OneToMany : Une catégorie contient plusieurs articles</span>
<span class="bash-comment"># ManyToMany : Les articles peuvent avoir plusieurs catégories</span>
<span class="bash-comment"># OneToOne : Relation un à un</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">ManyToOne</span>

<span class="bash-string">Cette entité est-elle le côté propriétaire de la relation ? (oui/no) [oui]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Un article peut-il être sans catégorie ? (nullable) (oui/no) [no]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Voulez-vous ajouter automatiquement une nouvelle propriété dans Category ? (oui/no) [yes]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-string">Comment voulez-vous nommer la nouvelle propriété dans Category ? [articles]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">articles</span>

<span class="bash-string">Type de relation dans Category sera OneToMany</span></code></pre>
                </div>

                <h3 class="text-purple">3. Code généré pour la relation</h3>
                <div class="code-example">
                    <h4 class="text-purple">Dans Article.php :</h4>
                    <pre v-pre><code class="language-php">#[<span class="php-class">ORM</span>\<span class="php-function">ManyToOne</span>(<span class="php-variable">targetEntity</span>: <span class="php-class">Category</span>::<span class="php-keyword">class</span>, <span class="php-variable">inversedBy</span>: <span class="php-string">'articles'</span>)]
#[<span class="php-class">ORM</span>\<span class="php-function">JoinColumn</span>(<span class="php-variable">nullable</span>: <span class="php-keyword">true</span>)]
<span class="php-keyword">private</span> ?<span class="php-class">Category</span> <span class="php-variable">$category</span> = <span class="php-keyword">null</span>;

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getCategory</span>(): ?<span class="php-class">Category</span>
{
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;category;
}

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">setCategory</span>(?<span class="php-class">Category</span> <span class="php-variable">$category</span>): <span class="php-keyword">static</span>
{
    <span class="php-variable">$this</span>-&gt;category = <span class="php-variable">$category</span>;
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>;
}</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Dans Category.php :</h4>
                    <pre v-pre><code class="language-php">#[<span class="php-class">ORM</span>\<span class="php-function">OneToMany</span>(<span class="php-variable">targetEntity</span>: <span class="php-class">Article</span>::<span class="php-keyword">class</span>, <span class="php-variable">mappedBy</span>: <span class="php-string">'category'</span>)]
<span class="php-keyword">private</span> <span class="php-class">Collection</span> <span class="php-variable">$articles</span>;

<span class="php-keyword">public</span> <span class="php-keyword">function</span> __construct()
{
    <span class="php-variable">$this</span>-&gt;articles = <span class="php-keyword">new</span> \<span class="php-class">ArrayCollection</span>();
}

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">getArticles</span>(): <span class="php-class">Collection</span>
{
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;articles;
}

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">addArticle</span>(<span class="php-class">Article</span> <span class="php-variable">$article</span>): <span class="php-keyword">static</span>
{
    <span class="php-keyword">if</span> (!<span class="php-variable">$this</span>-&gt;articles-&gt;<span class="php-function">contains</span>(<span class="php-variable">$article</span>)) {
        <span class="php-variable">$this</span>-&gt;articles-&gt;<span class="php-function">add</span>(<span class="php-variable">$article</span>);
        <span class="php-variable">$article</span>-&gt;<span class="php-function">setCategory</span>(<span class="php-variable">$this</span>);
    }
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>;
}

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">removeArticle</span>(<span class="php-class">Article</span> <span class="php-variable">$article</span>): <span class="php-keyword">static</span>
{
    <span class="php-keyword">if</span> (<span class="php-variable">$this</span>-&gt;articles-&gt;<span class="php-function">removeElement</span>(<span class="php-variable">$article</span>)) {
        <span class="php-comment">// Définir le côté propriétaire sur null (sauf si déjà modifié)</span>
        <span class="php-keyword">if</span> (<span class="php-variable">$article</span>-&gt;<span class="php-function">getCategory</span>() === <span class="php-variable">$this</span>) {
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setCategory</span>(<span class="php-keyword">null</span>);
        }
    }
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>;
}</code></pre>
                </div>

                <h3 class="text-purple">4. Types de relations disponibles</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># OneToOne : Relation un à un</span>
<span class="bash-comment"># Exemple : Un utilisateur a un profil, un profil appartient à un utilisateur</span>

<span class="bash-comment"># OneToMany / ManyToOne : Relation un à plusieurs</span>
<span class="bash-comment"># Exemple : Une catégorie a plusieurs articles, un article appartient à une catégorie</span>

<span class="bash-comment"># ManyToMany : Relation plusieurs à plusieurs</span>
<span class="bash-comment"># Exemple : Un article a plusieurs tags, un tag appartient à plusieurs articles</span>

<span class="bash-comment"># Relation ManyToMany avec entité de liaison :</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity ArticleTag --with-linking</span></code></pre>
                </div>
            </div>

            <!-- Étape 5 : Utiliser l'EntityManager et les Repository -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 5 : Utiliser l'EntityManager et les Repository</h2>
                <p class="textExemple">
                    Maintenant que vos entités sont créées, apprenez à les manipuler avec l'EntityManager 
                    et à effectuer des requêtes avec les Repository.
                </p>

                <h3 class="text-purple">1. Créer un contrôleur pour gérer les articles</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer un contrôleur pour gérer les articles</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:controller ArticleController</span></code></pre>
                </div>

                <h3 class="text-purple">2. Exemple de contrôleur avec opérations CRUD</h3>
                <div class="code-example">
                    <h4 class="text-purple">ArticleController.php - CRUD complet</h4>
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Controller</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Article</span>;
<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Category</span>;
<span class="php-keyword">use</span> App\<span class="php-class">Form</span>\<span class="php-class">ArticleType</span>;
<span class="php-keyword">use</span> App\<span class="php-class">Repository</span>\<span class="php-class">ArticleRepository</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">ORM</span>\<span class="php-class">EntityManagerInterface</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Bundle</span>\<span class="php-class">FrameworkBundle</span>\<span class="php-class">Controller</span>\<span class="php-class">AbstractController</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">HttpFoundation</span>\<span class="php-class">Request</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">HttpFoundation</span>\<span class="php-class">Response</span>;
<span class="php-keyword">use</span> Symfony\<span class="php-class">Component</span>\<span class="php-class">Routing</span>\<span class="php-class">Annotation</span>\<span class="php-class">Route</span>;

#[<span class="php-function">Route</span>(<span class="php-string">'/article'</span>)]
<span class="php-keyword">class</span> <span class="php-class">ArticleController</span> <span class="php-keyword">extends</span> <span class="php-class">AbstractController</span>
{
    <span class="php-comment">// CREATE : Créer un nouvel article</span>
    #[<span class="php-function">Route</span>(<span class="php-string">'/new'</span>, <span class="php-variable">name</span>: <span class="php-string">'article_new'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'GET'</span>, <span class="php-string">'POST'</span>])]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">new</span>(
        <span class="php-class">Request</span> <span class="php-variable">$request</span>,
        <span class="php-class">EntityManagerInterface</span> <span class="php-variable">$entityManager</span>
    ): <span class="php-class">Response</span> {
        <span class="php-variable">$article</span> = <span class="php-keyword">new</span> <span class="php-class">Article</span>();
        <span class="php-variable">$form</span> = <span class="php-variable">$this</span>-&gt;<span class="php-function">createForm</span>(<span class="php-class">ArticleType</span>::<span class="php-keyword">class</span>, <span class="php-variable">$article</span>);
        <span class="php-variable">$form</span>-&gt;<span class="php-function">handleRequest</span>(<span class="php-variable">$request</span>);

        <span class="php-keyword">if</span> (<span class="php-variable">$form</span>-&gt;<span class="php-function">isSubmitted</span>() &amp;&amp; <span class="php-variable">$form</span>-&gt;<span class="php-function">isValid</span>()) {
            <span class="php-comment">// Persist et flush pour sauvegarder</span>
            <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">persist</span>(<span class="php-variable">$article</span>);
            <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">flush</span>();

            <span class="php-variable">$this</span>-&gt;<span class="php-function">addFlash</span>(<span class="php-string">'success'</span>, <span class="php-string">'Article créé avec succès !'</span>);
            <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">redirectToRoute</span>(<span class="php-string">'article_index'</span>);
        }

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'article/new.html.twig'</span>, [
            <span class="php-string">'article'</span> =&gt; <span class="php-variable">$article</span>,
            <span class="php-string">'form'</span> =&gt; <span class="php-variable">$form</span>,
        ]);
    }

    <span class="php-comment">// READ : Lister tous les articles</span>
    #[<span class="php-function">Route</span>(<span class="php-string">'/'</span>, <span class="php-variable">name</span>: <span class="php-string">'article_index'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'GET'</span>])]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">index</span>(<span class="php-class">ArticleRepository</span> <span class="php-variable">$articleRepository</span>): <span class="php-class">Response</span>
    {
        <span class="php-comment">// Récupérer tous les articles</span>
        <span class="php-variable">$articles</span> = <span class="php-variable">$articleRepository</span>-&gt;<span class="php-function">findAll</span>();

        <span class="php-comment">// Ou avec une méthode personnalisée</span>
        <span class="php-variable">$recentArticles</span> = <span class="php-variable">$articleRepository</span>-&gt;<span class="php-function">findRecent</span>(<span class="php-number">10</span>);

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'article/index.html.twig'</span>, [
            <span class="php-string">'articles'</span> =&gt; <span class="php-variable">$articles</span>,
            <span class="php-string">'recent_articles'</span> =&gt; <span class="php-variable">$recentArticles</span>,
        ]);
    }

    <span class="php-comment">// READ : Afficher un article spécifique</span>
    #[<span class="php-function">Route</span>(<span class="php-string">'/{id}'</span>, <span class="php-variable">name</span>: <span class="php-string">'article_show'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'GET'</span>])]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">show</span>(<span class="php-class">Article</span> <span class="php-variable">$article</span>): <span class="php-class">Response</span>
    {
        <span class="php-comment">// Symfony fait automatiquement la requête grâce au ParamConverter</span>
        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'article/show.html.twig'</span>, [
            <span class="php-string">'article'</span> =&gt; <span class="php-variable">$article</span>,
        ]);
    }

    <span class="php-comment">// UPDATE : Modifier un article</span>
    #[<span class="php-function">Route</span>(<span class="php-string">'/{id}/edit'</span>, <span class="php-variable">name</span>: <span class="php-string">'article_edit'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'GET'</span>, <span class="php-string">'POST'</span>])]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">edit</span>(
        <span class="php-class">Request</span> <span class="php-variable">$request</span>,
        <span class="php-class">Article</span> <span class="php-variable">$article</span>,
        <span class="php-class">EntityManagerInterface</span> <span class="php-variable">$entityManager</span>
    ): <span class="php-class">Response</span> {
        <span class="php-variable">$form</span> = <span class="php-variable">$this</span>-&gt;<span class="php-function">createForm</span>(<span class="php-class">ArticleType</span>::<span class="php-keyword">class</span>, <span class="php-variable">$article</span>);
        <span class="php-variable">$form</span>-&gt;<span class="php-function">handleRequest</span>(<span class="php-variable">$request</span>);

        <span class="php-keyword">if</span> (<span class="php-variable">$form</span>-&gt;<span class="php-function">isSubmitted</span>() &amp;&amp; <span class="php-variable">$form</span>-&gt;<span class="php-function">isValid</span>()) {
            <span class="php-comment">// Pas besoin de persist pour une modification</span>
            <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">flush</span>();

            <span class="php-variable">$this</span>-&gt;<span class="php-function">addFlash</span>(<span class="php-string">'success'</span>, <span class="php-string">'Article modifié avec succès !'</span>);
            <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">redirectToRoute</span>(<span class="php-string">'article_index'</span>);
        }

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">render</span>(<span class="php-string">'article/edit.html.twig'</span>, [
            <span class="php-string">'article'</span> =&gt; <span class="php-variable">$article</span>,
            <span class="php-string">'form'</span> =&gt; <span class="php-variable">$form</span>,
        ]);
    }

    <span class="php-comment">// DELETE : Supprimer un article</span>
    #[<span class="php-function">Route</span>(<span class="php-string">'/{id}'</span>, <span class="php-variable">name</span>: <span class="php-string">'article_delete'</span>, <span class="php-variable">methods</span>: [<span class="php-string">'POST'</span>])]
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">delete</span>(
        <span class="php-class">Request</span> <span class="php-variable">$request</span>,
        <span class="php-class">Article</span> <span class="php-variable">$article</span>,
        <span class="php-class">EntityManagerInterface</span> <span class="php-variable">$entityManager</span>
    ): <span class="php-class">Response</span> {
        <span class="php-keyword">if</span> (<span class="php-variable">$this</span>-&gt;<span class="php-function">isCsrfTokenValid</span>(<span class="php-string">'delete'</span> . <span class="php-variable">$article</span>-&gt;<span class="php-function">getId</span>(), <span class="php-variable">$request</span>-&gt;<span class="php-function">request</span>-&gt;<span class="php-function">get</span>(<span class="php-string">'_token'</span>))) {
            <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">remove</span>(<span class="php-variable">$article</span>);
            <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">flush</span>();

            <span class="php-variable">$this</span>-&gt;<span class="php-function">addFlash</span>(<span class="php-string">'success'</span>, <span class="php-string">'Article supprimé avec succès !'</span>);
        }

        <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">redirectToRoute</span>(<span class="php-string">'article_index'</span>);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">3. Méthodes principales de l'EntityManager</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Injection de l'EntityManager dans un contrôleur</span>
<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">__construct</span>(<span class="php-class">EntityManagerInterface</span> <span class="php-variable">$entityManager</span>)
{
    <span class="php-variable">$this</span>-&gt;entityManager = <span class="php-variable">$entityManager</span>;
}

<span class="php-comment">// CRUD avec EntityManager</span>
<span class="php-variable">$article</span> = <span class="php-keyword">new</span> <span class="php-class">Article</span>();
<span class="php-variable">$article</span>-&gt;<span class="php-function">setTitle</span>(<span class="php-string">'Mon titre'</span>);
<span class="php-variable">$article</span>-&gt;<span class="php-function">setContent</span>(<span class="php-string">'Mon contenu'</span>);

<span class="php-comment">// Persist : prépare l'insertion</span>
<span class="php-variable">$entityManager</span>-&gt;<span class="php-function">persist</span>(<span class="php-variable">$article</span>);

<span class="php-comment">// Flush : exécute les requêtes SQL</span>
<span class="php-variable">$entityManager</span>-&gt;<span class="php-function">flush</span>();

<span class="php-comment">// Modification (pas besoin de persist)</span>
<span class="php-variable">$article</span>-&gt;<span class="php-function">setTitle</span>(<span class="php-string">'Nouveau titre'</span>);
<span class="php-variable">$entityManager</span>-&gt;<span class="php-function">flush</span>();

<span class="php-comment">// Suppression</span>
<span class="php-variable">$entityManager</span>-&gt;<span class="php-function">remove</span>(<span class="php-variable">$article</span>);
<span class="php-variable">$entityManager</span>-&gt;<span class="php-function">flush</span>();

<span class="php-comment">// Récupérer une entité</span>
<span class="php-variable">$article</span> = <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">find</span>(<span class="php-class">Article</span>::<span class="php-keyword">class</span>, <span class="php-number">1</span>);

<span class="php-comment">// Récupérer toutes les entités</span>
<span class="php-variable">$articles</span> = <span class="php-variable">$entityManager</span>-&gt;<span class="php-function">getRepository</span>(<span class="php-class">Article</span>::<span class="php-keyword">class</span>)-&gt;<span class="php-function">findAll</span>();</code></pre>
                </div>

                <h3 class="text-purple">4. Méthodes de recherche dans les Repository</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Dans ArticleRepository.php - Méthodes personnalisées</span>
<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findRecent</span>(<span class="php-keyword">int</span> <span class="php-variable">$maxResults</span> = <span class="php-number">10</span>): <span class="php-class">array</span>
{
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">createQueryBuilder</span>(<span class="php-string">'a'</span>)
        -&gt;<span class="php-function">andWhere</span>(<span class="php-string">'a.publishedAt IS NOT NULL'</span>)
        -&gt;<span class="php-function">orderBy</span>(<span class="php-string">'a.publishedAt'</span>, <span class="php-string">'DESC'</span>)
        -&gt;<span class="php-function">setMaxResults</span>(<span class="php-variable">$maxResults</span>)
        -&gt;<span class="php-function">getQuery</span>()
        -&gt;<span class="php-function">getResult</span>();
}

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">findByCategory</span>(<span class="php-class">Category</span> <span class="php-variable">$category</span>): <span class="php-class">array</span>
{
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">createQueryBuilder</span>(<span class="php-string">'a'</span>)
        -&gt;<span class="php-function">andWhere</span>(<span class="php-string">'a.category = :category'</span>)
        -&gt;<span class="php-function">setParameter</span>(<span class="php-string">'category'</span>, <span class="php-variable">$category</span>)
        -&gt;<span class="php-function">orderBy</span>(<span class="php-string">'a.publishedAt'</span>, <span class="php-string">'DESC'</span>)
        -&gt;<span class="php-function">getQuery</span>()
        -&gt;<span class="php-function">getResult</span>();
}

<span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">search</span>(<span class="php-keyword">string</span> <span class="php-variable">$query</span>): <span class="php-class">array</span>
{
    <span class="php-keyword">return</span> <span class="php-variable">$this</span>-&gt;<span class="php-function">createQueryBuilder</span>(<span class="php-string">'a'</span>)
        -&gt;<span class="php-function">andWhere</span>(<span class="php-string">'a.title LIKE :query OR a.content LIKE :query'</span>)
        -&gt;<span class="php-function">setParameter</span>(<span class="php-string">'query'</span>, <span class="php-string">'%'</span> . <span class="php-variable">$query</span> . <span class="php-string">'%'</span>)
        -&gt;<span class="php-function">orderBy</span>(<span class="php-string">'a.publishedAt'</span>, <span class="php-string">'DESC'</span>)
        -&gt;<span class="php-function">getQuery</span>()
        -&gt;<span class="php-function">getResult</span>();
}

<span class="php-comment">// Méthodes de recherche natives disponibles</span>
<span class="php-variable">$repository</span>-&gt;<span class="php-function">find</span>(<span class="php-number">1</span>);               <span class="php-comment">// Par ID</span>
<span class="php-variable">$repository</span>-&gt;<span class="php-function">findAll</span>();             <span class="php-comment">// Tous les enregistrements</span>
<span class="php-variable">$repository</span>-&gt;<span class="php-function">findBy</span>([...]);         <span class="php-comment">// Par critères</span>
<span class="php-variable">$repository</span>-&gt;<span class="php-function">findOneBy</span>([...]);     <span class="php-comment">// Un seul par critères</span>
<span class="php-variable">$repository</span>-&gt;<span class="php-function">count</span>([...]);          <span class="php-comment">// Compter les résultats</span></code></pre>
                </div>
            </div>

            <!-- Fixtures avec symfony make:fixtures -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Générer des données de test avec symfony make:fixtures</h2>
                <p class="textExemple">
                    Les fixtures permettent de peupler votre base de données avec des données de test pour le développement.
                </p>

                <h3 class="text-purple">1. Installation et création de fixtures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Installer le bundle de fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">composer require --dev orm-fixtures</span>

<span class="bash-comment"># Créer une classe de fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:fixtures</span>

<span class="bash-string">Comment voulez-vous nommer la classe de fixtures ?</span>
<span class="bash-parameter">[ex: AppFixtures]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">ArticleFixtures</span>

<span class="bash-success">✅ src/DataFixtures/ArticleFixtures.php créé</span></code></pre>
                </div>

                <h3 class="text-purple">2. Exemple de fixtures complètes</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">DataFixtures</span>;

<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Article</span>;
<span class="php-keyword">use</span> App\<span class="php-class">Entity</span>\<span class="php-class">Category</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Bundle</span>\<span class="php-class">FixturesBundle</span>\<span class="php-class">Fixture</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Persistence</span>\<span class="php-class">ObjectManager</span>;

<span class="php-keyword">class</span> <span class="php-class">ArticleFixtures</span> <span class="php-keyword">extends</span> <span class="php-class">Fixture</span>
{
    <span class="php-keyword">public</span> <span class="php-keyword">function</span> <span class="php-function">load</span>(<span class="php-class">ObjectManager</span> <span class="php-variable">$manager</span>): <span class="php-keyword">void</span>
    {
        <span class="php-comment">// Créer des catégories</span>
        <span class="php-variable">$categories</span> = [];
        <span class="php-variable">$categoryNames</span> = [<span class="php-string">'PHP'</span>, <span class="php-string">'Symfony'</span>, <span class="php-string">'Doctrine'</span>, <span class="php-string">'JavaScript'</span>];
        
        <span class="php-keyword">foreach</span> (<span class="php-variable">$categoryNames</span> <span class="php-keyword">as</span> <span class="php-variable">$index</span> =&gt; <span class="php-variable">$name</span>) {
            <span class="php-variable">$category</span> = <span class="php-keyword">new</span> <span class="php-class">Category</span>();
            <span class="php-variable">$category</span>-&gt;<span class="php-function">setName</span>(<span class="php-variable">$name</span>);
            <span class="php-variable">$manager</span>-&gt;<span class="php-function">persist</span>(<span class="php-variable">$category</span>);
            <span class="php-variable">$categories</span>[] = <span class="php-variable">$category</span>;
            
            <span class="php-comment">// Stocker la référence pour usage ultérieur</span>
            <span class="php-variable">$this</span>-&gt;<span class="php-function">addReference</span>(<span class="php-string">'category_'</span> . <span class="php-variable">$index</span>, <span class="php-variable">$category</span>);
        }

        <span class="php-comment">// Créer des articles</span>
        <span class="php-variable">$faker</span> = \<span class="php-class">Faker</span>\<span class="php-class">Factory</span>::<span class="php-function">create</span>(<span class="php-string">'fr_FR'</span>);
        
        <span class="php-keyword">for</span> (<span class="php-variable">$i</span> = <span class="php-number">0</span>; <span class="php-variable">$i</span> &lt; <span class="php-number">50</span>; <span class="php-variable">$i</span>++) {
            <span class="php-variable">$article</span> = <span class="php-keyword">new</span> <span class="php-class">Article</span>();
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setTitle</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">sentence</span>(<span class="php-number">6</span>));
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setContent</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">paragraphs</span>(<span class="php-number">3</span>, <span class="php-keyword">true</span>));
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setPublishedAt</span>(<span class="php-variable">$faker</span>-&gt;<span class="php-function">optional</span>(<span class="php-number">0.8</span>)-&gt;<span class="php-function">dateTimeBetween</span>(<span class="php-string">'-1 year'</span>, <span class="php-string">'now'</span>));
            
            <span class="php-comment">// Associer une catégorie aléatoire</span>
            <span class="php-variable">$article</span>-&gt;<span class="php-function">setCategory</span>(<span class="php-variable">$categories</span>[<span class="php-variable">$faker</span>-&gt;<span class="php-function">numberBetween</span>(<span class="php-number">0</span>, <span class="php-function">count</span>(<span class="php-variable">$categories</span>) - <span class="php-number">1</span>)]);
            
            <span class="php-variable">$manager</span>-&gt;<span class="php-function">persist</span>(<span class="php-variable">$article</span>);
        }

        <span class="php-variable">$manager</span>-&gt;<span class="php-function">flush</span>();
    }
}</code></pre>
                </div>

                <h3 class="text-purple">3. Charger les fixtures</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Charger toutes les fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span>

<span class="bash-string">Attention, cette action va vider la base de données. Continuer ? (oui/no) [no]</span>
<span class="bash-command">&gt;</span> <span class="bash-highlight">oui</span>

<span class="bash-success">✓ Purge de la base de données</span>
<span class="bash-success">✓ Chargement de ArticleFixtures</span>
<span class="bash-success">✅ Fixtures chargées avec succès</span>

<span class="bash-comment"># Charger une fixture spécifique</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --group=ArticleFixtures</span>

<span class="bash-comment"># Ajouter des données sans purger</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load --append</span></code></pre>
                </div>
            </div>

            <!-- Bonnes pratiques et commandes utiles -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques et commandes utiles</h2>

                <h3 class="text-purple">Commandes Doctrine essentielles</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># RÉSUMÉ DES COMMANDES PRINCIPALES</span>

<span class="bash-comment"># Configuration et base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:drop --force</span>

<span class="bash-comment"># Entités</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity --regenerate</span>  <span class="bash-comment"># Regénérer les getters/setters</span>

<span class="bash-comment"># Migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:status</span>

<span class="bash-comment"># Validation et schéma</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:validate</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:update --dump-sql</span>

<span class="bash-comment"># Fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span>

<span class="bash-comment"># Requêtes SQL</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:sql "SELECT * FROM article"</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:query:dql "SELECT a FROM App\Entity\Article a"</span></code></pre>
                </div>

                <h3 class="text-purple">Bonnes pratiques Doctrine</h3>
                <ul class="textExemple">
                    <li><strong>Utilisez toujours les migrations</strong> : Jamais de modifications directes en production</li>
                    <li><strong>Validez votre mapping</strong> : Exécutez <code>doctrine:schema:validate</code> régulièrement</li>
                    <li><strong>Nommez bien vos entités</strong> : Utilisez des noms au singulier (Article, pas Articles)</li>
                    <li><strong>Utilisez les Repository</strong> : Placez la logique de requête dans les Repository, pas dans les contrôleurs</li>
                    <li><strong>Gérez les transactions</strong> : Utilisez <code>beginTransaction()</code>, <code>commit()</code> et <code>rollback()</code> pour les opérations complexes</li>
                    <li><strong>Indexez vos colonnes</strong> : Ajoutez des index sur les colonnes fréquemment recherchées</li>
                </ul>

                <h3 class="text-purple">Optimisation des performances</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-php"><span class="php-comment">// Éviter le N+1 problème avec JOIN FETCH</span>
<span class="php-variable">$articles</span> = <span class="php-variable">$entityManager</span>
    -&gt;<span class="php-function">createQuery</span>(<span class="php-string">'
        SELECT a, c FROM App\Entity\Article a
        JOIN a.category c
        WHERE a.publishedAt IS NOT NULL
    '</span>)
    -&gt;<span class="php-function">getResult</span>();

<span class="php-comment">// Utiliser la pagination pour les grandes listes</span>
<span class="php-variable">$query</span> = <span class="php-variable">$entityManager</span>
    -&gt;<span class="php-function">getRepository</span>(<span class="php-class">Article</span>::<span class="php-keyword">class</span>)
    -&gt;<span class="php-function">createQueryBuilder</span>(<span class="php-string">'a'</span>)
    -&gt;<span class="php-function">orderBy</span>(<span class="php-string">'a.publishedAt'</span>, <span class="php-string">'DESC'</span>)
    -&gt;<span class="php-function">getQuery</span>();

<span class="php-variable">$paginator</span> = <span class="php-keyword">new</span> \<span class="php-class">Doctrine</span>\<span class="php-class">ORM</span>\<span class="php-class">Tools</span>\<span class="php-class">Pagination</span>\<span class="php-class">Paginator</span>(<span class="php-variable">$query</span>);
<span class="php-variable">$paginator</span>-&gt;<span class="php-function">getQuery</span>()
    -&gt;<span class="php-function">setFirstResult</span>(<span class="php-number">0</span>)  <span class="php-comment">// Offset</span>
    -&gt;<span class="php-function">setMaxResults</span>(<span class="php-number">10</span>); <span class="php-comment">// Limit</span></code></pre>
                </div>
            </div>

            <!-- Exercice pratique -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique : Système de blog complet</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créer un système de blog complet avec Doctrine.
                    </p>
                    <ol class="textExemple">
                        <li>Créer les entités suivantes :
                            <ul>
                                <li><code>Post</code> (titre, contenu, date de publication, slug)</li>
                                <li><code>Category</code> (nom, slug, description)</li>
                                <li><code>Comment</code> (auteur, contenu, date, post associé)</li>
                                <li><code>Tag</code> (nom, couleur) - Relation ManyToMany avec Post</li>
                            </ul>
                        </li>
                        <li>Configurer toutes les relations entre entités</li>
                        <li>Générer et exécuter les migrations</li>
                        <li>Créer des fixtures pour peupler la base de données</li>
                        <li>Créer un contrôleur avec les fonctionnalités CRUD pour les posts</li>
                        <li>Ajouter des méthodes de recherche dans les Repository</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Étapes de la solution :</h4>
                        
                        <div class="code-example">
                            <h5 class="text-purple">1. Créer les entités</h5>
                            <pre v-pre><code class="language-bash"><span class="bash-comment"># Créer les entités une par une</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Post</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Category</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Comment</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity Tag</span>

<span class="bash-comment"># Ajouter les relations</span>
<span class="bash-comment"># Post ↔ Category (ManyToOne)</span>
<span class="bash-comment"># Post ↔ Comment (OneToMany)</span>
<span class="bash-comment"># Post ↔ Tag (ManyToMany)</span></code></pre>
                        </div>

                        <div class="code-example">
                            <h5 class="text-purple">2. Exemple d'entité Post</h5>
                            <pre v-pre><code class="language-php"><span class="php-keyword">&lt;?php</span>

<span class="php-keyword">namespace</span> App\<span class="php-class">Entity</span>;

<span class="php-keyword">use</span> Doctrine\<span class="php-class">Common</span>\<span class="php-class">Collections</span>\<span class="php-class">ArrayCollection</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">Common</span>\<span class="php-class">Collections</span>\<span class="php-class">Collection</span>;
<span class="php-keyword">use</span> Doctrine\<span class="php-class">ORM</span>\<span class="php-class">Mapping</span> <span class="php-keyword">as</span> <span class="php-class">ORM</span>;

#[<span class="php-class">ORM</span>\<span class="php-function">Entity</span>]
<span class="php-keyword">class</span> <span class="php-class">Post</span>
{
    #[<span class="php-class">ORM</span>\<span class="php-function">Id</span>]
    #[<span class="php-class">ORM</span>\<span class="php-function">GeneratedValue</span>]
    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>]
    <span class="php-keyword">private</span> ?<span class="php-keyword">int</span> <span class="php-variable">$id</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">length</span>: <span class="php-number">255</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$title</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">type</span>: <span class="php-string">'text'</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$content</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">length</span>: <span class="php-number">255</span>, <span class="php-variable">unique</span>: <span class="php-keyword">true</span>)]
    <span class="php-keyword">private</span> ?<span class="php-keyword">string</span> <span class="php-variable">$slug</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">Column</span>(<span class="php-variable">type</span>: <span class="php-string">'datetime_immutable'</span>, <span class="php-variable">nullable</span>: <span class="php-keyword">true</span>)]
    <span class="php-keyword">private</span> ?\<span class="php-class">DateTimeImmutable</span> <span class="php-variable">$publishedAt</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">ManyToOne</span>(<span class="php-variable">targetEntity</span>: <span class="php-class">Category</span>::<span class="php-keyword">class</span>, <span class="php-variable">inversedBy</span>: <span class="php-string">'posts'</span>)]
    #[<span class="php-class">ORM</span>\<span class="php-function">JoinColumn</span>(<span class="php-variable">nullable</span>: <span class="php-keyword">false</span>)]
    <span class="php-keyword">private</span> ?<span class="php-class">Category</span> <span class="php-variable">$category</span> = <span class="php-keyword">null</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">OneToMany</span>(<span class="php-variable">targetEntity</span>: <span class="php-class">Comment</span>::<span class="php-keyword">class</span>, <span class="php-variable">mappedBy</span>: <span class="php-string">'post'</span>, <span class="php-variable">orphanRemoval</span>: <span class="php-keyword">true</span>)]
    <span class="php-keyword">private</span> <span class="php-class">Collection</span> <span class="php-variable">$comments</span>;

    #[<span class="php-class">ORM</span>\<span class="php-function">ManyToMany</span>(<span class="php-variable">targetEntity</span>: <span class="php-class">Tag</span>::<span class="php-keyword">class</span>, <span class="php-variable">inversedBy</span>: <span class="php-string">'posts'</span>)]
    <span class="php-keyword">private</span> <span class="php-class">Collection</span> <span class="php-variable">$tags</span>;

    <span class="php-keyword">public</span> <span class="php-keyword">function</span> __construct()
    {
        <span class="php-variable">$this</span>-&gt;comments = <span class="php-keyword">new</span> <span class="php-class">ArrayCollection</span>();
        <span class="php-variable">$this</span>-&gt;tags = <span class="php-keyword">new</span> <span class="php-class">ArrayCollection</span>();
    }

    <span class="php-comment">// Getters et Setters...</span>
}</code></pre>
                        </div>
                    </div>
                </details>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>
                <p class="textExemple">
                    Félicitations ! Vous maîtrisez maintenant les bases de Doctrine dans Symfony.
                    Vous savez configurer une base de données, créer des entités, gérer les migrations,
                    et effectuer des opérations CRUD avec l'EntityManager et les Repository.
                </p>

                <h3 class="text-purple">Résumé des commandes clés</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"><span class="bash-comment"># Gestion de la base de données</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:database:create</span>

<span class="bash-comment"># Gestion des entités</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:entity --regenerate</span>

<span class="bash-comment"># Gestion des migrations</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:migration</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:migrations:migrate</span>

<span class="bash-comment"># Validation et fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:schema:validate</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony make:fixtures</span>
<span class="bash-prompt">$</span> <span class="bash-command">symfony console doctrine:fixtures:load</span></code></pre>
                </div>

                <h3 class="text-purple">Prochaines étapes :</h3>
                <ul class="textExemple">
                    <li>Apprendre à utiliser les événements Doctrine (Lifecycle Callbacks)</li>
                    <li>Découvrir les requêtes DQL (Doctrine Query Language) avancées</li>
                    <li>Explorer les fonctionnalités avancées comme les héritages d'entités</li>
                    <li>Apprendre à optimiser les performances avec le cache de requêtes</li>
                    <li>Découvrir les filtres Doctrine pour la multi-location ou la soft-deletion</li>
                </ul>

                <h3 class="text-purple">Ressources supplémentaires :</h3>
                <ul class="textExemple">
                    <li><a href="https://symfony.com/doc/current/doctrine.html" target="_blank"
                            class="btn-purple btn-hover">Documentation officielle de Doctrine dans Symfony</a></li>
                    <li><a href="https://www.doctrine-project.org/projects/doctrine-orm/en/current/reference/association-mapping.html" target="_blank"
                            class="btn-purple btn-hover">Documentation des relations Doctrine</a></li>
                    <li><a href="https://symfonycasts.com/screencast/doctrine" target="_blank" class="btn-purple btn-hover">Tutoriels vidéo SymfonyCasts sur Doctrine</a></li>
                    <li><a href="https://github.com/doctrine/DoctrineFixturesBundle" target="_blank" class="btn-purple btn-hover">Bundle Doctrine Fixtures</a></li>
                    <li><a href="https://github.com/doctrine/DoctrineMigrationsBundle" target="_blank" class="btn-purple btn-hover">Bundle Doctrine Migrations</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DoctrineLessonPage',
    
    mounted() {
        // Optionnel : Ajouter la coloration syntaxique si vous utilisez Prism.js ou similaire
        if (typeof Prism !== 'undefined') {
            Prism.highlightAll();
        }
    }
}
</script>

<style scoped>
/* Les styles sont identiques à la leçon précédente */
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

.tip h4::before {
    content: '💡';
    font-size: 1.2rem;
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