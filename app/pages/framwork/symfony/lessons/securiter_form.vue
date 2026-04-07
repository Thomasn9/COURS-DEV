<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Sécuriser les formulaires Symfony</h1>
                <p class="lesson-meta text-white">Symfony • Twig • Doctrine • CSRF • XSS • Validation • Injection</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi la sécurité des formulaires est essentielle ?</h2>
                <p class="textExemple">
                    Les formulaires sont la principale porte d'entrée des données utilisateur dans une application.
                    Une faille de sécurité dans un formulaire peut entraîner des attaques comme le <strong>Cross-Site Request Forgery (CSRF)</strong>,
                    les <strong>injections SQL</strong> (via Doctrine), les <strong>attaques XSS</strong> ou encore le <strong>mass assignment</strong>.
                </p>
                <p class="textExemple">
                    Symfony intègre nativement de nombreuses protections, mais il est essentiel de comprendre comment les activer,
                    les configurer et les utiliser correctement avec Twig et Doctrine pour garantir la sécurité de vos données.
                </p>
            </section>

            <!-- CSRF Protection -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Protection CSRF (Cross-Site Request Forgery)</h2>

                <div class="textExemple">
                    <p>
                        La protection CSRF empêche un site malveillant d'envoyer des requêtes non autorisées à votre application
                        en exploitant la session active de l'utilisateur. Symfony active cette protection <strong>par défaut</strong>
                        sur tous les formulaires.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans votre FormType, la protection CSRF est activée automatiquement
class TaskType extends AbstractType
{
    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'csrf_protection' => true,   // activé par défaut
            'csrf_field_name' => '_token', // nom du champ caché
            'csrf_token_id'   => 'task_item', // identifiant unique
        ]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Vérification manuelle du token CSRF (cas particuliers)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un controller, si vous n'utilisez pas le composant Form
use Symfony\Component\Security\Csrf\CsrfTokenManagerInterface;
use Symfony\Component\Security\Csrf\CsrfToken;

