<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Introduction à Spring Boot</h1>
            </header>

            <!-- Objectifs d'apprentissage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">Objectifs d'apprentissage</h2>
                <p class="textExemple">
                    Cette leçon vous présente Spring Boot, un framework essentiel dans l'écosystème Java moderne. À la
                    fin de cette introduction, vous comprendrez ses principes fondamentaux, ses avantages et son rôle
                    dans le développement d'applications d'entreprise.
                </p>
                <ul class="textExemple">
                    <li>Comprendre la philosophie et les objectifs de Spring Boot</li>
                    <li>Identifier les problèmes que Spring Boot résout</li>
                    <li>Connaître les caractéristiques principales du framework</li>
                    <li>Comprendre l'écosystème Spring Boot et ses composants</li>
                    <li>Savoir quand et pourquoi utiliser Spring Boot dans vos projets</li>
                </ul>
            </section>

            <!-- Qu'est-ce que Spring Boot ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">Qu'est-ce que Spring Boot ?</h2>

                <p class="textExemple">
                    Spring Boot est un framework open-source basé sur le célèbre framework Spring, conçu pour simplifier
                    radicalement le développement d'applications Java d'entreprise. Il représente une approche
                    "convention plutôt que configuration", permettant aux développeurs de créer rapidement des
                    applications de production prêtes à l'emploi.
                </p>

                <p class="textExemple">
                    Le principal objectif de Spring Boot est de réduire la complexité de configuration inhérente aux
                    applications Spring traditionnelles. Avant Spring Boot, les développeurs passaient un temps
                    considérable à configurer manuellement les fichiers XML, les dépendances et les intégrations. Spring
                    Boot automatise cette configuration grâce à des mécanismes intelligents d'auto-configuration.
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h4 class="text-purple">Approche traditionnelle Spring</h4>
                        <pre><code>
<span class="comment">// Configuration manuelle complexe</span>
<span class="comment">// Fichiers XML volumineux</span>
<span class="comment">// Intégrations manuelles</span>
<span class="comment">// Dépendances difficiles à gérer</span>
            </code></pre>
                    </div>

                    <div class="code-block">
                        <h4 class="text-purple">Approche Spring Boot</h4>
                        <pre><code>
