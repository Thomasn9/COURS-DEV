<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Création d'utilisateur SQL</h1>
                <p class="lesson-meta text-white">SQL • MySQL • PostgreSQL • Oracle • Gestion des droits</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    La gestion des utilisateurs est une composante fondamentale de l'administration d'une base de données.
                    Créer un utilisateur SQL consiste à définir une identité de connexion, puis à lui accorder des droits
                    adaptés à son rôle. Ce document présente la procédure complète, étape par étape, applicable aux principaux SGBD :
                    MySQL/MariaDB, PostgreSQL et Oracle.
                </p>
                <p class="textExemple">
                    Un utilisateur SQL est distinct du compte système : il n'existe qu'au sein du SGBD et ne peut interagir
                    qu'avec les bases de données pour lesquelles il a reçu des autorisations.
                </p>
            </section>

            <!-- Prérequis -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis</h2>
                <div class="textExemple">
                    <ul>
                        <li>Disposer d'un accès administrateur (<code>root</code> ou super-utilisateur) à la base de données.</li>
                        <li>Connaître le SGBD utilisé (MySQL, PostgreSQL, Oracle...).</li>
                        <li>Avoir défini le périmètre d'action de l'utilisateur : quelles bases, quelles opérations.</li>
                        <li>S'assurer que le serveur de base de données est démarré et accessible.</li>
                    </ul>
                </div>
            </section>

            <!-- Connexion en tant qu'administrateur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Connexion en tant qu'administrateur</h2>
                <p class="textExemple">
                    La première étape consiste à se connecter au serveur de base de données avec un compte disposant
                    des privilèges suffisants pour créer des utilisateurs.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">MySQL / MariaDB</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">mysql -u root -p</code></pre>
                    </div>
                    <p>Le système demande le mot de passe root. Une fois connecté, le prompt <code>mysql&gt;</code> apparaît.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">PostgreSQL</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">sudo -u postgres psql</code></pre>
                    </div>
                    <p>Ou via le compte superutilisateur : <code>psql -U postgres</code>.</p>
                </div>
            </section>

            <!-- Création de l'utilisateur (MySQL) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Création d'un utilisateur (MySQL/MariaDB)</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe de base</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">CREATE USER 'nom_utilisateur'@'hôte' IDENTIFIED BY 'mot_de_passe';</code></pre>
                    </div>
                    <p>Exemple concret — créer un utilisateur <code>jean_dupont</code> autorisé à se connecter localement :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">CREATE USER 'jean_dupont'@'localhost' IDENTIFIED BY 'MotDePasse_S3cur!';</code></pre>
                    </div>

                    <table class="lesson-table">
                        <thead>
                            <tr><th>Paramètre</th><th>Description</th></tr>
                        </thead>
                        <tbody>
                            <tr><td><code>'jean_dupont'</code></td><td>Nom de l'utilisateur (identifiant de connexion)</td></tr>
                            <tr><td><code>'localhost'</code></td><td>Hôte autorisé (localhost = machine locale, '%' = tout hôte)</td></tr>
                            <tr><td><code>IDENTIFIED BY</code></td><td>Définit le mot de passe de l'utilisateur</td></tr>
                            <tr><td><code>'MotDePasse_S3cur!'</code></td><td>Mot de passe (respecter les règles de complexité)</td></tr>
                        </tbody>
                    </table>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Variante avec IF NOT EXISTS</h3>
                    <p>Pour éviter une erreur si l'utilisateur existe déjà :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">CREATE USER IF NOT EXISTS 'jean_dupont'@'localhost' IDENTIFIED BY 'MotDePasse_S3cur!';</code></pre>
                    </div>
                    <p class="note">⚠️ La clause <code>IF NOT EXISTS</code> est disponible à partir de MySQL 5.7.6 et MariaDB 10.1.3.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisateur accessible depuis n'importe quel hôte</h3>
                    <p>Pour autoriser la connexion depuis n'importe quelle adresse IP, on utilise le caractère générique <code>'%'</code>.
                        <strong>Cette pratique doit être réservée aux environnements de développement.</strong></p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">CREATE USER 'jean_dupont'@'%' IDENTIFIED BY 'MotDePasse_S3cur!';</code></pre>
                    </div>
                </div>
            </section>

            <!-- Attribution des privilèges -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Attribution des privilèges</h2>
                <p class="textExemple">
                    Un utilisateur nouvellement créé ne possède aucun droit. Il est nécessaire de lui accorder explicitement
                    des privilèges à l'aide de la commande <code>GRANT</code>.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Syntaxe générale</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">GRANT privilege1, privilege2, ... ON base_de_donnees.table TO 'nom_utilisateur'@'hôte';</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples courants</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">-- Tous les droits sur une base spécifique
GRANT ALL PRIVILEGES ON ma_base.* TO 'jean_dupont'@'localhost';

-- Uniquement la lecture (SELECT)
GRANT SELECT ON ma_base.* TO 'jean_dupont'@'localhost';

