<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">L'Importance du Fichier .env</h1>
        <p class="lesson-meta text-white">Apprenez pourquoi et comment utiliser les variables d'environnement pour sécuriser et configurer vos applications</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p>Le fichier <strong>.env</strong> (environment) est un élément crucial dans le développement moderne d'applications. Il permet de gérer la configuration de manière sécurisée et organisée, séparant les paramètres sensibles du code source.</p>
        
        <div class="textExemple">
          <h3 class="text-purple">Objectifs d'apprentissage</h3>
          <ul>
            <li>Comprendre l'utilité des variables d'environnement</li>
            <li>Apprendre à créer et utiliser un fichier .env</li>
            <li>Découvrir les bonnes pratiques de sécurité</li>
            <li>Implémenter .env dans différents frameworks</li>
            <li>Gérer les configurations multi-environnements</li>
          </ul>
        </div>
      </section>

      <!-- Section 1: Pourquoi utiliser .env ? -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">1. Pourquoi utiliser un fichier .env ?</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">AVANT (Sans .env) - Dangereux</h4>
            <div class="code-block">
              <pre>// config/database.php
$host = 'localhost';
$dbname = 'ma_base_production';
$username = 'root';
$password = 'MonSuperMotDePasse123!';

// Clés API exposées
$stripe_key = 'sk_live_123456789';
$sendgrid_key = 'SG.abc123...';</pre>
            </div>
            <p class="text-danger">Risques :</p>
            <ul>
              <li>Mot de passe en clair dans le code</li>
              <li>Clés API exposées</li>
              <li>Impossible de changer sans modifier le code</li>
              <li>Problèmes en collaboration d'équipe</li>
            </ul>
          </div>
          <div>
            <h4 class="text-purple">APRES (Avec .env) - Securise</h4>
            <div class="code-block">
              <pre># .env
DB_HOST=localhost
DB_NAME=ma_base_production
DB_USER=root
DB_PASS=MonSuperMotDePasse123!

STRIPE_SECRET_KEY=sk_live_123456789
SENDGRID_API_KEY=SG.abc123...</pre>
            </div>
            <p class="text-success">Avantages :</p>
            <ul>
              <li>Configuration centralisée</li>
              <li>Securite amelioree</li>
              <li>Environnements multiples</li>
              <li>Collaboration facilitee</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Section 2: Création d'un fichier .env -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">2. Creation et Structure d'un Fichier .env</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Structure typique d'un fichier .env</h3>
          <div class="code-block">
            <pre># APPLICATION CONFIGURATION
APP_NAME="Mon Application"
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8000

# DATABASE CONFIGURATION
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ma_base
DB_USERNAME=root
DB_PASSWORD=secret

# EXTERNAL SERVICES
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null

# API Keys (NE JAMAIS PARTAGER !)
STRIPE_SECRET_KEY=sk_test_123456789
STRIPE_PUBLIC_KEY=pk_test_123456789
SENDGRID_API_KEY=SG.abc123def456</pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Regles de syntaxe</h4>
          <ul>
            <li><strong>Noms en MAJUSCULES</strong> avec underscores : DB_HOST</li>
            <li><strong>Pas d'espaces</strong> autour du =</li>
            <li><strong>Guillemets</strong> optionnels pour les valeurs</li>
            <li><strong>Commentaires</strong> avec #</li>
            <li><strong>Pas de valeurs vides</strong> - utiliser "null" ou ""</li>
          </ul>
        </div>
      </section>

      <!-- Section 3: Utilisation en PHP -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">3. Utilisation des Variables d'Environnement en PHP</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Methode manuelle avec parse_ini_file()</h3>
          <div class="code-block">
            <pre>// Chargement du fichier .env
$env = parse_ini_file('.env');

// Utilisation des variables
$db_host = $env['DB_HOST'] ?? 'localhost';
$db_name = $env['DB_NAME'] ?? 'default_db';
$db_user = $env['DB_USER'] ?? 'root';
$db_pass = $env['DB_PASS'] ?? '';

// Connexion à la base de données
try {
    $pdo = new PDO(
        "mysql:host=$db_host;dbname=$db_name",
        $db_user,
        $db_pass
    );
} catch(PDOException $e) {
    echo "Erreur de connexion: " . $e->getMessage();
}