<span class="comment">// Configuration automatique</span>
<span class="comment">// Convention over configuration</span>
<span class="comment">// Serveurs embarqués inclus</span>
<span class="comment">// Dépendances prédéfinies</span>
            </code></pre>
                    </div>
                </div>
            </section>

            <!-- À quoi sert Spring Boot ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">À quoi sert Spring Boot ?</h2>

                <p class="textExemple">
                    Spring Boot est conçu pour répondre à plusieurs besoins spécifiques dans le développement
                    d'applications modernes :
                </p>

                <h3 class="text-purple mt-4">Accélération du développement</h3>
                <p class="textExemple">
                    Spring Boot réduit considérablement le temps nécessaire pour démarrer un nouveau projet. Avec ses
                    "starters" préconfigurés, vous pouvez ajouter des fonctionnalités comme l'accès aux bases de
                    données, la sécurité, ou les services web REST avec seulement quelques lignes de configuration.
                    Cette approche permet aux équipes de développement de se concentrer sur la logique métier plutôt que
                    sur l'infrastructure technique.
                </p>

                <h3 class="text-purple mt-4">Simplification de la configuration</h3>
                <p class="textExemple">
                    Le framework utilise le principe de "convention plutôt que configuration". Cela signifie que Spring
                    Boot fournit des valeurs par défaut intelligentes basées sur les dépendances présentes dans votre
                    projet. Par exemple, si vous ajoutez une dépendance à une base de données MySQL, Spring Boot
                    configure automatiquement un DataSource avec des paramètres raisonnables. Vous pouvez toujours
                    personnaliser ces configurations, mais vous n'êtes pas obligé de tout configurer manuellement.
                </p>

                <h3 class="text-purple mt-4">Applications prêtes pour la production</h3>
                <p class="textExemple">
                    Spring Boot inclut des fonctionnalités essentielles pour les applications de production : gestion de
                    la santé de l'application (health checks), métriques, configuration externalisée, et plus encore.
                    Ces fonctionnalités sont intégrées directement dans le framework, éliminant le besoin d'implémenter
                    ces aspects infrastructurels manuellement.
                </p>

                <h3 class="text-purple mt-4">Microservices et architecture moderne</h3>
                <p class="textExemple">
                    Spring Boot est particulièrement adapté au développement de microservices. Sa nature légère, sa
                    démarche rapide, et son support natif pour les architectures cloud en font un choix populaire pour
                    les applications décomposées. Le framework s'intègre parfaitement avec Spring Cloud pour fournir des
                    fonctionnalités avancées de microservices comme la découverte de service, la configuration
                    centralisée, et la tolérance aux pannes.
                </p>
            </section>

            <!-- Caractéristiques principales -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">Caractéristiques principales de Spring Boot</h2>

                <h3 class="text-purple mt-4">Serveurs embarqués</h3>
                <p class="textExemple">
                    Contrairement aux applications Java traditionnelles qui nécessitent l'installation et la
                    configuration d'un serveur d'application externe (comme Tomcat, JBoss, ou WebSphere), Spring Boot
                    inclut des serveurs web directement dans votre application. Vous pouvez exécuter votre application
                    comme un simple fichier JAR, et elle contiendra son propre serveur web embarqué. Cette approche
                    simplifie le déploiement et rend les applications plus portables.
                </p>

                <h3 class="text-purple mt-4">Auto-configuration intelligente</h3>
                <p class="textExemple">
                    Spring Boot analyse votre classpath et vos dépendances pour devoir automatiquement comment
                    configurer votre application. Si vous ajoutez une base de données H2 en dépendance, Spring Boot
                    configurera un DataSource en mémoire. Si vous ajoutez Spring Security, il configurera une sécurité
                    basique. Cette intelligence réduit considérablement le code de configuration requis.
                </p>

                <h3 class="text-purple mt-4">Actuators pour le monitoring</h3>
                <p class="textExemple">
                    Spring Boot Actuator fournit des endpoints HTTP prêts à l'emploi pour surveiller et gérer votre
                    application en production. Vous pouvez vérifier la santé de l'application, consulter les métriques
                    de performance, afficher les informations de configuration, et même redémarrer certaines
                    fonctionnalités sans arrêter l'application entière.
                </p>

                <h3 class="text-purple mt-4">Configuration externalisée</h3>
                <p class="textExemple">
                    Spring Boot permet de gérer la configuration de votre application à travers différents profils et
                    sources externes. Vous pouvez avoir des configurations différentes pour le développement, les tests,
                    et la production, et les changer facilement sans recompiler votre application. Le framework supporte
                    les fichiers properties, YAML, les variables d'environnement, et même les serveurs de configuration
                    distants.
                </p>
            </section>

            <!-- Écosystème Spring Boot -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">L'écosystème Spring Boot</h2>

                <p class="textExemple">
                    Spring Boot fait partie d'un écosystème plus large de projets Spring, chacun spécialisé dans un
                    domaine particulier :
                </p>

                <h3 class="text-purple mt-4">Spring Framework Core</h3>
                <p class="textExemple">
                    Le fondement de tout l'écosystème, fournissant l'injection de dépendances, la programmation orientée
                    aspect (AOP), et les fonctionnalités de base. Spring Boot s'appuie sur ce noyau et le simplifie.
                </p>

                <h3 class="text-purple mt-4">Spring Data</h3>
                <p class="textExemple">
                    Simplifie l'accès aux données en fournissant une abstraction cohérente sur différentes technologies
                    de persistance (JPA, MongoDB, Cassandra, Redis, etc.). Spring Boot intègre automatiquement Spring
                    Data basé sur les dépendances détectées.
                </p>

                <h3 class="text-purple mt-4">Spring Security</h3>
                <p class="textExemple">
                    Offre une sécurité complète pour les applications, incluant l'authentification, l'autorisation, et
                    la protection contre les attaques courantes. Spring Boot configure automatiquement une sécurité
                    basique et permet une personnalisation avancée.
                </p>

                <h3 class="text-purple mt-4">Spring Cloud</h3>
                <p class="textExemple">
                    Étend Spring Boot pour le développement d'applications cloud-native et de microservices, fournissant
                    des outils pour la configuration distribuée, la découverte de service, et les patterns de
                    résilience.
                </p>

                <h3 class="text-purple mt-4">Spring Batch</h3>
                <p class="textExemple">
                    Conçu pour le traitement par lots (batch processing) de grands volumes de données. Spring Boot
                    facilite la création et l'exécution de jobs batch avec une configuration minimale.
                </p>
            </section>

            <!-- Quand utiliser Spring Boot ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">Quand utiliser Spring Boot ?</h2>

                <p class="textExemple">
                    Spring Boot est particulièrement adapté dans les scénarios suivants :
                </p>

                <h3 class="text-purple mt-4">Nouveaux projets d'entreprise</h3>
                <p class="textExemple">
                    Pour tout nouveau projet Java nécessitant une architecture robuste, maintenable, et prête pour la
                    production. Spring Boot accélère le démarrage et réduit la complexité initiale.
                </p>

                <h3 class="text-purple mt-4">Microservices</h3>
                <p class="textExemple">
                    Lorsque vous construisez une architecture de microservices, Spring Boot fournit la légèreté et la
                    rapidité nécessaires, tout en offrant toutes les fonctionnalités d'entreprise requises.
                </p>

                <h3 class="text-purple mt-4">Prototypage rapide</h3>
                <p class="textExemple">
                    Pour créer rapidement des preuves de concept ou des prototypes fonctionnels. Spring Boot permet de
                    valider des idées sans s'embourber dans la configuration.
                </p>

                <h3 class="text-purple mt-4">Applications cloud-native</h3>
                <p class="textExemple">
                    Pour les applications conçues pour fonctionner dans des environnements cloud, avec besoin
                    d'évolutivité, de résilience, et d'observabilité.
                </p>

                <h3 class="text-purple mt-4">Migration vers des technologies modernes</h3>
                <p class="textExemple">
                    Pour moderniser des applications legacy en les réécrivant avec des architectures et des pratiques
                    modernes, tout en bénéficiant de la stabilité et de la maturité de l'écosystème Spring.
                </p>

                <p class="textExemple mt-4">
                    Cependant, Spring Boot peut être moins adapté pour des applications extrêmement légères où la taille
                    de l'empreinte mémoire est critique, ou pour des projets où vous avez besoin d'un contrôle absolu
                    sur chaque aspect de la configuration.
                </p>
            </section>

            <!-- Exemple minimal de code -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-3">Exemple minimal illustratif</h2>

                <p class="textExemple">
                    Pour illustrer la simplicité de Spring Boot, voici à quoi ressemble une application complète :
                </p>

                <div class="code-example">
                    <pre><code>
