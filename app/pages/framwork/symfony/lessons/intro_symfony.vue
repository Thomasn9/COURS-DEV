<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <div class="lesson-header">
        <h1 class="text-white" v-pre>Introduction à Symfony</h1>
        <p class="lesson-meta text-white" v-pre>Découvrez le framework PHP qui révolutionne le développement web</p>
      </div>

      <!-- Qu'est-ce que Symfony -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Qu'est-ce que Symfony ?</h2>
        <p class="textExemple" v-pre>
          Symfony est un framework PHP open-source complet qui facilite et accélère 
          le développement d'applications web. Créé en 2005, il est devenu l'un des frameworks PHP 
          les plus populaires et les plus utilisés dans le monde.
        </p>
        
        <div class="textExemple" v-pre>
          <strong>Symfony en chiffres :</strong> Plus de 600 000 développeurs, utilisé par 75% des sites PHP français,
          plus de 3 000 contributeurs, une communauté mondiale active et des mises à jour régulières avec du support long terme.
        </div>
      </div>

      <!-- Philosophie de Symfony -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>La Philosophie Symfony</h2>
        <p class="textExemple" v-pre>
          Symfony suit des principes fondamentaux qui en font un framework robuste et maintenable :
        </p>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Modularité</h4>
            <p v-pre>Composants réutilisables, chaque fonctionnalité est indépendante, vous utilisez seulement ce dont vous avez besoin.</p>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Configuration sobre</h4>
            <p v-pre>Convention over Configuration, moins de configuration, plus de codage, paramètres par défaut intelligents.</p>
          </div>
        </div>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Extensibilité</h4>
            <p v-pre>Architecture flexible, personnalisation avancée, Bundle system pour étendre les fonctionnalités.</p>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Standards ouverts</h4>
            <p v-pre>Respect des standards PHP, PSR (PHP Standards Recommendations), interopérabilité avec d'autres librairies.</p>
          </div>
        </div>
      </div>

      <!-- Architecture MVC -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Architecture MVC</h2>
        <p class="textExemple" v-pre>
          Symfony suit le pattern Modèle-Vue-Contrôleur (MVC) qui sépare clairement 
          la logique métier, l'interface utilisateur et la gestion des requêtes.
        </p>
        
        <div class="textExemple" v-pre>
          <strong>Structure MVC de Symfony :</strong> Le dossier src contient les contrôleurs, le dossier Entity contient les modèles (entités),
          et le dossier templates contient les vues (templates Twig).
        </div>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Contrôleur</h4>
            <p v-pre>Les contrôleurs gèrent les requêtes HTTP et retournent des réponses. Ils contiennent la logique métier de l'application.</p>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Vue (Twig)</h4>
            <p v-pre>Les vues utilisent le moteur de template Twig pour afficher l'interface utilisateur de manière séparée de la logique.</p>
          </div>
        </div>
      </div>

      <!-- Composants Symfony -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Les Composants Symfony</h2>
        <p class="textExemple" v-pre>
          Symfony est construit autour de composants découplés et réutilisables. 
          Vous pouvez utiliser ces composants indépendamment dans n'importe quel projet PHP.
        </p>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Composants principaux</h4>
            <ul v-pre>
              <li>HttpFoundation - Gestion des requêtes/réponses</li>
              <li>Routing - Système de routage URL</li>
              <li>Form - Création et validation de formulaires</li>
              <li>Validator - Validation des données</li>
              <li>Security - Système d'authentification</li>
              <li>Doctrine - ORM pour les bases de données</li>
              <li>Console - Interface en ligne de commande</li>
              <li>Twig - Moteur de templates</li>
            </ul>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Utilisation isolée des composants</h4>
            <p v-pre>Chaque composant peut être utilisé indépendamment via Composer. Par exemple, le composant Validator peut être utilisé seul pour valider des données dans n'importe quel projet PHP.</p>
          </div>
        </div>
      </div>

      <!-- Avantages de Symfony -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Pourquoi Choisir Symfony ?</h2>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Pour les entreprises</h4>
            <ul v-pre>
              <li>Maintenance à long terme</li>
              <li>Documentation exhaustive</li>
              <li>Support professionnel disponible</li>
              <li>Écosystème mature et stable</li>
              <li>Sécurité renforcée</li>
              <li>Scalabilité prouvée</li>
            </ul>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Pour les développeurs</h4>
            <ul v-pre>
              <li>Courbe d'apprentissage progressive</li>
              <li>Outils de développement puissants</li>
              <li>Debugging facilité (Profiler)</li>
              <li>Génération de code (MakerBundle)</li>
              <li>Tests automatisés intégrés</li>
              <li>Communauté active et aide</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Cas d'utilisation -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Cas d'Utilisation Typiques</h2>
        <p class="textExemple" v-pre>
          Symfony excelle dans divers types de projets, des simples sites web aux applications complexes.
        </p>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Sites web classiques</h4>
            <ul v-pre>
              <li>Sites corporate</li>
              <li>Portails d'information</li>
              <li>Sites e-commerce</li>
              <li>Plateformes de contenu</li>
              <li>Applications SaaS</li>
            </ul>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Applications complexes</h4>
            <ul v-pre>
              <li>APIs REST/GraphQL</li>
              <li>Applications mobiles backend</li>
              <li>Systèmes de gestion</li>
              <li>Plateformes B2B</li>
              <li>Microservices</li>
            </ul>
          </div>
        </div>
        
        <div class="textExemple" v-pre>
          <strong>Entreprises qui utilisent Symfony :</strong> BlaBlaCar, Spotify, Dailymotion, OpenClassrooms, et des milliers d'autres entreprises à travers le monde.
        </div>
      </div>

      <!-- Symfony vs Autres Solutions -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Symfony vs Autres Solutions</h2>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Comparaison avec Laravel</h4>
            <p v-pre>Symfony offre plus de flexibilité et une architecture modulaire, idéal pour les projets complexes. Laravel est plus simple à débuter avec un écosystème intégré, idéal pour les MVP rapides.</p>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Comparaison avec un framework maison</h4>
            <p v-pre>Symfony apporte une sécurité éprouvée, une maintenance garantie et une communauté active. Un framework maison peut être sur-mesure mais présente des risques de sécurité et une maintenance coûteuse.</p>
          </div>
        </div>
      </div>

      <!-- Écosystème Symfony -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>L'Écosystème Symfony</h2>
        <p class="textExemple" v-pre>
          Symfony ne se limite pas au framework lui-même, c'est tout un écosystème d'outils et de services.
        </p>
        
        <div class="code-comparison">
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Outils de développement</h4>
            <ul v-pre>
              <li>Symfony CLI - Interface en ligne de commande</li>
              <li>Webpack Encore - Gestion des assets</li>
              <li>MakerBundle - Génération de code</li>
              <li>Profiler - Debugging en temps réel</li>
              <li>Debug Bundle - Outils de développement</li>
            </ul>
          </div>
          
          <div class="textExemple">
            <h4 class="text-purple" v-pre>Bundles populaires</h4>
            <ul v-pre>
              <li>EasyAdmin - Backoffice automatique</li>
              <li>API Platform - Création d'API</li>
              <li>SonataAdmin - Administration avancée</li>
              <li>KnpPaginator - Système de pagination</li>
              <li>VichUploader - Gestion des uploads</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Exercice pratique -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Exercice de Compréhension</h2>
        <div class="exercise">
          <p class="textExemple" v-pre>
            <strong>Objectif :</strong> Identifier les avantages de Symfony pour différents scénarios de projet.
          </p>
          <ol class="textExemple" v-pre>
            <li>Pour chaque scénario ci-dessous, expliquez pourquoi Symfony serait un bon choix</li>
            <li>Listez les composants Symfony qui seraient les plus utiles</li>
          </ol>
          
          <div class="textExemple" v-pre>
            <strong>Scénarios :</strong>
            <ul>
              <li>Une startup veut créer un MVP d'application de réservation</li>
              <li>Une grande entreprise a besoin de migrer un legacy complexe</li>
              <li>Un développeur freelance crée un site vitrine pour un client</li>
              <li>Une équipe développe une API pour une application mobile</li>
            </ul>
          </div>
        </div>
        
        <details class="solution">
          <summary class="btn-purple btn-hover" v-pre>Voir les réponses suggérées</summary>
          <div class="solution-content">
            <h4 class="text-purple" v-pre>Réponses :</h4>
            
            <div class="textExemple">
              <h5 v-pre>MVP Startup</h5>
              <p v-pre>Symfony avec MakerBundle pour prototypage rapide, composants Form et Validator pour les données, Security pour l'authentification. Avantage : Évolutivité quand le projet grandit.</p>
            </div>
            
            <div class="textExemple">
              <h5 v-pre>Migration Legacy</h5>
              <p v-pre>Utilisation progressive des composants Symfony, Doctrine pour l'abstraction base de données, Console pour les scripts de migration. Avantage : Stabilité et maintenabilité.</p>
            </div>
            
            <div class="textExemple">
              <h5 v-pre>Site Vitrine</h5>
              <p v-pre>Symfony avec Twig pour les templates, Routing pour le SEO, Cache pour les performances. Avantage : Facilité de maintenance future.</p>
            </div>
            
            <div class="textExemple">
              <h5 v-pre>API Mobile</h5>
              <p v-pre>API Platform ou composant Serializer, Security JWT pour l'authentification, Validator pour la data validation. Avantage : Standards REST, documentation auto.</p>
            </div>
          </div>
        </details>
      </div>

      <!-- Conclusion -->
      <div class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple" v-pre>Conclusion</h2>
        <p class="textExemple" v-pre>
          Symfony est bien plus qu'un simple framework PHP. C'est un écosystème complet 
          qui offre aux développeurs les outils nécessaires pour créer des applications web robustes, 
          maintenables et évolutives.
        </p>
        
        <p class="textExemple" v-pre>
          Que vous soyez débutant ou expert, Symfony s'adapte à vos besoins grâce à sa modularité 
          et sa flexibilité. Son adoption massive par les entreprises et sa communauté active en font 
          un choix sûr pour vos projets actuels et futurs.
        </p>
        
        <h3 class="text-purple" v-pre>Prochaine étape :</h3>
        <p class="textExemple" v-pre>
          Maintenant que vous comprenez l'utilité globale de Symfony, passez à la leçon suivante 
          sur l'installation et la création de votre premier projet !
        </p>
        
        <div class="textExemple">
          <a href="/lessons/symfony-installation" class="btn-purple btn-hover" v-pre>Passer à l'installation</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SymfonyIntroductionLesson',
  head() {
    return {
      title: 'Introduction à Symfony - Leçons Symfony',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Découvrez Symfony : le framework PHP modulaire pour applications web professionnelles'
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
.code-example, .code-block {
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
}

/* POUR LES TRÈS PETITS ÉCRANS */
@media (max-width: 480px) {
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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>