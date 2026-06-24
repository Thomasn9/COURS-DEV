<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête -->
            <header class="lesson-header">
                <h1 class="text-white">Doctrine, Entités et Migrations</h1>
                <p class="lesson-meta text-white">Étape 3 • Doctrine ORM • Migrations • Repositories • EntityType</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    Dans les leçons précédentes, les joueurs étaient stockés en session. C'était suffisant
                    pour démarrer, mais le jeu nécessite maintenant une vraie base de données : on veut
                    stocker des catégories, des types de questions, des questions, et une configuration de partie.
                </p>
                <p class="textExemple">
                    Dans cette leçon, on va installer Doctrine, modéliser les entités et leurs relations,
                    créer les repositories avec des requêtes personnalisées, générer et exécuter une migration,
                    puis construire des formulaires qui lisent directement dans la base de données via
                    <code>EntityType</code>.
                </p>
                <p class="textExemple">
                    Voici la structure qu'on va mettre en place :
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-plaintext">Category ──────< QuestionType ──────< Question
                     │
GameConfig >────────< QuestionType   (ManyToMany : types activés pour la partie)</code></pre>
                </div>
            </section>

            <!-- Étape 0 : installation Doctrine -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 0 : Installer Doctrine</h2>

                <div class="textExemple">
                    <p>
                        Doctrine ORM s'installe via le pack officiel Symfony, qui inclut le bundle Doctrine,
                        le composant de migrations et les dépendances nécessaires :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Bundle Doctrine ORM
composer require symfony/orm-pack

# Bundle de migrations Doctrine
composer require doctrine/doctrine-migrations-bundle</code></pre>
                    </div>
                    <p class="textExemple">
                        Ensuite, configurez la connexion à votre base de données dans le fichier
                        <code>.env</code> à la racine du projet. Le fichier <code>.env</code> contient
                        des valeurs par défaut à adapter à votre environnement :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># .env

# Format général :
# DATABASE_URL="driver://user:password@host:port/dbname?serverVersion=version"

# Exemple MySQL / MariaDB
DATABASE_URL="mysql://root:@127.0.0.1:3306/mon_jeu?serverVersion=8.0"

# Exemple PostgreSQL
DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16"

# Exemple SQLite (pas d'installation serveur, parfait pour commencer)
DATABASE_URL="sqlite:///%kernel.project_dir%/var/app.db"</code></pre>
                    </div>
                    <p class="textExemple">
                        Une fois la variable configurée, créez la base de données (si elle n'existe pas déjà) :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console doctrine:database:create
# Affiche : Created database "mon_jeu" for connection named default</code></pre>
                    </div>
                </div>
            </section>

            <!-- Étape 1 : Entité Category -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : L'entité Category</h2>

                <div class="textExemple">
                    <p>
                        On commence par l'entité la plus simple : une catégorie de jeu. Elle a un nom, un
                        slug (identifiant URL), une description, une couleur d'affichage et une icône.
                        On la génère avec le Maker Bundle :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity Category</code></pre>
                    </div>
                    <p class="textExemple">
                        La commande démarre un assistant interactif : elle vous demande le nom de chaque
                        champ, son type Doctrine, s'il est nullable, etc. Voici les champs à saisir :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">New property name: name
Field type: string
Field length: 100
Can this field be null: no

New property name: slug
Field type: string
Field length: 50
Can this field be null: no

New property name: description
Field type: string
Field length: 255
Can this field be null: yes

New property name: color
Field type: string
Field length: 7
Can this field be null: yes

New property name: icon
Field type: string
Field length: 50
Can this field be null: yes

(Entrée vide pour terminer)</code></pre>
                    </div>
                    <p class="textExemple">
                        Le fichier généré dans <code>src/Entity/Category.php</code> ressemble à ceci (les
                        relations seront ajoutées aux étapes suivantes) :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Category.php
namespace App\Entity;

use App\Repository\CategoryRepository;
use Doctrine\Common\Collections\ArrayCollection;
use Doctrine\Common\Collections\Collection;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity(repositoryClass: CategoryRepository::class)]
#[ORM\Table(name: 'category')]
class Category
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 100)]
    private ?string $name = null;

    // Slug : identifiant court et lisible pour les URLs et la logique métier
    // ex: 'culture', 'action', 'jamais'
    #[ORM\Column(length: 50, unique: true)]
    private ?string $slug = null;

    #[ORM\Column(length: 255, nullable: true)]
    private ?string $description = null;

    // Couleur hexadécimale pour l'affichage de la carte : '#3B82F6'
    #[ORM\Column(length: 7, nullable: true)]
    private ?string $color = null;

    // Emoji ou classe CSS : '🧠', '⚡', etc.
    #[ORM\Column(length: 50, nullable: true)]
    private ?string $icon = null;

    // Les relations OneToMany seront ajoutées à l'étape 2 et 3
    #[ORM\OneToMany(mappedBy: 'category', targetEntity: QuestionType::class, orphanRemoval: true)]
    private Collection $questionTypes;

    #[ORM\OneToMany(mappedBy: 'category', targetEntity: Question::class, orphanRemoval: true)]
    private Collection $questions;

    public function __construct()
    {
        $this->questionTypes = new ArrayCollection();
        $this->questions     = new ArrayCollection();
    }

    // Getters / setters générés automatiquement par make:entity...
    public function getId(): ?int    { return $this->id; }
    public function getName(): ?string  { return $this->name; }
    public function setName(string $name): static { $this->name = $name; return $this; }
    public function getSlug(): ?string  { return $this->slug; }
    public function setSlug(string $slug): static { $this->slug = $slug; return $this; }
    public function getDescription(): ?string { return $this->description; }
    public function setDescription(?string $d): static { $this->description = $d; return $this; }
    public function getColor(): ?string  { return $this->color; }
    public function setColor(?string $c): static { $this->color = $c; return $this; }
    public function getIcon(): ?string   { return $this->icon; }
    public function setIcon(?string $i): static { $this->icon = $i; return $this; }

    public function getQuestionTypes(): Collection { return $this->questionTypes; }
    public function getQuestions(): Collection     { return $this->questions; }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Le slug : pourquoi et comment</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Le <strong>slug</strong> est un identifiant court, en minuscules, sans accents ni
                            espaces, destiné à être utilisé dans les URLs et dans la logique métier PHP.
                            Il est déclaré <code>unique: true</code> sur la colonne, ce qui crée un index
                            UNIQUE en base de données et garantit qu'on ne peut pas avoir deux catégories
                            avec le même slug. On préfère le slug à l'<code>id</code> numérique dans les
                            routes car il reste lisible et stable même après un rechargement des données.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Étape 2 : Entité QuestionType -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : L'entité QuestionType et la relation ManyToOne</h2>

                <div class="textExemple">
                    <p>
                        Un <code>QuestionType</code> est un sous-type de catégorie : par exemple, dans
                        la catégorie "Culture", on peut avoir les types "Histoire", "Sport", "Cinéma"…
                        Chaque type appartient à une seule catégorie (relation <strong>ManyToOne</strong>).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity QuestionType</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">New property name: name
