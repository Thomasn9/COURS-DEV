<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Créer un projet Spring Boot avec Spring Initializr</h1>
        <div class="lesson-meta text-white">
          Leçon 2 • Configuration projet • Guide pratique étape par étape
        </div>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Introduction à Spring Initializr</h2>
        <p class="textExemple">
          Spring Initializr est l'outil officiel recommandé par l'équipe Spring pour initialiser un projet Spring Boot. Il s'agit d'une application web simple qui génère la structure de base d'un projet Spring Boot avec toutes les configurations nécessaires.
        </p>
        <p class="textExemple">
          L'objectif principal de Spring Initializr est de simplifier et d'accélérer le démarrage d'un nouveau projet en éliminant la configuration manuelle fastidieuse. Il vous permet de choisir les dépendances dont vous avez besoin, configure automatiquement les fichiers de build, et génère une structure de projet conforme aux meilleures pratiques de l'écosystème Spring.
        </p>
        <div class="text-center mt-4">
          <a href="https://start.spring.io" target="_blank" class="btn-purple btn-hover">Accéder à Spring Initializr</a>
        </div>
      </section>

      <!-- Pourquoi utiliser Spring Initializr -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Pourquoi utiliser Spring Initializr ?</h2>
        
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Sans Spring Initializr</h4>
            <ul class="textExemple">
              <li>Création manuelle de la structure de projet</li>
              <li>Configuration manuelle des fichiers de build (pom.xml ou build.gradle)</li>
              <li>Recherche et ajout manuel des dépendances</li>
              <li>Gestion manuelle des versions de compatibilité</li>
              <li>Configuration manuelle des plugins et outils</li>
              <li>Risque d'erreurs de configuration</li>
            </ul>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Avec Spring Initializr</h4>
            <ul class="textExemple">
              <li>Interface web intuitive et simple d'utilisation</li>
              <li>Génération automatique de la structure de projet</li>
              <li>Sélection visuelle des dépendances avec descriptions</li>
              <li>Gestion automatique des compatibilités de versions</li>
              <li>Configuration optimale des plugins et outils</li>
              <li>Suivi des meilleures pratiques de l'écosystème Spring</li>
            </ul>
          </div>
        </div>
        
        <p class="textExemple mt-4">
          Spring Initializr garantit que votre projet démarre sur des bases solides, avec une configuration optimale et conforme aux standards actuels. Cela réduit considérablement le temps passé sur la configuration initiale et minimise les risques d'erreurs.
        </p>
      </section>

      <!-- Étapes détaillées de configuration -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Configuration étape par étape</h2>
        
        <h3 class="text-purple mt-4">Étape 1 : Type de projet et langage</h3>
        <p class="textExemple">
          La première section vous permet de choisir les fondations de votre projet :
        </p>
        <div class="code-example">
          <pre><code>
<span class="comment">// Options disponibles :</span>

<span class="comment">// Type de projet :</span>
- Maven Project (fichier pom.xml)
- Gradle Project (fichier build.gradle)

<span class="comment">// Langage de programmation :</span>
- Java (choix recommandé pour la majorité des projets)
- Kotlin (alternative moderne et concise)
- Groovy (langage dynamique pour des cas spécifiques)

<span class="comment">// Version de Spring Boot :</span>
- Choisissez la version stable la plus récente (non SNAPSHOT)
- Les versions LTS (Long Term Support) offrent une stabilité prolongée
          </code></pre>
        </div>
        <p class="textExemple">
          Pour la plupart des projets débutants et intermédiaires, nous recommandons : <strong>Maven Project</strong>, <strong>Java</strong>, et la dernière version <strong>stable</strong> de Spring Boot.
        </p>

        <h3 class="text-purple mt-4">Étape 2 : Métadonnées du projet</h3>
        <p class="textExemple">
          Cette section définit l'identité de votre projet dans l'écosystème Java :
        </p>
        <div class="code-example">
          <pre><code>
<span class="comment">// Métadonnées à configurer :</span>