public function delete(Request $request, CsrfTokenManagerInterface $csrfTokenManager): Response
{
    $submittedToken = $request->request->get('_token');
    
    if ($csrfTokenManager->isTokenValid(new CsrfToken('delete-item', $submittedToken))) {
        // Traitement sécurisé
    } else {
        throw $this->createAccessDeniedException('Token CSRF invalide');
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <div class="warning-section">
                        <h4 class="text-purple">⚠️ Ne jamais désactiver la protection CSRF sans raison valable</h4>
                        <p class="warning-text">
                            Désactiver <code>csrf_protection</code> expose votre formulaire aux attaques CSRF.
                            Ne le faites que pour des API publiques ou des formulaires GET sans effet de bord.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Prévention XSS (Cross-Site Scripting) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prévention XSS avec Twig</h2>

                <div class="textExemple">
                    <p>
                        Les attaques XSS permettent à un attaquant d'injecter du code JavaScript malveillant dans vos pages.
                        Twig protège automatiquement vos données grâce à l'<strong>échappement automatique</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# Échappement automatique : tous les caractères spéciaux sont convertis #}
&lt;!-- Si le champ 'titre' contient &lt;script&gt;alert('XSS')&lt;/script&gt; --&gt;
{{ form_widget(form.titre) }}
{{ form.titre.vars.value }} {# sera affiché en texte brut, sans exécution #}

{# Pour afficher du HTML sécurisé (ex: texte enrichi), utilisez le filtre raw AVEC précaution #}
{{ article.contenu|raw }}

{# Alternative plus sûre : nettoyer le HTML avec un outil comme HTMLPurifier #}
{# composer require ezyang/htmlpurifier-bundle #}
{{ article.contenu|purify }}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques contre les XSS</h3>
                    <ul>
                        <li><strong>Ne jamais utiliser <code>|raw</code> sur des données utilisateur non filtrées</strong></li>
                        <li>Utiliser <code>striptags</code> si vous voulez supprimer tout HTML : <code>{{ comment|striptags }}</code></li>
                        <li>Valider et nettoyer les entrées utilisateur avec les contraintes de validation</li>
                        <li>Définir l'en-tête <code>Content-Security-Policy</code> pour limiter les scripts exécutables</li>
                    </ul>
                </div>
            </section>

            <!-- Validation des données : première ligne de défense -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Validation des données : barrière contre les injections</h2>

                <div class="textExemple">
                    <p>
                        La validation des données est cruciale pour empêcher l'injection de contenu malveillant.
                        Symfony Validator filtre les données <strong>avant même qu'elles n'atteignent la base de données</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Product.php
use Symfony\Component\Validator\Constraints as Assert;

class Product
{
    #[ORM\Column(length: 255)]
    #[Assert\NotBlank]
    #[Assert\Length(min: 3, max: 255)]
    #[Assert\Regex(
        pattern: '/^[a-zA-Z0-9\s\-]+$/',
        message: 'Le nom ne doit contenir que des lettres, chiffres, espaces ou tirets'
    )]
    private ?string $name = null;

    #[ORM\Column(type: 'text')]
    #[Assert\NotBlank]
    #[Assert\NoSuspiciousCharacters] // Empêche les caractères invisibles ou homographes
    private ?string $description = null;

    #[ORM\Column(type: 'float')]
    #[Assert\Positive]
    #[Assert\LessThan(10000)]
    private ?float $price = null;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes de validation spécifiques à la sécurité</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints as Assert;

// Empêche les caractères suspects (bi-directionnels, homographes)
#[Assert\NoSuspiciousCharacters]

// Vérifie qu'une valeur ne contient pas de balises HTML
#[Assert\NotCompromisedPassword] // Pour les mots de passe (vérifie si leak)

// Validation d'email + DNS (vérifie que le domaine existe)
#[Assert\Email(mode: 'strict')]

// Contrôle de type strict
#[Assert\Type(type: 'integer')]

// Évite les injections SQL via des caractères spéciaux (complément)
#[Assert\Regex(pattern: '/[\'";\\\\-]/', match: false, message: 'Caractère interdit')]</code></pre>
                    </div>
                </div>
            </section>

            <!-- Doctrine : prévention des injections SQL -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Doctrine : prévention des injections SQL</h2>

                <div class="textExemple">
                    <p>
                        Doctrine utilise les <strong>requêtes préparées</strong> (paramètres liés) qui neutralisent automatiquement
                        les tentatives d'injection SQL. Cependant, certaines pratiques sont à éviter.
                    </p>
                    <div class="code-comparison">
                        <div>
                            <h5>❌ Vulnérable (concaténation)</h5>
                            <div class="code-example">
                                <pre v-pre><code class="language-php">// À ne JAMAIS faire
$search = $_GET['search'];
$query = $em->createQuery(
    "SELECT p FROM Product p WHERE p.name LIKE '%$search%'"
);
// Injection possible : ' OR 1=1 --</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>✅ Sécurisé (paramètres liés)</h5>
                            <div class="code-example">
                                <pre v-pre><code class="language-php">$search = $request->query->get('search');
$query = $em->createQuery(
    'SELECT p FROM Product p WHERE p.name LIKE :search'
)->setParameter('search', '%' . $search . '%');
// Doctrine échappe automatiquement $search</code></pre>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">EntityType : sécuriser les relations Doctrine</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Bridge\Doctrine\Form\Type\EntityType;

$builder->add('category', EntityType::class, [
    'class' => Category::class,
    'choice_label' => 'name',
    // ⚠️ Toujours filtrer les résultats pour éviter les fuites de données
    'query_builder' => function (EntityRepository $er) {
        return $er->createQueryBuilder('c')
            ->andWhere('c.isActive = :active')
            ->setParameter('active', true);
    },
]);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Mass Assignment Protection -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Protection contre le Mass Assignment</h2>

                <div class="textExemple">
                    <p>
                        Le <strong>mass assignment</strong> se produit quand un attaquant soumet des champs non autorisés
                        (ex: <code>isAdmin</code>, <code>role</code>) pour modifier des propriétés protégées.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/User.php
class User
{
    #[ORM\Column]
    private bool $isAdmin = false; // Champ sensible

    // ✅ Dans votre FormType, n'incluez PAS ce champ
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('username', TextType::class)
            ->add('email', EmailType::class);
        // N'ajoutez PAS 'isAdmin' ici !
    }
}

// ❌ Mauvais : si vous utilisez $form->submit($request->request->all())
// sans définir explicitement les champs, un attaquant pourrait ajouter 'isAdmin'

// ✅ Bon : le FormType définit explicitement les champs autorisés
// Tout champ supplémentaire est ignoré par défaut</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <div class="warning-section">
                        <h4 class="text-purple">⚠️ Astuce de sécurité : désactiver les champs non mappés</h4>
                        <pre v-pre><code class="language-php">// Dans config/packages/framework.yaml
framework:
    form:
        legacy_error_messages: false
        # Empêche la soumission de champs non déclarés
        # (déclenche une exception en prod si extra_fields)
    validation:
        auto_mapping:
            App\Entity\: []</code></pre>
                        <p class="warning-text">
                            Utilisez <code>allow_extra_fields: false</code> (par défaut) dans vos FormTypes
                            pour rejeter automatiquement les champs inattendus.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Sécurité des fichiers uploadés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Sécuriser l'upload de fichiers</h2>

                <div class="textExemple">
                    <p>
                        L'upload de fichiers est une source fréquente de vulnérabilités (exécution de scripts, déni de service).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans votre FormType
use Symfony\Component\Form\Extension\Core\Type\FileType;
use Symfony\Component\Validator\Constraints\File;

$builder->add('document', FileType::class, [
    'label' => 'Document (PDF, DOCX)',
    'mapped' => false,
    'constraints' => [
        new File([
            'maxSize' => '5M',
            'mimeTypes' => [
                'application/pdf',
                'application/msword',
                'application/vnd.openxmlformats-officedocument.wordprocessingml.document',
            ],
            'mimeTypesMessage' => 'Veuillez uploader un document valide (PDF, DOC)',
            'disallowEmptyMessage' => 'Le fichier ne peut pas être vide',
        ])
    ],
]);

// Dans le controller
if ($form->isSubmitted() && $form->isValid()) {
    $file = $form->get('document')->getData();
    
    if ($file) {
        // 🔒 1. Générer un nom unique et aléatoire (pas de nom utilisateur)
        $newFilename = bin2hex(random_bytes(16)) . '.' . $file->guessExtension();
        
        // 🔒 2. Stocker hors du webroot ou avec .htaccess bloquant l'exécution
        $uploadDir = $this->getParameter('kernel.project_dir') . '/var/uploads/';
        $file->move($uploadDir, $newFilename);
        
        // 🔒 3. Ne jamais exécuter le fichier, ne pas stocker dans un dossier accessible publiquement
        // 🔒 4. Scanner antivirus (optionnel avec ClamAV)
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Bonnes pratiques upload</h3>
                    <ul>
                        <li>Limiter la taille maximale (client + serveur)</li>
                        <li>Vérifier le type MIME réel (pas seulement l'extension)</li>
                        <li>Renommer le fichier avec un nom aléatoire</li>
                        <li>Stocker les fichiers en dehors du répertoire public</li>
                        <li>Désactiver l'exécution de scripts dans le dossier d'upload (.htaccess)</li>
                    </ul>
                </div>
            </section>

            <!-- Authentification et autorisation dans les formulaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Contrôle d'accès : Voter & Security</h2>

                <div class="textExemple">
                    <p>
                        Même si un formulaire est affiché, l'utilisateur doit avoir les droits d'exécuter l'action.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans votre controller
use Symfony\Component\Security\Http\Attribute\IsGranted;

#[Route('/article/{id}/edit', name: 'article_edit')]
#[IsGranted('EDIT', subject: 'article')] // Vérifie l'autorisation avant d'afficher le formulaire
public function edit(Article $article, Request $request): Response
{
    // L'utilisateur n'arrive ici que s'il a le droit d'éditer
    $form = $this->createForm(ArticleType::class, $article);
    // ...
}

// Voter personnalisé pour des règles métier complexes
// src/Security/ArticleVoter.php
class ArticleVoter extends Voter
{
    protected function supports(string $attribute, $subject): bool
    {
        return $attribute === 'EDIT' && $subject instanceof Article;
    }
    
    protected function voteOnAttribute(string $attribute, $subject, TokenInterface $token): bool
    {
        $user = $token->getUser();
        if (!$user instanceof User) return false;
        
        /** @var Article $article */
        $article = $subject;
        
        // Seul l'auteur peut modifier son article
        return $user === $article->getAuthor();
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices : Mettez en pratique la sécurité</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Sécuriser un formulaire de contact</h3>
                    <p>Vous devez ajouter les protections suivantes à un formulaire de contact existant :</p>
                    <ul>
                        <li>Activer la protection CSRF (vérifier qu'elle est active)</li>
                        <li>Ajouter des contraintes de validation anti-XSS (Regex, NoSuspiciousCharacters)</li>
                        <li>Empêcher l'injection SQL dans le message (utiliser les paramètres liés en Doctrine)</li>
                        <li>Protéger le champ email contre les attaques par header injection</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Form/ContactType.php
class ContactType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('name', TextType::class, [
                'constraints' => [
                    new Assert\NotBlank(),
                    new Assert\Length(['min' => 2, 'max' => 100]),
                    new Assert\Regex(['pattern' => '/^[a-zA-Z\s\-]+$/']),
                ]
            ])
            ->add('email', EmailType::class, [
                'constraints' => [
                    new Assert\NotBlank(),
                    new Assert\Email(['mode' => 'html5']), // Protection injection email
                ]
            ])
            ->add('message', TextareaType::class, [
                'constraints' => [
                    new Assert\NotBlank(),
                    new Assert\NoSuspiciousCharacters(),
                    new Assert\Length(['max' => 2000]),
                ]
            ]);
    }
    
    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'csrf_protection' => true, // Vérifier que c'est true
        ]);
    }
}

// Dans le controller
$message = $form->get('message')->getData();
// Requête Doctrine sécurisée
$qb = $em->createQueryBuilder();
$qb->select('c')
   ->from(Contact::class, 'c')
   ->where($qb->expr()->like('c.message', ':msg'))
   ->setParameter('msg', '%' . addcslashes($message, '%_') . '%');</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Formulaire d'upload sécurisé</h3>
                    <p>Créez un formulaire d'upload d'avatar avec les règles suivantes :</p>
                    <ul>
                        <li>Types autorisés : JPG, PNG, WebP (max 2 Mo)</li>
                        <li>Renommer le fichier avec un UUID</li>
                        <li>Stocker dans un répertoire non accessible directement</li>
                        <li>Redimensionner l'image pour éviter les bombes de décompression</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Form/AvatarType.php
use Symfony\Component\Form\Extension\Core\Type\FileType;
use Symfony\Component\Validator\Constraints\File;

$builder->add('avatar', FileType::class, [
    'constraints' => [
        new File([
            'maxSize' => '2M',
            'mimeTypes' => ['image/jpeg', 'image/png', 'image/webp'],
            'mimeTypesMessage' => 'Formats autorisés : JPG, PNG, WebP',
        ])
    ],
]);

// Dans le controller
if ($form->isSubmitted() && $form->isValid()) {
    $file = $form->get('avatar')->getData();
    if ($file) {
        // Génération nom sécurisé
        $newName = uniqid('avatar_', true) . '.' . $file->guessExtension();
        
        // Redimensionnement avec intervention/image
        $image = Image::read($file->getPathname());
        $image->cover(200, 200);
        $image->save($this->getParameter('avatars_dir') . '/' . $newName);
        
        // Stockage en base du nom (pas du chemin complet)
        $user->setAvatarFilename($newName);
    }
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques finales -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récapitulatif des bonnes pratiques de sécurité</h2>

                <div class="textExemple">
                    <h3 class="text-purple">✅ À faire systématiquement</h3>
                    <ul>
                        <li>Laisser la protection CSRF activée sur tous les formulaires modifiant des données</li>
                        <li>Définir des contraintes de validation strictes (type, longueur, format)</li>
                        <li>Utiliser Twig pour l'échappement automatique (ne pas utiliser <code>|raw</code> sans nettoyage)</li>
                        <li>Paramétrer les requêtes Doctrine avec <code>setParameter()</code> ou QueryBuilder</li>
                        <li>Ne mapper que les champs nécessaires dans le FormType</li>
                        <li>Vérifier les droits utilisateur avec Voter ou <code>#[IsGranted]</code></li>
                        <li>Stocker les fichiers uploadés avec un nom aléatoire, hors webroot</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">❌ À éviter impérativement</h3>
                    <ul>
                        <li>Désactiver <code>csrf_protection</code> sans raison valable</li>
                        <li>Concaténer des variables utilisateur dans une requête SQL ou DQL</li>
                        <li>Faire confiance aux données <code>$_GET</code>/<code>$_POST</code> brutes</li>
                        <li>Inclure des champs sensibles (<code>isAdmin</code>, <code>roles</code>) dans un FormType</li>
                        <li>Accepter tous les types MIME en upload</li>
                        <li>Ignorer les erreurs de validation</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Outils de sécurité complémentaires</h3>
                    <ul>
                        <li><strong>symfony/security-bundle</strong> : authentification, autorisation</li>
                        <li><strong>symfony/validator</strong> : validation des entités et formulaires</li>
                        <li><strong>symfony/expression-language</strong> : règles d'accès complexes</li>
                        <li><strong>friendsofsymfony/elastica-bundle</strong> : recherche sécurisée</li>
                        <li><strong>nelmio/security-bundle</strong> : analyse des vulnérabilités</li>
                        <li><strong>sentry/sentry-symfony</strong> : monitoring des erreurs de sécurité</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        La sécurité des formulaires Symfony repose sur une combinaison de protections intégrées (CSRF, échappement Twig, requêtes préparées)
                        et de bonnes pratiques de validation et de contrôle d'accès. En respectant ces principes, vous protégez votre application
                        contre les attaques les plus courantes tout en offrant une expérience utilisateur fluide.
                    </p>
                    <p>
                        <strong>Règle d'or</strong> : Ne faites jamais confiance aux données utilisateur. Validez, filtrez, échappez, et autorisez.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyFormSecurityLesson',

    mounted() {
        // Chargement de highlight.js + thème VS Code Dark
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
                    // Langages PHP et Twig
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const twigScript = document.createElement('script');
                        twigScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/twig.min.js';
                        twigScript.onload = resolve;
                        document.head.appendChild(twigScript);
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

.border-purple {
    border: 2px solid #e0d6ff;
    transition: all 0.3s ease;
}

.text-purple { color: #6A3093 !important; }
.text-white  { color: white !important; }

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

.code-example {
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

.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
}

.warning-text {
    color: #d63031;
    font-weight: bold;
    margin-top: 0.5rem;
}

.success-text {
    color: #00b894;
    font-weight: bold;
    margin-top: 0.5rem;
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
    .lesson-container  { padding: 1rem; }
    .lesson-header     { padding: 2rem 1rem; }
    .lesson-header h1  { font-size: 2rem; }
    .lesson-section    { padding: 1.5rem; }
    .code-comparison   { grid-template-columns: 1fr; gap: 1rem; }
    pre                { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
    pre               { padding: 0.75rem !important; font-size: 0.8rem; }
    .lesson-container { padding: 0.5rem; }
    .lesson-section   { padding: 1rem; }
    .lesson-header    { padding: 1.5rem 1rem; }
    .lesson-header h1 { font-size: 1.75rem; }
}

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}
</style>