Field type: string
Field length: 100

New property name: slug
Field type: string
Field length: 50

New property name: category
Field type: relation
What class should this entity be related to? Category
Relation type? ManyToOne
Is the category property allowed to be null? no
Add a new property on Category so you can access/update QuestionType objects? yes
New field name inside Category [questionTypes]: questionTypes
Do you want to activate orphanRemoval on Category.questionTypes? yes</code></pre>
                    </div>
                    <p class="textExemple">
                        Le Maker Bundle a automatiquement mis à jour l'entité <code>Category</code> pour y
                        ajouter la collection <code>$questionTypes</code> et ses méthodes
                        <code>addQuestionType</code> / <code>removeQuestionType</code>. Voici l'entité
                        <code>QuestionType</code> complète :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/QuestionType.php
namespace App\Entity;

use App\Repository\QuestionTypeRepository;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity(repositoryClass: QuestionTypeRepository::class)]
#[ORM\Table(name: 'question_type')]
class QuestionType
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private ?int $id = null;

    // Côté "many" : chaque QuestionType appartient à une Category
    #[ORM\ManyToOne(inversedBy: 'questionTypes')]
    #[ORM\JoinColumn(nullable: false)]
    private ?Category $category = null;

    #[ORM\Column(length: 100)]
    private ?string $name = null;

    #[ORM\Column(length: 50)]
    private ?string $slug = null;

    // Les questions de ce type (côté inverse de la relation)
    #[ORM\OneToMany(mappedBy: 'questionType', targetEntity: Question::class)]
    private Collection $questions;

    public function __construct()
    {
        $this->questions = new ArrayCollection();
    }

    public function getId(): ?int        { return $this->id; }
    public function getName(): ?string   { return $this->name; }
    public function setName(string $n): static { $this->name = $n; return $this; }
    public function getSlug(): ?string   { return $this->slug; }
    public function setSlug(string $s): static { $this->slug = $s; return $this; }
    public function getCategory(): ?Category  { return $this->category; }
    public function setCategory(?Category $c): static { $this->category = $c; return $this; }
    public function getQuestions(): Collection { return $this->questions; }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">ManyToOne / OneToMany : les deux faces d'une même relation</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Une relation entre deux entités a toujours deux côtés. Du côté
                            <code>QuestionType</code>, la propriété <code>$category</code> est annotée
                            <code>ManyToOne</code> (plusieurs types pour une seule catégorie) : c'est le
                            <strong>côté propriétaire</strong> qui porte la clé étrangère
                            (<code>category_id</code>) dans la table SQL. Du côté <code>Category</code>,
                            la collection <code>$questionTypes</code> est annotée <code>OneToMany</code> avec
                            <code>mappedBy: 'category'</code> : c'est le <strong>côté inverse</strong>, qui
                            n'écrit rien en base mais permet de naviguer la relation dans le sens contraire.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Étape 3 : Entité Question -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : L'entité Question</h2>

                <div class="textExemple">
                    <p>
                        La question est l'entité centrale. Elle est liée à une <code>Category</code> et
                        un <code>QuestionType</code>, et porte les données métier du jeu : le texte, la
                        réponse (uniquement pour les questions de culture générale), le nombre de gorgées
                        à boire, le niveau de contenu et un flag actif/inactif.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity Question</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Question.php
