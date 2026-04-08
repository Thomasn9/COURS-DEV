<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">CRUD dans Symfony</h1>
                <p class="lesson-meta text-white">PHP • Symfony • Doctrine • Formulaires • MakerBundle</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le CRUD ?</h2>
                <p class="textExemple">
                    <strong>CRUD</strong> est l'acronyme de <strong>C</strong>reate, <strong>R</strong>ead, <strong>U</strong>pdate, <strong>D</strong>elete.
                    Ce sont les quatre opérations de base pour la gestion de données en base de données.
                    Dans Symfony, le CRUD est généralement implémenté via :
                </p>
                <ul>
                    <li>Une <strong>entité Doctrine</strong> (le modèle de données)</li>
                    <li>Un <strong>formulaire Symfony</strong> (pour la saisie et la modification)</li>
                    <li>Un <strong>controller</strong> avec des routes pour chaque action</li>
                    <li>Des <strong>templates Twig</strong> pour l'affichage</li>
                </ul>
                <p class="textExemple">
                    Grâce au <strong>MakerBundle</strong>, Symfony peut générer automatiquement un CRUD complet
                    pour une entité donnée, en quelques secondes.
                </p>
            </section>

            <!-- Génération automatique du CRUD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Génération automatique du CRUD</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Prérequis</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Avoir une entité Doctrine existante (ex: Article)
php bin/console make:entity Article

# Installer MakerBundle (déjà fait si vous avez suivi les leçons précédentes)
composer require --dev symfony/maker-bundle</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Générer tout le CRUD en une commande</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:crud Article

# La commande demande :
#   - Le nom de la classe (Article)
#   - Le préfixe de route (par défaut : /article)
#   - Le nom du template (par défaut : article)
#   - Le nom du formulaire (par défaut : ArticleType)</code></pre>
                    </div>
                    <p>Cette commande génère :</p>
                    <ul>
                        <li>Un <strong>controller</strong> <code>ArticleController</code> avec toutes les actions CRUD</li>
                        <li>Un <strong>formulaire</strong> <code>ArticleType</code> (s'il n'existe pas)</li>
                        <li>Des <strong>templates Twig</strong> : <code>index.html.twig</code>, <code>new.html.twig</code>, <code>show.html.twig</code>, <code>edit.html.twig</code></li>
                        <li>Les routes sont automatiquement configurées avec des noms logiques</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Structure générée</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">src/
├── Controller/
│   └── ArticleController.php
├── Form/
│   └── ArticleType.php
└── Entity/
    └── Article.php

templates/
└── article/
    ├── index.html.twig
    ├── new.html.twig
    ├── show.html.twig
    └── edit.html.twig</code></pre>
                    </div>
                </div>
            </section>

            <!-- Analyse du contrôleur CRUD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Analyse du contrôleur CRUD généré</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Le contrôleur ArticleController</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/ArticleController.php
namespace App\Controller;

use App\Entity\Article;
use App\Form\ArticleType;
use App\Repository\ArticleRepository;
use Doctrine\ORM\EntityManagerInterface;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

#[Route('/article')]
class ArticleController extends AbstractController
{
    // 1. LISTE (Read - Index)
    #[Route('/', name: 'app_article_index', methods: ['GET'])]
    public function index(ArticleRepository $articleRepository): Response
    {
        return $this->render('article/index.html.twig', [
            'articles' => $articleRepository->findAll(),
        ]);
    }

    // 2. FORMULAIRE DE CRÉATION (Create - New)
    #[Route('/new', name: 'app_article_new', methods: ['GET', 'POST'])]
    public function new(Request $request, EntityManagerInterface $entityManager): Response
    {
        $article = new Article();
        $form = $this->createForm(ArticleType::class, $article);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            $entityManager->persist($article);
            $entityManager->flush();

            return $this->redirectToRoute('app_article_index', [], Response::HTTP_SEE_OTHER);
        }