<span class="variable">Group</span> : com.votresociete      <span class="comment">// Identifiant de votre organisation</span>
<span class="variable">Artifact</span> : nom-du-projet      <span class="comment">// Nom technique du projet</span>
<span class="variable">Name</span> : Nom du Projet         <span class="comment">// Nom d'affichage (peut contenir des espaces)</span>
<span class="variable">Description</span> : Description...  <span class="comment">// Brève description du projet</span>
<span class="variable">Package name</span> : auto-généré   <span class="comment">// Généré à partir de Group + Artifact</span>

<span class="comment">// Packaging :</span>
- JAR (recommandé) : Application autonome avec serveur embarqué
- WAR : Pour déploiement sur serveur d'applications externe

<span class="comment">// Version Java :</span>
- 17 ou 21 (versions LTS recommandées)
- 11 (pour compatibilité avec des environnements spécifiques)
          </code></pre>
        </div>
        <p class="textExemple">
          La convention de nommage recommande d'utiliser le domaine inversé de votre organisation pour le Group (ex: com.votresociete, org.votreorganisation). L'Artifact doit être en minuscules avec des tirets si nécessaire.
        </p>

        <h3 class="text-purple mt-4">Étape 3 : Sélection des dépendances</h3>
        <p class="textExemple">
          C'est la partie la plus importante de la configuration. Les dépendances déterminent les fonctionnalités disponibles dans votre projet. Vous pouvez rechercher et ajouter des dépendances via le champ de recherche ou en parcourant les catégories.
        </p>
        
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Dépendances essentielles</h4>
            <ul class="textExemple">
              <li><strong>Spring Web</strong> : Pour créer des applications web et APIs REST</li>
              <li><strong>Spring Data JPA</strong> : Pour l'accès aux bases de données relationnelles</li>
              <li><strong>Spring Boot DevTools</strong> : Outils de développement (redémarrage automatique, etc.)</li>
              <li><strong>Spring Security</strong> : Authentification et autorisation (ajouter selon besoin)</li>
            </ul>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Dépendances optionnelles courantes</h4>
            <ul class="textExemple">
              <li><strong>H2 Database</strong> : Base de données en mémoire pour le développement</li>
              <li><strong>MySQL Driver</strong> : Connexion aux bases de données MySQL</li>
              <li><strong>PostgreSQL Driver</strong> : Connexion aux bases de données PostgreSQL</li>
              <li><strong>Spring Boot Actuator</strong> : Monitoring et gestion de l'application</li>
            </ul>
          </div>
        </div>
        
        <p class="textExemple mt-3">
          Conseil important : Ne sélectionnez que les dépendances dont vous avez réellement besoin au démarrage. Vous pourrez toujours en ajouter ultérieurement en modifiant votre fichier de build.
        </p>
      </section>

      <!-- Génération et structure du projet -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Génération et structure du projet</h2>
        
        <h3 class="text-purple mt-4">Génération du projet</h3>
        <p class="textExemple">
          Après avoir configuré toutes les options, cliquez sur le bouton <strong>"Generate"</strong> (ou utilisez le raccourci CTRL+ENTER). Spring Initializr va générer un fichier ZIP contenant la structure complète de votre projet.
        </p>
        
        <h3 class="text-purple mt-4">Structure du projet généré</h3>
        <p class="textExemple">
          Après extraction du fichier ZIP, vous obtiendrez une structure de projet standard :
        </p>
        <div class="code-example">
          <pre><code>