namespace App\Entity;

use App\Repository\QuestionRepository;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity(repositoryClass: QuestionRepository::class)]
#[ORM\Table(name: 'question')]
class Question
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private ?int $id = null;

    #[ORM\ManyToOne(inversedBy: 'questions')]
    #[ORM\JoinColumn(nullable: false)]
    private ?Category $category = null;

    #[ORM\ManyToOne(inversedBy: 'questions')]
    #[ORM\JoinColumn(nullable: false)]
    private ?QuestionType $questionType = null;

    // Texte principal de la question ou de l'action à réaliser
    #[ORM\Column(type: 'text')]
    private ?string $content = null;

    // Réponse correcte : uniquement pour les questions de type "Culture Générale"
    // Null pour toutes les autres catégories
    #[ORM\Column(type: 'text', nullable: true)]
    private ?string $answer = null;

    // Nombre de gorgées : combien le perdant doit boire
    #[ORM\Column]
    private int $sips = 2;

    // Chemin vers une image illustrant la question (optionnel)
    #[ORM\Column(length: 255, nullable: true)]
    private ?string $imagePath = null;

    // Niveau : 'soft' (tout public), 'normal', 'hard' (adultes)
    #[ORM\Column(length: 20)]
    private string $contentLevel = 'normal';

    // Flag pour désactiver une question sans la supprimer
    #[ORM\Column]
    private bool $isActive = true;

    #[ORM\Column]
    private \DateTimeImmutable $createdAt;

    public function __construct()
    {
        $this->createdAt = new \DateTimeImmutable();
    }

    public function getId(): ?int              { return $this->id; }
    public function getCategory(): ?Category   { return $this->category; }
    public function setCategory(?Category $c): static { $this->category = $c; return $this; }
    public function getQuestionType(): ?QuestionType { return $this->questionType; }
    public function setQuestionType(?QuestionType $qt): static { $this->questionType = $qt; return $this; }
    public function getContent(): ?string       { return $this->content; }
    public function setContent(string $c): static { $this->content = $c; return $this; }
    public function getAnswer(): ?string        { return $this->answer; }
    public function setAnswer(?string $a): static { $this->answer = $a; return $this; }
    public function getSips(): int              { return $this->sips; }
    public function setSips(int $s): static     { $this->sips = $s; return $this; }
    public function getImagePath(): ?string     { return $this->imagePath; }
    public function setImagePath(?string $p): static { $this->imagePath = $p; return $this; }
    public function getContentLevel(): string   { return $this->contentLevel; }
    public function setContentLevel(string $l): static { $this->contentLevel = $l; return $this; }
    public function isActive(): bool            { return $this->isActive; }
    public function setIsActive(bool $a): static { $this->isActive = $a; return $this; }
    public function getCreatedAt(): \DateTimeImmutable { return $this->createdAt; }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Étape 4 : Entité GameConfig + ManyToMany -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4 : L'entité GameConfig et la relation ManyToMany</h2>

                <div class="textExemple">
                    <p>
                        <code>GameConfig</code> stocke la configuration globale de la partie : le nombre de
                        questions et la liste des types de questions activés. Un <code>GameConfig</code>
                        peut avoir plusieurs <code>QuestionType</code> activés, et un même
                        <code>QuestionType</code> peut être activé dans plusieurs <code>GameConfig</code>.
                        C'est une relation <strong>ManyToMany</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:entity GameConfig</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">New property name: questionCount
Field type: integer
Can this field be null: no

New property name: enabledQuestionTypes
Field type: relation
What class should this entity be related to? QuestionType
Relation type? ManyToMany
Do you want to add a new property to QuestionType? yes
New field name inside QuestionType [gameConfigs]: gameConfigs</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/GameConfig.php
namespace App\Entity;

