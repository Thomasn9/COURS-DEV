<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Le Modèle MVC en PHP</h1>
                <p class="lesson-meta text-white">Comprendre l'architecture Modèle-Vue-Contrôleur étape par étape</p>
            </header>

            <!-- Introduction avec schéma global -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction au Modèle MVC</h2>
                <p>
                    Le modèle MVC (Modèle-Vue-Contrôleur) est une architecture logicielle qui sépare une application en
                    trois composants interconnectés. Cette séparation permet une meilleure organisation du code, une
                    maintenance facilitée et une réutilisation des composants.
                </p>

                <!-- Zone pour schéma global MVC -->
                <div class="schema-container">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Schéma complet du modèle MVC en PHP"
                            class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <h3 class="text-purple">Schéma Global MVC</h3>
                        <p>Vue d'ensemble du flux de données dans l'architecture MVC</p>
                    </div>
                </div>

                <p>
                    Dans le contexte PHP, le MVC est souvent utilisé dans les frameworks comme Laravel, Symfony ou
                    CodeIgniter. Analysons maintenant chaque étape du processus illustré dans votre schéma.
                </p>
            </section>

            <!-- Étape 1: Le Client -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1: Le Client</h2>
                <p>
                    Tout commence par le <strong>client</strong> (navigateur web) qui envoie une requête HTTP vers le
                    serveur.
                </p>
                <div class="code-example">
                    <pre><code>Requête HTTP: GET http://localhost:8000</code></pre>
                </div>

                <!-- Zone pour schéma client -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Client du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Client → Requête HTTP</p>
                    </div>
                </div>

                <p>
                    Cette requête contient des informations sur l'action demandée (GET, POST, etc.), l'URL cible, et
                    éventuellement des données.
                </p>
            </section>

            <!-- Étape 2: Le Routeur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2: Le Routeur</h2>
                <p>
                    Le <strong>routeur</strong> (Router) intercepte la requête HTTP et détermine quel contrôleur doit
                    traiter cette requête en fonction de l'URL et de la méthode HTTP.
                </p>
                <div class="code-example">
                    <pre><code>Router: Analyse l'URL et appelle le contrôleur approprié</code></pre>
                </div>

                <!-- Zone pour schéma routeur -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Routeur du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Requête HTTP → Router → Contrôleur</p>
                    </div>
                </div>

                <p>
                    Le routeur fait le lien entre l'URL demandée et la méthode du contrôleur qui doit être exécutée.
                </p>
            </section>

            <!-- Étape 3: Le Contrôleur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3: Le Contrôleur</h2>
                <p>
                    Le <strong>contrôleur</strong> (Controller) reçoit la requête du routeur. Son rôle est de coordonner
                    les actions nécessaires pour répondre à la requête.
                </p>
                <div class="code-example">
                    <pre><code>Controller: Reçoit la requête, appelle les services nécessaires, et prépare la réponse</code></pre>
                </div>

                <!-- Zone pour schéma contrôleur -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Contrôleur du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Contrôleur → Service</p>
                    </div>
                </div>

                <p>
                    Le contrôleur ne contient pas la logique métier directement. Il délègue cette responsabilité aux
                    services.
                </p>
            </section>

            <!-- Étape 4: Le Service (Logique Métier) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4: Le Service (Logique Métier)</h2>
                <p>
                    Le <strong>service</strong> contient la logique métier de l'application. Il traite les données,
                    applique les règles métier, et prépare les informations nécessaires.
                </p>
                <div class="code-example">
                    <pre><code>Service: Contient la logique métier, traite les données</code></pre>
                </div>

                <!-- Zone pour schéma service -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Service du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Service → Repository</p>
                    </div>
                </div>

                <p>
                    Les services sont responsables de l'application des règles métier et de la coordination entre
                    différents composants.
                </p>
            </section>

            <!-- Étape 5: Le Repository (Interaction avec la BDD) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 5: Le Repository (Interaction avec la BDD)</h2>
                <p>
                    Le <strong>repository</strong> est responsable de toutes les interactions avec la base de données.
                    Il exécute les requêtes SQL et retourne les résultats.
                </p>
                <div class="code-example">
                    <pre><code>Repository: Exécute les requêtes SQL et retourne les données</code></pre>
                </div>

                <!-- Zone pour schéma repository -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Repository du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Repository → BDD</p>
                    </div>
                </div>

                <p>
                    Le repository isole la couche d'accès aux données, permettant de changer facilement de système de
                    base de données si nécessaire.
                </p>
            </section>

            <!-- Étape 6: Les Entities (Objets Métiers) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 6: Les Entities (Objets Métiers)</h2>
                <p>
                    Les <strong>entities</strong> représentent les objets métiers de l'application. Ce sont généralement
                    des classes PHP qui mappent les tables de la base de données.
                </p>
                <div class="code-example">
                    <pre><code>Entity: Représente un objet métier (ex: User, Product, Order)</code></pre>
                </div>

                <!-- Zone pour schéma entities -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Entities du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Entity (objets métiers)</p>
                    </div>
                </div>

                <p>
                    Les entities contiennent les données et éventuellement des méthodes pour manipuler ces données.
                </p>
            </section>

            <!-- Étape 7: La Vue (Template) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 7: La Vue (Template)</h2>
                <p>
                    La <strong>vue</strong> (Template) est responsable de l'affichage des données. Elle reçoit les
                    données du contrôleur et les présente à l'utilisateur.
                </p>
                <div class="code-example">
                    <pre><code>Vue: Affiche les données dans un format HTML</code></pre>
                </div>

                <!-- Zone pour schéma vue -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Vue du schéma MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Vue → Réponse HTTP</p>
                    </div>
                </div>

                <p>
                    La vue ne contient pas de logique métier, seulement de la logique d'affichage.
                </p>
            </section>

            <!-- Étape 8: La Réponse HTTP -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 8: La Réponse HTTP</h2>
                <p>
                    Enfin, le contrôleur retourne une <strong>réponse HTTP</strong> au client. Cette réponse contient:
                </p>
                <ul>
                    <li>Un <strong>header</strong> avec les métadonnées</li>
                    <li>Un <strong>code status</strong> (200, 404, 500, etc.)</li>
                    <li>Un <strong>body</strong> avec le contenu (généralement du HTML)</li>
                </ul>
                <div class="code-example">
                    <pre><code>Réponse HTTP: header + code status + body (HTML généré par la vue)</code></pre>
                </div>

                <!-- Zone pour schéma réponse HTTP -->
                <div class="schema-container mini-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Partie Réponse HTTP du schéma MVC"
                            class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <p>Réponse HTTP → Client</p>
                    </div>
                </div>
            </section>

            <!-- Flux Complet avec schéma détaillé -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Flux Complet du MVC</h2>
                <p>
                    En résumé, le flux complet d'une requête dans une architecture MVC est le suivant:
                </p>

                <!-- Zone pour schéma détaillé du flux complet -->
                <div class="schema-container large-schema">
                    <div class="schema-image-wrapper">
                        <img src="/img_php/logiquemMvc.png" alt="Schéma détaillé du flux MVC" class="schema-image">
                    </div>
                    <div class="schema-caption">
                        <h3 class="text-purple">Schéma Détaillé du Flux MVC</h3>
                        <p>Visualisation complète du processus MVC avec toutes les interactions</p>
                    </div>
                </div>

                <ol class="flow-list">
                    <li><strong>Client</strong> → Requête HTTP</li>
                    <li><strong>Routeur</strong> → Analyse et redirection</li>
                    <li><strong>Contrôleur</strong> → Coordination</li>
                    <li><strong>Service</strong> → Logique métier</li>
                    <li><strong>Repository</strong> → Interaction BDD</li>
                    <li><strong>Entity</strong> → Objets métiers</li>
                    <li><strong>Vue</strong> → Affichage</li>
                    <li><strong>Contrôleur</strong> → Réponse HTTP</li>
                    <li><strong>Client</strong> → Réception de la réponse</li>
                </ol>
                <p>
                    Cette architecture permet une séparation claire des préoccupations, rendant le code plus
                    maintenable, testable et évolutif.
                </p>
            </section>

            <!-- Avantages du MVC -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages du Modèle MVC</h2>
                <div class="advantages-grid">
                    <div class="advantage-card">
                        <h4 class="text-purple">Séparation des préoccupations</h4>
                        <p>Chaque composant a un rôle spécifique et bien défini</p>
                    </div>
                    <div class="advantage-card">
                        <h4 class="text-purple">Réutilisation du code</h4>
                        <p>Les modèles et vues peuvent être réutilisés dans différentes parties de l'application</p>
                    </div>
                    <div class="advantage-card">
                        <h4 class="text-purple">Maintenance facilitée</h4>
                        <p>Les modifications sont localisées et n'affectent pas l'ensemble de l'application</p>
                    </div>
                    <div class="advantage-card">
                        <h4 class="text-purple">Développement parallèle</h4>
                        <p>Plusieurs développeurs peuvent travailler simultanément sur différentes parties</p>
                    </div>
                    <div class="advantage-card">
                        <h4 class="text-purple">Testabilité</h4>
                        <p>Chaque composant peut être testé indépendamment des autres</p>
                    </div>
                    <div class="advantage-card">
                        <h4 class="text-purple">Évolutivité</h4>
                        <p>L'architecture facilite l'ajout de nouvelles fonctionnalités</p>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MVCLesson',
    // Vous pouvez ajouter ici des données ou méthodes si nécessaire
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

