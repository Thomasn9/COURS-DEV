<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Injection SQL – Comprendre et prévenir l'attaque</h1>
                <p class="lesson-meta text-white">Sécurité • Base de données • SQL • OWASP Top 10</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'une injection SQL ?</h2>
                <p class="textExemple">
                    L’<strong>injection SQL</strong> (SQLi) est une technique d’attaque qui consiste à insérer du code SQL malveillant
                    dans une requête, via une entrée utilisateur non filtrée. Si l’application construit dynamiquement
                    une requête SQL en concaténant des chaînes, l’attaquant peut modifier la structure de la requête
                    pour lire, modifier ou supprimer des données, voire exécuter des commandes sur le serveur.
                </p>
                <div class="warning-section">
                    <h4 class="text-purple">⚠️ Risques majeurs</h4>
                    <ul>
                        <li>Lecture de données sensibles (identifiants, emails, cartes bancaires)</li>
                        <li>Modification ou suppression de données</li>
                        <li>Contournement d’authentification</li>
                        <li>Exécution de commandes système (via <code>xp_cmdshell</code> sur SQL Server, ou <code>INTO OUTFILE</code> sur MySQL)</li>
                        <li>Prise de contrôle du serveur de base de données</li>
                    </ul>
                </div>
            </section>

            <!-- Exemple simple d'injection -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple concret d’injection SQL</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Code vulnérable (PHP)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Récupération de l'identifiant depuis l'URL
$id = $_GET['id'];

// Requête construite par concaténation
$sql = "SELECT * FROM utilisateurs WHERE id = " . $id;
$result = $conn->query($sql);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Attaque possible</h3>
                    <p>L’attaquant appelle l’URL suivante :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-http">https://exemple.com/profil?id=1 OR 1=1</code></pre>
                    </div>
                    <p>La requête devient :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">SELECT * FROM utilisateurs WHERE id = 1 OR 1=1</code></pre>
                    </div>
                    <p>La condition <code>1=1</code> étant toujours vraie, la requête retourne <strong>tous les utilisateurs</strong>.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contournement d’authentification</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$sql = "SELECT * FROM users WHERE login = '$login' AND password = '$password'";</code></pre>
                    </div>
                    <p>L’attaquant saisit :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">login : admin' --
password : n'importe quoi</code></pre>
                    </div>
                    <p>La requête devient :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">SELECT * FROM users WHERE login = 'admin' -- ' AND password = '...'</code></pre>
                    </div>
                    <p>Le reste de la requête est commenté (<code>--</code>). L’attaquant est connecté en tant qu’<strong>admin sans connaître son mot de passe</strong>.</p>
                </div>
            </section>

            <!-- Types d'injection SQL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les différents types d'injection SQL</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Injection classique (in‑band)</h3>
                    <p>L’attaquant récupère les données directement dans la réponse HTTP (exemple ci‑dessus).</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Injection aveugle (blind)</h3>
                    <p>L’application n’affiche pas les données, mais son comportement change (vrai/faux, temps de réponse).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">SELECT * FROM users WHERE id = 1 AND (SELECT SUBSTRING(password,1,1) FROM users WHERE id=1) = 'a'</code></pre>
                    </div>
                    <p>L’attaquant peut ainsi deviner le mot de passe caractère par caractère.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Injection hors bande (out‑of‑band)</h3>
                    <p>L’exfiltration des données se fait par un autre canal (DNS, HTTP externe). Utilisé quand la réponse directe n’est pas possible.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">4. Injection temporelle (time‑based)</h3>
                    <p>L’attaquant mesure le temps de réponse pour déduire des informations.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-sql">SELECT * FROM users WHERE id = 1 AND IF(1=1, SLEEP(5), 0)</code></pre>
                    </div>
                </div>
            </section>

            <!-- Prévention – Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Comment se protéger des injections SQL ?</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Utiliser des requêtes paramétrées (requêtes préparées)</h3>
                    <p>C’est la méthode <strong>la plus efficace</strong>. Les paramètres sont envoyés séparément du SQL, donc jamais interprétés comme du code.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// PDO
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
$stmt->execute(['id' => $id]);

// MySQLi
$stmt = $mysqli->prepare("SELECT * FROM users WHERE id = ?");
$stmt->bind_param("i", $id);
$stmt->execute();</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Utiliser un ORM (Doctrine, Eloquent, etc.)</h3>
                    <p>Les ORM utilisent nativement des requêtes paramétrées.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Doctrine (Symfony)
$user = $repo->find($id);
// ou
$user = $repo->findOneBy(['login' => $login]);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Valider et filtrer les entrées (whitelist)</h3>
                    <p>Pour les données qui doivent correspondre à un format précis (ex: email, nombre), validez avant tout.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">if (!ctype_digit($id)) {
    throw new Exception("ID invalide");
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">4. Échapper les caractères spéciaux (en dernier recours)</h3>
                    <p>Si vous ne pouvez pas utiliser de requêtes préparées, échappez les entrées avec la fonction adaptée à votre SGBD.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$safe = mysqli_real_escape_string($conn, $userInput);</code></pre>
                    </div>
                    <div class="warning-section">
                        <h4 class="text-purple">⚠️ Attention</h4>
                        <p>L’échappement n’est pas infaillible selon l’encodage (problèmes de charset). Préférez toujours les requêtes préparées.</p>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">5. Principe du moindre privilège</h3>
                    <p>Le compte de base de données utilisé par l’application ne doit avoir que les droits nécessaires (SELECT, INSERT, UPDATE sur certaines tables, jamais DROP, CREATE, FILE).</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">6. Utiliser un pare-feu applicatif (WAF)</h3>
                    <p>Un WAF peut bloquer des patterns d’injection connus, mais ne remplace pas un code sûr.</p>
                </div>
            </section>

            <!-- Exemples de payloads (à des fins éducatives) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Payloads SQL courants (éducation uniquement)</h2>
                <div class="warning-section">
                    <h4 class="text-purple">⚠️ Ne testez que sur vos propres applications ou environnements dédiés (ex: DVWA, SQLi Labs).</h4>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-sql">-- Contournement de login
