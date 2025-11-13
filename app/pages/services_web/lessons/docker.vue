<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Docker et son Utilité</h1>
                <p class="lesson-meta text-white">Conteneurisation et déploiement d'applications</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Docker</h2>
                <p class="textExemple">
                    Docker est une plateforme open-source qui permet de créer, déployer et exécuter des applications
                    dans des conteneurs.
                    Les conteneurs permettent d'empaqueter une application avec toutes ses dépendances dans une unité
                    standardisée,
                    garantissant qu'elle fonctionne de manière cohérente quel que soit l'environnement.
                </p>
                <div class="code-example">
                    <pre><code># Exemple de commande Docker simple
<span class="keyword">docker</span> <span class="function">run</span> <span class="variable">-d</span> <span class="variable">-p</span> <span class="number">80</span>:<span class="number">80</span> <span class="variable">nginx</span></code></pre>
                </div>
            </section>

            <!-- Pourquoi Docker ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser Docker ?</h2>
                <div class="textExemple">
                    <h3 class="text-purple">Avantages principaux :</h3>
                    <ul>
                        <li><strong>Portabilité :</strong> Une application Dockerisée fonctionne de la même manière sur
                            tout système</li>
                        <li><strong>Isolation :</strong> Chaque conteneur s'exécute de manière isolée</li>
                        <li><strong>Efficacité :</strong> Meilleure utilisation des ressources que les machines
                            virtuelles</li>
                        <li><strong>Scalabilité :</strong> Facilite le déploiement et la mise à l'échelle</li>
                        <li><strong>Réutilisabilité :</strong> Les images peuvent être partagées et réutilisées</li>
                    </ul>
                </div>
            </section>

            <!-- Concepts fondamentaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Images Docker</h3>
                    <p>Une image est un modèle en lecture seule qui contient les instructions pour créer un conteneur.
                    </p>

                    <div class="code-example">
                        <pre><code># Exemple de Dockerfile
<span class="keyword">FROM</span> <span class="variable">node</span>:<span class="number">18</span>-alpine
<span class="keyword">WORKDIR</span> <span class="variable">/app</span>
<span class="keyword">COPY</span> <span class="variable">package*.json .</span>/
<span class="keyword">RUN</span> <span class="variable">npm</span> <span class="function">install</span>
<span class="keyword">COPY</span> <span class="variable">. .</span>
<span class="keyword">EXPOSE</span> <span class="number">3000</span>
<span class="keyword">CMD</span> [<span class="string">"npm"</span>, <span class="string">"start"</span>]</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conteneurs Docker</h3>
                    <p>Un conteneur est une instance exécutable d'une image.</p>

                    <div class="code-comparison">
                        <div>
                            <h4>Création d'un conteneur</h4>
                            <pre><code><span class="keyword">docker</span> <span class="function">create</span> <span class="variable">--name</span> <span class="variable">mon-conteneur</span> <span class="variable">nginx</span></code></pre>
                        </div>
                        <div>
                            <h4>Démarrage d'un conteneur</h4>
                            <pre><code><span class="keyword">docker</span> <span class="function">start</span> <span class="variable">mon-conteneur</span></code></pre>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Docker Compose -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Docker Compose</h2>
                <p class="textExemple">
                    Docker Compose permet de définir et d'exécuter des applications multi-conteneurs.
                    Il utilise un fichier YAML pour configurer les services de l'application.
                </p>

                <div class="code-example">
                    <pre><code><span class="comment"># docker-compose.yml</span>
