<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Migrations Doctrine avec Symfony</h1>
                <p class="lesson-meta text-white">Symfony • Doctrine • Base de données • Migration • Versionnement</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Migrations</h2>
                <p class="textExemple">
                    Les migrations sont un système de versionnement pour votre schéma de base de données.
                    Elles permettent de modifier la structure de votre BDD (création/modification/suppression de tables, colonnes, index, contraintes)
                    de manière progressive, reproductible et sans perte de données.
                </p>
                <p class="textExemple">
                    Dans Symfony, Doctrine Migrations est l'outil officiel. Chaque migration est une classe PHP
                    contenant deux méthodes : <code>up()</code> (pour appliquer les changements) et <code>down()</code>
                    (pour les annuler). Toutes les migrations sont stockées dans le dossier <code>migrations/</code>
                    et peuvent être exécutées ou annulées dans l'ordre.
                </p>
            </section>

            <!-- Pourquoi les migrations ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser les migrations ?</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Versionnement</strong> : Chaque migration est un fichier versionné dans Git, l’équipe applique les mêmes changements.</li>
                        <li><strong>Reproductibilité</strong> : Tous les environnements (dev, staging, prod) restent synchronisés.</li>
                        <li><strong>Rollback possible</strong> : Possibilité de revenir à un état antérieur (si <code>down()</code> est correctement implémenté).</li>
                        <li><strong>Automatisation</strong> : Intégration facile dans une pipeline CI/CD.</li>
                        <li><strong>Sécurité</strong> : Pas de modification manuelle de la BDD en production.</li>
                    </ul>
                </div>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et configuration</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Installer Doctrine Migrations</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer le bundle (déjà inclus dans symfony/webapp-pack)
composer require doctrine/doctrine-migrations-bundle

# Si vous partez d'un projet minimal
composer require symfony/orm-pack
composer require --dev symfony/maker-bundle</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Configuration (config/packages/doctrine_migrations.yaml)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml"># config/packages/doctrine_migrations.yaml
doctrine_migrations:
    migrations_paths:
        'DoctrineMigrations': '%kernel.project_dir%/migrations'
    enable_profiler: false
    organize_migrations: false
    # Personnalisation du nom des classes
    custom_template: null
    # Connexion à utiliser (si plusieurs)
    connection: default
    # Storage pour l'historique des migrations
    storage:
        table_storage:
            table_name: 'doctrine_migration_versions'
            version_column_name: 'version'
            version_column_length: 191
            executed_at_column_name: 'executed_at'</code></pre>
                    </div>
                </div>
            </section>

            <!-- Création d'une migration -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer une migration</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Méthode 1 : Génération automatique (recommandée)</h3>
                    <p>Après avoir modifié vos entités Doctrine, lancez :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Compare le schéma actuel avec les entités et génère la migration
php bin/console doctrine:migrations:diff

# Avec MakerBundle (alias plus court)
php bin/console make:migration</code></pre>
                    </div>
                    <p>Exemple : vous ajoutez une propriété <code>description</code> dans l'entité <code>Article</code> :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Article.php
#[ORM\Column(type: 'text', nullable: true)]
private ?string $description = null;</code></pre>
                    </div>
                    <p>La commande <code>make:migration</code> génère automatiquement :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// migrations/Version20250315120000.php
final class Version20250315120000 extends AbstractMigration
{
    public function up(Schema $schema): void
    {
        $this->addSql('ALTER TABLE article ADD description LONGTEXT DEFAULT NULL');
    }

