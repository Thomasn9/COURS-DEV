<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Validation Symfony : Les Assert</h1>
                <p class="lesson-meta text-white">Symfony • Validator • Contraintes • Attributs PHP • Bonnes pratiques</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à la validation Symfony</h2>
                <p class="textExemple">
                    Le composant <strong>Validator</strong> de Symfony permet de s'assurer que les données respectent
                    un ensemble de règles métier avant de les utiliser (persistance, envoi d'email, traitement, etc.).
                    Les contraintes de validation sont appelées "assertions" car elles "affirment" qu'une propriété doit
                    satisfaire une condition.
                </p>
                <p class="textExemple">
                    Depuis Symfony 5.2, les attributs PHP (annotations natives) sont la méthode privilégiée pour déclarer
                    les contraintes directement dans les classes (entités, DTO, formulaires). Le Validator peut être utilisé
                    de manière autonome, sans formulaire, pour valider n'importe quel objet.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Installer le composant Validator (si ce n'est pas déjà fait)
composer require symfony/validator</code></pre>
                </div>
            </section>

            <!-- Concepts fondamentaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Concepts fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Le service Validator</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans un contrôleur Symfony
use Symfony\Component\Validator\Validator\ValidatorInterface;

#[Route('/api/user')]
public function create(Request $request, ValidatorInterface $validator): Response
{
    $user = new User();
    $user->setEmail($request->get('email'));
    $user->setAge($request->get('age'));

    $errors = $validator->validate($user);

    if (count($errors) > 0) {
        // Il y a des violations
        return $this->json($errors, 400);
    }

    // Données valides
    // ...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Violations (ConstraintViolation)</h3>
                    <p>
                        Lorsqu'une contrainte n'est pas respectée, le Validator retourne une collection d'objets
                        <code>ConstraintViolation</code>. Chaque violation contient :
                    </p>
                    <ul>
                        <li>Le message d'erreur</li>
                        <li>Le chemin de la propriété (ex: <code>email</code>)</li>
                        <li>La valeur invalide</li>
                        <li>Le code de la contrainte</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Afficher toutes les erreurs
foreach ($errors as $error) {
    echo $error->getPropertyPath() . ': ' . $error->getMessage();
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Syntaxe des attributs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe des attributs de validation</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Import des contraintes</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints as Assert;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contrainte simple sur une propriété</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Assert\NotBlank(message: 'L\'email ne peut pas être vide.')]
private ?string $email = null;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes multiples</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Assert\NotBlank]
#[Assert\Email]
#[Assert\Length(max: 180)]
private ?string $email = null;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contrainte avec paramètres (ex: Length)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Assert\Length(
    min: 2,
    max: 50,
    minMessage: 'Le prénom doit comporter au moins {{ limit }} caractères.',
    maxMessage: 'Le prénom ne peut pas dépasser {{ limit }} caractères.'
)]
private ?string $firstName = null;</code></pre>
                    </div>
                    <p>Les placeholders <code>{{ value }}</code>, <code>{{ limit }}</code> sont automatiquement remplacés.</p>
                </div>
            </section>

            <!-- Contraintes les plus utiles -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Contraintes essentielles</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes de base</h3>
                    <table class="lesson-table">
                        <thead><tr><th>Attribut</th><th>Description</th></tr></thead>
                        <tbody>
                            <tr><td><code>#[Assert\NotBlank]</code></td><td>La valeur ne doit pas être vide (null, chaîne vide, tableau vide).</td></tr>
                            <tr><td><code>#[Assert\NotNull]</code></td><td>La valeur ne doit pas être null (mais peut être une chaîne vide).</td></tr>
                            <tr><td><code>#[Assert\IsTrue]</code></td><td>La valeur doit être true (ex: case à cocher "J'accepte les CGU").</td></tr>
                            <tr><td><code>#[Assert\IsFalse]</code></td><td>La valeur doit être false.</td></tr>
                        </tbody>
                    </table>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes de chaînes et nombres</h3>
                    <table class="lesson-table">
                        <thead><tr><th>Attribut</th><th>Description</th></tr></thead>
                        <tbody>
                            <tr><td><code>#[Assert\Length(min, max)]</code></td><td>Longueur d'une chaîne (ou nombre d'éléments).</td></tr>
                            <tr><td><code>#[Assert\Email]</code></td><td>Format d'email valide (plusieurs modes).</td></tr>
                            <tr><td><code>#[Assert\Url]</code></td><td>Format d'URL valide.</td></tr>
                            <tr><td><code>#[Assert\Regex(pattern)]</code></td><td>Expression régulière.</td></tr>
                            <tr><td><code>#[Assert\Range(min, max)]</code></td><td>Valeur numérique entre min et max.</td></tr>
                            <tr><td><code>#[Assert\Positive]</code></td><td>Nombre strictement positif.</td></tr>
                            <tr><td><code>#[Assert\PositiveOrZero]</code></td><td>Nombre positif ou zéro.</td></tr>
                            <tr><td><code>#[Assert\Negative]</code></td><td>Nombre strictement négatif.</td></tr>
                        </tbody>
                    </table>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes de dates</h3>
                    <table class="lesson-table">
                        <thead><tr><th>Attribut</th><th>Description</th></tr></thead>
                        <tbody>
                            <tr><td><code>#[Assert\Date]</code></td><td>Chaîne au format YYYY-MM-DD valide.</td></tr>
                            <tr><td><code>#[Assert\DateTime]</code></td><td>Chaîne au format YYYY-MM-DD HH:MM:SS valide.</td></tr>
                            <tr><td><code>#[Assert\LessThan(value)]</code></td><td>Valeur inférieure à une date/heure donnée.</td></tr>
                            <tr><td><code>#[Assert\LessThanOrEqual]</code></td><td>Inférieure ou égale.</td></tr>
                            <tr><td><code>#[Assert\GreaterThan(value)]</code></td><td>Supérieure à une date/heure donnée.</td></tr>
                            <tr><td><code>#[Assert\GreaterThanOrEqual]</code></td><td>Supérieure ou égale.</td></tr>
                        </tbody>
                    </table>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes de choix et collection</h3>
                    <table class="lesson-table">
                        <thead><tr><th>Attribut</th><th>Description</th></tr></thead>
                        <tbody>
                            <tr><td><code>#[Assert\Choice(choices: [ ... ])]</code></td><td>La valeur doit appartenir à une liste.</td></tr>
                            <tr><td><code>#[Assert\Count(min, max)]</code></td><td>Nombre d'éléments dans un tableau ou une collection.</td></tr>
                            <tr><td><code>#[Assert\Unique]</code></td><td>Tous les éléments d'une collection sont uniques.</td></tr>
                        </tbody>
                    </table>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes de fichier</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Assert\File(
    maxSize: '2M',
    mimeTypes: ['image/jpeg', 'image/png', 'application/pdf'],
    maxSizeMessage: 'Le fichier est trop gros ({{ size }} {{ suffix }}). Maximum {{ limit }} {{ suffix }}',
    mimeTypesMessage: 'Type de fichier non autorisé ({{ type }}). Formats autorisés : {{ types }}'
)]
private $document;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Contraintes avancées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Contraintes avancées</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Validation croisée : Expression</h3>
                    <p>Valider une condition impliquant plusieurs propriétés.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints as Assert;