-- Lecture, insertion et modification sur une table précise
GRANT SELECT, INSERT, UPDATE ON ma_base.ma_table TO 'jean_dupont'@'localhost';</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Principaux privilèges disponibles</h3>
                    <table class="lesson-table">
                        <thead><tr><th>Commande</th><th>Description</th></tr></thead>
                        <tbody>
                            <tr><td><code>ALL PRIVILEGES</code></td><td>Tous les droits (sauf GRANT OPTION)</td></tr>
                            <tr><td><code>SELECT</code></td><td>Lecture des données</td></tr>
                            <tr><td><code>INSERT</code></td><td>Insertion de nouvelles lignes</td></tr>
                            <tr><td><code>UPDATE</code></td><td>Modification des données existantes</td></tr>
                            <tr><td><code>DELETE</code></td><td>Suppression de lignes</td></tr>
                            <tr><td><code>CREATE</code></td><td>Création de bases et de tables</td></tr>
                            <tr><td><code>DROP</code></td><td>Suppression de bases et de tables</td></tr>
                            <tr><td><code>INDEX</code></td><td>Gestion des index</td></tr>
                            <tr><td><code>EXECUTE</code></td><td>Exécution de procédures stockées</td></tr>
                        </tbody>
                    </table>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Application des privilèges</h3>
                    <p>Après toute modification des privilèges, il est recommandé d'exécuter :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">FLUSH PRIVILEGES;</code></pre>
                    </div>
                    <p class="note">⚠️ Depuis MySQL 5.7, <code>FLUSH PRIVILEGES</code> n'est plus strictement nécessaire lorsque l'on utilise <code>GRANT</code>, mais reste une bonne pratique.</p>
                </div>
            </section>

            <!-- Vérification -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Vérification</h2>
                <p class="textExemple">Il est important de vérifier que l'utilisateur a bien été créé et que ses droits sont correctement attribués.</p>

                <div class="textExemple">
                    <h3 class="text-purple">Lister les utilisateurs</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">SELECT user, host FROM mysql.user;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Afficher les privilèges d'un utilisateur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">SHOW GRANTS FOR 'jean_dupont'@'localhost';</code></pre>
                    </div>
                    <p>Résultat attendu :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">+--------------------------------------------------------------------+
| Grants for jean_dupont@localhost                                   |
+--------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'jean_dupont'@'localhost'                    |
| GRANT ALL PRIVILEGES ON `ma_base`.* TO 'jean_dupont'@'localhost'   |
+--------------------------------------------------------------------+</code></pre>
                    </div>
                </div>
            </section>

            <!-- Syntaxes pour d'autres SGBD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxes pour d'autres SGBD</h2>

                <div class="textExemple">
                    <h3 class="text-purple">PostgreSQL</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">-- Créer le rôle (utilisateur)
CREATE ROLE jean_dupont WITH LOGIN PASSWORD 'MotDePasse_S3cur!';

-- Accorder des droits sur une base
GRANT CONNECT ON DATABASE ma_base TO jean_dupont;
GRANT USAGE ON SCHEMA public TO jean_dupont;
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA public TO jean_dupont;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Oracle</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">-- Créer l'utilisateur
CREATE USER jean_dupont IDENTIFIED BY MotDePasse_S3cur!
  DEFAULT TABLESPACE users
  TEMPORARY TABLESPACE temp;

-- Accorder la connexion et les droits
GRANT CREATE SESSION TO jean_dupont;
GRANT SELECT, INSERT ON ma_table TO jean_dupont;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Modification et suppression -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Modification et suppression d'un utilisateur</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Modifier le mot de passe</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">-- MySQL 5.7.6+
ALTER USER 'jean_dupont'@'localhost' IDENTIFIED BY 'NouveauMDP_2024!';

-- Ancienne syntaxe
SET PASSWORD FOR 'jean_dupont'@'localhost' = PASSWORD('NouveauMDP_2024!');</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Révoquer des privilèges</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">REVOKE ALL PRIVILEGES ON ma_base.* FROM 'jean_dupont'@'localhost';
FLUSH PRIVILEGES;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Supprimer un utilisateur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">DROP USER 'jean_dupont'@'localhost';</code></pre>
                    </div>
                    <p class="note">⚠️ La suppression d'un utilisateur révoque automatiquement tous ses privilèges. Elle est irréversible.</p>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul class="textExemple">
                    <li><strong>Principe du moindre privilège</strong> : n'accorder que les droits strictement nécessaires à l'utilisateur pour accomplir sa mission.</li>
                    <li><strong>Utiliser des mots de passe complexes</strong> : majuscules, minuscules, chiffres et caractères spéciaux, d'au moins 12 caractères.</li>
                    <li><strong>Éviter le caractère '%' comme hôte en production</strong> : restreindre les connexions à des adresses IP ou hôtes spécifiques.</li>
                    <li><strong>Ne jamais utiliser le compte root pour les applications</strong> : créer un compte dédié avec les droits minimaux.</li>
                    <li><strong>Documenter les comptes créés</strong> : tenir un registre des utilisateurs, de leurs droits et de leur objectif.</li>
                    <li><strong>Auditer régulièrement les comptes</strong> : supprimer les utilisateurs inactifs ou obsolètes.</li>
                </ul>
            </section>

            <!-- Récapitulatif des commandes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récapitulatif des commandes (MySQL)</h2>
                <p class="textExemple">Voici la séquence complète pour créer un utilisateur opérationnel :</p>
                <div class="code-example">
                    <pre v-pre><code class="language-sql">-- 1. Connexion en tant qu'administrateur
