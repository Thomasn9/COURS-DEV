<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">DTO (Data Transfer Objects) dans Symfony</h1>
                <p class="lesson-meta text-white">Symfony • DTO • Transfert de données • Validation • Mapping</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'un DTO ?</h2>
                <p class="textExemple">
                    Un <strong>Data Transfer Object (DTO)</strong> est un objet simple, souvent anémique, dont l'unique but est de <strong>transporter des données</strong> entre différentes couches d'une application. Contrairement aux entités (qui contiennent de la logique métier et un identifiant), un DTO ne possède généralement que des propriétés publiques (ou privées avec getters/setters) et aucune méthode métier.
                </p>
                <p class="textExemple">
                    Dans le cadre de Symfony, les DTO sont très utilisés pour : 
                    <ul>
                        <li>Découpler les formulaires des entités Doctrine</li>
                        <li>Transférer des données entre un contrôleur et un service</li>
                        <li>Structurer les réponses d'une API (sérialisation)</li>
                        <li>Valider des données sans les mapper directement à une entité</li>
                    </ul>
                </p>
            </section>

            <!-- Pourquoi utiliser un DTO -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi utiliser un DTO plutôt qu'une entité ?</h2>
                <div class="code-comparison">
                    <div>
                        <h3 class="text-purple">Sans DTO (problèmes courants)</h3>
                        <ul>
                            <li>L'entité est liée à la base de données via Doctrine.</li>
                            <li>Les champs du formulaire correspondent directement aux colonnes.</li>
                            <li>Difficulté à gérer des champs virtuels (mot de passe, confirmation).</li>
                            <li>Problèmes de validation (contraintes métier vs formulaire).</li>
                            <li>Risque de modification accidentelle de l'entité.</li>
                        </ul>
                    </div>
                    <div>
                        <h3 class="text-purple">Avec DTO (avantages)</h3>
                        <ul>
                            <li>Séparation claire entre la couche présentation et la couche métier.</li>
                            <li>Champs virtuels et validation indépendante de l'entité.</li>
                            <li>Facilité à combiner des données provenant de plusieurs sources.</li>
                            <li>Sécurité : on ne mappe que les champs souhaités.</li>
                            <li>Meilleure testabilité et maintenabilité.</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- DTO simple -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple basique : DTO de création d'article</h2>
                <div class="textExemple">
                    <p>Imaginons une entité <code>Article</code> qui possède des champs en base. Pour créer un article, nous voulons un formulaire avec un champ <code>title</code>, <code>content</code> et une case à cocher "publier immédiatement". Ce dernier n'existe pas dans l'entité : c'est un parfait cas d'usage pour un DTO.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/DTO/CreateArticleDTO.php
namespace App\DTO;

use Symfony\Component\Validator\Constraints as Assert;

class CreateArticleDTO
{
    #[Assert\NotBlank]
    #[Assert\Length(min: 5, max: 255)]
    public string $title;

    #[Assert\NotBlank]
    #[Assert\Length(min: 20)]
    public string $content;

    // Champ virtuel : ne sera pas mappé en base
    public bool $publishImmediately = false;