// Utilisation des clés API
$stripe_secret = $env['STRIPE_SECRET_KEY'] ?? null;
$sendgrid_key = $env['SENDGRID_API_KEY'] ?? null;</pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Classe Helper pour gerer .env</h3>
          <div class="code-block">
            <pre>class Env {
    private static $variables = [];

    public static function load($path = '.env') {
        if (!file_exists($path)) {
            throw new Exception("Fichier .env non trouvé");
        }

        $lines = file($path, FILE_IGNORE_NEW_LINES | FILE_SKIP_EMPTY_LINES);
        
        foreach ($lines as $line) {
            // Ignorer les commentaires
            if (strpos(trim($line), '#') === 0) {
                continue;
            }

            // Separer nom et valeur
            list($name, $value) = explode('=', $line, 2);
            $name = trim($name);
            $value = trim($value);

            // Supprimer les guillemets
            $value = trim($value, '"\'"');

            // Stocker dans le tableau
            self::$variables[$name] = $value;
            
            // Definir aussi dans $_ENV pour compatibilite
            $_ENV[$name] = $value;
            putenv("$name=$value");
        }
    }

    public static function get($key, $default = null) {
        return self::$variables[$key] ?? $default;
    }
}

// Utilisation
Env::load();

$dbHost = Env::get('DB_HOST', 'localhost');
$apiKey = Env::get('STRIPE_SECRET_KEY');</pre>
          </div>
        </div>
      </section>

      <!-- Section 4: Gestion multi-environnements -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">4. Gestion des Multi-Environnements</h2>
        
        <div class="code-example">
          <h3 class="text-purple">Structure pour differents environnements</h3>
          <div class="code-block">
            <pre># Structure de fichiers
.env                    # valeurs par defaut (optionnel)
.env.local             # surcharge pour l'environnement local
.env.development        # developpement
.env.staging           # pre-production
.env.production         # production
.env.example           # template pour nouveaux developpeurs</pre>
          </div>
        </div>

        <div class="code-comparison">
          <div>
            <h4 class="text-purple">.env.development</h4>
            <div class="code-block">
              <pre>APP_ENV=development
APP_DEBUG=true
APP_URL=http://localhost:8000

DB_HOST=localhost
DB_NAME=myapp_dev
DB_USER=dev_user
DB_PASS=dev_password

STRIPE_SECRET_KEY=sk_test_123456789</pre>
            </div>
          </div>
          <div>
            <h4 class="text-purple">.env.production</h4>
            <div class="code-block">
              <pre>APP_ENV=production
APP_DEBUG=false
APP_URL=https://monapp.com

DB_HOST=db.production.com
DB_NAME=myapp_prod
DB_USER=prod_user
DB_PASS=SuperMot2Passe!Complexe

STRIPE_SECRET_KEY=sk_live_987654321</pre>
            </div>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Chargement automatique selon l'environnement</h3>
          <div class="code-block">
            <pre>// Determiner l'environnement
$environment = getenv('APP_ENV') ?: 'development';

// Charger le fichier .env correspondant
$envFile = '.env.' . $environment;

if (file_exists($envFile)) {
    Env::load($envFile);
} elseif (file_exists('.env')) {
    Env::load('.env');
} else {
    throw new Exception('Aucun fichier .env trouvé');
}</pre>
          </div>
        </div>
      </section>

      <!-- Section 5: Bonnes pratiques de sécurité -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">5. Bonnes Pratiques de Securite</h2>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">A FAIRE</h4>
            <ul>
              <li>Ajouter .env dans .gitignore</li>
              <li>Creer un .env.example versionne</li>
              <li>Utiliser des mots de passe complexes</li>
              <li>Changer les cles entre environnements</li>
              <li>Valider les variables requises</li>
              <li>Chiffrer les fichiers en production</li>
            </ul>
          </div>
          <div>
            <h4 class="text-purple">A EVITER</h4>
            <ul>
              <li>Committer le fichier .env</li>
              <li>Utiliser des valeurs par defaut faibles</li>
              <li>Partager le .env par email</li>
              <li>Stocker en clair sur le serveur</li>
              <li>Utiliser les memes cles partout</li>
              <li>Oublier de mettre a jour .env.example</li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Fichier .gitignore</h3>
          <div class="code-block">
            <pre># Fichiers d'environnement
.env
.env.local
.env.*.local
!.env.example  # sauf le template

