<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Créer un Jeu de Cartes avec Symfony</h1>
                <p class="lesson-meta text-white">Étape 1 • PHP • Symfony • Session • Form Component</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction : Construire un Jeu de Cartes pas à pas</h2>
                <p class="textExemple">
                    Dans cette série de leçons, nous allons construire un jeu de cartes complet avec Symfony,
                    en partant de zéro et en avançant étape par étape, exactement comme dans un vrai projet.
                </p>
                <p class="textExemple">
                    Cette première leçon se concentre sur la <strong>première brique</strong> du jeu : l'écran
                    de démarrage qui permet d'enregistrer les joueurs avant de lancer une partie. Pour aller vite
                    et garder les choses simples au départ, les joueurs ne sont <strong>pas stockés en base de
                    données</strong> mais directement en <strong>session</strong>. On pourra brancher Doctrine plus tard
                    sans changer le reste de l'architecture.
                </p>
                <p class="textExemple">
                    À la fin de cette leçon, vous saurez : ajouter un joueur via un formulaire, afficher la liste
                    des joueurs enregistrés, supprimer un joueur, vider la liste, et bloquer le lancement de la
                    partie tant qu'un nombre minimum de joueurs n'est pas atteint.
                </p>
            </section>

            <!-- Architecture -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture de l'écran de démarrage</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Les 4 briques que l'on va créer</h3>
                    <ul>
                        <li><strong>Player (Entity)</strong> : une classe simple représentant un joueur (juste un nom)</li>
                        <li><strong>PlayerType (FormType)</strong> : le formulaire d'ajout d'un joueur</li>
                        <li><strong>PlayerManager (Service)</strong> : gère la liste des joueurs en session (ajout, suppression, comptage)</li>
                        <li><strong>StartController (Controller)</strong> : expose les routes et fait le lien entre tout ça et le Twig</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Schéma de fonctionnement</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">Utilisateur          StartController         PlayerManager          Session
    │                      │                       │                    │
    │ ── GET / ──────────→ │                       │                    │
    │                      │ ── getPlayers() ────→ │ ── get('players') ─→
    │                      │ ←── Player[] ───────── │ ←──────────────────
    │ ←── Liste affichée ── │                       │                    │
    │                      │                       │                    │
    │ ── POST / (nom) ───→ │                       │                    │
    │                      │ ── isValid() ────────  Validation Form     │
    │                      │ ── addPlayer($name) → │ ── set('players') ─→
    │                      │ ←── redirect (PRG) ─── │                    │</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">📌 Pourquoi la session plutôt que la base de données ?</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Pour un jeu local "sur canapé" (tout le monde joue depuis le même navigateur), la session
                            suffit largement : les joueurs n'ont pas besoin d'être persistés entre deux parties.
                            C'est aussi l'occasion d'apprendre à manipuler la <code>SessionInterface</code> de Symfony
                            sans dépendre de Doctrine. On pourra remplacer <code>PlayerManager</code> par une version
                            "base de données" plus tard, sans toucher au Controller ni au Twig.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Prérequis -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Prérequis</h2>

                <div class="textExemple">
                    <p>
                        On part du principe que vous avez déjà un projet Symfony fonctionnel (webapp) avec le
                        composant Form, Twig et Bootstrap 5 disponibles. Si ce n'est pas le cas :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash"># Composants nécessaires pour cette leçon
composer require symfony/form
composer require symfony/twig-bundle
composer require symfony/validator

# Pour le rendu Bootstrap 5 utilisé dans le template
composer require symfony/twig-extra-bundle</code></pre>
                    </div>
                    <p class="textExemple">
                        Aucune entité Doctrine n'est nécessaire pour cette leçon : pas de base de données,
                        pas de migration, on reste 100% en mémoire de session.
                    </p>
                </div>
            </section>

            <!-- Etape 1 : Entity Player -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : L'entité Player</h2>

                <div class="textExemple">
                    <p>
                        On commence par le plus simple : une classe PHP "normale", sans annotation Doctrine,
                        qui représente un joueur. Elle ne contient pour l'instant qu'un nom.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Entity/Player.php
namespace App\Entity;