use App\Repository\GameConfigRepository;
use Doctrine\Common\Collections\ArrayCollection;
use Doctrine\Common\Collections\Collection;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity(repositoryClass: GameConfigRepository::class)]
#[ORM\Table(name: 'game_config')]
class GameConfig
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private ?int $id = null;

    #[ORM\Column]
    private int $questionCount = 20;

    // La relation ManyToMany génère une table de jointure automatiquement
    // "game_config_question_type" avec deux colonnes de clés étrangères
    #[ORM\ManyToMany(targetEntity: QuestionType::class, inversedBy: 'gameConfigs')]
    #[ORM\JoinTable(name: 'game_config_question_type')]
    private Collection $enabledQuestionTypes;

    #[ORM\Column]
    private \DateTimeImmutable $updatedAt;

    public function __construct()
    {
        $this->enabledQuestionTypes = new ArrayCollection();
        $this->updatedAt            = new \DateTimeImmutable();
    }

    public function getId(): ?int          { return $this->id; }
    public function getQuestionCount(): int { return $this->questionCount; }
    public function setQuestionCount(int $n): static { $this->questionCount = $n; return $this; }
    public function getUpdatedAt(): \DateTimeImmutable { return $this->updatedAt; }
    public function setUpdatedAt(\DateTimeImmutable $d): static { $this->updatedAt = $d; return $this; }

    public function getEnabledQuestionTypes(): Collection { return $this->enabledQuestionTypes; }

    public function addEnabledQuestionType(QuestionType $qt): static
    {
        if (!$this->enabledQuestionTypes->contains($qt)) {
            $this->enabledQuestionTypes->add($qt);
        }
        return $this;
    }

    public function removeEnabledQuestionType(QuestionType $qt): static
    {
        $this->enabledQuestionTypes->removeElement($qt);
        return $this;
    }

    // Méthode utilitaire : remplace toute la collection d'un coup
    public function setEnabledQuestionTypes(array $types): static
    {
        $this->enabledQuestionTypes->clear();
        foreach ($types as $type) {
            $this->addEnabledQuestionType($type);
        }
        return $this;
    }

    // Retourne les IDs (utile pour les formulaires et la logique de session)
    public function getEnabledQuestionTypeIds(): array
    {
        return $this->enabledQuestionTypes->map(fn($qt) => $qt->getId())->toArray();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">La table de jointure ManyToMany</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Une relation <code>ManyToMany</code> nécessite une <strong>table de jointure</strong>
                            en base de données. Doctrine la crée automatiquement lors de la migration. Elle
                            s'appelle ici <code>game_config_question_type</code> (défini par
                            <code>#[ORM\JoinTable]</code>) et contient deux colonnes : <code>game_config_id</code>
                            et <code>question_type_id</code>. Vous n'avez pas à créer une entité dédiée pour
                            cette table : Doctrine la gère entièrement en coulisses.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Étape 5 : Migrations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 5 : Générer et exécuter les migrations</h2>

                <div class="textExemple">
                    <p>
                        Une fois les entités créées, Doctrine peut comparer leur mapping avec la structure
                        actuelle de la base de données et générer le SQL de mise à jour sous forme de
                        <strong>fichier de migration</strong>. C'est la façon propre de faire évoluer un
                        schéma en production : chaque migration est versionnée, réversible et tracée.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># 1. Générer le fichier de migration (compare entités ↔ base de données)
php bin/console make:migration

# Le fichier est créé dans migrations/VersionYYYYMMDDHHMMSS.php
# Prenez le temps de le lire avant de l'exécuter !

# 2. Appliquer la migration à la base de données
php bin/console doctrine:migrations:migrate

# Pour voir les migrations en attente
php bin/console doctrine:migrations:status</code></pre>
                    </div>
                    <p class="textExemple">
                        Le fichier généré contient deux méthodes : <code>up()</code> (applique la migration)
                        et <code>down()</code> (l'annule). Voici à quoi ressemble une migration pour nos
                        entités :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// migrations/Version20250001000000.php
namespace DoctrineMigrations;

use Doctrine\DBAL\Schema\Schema;
use Doctrine\Migrations\AbstractMigration;

final class Version20250001000000 extends AbstractMigration
{
    public function getDescription(): string
    {
        return 'Création des tables Category, QuestionType, Question, GameConfig';
    }

    public function up(Schema $schema): void
    {
        // Doctrine génère ce SQL automatiquement depuis le mapping des entités
        $this->addSql('CREATE TABLE category (
            id          INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
            name        VARCHAR(100) NOT NULL,
            slug        VARCHAR(50)  NOT NULL UNIQUE,
            description VARCHAR(255) DEFAULT NULL,
            color       VARCHAR(7)   DEFAULT NULL,
            icon        VARCHAR(50)  DEFAULT NULL
        )');

        $this->addSql('CREATE TABLE question_type (
            id          INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
            category_id INT NOT NULL,
            name        VARCHAR(100) NOT NULL,
            slug        VARCHAR(50)  NOT NULL,
            CONSTRAINT fk_qt_category FOREIGN KEY (category_id)
                REFERENCES category(id) ON DELETE CASCADE
        )');

        $this->addSql('CREATE TABLE question (
            id               INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
            category_id      INT NOT NULL,
            question_type_id INT NOT NULL,
            content          LONGTEXT NOT NULL,
            answer           LONGTEXT DEFAULT NULL,
            sips             INT NOT NULL DEFAULT 2,
            image_path       VARCHAR(255) DEFAULT NULL,
            content_level    VARCHAR(20)  NOT NULL DEFAULT "normal",
            is_active        TINYINT(1)   NOT NULL DEFAULT 1,
            created_at       DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
            CONSTRAINT fk_q_category FOREIGN KEY (category_id)      REFERENCES category(id) ON DELETE CASCADE,
            CONSTRAINT fk_q_type     FOREIGN KEY (question_type_id) REFERENCES question_type(id) ON DELETE CASCADE
        )');

        $this->addSql('CREATE TABLE game_config (
            id             INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
            question_count INT NOT NULL DEFAULT 20,
            updated_at     DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
        )');

        // Table de jointure ManyToMany (générée automatiquement par Doctrine)
        $this->addSql('CREATE TABLE game_config_question_type (
            game_config_id   INT NOT NULL,
            question_type_id INT NOT NULL,
            PRIMARY KEY (game_config_id, question_type_id),
            CONSTRAINT fk_gcqt_config FOREIGN KEY (game_config_id)   REFERENCES game_config(id) ON DELETE CASCADE,
            CONSTRAINT fk_gcqt_type   FOREIGN KEY (question_type_id) REFERENCES question_type(id) ON DELETE CASCADE
        )');
    }

    public function down(Schema $schema): void
    {
        // Suppression dans l'ordre inverse pour respecter les clés étrangères
        $this->addSql('DROP TABLE IF EXISTS game_config_question_type');
        $this->addSql('DROP TABLE IF EXISTS game_config');
        $this->addSql('DROP TABLE IF EXISTS question');
        $this->addSql('DROP TABLE IF EXISTS question_type');
        $this->addSql('DROP TABLE IF EXISTS category');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Insérer des données de départ dans la migration</h3>
                    <p>
                        Une migration peut aussi contenir des <code>INSERT</code> pour peupler la base
                        avec des données initiales (fixtures statiques). C'est utile pour les données
                        "métier" qui ne changent pas (les catégories du jeu, par exemple) et qu'on veut
                        intégrer dès le déploiement, sans passer par les fixtures Doctrine :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans la méthode up() de la migration, après les CREATE TABLE :

// Catégories du jeu
$this->addSql("INSERT INTO category (name, slug, description, color, icon) VALUES
    ('Culture Générale', 'culture', 'Bonne réponse → tu distribues. Mauvaise réponse → tu bois !', '#3B82F6', '🧠'),
    ('Je n''ai jamais',  'jamais',  'Tu l''as fait → tu bois. Jamais fait → tu ne bois pas !',    '#8B5CF6', '🙈'),
    ('Carte Action',     'action',  'Suis la règle ou bois le nombre de gorgées indiqué.',         '#EF4444', '⚡')
");

// Types de questions par catégorie
$this->addSql("INSERT INTO question_type (category_id, name, slug) VALUES
    (1, 'Histoire',        'histoire'),
    (1, 'Sport',           'sport'),
    (1, 'Cinéma',          'cinema'),
    (1, 'Jeux vidéo',      'jeux-video'),
    (1, 'Musique',         'musique'),
    (2, 'Situation drôle', 'situation-drole'),
    (2, 'Vie quotidienne', 'vie-quotidienne'),
    (3, 'Nouvelle règle',  'nouvelle-regle'),
    (3, 'Action à faire',  'action-faire')
");

// Config par défaut (singleton id=1)
$this->addSql("INSERT INTO game_config (id, question_count, updated_at) VALUES (1, 20, NOW())");

// Activer tous les types sauf les adultes par défaut
$this->addSql("INSERT INTO game_config_question_type (game_config_id, question_type_id)
    SELECT 1, id FROM question_type
");

// Quelques questions de démonstration
$this->addSql("INSERT INTO question (category_id, question_type_id, content, answer, sips, content_level) VALUES
    (1, 1, 'En quelle année a eu lieu la Révolution française ?', '1789', 2, 'normal'),
    (1, 1, 'Qui a peint la Joconde ?',                            'Léonard de Vinci', 2, 'normal'),
    (1, 2, 'Quel pays a remporté la Coupe du Monde 2018 ?',       'France', 2, 'normal'),
    (1, 3, 'Qui joue Tony Stark dans Iron Man ?',                 'Robert Downey Jr', 2, 'normal'),
    (1, 4, 'Quel est le nom du cheval de Link dans Zelda ?',      'Épona', 3, 'hard'),
    (1, 5, 'Quel groupe a chanté Bohemian Rhapsody ?',            'Queen', 2, 'normal'),
    (2, 6, 'Je n''ai jamais... raté un high-five devant tout le monde.',             NULL, 2, 'normal'),
    (2, 7, 'Je n''ai jamais... mangé de la nourriture tombée par terre.',            NULL, 2, 'normal'),
    (3, 8, 'Nouvelle règle : interdiction de dire le mot « boire ». Erreur = 2 gorgées.', NULL, 2, 'normal'),
    (3, 9, 'Chante le refrain d''une chanson au choix du groupe ou bois 2 gorgées.', NULL, 2, 'normal')
");</code></pre>
                    </div>
                    <p class="textExemple">
                        Notez le double guillemet simple (<code>''</code>) pour échapper les apostrophes
                        dans les chaînes SQL à l'intérieur d'une chaîne PHP double-quotée.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Vérifier le résultat</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Vérifier que le schéma en base correspond aux entités (doit retourner "Nothing to update")
php bin/console doctrine:schema:validate

# Voir les tables créées directement via Doctrine
php bin/console doctrine:query:sql "SHOW TABLES"

# Revenir en arrière si besoin (annule la dernière migration)
php bin/console doctrine:migrations:migrate prev</code></pre>
                    </div>
                </div>
            </section>

            <!-- Étape 6 : Repositories -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 6 : Les Repositories et le QueryBuilder</h2>

                <div class="textExemple">
                    <p>
                        Un <strong>repository</strong> est la classe qui sert d'interface entre votre code
                        PHP et la base de données pour une entité donnée. Doctrine en génère un automatiquement
                        avec <code>make:entity</code>. Il hérite de <code>ServiceEntityRepository</code> et
                        fournit des méthodes prêtes à l'emploi (<code>find()</code>, <code>findAll()</code>,
                        <code>findBy()</code>...) que l'on complète avec des requêtes sur mesure.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">CategoryRepository : requête avec jointure</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Repository/CategoryRepository.php
namespace App\Repository;

use App\Entity\Category;
use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
use Doctrine\Persistence\ManagerRegistry;

class CategoryRepository extends ServiceEntityRepository
{
    public function __construct(ManagerRegistry $registry)
    {
        parent::__construct($registry, Category::class);
    }

    /**
     * Toutes les catégories avec leurs types préchargés en une seule requête.
     * Sans leftJoin, Doctrine ferait N requêtes supplémentaires (problème N+1).
     */
    public function findAllWithTypes(): array
    {
        return $this->createQueryBuilder('c')
            ->leftJoin('c.questionTypes', 'qt')
            ->addSelect('qt')          // inclut les types dans le résultat
            ->orderBy('c.id', 'ASC')
            ->getQuery()
            ->getResult();
    }

    public function findBySlug(string $slug): ?Category
    {
        return $this->findOneBy(['slug' => $slug]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">QuestionRepository : requête aléatoire avec filtres</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Repository/QuestionRepository.php
namespace App\Repository;

use App\Entity\Question;
use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
use Doctrine\Persistence\ManagerRegistry;

class QuestionRepository extends ServiceEntityRepository
{
    public function __construct(ManagerRegistry $registry)
    {
        parent::__construct($registry, Question::class);
    }

    /**
     * Tire une question au hasard dans une catégorie donnée,
     * parmi les types activés, en excluant les questions déjà posées.
     *
     * @param string $categorySlug   Slug de la catégorie choisie par le joueur
     * @param int[]  $enabledTypeIds IDs des types activés dans la config
     * @param int[]  $alreadyAsked   IDs des questions déjà posées dans cette partie
     */
    public function findRandom(
        string $categorySlug,
        array $enabledTypeIds,
        array $alreadyAsked = []
    ): ?Question {
        $qb = $this->createQueryBuilder('q')
            ->join('q.category', 'c')
            ->join('q.questionType', 'qt')
            ->where('c.slug = :slug')
            ->andWhere('q.isActive = true')
            ->setParameter('slug', $categorySlug);

        if (!empty($enabledTypeIds)) {
            $qb->andWhere('qt.id IN (:typeIds)')
               ->setParameter('typeIds', $enabledTypeIds);
        }

        // Exclure les questions déjà posées pendant cette partie
        if (!empty($alreadyAsked)) {
            $qb->andWhere('q.id NOT IN (:asked)')
               ->setParameter('asked', $alreadyAsked);
        }

        $results = $qb->getQuery()->getResult();

        if (empty($results)) {
            return null;
        }

        // array_rand retourne un index aléatoire dans le tableau de résultats
        return $results[array_rand($results)];
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">GameConfigRepository : pattern singleton</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Repository/GameConfigRepository.php
namespace App\Repository;

use App\Entity\GameConfig;
use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
use Doctrine\Persistence\ManagerRegistry;

class GameConfigRepository extends ServiceEntityRepository
{
    public function __construct(ManagerRegistry $registry)
    {
        parent::__construct($registry, GameConfig::class);
    }

    /**
     * Récupère la configuration globale (toujours l'id=1),
     * et la crée si elle n'existe pas encore.
     * On parle de pattern "singleton" : une seule instance partagée.
     */
    public function getOrCreate(): GameConfig
    {
        $config = $this->find(1);

        if (!$config) {
            $config = new GameConfig();
            $this->getEntityManager()->persist($config);
            $this->getEntityManager()->flush();
        }

        return $config;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Le problème N+1 et pourquoi on utilise leftJoin + addSelect</h3>
                    <div class="warning-section">
                        <p>
                            Sans <code>leftJoin</code> et <code>addSelect</code>, Doctrine charge d'abord
                            toutes les catégories en une requête, puis, chaque fois que le code accède à
                            <code>$category->getQuestionTypes()</code> dans la boucle Twig, il exécute une
                            requête supplémentaire. Avec 10 catégories, cela fait 11 requêtes au lieu d'1.
                            C'est le <strong>problème N+1</strong>. La méthode <code>findAllWithTypes()</code>
                            du <code>CategoryRepository</code> le résout en chargeant tout en une seule requête
                            avec une jointure SQL.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Étape 7 : Formulaires liés à Doctrine -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 7 : Formulaires avec EntityType</h2>

                <div class="textExemple">
                    <p>
                        <code>EntityType</code> est un type de champ Symfony qui charge automatiquement
                        les entrées depuis la base de données et les présente sous forme de
                        <code>&lt;select&gt;</code> ou de cases à cocher. C'est l'équivalent de
                        <code>ChoiceType</code> mais branché directement sur une entité Doctrine.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">QuestionFormType : formulaire d'administration</h3>
                    <p>
                        Ce formulaire sert à créer ou modifier une question. Il utilise
                        <code>EntityType</code> pour le champ <code>category</code> et un champ
                        <code>questionType</code> qui se met à jour dynamiquement selon la catégorie
                        choisie (on y revient juste après).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/QuestionFormType.php
namespace App\Form;

use App\Entity\Category;
use App\Entity\Question;
use App\Entity\QuestionType;
use Symfony\Bridge\Doctrine\Form\Type\EntityType;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\ChoiceType;
use Symfony\Component\Form\Extension\Core\Type\IntegerType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;
use Symfony\Component\Validator\Constraints\NotBlank;
use Symfony\Component\Validator\Constraints\Range;

class QuestionFormType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            // EntityType : affiche toutes les catégories en select
            ->add('category', EntityType::class, [
                'class'        => Category::class,
                // choice_label peut être une string (nom de propriété) ou un callable
                'choice_label' => fn(Category $c) => $c->getIcon() . ' ' . $c->getName(),
                'label'        => 'Catégorie',
                'placeholder'  => '-- Choisir --',
                'attr'         => ['class' => 'form-select', 'id' => 'category-select'],
                'constraints'  => [new NotBlank(message: 'Choisissez une catégorie.')],
            ])
            ->add('content', TextareaType::class, [
                'label'       => 'Texte de la question',
                'attr'        => ['class' => 'form-control', 'rows' => 3],
                'constraints' => [new NotBlank()],
            ])
            ->add('answer', TextareaType::class, [
                'label'    => 'Réponse (Culture uniquement, laisser vide sinon)',
                'required' => false,
                'attr'     => ['class' => 'form-control', 'rows' => 2],
            ])
            ->add('sips', IntegerType::class, [
                'label'       => 'Nombre de gorgées',
                'data'        => 2,
                'attr'        => ['class' => 'form-control', 'min' => 1, 'max' => 10],
                'constraints' => [new Range(min: 1, max: 10)],
            ])
            ->add('contentLevel', ChoiceType::class, [
                'label'   => 'Niveau de contenu',
                'choices' => ['Normal' => 'normal', 'Hard' => 'hard', 'Soft' => 'soft'],
                'attr'    => ['class' => 'form-select'],
            ]);

        // Le champ questionType est géré séparément via FormEvents (voir ci-dessous)
        $this->addQuestionTypeField($builder);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults(['data_class' => Question::class]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Formulaire dynamique avec FormEvents</h3>
                    <p>
                        Le champ <code>questionType</code> dépend de la catégorie sélectionnée : on ne
                        veut afficher que les types appartenant à la catégorie choisie, pas tous les types
                        de toutes les catégories. Symfony gère ça via les <strong>FormEvents</strong> :
                        des hooks qui s'exécutent à différents moments du cycle de vie du formulaire.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// À ajouter dans QuestionFormType::buildForm(), après les autres champs

use Symfony\Component\Form\FormEvents;
use Symfony\Component\Form\FormEvent;
use Symfony\Component\Form\FormInterface;

// Closure réutilisée par les deux événements
$addTypeField = function (FormInterface $form, ?Category $category) {
    $types = $category ? $category->getQuestionTypes()->toArray() : [];

    $form->add('questionType', EntityType::class, [
        'class'        => QuestionType::class,
        'choices'      => $types,    // uniquement les types de la catégorie choisie
        'choice_label' => 'name',
        'label'        => 'Type de question',
        'placeholder'  => $category ? '-- Choisir --' : '-- Choisissez d\'abord une catégorie --',
        'attr'         => ['class' => 'form-select'],
        'constraints'  => [new NotBlank(message: 'Choisissez un type.')],
    ]);
};

// PRE_SET_DATA : au chargement du formulaire (GET)
// On lit la catégorie déjà définie sur l'objet Question (mode édition)
$builder->addEventListener(FormEvents::PRE_SET_DATA, function (FormEvent $event) use ($addTypeField) {
    $question = $event->getData();
    $category = $question?->getCategory();    // null si nouvelle question
    $addTypeField($event->getForm(), $category);
});

// PRE_SUBMIT : à la soumission (POST)
// On ne peut pas charger la Category depuis l'objet ici (pas encore hydraté),
// donc on passe null et on laisse la validation côté serveur faire le reste
$builder->addEventListener(FormEvents::PRE_SUBMIT, function (FormEvent $event) use ($addTypeField) {
    $addTypeField($event->getForm(), null);
});</code></pre>
                    </div>
                    <p class="textExemple">
                        Côté JavaScript, une requête AJAX vers <code>/admin/api/types/{categoryId}</code>
                        recharge le select des types quand l'utilisateur change de catégorie dans le
                        formulaire. Côté serveur, le <code>PRE_SUBMIT</code> reconstruit le champ avec
                        <code>null</code> (tous les types acceptés) et la contrainte <code>NotBlank</code>
                        assure qu'un type a bien été soumis. Doctrine vérifiera ensuite que le type soumis
                        appartient bien à la catégorie via la validation de l'entité.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">GameConfigType : EntityType multiple avec cases à cocher</h3>
                    <p>
                        Ce formulaire permet de configurer la partie : nombre de questions et types activés.
                        Comme les types sont groupés par catégorie, on génère dynamiquement un champ
                        <code>EntityType</code> par catégorie, avec <code>multiple: true</code> et
                        <code>expanded: true</code> pour obtenir des cases à cocher.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/GameConfigType.php
namespace App\Form;

use App\Entity\Category;
use App\Entity\GameConfig;
use App\Entity\QuestionType;
use Symfony\Bridge\Doctrine\Form\Type\EntityType;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\IntegerType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;
use Symfony\Component\Validator\Constraints\Range;

class GameConfigType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        /** @var Category[] $categories */
        $categories = $options['categories'];   // passées depuis le Controller

        $builder->add('questionCount', IntegerType::class, [
            'label'       => 'Nombre de questions',
            'attr'        => ['class' => 'form-control', 'min' => 5, 'max' => 100],
            'constraints' => [new Range(min: 5, max: 100)],
        ]);

        // Un groupe de cases à cocher par catégorie
        foreach ($categories as $category) {
            $builder->add('types_' . $category->getSlug(), EntityType::class, [
                'class'        => QuestionType::class,
                'choices'      => $category->getQuestionTypes(),  // types de cette catégorie
                'choice_label' => 'name',
                'multiple'     => true,     // plusieurs sélections possibles
                'expanded'     => true,     // rendu en checkboxes plutôt qu'en select
                'mapped'       => false,    // ce champ n'est PAS lié directement à l'entité
                'label'        => $category->getIcon() . ' ' . $category->getName(),
                // Pré-cocher les types déjà activés dans la config
                'data'         => $options['selected_types'][$category->getSlug()] ?? [],
            ]);
        }
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class'     => GameConfig::class,
            'categories'     => [],    // injectées depuis le Controller
            'selected_types' => [],    // types déjà activés, par slug de catégorie
        ]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">mapped: false — quand le champ ne correspond pas à une propriété</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Par défaut, Symfony essaie de faire correspondre chaque champ du formulaire à
                            une propriété de l'entité liée (<code>data_class</code>). Ici, les champs
                            <code>types_culture</code>, <code>types_action</code>, etc. n'existent pas comme
                            propriétés sur <code>GameConfig</code>. On passe <code>'mapped' => false</code>
                            pour dire à Symfony de ne pas tenter ce mapping automatique. Le Controller
                            récupère alors manuellement les données de ces champs avec
                            <code>$form->get('types_culture')->getData()</code> et les traite lui-même.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Récapitulatif -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récapitulatif : ordre de mise en place</h2>
                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># 1. Installer Doctrine et configurer DATABASE_URL dans .env
composer require symfony/orm-pack doctrine/doctrine-migrations-bundle
php bin/console doctrine:database:create

# 2. Créer les entités dans l'ordre (du moins dépendant au plus dépendant)
php bin/console make:entity Category
php bin/console make:entity QuestionType    # → déclare la relation ManyToOne vers Category
php bin/console make:entity Question        # → déclare les relations vers Category et QuestionType
php bin/console make:entity GameConfig      # → déclare la relation ManyToMany vers QuestionType

# 3. Générer et appliquer la migration
php bin/console make:migration
php bin/console doctrine:migrations:migrate

# 4. Vérifier
php bin/console doctrine:schema:validate

# 5. Créer les formulaires
php bin/console make:form QuestionFormType Question
php bin/console make:form GameConfigType GameConfig</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Ce qu'on a appliqué dans cette leçon</h3>
                    <ul>
                        <li><strong>Entités dans l'ordre de dépendance</strong> : on crée d'abord <code>Category</code> avant <code>QuestionType</code> qui en dépend, pour éviter les erreurs de référence circulaire dans le Maker</li>
                        <li><strong>Slugs uniques</strong> : préférés aux IDs dans les routes et la logique métier car plus lisibles et stables</li>
                        <li><strong>orphanRemoval: true</strong> sur les OneToMany : supprime automatiquement les types et questions orphelins quand on supprime une catégorie</li>
                        <li><strong>findAllWithTypes() avec leftJoin</strong> : évite le problème N+1 en chargeant les relations en une seule requête</li>
                        <li><strong>Données de test dans la migration</strong> : les catégories et types du jeu ne changent pas, les intégrer dans la migration garantit qu'ils existent dès le premier déploiement</li>
                        <li><strong>mapped: false</strong> pour les champs qui ne correspondent pas à une propriété de l'entité mais sont gérés manuellement dans le Controller</li>
                        <li><strong>FormEvents</strong> pour les champs dynamiques : <code>PRE_SET_DATA</code> au chargement, <code>PRE_SUBMIT</code> à la soumission</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Le projet a maintenant une vraie base de données, des entités bien structurées avec
                        leurs relations, des repositories avec des requêtes sur mesure, et des formulaires
                        capables de lire et d'écrire en base. L'architecture mise en place ici (entités →
                        repositories → forms → controllers) est la même que vous retrouverez dans n'importe
                        quel projet Symfony de taille réelle.
                    </p>
                    <p>
                        <strong>Prochaine leçon</strong> : le moteur de jeu avec <code>GameService</code>,
                        la gestion de l'état de partie en session et les controllers
                        <code>SetupController</code> / <code>GameController</code>.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyDoctrineLesson',

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
                        const twigScript = document.createElement('script');
                        twigScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/twig.min.js';
                        twigScript.onload = resolve;
                        document.head.appendChild(twigScript);
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