# Fichiers sensibles
config/credentials.json
*.key
*.pem
*.cert</pre>
          </div>
        </div>

        <div class="code-example">
          <h3 class="text-purple">Validation des variables requises</h3>
          <div class="code-block">
            <pre>class EnvValidator {
    public static function validateRequired($requiredVars = []) {
        $missing = [];

        foreach ($requiredVars as $var) {
            if (empty(Env::get($var))) {
                $missing[] = $var;
            }
        }

        if (!empty($missing)) {
            throw new Exception(
                "Variables d'environnement manquantes: " . 
                implode(', ', $missing)
            );
        }
    }
}

// Utilisation
EnvValidator::validateRequired([
    'DB_HOST',
    'DB_NAME', 
    'DB_USER',
    'DB_PASS',
    'APP_KEY'
]);</pre>
          </div>
        </div>
      </section>

      <!-- Section 6: Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">6. Exercice Pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Mission : Securiser une Application</h3>
          <p>Vous avez herite d'une application PHP avec les informations sensibles en dur dans le code. Votre mission est de la securiser en utilisant un fichier .env.</p>
          
          <div class="code-example">
            <h4 class="text-purple">Code initial (a corriger)</h4>
            <div class="code-block">
              <pre>// Ancien code avec donnees sensibles en dur
$database = [
    'host' => 'prod-db.example.com',
    'name' => 'production_database',
    'user' => 'admin',
    'pass' => 'SuperSecret123!'
];

$stripe = [
    'secret_key' => 'sk_live_abc123def456',
    'public_key' => 'pk_live_xyz789'
];

$email = [
    'smtp_host' => 'smtp.sendgrid.net',
    'smtp_user' => 'apikey',
    'smtp_pass' => 'SG.abc123.def456'
];</pre>
            </div>
          </div>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <h4 class="text-purple">Etape 1 : Creer le fichier .env</h4>
              <div class="code-block">
                <pre># .env
APP_ENV=production
APP_DEBUG=false

DB_HOST=prod-db.example.com
DB_NAME=production_database
DB_USER=admin
DB_PASS=SuperSecret123!

STRIPE_SECRET_KEY=sk_live_abc123def456
STRIPE_PUBLIC_KEY=pk_live_xyz789

SMTP_HOST=smtp.sendgrid.net
SMTP_USER=apikey
SMTP_PASS=SG.abc123.def456</pre>
              </div>

              <h4 class="text-purple">Etape 2 : Code final securise</h4>
              <div class="code-block">
                <pre>// Nouveau code utilisant .env
$database = [
    'host' => Env::get('DB_HOST'),
    'name' => Env::get('DB_NAME'),
    'user' => Env::get('DB_USER'),
    'pass' => Env::get('DB_PASS')
];

$stripe = [
    'secret_key' => Env::get('STRIPE_SECRET_KEY'),
    'public_key' => Env::get('STRIPE_PUBLIC_KEY')
];

$email = [
    'smtp_host' => Env::get('SMTP_HOST'),
    'smtp_user' => Env::get('SMTP_USER'),
    'smtp_pass' => Env::get('SMTP_PASS')
];</pre>
              </div>
            </div>
          </details>
        </div>
      </section>

      <!-- Section 7: Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p>Le fichier .env est bien plus qu'une simple convention - c'est une pratique essentielle pour le developpement moderne d'applications securisees et maintenables.</p>
        
        <div class="textExemple">
          <h3 class="text-purple">Points Cles a Retenir</h3>
          <ul>
            <li><strong>Securite</strong> : Ne jamais commettre de donnees sensibles</li>
            <li><strong>Flexibilite</strong> : Configuration par environnement</li>
            <li><strong>Collaboration</strong> : .env.example pour l'equipe</li>
            <li><strong>Deploiement</strong> : Variables d'environnement en production</li>
            <li><strong>Maintenabilite</strong> : Configuration centralisee</li>
          </ul>
        </div>
        
        <a href="#" class="btn-purple btn-hover">Passer a la lecon suivante</a>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EnvFileLesson',
  data() {
    return {
      lessonTitle: 'L\'Importance du Fichier .env'
    }
  },
  head() {
    return {
      title: this.lessonTitle,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Apprenez pourquoi et comment utiliser les variables d\'environnement pour securiser et configurer vos applications professionnelles.'
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

pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

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

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

.text-danger {
    color: #dc3545 !important;
    font-weight: bold;
}

.text-success {
    color: #28a745 !important;
    font-weight: bold;
}

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