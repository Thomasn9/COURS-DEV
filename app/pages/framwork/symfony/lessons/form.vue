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
                    de validation. Le controller se charge ensuite de traiter la requête et le template Twig affiche le
                    rendu.
                </p>
            </section>

            <!-- Concepts fondamentaux -->
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
                        <pre><code>Utilisateur          Controller               FormType
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
                        <pre><code><span class="php-comment"># Installer le composant Form (inclus dans symfony/webapp-pack)</span>
<span class="php-string">composer require symfony/form</span>

<span class="php-comment"># Installer le composant Validator pour la validation</span>
<span class="php-string">composer require symfony/validator</span>

<span class="php-comment"># Installer Twig pour les templates (si pas déjà installé)</span>
<span class="php-string">composer require symfony/twig-bundle</span>

<span class="php-comment"># Pour les formulaires Bootstrap (optionnel)</span>
<span class="php-string">composer require symfony/twig-extra-bundle</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Créer une classe FormType avec le CLI</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment"># Générer automatiquement un FormType avec Maker Bundle</span>
<span class="php-string">composer require symfony/maker-bundle --dev</span>

<span class="php-comment"># Créer un FormType lié à une entité</span>
<span class="php-string">php bin/console make:form ArticleType Article</span>

<span class="php-comment"># Créer un FormType sans entité</span>
<span class="php-string">php bin/console make:form ContactType</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Créer un FormType -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer un FormType</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Structure d'un FormType de base</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// src/Form/ArticleType.php</span>
<span class="php-reserved">namespace</span> <span class="php-identifier">App\Form</span>;

<span class="php-reserved">use</span> <span class="php-identifier">App\Entity\Article</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\AbstractType</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\Extension\Core\Type\TextType</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\Extension\Core\Type\TextareaType</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\Extension\Core\Type\DateType</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\Extension\Core\Type\SubmitType</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\FormBuilderInterface</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\OptionsResolver\OptionsResolver</span>;

