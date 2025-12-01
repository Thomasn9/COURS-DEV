<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- HEADER -->
            <header class="lesson-header">
                <h1>Les blocs sémantiques Twig en Symfony</h1>
                <p class="lesson-meta">Maîtriser l'héritage, la surcharge et la structuration avancée des templates Twig
                </p>
            </header>

            <!-- SECTION : Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">1. Qu'est‑ce qu'un bloc Twig ?</h2>
                <p>
                    Les <strong>blocs Twig</strong> sont des sections nommées dans un template, destinées à être
                    <strong>surchargées</strong> dans des templates enfants.
                    Ils permettent de créer un système d’héritage clair et puissant dans Symfony.
                </p>
                <p>
                    Ce système offre deux avantages majeurs :
                </p>
                <ul>
                    <li>✔️ Réutilisation propre et efficace du HTML,</li>
                    <li>✔️ Structure claire d'un layout principal avec des zones modifiables.</li>
                </ul>
            </section>

            <!-- SECTION : Définir un bloc -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">2. Définir un bloc Twig</h2>
                <p>Un bloc se définit avec les balises <code>{% block nom %}</code> et <code>{% endblock %}</code>.</p>

                <div class="code-example">
                    <pre v-pre><code>{% block content %}
    <h1>Bienvenue</h1>
    <p>Ceci est un bloc de contenu.</p>
{% endblock %}</code></pre>
                </div>

                <p>
                    Le nom du bloc (<code>content</code> ici) sera utilisé lors de la surcharge dans un template enfant.
                </p>
            </section>

            <!-- SECTION : Héritage -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">3. Hériter d'un template dans Symfony</h2>
                <p>
                    Pour exploiter les blocs, un template doit d’abord <strong>hériter</strong> d’un layout parent grâce
                    à :
                </p>

                <div class="code-example">
                    <pre v-pre><code>{% extends 'base.html.twig' %}</code></pre>
                </div>

                <p>Ensuite, on peut surcharger les blocs définis dans le layout parent :</p>

                <div class="code-example">
                    <pre v-pre><code>{% extends 'base.html.twig' %}

{% block title %}Accueil{% endblock %}

{% block content %}
    <p>Contenu de la page d'accueil.</p>
{% endblock %}</code></pre>
                </div>
            </section>

            <!-- SECTION : parent() -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">4. Appeler le contenu parent avec <code>parent()</code></h2>
                <p>
                    Lorsque vous surchargez un bloc, vous pouvez inclure son contenu original via la fonction
                    <code>parent()</code>.
                </p>

                <div class="code-example">
                    <pre v-pre><code>{% block sidebar %}
    {{ parent() }}
    <p>Élément ajouté dans le template enfant.</p>
{% endblock %}</code></pre>
                </div>

                <p>
                    Très utile pour garder le layout global tout en ajoutant des éléments spécifiques !
                </p>
            </section>

            <!-- SECTION : blocs imbriqués -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">5. Blocs imbriqués et organisation avancée</h2>
                <p>Il est possible de créer plusieurs sous‑blocs dans un même template afin de structurer finement vos
                    pages.</p>

                <div class="code-example">
                    <pre v-pre><code>{% block page %}
    <h1>Titre</h1>

    {% block page_content %}
        <p>Contenu interne du bloc page_content.</p>
    {% endblock %}
{% endblock %}</code></pre>
                </div>

                <p>
                    Les templates enfants peuvent alors surcharger uniquement certains sous‑blocs si nécessaire.
                </p>
            </section>

            <!-- SECTION : Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">6. Bonnes pratiques essentielles</h2>
                <ul>
                    <li>🟣 Utiliser des noms de blocs explicites : <code>content</code>, <code>sidebar</code>,
                        <code>footer</code>…</li>
                    <li>🟣 Centraliser vos layouts dans un dossier <code>templates/layout/</code>.</li>
                    <li>🟣 Ne surchargez que les blocs nécessaires.</li>
                    <li>🟣 Gardez un layout HTML minimal et clair.</li>
                </ul>
            </section>

            <!-- SECTION : EXERCICES -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">7. Exercice pratique</h2>
                <p class="textExemple">Créer un template enfant basé sur <code>layout.html.twig</code> et y ajouter du
                    contenu personnalisé.</p>

                <details class="exercise">
                    <summary>Afficher la solution</summary>
                    <div class="solution-content">
                        <h4>Solution :</h4>
                        <pre v-pre><code>{% extends 'layout.html.twig' %}

{% block body %}
    <h2>Page personnalisée</h2>
    <p>Voici mon contenu ajouté.</p>
{% endblock %}</code></pre>
                    </div>
                </details>
            </section>

        </div>
    </div>
</template>


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
    /* Permet le retour à la ligne */
    word-wrap: break-word;
    /* Casse les mots longs */
    word-break: break-word;
    /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (for, while, if, function, etc.) */
.variable {
    color: #9cdcfe !important;
}

/* Variables et noms de fonctions */
.string {
    color: #ce9178 !important;
}

/* Chaînes de caractères */
.comment {
    color: #6a9955 !important;
}

/* Commentaires */
.function {
    color: #dcdcaa !important;
}

/* Noms de fonctions */
.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs (+, -, =, =>, etc.) */
.constant {
    color: #4fc1ff !important;
}

/* Constantes */
.number {
    color: #b5cea8 !important;
}

/* Nombres */
.class-name {
    color: #4ec9b0 !important;
}

/* Noms de classes */

/* Exercices et solutions */
.exercise {
    margin: 2rem 0;
}

.solution {
    margin: 1rem 0;
}

.solution-content {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #8B5FBF;
}

.solution-content h4 {
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
}

details summary {
    cursor: pointer;
    outline: none;
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