/* STYLES POUR LES ZONES DE SCHÉMA AMÉLIORÉES */
.schema-container {
    margin: 2rem 0;
    border-radius: 12px;
    background: white;
    box-shadow: 0 4px 15px rgba(106, 48, 147, 0.1);
    transition: all 0.3s ease;
    overflow: hidden;
}

.schema-container:hover {
    box-shadow: 0 8px 25px rgba(106, 48, 147, 0.15);
    transform: translateY(-2px);
}

.schema-image-wrapper {
    position: relative;
    width: 100%;
    overflow: hidden;
    background: #f8f9fa;
}

.schema-image {
    width: 100%;
    height: auto;
    display: block;
    transition: transform 0.3s ease;
}

.schema-container:hover .schema-image {
    transform: scale(1.02);
}

.schema-highlight {
    position: absolute;
    border: 3px solid #8B5FBF;
    border-radius: 8px;
    background: rgba(139, 95, 191, 0.2);
    pointer-events: none;
    animation: pulse 2s infinite;
}

.schema-caption {
    padding: 1.5rem;
    text-align: center;
    background: linear-gradient(135deg, #f8f6ff 0%, #ffffff 100%);
}

.schema-caption h3 {
    margin-bottom: 0.5rem;
}

.schema-caption p {
    color: #666;
    font-size: 0.95rem;
    margin: 0;
}

/* Schémas de différentes tailles */
.mini-schema {
    max-width: 500px;
    margin-left: auto;
    margin-right: auto;
}

.mini-schema .schema-image-wrapper {
    max-height: 200px;
}

.mini-schema .schema-image {
    max-height: 200px;
    object-fit: contain;
}

.large-schema .schema-image-wrapper {
    max-height: 500px;
}

.large-schema .schema-image {
    max-height: 500px;
    object-fit: contain;
}

/* Liste du flux MVC */
.flow-list {
    padding-left: 1.5rem;
    margin: 1.5rem 0;
}

.flow-list li {
    margin-bottom: 0.75rem;
    line-height: 1.6;
    padding-left: 0.5rem;
}

/* Grille des avantages */
.advantages-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
}

