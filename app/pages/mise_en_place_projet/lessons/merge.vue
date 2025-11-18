<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Merges de branches Git</h1>
                <p class="lesson-meta text-white">Apprenez à fusionner vos branches efficacement avec Git et GitHub</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>Dans ce tutoriel, nous allons apprendre à fusionner des branches Git en suivant un workflow complet,
                    de la création d'une branche de fonctionnalité à sa fusion dans la branche principale via une pull
                    request sur GitHub.</p>
                <p>Ce processus est essentiel pour le développement collaboratif et la gestion de versions dans vos
                    projets.</p>
            </div>

            <!-- Étape 1 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 1 : Création de la branche feature/createLessons</h3>
                <p>La première étape consiste à créer une nouvelle branche pour développer notre fonctionnalité. Cette
                    pratique permet d'isoler les changements et de travailler sans affecter la branche principale.</p>

                <div class="code-example">
                    <h4 class="text-purple">Commande Git :</h4>
                    <pre><code class="language-bash"><span class="function">git</span> <span class="variable">checkout</span> <span class="operator">-b</span> <span class="variable">feature</span><span class="operator">/</span><span class="variable">createLessons</span></code></pre>
                </div>

                <p class="textExemple">Cette commande crée une nouvelle branche nommée
                    <code>feature/createLessons</code> et bascule automatiquement dessus.</p>
            </div>

            <!-- Étape 2 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 2 : Changement de branche</h3>
                <p>Si vous avez déjà créé la branche précédemment, vous pouvez simplement basculer dessus avec la
                    commande suivante :</p>

                <div class="code-example">
                    <h4 class="text-purple">Commande Git :</h4>
                    <pre><code class="language-bash"><span class="function">git</span> <span class="variable">checkout</span> <span class="variable">feature</span><span class="operator">/</span><span class="variable">createLessons</span></code></pre>
                </div>

                <p class="textExemple">Vous devriez voir un message confirmant que vous êtes maintenant sur la branche
                    <code>feature/createLessons</code>.</p>
            </div>

            <!-- Étape 3 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 3 : Appliquer les changements via git add + commit</h3>
                <p>Une fois vos modifications effectuées (création de fichiers, modifications, etc.), vous devez les
                    ajouter à l'index et les commiter.</p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Ajouter tous les fichiers modifiés :</h4>
                        <pre><code class="language-bash"><span class="function">git</span> <span class="variable">add</span> <span class="operator">*</span></code></pre>
                    </div>
                    <div>
                        <h4 class="text-purple">Créer un commit avec un message descriptif :</h4>
                        <pre><code class="language-bash"><span class="function">git</span> <span class="variable">commit</span> <span class="operator">-m</span> <span class="string">"Ajout du début de la leçon sur les merges de branches"</span></code></pre>
                    </div>
                </div>

                <p class="textExemple">Le message de commit doit être clair et descriptif pour faciliter la
                    compréhension des changements apportés.</p>
            </div>

            <!-- Étape 4 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 4 : Faire un pull request sur GitHub</h3>
                <p>Maintenant que vos changements sont commités, vous devez pousser votre branche vers le dépôt distant
                    et créer une pull request.</p>

                <div class="code-example">
                    <h4 class="text-purple">Pousser la branche vers le dépôt distant :</h4>
                    <pre><code class="language-bash"><span class="function">git</span> <span class="variable">push</span> <span class="variable">origin</span> <span class="variable">feature</span><span class="operator">/</span><span class="variable">createLessons</span></code></pre>
                </div>

                <p>Ensuite, rendez-vous sur GitHub :</p>
                <ol>
                    <li>Allez dans votre dépôt sur GitHub</li>
                    <li>Cliquez sur l'onglet "Pull requests"</li>
                    <li>Cliquez sur "New pull request"</li>
                    <li>Sélectionnez <code>main</code> comme base et <code>feature/createLessons</code> comme branche à
                        comparer</li>
                    <li>Rédigez un titre et une description clairs expliquant les changements et le but de cette branche
                    </li>
                    <li>Cliquez sur "Create pull request"</li>
                </ol>

                <p class="textExemple">Dans la description, expliquez clairement ce que cette branche apporte au projet
                    et pourquoi elle devrait être fusionnée.</p>
            </div>

            <!-- Étape 5 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 5 : Valider la pull request</h3>
                <p>Une fois la pull request créée, elle peut être examinée par d'autres membres de l'équipe. Si tout est
                    correct, vous pouvez la fusionner.</p>

                <p>Sur la page de la pull request sur GitHub :</p>
                <ol>
                    <li>Vérifiez que tous les tests passent (s'il y en a)</li>
                    <li>Lisez les commentaires éventuels des reviewers</li>
                    <li>Cliquez sur "Merge pull request"</li>
                    <li>Confirmez la fusion en cliquant sur "Confirm merge"</li>
                </ol>

                <p class="textExemple">GitHub vous proposera généralement de supprimer la branche après la fusion, ce
                    qui est recommandé pour garder le dépôt propre.</p>
            </div>

            <!-- Étape 6 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 6 : Revenir sur la branche main</h3>
                <p>Maintenant que la fusion est effectuée sur GitHub, vous devez retourner sur votre branche principale
                    locale.</p>

                <div class="code-example">
                    <h4 class="text-purple">Commande Git :</h4>
                    <pre><code class="language-bash"><span class="function">git</span> <span class="variable">checkout</span> <span class="variable">main</span></code></pre>
                </div>

                <p class="textExemple">Cette commande vous ramène sur la branche principale de votre dépôt local.</p>
            </div>

            <!-- Étape 7 -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Étape 7 : Effectuer un pull depuis la branche main</h3>
                <p>Pour récupérer les changements fusionnés depuis le dépôt distant, vous devez effectuer un pull.</p>

                <div class="code-example">
                    <h4 class="text-purple">Commande Git :</h4>
                    <pre><code class="language-bash"><span class="function">git</span> <span class="variable">pull</span> <span class="variable">origin</span> <span class="variable">main</span></code></pre>
                </div>

                <p class="textExemple">Cette commande met à jour votre branche principale locale avec tous les
                    changements fusionnés depuis GitHub.</p>
            </div>

            <!-- Conclusion -->
            <div class="lesson-section bg-light-purple border-purple">
                <h3 class="text-purple">Conclusion</h3>
                <p>Félicitations ! Vous avez maintenant complété le processus complet de fusion de branches avec Git et
                    GitHub. Les ajouts de la branche <code>feature/createLessons</code> sont désormais présents sur
                    votre branche principale locale.</p>

                <p>Ce workflow est essentiel pour :</p>
                <ul>
                    <li>Développer des fonctionnalités de manière isolée</li>
                    <li>Faciliter la revue de code</li>
                    <li>Maintenir une histoire de projet propre et compréhensible</li>
                    <li>Collaborer efficacement avec d'autres développeurs</li>
                </ul>

                <!-- Exercice pratique -->
                <div class="exercise">
                    <h4 class="text-purple">Exercice pratique</h4>
                    <p>Pour consolider vos connaissances, essayez de reproduire ce processus avec une nouvelle fonctionnalité :</p>
                    
                    <ol>
                        <li>Créez une branche <code>feature/add-exercises</code></li>
                        <li>Ajoutez un fichier d'exercices à votre projet</li>
                        <li>Commitez vos changements</li>
                        <li>Créez une pull request sur GitHub</li>
                        <li>Fusionnez la pull request</li>
                        <li>Mettez à jour votre branche principale locale</li>
                    </ol>
                </div>

                <details class="solution">
                    <summary class="btn-purple">Voir la solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Commandes Git pour l'exercice :</h4>
                        <pre><code class="language-bash"><span class="comment"># Créer et basculer sur la nouvelle branche</span>
<span class="function">git</span> <span class="variable">checkout</span> <span class="operator">-b</span> <span class="variable">feature</span><span class="operator">/</span><span class="variable">add</span><span class="operator">-</span><span class="variable">exercises</span>

<span class="comment"># Créer un fichier d'exercices (par exemple exercises.md)</span>
<span class="function">echo</span> <span class="string">"# Exercices pratiques"</span> <span class="operator">></span> <span class="variable">exercises</span><span class="operator">.</span><span class="variable">md</span>

<span class="comment"># Ajouter et commiter les changements</span>
<span class="function">git</span> <span class="variable">add</span> <span class="variable">exercises</span><span class="operator">.</span><span class="variable">md</span>
<span class="function">git</span> <span class="variable">commit</span> <span class="operator">-m</span> <span class="string">"Ajout d'un fichier d'exercices pratiques"</span>

<span class="comment"># Pousser la branche vers GitHub</span>
<span class="function">git</span> <span class="variable">push</span> <span class="variable">origin</span> <span class="variable">feature</span><span class="operator">/</span><span class="variable">add</span><span class="operator">-</span><span class="variable">exercises</span>

<span class="comment"># Ensuite, sur GitHub, créer une pull request et la fusionner</span>

<span class="comment"># Revenir sur main et mettre à jour</span>
<span class="function">git</span> <span class="variable">checkout</span> <span class="variable">main</span>
<span class="function">git</span> <span class="variable">pull</span> <span class="variable">origin</span> <span class="variable">main</span></code></pre>
                    </div>
                </details>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'GitMergeLesson',
    head() {
        return {
            title: 'Merges de branches Git - Leçons',
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Apprenez à fusionner des branches Git efficacement avec ce tutoriel complet.'
                }
            ]
        }
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