<span class="keyword">version</span>: <span class="string">'3.8'</span>
<span class="keyword">services</span>:
  <span class="variable">web</span>:
    <span class="keyword">build</span>: <span class="variable">.</span>
    <span class="keyword">ports</span>:
      - <span class="string">"3000:3000"</span>
    <span class="keyword">depends_on</span>:
      - <span class="variable">db</span>
  
  <span class="variable">db</span>:
    <span class="keyword">image</span>: <span class="variable">postgres</span>:<span class="number">13</span>
    <span class="keyword">environment</span>:
      <span class="variable">POSTGRES_PASSWORD</span>: <span class="string">"example"</span></code></pre>
                </div>
            </section>

            <!-- Cas d'utilisation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Cas d'utilisation courants</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Environnement de développement</h3>
                    <p>Docker permet de standardiser les environnements de développement entre les membres d'une équipe.
                    </p>

                    <h3 class="text-purple">CI/CD (Intégration Continue/Déploiement Continu)</h3>
                    <p>Les conteneurs Docker sont parfaits pour les pipelines de déploiement automatisés.</p>

                    <h3 class="text-purple">Microservices</h3>
                    <p>Chaque microservice peut s'exécuter dans son propre conteneur, facilitant le déploiement et la
                        scalabilité.</p>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Créer votre premier conteneur</h3>
                    <p>Créez un conteneur Nginx et accédez-y via votre navigateur.</p>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <h4>Étapes :</h4>
                            <ol>
                                <li>Lancez un conteneur Nginx :
                                    <pre><code><span class="keyword">docker</span> <span class="function">run</span> <span class="variable">-d</span> <span class="variable">--name</span> <span class="variable">mon-nginx</span> <span class="variable">-p</span> <span class="number">8080</span>:<span class="number">80</span> <span class="variable">nginx</span></code></pre>
                                </li>
                                <li>Ouvrez votre navigateur et allez sur <code>http://localhost:8080</code></li>
                                <li>Vous devriez voir la page d'accueil de Nginx</li>
                                <li>Pour arrêter le conteneur :
                                    <pre><code><span class="keyword">docker</span> <span class="function">stop</span> <span class="variable">mon-nginx</span></code></pre>
                                </li>
                            </ol>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Commandes utiles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Commandes Docker essentielles</h2>

                <div class="code-comparison">
                    <div>
                        <h4>Gestion des conteneurs</h4>
                        <pre><code><span class="comment"># Lister les conteneurs en cours d'exécution</span>
<span class="keyword">docker</span> <span class="function">ps</span>

<span class="comment"># Lister tous les conteneurs</span>
<span class="keyword">docker</span> <span class="function">ps</span> <span class="variable">-a</span>

<span class="comment"># Arrêter un conteneur</span>
<span class="keyword">docker</span> <span class="function">stop</span> <span class="variable">&lt;container_id&gt;</span>

<span class="comment"># Supprimer un conteneur</span>
<span class="keyword">docker</span> <span class="function">rm</span> <span class="variable">&lt;container_id&gt;</span></code></pre>
                    </div>
                    <div>
                        <h4>Gestion des images</h4>
                        <pre><code><span class="comment"># Lister les images</span>
<span class="keyword">docker</span> <span class="function">images</span>

<span class="comment"># Construire une image depuis un Dockerfile</span>
<span class="keyword">docker</span> <span class="function">build</span> <span class="variable">-t</span> <span class="variable">mon-image</span> <span class="variable">.</span>

<span class="comment"># Supprimer une image</span>
<span class="keyword">docker</span> <span class="function">rmi</span> <span class="variable">&lt;image_id&gt;</span>

<span class="comment"># Télécharger une image depuis Docker Hub</span>
<span class="keyword">docker</span> <span class="function">pull</span> <span class="variable">nginx</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Docker a révolutionné la façon dont nous développons, déployons et exécutons des applications.
                    En fournissant une abstraction au niveau du système d'exploitation, il permet une portabilité sans
                    précédent
                    et une gestion efficace des dépendances. Que vous soyez développeur, administrateur système ou
                    DevOps,
                    maîtriser Docker est devenu une compétence essentielle dans le paysage technologique actuel.
                </p>
            </section>
        </div>
    </div>
</template>

<script>

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