nom-du-projet/
├── <span class="comment">pom.xml</span>                    <span class="comment">// Configuration Maven (dépendances, plugins)</span>
├── <span class="comment">mvnw</span>                       <span class="comment">// Maven Wrapper (exécutable Unix)</span>
├── <span class="comment">mvnw.cmd</span>                   <span class="comment">// Maven Wrapper (exécutable Windows)</span>
├── <span class="comment">.mvn/</span>                       <span class="comment">// Configuration du Maven Wrapper</span>
├── <span class="comment">src/</span>
│   ├── <span class="comment">main/</span>
│   │   ├── <span class="comment">java/</span>
│   │   │   └── <span class="comment">com/votresociete/nomduprojet/</span>
│   │   │       └── <span class="comment">NomduprojetApplication.java</span>  <span class="comment">// Classe principale</span>
│   │   └── <span class="comment">resources/</span>
│   │       ├── <span class="comment">application.properties</span>        <span class="comment">// Fichier de configuration</span>
│   │       ├── <span class="comment">static/</span>                     <span class="comment">// Ressources statiques (CSS, JS, images)</span>
│   │       └── <span class="comment">templates/</span>                  <span class="comment">// Templates de vues (si applicable)</span>
│   └── <span class="comment">test/</span>                               <span class="comment">// Tests unitaires et d'intégration</span>
│       └── <span class="comment">java/</span>
│           └── <span class="comment">com/votresociete/nomduprojet/</span>
│               └── <span class="comment">NomduprojetApplicationTests.java</span>  <span class="comment">// Test de la classe principale</span>
          </code></pre>
        </div>
        
        <h3 class="text-purple mt-4">Le fichier pom.xml généré</h3>
        <p class="textExemple">
          Voici un exemple de ce que Spring Initializr génère dans le fichier pom.xml :
        </p>
        <div class="code-example">
          <pre><code>
<span class="comment">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
&lt;project xmlns="http://maven.apache.org/POM/4.0.0"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
    
    <span class="comment">&lt;!-- Héritage de Spring Boot --&gt;</span>
    &lt;parent&gt;
        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
        &lt;artifactId&gt;spring-boot-starter-parent&lt;/artifactId&gt;
        &lt;version&gt;3.1.5&lt;/version&gt; <span class="comment">&lt;!-- Version configurée --&gt;</span>
    &lt;/parent&gt;
    
    <span class="comment">&lt;!-- Métadonnées configurées --&gt;</span>
    &lt;groupId&gt;com.votresociete&lt;/groupId&gt;
    &lt;artifactId&gt;nom-du-projet&lt;/artifactId&gt;
    &lt;version&gt;0.0.1-SNAPSHOT&lt;/version&gt;
    &lt;name&gt;nom-du-projet&lt;/name&gt;
    &lt;description&gt;Description du projet&lt;/description&gt;
    
    <span class="comment">&lt;!-- Propriétés Java --&gt;</span>
    &lt;properties&gt;
        &lt;java.version&gt;17&lt;/java.version&gt; <span class="comment">&lt;!-- Version Java configurée --&gt;</span>
    &lt;/properties&gt;
    
    <span class="comment">&lt;!-- Dépendances sélectionnées --&gt;</span>
    &lt;dependencies&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-web&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-test&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        <span class="comment">&lt;!-- Autres dépendances ajoutées --&gt;</span>
    &lt;/dependencies&gt;
    
    <span class="comment">&lt;!-- Plugin Spring Boot --&gt;</span>
    &lt;build&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
                &lt;artifactId&gt;spring-boot-maven-plugin&lt;/artifactId&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
    &lt;/build&gt;
&lt;/project&gt;
          </code></pre>
        </div>
      </section>

      <!-- Premiers pas avec le projet généré -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Premiers pas avec le projet généré</h2>
        
        <h3 class="text-purple mt-4">Importation dans un IDE</h3>
        <p class="textExemple">
          Le projet généré peut être importé dans n'importe quel IDE supportant Maven ou Gradle :
        </p>
        <ul class="textExemple">
          <li><strong>IntelliJ IDEA</strong> : File → Open → Sélectionnez le dossier du projet</li>
          <li><strong>Eclipse</strong> : File → Import → Maven → Existing Maven Projects</li>
          <li><strong>VS Code</strong> : Ouvrez le dossier, installez les extensions Java et Spring Boot</li>
        </ul>
        
        <h3 class="text-purple mt-4">Première exécution</h3>
        <p class="textExemple">
          Vous pouvez exécuter votre application Spring Boot de plusieurs façons :
        </p>
        
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Via la ligne de commande</h4>
            <pre><code>
<span class="comment"># Avec le Maven Wrapper (recommandé)</span>
<span class="function">./mvnw spring-boot:run</span>      <span class="comment"># Linux/Mac</span>
<span class="function">mvnw.cmd spring-boot:run</span>    <span class="comment"># Windows</span>