class Player
{
    private string $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function setName(string $name): self
    {
        $this->name = $name;
        return $this;
    }
}</code></pre>
                    </div>
                    <p class="textExemple">
                        Cette classe n'est <strong>pas liée à Doctrine</strong> : c'est un simple objet PHP (POPO).
                        Elle va quand même nous servir de <code>data_class</code> pour notre formulaire, exactement
                        comme on le ferait avec une vraie entité.
                    </p>
                </div>
            </section>

            <!-- Etape 2 : FormType -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Le formulaire PlayerType</h2>

                <div class="textExemple">
                    <p>
                        Un formulaire minimal avec un seul champ texte : le nom du joueur.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/PlayerType.php
namespace App\Form;

use App\Entity\Player;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class PlayerType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('name', TextType::class, [
                'label' => 'Nom du joueur',
                'attr'  => ['placeholder' => 'Entrez un nom', 'autofocus' => true],
            ]);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => Player::class,
        ]);
    }
}</code></pre>
                    </div>
                    <p class="textExemple">
                        Le <code>data_class</code> indique à Symfony de remplir un objet <code>Player</code>
                        avec les données soumises. Pas besoin de gérer la validation ici pour l'instant :
                        elle sera gérée côté <code>PlayerManager</code> (on filtre les noms vides et les doublons).
                    </p>
                </div>
            </section>

            <!-- Etape 3 : Service PlayerManager -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Le service PlayerManager</h2>

                <div class="textExemple">
                    <p>
                        C'est le cœur de cette leçon : un service qui centralise toute la logique de gestion
                        des joueurs en session. Le Controller ne touchera jamais directement à la session,
                        il passera toujours par ce service.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Service/PlayerManager.php
namespace App\Service;

use App\Entity\Player;
use Symfony\Component\HttpFoundation\RequestStack;
use Symfony\Component\HttpFoundation\Session\SessionInterface;

class PlayerManager
{
    private SessionInterface $session;
    private const SESSION_KEY = 'players';

    public function __construct(RequestStack $requestStack)
    {
        $this->session = $requestStack->getSession();
    }

    /**
     * @return Player[]
     */
    public function getPlayers(): array
    {
        $data = $this->session->get(self::SESSION_KEY, []);
        return array_map(fn(string $name) => new Player($name), $data);
    }

    public function getPlayerCount(): int
    {
        return count($this->session->get(self::SESSION_KEY, []));
    }

    public function addPlayer(string $name): void
    {
        $players = $this->session->get(self::SESSION_KEY, []);
        $name = trim($name);

        if ($name === '') {
            return;
        }

        // Évite les doublons (si vous voulez autoriser les doublons, retirez cette condition)
        if (!in_array($name, $players, true)) {
            $players[] = $name;
            $this->session->set(self::SESSION_KEY, $players);
        }
    }

    public function removePlayer(string $name): void
    {
        $players = $this->session->get(self::SESSION_KEY, []);
        $players = array_values(array_filter($players, fn($p) => $p !== $name));
        $this->session->set(self::SESSION_KEY, $players);
    }

