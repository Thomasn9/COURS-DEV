<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Formulaires Symfony</h1>
                <p class="lesson-meta text-white">PHP • Symfony • Form Component • Validation</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux Formulaires Symfony</h2>
                <p class="textExemple">
                    Le composant Form de Symfony est l'un des systèmes les plus puissants du framework.
                    Il permet de créer, valider et traiter des formulaires HTML de manière orientée objet,
                    en découplant complètement la logique métier de la présentation.
                </p>
                <p class="textExemple">
                    Un formulaire Symfony est une classe PHP qui définit les champs, leurs types et leurs contraintes
                    de validation. Le controller se charge ensuite de traiter la requête et le template Twig affiche le rendu.
                </p>
            </section>

            <!-- Architecture -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture d'un Formulaire Symfony</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Les 3 couches d'un formulaire</h3>
                    <ul>
                        <li><strong>FormType</strong> : La classe qui définit les champs et leur configuration</li>
                        <li><strong>Controller</strong> : Crée le formulaire, gère la soumission et la validation</li>
                        <li><strong>Template Twig</strong> : Affiche le formulaire HTML avec les erreurs</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Utilisateur          Controller               FormType
    │                     │                       │
    │ ─── GET /form ────→ │                       │
    │                     │ ── createForm() ────→ │
    │                     │ ←── Form objet ─────── │
    │ ←── HTML rendu ──── │                       │
    │                     │                       │
    │ ─── POST /form ───→ │                       │
    │                     │ ── handleRequest() ──→ │
    │                     │ ── isSubmitted()       │
    │                     │ ── isValid() ──────── Validation
    │                     │      │                 │
    │                     │   Sauvegarde           │
    │ ←── Redirect ─────── │                       │</code></pre>
                    </div>
                </div>
            </section>

            <!-- Installation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Installation et Prérequis</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Installer le composant Form</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Installer le composant Form (inclus dans symfony/webapp-pack)
composer require symfony/form

# Installer le composant Validator pour la validation
composer require symfony/validator

# Installer Twig pour les templates (si pas déjà installé)
composer require symfony/twig-bundle

# Pour les formulaires Bootstrap (optionnel)
composer require symfony/twig-extra-bundle</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer une classe FormType avec le CLI</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Générer automatiquement un FormType avec Maker Bundle
composer require symfony/maker-bundle --dev

# Créer un FormType lié à une entité
php bin/console make:form ArticleType Article

# Créer un FormType sans entité
php bin/console make:form ContactType</code></pre>
                    </div>
                </div>
            </section>

            <!-- Créer un FormType -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer un FormType</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Structure d'un FormType de base</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/ArticleType.php
namespace App\Form;

use App\Entity\Article;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\Extension\Core\Type\DateType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class ArticleType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('titre', TextType::class, [
                'label'    => 'Titre de l\'article',
                'attr'     => ['placeholder' => 'Saisissez un titre...'],
                'required' => true,
            ])
            ->add('contenu', TextareaType::class, [
                'label' => 'Contenu',
                'attr'  => ['rows' => 8],
            ])
            ->add('publishedAt', DateType::class, [
                'label'  => 'Date de publication',
                'widget' => 'single_text',
            ])
            ->add('save', SubmitType::class, [
                'label' => 'Publier l\'article',
            ]);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => Article::class,
        ]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les types de champs courants</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Champs texte
TextType::class         // input type="text"
TextareaType::class     // textarea
EmailType::class        // input type="email"
PasswordType::class     // input type="password"
SearchType::class       // input type="search"
UrlType::class          // input type="url"

// Champs numériques et dates
IntegerType::class      // input type="number"
NumberType::class       // input type="number" (float)
DateType::class         // Sélecteur de date
DateTimeType::class     // Date + heure

// Champs de choix
ChoiceType::class       // select ou radio/checkbox
EntityType::class       // select depuis une entité Doctrine
CheckboxType::class     // input type="checkbox"
RadioType::class        // input type="radio"

// Champs fichier et divers
FileType::class         // input type="file"
HiddenType::class       // input type="hidden"
SubmitType::class       // button type="submit"</code></pre>
                    </div>
                </div>
            </section>

            <!-- Controller -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gérer le Formulaire dans le Controller</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Controller complet : Création et modification</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/ArticleController.php
namespace App\Controller;