        return $this->render('article/new.html.twig', [
            'article' => $article,
            'form' => $form,
        ]);
    }

    // 3. AFFICHAGE DÉTAIL (Read - Show)
    #[Route('/{id}', name: 'app_article_show', methods: ['GET'])]
    public function show(Article $article): Response
    {
        return $this->render('article/show.html.twig', [
            'article' => $article,
        ]);
    }

    // 4. FORMULAIRE D'ÉDITION (Update - Edit)
    #[Route('/{id}/edit', name: 'app_article_edit', methods: ['GET', 'POST'])]
    public function edit(Request $request, Article $article, EntityManagerInterface $entityManager): Response
    {
        $form = $this->createForm(ArticleType::class, $article);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            $entityManager->flush();

            return $this->redirectToRoute('app_article_index', [], Response::HTTP_SEE_OTHER);
        }

        return $this->render('article/edit.html.twig', [
            'article' => $article,
            'form' => $form,
        ]);
    }

    // 5. SUPPRESSION (Delete)
    #[Route('/{id}', name: 'app_article_delete', methods: ['POST'])]
    public function delete(Request $request, Article $article, EntityManagerInterface $entityManager): Response
    {
        // Vérification du token CSRF pour la suppression
        if ($this->isCsrfTokenValid('delete'.$article->getId(), $request->request->get('_token'))) {
            $entityManager->remove($article);
            $entityManager->flush();
        }

        return $this->redirectToRoute('app_article_index', [], Response::HTTP_SEE_OTHER);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Points importants</h3>
                    <ul>
                        <li>La méthode <code>show()</code> et <code>edit()</code> utilisent le <strong>ParamConverter</strong> de Symfony : <code>Article $article</code> charge automatiquement l'entité depuis l'ID dans l'URL.</li>
                        <li>La suppression utilise la méthode HTTP <code>POST</code> (pas <code>GET</code>) et un token CSRF pour la sécurité.</li>
                        <li>Les routes sont préfixées par <code>/article</code>.</li>
                    </ul>
                </div>
            </section>

            <!-- Le formulaire associé -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Le formulaire ArticleType</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/ArticleType.php
namespace App\Form;

use App\Entity\Article;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\Extension\Core\Type\DateTimeType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class ArticleType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('titre', TextType::class, [
                'label' => 'Titre',
                'attr' => ['class' => 'form-control']
            ])
            ->add('contenu', TextareaType::class, [
                'label' => 'Contenu',
                'attr' => ['rows' => 8, 'class' => 'form-control']
            ])
            ->add('dateCreation', DateTimeType::class, [
                'label' => 'Date de création',
                'widget' => 'single_text',
                'attr' => ['class' => 'form-control']
            ])
            ->add('save', SubmitType::class, [
                'label' => 'Enregistrer',
                'attr' => ['class' => 'btn btn-primary']
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
            </section>

            <!-- Templates Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les templates Twig</h2>

                <div class="textExemple">
                    <h3 class="text-purple">index.html.twig (liste des articles)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{% extends 'base.html.twig' %}

{% block body %}
    <h1>Liste des articles</h1>

    <a href="{{ path('app_article_new') }}" class="btn btn-success mb-3">Créer un article</a>

    <table class="table">
        <thead>
            <tr>
                <th>ID</th>
                <th>Titre</th>
                <th>Date création</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            {% for article in articles %}
                <tr>
                    <td>{{ article.id }}</td>
                    <td>{{ article.titre }}</td>
                    <td>{{ article.dateCreation|date('d/m/Y H:i') }}</td>
                    <td>
                        <a href="{{ path('app_article_show', {'id': article.id}) }}" class="btn btn-sm btn-info">Voir</a>
                        <a href="{{ path('app_article_edit', {'id': article.id}) }}" class="btn btn-sm btn-warning">Modifier</a>
                        <form method="post" action="{{ path('app_article_delete', {'id': article.id}) }}" style="display:inline-block">
                            <input type="hidden" name="_token" value="{{ csrf_token('delete' ~ article.id) }}">
                            <button class="btn btn-sm btn-danger" onclick="return confirm('Confirmer la suppression ?')">Supprimer</button>
                        </form>
                    </td>
                </tr>
            {% else %}
                <tr><td colspan="4">Aucun article trouvé</td></tr>
            {% endfor %}
        </tbody>
    </table>
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">new.html.twig (création)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{% extends 'base.html.twig' %}

{% block body %}
    <h1>Nouvel article</h1>

    {{ form_start(form) }}
        {{ form_widget(form) }}
        <button type="submit" class="btn btn-primary">Créer</button>
        <a href="{{ path('app_article_index') }}" class="btn btn-secondary">Retour</a>
    {{ form_end(form) }}
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">show.html.twig (détail)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{% extends 'base.html.twig' %}

{% block body %}
    <h1>{{ article.titre }}</h1>

    <p><strong>Date :</strong> {{ article.dateCreation|date('d/m/Y H:i') }}</p>
    <p><strong>Contenu :</strong></p>
    <div class="well">
        {{ article.contenu|nl2br }}
    </div>

    <a href="{{ path('app_article_edit', {'id': article.id}) }}" class="btn btn-warning">Modifier</a>
    <a href="{{ path('app_article_index') }}" class="btn btn-secondary">Retour</a>

    <form method="post" action="{{ path('app_article_delete', {'id': article.id}) }}" style="display:inline-block">
        <input type="hidden" name="_token" value="{{ csrf_token('delete' ~ article.id) }}">
        <button class="btn btn-danger" onclick="return confirm('Supprimer cet article ?')">Supprimer</button>
    </form>
{% endblock %}</code></pre>
                    </div>
                </div>
            </section>

            <!-- CRUD manuel sans générateur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">CRUD manuel (sans générateur)</h2>

                <div class="textExemple">
                    <p>
                        Vous pouvez aussi écrire votre propre CRUD sans utiliser <code>make:crud</code>. Voici les étapes clés :
                    </p>
                    <ol>
                        <li>Créez l'entité avec <code>make:entity</code>.</li>
                        <li>Créez un formulaire avec <code>make:form</code> (ou manuellement).</li>
                        <li>Créez un contrôleur avec les 5 actions (index, new, show, edit, delete).</li>
                        <li>Créez les templates Twig correspondants.</li>
                    </ol>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple d'action "edit" manuelle</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">#[Route('/{id}/edit', name: 'article_edit')]
public function edit(Request $request, Article $article, EntityManagerInterface $em): Response
{
    $form = $this->createForm(ArticleType::class, $article);
    $form->handleRequest($request);

    if ($form->isSubmitted() && $form->isValid()) {
        $em->flush();
        $this->addFlash('success', 'Article modifié !');
        return $this->redirectToRoute('article_index');
    }

    return $this->render('article/edit.html.twig', [
        'form' => $form->createView(),
        'article' => $article,
    ]);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des relations dans le CRUD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">CRUD avec relations (ManyToOne, ManyToMany)</h2>

                <div class="textExemple">
                    <p>
                        Si votre entité possède des relations, le formulaire généré par <code>make:crud</code> les gère automatiquement
                        via les champs de type <code>EntityType</code>. Vous pouvez les personnaliser.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// Dans ArticleType.php
use Symfony\Bridge\Doctrine\Form\Type\EntityType;
use App\Entity\Categorie;

$builder->add('categorie', EntityType::class, [
    'class' => Categorie::class,
    'choice_label' => 'nom',
    'label' => 'Catégorie',
    'placeholder' => 'Choisir une catégorie',
    'attr' => ['class' => 'form-select']
]);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Validation et sécurité -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Validation et sécurité</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Validation des formulaires</h3>
                    <p>Ajoutez des contraintes de validation dans l'entité ou directement dans le formulaire.</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Article.php
use Symfony\Component\Validator\Constraints as Assert;

#[Assert\NotBlank(message: 'Le titre est obligatoire')]
#[Assert\Length(min: 5, max: 255)]
private ?string $titre = null;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Sécurisation des actions</h3>
                    <ul>
                        <li>La suppression est protégée par un token CSRF.</li>
                        <li>Utilisez les <strong>voters</strong> ou <strong>@IsGranted</strong> pour restreindre l'accès.</li>
                        <li>Exemple : seuls les administrateurs peuvent supprimer.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">use Symfony\Component\Security\Http\Attribute\IsGranted;

#[IsGranted('ROLE_ADMIN')]
#[Route('/{id}/edit', name: 'app_article_edit')]
public function edit(...) { ... }</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Générer un CRUD pour Produit</h3>
                    <p>À partir de l'entité <code>Produit</code> créée précédemment (nom, prix, stock, dateCreation), générez le CRUD complet avec <code>make:crud</code>.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:crud Produit
# Répondez aux questions (préfixe de route : /produit, template : produit, form : ProduitType)
# Le CRUD est généré dans src/Controller/ProduitController.php et templates/produit/</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Personnaliser le formulaire</h3>
                    <p>Ajoutez un champ <code>slug</code> à l'entité Article, puis modifiez le formulaire ArticleType pour inclure ce champ (automatique ou manuel).</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">php bin/console make:entity Article
# Ajoutez slug (string, 255, nullable)

# Dans ArticleType.php :
->add('slug', TextType::class, [
    'label' => 'Slug',
    'required' => false,
    'attr' => ['class' => 'form-control']
])</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Ajouter une pagination</h3>
                    <p>Modifiez la méthode <code>index()</code> du contrôleur pour paginer les résultats (utilisez <code>KnpPaginatorBundle</code> ou une pagination manuelle).</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-bash">composer require knplabs/knp-paginator-bundle</code></pre>
                            <pre v-pre><code class="language-php">// Dans le controller
use Knp\Component\Pager\PaginatorInterface;

public function index(ArticleRepository $repo, PaginatorInterface $paginator, Request $request): Response
{
    $query = $repo->createQueryBuilder('a')->getQuery();
    $articles = $paginator->paginate(
        $query,
        $request->query->getInt('page', 1),
        10
    );
    return $this->render('article/index.html.twig', ['articles' => $articles]);
}</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques pour un CRUD Symfony</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Utilisez les routes nommées</strong> avec <code>path()</code> pour générer les URLs.</li>
                        <li><strong>Séparez les méthodes GET et POST</strong> : les formulaires utilisent <code>methods: ['GET', 'POST']</code>.</li>
                        <li><strong>Protégez toujours la suppression</strong> avec un token CSRF et une méthode POST.</li>
                        <li><strong>Utilisez les messages flash</strong> pour informer l'utilisateur du succès/échec des opérations.</li>
                        <li><strong>Validez côté serveur</strong> en plus de la validation HTML5.</li>
                        <li><strong>Optimisez les requêtes</strong> : dans l'index, utilisez <code>findBy()</code> avec des critères plutôt que <code>findAll()</code> si la table est volumineuse.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple avec message flash</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">if ($form->isSubmitted() && $form->isValid()) {
    $em->persist($article);
    $em->flush();
    $this->addFlash('success', 'Article créé avec succès !');
    return $this->redirectToRoute('app_article_index');
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <p>
                        Le CRUD est la brique de base de toute application web. Symfony, avec MakerBundle,
                        vous permet de générer un CRUD fonctionnel en quelques secondes.
                    </p>
                    <p>
                        Vous pouvez ensuite personnaliser chaque partie : contrôleur, formulaire, templates.
                        La séparation des responsabilités (entité, formulaire, contrôleur, vue) rend le code
                        maintenable et évolutif.
                    </p>
                    <p>
                        Prochaines étapes : ajouter des règles d'accès (voters), des événements de formulaire,
                        des collections de formulaires (formulaires imbriqués) et des API avec API Platform.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyCrudLesson',

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
                        const twigScript = document.createElement('script');
                        twigScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/twig.min.js';
                        twigScript.onload = () => {
                            const bashScript = document.createElement('script');
                            bashScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/bash.min.js';
                            bashScript.onload = resolve;
                            document.head.appendChild(bashScript);
                        };
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