<span class="php-reserved">class</span> <span class="php-class">ArticleType</span> <span class="php-reserved">extends</span> <span class="php-class">AbstractType</span>
{
    <span class="php-reserved">public function</span> <span class="php-function">buildForm</span>(<span class="php-class">FormBuilderInterface</span> <span class="php-variable">$builder</span>, <span class="php-reserved">array</span> <span class="php-variable">$options</span>): <span class="php-reserved">void</span>
    {
        <span class="php-variable">$builder</span>
            -><span class="php-function">add</span>(<span class="php-string">'titre'</span>, <span class="php-class">TextType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>    => <span class="php-string">'Titre de l\'article'</span>,
                <span class="php-string">'attr'</span>     => [<span class="php-string">'placeholder'</span> => <span class="php-string">'Saisissez un titre...'</span>],
                <span class="php-string">'required'</span> => <span class="php-reserved">true</span>,
            ])
            -><span class="php-function">add</span>(<span class="php-string">'contenu'</span>, <span class="php-class">TextareaType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span> => <span class="php-string">'Contenu'</span>,
                <span class="php-string">'attr'</span>  => [<span class="php-string">'rows'</span> => <span class="php-number">8</span>],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'publishedAt'</span>, <span class="php-class">DateType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>  => <span class="php-string">'Date de publication'</span>,
                <span class="php-string">'widget'</span> => <span class="php-string">'single_text'</span>,
            ])
            -><span class="php-function">add</span>(<span class="php-string">'save'</span>, <span class="php-class">SubmitType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span> => <span class="php-string">'Publier l\'article'</span>,
            ]);
    }

    <span class="php-reserved">public function</span> <span class="php-function">configureOptions</span>(<span class="php-class">OptionsResolver</span> <span class="php-variable">$resolver</span>): <span class="php-reserved">void</span>
    {
        <span class="php-variable">$resolver</span>-><span class="php-function">setDefaults</span>([
            <span class="php-string">'data_class'</span> => <span class="php-class">Article</span>::<span class="php-reserved">class</span>,
        ]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les types de champs courants</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// Champs texte</span>
<span class="php-class">TextType</span>::<span class="php-reserved">class</span>         <span class="php-comment">// &lt;input type="text"&gt;</span>
<span class="php-class">TextareaType</span>::<span class="php-reserved">class</span>     <span class="php-comment">// &lt;textarea&gt;</span>
<span class="php-class">EmailType</span>::<span class="php-reserved">class</span>        <span class="php-comment">// &lt;input type="email"&gt;</span>
<span class="php-class">PasswordType</span>::<span class="php-reserved">class</span>     <span class="php-comment">// &lt;input type="password"&gt;</span>
<span class="php-class">SearchType</span>::<span class="php-reserved">class</span>       <span class="php-comment">// &lt;input type="search"&gt;</span>
<span class="php-class">UrlType</span>::<span class="php-reserved">class</span>          <span class="php-comment">// &lt;input type="url"&gt;</span>

<span class="php-comment">// Champs numériques et dates</span>
<span class="php-class">IntegerType</span>::<span class="php-reserved">class</span>      <span class="php-comment">// &lt;input type="number"&gt;</span>
<span class="php-class">NumberType</span>::<span class="php-reserved">class</span>       <span class="php-comment">// &lt;input type="number"&gt; (float)</span>
<span class="php-class">DateType</span>::<span class="php-reserved">class</span>         <span class="php-comment">// Sélecteur de date</span>
<span class="php-class">DateTimeType</span>::<span class="php-reserved">class</span>     <span class="php-comment">// Date + heure</span>

<span class="php-comment">// Champs de choix</span>
<span class="php-class">ChoiceType</span>::<span class="php-reserved">class</span>       <span class="php-comment">// &lt;select&gt; ou radio/checkbox</span>
<span class="php-class">EntityType</span>::<span class="php-reserved">class</span>       <span class="php-comment">// &lt;select&gt; depuis une entité Doctrine</span>
<span class="php-class">CheckboxType</span>::<span class="php-reserved">class</span>    <span class="php-comment">// &lt;input type="checkbox"&gt;</span>
<span class="php-class">RadioType</span>::<span class="php-reserved">class</span>        <span class="php-comment">// &lt;input type="radio"&gt;</span>

<span class="php-comment">// Champs fichier et divers</span>
<span class="php-class">FileType</span>::<span class="php-reserved">class</span>         <span class="php-comment">// &lt;input type="file"&gt;</span>
<span class="php-class">HiddenType</span>::<span class="php-reserved">class</span>       <span class="php-comment">// &lt;input type="hidden"&gt;</span>
<span class="php-class">SubmitType</span>::<span class="php-reserved">class</span>       <span class="php-comment">// &lt;button type="submit"&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Controller -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gérer le Formulaire dans le Controller</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Controller complet : Création et modification</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// src/Controller/ArticleController.php</span>
<span class="php-reserved">namespace</span> <span class="php-identifier">App\Controller</span>;

<span class="php-reserved">use</span> <span class="php-identifier">App\Entity\Article</span>;
<span class="php-reserved">use</span> <span class="php-identifier">App\Form\ArticleType</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Doctrine\ORM\EntityManagerInterface</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Bundle\FrameworkBundle\Controller\AbstractController</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\HttpFoundation\Request</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\HttpFoundation\Response</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Routing\Attribute\Route</span>;

<span class="php-reserved">class</span> <span class="php-class">ArticleController</span> <span class="php-reserved">extends</span> <span class="php-class">AbstractController</span>
{
    <span class="php-comment">// ─── Création d'un nouvel article ──────────────────────</span>
    <span class="php-reserved">#[Route</span>(<span class="php-string">'/article/new'</span>, name: <span class="php-string">'article_new'</span>)]
    <span class="php-reserved">public function</span> <span class="php-function">new</span>(
        <span class="php-class">Request</span> <span class="php-variable">$request</span>,
        <span class="php-class">EntityManagerInterface</span> <span class="php-variable">$em</span>
    ): <span class="php-class">Response</span> {
        <span class="php-comment">// 1. Créer une nouvelle entité vide</span>
        <span class="php-variable">$article</span> = <span class="php-reserved">new</span> <span class="php-class">Article</span>();

        <span class="php-comment">// 2. Créer le formulaire lié à l'entité</span>
        <span class="php-variable">$form</span> = <span class="php-variable">$this</span>-><span class="php-function">createForm</span>(<span class="php-class">ArticleType</span>::<span class="php-reserved">class</span>, <span class="php-variable">$article</span>);

        <span class="php-comment">// 3. Traiter la requête HTTP</span>
        <span class="php-variable">$form</span>-><span class="php-function">handleRequest</span>(<span class="php-variable">$request</span>);

        <span class="php-comment">// 4. Vérifier si le formulaire est soumis et valide</span>
        <span class="php-reserved">if</span> (<span class="php-variable">$form</span>-><span class="php-function">isSubmitted</span>() && <span class="php-variable">$form</span>-><span class="php-function">isValid</span>()) {
            <span class="php-comment">// 5. Persister et sauvegarder en base</span>
            <span class="php-variable">$em</span>-><span class="php-function">persist</span>(<span class="php-variable">$article</span>);
            <span class="php-variable">$em</span>-><span class="php-function">flush</span>();

            <span class="php-comment">// 6. Rediriger après succès (pattern PRG)</span>
            <span class="php-reserved">return</span> <span class="php-variable">$this</span>-><span class="php-function">redirectToRoute</span>(<span class="php-string">'article_show'</span>, [
                <span class="php-string">'id'</span> => <span class="php-variable">$article</span>-><span class="php-function">getId</span>(),
            ]);
        }

        <span class="php-comment">// 7. Afficher le formulaire (GET ou erreurs)</span>
        <span class="php-reserved">return</span> <span class="php-variable">$this</span>-><span class="php-function">render</span>(<span class="php-string">'article/new.html.twig'</span>, [
            <span class="php-string">'form'</span> => <span class="php-variable">$form</span>,
        ]);
    }

    <span class="php-comment">// ─── Édition d'un article existant ─────────────────────</span>
    <span class="php-reserved">#[Route</span>(<span class="php-string">'/article/{id}/edit'</span>, name: <span class="php-string">'article_edit'</span>)]
    <span class="php-reserved">public function</span> <span class="php-function">edit</span>(
        <span class="php-class">Article</span> <span class="php-variable">$article</span>,
        <span class="php-class">Request</span> <span class="php-variable">$request</span>,
        <span class="php-class">EntityManagerInterface</span> <span class="php-variable">$em</span>
    ): <span class="php-class">Response</span> {
        <span class="php-comment">// L'article existant est injecté automatiquement (ParamConverter)</span>
        <span class="php-variable">$form</span> = <span class="php-variable">$this</span>-><span class="php-function">createForm</span>(<span class="php-class">ArticleType</span>::<span class="php-reserved">class</span>, <span class="php-variable">$article</span>);
        <span class="php-variable">$form</span>-><span class="php-function">handleRequest</span>(<span class="php-variable">$request</span>);

        <span class="php-reserved">if</span> (<span class="php-variable">$form</span>-><span class="php-function">isSubmitted</span>() && <span class="php-variable">$form</span>-><span class="php-function">isValid</span>()) {
            <span class="php-variable">$em</span>-><span class="php-function">flush</span>(); <span class="php-comment">// Pas besoin de persist() pour une entité déjà gérée</span>

            <span class="php-reserved">return</span> <span class="php-variable">$this</span>-><span class="php-function">redirectToRoute</span>(<span class="php-string">'article_show'</span>, [
                <span class="php-string">'id'</span> => <span class="php-variable">$article</span>-><span class="php-function">getId</span>(),
            ]);
        }

        <span class="php-reserved">return</span> <span class="php-variable">$this</span>-><span class="php-function">render</span>(<span class="php-string">'article/edit.html.twig'</span>, [
            <span class="php-string">'article'</span> => <span class="php-variable">$article</span>,
            <span class="php-string">'form'</span>    => <span class="php-variable">$form</span>,
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
                                    <pre><code><span class="php-reserved">if</span> (<span class="php-variable">$form</span>-><span class="php-function">isSubmitted</span>() && <span class="php-variable">$form</span>-><span class="php-function">isValid</span>()) {
    <span class="php-variable">$em</span>-><span class="php-function">flush</span>();

    <span class="php-comment">// ❌ Pas de redirect !</span>
    <span class="php-reserved">return</span> <span class="php-variable">$this</span>-><span class="php-function">render</span>(
        <span class="php-string">'article/success.html.twig'</span>
    );
    <span class="php-comment">// Rechargement = re-soumission du formulaire !</span>
}</span></code></pre>
                                </div>
                                <p class="warning-text">Re-soumission si l'utilisateur recharge la page</p>
                            </div>
                            <div>
                                <h5>Bonne pratique (PRG)</h5>
                                <div class="code-example">
                                    <pre><code><span class="php-reserved">if</span> (<span class="php-variable">$form</span>-><span class="php-function">isSubmitted</span>() && <span class="php-variable">$form</span>-><span class="php-function">isValid</span>()) {
    <span class="php-variable">$em</span>-><span class="php-function">flush</span>();

    <span class="php-comment">// ✅ Toujours rediriger !</span>
    <span class="php-reserved">return</span> <span class="php-variable">$this</span>-><span class="php-function">redirectToRoute</span>(
        <span class="php-string">'article_list'</span>
    );
    <span class="php-comment">// Rechargement = simple GET, pas de double envoi</span>
}</span></code></pre>
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
                        <pre><code><span class="php-comment">// src/Entity/Article.php</span>
<span class="php-reserved">namespace</span> <span class="php-identifier">App\Entity</span>;

<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Validator\Constraints</span> <span class="php-reserved">as</span> <span class="php-identifier">Assert</span>;
<span class="php-reserved">use</span> <span class="php-identifier">Doctrine\ORM\Mapping</span> <span class="php-reserved">as</span> <span class="php-identifier">ORM</span>;

<span class="php-reserved">#[ORM\Entity]</span>
<span class="php-reserved">class</span> <span class="php-class">Article</span>
{
    <span class="php-reserved">#[ORM\Column(length: 255)]</span>
    <span class="php-reserved">#[Assert\NotBlank(message: 'Le titre ne peut pas être vide')]</span>
    <span class="php-reserved">#[Assert\Length(
        min: 5,
        max: 255,
        minMessage: 'Le titre doit faire au moins {{ limit }} caractères',
        maxMessage: 'Le titre ne peut pas dépasser {{ limit }} caractères'
    )]</span>
    <span class="php-reserved">private</span> ?<span class="php-reserved">string</span> <span class="php-variable">$titre</span> = <span class="php-reserved">null</span>;

    <span class="php-reserved">#[ORM\Column(type: 'text')]</span>
    <span class="php-reserved">#[Assert\NotBlank]</span>
    <span class="php-reserved">#[Assert\Length(min: 20, minMessage: 'Le contenu est trop court')]</span>
    <span class="php-reserved">private</span> ?<span class="php-reserved">string</span> <span class="php-variable">$contenu</span> = <span class="php-reserved">null</span>;

    <span class="php-reserved">#[ORM\Column(type: 'string', length: 180, unique: true)]</span>
    <span class="php-reserved">#[Assert\NotBlank]</span>
    <span class="php-reserved">#[Assert\Email(message: "'{{ value }}' n'est pas un email valide")]</span>
    <span class="php-reserved">private</span> ?<span class="php-reserved">string</span> <span class="php-variable">$email</span> = <span class="php-reserved">null</span>;

    <span class="php-reserved">#[ORM\Column]</span>
    <span class="php-reserved">#[Assert\NotNull]</span>
    <span class="php-reserved">#[Assert\GreaterThanOrEqual('today', message: 'La date doit être dans le futur')]</span>
    <span class="php-reserved">private</span> ?<span class="php-class">\DateTimeInterface</span> <span class="php-variable">$publishedAt</span> = <span class="php-reserved">null</span>;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les contraintes de validation les plus utiles</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// Contraintes de base</span>
<span class="php-reserved">#[Assert\NotBlank]</span>                     <span class="php-comment">// Valeur non vide (chaîne non vide)</span>
<span class="php-reserved">#[Assert\NotNull]</span>                      <span class="php-comment">// Valeur non nulle</span>
<span class="php-reserved">#[Assert\IsTrue]</span>                       <span class="php-comment">// Doit être true (ex: CGU cochées)</span>

<span class="php-comment">// Contraintes de chaîne</span>
<span class="php-reserved">#[Assert\Length(min: 2, max: 100)]</span>     <span class="php-comment">// Longueur min/max</span>
<span class="php-reserved">#[Assert\Email]</span>                        <span class="php-comment">// Format email valide</span>
<span class="php-reserved">#[Assert\Url]</span>                          <span class="php-comment">// Format URL valide</span>
<span class="php-reserved">#[Assert\Regex(pattern: '/^[a-z]+$/')]</span> <span class="php-comment">// Expression régulière</span>

<span class="php-comment">// Contraintes numériques</span>
<span class="php-reserved">#[Assert\Range(min: 0, max: 100)]</span>      <span class="php-comment">// Valeur entre min et max</span>
<span class="php-reserved">#[Assert\Positive]</span>                     <span class="php-comment">// Nombre strictement positif</span>
<span class="php-reserved">#[Assert\GreaterThan(0)]</span>               <span class="php-comment">// Supérieur à une valeur</span>

<span class="php-comment">// Contraintes de choix</span>
<span class="php-reserved">#[Assert\Choice(choices: ['a', 'b'])]</span>  <span class="php-comment">// Valeur dans une liste</span>
<span class="php-reserved">#[Assert\Count(min: 1, max: 5)]</span>        <span class="php-comment">// Nombre d'éléments d'une collection</span>

<span class="php-comment">// Contraintes de date</span>
<span class="php-reserved">#[Assert\Date]</span>                         <span class="php-comment">// Format date valide (YYYY-MM-DD)</span>
<span class="php-reserved">#[Assert\DateTime]</span>                     <span class="php-comment">// Format datetime valide</span>
<span class="php-reserved">#[Assert\GreaterThanOrEqual('today')]</span>  <span class="php-comment">// Date dans le futur</span>

<span class="php-comment">// Contraintes de fichier</span>
<span class="php-reserved">#[Assert\File(
    maxSize: '2M',
    mimeTypes: ['image/jpeg', 'image/png']
)]</span>                                       <span class="php-comment">// Validation d'un fichier uploadé</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Template Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Affichage dans un Template Twig</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Rendu complet du formulaire</h3>
                    <div class="code-example">
                        <pre><code><span class="twig-comment">{# templates/article/new.html.twig #}</span>
<span class="twig-tag">{% extends 'base.html.twig' %}</span>

<span class="twig-tag">{% block body %}</span>
    <span class="twig-tag">{{ form_start(form) }}</span>

        <span class="twig-comment">{# Afficher tous les champs d'un coup (pratique en dev) #}</span>
        <span class="twig-tag">{{ form_widget(form) }}</span>

        <span class="twig-comment">{# --- OU --- Affichage personnalisé champ par champ #}</span>
        <span class="twig-tag">{{ form_row(form.titre) }}</span>
        <span class="twig-tag">{{ form_row(form.contenu) }}</span>
        <span class="twig-tag">{{ form_row(form.publishedAt) }}</span>

        <span class="twig-comment">{# Bouton submit personnalisé #}</span>
        &lt;button type=&quot;submit&quot; class=&quot;btn btn-primary&quot;&gt;
            Publier l'article
        &lt;/button&gt;

    <span class="twig-tag">{{ form_end(form) }}</span>
<span class="twig-tag">{% endblock %}</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Rendu personnalisé avec séparation label/widget/erreurs</h3>
                    <div class="code-example">
                        <pre><code><span class="twig-tag">{{ form_start(form, { 'attr': { 'class': 'needs-validation', 'novalidate': true }}) }}</span>

    &lt;div class=&quot;mb-3&quot;&gt;
        <span class="twig-comment">{# Label du champ #}</span>
        <span class="twig-tag">{{ form_label(form.titre, 'Titre', { 'label_attr': { 'class': 'form-label fw-bold' }}) }}</span>

        <span class="twig-comment">{# Input du champ #}</span>
        <span class="twig-tag">{{ form_widget(form.titre, { 'attr': { 'class': 'form-control' }}) }}</span>

        <span class="twig-comment">{# Affichage des erreurs #}</span>
        <span class="twig-tag">{% for error in form.titre.vars.errors %}</span>
            &lt;div class=&quot;text-danger small mt-1&quot;&gt;
                <span class="twig-tag">{{ error.message }}</span>
            &lt;/div&gt;
        <span class="twig-tag">{% endfor %}</span>
    &lt;/div&gt;

    &lt;div class=&quot;mb-3&quot;&gt;
        <span class="twig-tag">{{ form_label(form.contenu) }}</span>
        <span class="twig-tag">{{ form_widget(form.contenu, { 'attr': { 'class': 'form-control', 'rows': 6 }}) }}</span>
        <span class="twig-tag">{{ form_errors(form.contenu) }}</span>
    &lt;/div&gt;

    <span class="twig-comment">{# Champs cachés (token CSRF etc.) #}</span>
    <span class="twig-tag">{{ form_rest(form) }}</span>

<span class="twig-tag">{{ form_end(form) }}</span></code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Thèmes de formulaire disponibles</h3>
                    <div class="code-example">
                        <pre><code><span class="twig-comment">{# Appliquer un thème Bootstrap 5 sur un seul formulaire #}</span>
<span class="twig-tag">{% form_theme form 'bootstrap_5_layout.html.twig' %}</span>

<span class="twig-comment">{# Ou globalement dans config/packages/twig.yaml #}</span>
<span class="twig-comment"># twig:
#   form_themes:
#     - 'bootstrap_5_layout.html.twig'
#     - 'foundation_5_layout.html.twig'  # Alternative Foundation CSS
#     - 'form_div_layout.html.twig'      # Thème par défaut (divs)
#     - 'form_table_layout.html.twig'    # Thème tableau</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Fonctionnalités avancées -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Fonctionnalités Avancées</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Formulaire avec EntityType (relation Doctrine)</h3>
                    <div class="code-example">
                        <pre><code><span class="php-reserved">use</span> <span class="php-identifier">Symfony\Bridge\Doctrine\Form\Type\EntityType</span>;

<span class="php-variable">$builder</span>
    -><span class="php-function">add</span>(<span class="php-string">'categorie'</span>, <span class="php-class">EntityType</span>::<span class="php-reserved">class</span>, [
        <span class="php-string">'class'</span>        => <span class="php-class">Categorie</span>::<span class="php-reserved">class</span>,
        <span class="php-string">'choice_label'</span> => <span class="php-string">'nom'</span>,       <span class="php-comment">// Propriété à afficher dans &lt;option&gt;</span>
        <span class="php-string">'label'</span>        => <span class="php-string">'Catégorie'</span>,
        <span class="php-string">'placeholder'</span>  => <span class="php-string">'Choisissez une catégorie'</span>,
        <span class="php-string">'query_builder'</span> => <span class="php-reserved">function</span>(<span class="php-class">EntityRepository</span> <span class="php-variable">$repo</span>) {
            <span class="php-reserved">return</span> <span class="php-variable">$repo</span>-><span class="php-function">createQueryBuilder</span>(<span class="php-string">'c'</span>)
                -><span class="php-function">orderBy</span>(<span class="php-string">'c.nom'</span>, <span class="php-string">'ASC'</span>);
        },
    ])
    -><span class="php-function">add</span>(<span class="php-string">'tags'</span>, <span class="php-class">EntityType</span>::<span class="php-reserved">class</span>, [
        <span class="php-string">'class'</span>        => <span class="php-class">Tag</span>::<span class="php-reserved">class</span>,
        <span class="php-string">'choice_label'</span> => <span class="php-string">'nom'</span>,
        <span class="php-string">'multiple'</span>     => <span class="php-reserved">true</span>,   <span class="php-comment">// Sélection multiple</span>
        <span class="php-string">'expanded'</span>     => <span class="php-reserved">true</span>,   <span class="php-comment">// Affichage en checkboxes</span>
        <span class="php-string">'label'</span>        => <span class="php-string">'Tags'</span>,
    ]);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Formulaire de contact sans entité</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// src/Form/ContactType.php</span>
<span class="php-reserved">class</span> <span class="php-class">ContactType</span> <span class="php-reserved">extends</span> <span class="php-class">AbstractType</span>
{
    <span class="php-reserved">public function</span> <span class="php-function">buildForm</span>(<span class="php-class">FormBuilderInterface</span> <span class="php-variable">$builder</span>, <span class="php-reserved">array</span> <span class="php-variable">$options</span>): <span class="php-reserved">void</span>
    {
        <span class="php-variable">$builder</span>
            -><span class="php-function">add</span>(<span class="php-string">'nom'</span>, <span class="php-class">TextType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'constraints'</span> => [
                    <span class="php-reserved">new</span> <span class="php-class">Assert\NotBlank</span>(),
                    <span class="php-reserved">new</span> <span class="php-class">Assert\Length</span>([<span class="php-string">'min'</span> => <span class="php-number">2</span>]),
                ],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'email'</span>, <span class="php-class">EmailType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'constraints'</span> => [<span class="php-reserved">new</span> <span class="php-class">Assert\NotBlank</span>(), <span class="php-reserved">new</span> <span class="php-class">Assert\Email</span>()],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'sujet'</span>, <span class="php-class">ChoiceType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'choices'</span> => [
                    <span class="php-string">'Question générale'</span> => <span class="php-string">'general'</span>,
                    <span class="php-string">'Support technique'</span> => <span class="php-string">'support'</span>,
                    <span class="php-string">'Partenariat'</span>       => <span class="php-string">'partenariat'</span>,
                ],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'message'</span>, <span class="php-class">TextareaType</span>::<span class="php-reserved">class</span>);
    }

    <span class="php-reserved">public function</span> <span class="php-function">configureOptions</span>(<span class="php-class">OptionsResolver</span> <span class="php-variable">$resolver</span>): <span class="php-reserved">void</span>
    {
        <span class="php-comment">// Pas de data_class car pas d'entité liée</span>
        <span class="php-variable">$resolver</span>-><span class="php-function">setDefaults</span>([]);
    }
}

<span class="php-comment">// Récupérer les données dans le controller</span>
<span class="php-reserved">if</span> (<span class="php-variable">$form</span>-><span class="php-function">isSubmitted</span>() && <span class="php-variable">$form</span>-><span class="php-function">isValid</span>()) {
    <span class="php-variable">$data</span> = <span class="php-variable">$form</span>-><span class="php-function">getData</span>(); <span class="php-comment">// Retourne un tableau associatif</span>
    <span class="php-comment">// $data['nom'], $data['email'], $data['message']...</span>
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Upload de fichier</h3>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// Dans le FormType</span>
<span class="php-variable">$builder</span>-><span class="php-function">add</span>(<span class="php-string">'imageFile'</span>, <span class="php-class">FileType</span>::<span class="php-reserved">class</span>, [
    <span class="php-string">'label'</span>      => <span class="php-string">'Image (JPG ou PNG)'</span>,
    <span class="php-string">'mapped'</span>     => <span class="php-reserved">false</span>,  <span class="php-comment">// Non mappé sur l'entité</span>
    <span class="php-string">'required'</span>   => <span class="php-reserved">false</span>,
    <span class="php-string">'constraints'</span> => [
        <span class="php-reserved">new</span> <span class="php-class">Assert\File</span>([
            <span class="php-string">'maxSize'</span>       => <span class="php-string">'2M'</span>,
            <span class="php-string">'mimeTypes'</span>     => [<span class="php-string">'image/jpeg'</span>, <span class="php-string">'image/png'</span>, <span class="php-string">'image/webp'</span>],
            <span class="php-string">'mimeTypesMessage'</span> => <span class="php-string">'Veuillez uploader une image valide'</span>,
        ])
    ],
]);

<span class="php-comment">// Dans le controller</span>
<span class="php-variable">$imageFile</span> = <span class="php-variable">$form</span>-><span class="php-function">get</span>(<span class="php-string">'imageFile'</span>)-><span class="php-function">getData</span>();

<span class="php-reserved">if</span> (<span class="php-variable">$imageFile</span>) {
    <span class="php-variable">$newFilename</span> = <span class="php-function">uniqid</span>() . <span class="php-string">'.'</span> . <span class="php-variable">$imageFile</span>-><span class="php-function">guessExtension</span>();
    <span class="php-variable">$imageFile</span>-><span class="php-function">move</span>(
        <span class="php-variable">$this</span>-><span class="php-function">getParameter</span>(<span class="php-string">'uploads_directory'</span>),
        <span class="php-variable">$newFilename</span>
    );
    <span class="php-variable">$article</span>-><span class="php-function">setImageFilename</span>(<span class="php-variable">$newFilename</span>);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Sécurité CSRF -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Sécurité : Protection CSRF</h2>

                <div class="textExemple">
                    <p>
                        Symfony active automatiquement la protection CSRF (Cross-Site Request Forgery) sur tous les
                        formulaires.
                        Un token unique est généré et vérifié à chaque soumission, sans que vous ayez à le gérer
                        manuellement.
                    </p>
                    <div class="code-example">
                        <pre><code><span class="php-comment">// La protection CSRF est active par défaut
// Elle peut être désactivée si nécessaire (API publique par exemple)</span>
<span class="php-reserved">public function</span> <span class="php-function">configureOptions</span>(<span class="php-class">OptionsResolver</span> <span class="php-variable">$resolver</span>): <span class="php-reserved">void</span>
{
    <span class="php-variable">$resolver</span>-><span class="php-function">setDefaults</span>([
        <span class="php-string">'data_class'</span>      => <span class="php-class">Article</span>::<span class="php-reserved">class</span>,
        <span class="php-string">'csrf_protection'</span> => <span class="php-reserved">true</span>,     <span class="php-comment">// Activé par défaut</span>
        <span class="php-string">'csrf_field_name'</span> => <span class="php-string">'_token'</span>, <span class="php-comment">// Nom du champ caché</span>
        <span class="php-string">'csrf_token_id'</span>   => <span class="php-string">'article_item'</span>, <span class="php-comment">// Identifiant unique</span>
    ]);
}

<span class="php-comment">// Dans le template Twig, form_end() ajoute automatiquement le token :
// {{ form_end(form) }} → génère &lt;input type="hidden" name="_token" value="..."&gt;</span></code></pre>
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
                        <li>Email (requis, format valide, unique en BDD)</li>
                        <li>Mot de passe (requis, min 8 caractères, avec confirmation)</li>
                        <li>Date de naissance (requis, doit avoir au moins 18 ans)</li>
                        <li>Acceptation des CGU (checkbox obligatoire)</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code><span class="php-comment">// src/Form/RegistrationFormType.php</span>
<span class="php-reserved">use</span> <span class="php-identifier">Symfony\Component\Form\Extension\Core\Type\RepeatedType</span>;

<span class="php-reserved">class</span> <span class="php-class">RegistrationFormType</span> <span class="php-reserved">extends</span> <span class="php-class">AbstractType</span>
{
    <span class="php-reserved">public function</span> <span class="php-function">buildForm</span>(<span class="php-class">FormBuilderInterface</span> <span class="php-variable">$builder</span>, <span class="php-reserved">array</span> <span class="php-variable">$options</span>): <span class="php-reserved">void</span>
    {
        <span class="php-variable">$builder</span>
            -><span class="php-function">add</span>(<span class="php-string">'prenom'</span>, <span class="php-class">TextType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span> => <span class="php-string">'Prénom'</span>,
                <span class="php-string">'constraints'</span> => [
                    <span class="php-reserved">new</span> <span class="php-class">Assert\NotBlank</span>(),
                    <span class="php-reserved">new</span> <span class="php-class">Assert\Length</span>([<span class="php-string">'min'</span> => <span class="php-number">2</span>]),
                ],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'nom'</span>, <span class="php-class">TextType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span> => <span class="php-string">'Nom'</span>,
                <span class="php-string">'constraints'</span> => [
                    <span class="php-reserved">new</span> <span class="php-class">Assert\NotBlank</span>(),
                    <span class="php-reserved">new</span> <span class="php-class">Assert\Length</span>([<span class="php-string">'min'</span> => <span class="php-number">2</span>]),
                ],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'email'</span>, <span class="php-class">EmailType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'constraints'</span> => [<span class="php-reserved">new</span> <span class="php-class">Assert\NotBlank</span>(), <span class="php-reserved">new</span> <span class="php-class">Assert\Email</span>()],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'plainPassword'</span>, <span class="php-class">RepeatedType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'type'</span>            => <span class="php-class">PasswordType</span>::<span class="php-reserved">class</span>,
                <span class="php-string">'first_options'</span>   => [<span class="php-string">'label'</span> => <span class="php-string">'Mot de passe'</span>],
                <span class="php-string">'second_options'</span>  => [<span class="php-string">'label'</span> => <span class="php-string">'Confirmer le mot de passe'</span>],
                <span class="php-string">'invalid_message'</span> => <span class="php-string">'Les mots de passe doivent correspondre'</span>,
                <span class="php-string">'mapped'</span>          => <span class="php-reserved">false</span>,
                <span class="php-string">'constraints'</span>     => [
                    <span class="php-reserved">new</span> <span class="php-class">Assert\NotBlank</span>(),
                    <span class="php-reserved">new</span> <span class="php-class">Assert\Length</span>([<span class="php-string">'min'</span> => <span class="php-number">8</span>]),
                ],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'dateNaissance'</span>, <span class="php-class">DateType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>        => <span class="php-string">'Date de naissance'</span>,
                <span class="php-string">'widget'</span>       => <span class="php-string">'single_text'</span>,
                <span class="php-string">'constraints'</span>  => [
                    <span class="php-reserved">new</span> <span class="php-class">Assert\NotNull</span>(),
                    <span class="php-reserved">new</span> <span class="php-class">Assert\LessThanOrEqual</span>(<span class="php-string">'-18 years'</span>),
                ],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'agreeTerms'</span>, <span class="php-class">CheckboxType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>       => <span class="php-string">'J\'accepte les conditions d\'utilisation'</span>,
                <span class="php-string">'mapped'</span>      => <span class="php-reserved">false</span>,
                <span class="php-string">'constraints'</span> => [<span class="php-reserved">new</span> <span class="php-class">Assert\IsTrue</span>([
                    <span class="php-string">'message'</span> => <span class="php-string">'Vous devez accepter les CGU'</span>,
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
                            <pre><code><span class="php-comment">// src/Form/ProduitSearchType.php</span>
<span class="php-reserved">class</span> <span class="php-class">ProduitSearchType</span> <span class="php-reserved">extends</span> <span class="php-class">AbstractType</span>
{
    <span class="php-reserved">public function</span> <span class="php-function">buildForm</span>(<span class="php-class">FormBuilderInterface</span> <span class="php-variable">$builder</span>, <span class="php-reserved">array</span> <span class="php-variable">$options</span>): <span class="php-reserved">void</span>
    {
        <span class="php-variable">$builder</span>
            -><span class="php-function">add</span>(<span class="php-string">'recherche'</span>, <span class="php-class">SearchType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'required'</span>   => <span class="php-reserved">false</span>,
                <span class="php-string">'label'</span>      => <span class="php-string">'Rechercher un produit'</span>,
                <span class="php-string">'attr'</span>       => [<span class="php-string">'placeholder'</span> => <span class="php-string">'Nom, référence...'</span>],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'categorie'</span>, <span class="php-class">EntityType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'class'</span>        => <span class="php-class">Categorie</span>::<span class="php-reserved">class</span>,
                <span class="php-string">'choice_label'</span> => <span class="php-string">'nom'</span>,
                <span class="php-string">'required'</span>     => <span class="php-reserved">false</span>,
                <span class="php-string">'placeholder'</span>  => <span class="php-string">'Toutes les catégories'</span>,
            ])
            -><span class="php-function">add</span>(<span class="php-string">'prixMin'</span>, <span class="php-class">NumberType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>    => <span class="php-string">'Prix minimum (€)'</span>,
                <span class="php-string">'required'</span> => <span class="php-reserved">false</span>,
                <span class="php-string">'constraints'</span> => [<span class="php-reserved">new</span> <span class="php-class">Assert\PositiveOrZero</span>()],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'prixMax'</span>, <span class="php-class">NumberType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>    => <span class="php-string">'Prix maximum (€)'</span>,
                <span class="php-string">'required'</span> => <span class="php-reserved">false</span>,
                <span class="php-string">'constraints'</span> => [<span class="php-reserved">new</span> <span class="php-class">Assert\Positive</span>()],
            ])
            -><span class="php-function">add</span>(<span class="php-string">'tri'</span>, <span class="php-class">ChoiceType</span>::<span class="php-reserved">class</span>, [
                <span class="php-string">'label'</span>   => <span class="php-string">'Trier par'</span>,
                <span class="php-string">'choices'</span> => [
                    <span class="php-string">'Nom A → Z'</span>     => <span class="php-string">'nom_asc'</span>,
                    <span class="php-string">'Nom Z → A'</span>     => <span class="php-string">'nom_desc'</span>,
                    <span class="php-string">'Prix croissant'</span> => <span class="php-string">'prix_asc'</span>,
                    <span class="php-string">'Plus récent'</span>   => <span class="php-string">'date_desc'</span>,
                ],
                <span class="php-string">'required'</span> => <span class="php-reserved">false</span>,
            ]);
    }

    <span class="php-reserved">public function</span> <span class="php-function">configureOptions</span>(<span class="php-class">OptionsResolver</span> <span class="php-variable">$resolver</span>): <span class="php-reserved">void</span>
    {
        <span class="php-variable">$resolver</span>-><span class="php-function">setDefaults</span>([
            <span class="php-string">'method'</span> => <span class="php-string">'GET'</span>, <span class="php-comment">// Formulaire de recherche → méthode GET</span>
            <span class="php-string">'csrf_protection'</span> => <span class="php-reserved">false</span>, <span class="php-comment">// Pas de CSRF pour les GET</span>
        ]);
    }

    <span class="php-comment">// Dans le controller :</span>
    <span class="php-comment">// $form = $this->createForm(ProduitSearchType::class);
    // $form->handleRequest($request);
    // $data = $form->getData(); // Utiliser $data pour filtrer le repository</span>
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
                        <li><strong>Un FormType par formulaire</strong> : évitez les FormTypes "fourre-tout"</li>
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
                        <li>Pré-remplir les formulaires d'édition en passant l'entité existante à createForm()</li>
                        <li>Afficher les erreurs au plus près du champ concerné</li>
                        <li>Ajouter des <code>placeholder</code> et <code>help</code> clairs pour guider l'utilisateur
                        </li>
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
                        son traitement (Controller) et son affichage (Twig) pour respecter le principe de séparation des
                        responsabilités.
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
    name: 'SymfonyFormLesson'
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

/* COULEURS PHP / SYMFONY */
.php-reserved {
    color: #FF6B8B !important;
    font-weight: bold;
}

.php-class {
    color: #4EC9B0 !important;
    font-weight: bold;
}

.php-function {
    color: #DCDCAA !important;
}

.php-identifier {
    color: #9CDCFE !important;
}

.php-variable {
    color: #9CDCFE !important;
}

.php-string {
    color: #CE9178 !important;
}

.php-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.php-number {
    color: #B5CEA8 !important;
}

/* COULEURS TWIG */
.twig-tag {
    color: #FF6B8B !important;
    font-weight: bold;
}

.twig-comment {
    color: #6A9955 !important;
    font-style: italic;
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

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
}

/* Responsive */
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
</style>