    public function __construct(string $title = '', string $content = '')
    {
        $this->title = $title;
        $this->content = $content;
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- DTO avec validation avancée -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Validation des DTO</h2>
                <p class="textExemple">
                    Les DTO bénéficient du système de validation de Symfony exactement comme les entités. On peut utiliser des attributs, des contraintes personnalisées et la validation de groupe.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/DTO/UserRegistrationDTO.php
namespace App\DTO;

use Symfony\Component\Validator\Constraints as Assert;
use App\Validator\Constraints\UniqueEmail;

class UserRegistrationDTO
{
    #[Assert\NotBlank]
    #[Assert\Email]
    #[UniqueEmail] // contrainte personnalisée
    public string $email;

    #[Assert\NotBlank]
    #[Assert\Length(min: 8, minMessage: 'Le mot de passe doit faire au moins 8 caractères')]
    #[Assert\Regex(pattern: '/[0-9]/', message: 'Le mot de passe doit contenir au moins un chiffre')]
    public string $password;

    #[Assert\EqualTo(propertyPath: 'password', message: 'Les mots de passe ne correspondent pas')]
    public string $confirmPassword;

    #[Assert\IsTrue(message: 'Vous devez accepter les conditions')]
    public bool $acceptTerms = false;
}</code></pre>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Validation dans le contrôleur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Validator\Validator\ValidatorInterface;

#[Route('/register', name: 'register', methods: ['POST'])]
public function register(Request $request, ValidatorInterface $validator): Response
{
    $dto = new UserRegistrationDTO();
    $dto->email = $request->get('email');
    $dto->password = $request->get('password');
    $dto->confirmPassword = $request->get('confirm_password');
    $dto->acceptTerms = (bool) $request->get('accept_terms');

    $errors = $validator->validate($dto);
    if (count($errors) > 0) {
        // Gérer les erreurs (par exemple renvoyer un formulaire avec erreurs)
    }

    // Si validation OK, on peut mapper le DTO vers l'entité User
    // ...
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- DTO et formulaires Symfony -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation des DTO avec les formulaires Symfony</h2>
                <p class="textExemple">
                    Un FormType peut être lié à un DTO plutôt qu'à une entité. C'est très pratique pour les formulaires de recherche, de contact, ou d'inscription.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/Form/ContactDTOType.php
namespace App\Form;

use App\DTO\ContactDTO;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\EmailType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class ContactDTOType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('name', TextType::class, ['label' => 'Votre nom'])
            ->add('email', EmailType::class, ['label' => 'Votre email'])
            ->add('message', TextareaType::class, ['label' => 'Message']);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => ContactDTO::class,
        ]);
    }
}</code></pre>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">Contrôleur associé</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/contact', name: 'contact')]
public function contact(Request $request): Response
{
    $dto = new ContactDTO();
    $form = $this->createForm(ContactDTOType::class, $dto);
    $form->handleRequest($request);

    if ($form->isSubmitted() && $form->isValid()) {
        // Envoyer l'email, etc.
        $this->addFlash('success', 'Message envoyé');
        return $this->redirectToRoute('home');
    }

    return $this->render('contact/index.html.twig', [
        'form' => $form->createView(),
    ]);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Mapping DTO ↔ Entité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Mapper un DTO vers une entité (et vice-versa)</h2>
                <p class="textExemple">
                    Pour transformer un DTO en entité (ou l'inverse), on utilise souvent un <strong>Mapper</strong> (manuel, avec Symfony Serializer, ou un bundle comme AutoMapper). Voici un exemple manuel simple.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/Mapper/ArticleMapper.php
namespace App\Mapper;

use App\DTO\CreateArticleDTO;
use App\Entity\Article;

class ArticleMapper
{
    public function toEntity(CreateArticleDTO $dto): Article
    {
        $article = new Article();
        $article->setTitle($dto->title);
        $article->setContent($dto->content);
        // Le champ publishImmediately n'existe pas dans l'entité
        // On peut l'utiliser pour définir une date de publication
        if ($dto->publishImmediately) {
            $article->setPublishedAt(new \DateTimeImmutable());
        }
        return $article;
    }

    public function toDTO(Article $article): CreateArticleDTO
    {
        return new CreateArticleDTO(
            title: $article->getTitle(),
            content: $article->getContent()
        );
    }
}</code></pre>
                </div>
                <div class="textExemple">
                    <p><strong>Alternative avec Symfony Serializer</strong> (pour les cas simples) :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Serializer\SerializerInterface;

$dto = $serializer->denormalize($requestData, CreateArticleDTO::class);
$article = $serializer->denormalize($dto, Article::class);</code></pre>
                    </div>
                </div>
            </section>

            <!-- DTO pour les API (sérialisation) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">DTO pour les API (sérialisation)</h2>
                <p class="textExemple">
                    Dans une API REST ou GraphQL, on utilise souvent des DTO pour contrôler précisément les données exposées. Symfony Serializer permet d'ajouter des groupes de sérialisation.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/DTO/Api/ArticleOutputDTO.php
namespace App\DTO\Api;

use Symfony\Component\Serializer\Annotation\Groups;

class ArticleOutputDTO
{
    #[Groups(['article:read'])]
    public int $id;

    #[Groups(['article:read'])]
    public string $title;

    #[Groups(['article:read'])]
    public string $content;

    #[Groups(['article:read'])]
    public string $createdAt;

    // On n'expose pas l'auteur (champ sensible) ni les données internes
}</code></pre>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Dans le contrôleur
#[Route('/api/articles/{id}', name: 'api_article_show', methods: ['GET'])]
public function show(Article $article, SerializerInterface $serializer): Response
{
    $dto = new ArticleOutputDTO();
    $dto->id = $article->getId();
    $dto->title = $article->getTitle();
    $dto->content = $article->getContent();
    $dto->createdAt = $article->getCreatedAt()->format('Y-m-d H:i:s');

    $json = $serializer->serialize($dto, 'json', ['groups' => 'article:read']);
    return new Response($json, 200, ['Content-Type' => 'application/json']);
}</code></pre>
                </div>
            </section>

            <!-- DTO avec groupes de validation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Groupes de validation sur les DTO</h2>
                <p class="textExemple">
                    On peut utiliser les groupes de validation pour appliquer des contraintes différentes selon le contexte (création, mise à jour, recherche).
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// src/DTO/ProductDTO.php
namespace App\DTO;

use Symfony\Component\Validator\Constraints as Assert;

class ProductDTO
{
    #[Assert\NotBlank(groups: ['create', 'update'])]
    #[Assert\Length(min: 3, groups: ['create', 'update'])]
    public string $name;

    #[Assert\Positive(groups: ['create', 'update'])]
    public float $price;

    #[Assert\NotBlank(groups: ['create'])] // obligatoire à la création, optionnel en update
    public ?string $barcode = null;
}</code></pre>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-php">// Validation dans le contrôleur
$errors = $validator->validate($dto, null, ['create']); // uniquement les contraintes du groupe 'create'</code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec les DTO</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>Gardez les DTO anémiques</strong> : pas de logique métier, uniquement des données et éventuellement des contraintes de validation.</li>
                        <li><strong>Utilisez des propriétés typées (PHP 7.4+)</strong> : c'est plus clair et cela aide la sérialisation.</li>
                        <li><strong>Préférez l'immutabilité si possible</strong> : utilisez des <code>readonly</code> classes (PHP 8.2+) ou des constructeurs avec promotion des propriétés.</li>
                        <li><strong>Nommez les DTO explicitement</strong> : <code>CreateUserDTO</code>, <code>ArticleSearchDTO</code>, <code>OrderOutputDTO</code>.</li>
                        <li><strong>Ne les utilisez pas partout</strong> : pour les formulaires simples liés directement à une entité, un DTO peut être superflu.</li>
                        <li><strong>Stockez les DTO dans un namespace dédié</strong> : <code>App\DTO</code> ou <code>App\Dto</code>.</li>
                    </ul>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : DTO de recherche de produits</h3>
                    <p>Créez un DTO <code>ProductSearchDTO</code> avec les champs : <code>keyword</code> (string, optionnel), <code>minPrice</code> (float, optionnel, ≥0), <code>maxPrice</code> (float, optionnel, >0), <code>categoryId</code> (int, optionnel). Ajoutez les contraintes de validation appropriées.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/DTO/ProductSearchDTO.php
namespace App\DTO;

use Symfony\Component\Validator\Constraints as Assert;

class ProductSearchDTO
{
    public ?string $keyword = null;

    #[Assert\PositiveOrZero]
    public ?float $minPrice = null;

    #[Assert\Positive]
    public ?float $maxPrice = null;

    #[Assert\Positive]
    public ?int $categoryId = null;

    // Validation croisée : minPrice <= maxPrice (optionnel)
    #[Assert\Expression(expression: 'this.minPrice === null or this.maxPrice === null or this.minPrice <= this.maxPrice', message: 'Le prix minimum doit être inférieur ou égal au prix maximum')]
    public array $extra = []; // astuce pour la contrainte Expression
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Formulaire d'inscription avec DTO</h3>
                    <p>Implémentez un DTO <code>RegisterDTO</code> avec les champs <code>email</code>, <code>plainPassword</code>, <code>confirmPassword</code>, <code>fullName</code>. Créez un FormType lié à ce DTO et traitez la soumission dans un contrôleur en affichant les erreurs de validation.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution (extrait)</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// DTO
class RegisterDTO
{
    #[Assert\NotBlank, Assert\Email]
    public string $email;

    #[Assert\NotBlank, Assert\Length(min: 8)]
    public string $plainPassword;

    #[Assert\EqualTo(propertyPath: 'plainPassword')]
    public string $confirmPassword;

    #[Assert\NotBlank]
    public string $fullName;
}

// FormType (RegisterDTOType)
// Contrôleur :
$dto = new RegisterDTO();
$form = $this->createForm(RegisterDTOType::class, $dto);
$form->handleRequest($request);
if ($form->isSubmitted() && $form->isValid()) {
    // mapper $dto vers une entité User et enregistrer
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <div class="textExemple">
                    <p>
                        Les DTO sont un outil simple mais puissant pour structurer vos échanges de données dans Symfony. Ils renforcent la séparation des couches, améliorent la sécurité et la maintenabilité, et s'intègrent parfaitement avec les formulaires, la validation et la sérialisation.
                    </p>
                    <p>
                        Dans les leçons suivantes, nous verrons comment utiliser les DTO avec les bus de messages (Messenger) et comment automatiser le mapping avec des bibliothèques comme AutoMapper.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyDtoLesson',

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
                    // Charger PHP, Bash (pour les commandes) et YAML
                    const phpScript = document.createElement('script');
                    phpScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/php.min.js';
                    phpScript.onload = () => {
                        const bashScript = document.createElement('script');
                        bashScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/bash.min.js';
                        bashScript.onload = () => {
                            const yamlScript = document.createElement('script');
                            yamlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/yaml.min.js';
                            yamlScript.onload = resolve;
                            document.head.appendChild(yamlScript);
                        };
                        document.head.appendChild(bashScript);
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