class User
{
    #[Assert\NotBlank]
    private string $password;

    #[Assert\Expression(
        'this.getPassword() == this.getConfirmPassword()',
        message: 'Les mots de passe ne correspondent pas.'
    )]
    private string $confirmPassword;

    // getters/setters...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Validation au niveau de la classe (Callback)</h3>
                    <p>Permet d'écrire une méthode de validation personnalisée.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints as Assert;
use Symfony\Component\Validator\Context\ExecutionContextInterface;

#[Assert\Callback]
public function validate(ExecutionContextInterface $context): void
{
    if ($this->startDate > $this->endDate) {
        $context->buildViolation('La date de début doit être antérieure à la date de fin.')
            ->atPath('startDate')
            ->addViolation();
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer une contrainte personnalisée</h3>
                    <p>Pour des règles métier complexes non couvertes par les contraintes natives.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Validator/Constraints/ContainsAlpha.php
namespace App\Validator\Constraints;

use Symfony\Component\Validator\Constraint;

#[Attribute]
class ContainsAlpha extends Constraint
{
    public string $message = 'La chaîne "{{ value }}" doit contenir au moins une lettre.';
}

// src/Validator/Constraints/ContainsAlphaValidator.php
namespace App\Validator\Constraints;

use Symfony\Component\Validator\Constraint;
use Symfony\Component\Validator\ConstraintValidator;

class ContainsAlphaValidator extends ConstraintValidator
{
    public function validate($value, Constraint $constraint): void
    {
        if (!preg_match('/[a-zA-Z]/', $value)) {
            $this->context->buildViolation($constraint->message)
                ->setParameter('{{ value }}', $value)
                ->addViolation();
        }
    }
}

// Utilisation dans une entité
use App\Validator\Constraints as AppAssert;

#[AppAssert\ContainsAlpha]
private string $title;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Groupes de validation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Groupes de validation</h2>
                <p class="textExemple">
                    Les groupes permettent d'appliquer différentes contraintes selon le contexte (création, modification, recherche, etc.).
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Déclaration des groupes</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints as Assert;

class User
{
    #[Assert\NotBlank(groups: ['registration', 'profile'])]
    #[Assert\Length(min: 2, groups: ['registration'])]
    private string $username;

    #[Assert\NotBlank(groups: ['registration'])]
    #[Assert\Email(groups: ['registration', 'contact'])]
    private string $email;

    #[Assert\NotBlank(groups: ['password_change'])]
    #[Assert\Length(min: 8, groups: ['password_change'])]
    private string $password;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Validation avec groupes spécifiques</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Valider uniquement les contraintes du groupe 'registration'
$errors = $validator->validate($user, null, ['registration']);

// Valider plusieurs groupes
$errors = $validator->validate($user, null, ['registration', 'contact']);

// Valider tous les groupes sauf un (avec Default)
$errors = $validator->validate($user, null, ['Default', 'profile']);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Groupe par défaut (Default)</h3>
                    <p>
                        Si aucun groupe n'est spécifié, le Validator utilise le groupe <code>Default</code>.
                        Une contrainte sans groupe appartient automatiquement au groupe <code>Default</code>.
                    </p>
                </div>
            </section>

            <!-- Validation séquentielle -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Validation séquentielle (Sequential)</h2>
                <p class="textExemple">
                    Permet d'arrêter la validation dès qu'une contrainte échoue. Utile pour éviter des erreurs
                    cascades ou pour valider des données complexes étape par étape.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints\Sequential;

#[Sequential([
    new Assert\NotBlank(),
    new Assert\Length(min: 5),
    new Assert\Regex('/^[a-z]+$/')
])]
private string $slug;</code></pre>
                </div>
            </section>

            <!-- Validation dans les formulaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Intégration avec les formulaires Symfony</h2>
                <p class="textExemple">
                    Lorsqu'un formulaire Symfony est lié à une entité (via <code>data_class</code>), les contraintes
                    de l'entité sont automatiquement appliquées. Vous pouvez aussi ajouter des contraintes spécifiques
                    au formulaire dans le FormType.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes dans le FormType (option)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">$builder->add('email', EmailType::class, [
    'constraints' => [
        new Assert\NotBlank(['message' => 'L\'email est requis.']),
        new Assert\Email(),
    ],
]);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Afficher les erreurs dans Twig</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{{ form_errors(form.email) }}

