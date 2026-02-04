<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white"> Une Journée Type avec Git</h1>
                <p class="lesson-meta text-white">
                    Apprenez à gérer votre workflow quotidien avec Git
                </p>
            </div>

            <!-- Section d'introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple mb-4">Objectif de la leçon</h2>
                <p class="textExemple">
                    Cette leçon vous guide à travers un scénario réaliste de développement quotidien avec Git.
                    Vous apprendrez les commandes essentielles pour collaborer efficacement sur un projet
                    tout en maintenant un historique propre et organisé.
                </p>
                <div class="mt-4">
                    <strong class="text-purple">Prérequis :</strong>
                    <ul class="mt-2">
                        <li>Git installé sur votre machine</li>
                        <li>Un compte sur une plateforme Git (GitHub, GitLab, etc.)</li>
                        <li>Connaissance basique des commandes terminal</li>
                    </ul>
                </div>
            </div>

            <!-- Section 1 : Démarrer la journée -->
            <div class="lesson-section bg-light-purple border-purple">
                <div class="d-flex align-items-center mb-4">
                    <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3"
                        style="width: 50px; height: 50px;">
                        <span style="font-size: 1.5rem;">1</span>
                    </div>
                    <h2 class="text-purple mb-0">Démarrer la journée de travail</h2>
                </div>

                <p class="textExemple mb-4">
                    Avant de commencer à coder, il est essentiel de synchroniser votre branche avec les dernières
                    modifications.
                    Cette étape garantit que vous travaillez sur une base à jour et évite les conflits futurs.
                </p>

                <div class="code-example">
                    <h4 class="text-purple mb-3">Commandes à exécuter :</h4>
                    <pre><code># 1. Se positionner sur la branche de développement
<span class="keyword">git</span> <span class="variable">checkout</span> dev

# 2. Récupérer les dernières modifications
<span class="keyword">git</span> <span class="variable">pull</span> origin dev

# 3. Créer ou se positionner sur votre branche de travail
<span class="keyword">git</span> <span class="variable">checkout</span> thomas

# 4. Fusionner les dernières modifications de dev dans votre branche
<span class="keyword">git</span> <span class="variable">merge</span> dev</code></pre>
                </div>

                <div class="mt-4 p-3 bg-gradient-primary text-white rounded">
                    <strong>Conseil :</strong> Toujours faire un <code>git pull</code> avant de commencer à
                    travailler pour éviter les conflits.
                </div>
            </div>

            <!-- Section 2 : Travailler -->
            <div class="lesson-section bg-light-purple border-purple">
                <div class="d-flex align-items-center mb-4">
                    <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3"
                        style="width: 50px; height: 50px;">
                        <span style="font-size: 1.5rem;">2</span>
                    </div>
                    <h2 class="text-purple mb-0">Phase de travail</h2>
                </div>

                <p class="textExemple mb-4">
                    Pendant cette phase, vous implémentez vos fonctionnalités ou corrections.
                    Sauvegardez régulièrement votre travail avec des commits clairs et descriptifs.
                </p>

                <div class="code-example">
                    <h4 class="text-purple mb-3">Workflow de travail :</h4>
                    <pre><code># ... faire vos modifications dans votre éditeur de code ...

# 1. Ajouter tous les fichiers modifiés
<span class="keyword">git</span> <span class="variable">add</span> .

# 2. Créer un commit avec un message descriptif
<span class="keyword">git</span> <span class="variable">commit</span> -m <span class="string">"feat: ajout validation formulaire"</span>

# 3. Pousser vos modifications sur le dépôt distant
<span class="keyword">git</span> <span class="variable">push</span> origin thomas</code></pre>
                </div>

                <div class="mt-4">
                    <h4 class="text-purple">Bonnes pratiques pour les messages de commit :</h4>
                    <ul class="mt-2">
                        <li><strong>feat:</strong> pour une nouvelle fonctionnalité</li>
                        <li><strong>fix:</strong> pour une correction de bug</li>
                        <li><strong>docs:</strong> pour des modifications de documentation</li>
                        <li><strong>style:</strong> pour des changements de formatage</li>
                        <li><strong>refactor:</strong> pour du refactoring de code</li>
                    </ul>
                </div>
            </div>

            <!-- Section 3 : Fusionner dans dev -->
            <div class="lesson-section bg-light-purple border-purple">
                <div class="d-flex align-items-center mb-4">
                    <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3"
                        style="width: 50px; height: 50px;">
                        <span style="font-size: 1.5rem;">3</span>
                    </div>
                    <h2 class="text-purple mb-0">Fusionner dans la branche dev</h2>
                </div>

                <p class="textExemple mb-4">
                    Une fois votre fonctionnalité terminée et testée localement, il est temps de l'intégrer
                    dans la branche principale de développement.
                </p>

                <div class="code-example">
                    <h4 class="text-purple mb-3">Processus de fusion :</h4>
                    <pre><code># 1. Revenir sur la branche dev
<span class="keyword">git</span> <span class="variable">checkout</span> dev