mysql -u root -p

-- 2. Création de l'utilisateur
CREATE USER 'jean_dupont'@'localhost' IDENTIFIED BY 'MotDePasse_S3cur!';

-- 3. Attribution des privilèges
GRANT ALL PRIVILEGES ON ma_base.* TO 'jean_dupont'@'localhost';

-- 4. Actualisation des droits
FLUSH PRIVILEGES;

-- 5. Vérification
SHOW GRANTS FOR 'jean_dupont'@'localhost';</code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Création d'un utilisateur pour une application web</h3>
                    <p>Vous administrez une base de données MySQL pour une application de blog. Créez un utilisateur <code>blog_app</code> avec :</p>
                    <ul>
                        <li>Connexion autorisée uniquement depuis le réseau local (IP 192.168.1.0/24 → utilisez '192.168.1.%')</li>
                        <li>Mot de passe robuste (ex: "BlogP@ss2024!")</li>
                        <li>Privilèges : SELECT, INSERT, UPDATE, DELETE sur la base <code>blog_db</code></li>
                        <li>Pas de droit de création/modification de structure (CREATE, DROP, ALTER)</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-sql">CREATE USER 'blog_app'@'192.168.1.%' IDENTIFIED BY 'BlogP@ss2024!';
GRANT SELECT, INSERT, UPDATE, DELETE ON blog_db.* TO 'blog_app'@'192.168.1.%';
FLUSH PRIVILEGES;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Utilisateur en lecture seule</h3>
                    <p>Un analyste a besoin de consulter les données de la base <code>reporting</code> (toutes les tables) sans pouvoir les modifier. Créez l'utilisateur <code>analyst</code> avec les droits appropriés, accessible uniquement depuis <code>localhost</code>.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-sql">CREATE USER 'analyst'@'localhost' IDENTIFIED BY 'ReadOnly2024!';
GRANT SELECT ON reporting.* TO 'analyst'@'localhost';
FLUSH PRIVILEGES;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Suppression d'un utilisateur obsolète</h3>
                    <p>L'utilisateur <code>old_dev</code> n'est plus utilisé. Supprimez-le définitivement ainsi que tous ses privilèges.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-sql">DROP USER 'old_dev'@'localhost';</code></pre>
                            <p>La commande <code>DROP USER</code> révoque automatiquement tous les privilèges.</p>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    La gestion fine des utilisateurs SQL est une compétence essentielle pour tout administrateur de base de données.
                    En appliquant le principe du moindre privilège, en utilisant des mots de passe forts et en restreignant les hôtes de connexion,
                    vous renforcez considérablement la sécurité de vos données.
                </p>
                <p class="textExemple">
                    Les commandes <code>CREATE USER</code>, <code>GRANT</code> et <code>REVOKE</code> sont les piliers de cette gestion.
                    Pensez à vérifier régulièrement les droits attribués avec <code>SHOW GRANTS</code> et à nettoyer les comptes obsolètes.
                </p>
                <p class="textExemple">
                    Prochaine étape : apprendre à gérer les rôles (GROUP ROLE) pour simplifier l'administration des droits sur des ensembles d'utilisateurs similaires.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SqlUserLesson',

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
                    // Charger les langages SQL, Bash et Plaintext
                    const languages = ['sql', 'bash', 'plaintext'];
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
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
/* Reprise exacte des styles du template Symfony, avec ajout du style pour les tableaux */
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
.border-purple { border: 2px solid #e0d6ff; transition: all 0.3s ease; }
.text-purple { color: #6A3093 !important; }
.text-white { color: white !important; }

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

.lesson-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.lesson-table th, .lesson-table td {
    border: 1px solid #ddd;
    padding: 10px 12px;
    text-align: left;
    vertical-align: top;
}

.lesson-table th {
    background: #6A3093;
    color: white;
    font-weight: 600;
}

.lesson-table tr:nth-child(even) {
    background-color: #f9f9f9;
}

.note {
    background: #fff3cd;
    border-left: 4px solid #ffc107;
    padding: 0.75rem 1rem;
    margin: 1rem 0;
    border-radius: 4px;
    font-size: 0.95rem;
}

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
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
    .lesson-table th, .lesson-table td { padding: 6px 8px; }
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