{# Affichage personnalisé #}
{% for error in form.email.vars.errors %}
    <div class="alert alert-danger">{{ error.message }}</div>
{% endfor %}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul class="textExemple">
                    <li><strong>Placer les contraintes sur l'entité plutôt que dans le formulaire</strong> : cela garantit que la validation s'applique partout (API, CLI, formulaire).</li>
                    <li><strong>Utiliser des messages d'erreur explicites et adaptés à l'utilisateur</strong> : évitez les messages techniques.</li>
                    <li><strong>Ne jamais faire confiance à la validation côté client</strong> : la validation serveur est obligatoire pour la sécurité.</li>
                    <li><strong>Découper en groupes de validation</strong> pour les entités utilisées dans différents contextes.</li>
                    <li><strong>Pour les DTO (Data Transfer Object)</strong> : les contraintes se placent directement sur les propriétés du DTO.</li>
                    <li><strong>Utiliser <code>@Assert\Valid</code></strong> pour valider les objets imbriqués (relations).</li>
                </ul>
            </section>

            <!-- Exemple complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple complet : Entité User avec contraintes riches</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/Entity/User.php
namespace App\Entity;

use Symfony\Component\Validator\Constraints as Assert;
use Symfony\Bridge\Doctrine\Validator\Constraints\UniqueEntity;

#[UniqueEntity(fields: ['email'], message: 'Cet email est déjà utilisé.')]
class User
{
    #[Assert\NotBlank]
    #[Assert\Length(min: 2, max: 50)]
    private string $firstName;

    #[Assert\NotBlank]
    #[Assert\Length(min: 2, max: 50)]
    private string $lastName;

    #[Assert\NotBlank]
    #[Assert\Email]
    #[Assert\Length(max: 180)]
    private string $email;

    #[Assert\NotBlank(groups: ['registration'])]
    #[Assert\Length(min: 8, groups: ['registration'])]
    #[Assert\Regex(
        pattern: '/^(?=.*[A-Z])(?=.*[a-z])(?=.*\d).+$/',
        message: 'Le mot de passe doit contenir au moins une majuscule, une minuscule et un chiffre.',
        groups: ['registration']
    )]
    private string $plainPassword;

    #[Assert\Range(min: 18, max: 120)]
    private int $age;

    #[Assert\Date]
    private ?string $birthDate = null;

    #[Assert\Country]
    private ?string $country = null;

    #[Assert\CardScheme(schemes: ['VISA', 'MASTERCARD'])]
    private ?string $creditCardNumber = null;

    // getters/setters...
}</code></pre>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Validation d'un DTO de contact</h3>
                    <p>Créez un DTO <code>ContactDTO</code> avec les propriétés suivantes et les contraintes associées :</p>
                    <ul>
                        <li><code>name</code> : obligatoire, min 3 caractères, max 100</li>
                        <li><code>email</code> : obligatoire, email valide</li>
                        <li><code>message</code> : obligatoire, min 10 caractères</li>
                        <li><code>priority</code> : doit être l'une des valeurs ['low', 'normal', 'high']</li>
                        <li><code>sendCopy</code> : booléen (facultatif, par défaut false)</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">use Symfony\Component\Validator\Constraints as Assert;