use App\Entity\Article;
use App\Form\ArticleType;
use Doctrine\ORM\EntityManagerInterface;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class ArticleController extends AbstractController
{
    // ─── Création d'un nouvel article ──────────────────────
    #[Route('/article/new', name: 'article_new')]
    public function new(
        Request $request,
        EntityManagerInterface $em
    ): Response {
        // 1. Créer une nouvelle entité vide
        $article = new Article();

        // 2. Créer le formulaire lié à l'entité
        $form = $this->createForm(ArticleType::class, $article);

        // 3. Traiter la requête HTTP
        $form->handleRequest($request);

        // 4. Vérifier si le formulaire est soumis et valide
        if ($form->isSubmitted() && $form->isValid()) {
            // 5. Persister et sauvegarder en base
            $em->persist($article);
            $em->flush();

            // 6. Rediriger après succès (pattern PRG)
            return $this->redirectToRoute('article_show', [
                'id' => $article->getId(),
            ]);
        }

        // 7. Afficher le formulaire (GET ou erreurs)
        return $this->render('article/new.html.twig', [
            'form' => $form,
        ]);
    }

    // ─── Édition d'un article existant ─────────────────────
    #[Route('/article/{id}/edit', name: 'article_edit')]
    public function edit(
        Article $article,
        Request $request,
        EntityManagerInterface $em
    ): Response {
        // L'article existant est injecté automatiquement (ParamConverter)
        $form = $this->createForm(ArticleType::class, $article);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            $em->flush(); // Pas besoin de persist() pour une entité déjà gérée

            return $this->redirectToRoute('article_show', [
                'id' => $article->getId(),
            ]);
        }

        return $this->render('article/edit.html.twig', [
            'article' => $article,
            'form'    => $form,
        ]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">⚠️ Le Pattern Post/Redirect/Get (PRG)</h3>
                    <div class="warning-section">
                        <h4 class="text-purple">Pourquoi toujours rediriger après une soumission réussie</h4>
                        <div class="code-comparison">
                            <div>
                                <h5>Mauvaise pratique</h5>
                                <div class="code-example">
                                    <pre v-pre><code class="language-php">if ($form->isSubmitted() && $form->isValid()) {
    $em->flush();

    // ❌ Pas de redirect !
    return $this->render(
        'article/success.html.twig'
    );
    // Rechargement = re-soumission !
}</code></pre>
                                </div>
                                <p class="warning-text">Re-soumission si l'utilisateur recharge la page</p>
                            </div>
                            <div>
                                <h5>Bonne pratique (PRG)</h5>
                                <div class="code-example">
                                    <pre v-pre><code class="language-php">if ($form->isSubmitted() && $form->isValid()) {
    $em->flush();

    // ✅ Toujours rediriger !
    return $this->redirectToRoute(
        'article_list'
    );
    // Rechargement = simple GET
}</code></pre>
                                </div>
                                <p class="success-text">Aucun risque de double soumission</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Validation -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Validation des Données</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Contraintes via les attributs PHP (sur l'entité)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Article.php
namespace App\Entity;

use Symfony\Component\Validator\Constraints as Assert;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity]
class Article
{
    #[ORM\Column(length: 255)]
    #[Assert\NotBlank(message: 'Le titre ne peut pas être vide')]
    #[Assert\Length(
        min: 5,
        max: 255,
        minMessage: 'Le titre doit faire au moins {{ limit }} caractères',
        maxMessage: 'Le titre ne peut pas dépasser {{ limit }} caractères'
    )]
    private ?string $titre = null;

    #[ORM\Column(type: 'text')]
    #[Assert\NotBlank]
    #[Assert\Length(min: 20, minMessage: 'Le contenu est trop court')]
    private ?string $contenu = null;

    #[ORM\Column(type: 'string', length: 180, unique: true)]
    #[Assert\NotBlank]
    #[Assert\Email(message: "'{{ value }}' n'est pas un email valide")]
    private ?string $email = null;

    #[ORM\Column]
    #[Assert\NotNull]
    #[Assert\GreaterThanOrEqual('today', message: 'La date doit être dans le futur')]
    private ?\DateTimeInterface $publishedAt = null;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les contraintes de validation les plus utiles</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Contraintes de base
#[Assert\NotBlank]                     // Valeur non vide
#[Assert\NotNull]                      // Valeur non nulle
#[Assert\IsTrue]                       // Doit être true (ex: CGU cochées)

// Contraintes de chaîne
#[Assert\Length(min: 2, max: 100)]     // Longueur min/max
#[Assert\Email]                        // Format email valide
#[Assert\Url]                          // Format URL valide
#[Assert\Regex(pattern: '/^[a-z]+$/')] // Expression régulière

// Contraintes numériques
#[Assert\Range(min: 0, max: 100)]      // Valeur entre min et max
#[Assert\Positive]                     // Nombre strictement positif
#[Assert\GreaterThan(0)]               // Supérieur à une valeur

// Contraintes de choix
#[Assert\Choice(choices: ['a', 'b'])]  // Valeur dans une liste
#[Assert\Count(min: 1, max: 5)]        // Nombre d'éléments d'une collection

// Contraintes de date
#[Assert\Date]                         // Format date valide (YYYY-MM-DD)
#[Assert\DateTime]                     // Format datetime valide
#[Assert\GreaterThanOrEqual('today')]  // Date dans le futur

// Contraintes de fichier
#[Assert\File(
    maxSize: '2M',
    mimeTypes: ['image/jpeg', 'image/png']
)]                                     // Validation d'un fichier uploadé</code></pre>
                    </div>
                </div>
            </section>

            <!-- Template Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Affichage dans un Template Twig</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Rendu complet du formulaire</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/article/new.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    {{ form_start(form) }}

        {# Afficher tous les champs d'un coup (pratique en dev) #}
        {{ form_widget(form) }}

        {# --- OU --- Affichage personnalisé champ par champ #}
        {{ form_row(form.titre) }}
        {{ form_row(form.contenu) }}
        {{ form_row(form.publishedAt) }}

        {# Bouton submit personnalisé #}
        <button type="submit" class="btn btn-primary">
            Publier l'article
        </button>

    {{ form_end(form) }}
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Rendu personnalisé avec séparation label/widget/erreurs</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{{ form_start(form, {'attr': {'class': 'needs-validation', 'novalidate': true}}) }}

    <div class="mb-3">
        {# Label du champ #}
        {{ form_label(form.titre, 'Titre', {'label_attr': {'class': 'form-label fw-bold'}}) }}

        {# Input du champ #}
        {{ form_widget(form.titre, {'attr': {'class': 'form-control'}}) }}

        {# Affichage des erreurs #}
        {% for error in form.titre.vars.errors %}
            <div class="text-danger small mt-1">
                {{ error.message }}
            </div>
        {% endfor %}
    </div>

    <div class="mb-3">
        {{ form_label(form.contenu) }}
        {{ form_widget(form.contenu, {'attr': {'class': 'form-control', 'rows': 6}}) }}
        {{ form_errors(form.contenu) }}
    </div>

    {# Champs cachés (token CSRF etc.) #}
    {{ form_rest(form) }}

{{ form_end(form) }}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Thèmes de formulaire disponibles</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# Appliquer un thème Bootstrap 5 sur un seul formulaire #}
{% form_theme form 'bootstrap_5_layout.html.twig' %}

{# Ou globalement dans config/packages/twig.yaml #}
# twig:
#   form_themes:
#     - 'bootstrap_5_layout.html.twig'
#     - 'foundation_5_layout.html.twig'  # Alternative Foundation CSS
#     - 'form_div_layout.html.twig'      # Thème par défaut (divs)
#     - 'form_table_layout.html.twig'    # Thème tableau</code></pre>
                    </div>
                </div>
            </section>

            <!-- Fonctionnalités avancées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fonctionnalités Avancées</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Formulaire avec EntityType (relation Doctrine)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Bridge\Doctrine\Form\Type\EntityType;

$builder
    ->add('categorie', EntityType::class, [
        'class'        => Categorie::class,
        'choice_label' => 'nom',       // Propriété à afficher dans l'option
        'label'        => 'Catégorie',
        'placeholder'  => 'Choisissez une catégorie',
        'query_builder' => function(EntityRepository $repo) {
            return $repo->createQueryBuilder('c')
                ->orderBy('c.nom', 'ASC');
        },
    ])
    ->add('tags', EntityType::class, [
        'class'        => Tag::class,
        'choice_label' => 'nom',
        'multiple'     => true,   // Sélection multiple
        'expanded'     => true,   // Affichage en checkboxes
        'label'        => 'Tags',
    ]);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Formulaire de contact sans entité</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/ContactType.php
class ContactType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('nom', TextType::class, [
                'constraints' => [
                    new Assert\NotBlank(),
                    new Assert\Length(['min' => 2]),
                ],
            ])
            ->add('email', EmailType::class, [
                'constraints' => [new Assert\NotBlank(), new Assert\Email()],
            ])
            ->add('sujet', ChoiceType::class, [
                'choices' => [
                    'Question générale' => 'general',
                    'Support technique' => 'support',
                    'Partenariat'       => 'partenariat',
                ],
            ])
            ->add('message', TextareaType::class);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        // Pas de data_class car pas d'entité liée
        $resolver->setDefaults([]);
    }
}

// Récupérer les données dans le controller
if ($form->isSubmitted() && $form->isValid()) {
    $data = $form->getData(); // Retourne un tableau associatif
    // $data['nom'], $data['email'], $data['message']...
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Upload de fichier</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans le FormType
$builder->add('imageFile', FileType::class, [
    'label'      => 'Image (JPG ou PNG)',
    'mapped'     => false,  // Non mappé sur l'entité
    'required'   => false,
    'constraints' => [
        new Assert\File([
            'maxSize'          => '2M',
            'mimeTypes'        => ['image/jpeg', 'image/png', 'image/webp'],
            'mimeTypesMessage' => 'Veuillez uploader une image valide',
        ])
    ],
]);

// Dans le controller
$imageFile = $form->get('imageFile')->getData();

if ($imageFile) {
    $newFilename = uniqid() . '.' . $imageFile->guessExtension();
    $imageFile->move(
        $this->getParameter('uploads_directory'),
        $newFilename
    );
    $article->setImageFilename($newFilename);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Sécurité CSRF -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Sécurité : Protection CSRF</h2>

                <div class="textExemple">
                    <p>
                        Symfony active automatiquement la protection CSRF sur tous les formulaires.
                        Un token unique est généré et vérifié à chaque soumission, sans gestion manuelle.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// La protection CSRF est active par défaut
public function configureOptions(OptionsResolver $resolver): void
{
    $resolver->setDefaults([
        'data_class'      => Article::class,
        'csrf_protection' => true,           // Activé par défaut
        'csrf_field_name' => '_token',       // Nom du champ caché
        'csrf_token_id'   => 'article_item', // Identifiant unique
    ]);
}

// form_end(form) génère automatiquement :
// <input type="hidden" name="_token" value="..."></code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices Pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Formulaire d'inscription utilisateur</h3>
                    <p>Créer un formulaire d'inscription avec les champs et contraintes suivantes :</p>
                    <ul>
                        <li>Prénom et Nom (requis, min 2 caractères)</li>
                        <li>Email (requis, format valide)</li>
                        <li>Mot de passe (requis, min 8 caractères, avec confirmation)</li>
                        <li>Date de naissance (requis, doit avoir au moins 18 ans)</li>
                        <li>Acceptation des CGU (checkbox obligatoire)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Form/RegistrationFormType.php
use Symfony\Component\Form\Extension\Core\Type\RepeatedType;

class RegistrationFormType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('prenom', TextType::class, [
                'label' => 'Prénom',
                'constraints' => [
                    new Assert\NotBlank(),
                    new Assert\Length(['min' => 2]),
                ],
            ])
            ->add('nom', TextType::class, [
                'label' => 'Nom',
                'constraints' => [
                    new Assert\NotBlank(),
                    new Assert\Length(['min' => 2]),
                ],
            ])
            ->add('email', EmailType::class, [
                'constraints' => [new Assert\NotBlank(), new Assert\Email()],
            ])
            ->add('plainPassword', RepeatedType::class, [
                'type'            => PasswordType::class,
                'first_options'   => ['label' => 'Mot de passe'],
                'second_options'  => ['label' => 'Confirmer le mot de passe'],
                'invalid_message' => 'Les mots de passe doivent correspondre',
                'mapped'          => false,
                'constraints'     => [
                    new Assert\NotBlank(),
                    new Assert\Length(['min' => 8]),
                ],
            ])
            ->add('dateNaissance', DateType::class, [
                'label'       => 'Date de naissance',
                'widget'      => 'single_text',
                'constraints' => [
                    new Assert\NotNull(),
                    new Assert\LessThanOrEqual('-18 years'),
                ],
            ])
            ->add('agreeTerms', CheckboxType::class, [
                'label'       => 'J\'accepte les conditions d\'utilisation',
                'mapped'      => false,
                'constraints' => [new Assert\IsTrue([
                    'message' => 'Vous devez accepter les CGU',
                ])],
            ]);
    }
}</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Formulaire de recherche avec filtres</h3>
                    <p>Créer un formulaire de recherche pour filtrer des produits :</p>
                    <ul>
                        <li>Champ de recherche texte (optionnel)</li>
                        <li>Sélection de catégorie via EntityType</li>
                        <li>Fourchette de prix (min et max)</li>
                        <li>Tri par (nom, prix, date) avec ChoiceType</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-php">// src/Form/ProduitSearchType.php
class ProduitSearchType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('recherche', SearchType::class, [
                'required' => false,
                'label'    => 'Rechercher un produit',
                'attr'     => ['placeholder' => 'Nom, référence...'],
            ])
            ->add('categorie', EntityType::class, [
                'class'        => Categorie::class,
                'choice_label' => 'nom',
                'required'     => false,
                'placeholder'  => 'Toutes les catégories',
            ])
            ->add('prixMin', NumberType::class, [
                'label'       => 'Prix minimum (€)',
                'required'    => false,
                'constraints' => [new Assert\PositiveOrZero()],
            ])
            ->add('prixMax', NumberType::class, [
                'label'       => 'Prix maximum (€)',
                'required'    => false,
                'constraints' => [new Assert\Positive()],
            ])
            ->add('tri', ChoiceType::class, [
                'label'   => 'Trier par',
                'choices' => [
                    'Nom A → Z'      => 'nom_asc',
                    'Nom Z → A'      => 'nom_desc',
                    'Prix croissant' => 'prix_asc',
                    'Plus récent'    => 'date_desc',
                ],
                'required' => false,
            ]);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'method'          => 'GET',   // Formulaire de recherche → méthode GET
            'csrf_protection' => false,   // Pas de CSRF pour les GET
        ]);
    }
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Organisation et architecture</h3>
                    <ul>
                        <li><strong>Un FormType par formulaire</strong> : évitez les FormTypes « fourre-tout »</li>
                        <li><strong>data_class sur les entités</strong> : laissez Symfony mapper automatiquement</li>
                        <li><strong>Contraintes sur l'entité</strong> : réutilisables partout (API, CLI, Form)</li>
                        <li><strong>Contraintes dans le Form</strong> : uniquement si spécifiques à ce formulaire</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurité</h3>
                    <ul>
                        <li>Ne jamais désactiver la protection CSRF sans raison valide</li>
                        <li>Toujours valider côté serveur, même si validé côté client</li>
                        <li>Utiliser <code>mapped: false</code> pour les champs sensibles (mot de passe, fichiers)</li>
                        <li>Rediriger systématiquement après une soumission réussie (pattern PRG)</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Performance et expérience utilisateur</h3>
                    <ul>
                        <li>Utiliser <code>query_builder</code> sur EntityType pour filtrer les choix en BDD</li>
                        <li>Pré-remplir les formulaires d'édition en passant l'entité existante à <code>createForm()</code></li>
                        <li>Afficher les erreurs au plus près du champ concerné</li>
                        <li>Ajouter des <code>placeholder</code> et <code>help</code> clairs pour guider l'utilisateur</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Le composant Form de Symfony est un outil extrêmement puissant qui, une fois maîtrisé,
                        permet de construire des formulaires robustes, sécurisés et maintenables en très peu de code.
                    </p>
                    <p>
                        <strong>Rappel crucial</strong> : Séparez toujours la définition du formulaire (FormType),
                        son traitement (Controller) et son affichage (Twig) pour respecter la séparation des responsabilités.
                    </p>
                    <p>
                        Dans les prochaines leçons, nous aborderons les Form Collections (formulaires imbriqués),
                        les Form Events pour des formulaires dynamiques et la création de types de champs personnalisés.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyFormLesson',

    mounted() {
        // Charger highlight.js + thème VS Code Dark via CDN
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
                    // Charger les langages PHP et Twig en plus
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
            // Appliquer la coloration sur tous les blocs de code
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