    public function down(Schema $schema): void
    {
        $this->addSql('ALTER TABLE article DROP description');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Méthode 2 : Migration vide (écriture manuelle)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console doctrine:migrations:generate</code></pre>
                    </div>
                    <p>Vous pouvez alors écrire vos propres requêtes SQL :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">public function up(Schema $schema): void
{
    $this->addSql('CREATE INDEX idx_article_date ON article (created_at)');
    $this->addSql('UPDATE article SET status = "published" WHERE published_at IS NOT NULL');
}

public function down(Schema $schema): void
{
    $this->addSql('DROP INDEX idx_article_date ON article');
    $this->addSql('UPDATE article SET status = "draft"');
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Structure d'une migration -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure d'une classe de migration</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// migrations/Version20250315120000.php
declare(strict_types=1);

namespace DoctrineMigrations;

use Doctrine\DBAL\Schema\Schema;
use Doctrine\Migrations\AbstractMigration;

final class Version20250315120000 extends AbstractMigration
{
    // Description optionnelle (affichée dans la console)
    public function getDescription(): string
    {
        return 'Ajout de la colonne description sur la table article';
    }

    // ⬆️ Applique la migration : ajoute/modifie la structure
    public function up(Schema $schema): void
    {
        // addSql() accepte plusieurs requêtes séparées
        $this->addSql('ALTER TABLE article ADD COLUMN description TEXT');
        $this->addSql('CREATE INDEX idx_article_date ON article (created_at)');
    }

    // ⬇️ Annule la migration : revient à l'état précédent
    public function down(Schema $schema): void
    {
        $this->addSql('ALTER TABLE article DROP COLUMN description');
        $this->addSql('DROP INDEX idx_article_date ON article');
    }
}</code></pre>
                    </div>
                    <p class="textExemple">
                        <strong>⚠️ Important</strong> : Doctrine ne peut pas deviner le contenu de <code>down()</code> automatiquement
                        pour les migrations complexes. Vérifiez toujours que la méthode <code>down()</code> est correcte.
                    </p>
                </div>
            </section>

            <!-- Exécution des migrations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exécuter les migrations</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Commandes principales</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Appliquer toutes les migrations non encore exécutées
php bin/console doctrine:migrations:migrate

# Appliquer jusqu'à une version spécifique
php bin/console doctrine:migrations:migrate 'DoctrineMigrations\Version20250315120000'

# Simuler l'exécution (dry-run) sans toucher à la BDD
php bin/console doctrine:migrations:migrate --dry-run

# Exécuter une seule migration (même si déjà exécutée)
php bin/console doctrine:migrations:execute --up 'DoctrineMigrations\Version20250315120000'

# Annuler la dernière migration (exécute down())
php bin/console doctrine:migrations:migrate prev

# Annuler et revenir à une version antérieure
php bin/console doctrine:migrations:migrate 'DoctrineMigrations\Version20250310120000'</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Voir l'état des migrations</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Liste toutes les migrations avec leur statut (executed/pending)
php bin/console doctrine:migrations:status

# Affiche le SQL des migrations sans les exécuter
php bin/console doctrine:migrations:migrate --write-sql

# Affiche la dernière version exécutée
php bin/console doctrine:migrations:latest</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des données dans les migrations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Migrations de données (Data migrations)</h2>

                <div class="textExemple">
                    <p>
                        Il est fréquent d'avoir besoin de migrer des données existantes lors d'un changement de schéma.
                        Exemple : transformer une colonne <code>full_name</code> en <code>first_name</code> et <code>last_name</code>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">final class Version20250315130000 extends AbstractMigration
{
    public function up(Schema $schema): void
    {
        // 1. Ajouter les nouvelles colonnes
        $this->addSql('ALTER TABLE user ADD first_name VARCHAR(100) DEFAULT NULL, ADD last_name VARCHAR(100) DEFAULT NULL');

        // 2. Migrer les données existantes
        $this->addSql('UPDATE user SET first_name = SUBSTRING_INDEX(full_name, " ", 1), last_name = SUBSTRING_INDEX(full_name, " ", -1)');

        // 3. Rendre les colonnes NOT NULL après migration
        $this->addSql('ALTER TABLE user MODIFY first_name VARCHAR(100) NOT NULL, MODIFY last_name VARCHAR(100) NOT NULL');

        // 4. Supprimer l'ancienne colonne
        $this->addSql('ALTER TABLE user DROP full_name');
    }

    public function down(Schema $schema): void
    {
        $this->addSql('ALTER TABLE user ADD full_name VARCHAR(200) DEFAULT NULL');
        $this->addSql('UPDATE user SET full_name = CONCAT(first_name, " ", last_name)');
        $this->addSql('ALTER TABLE user DROP first_name, DROP last_name');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utiliser le QueryBuilder ou l'EntityManager (déconseillé)</h3>
                    <p>
                        Dans une migration, évitez d'utiliser l'EntityManager car les entités peuvent avoir changé.
                        Préférez les requêtes SQL brutes avec <code>$this->addSql()</code>.
                        Si vous devez absolument utiliser des objets, utilisez <code>Schema</code> et <code>Connection</code> :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">public function up(Schema $schema): void
{
    $this->connection->executeStatement('UPDATE user SET role = "admin" WHERE is_admin = 1');
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques des migrations</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Ne jamais modifier manuellement une migration déjà exécutée en production</strong> – créez une nouvelle migration de correction.</li>
                        <li><strong>Tester <code>down()</code></strong> : assurez-vous que le rollback fonctionne.</li>
                        <li><strong>Une migration = une seule responsabilité</strong> : évitez de mélanger des changements indépendants.</li>
                        <li><strong>Versionnez toutes les migrations dans Git</strong>.</li>
                        <li><strong>Utilisez <code>--dry-run</code> avant d'exécuter en production</strong>.</li>
                        <li><strong>Évitez les instructions destructives sans <code>down()</code> symétrique</strong> (DROP TABLE, DROP COLUMN).</li>
                        <li><strong>Pour les très grosses tables</strong>, privilégiez des migrations par lots ou des opérations sans verrouillage (pt-online-schema-change).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Migration en environnement de production</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># 1. Sauvegarder la BDD (indispensable)
mysqldump -u user -p ma_base > backup_before_migration.sql

# 2. Simuler
php bin/console doctrine:migrations:migrate --dry-run --env=prod

# 3. Exécuter (de préférence pendant une fenêtre de maintenance)
php bin/console doctrine:migrations:migrate --env=prod

# 4. Vérifier les logs et les données</code></pre>
                    </div>
                </div>
            </section>

            <!-- Problèmes courants -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Problèmes fréquents et solutions</h2>

                <div class="textExemple">
                    <div class="warning-section">
                        <h4 class="text-purple">1. Migration bloquée : "already at latest version"</h4>
                        <p>La migration est déjà marquée comme exécutée dans la table <code>doctrine_migration_versions</code>.<br>
                        Solution : supprimer la ligne correspondante ou utiliser <code>--force</code>.</p>
                    </div>

                    <div class="warning-section">
                        <h4 class="text-purple">2. Erreur de dépendances circulaires (clés étrangères)</h4>
                        <p>Désactivez temporairement les contraintes :</p>
                        <pre v-pre><code class="language-php">public function up(Schema $schema): void
{
    $this->addSql('SET FOREIGN_KEY_CHECKS=0');
    // vos opérations
    $this->addSql('SET FOREIGN_KEY_CHECKS=1');
}</code></pre>
                    </div>

                    <div class="warning-section">
                        <h4 class="text-purple">3. Migration générée vide après modification d'entité</h4>
                        <p>Vérifiez que la table de métadonnées existe et que Doctrine a bien accès à la BDD.
                        Parfois un <code>php bin/console doctrine:cache:clear-metadata</code> résout le problème.</p>
                    </div>

                    <div class="warning-section">
                        <h4 class="text-purple">4. Conflit de plateformes (MySQL vs PostgreSQL)</h4>
                        <p>Utilisez des types Doctrine (ex: <code>string</code>, <code>text</code>, <code>integer</code>) plutôt que des types SQL directs.</p>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Première migration</h3>
                    <p>Créez une entité <code>Category</code> avec les champs : id (auto-incrément), name (string, 100), slug (string, unique).</p>
                    <p>Générez la migration et exécutez-la. Vérifiez la table dans votre SGBD.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:entity Category
# Ajouter les champs name (string, 100) et slug (string, 100, unique)
php bin/console make:migration
php bin/console doctrine:migrations:migrate</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Migration de données</h3>
                    <p>Dans une entité <code>Product</code>, remplacez la colonne <code>price_ht</code> par <code>price_ttc</code> (TVA 20%).
                    Écrivez une migration qui convertit les anciennes données (price_ttc = price_ht * 1.2) et supprime price_ht.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">public function up(Schema $schema): void
{
    $this->addSql('ALTER TABLE product ADD price_ttc NUMERIC(10,2) DEFAULT NULL');
    $this->addSql('UPDATE product SET price_ttc = price_ht * 1.2');
    $this->addSql('ALTER TABLE product MODIFY price_ttc NUMERIC(10,2) NOT NULL');
    $this->addSql('ALTER TABLE product DROP price_ht');
}

public function down(Schema $schema): void
{
    $this->addSql('ALTER TABLE product ADD price_ht NUMERIC(10,2) DEFAULT NULL');
    $this->addSql('UPDATE product SET price_ht = price_ttc / 1.2');
    $this->addSql('ALTER TABLE product MODIFY price_ht NUMERIC(10,2) NOT NULL');
    $this->addSql('ALTER TABLE product DROP price_ttc');
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Rollback et versionnement</h3>
                    <p>Exécutez la migration de l'exercice 1, puis annulez-la (<code>migrate prev</code>). Vérifiez que la table <code>category</code> a disparu.
                    Refaites la migration et vérifiez que tout est rétabli.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash"># Appliquer
php bin/console doctrine:migrations:migrate

# Annuler la dernière
php bin/console doctrine:migrations:migrate prev

# Réappliquer
php bin/console doctrine:migrations:migrate</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Intégration continue -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Automatisation avec CI/CD</h2>
                <div class="textExemple">
                    <p>Exemple de job GitLab CI pour exécuter les migrations automatiquement en staging/production :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">deploy:
  stage: deploy
  script:
    - composer install --no-dev
    - php bin/console doctrine:migrations:migrate --no-interaction --allow-no-migration
  only:
    - main
  environment: production</code></pre>
                    </div>
                    <p>Sur SymfonyCloud / Platform.sh, ajoutez dans <code>.platform.app.yaml</code> :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-yaml">hooks:
    deploy: |
        php bin/console doctrine:migrations:migrate --no-interaction</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Les migrations Doctrine sont un outil indispensable pour gérer l'évolution de votre base de données
                        dans un projet Symfony. Elles apportent rigueur, traçabilité et sécurité.
                    </p>
                    <ul>
                        <li><strong>Ne jamais modifier une migration exécutée en production</strong> → créer une nouvelle migration.</li>
                        <li><strong>Toujours tester <code>down()</code></strong> pour pouvoir annuler rapidement en cas d'incident.</li>
                        <li><strong>Préférer <code>make:migration</code> pour la génération automatique</strong>, mais savoir écrire du SQL manuel pour les cas complexes.</li>
                    </ul>
                    <p>
                        Prochaines leçons : migrations avancées (plateformes multiples, fixtures de données avec <code>doctrine:fixtures:load</code>,
                        et gestion des migrations dans un environnement distribué).
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'DoctrineMigrationsLesson',

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
                    // Charger les langages nécessaires (bash, php, yaml)
                    const languages = ['bash', 'php', 'yaml'];
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
            // Appliquer la coloration sur tous les blocs de code
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
/* === TOUS LES STYLES SONT IDENTIQUES À CEUX DU FORMULAIRE === */
/* Je les reproduis intégralement pour que la leçon soit autonome */

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