class ContactDTO
{
    #[Assert\NotBlank]
    #[Assert\Length(min: 3, max: 100)]
    public string $name;

    #[Assert\NotBlank]
    #[Assert\Email]
    public string $email;

    #[Assert\NotBlank]
    #[Assert\Length(min: 10)]
    public string $message;

    #[Assert\Choice(choices: ['low', 'normal', 'high'])]
    public string $priority = 'normal';

    #[Assert\IsTrue(message: 'Vous devez accepter les CGU')]
    public bool $acceptTerms = false;
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Validation avec groupe "password_change"</h3>
                    <p>Dans une entité User, assurez-vous que le champ <code>newPassword</code> n'est validé (non vide, min 8 caractères) que lorsque le groupe "password_change" est utilisé. Le champ <code>email</code> doit toujours être validé.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">class User
{
    #[Assert\NotBlank]
    #[Assert\Email]
    private string $email;

    #[Assert\NotBlank(groups: ['password_change'])]
    #[Assert\Length(min: 8, groups: ['password_change'])]
    private string $newPassword;

    // getters/setters...
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Contrainte personnalisée "FrenchPhoneNumber"</h3>
                    <p>Créez une contrainte qui valide un numéro de téléphone français (10 chiffres, commençant par 0 ou +33).</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Validator/Constraints/FrenchPhoneNumber.php
namespace App\Validator\Constraints;

use Symfony\Component\Validator\Constraint;

#[Attribute]
class FrenchPhoneNumber extends Constraint
{
    public string $message = 'Le numéro "{{ value }}" n\'est pas un numéro français valide.';
}

// src/Validator/Constraints/FrenchPhoneNumberValidator.php
namespace App\Validator\Constraints;

use Symfony\Component\Validator\Constraint;
use Symfony\Component\Validator\ConstraintValidator;

class FrenchPhoneNumberValidator extends ConstraintValidator
{
    public function validate($value, Constraint $constraint): void
    {
        if (!preg_match('/^(0|\+33)[1-9][0-9]{8}$/', $value)) {
            $this->context->buildViolation($constraint->message)
                ->setParameter('{{ value }}', $value)
                ->addViolation();
        }
    }
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Le composant Validator de Symfony est extrêmement puissant et flexible. En utilisant les attributs PHP,
                    vous rendez la validation déclarative, lisible et maintenable. N'oubliez pas :
                </p>
                <ul class="textExemple">
                    <li>✅ Toujours valider côté serveur, même si vous validez côté client.</li>
                    <li>✅ Utiliser les groupes de validation pour distinguer les contextes.</li>
                    <li>✅ Personnaliser les messages d'erreur pour une meilleure UX.</li>
                    <li>✅ Créer des contraintes personnalisées pour les règles métier complexes.</li>
                </ul>
                <p class="textExemple">
                    Prochaine étape : découvrir les <strong>Event Listeners</strong> de validation pour modifier dynamiquement
                    les contraintes avant validation.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyAssertLesson',

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
                    const languages = ['php', 'bash', 'twig', 'sql', 'plaintext'];
                    let loaded = 0;
                    languages.forEach(lang => {
                        const langScript = document.createElement('script');
                        langScript.src = `https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/${lang}.min.js`;
                        langScript.onload = () => {
                            loaded++;
                            if (loaded === languages.length) resolve();
                        };
                        document.head.appendChild(langScript);
                    });
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
/* Mêmes styles que la leçon Symfony (copie exacte depuis votre template) */
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
.border-purple { border: 2px solid #e0d6ff; transition: all 0.3s ease; }
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

.lesson-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.lesson-table th, .lesson-table td {
    border: 1px solid #ddd;
    padding: 10px 12px;
    text-align: left;
    vertical-align: top;
}

.lesson-table th {
    background: #6A3093;
    color: white;
    font-weight: 600;
}

.lesson-table tr:nth-child(even) {
    background-color: #f9f9f9;
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
    pre                { padding: 1rem !important; font-size: 0.85rem; }
    .lesson-table th, .lesson-table td { padding: 6px 8px; }
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