' OR '1'='1' --
admin' --
admin' #

-- Union pour extraire des données
' UNION SELECT 1,2,3,4 --
' UNION SELECT username, password FROM users --

-- Sous-requêtes
' AND (SELECT COUNT(*) FROM users) > 10 --

-- Time-based (MySQL)
' AND SLEEP(5) --

-- Commentaires
admin' /* commentaire */</code></pre>
                </div>
            </section>

            <!-- Outils de détection -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outils pour détecter les failles SQLi</h2>
                <ul>
                    <li><strong>sqlmap</strong> : outil automatisé de détection et d’exploitation.</li>
                    <li><strong>OWASP ZAP</strong> : scanner passif/actif.</li>
                    <li><strong>Burp Suite</strong> (version Pro) : scanner avancé.</li>
                    <li><strong>Audit manuel</strong> : tests avec des payloads simples (' , ", etc.).</li>
                </ul>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Trouver et corriger une injection SQL</h3>
                    <p>Le code suivant est vulnérable. Expliquez l’attaque possible et corrigez-le en utilisant une requête préparée.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$search = $_GET['search'];
$sql = "SELECT * FROM produits WHERE nom LIKE '%$search%'";
$result = $conn->query($sql);</code></pre>
                    </div>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <p><strong>Attaque</strong> : <code>search=' OR '1'='1' -- </code> → affiche tous les produits.</p>
                            <pre v-pre><code class="language-php">// Correction avec PDO
$stmt = $conn->prepare("SELECT * FROM produits WHERE nom LIKE :search");
$searchTerm = "%" . $search . "%";
$stmt->execute(['search' => $searchTerm]);</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Injection dans une clause ORDER BY</h3>
                    <p>Le code ci-dessous trie les résultats selon le paramètre <code>sort</code>. Pourquoi est-ce dangereux ? Comment corriger ?</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$sort = $_GET['sort'] ?? 'nom';
$sql = "SELECT * FROM articles ORDER BY $sort";
$result = $conn->query($sql);</code></pre>
                    </div>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <p>Un attaquant peut injecter : <code>sort=(SELECT SLEEP(5))</code> ou <code>sort=id; DROP TABLE articles --</code> (selon SGBD).</p>
                            <p><strong>Correction</strong> : utiliser une whitelist des colonnes autorisées.</p>
                            <pre v-pre><code class="language-php">$allowed = ['nom', 'prix', 'date'];
$sort = in_array($_GET['sort'], $allowed) ? $_GET['sort'] : 'nom';
$sql = "SELECT * FROM articles ORDER BY $sort"; // maintenant sûr</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Rôle de l’ORM</h3>
                    <p>Avec Doctrine (Symfony), écrivez une requête sécurisée pour trouver un utilisateur par son email, en évitant toute injection.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// Repository
$user = $userRepository->findOneBy(['email' => $email]);

// QueryBuilder
$user = $userRepository->createQueryBuilder('u')
    ->where('u.email = :email')
    ->setParameter('email', $email)
    ->getQuery()
    ->getOneOrNullResult();</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Les injections SQL sont faciles à comprendre et à prévenir, pourtant elles restent omniprésentes.
                        <strong>La règle d’or : ne jamais construire une requête SQL par concaténation avec des données utilisateur.</strong>
                        Utilisez systématiquement des requêtes paramétrées ou un ORM.
                    </p>
                    <p>
                        Dans la prochaine leçon, nous verrons comment les frameworks comme Symfony, Laravel ou Django
                        vous protègent automatiquement, et ce qu’il faut surveiller malgré tout.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SqlInjectionLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel  = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const sqlScript = document.createElement('script');
                        sqlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/sql.min.js';
                        sqlScript.onload = resolve;
                        document.head.appendChild(sqlScript);
                    };
                    document.head.appendChild(phpScript);
                };
                document.head.appendChild(script);
            });
        };

        loadHighlightJS().then(() => {
            this.$el.querySelectorAll('pre code').forEach((block) => {
                window.hljs.highlightElement(block);
            });
        });
    }
}
</script>

<style scoped>
/* Les styles sont identiques aux leçons précédentes */
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
    top: 0; left: 0; right: 0; bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
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
    animation: fadeInUp 0.6s ease forwards;
}

.lesson-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
}

.bg-light-purple { background-color: #f8f6ff; }
.border-purple { border: 2px solid #e0d6ff; }
.text-purple { color: #6A3093 !important; }
.text-white { color: white !important; }

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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
}

.code-example {
    margin: 1.5rem 0;
    width: 100%;
    box-sizing: border-box;
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
    width: 100%;
    box-sizing: border-box;
    white-space: pre;
    margin: 0;
}

pre code {
    display: block;
    white-space: pre;
    width: 100%;
}

.exercise { margin: 2rem 0; }
.solution { margin: 1rem 0; }
.solution-content {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #8B5FBF;
}

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

@media (max-width: 768px) {
    .lesson-container { padding: 1rem; }
    .lesson-header { padding: 2rem 1rem; }
    .lesson-header h1 { font-size: 2rem; }
    .lesson-section { padding: 1.5rem; }
    pre { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section { padding: 1rem; }
    .lesson-header { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
}
</style>