# 2. Récupérer les dernières modifications
<span class="keyword">git</span> <span class="variable">pull</span> origin dev

# 3. Fusionner votre branche dans dev
<span class="keyword">git</span> <span class="variable">merge</span> thomas

<span class="comment"># Si conflits :</span>
<span class="comment"># 1. Ouvrez les fichiers en conflit</span>
<span class="comment"># 2. Résolvez manuellement</span>
<span class="comment"># 3. git add .</span>
<span class="comment"># 4. git commit -m "Merge thomas into dev"</span>

# 4. Pousser la fusion sur le dépôt distant
<span class="keyword">git</span> <span class="variable">push</span> origin dev</code></pre>
                </div>
            </div>

            <!-- Section 4 : Préparer la production -->
            <div class="lesson-section bg-light-purple border-purple">
                <div class="d-flex align-items-center mb-4">
                    <div class="bg-gradient-primary text-white rounded-circle d-flex align-items-center justify-content-center me-3"
                        style="width: 50px; height: 50px;">
                        <span style="font-size: 1.5rem;">4</span>
                    </div>
                    <h2 class="text-purple mb-0">Préparer la production</h2>
                </div>

                <p class="textExemple mb-4">
                    Quand la branche dev est stable et testée, on peut préparer une version pour la production.
                    Cette étape est généralement faite par le responsable technique.
                </p>

                <div class="code-example">
                    <h4 class="text-purple mb-3">Mise en production :</h4>
                    <pre><code># 1. Se positionner sur la branche main (ou master)
<span class="keyword">git</span> <span class="variable">checkout</span> main

# 2. Récupérer les dernières modifications
<span class="keyword">git</span> <span class="variable">pull</span> origin main

# 3. Fusionner dev dans main
<span class="keyword">git</span> <span class="variable">merge</span> dev

# 4. Pousser la version de production
<span class="keyword">git</span> <span class="variable">push</span> origin main</code></pre>
                </div>

                <div class="mt-4 p-3 bg-gradient-primary text-white rounded">
                    <strong>Important :</strong> La branche main doit toujours contenir du code stable et prêt pour la
                    production.
                </div>
            </div>

            <!-- Section résumé -->
            <div class="lesson-section bg-gradient-primary text-white">
                <h2 class="mb-4"> Résumé du Workflow</h2>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-white">Workflow complet :</h4>
                        <ol class="mt-3">
                            <li>Mettre à jour depuis dev</li>
                            <li>Travailler sur votre branche</li>
                            <li>Commiter régulièrement</li>
                            <li>Fusionner dans dev après tests</li>
                            <li>Mettre en production quand stable</li>
                        </ol>
                    </div>

                    <div>
                        <h4 class="text-white">Avantages :</h4>
                        <ul class="mt-3">
                            <li>Historique de commits propre</li>
                            <li>Conflits minimisés</li>
                            <li>Code toujours testé avant fusion</li>
                            <li>Séparation claire des environnements</li>
                        </ul>
                    </div>
                </div>

                <div class="mt-4">
                    <h4 class="text-white">Commandes clés à retenir :</h4>
                    <div class="d-flex flex-wrap gap-2 mt-3">
                        <span class="btn-purple btn-hover">git checkout</span>
                        <span class="btn-purple btn-hover">git pull</span>
                        <span class="btn-purple btn-hover">git merge</span>
                        <span class="btn-purple btn-hover">git add .</span>
                        <span class="btn-purple btn-hover">git commit -m</span>
                        <span class="btn-purple btn-hover">git push</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
// Vous pouvez ajouter ici des variables réactives si nécessaire
const pageTitle = "Une Journée Type avec Git";

// Met à jour le titre de la page
useHead({
    title: pageTitle
});
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

/* Styles additionnels pour cette page spécifique */
.mb-0 {
    margin-bottom: 0 !important;
}

.mb-2 {
    margin-bottom: 0.5rem !important;
}

.mb-3 {
    margin-bottom: 1rem !important;
}

.mb-4 {
    margin-bottom: 1.5rem !important;
}

.mt-2 {
    margin-top: 0.5rem !important;
}

.mt-3 {
    margin-top: 1rem !important;
}

.mt-4 {
    margin-top: 1.5rem !important;
}

.me-3 {
    margin-right: 1rem !important;
}

.d-flex {
    display: flex !important;
}

.align-items-center {
    align-items: center !important;
}

.justify-content-center {
    justify-content: center !important;
}

.justify-content-between {
    justify-content: space-between !important;
}

.rounded-circle {
    border-radius: 50% !important;
}

.rounded {
    border-radius: 8px !important;
}

.flex-wrap {
    flex-wrap: wrap !important;
}

.gap-2 {
    gap: 0.5rem !important;
}

.p-3 {
    padding: 1rem !important;
}

/* Style pour les listes dans les sections colorées */
.text-white ul,
.text-white ol {
    color: white;
}

.text-white li {
    margin-bottom: 0.5rem;
}
</style>