<span class="comment">// La classe principale - point d'entrée de l'application</span>
<span class="annotation">@SpringBootApplication</span>
<span class="keyword">public class</span> <span class="class-name">MonApplication</span> {
    
    <span class="keyword">public static void</span> <span class="function">main</span>(String[] args) {
        <span class="comment">// Une seule ligne pour démarrer toute l'application</span>
        SpringApplication.<span class="function">run</span>(MonApplication.<span class="keyword">class</span>, args);
    }
}

<span class="comment">// Un contrôleur REST basique</span>
<span class="annotation">@RestController</span>
<span class="keyword">public class</span> <span class="class-name">AccueilController</span> {

    <span class="annotation">@GetMapping</span>(<span class="string">"/"</span>)
    <span class="keyword">public</span> String <span class="function">accueil</span>() {
        <span class="keyword">return</span> <span class="string">"Application Spring Boot en marche !"</span>;
    }
}
        </code></pre>
                </div>

                <p class="textExemple mt-3">
                    Avec seulement ces quelques lignes de code, vous avez une application web complète avec un serveur
                    embarqué, prête à accepter des requêtes HTTP. Spring Boot gère automatiquement la configuration du
                    serveur web, le mapping des requêtes, et toutes les infrastructures sous-jacentes.
                </p>
            </section>

            <!-- Conclusion et prochaines étapes -->
            <section class="lesson-section bg-gradient-primary">
                <h2 class="text-white mb-3">Conclusion et prochaines étapes</h2>

                <p class="text-white">
                    Spring Boot a révolutionné le développement d'applications Java en réduisant radicalement la
                    complexité de configuration et en accélérant le temps de développement. En adoptant le principe de
                    "convention plutôt que configuration", il permet aux développeurs de se concentrer sur la logique
                    métier plutôt que sur l'infrastructure technique.
                </p>

                <p class="text-white mt-3">
                    Son succès réside dans sa capacité à combiner la puissance de l'écosystème Spring avec la simplicité
                    d'utilisation. Que vous développiez une API REST simple, une application web complète, ou un système
                    de microservices complexe, Spring Boot fournit les outils et les conventions nécessaires pour
                    travailler efficacement.
                </p>

                <p class="text-white mt-3">
                    Dans les leçons suivantes, nous explorerons plus en détail comment créer des applications Spring
                    Boot, travailler avec des bases de données, implémenter la sécurité, et déployer vos applications en
                    production.
                </p>

                <div class="mt-4">
                    <h3 class="text-white">Pour aller plus loin</h3>
                    <ul class="text-white">
                        <li>Documentation officielle de Spring Boot</li>
                        <li>Guide de démarrage avec Spring Initializr</li>
                        <li>Bonnes pratiques pour les applications Spring Boot en production</li>
                        <li>Intégration avec les bases de données relationnelles et NoSQL</li>
                        <li>Développement d'APIs REST avec Spring Boot</li>
                    </ul>
                </div>
            </section>
        </div>
    </div>