    public function clearPlayers(): void
    {
        $this->session->remove(self::SESSION_KEY);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">🔍 Pourquoi RequestStack et pas SessionInterface directement ?</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Injecter <code>SessionInterface</code> directement dans un service peut poser des
                            problèmes si le service est instancié avant qu'une requête HTTP n'existe (par exemple
                            en CLI). <code>RequestStack</code> permet de récupérer la session de façon paresseuse,
                            au moment où on en a réellement besoin, via <code>getSession()</code>.
                        </p>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Pourquoi on stocke des <em>noms</em> et pas des objets Player en session ?</h3>
                    <p>
                        On stocke un simple tableau de chaînes (<code>string[]</code>) en session plutôt que des
                        objets <code>Player</code>. C'est plus simple à sérialiser, et on reconstruit les objets
                        <code>Player</code> à la volée dans <code>getPlayers()</code>. Cela évite aussi les soucis
                        de désérialisation si la classe <code>Player</code> évolue entre deux requêtes.
                    </p>
                </div>
            </section>

            <!-- Etape 4 : Controller -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4 : Le StartController</h2>

                <div class="textExemple">
                    <p>
                        Le controller expose 4 routes : l'affichage/ajout (<code>/</code>), la suppression d'un
                        joueur, le vidage de la liste, et le lancement de la partie (avec garde-fou sur le
                        nombre minimum de joueurs).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Controller/StartController.php
namespace App\Controller;

use App\Form\PlayerType;
use App\Entity\Player;
use App\Service\PlayerManager;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class StartController extends AbstractController
{
    private const MIN_PLAYERS = 2; // Nombre minimum de joueurs requis

    #[Route('/', name: 'game_start')]
    public function start(Request $request, PlayerManager $playerManager): Response
    {
        $player = new Player('');
        $form = $this->createForm(PlayerType::class, $player);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            $playerManager->addPlayer($player->getName());
            return $this->redirectToRoute('game_start');
        }

        $players = $playerManager->getPlayers();
        $playerCount = $playerManager->getPlayerCount();

        return $this->render('start/index.html.twig', [
            'form' => $form->createView(),
            'players' => $players,
            'playerCount' => $playerCount,
            'canStart' => $playerCount >= self::MIN_PLAYERS,
            'minPlayers' => self::MIN_PLAYERS,
        ]);
    }

    #[Route('/player/remove/{name}', name: 'game_player_remove')]
    public function removePlayer(string $name, PlayerManager $playerManager): Response
    {
        $playerManager->removePlayer($name);
        return $this->redirectToRoute('game_start');
    }

    #[Route('/game/clear', name: 'game_clear')]
    public function clear(PlayerManager $playerManager): Response
    {
        $playerManager->clearPlayers();
        return $this->redirectToRoute('game_start');
    }

    #[Route('/game', name: 'game_play')]
    public function play(PlayerManager $playerManager): Response
    {
        // Sécurité : on vérifie que le nombre minimum est atteint
        if ($playerManager->getPlayerCount() < self::MIN_PLAYERS) {
            $this->addFlash('warning', 'Vous devez avoir au moins ' . self::MIN_PLAYERS . ' joueurs pour commencer.');
            return $this->redirectToRoute('game_start');
        }

        $players = $playerManager->getPlayers();

        return $this->render('game/index.html.twig', [
            'players' => $players,
        ]);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">⚠️ Le pattern Post/Redirect/Get (PRG), encore une fois</h3>
                    <div class="warning-section">
                        <h4 class="text-purple">Pourquoi on redirige systématiquement vers game_start</h4>
                        <p>
                            Que ce soit après l'ajout d'un joueur, sa suppression, ou le vidage de la liste,
                            on redirige <strong>toujours</strong> vers <code>game_start</code> plutôt que de
                            rendre directement un template. Cela évite qu'un rechargement de page (F5)
                            ne ré-ajoute le même joueur ou ne relance une action déjà effectuée.
                        </p>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Le garde-fou sur la route /game</h3>
                    <p>
                        Même si le bouton "Début de la partie" n'est affiché que lorsque
                        <code>canStart</code> est vrai côté Twig, rien n'empêche un utilisateur de taper
                        directement l'URL <code>/game</code> dans son navigateur. C'est pourquoi la vérification
                        du nombre minimum de joueurs est <strong>refaite côté serveur</strong>, dans la méthode
                        <code>play()</code>. Ne jamais faire confiance uniquement à l'affichage côté client.
                    </p>
                </div>
            </section>

            <!-- Etape 5 : Template Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 5 : Le template Twig</h2>

                <div class="textExemple">
                    <p>
                        Enfin, le template qui affiche le formulaire d'ajout, la liste des joueurs déjà
                        enregistrés, et les actions (démarrer / vider la liste).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/start/index.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
&lt;div class="container mt-4"&gt;
    &lt;h1&gt;Bienvenue sur le jeu&lt;/h1&gt;
    &lt;p&gt;Ajoutez au moins &lt;strong&gt;{{ minPlayers }}&lt;/strong&gt; joueurs pour commencer.&lt;/p&gt;

    {# Formulaire d'ajout #}
    {{ form_start(form) }}
    &lt;div class="row g-3 align-items-end"&gt;
        &lt;div class="col-auto"&gt;
            {{ form_row(form.name) }}
        &lt;/div&gt;
        &lt;div class="col-auto"&gt;
            &lt;button type="submit" class="btn btn-primary"&gt;Ajouter joueur&lt;/button&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    {{ form_end(form) }}

    &lt;hr&gt;

    {# Liste des joueurs #}
    &lt;h2&gt;Joueurs inscrits ({{ playerCount }})&lt;/h2&gt;
    &lt;ul class="list-group mb-3" style="max-width: 400px;"&gt;
        {% for player in players %}
        &lt;li class="list-group-item d-flex justify-content-between align-items-center"&gt;
            {{ player.name }}
            &lt;a href="{{ path('game_player_remove', { name: player.name }) }}" class="btn btn-sm btn-outline-danger"
                onclick="return confirm('Supprimer {{ player.name }} ?')"&gt;
                Supprimer Joueur
            &lt;/a&gt;
        &lt;/li&gt;
        {% else %}
        &lt;li class="list-group-item text-muted"&gt;Aucun joueur enregistré pour l'instant.&lt;/li&gt;
        {% endfor %}
    &lt;/ul&gt;

    {# Actions (bouton Démarrer / Vider) #}
    &lt;div class="d-flex gap-2"&gt;
        {% if canStart %}
        &lt;a href="{{ path('game_play') }}" class="btn btn-success btn-lg"&gt;
            Début de la partie !
        &lt;/a&gt;
        {% else %}
        &lt;button class="btn btn-secondary btn-lg" disabled&gt;
            Ajoutez {{ minPlayers - playerCount }} joueur(s) supplémentaire(s)
        &lt;/button&gt;
        {% endif %}

        {% if players|length > 0 %}
        &lt;a href="{{ path('game_clear') }}" class="btn btn-outline-secondary"
            onclick="return confirm('Vider toute la liste ?')"&gt;
            Supprimer toute la liste de joueur
        &lt;/a&gt;
        {% endif %}
    &lt;/div&gt;
&lt;/div&gt;
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Détails utiles sur ce template</h3>
                    <ul>
                        <li><code>{% else %}</code> dans une boucle <code>for</code> : s'exécute uniquement si la liste est vide, pratique pour afficher un message par défaut sans condition séparée</li>
                        <li><code>path('game_player_remove', { name: player.name })</code> génère l'URL en injectant le paramètre de route directement</li>
                        <li><code>onclick="return confirm(...)"</code> ajoute une confirmation JS simple avant une action destructive, en attendant une vraie modale plus tard</li>
                        <li>Le bouton "Début de la partie" est <code>disabled</code> tant que <code>canStart</code> est faux, mais on a vu plus haut que le Controller protège aussi la route côté serveur</li>
                    </ul>
                </div>
            </section>

            <!-- Récap / flux complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récapitulatif du flux complet</h2>
                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">1. L'utilisateur arrive sur "/" → StartController::start()
2. Il soumet le formulaire → PlayerType valide les données
3. PlayerManager::addPlayer() ajoute le nom en session (si non vide, non doublon)
4. Redirection vers "/" (pattern PRG)
5. La liste des joueurs est rechargée depuis la session
6. Dès que playerCount >= MIN_PLAYERS, le bouton "Démarrer" devient actif
7. Clic sur "Démarrer" → StartController::play() revérifie le minimum côté serveur
8. Si OK → game/index.html.twig avec la liste des joueurs</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Ce qu'on a appliqué dans cette leçon</h3>
                    <ul>
                        <li><strong>Séparation des responsabilités</strong> : le Controller ne connaît pas la session, il délègue tout à <code>PlayerManager</code></li>
                        <li><strong>Pattern PRG</strong> : chaque action qui modifie l'état redirige plutôt que de rendre une vue</li>
                        <li><strong>Sécurité côté serveur</strong> : le nombre minimum de joueurs est vérifié dans le Controller, pas seulement dans le Twig</li>
                        <li><strong>Service réutilisable</strong> : en injectant <code>PlayerManager</code> via le constructeur, il pourra être réutilisé partout (autres controllers, commandes CLI, etc.)</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Limites actuelles (et pourquoi c'est normal)</h3>
                    <ul>
                        <li>Les joueurs sont perdus si l'utilisateur vide ses cookies ou change de navigateur : normal, c'est de la session, pas de la persistance</li>
                        <li>Pas de gestion multi-table / multi-room : pour l'instant, une session = une partie</li>
                        <li>Pas encore de logique de jeu (cartes, tours, scores) : ce sera l'objet des prochaines leçons</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Vous avez maintenant un écran de démarrage fonctionnel, avec ajout, suppression et
                        vidage de la liste des joueurs, sans aucune base de données. L'architecture en couches
                        (Entity / FormType / Service / Controller / Twig) que vous venez de mettre en place
                        est exactement la même que celle utilisée dans une application Symfony avec Doctrine :
                        seul le contenu du <code>PlayerManager</code> changera le jour où vous voudrez persister
                        les joueurs.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyPlayerSystemLesson',

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