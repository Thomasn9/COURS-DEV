<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Unsplash - La plateforme de photos libres de droits</h1>
                <p class="lesson-meta text-white">Leçon sur l'utilisation des ressources visuelles gratuites</p>
            </header>

            <!-- Section d'introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'Unsplash ?</h2>
                <p class="textExemple">
                    Unsplash est une plateforme en ligne qui propose une vaste collection de photographies
                    de haute qualité, entièrement gratuites et libres de droits. Lancée en 2013, elle est
                    devenue une référence pour les créateurs, développeurs, designers et marketeurs
                    cherchant des images professionnelles sans contraintes légales.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Caractéristiques principales :</h3>
                    <ul>
                        <li><strong>Gratuité totale</strong> - Pas de frais d'utilisation</li>
                        <li><strong>Licence permissive</strong> - Utilisation commerciale et personnelle autorisée</li>
                        <li><strong>Haute qualité</strong> - Images professionnelles en haute résolution</li>
                        <li><strong>API développeur</strong> - Intégration facile dans vos applications</li>
                        <li><strong>Communauté active</strong> - Des milliers de photographes contributeurs</li>
                    </ul>
                </div>
            </section>

            <!-- Section utilité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilité d'Unsplash</h2>

                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Pour les développeurs</h3>
                        <ul>
                            <li>Images de placeholder pour les prototypes</li>
                            <li>Illustrations pour sites web et applications</li>
                            <li>Intégration via API pour générer du contenu dynamique</li>
                            <li>Ressources pour les interfaces utilisateur</li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-purple">Pour les designers</h3>
                        <ul>
                            <li>Arrière-plans pour maquettes</li>
                            <li>Éléments visuels pour présentations</li>
                            <li>Inspiration créative</li>
                            <li>Ressources pour projets clients</li>
                        </ul>
                    </div>
                </div>

                <p class="textExemple">
                    Unsplash élimine les barrières légales et financières traditionnellement associées
                    à l'utilisation d'images professionnelles, permettant à chacun de créer des projets
                    visuellement attrayants sans compromis sur la qualité.
                </p>
            </section>

            <!-- Section utilisation technique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation technique</h2>

                <h3 class="text-purple">Intégration via API</h3>
                <p class="textExemple">
                    Unsplash propose une API RESTful permettant de rechercher, récupérer et afficher
                    des images directement dans vos applications. Voici un exemple d'intégration :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Exemple d'appel API :</h4>
                    <pre><code class="javascript">// Recherche d'images sur Unsplash
async function searchUnsplash(query) {
  const accessKey = 'VOTRE_CLE_API';
  const response = await fetch(
    `https://api.unsplash.com/search/photos?query=${query}&client_id=${accessKey}`
  );
  const data = await response.json();
  return data.results;
}

// Utilisation
const natureImages = await searchUnsplash('nature');</code></pre>
                </div>

                <h3 class="text-purple">Intégration directe dans le HTML</h3>
                <p class="textExemple">
                    Vous pouvez également utiliser directement les images d'Unsplash via leur URL :
                </p>

                <div class="code-example">
                    <pre><code class="html">&lt;img 
  src="https://images.unsplash.com/photo-1541963463532-d68292c34b19?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" 
  alt="Livre sur une table" 
  width="800" 
  height="600"&gt;</code></pre>
                </div>
            </section>

            <!-- Section bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques d'utilisation</h2>

                <div class="code-example">
                    <h3 class="text-purple">Respect des conditions d'utilisation :</h3>
                    <ul>
                        <li>✅ Attribution non obligatoire mais appréciée</li>
                        <li>✅ Utilisation commerciale autorisée</li>
                        <li>✅ Modification des images permise</li>
                        <li>❌ Revendre les images telles quelles</li>
                        <li>❌ Créer une plateforme concurrente avec leur contenu</li>
                        <li>❌ Utilisation immorale ou illégale</li>
                    </ul>
                </div>

                <p class="textExemple">
                    Bien que l'attribution ne soit pas obligatoire, il est de bonne pratique de créditer
                    les photographes lorsque cela est possible, surtout dans des contextes éducatifs ou
                    lorsque la visibilité du créateur est importante.
                </p>
            </section>


            <!-- Section ressources supplémentaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Ressources supplémentaires</h2>

                <div class="code-example">
                    <h3 class="text-purple">Liens utiles :</h3>
                    <ul>
                        <li>
                            <a href="https://unsplash.com" target="_blank" class="btn-purple btn-hover"
                                style="margin: 0.25rem;">
                                Site officiel Unsplash
                            </a>
                        </li>
                        <li>
                            <a href="https://unsplash.com/developers" target="_blank" class="btn-purple btn-hover"
                                style="margin: 0.25rem;">
                                Documentation API
                            </a>
                        </li>
                        <li>
                            <a href="https://unsplash.com/documentation" target="_blank" class="btn-purple btn-hover"
                                style="margin: 0.25rem;">
                                Guide d'utilisation
                            </a>
                        </li>
                    </ul>
                </div>

                <p class="textExemple">
                    N'hésitez pas à explorer la plateforme et à expérimenter avec différentes intégrations.
                    Unsplash est une ressource incroyablement précieuse pour tout projet nécessitant
                    des visuels de qualité professionnelle.
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