.advantage-card {
    padding: 1.5rem;
    background: white;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
    transition: all 0.3s ease;
}

.advantage-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 5px 15px rgba(106, 48, 147, 0.1);
}

.advantage-card h4 {
    margin-bottom: 0.75rem;
    font-size: 1.1rem;
}

.advantage-card p {
    color: #666;
    margin: 0;
    line-height: 1.5;
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

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe */
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

    .schema-caption {
        padding: 1rem;
    }

    .mini-schema .schema-image-wrapper {
        max-height: 150px;
    }

    .mini-schema .schema-image {
        max-height: 150px;
    }

    .large-schema .schema-image-wrapper {
        max-height: 300px;
    }

    .large-schema .schema-image {
        max-height: 300px;
    }

    .advantages-grid {
        grid-template-columns: 1fr;
        gap: 1rem;
    }

    .advantage-card {
        padding: 1.25rem;
    }
}

/* POUR LES TRÈS PETITS ÉCRANS */
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

    .mini-schema .schema-image-wrapper {
        max-height: 120px;
    }

    .mini-schema .schema-image {
        max-height: 120px;
    }

    .large-schema .schema-image-wrapper {
        max-height: 200px;
    }

    .large-schema .schema-image {
        max-height: 200px;
    }

    .schema-caption {
        padding: 0.75rem;
    }

    .schema-caption h3 {
        font-size: 1.1rem;
    }
}

/* POUR LES TRÈS GRANDS ÉCRANS */
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
</style>