<span class="comment"># Avec Maven installé globalement</span>
<span class="function">mvn spring-boot:run</span>
            </code></pre>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Via votre IDE</h4>
            <pre><code>
<span class="comment">// IntelliJ : Exécutez la classe principale</span>
<span class="comment">// Eclipse : Run As → Spring Boot App</span>
<span class="comment">// VS Code : Spring Boot Dashboard → Start</span>

<span class="comment">// L'application démarre sur :</span>
<span class="comment">// http://localhost:8080</span>
            </code></pre>
          </div>
        </div>
        
        <h3 class="text-purple mt-4">Vérification du démarrage</h3>
        <p class="textExemple">
          Lorsque votre application démarre, vous devriez voir dans les logs quelque chose comme :
        </p>
        <div class="code-example">
          <pre><code>
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.1.5)

2023-11-15T10:30:00.000+01:00  INFO 12345 --- [main]
  c.v.n.NomduprojetApplication   : Starting NomduprojetApplication
2023-11-15T10:30:00.500+01:00  INFO 12345 --- [main]
  o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8080
2023-11-15T10:30:00.502+01:00  INFO 12345 --- [main]
  c.v.n.NomduprojetApplication   : Started NomduprojetApplication in 1.5 seconds
          </code></pre>
        </div>
      </section>

      <!-- Bonnes pratiques et conseils -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Bonnes pratiques et conseils</h2>
        
        <h3 class="text-purple mt-4">Conseils de configuration</h3>
        <ul class="textExemple">
          <li><strong>Commencez simple</strong> : Ajoutez uniquement les dépendances essentielles au départ</li>
          <li><strong>Utilisez le Maven/Gradle Wrapper</strong> : Cela garantit que tous les développeurs utilisent la même version des outils</li>
          <li><strong>Versionnez votre code</strong> : Initialisez un dépôt Git dès la génération du projet</li>
          <li><strong>Documentez les choix</strong> : Notez pourquoi certaines dépendances ont été choisies</li>
        </ul>
        
        <h3 class="text-purple mt-4">Dépendances couramment utilisées</h3>
        <div class="code-example">
          <pre><code>