</template>

<script setup>

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

/* Header avec le style gradient */
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

/* Sections de leçon */
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

/* Classes CSS de l'autre page */
.bg-gradient-primary {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
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

/* Boutons */
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

.btn-hover {
    position: relative;
    overflow: hidden;
}

.btn-hover::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 50%;
    transition: all 0.5s ease;
    transform: translate(-50%, -50%);
}

.btn-hover:hover::after {
    width: 300px;
    height: 300px;
}

/* CORRECTION RESPONSIVE POUR LES BLOCS DE CODE */
.code-example,
.code-block {
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
    max-width: 100%;
    width: 100%;
    box-sizing: border-box;
    white-space: pre-wrap;
    word-wrap: break-word;
    word-break: break-word;
}

pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs syntaxiques supplémentaires pour Java */
.keyword {
    color: #c586c0 !important;
}

.variable {
    color: #9cdcfe !important;
}

.string {
    color: #ce9178 !important;
}

.comment {
    color: #6a9955 !important;
}

.function {
    color: #dcdcaa !important;
}

.operator {
    color: #d4d4d4 !important;
}

.constant {
    color: #4fc1ff !important;
}

.number {
    color: #b5cea8 !important;
}

.class-name {
    color: #4ec9b0 !important;
}

.annotation {
    color: #569cd6 !important;
}

/* Texte des exemples */
.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* RESPONSIVE DESIGN AMÉLIORÉ */
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

    .code-comparison {
        grid-template-columns: 1fr;
        gap: 1rem;
    }

    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
    }

    .btn-purple {
        display: block;
        margin: 0.5rem 0;
        width: 100%;
        text-align: center;
    }

    .ml-2 {
        margin-left: 0 !important;
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

@media (min-width: 1400px) {
    .lesson-content {
        max-width: 1300px;
    }
}

/* Animations */
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

.lesson-section:nth-child(1) {
    animation-delay: 0.1s;
}

.lesson-section:nth-child(2) {
    animation-delay: 0.2s;
}

.lesson-section:nth-child(3) {
    animation-delay: 0.3s;
}

.lesson-section:nth-child(4) {
    animation-delay: 0.4s;
}

.lesson-section:nth-child(5) {
    animation-delay: 0.5s;
}

/* Utilitaires */
.mb-3 {
    margin-bottom: 1rem;
}

.mt-3 {
    margin-top: 1rem;
}

.mt-4 {
    margin-top: 1.5rem;
}

.ml-2 {
    margin-left: 0.5rem;
}
</style>