<span class="comment">// Pour une API REST complète :</span>
- Spring Web
- Spring Data JPA
- Spring Boot DevTools
- H2 Database (développement)
- Spring Security (si besoin d'authentification)

<span class="comment">// Pour une application web traditionnelle :</span>
- Spring Web
- Thymeleaf (templates HTML)
- Spring Boot DevTools
- Spring Security

<span class="comment">// Pour un microservice :</span>
- Spring Web
- Spring Cloud dependencies (via Spring Initializr ou manuellement)
- Spring Boot Actuator (monitoring)
          </code></pre>
        </div>
        
        <h3 class="text-purple mt-4">Éviter les pièges courants</h3>
        <ul class="textExemple">
          <li><strong>Ne pas surcharger en dépendances</strong> : Chaque dépendance ajoute de la complexité et du temps de build</li>
          <li><strong>Vérifier les compatibilités</strong> : Certaines dépendances peuvent ne pas être compatibles entre elles</li>
          <li><strong>Sauvegarder la configuration</strong> : Notez les paramètres utilisés pour pouvoir régénérer le projet si nécessaire</li>
          <li><strong>Tester immédiatement</strong> : Lancez le projet tout de suite pour vérifier qu'il fonctionne</li>
        </ul>
      </section>

      <!-- Alternatives et options avancées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Alternatives et options avancées</h2>
        
        <h3 class="text-purple mt-4">Spring Initializr via ligne de commande</h3>
        <p class="textExemple">
          Vous pouvez également utiliser Spring Initializr via curl ou HTTPie :
        </p>
        <div class="code-example">
          <pre><code>
<span class="comment"># Exemple avec curl :</span>
<span class="function">curl https://start.spring.io/starter.zip \</span>
  <span class="function">-d type=maven-project \</span>
  <span class="function">-d language=java \</span>
  <span class="function">-d bootVersion=3.1.5 \</span>
  <span class="function">-d baseDir=mon-projet \</span>
  <span class="function">-d groupId=com.example \</span>
  <span class="function">-d artifactId=demo \</span>
  <span class="function">-d name=demo \</span>
  <span class="function">-d description=Demo%20project \</span>
  <span class="function">-d packageName=com.example.demo \</span>
  <span class="function">-d packaging=jar \</span>
  <span class="function">-d javaVersion=17 \</span>
  <span class="function">-d dependencies=web,devtools \</span>
  <span class="function">-o demo.zip</span>
          </code></pre>
        </div>
        
        <h3 class="text-purple mt-4">Intégration avec les IDEs</h3>
        <p class="textExemple">
          La plupart des IDEs modernes intègrent Spring Initializr directement :
        </p>
        <ul class="textExemple">
          <li><strong>IntelliJ IDEA Ultimate</strong> : Intégration native via le menu New Project</li>
          <li><strong>Spring Tools Suite (STS)</strong> : Intégration complète dédiée à Spring</li>
          <li><strong>VS Code avec extension Spring Boot</strong> : Assistant de création de projet</li>
        </ul>
        
        <h3 class="text-purple mt-4">Spring Initializr API</h3>
        <p class="textExemple">
          Spring Initializr expose également une API REST que vous pouvez utiliser dans vos scripts ou outils :
        </p>
        <div class="code-example">
          <pre><code>
<span class="comment">// Récupérer les métadonnées (versions disponibles, etc.) :</span>
GET https://start.spring.io

<span class="comment">// Générer un projet avec des paramètres spécifiques :</span>
POST https://start.spring.io/starter.zip
Content-Type: application/json

{
  "type": "maven-project",
  "language": "java",
  "bootVersion": "3.1.5",
  "groupId": "com.example",
  "artifactId": "demo",
  "dependencies": ["web", "devtools"]
}
          </code></pre>
        </div>
      </section>

      <!-- Conclusion et exercice -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white mb-3">Exercice pratique</h2>
        
        <p class="text-white">
          Maintenant que vous comprenez comment utiliser Spring Initializr, réalisez l'exercice suivant pour pratiquer :
        </p>
        
        <div class="exercise mt-4">
          <h3 class="text-white">Objectif</h3>
          <p class="text-white">
            Créer un projet Spring Boot pour une API de gestion de bibliothèque
          </p>
          
          <h3 class="text-white mt-3">Spécifications</h3>
          <ol class="text-white">
            <li>Utilisez Spring Initializr pour générer le projet</li>
            <li>Configurez les métadonnées :
              <ul>
                <li>Group : com.bibliotheque</li>
                <li>Artifact : api-bibliotheque</li>
                <li>Description : API pour la gestion d'une bibliothèque</li>
                <li>Java version : 17</li>
                <li>Packaging : JAR</li>
              </ul>
            </li>
            <li>Ajoutez les dépendances suivantes :
              <ul>
                <li>Spring Web</li>
                <li>Spring Data JPA</li>
                <li>H2 Database</li>
                <li>Spring Boot DevTools</li>
                <li>Spring Boot Actuator</li>
              </ul>
            </li>
            <li>Générez et téléchargez le projet</li>
            <li>Importez-le dans votre IDE et exécutez-le</li>
            <li>Vérifiez que l'application démarre correctement</li>
            <li>Accédez à http://localhost:8080/actuator/health pour vérifier le statut</li>
          </ol>
          
          <h3 class="text-white mt-3">Validation</h3>
          <p class="text-white">
            Si l'exercice est réussi, vous devriez voir dans les logs que l'application démarre sur le port 8080, et l'endpoint /actuator/health devrait retourner {"status":"UP"}.
          </p>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
// Logique minimale pour cette page de leçon
</script>

<style scoped>
/* Votre CSS fourni est déjà intégré ici */
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

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }

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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }

/* Classes utilitaires */
.mt-3 { margin-top: 1rem; }
.mt-4 { margin-top: 1.5rem; }
.mb-3 { margin-bottom: 1rem; }
.text-center { text-align: center; }
</style>