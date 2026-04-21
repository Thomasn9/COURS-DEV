<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Domain-Driven Design (DDD)</h1>
                <p class="lesson-meta text-white">DDD • Modélisation • Architecture logicielle • Domain</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le Domain-Driven Design ?</h2>
                <p class="textExemple">
                    Le Domain-Driven Design est une approche de conception logicielle centrée sur le domaine métier.
                    Proposé par Eric Evans dans son livre éponyme (2003), le DDD propose de modéliser le logiciel en
                    partant de la réalité du métier, en collaboration étroite avec les experts du domaine.
                </p>
                <p class="textExemple">
                    L'objectif est de créer un langage commun (ubiquitous language) entre les développeurs et les métiers,
                    et de structurer le code autour des concepts métiers plutôt qu'autour de considérations techniques.
                </p>
            </section>

            <!-- Pourquoi DDD ? -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi adopter le DDD ?</h2>
                <ul class="textExemple">
                    <li><strong>Complexité maîtrisée</strong> : le DDD est conçu pour les domaines complexes, où les règles métiers sont nombreuses et évolutives.</li>
                    <li><strong>Alignement métier-code</strong> : le code reflète directement le vocabulaire et les concepts du métier.</li>
                    <li><strong>Maintenabilité</strong> : un modèle clair et bien délimité facilite les évolutions.</li>
                    <li><strong>Réduction des bugs</strong> : les règles métiers sont centralisées dans le domaine, pas noyées dans les contrôleurs ou les vues.</li>
                    <li><strong>Communication améliorée</strong> : le langage ubiquitaire permet aux équipes techniques et métier de se comprendre.</li>
                </ul>
            </section>

            <!-- Les blocs de base du DDD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les concepts fondamentaux</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Langage ubiquitaire (Ubiquitous Language)</h3>
                    <p>
                        C'est le vocabulaire commun, rigoureusement défini, utilisé à la fois par les experts métier,
                        les développeurs et dans le code. Un même terme a la même signification partout.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Le terme "Client" a la même définition dans les discussions, la documentation, et le code
public class Client {
    private ClientId id;
    private Nom nom;
    private Adresse adresse;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Contexte délimité (Bounded Context)</h3>
                    <p>
                        Un contexte délimité est une frontière explicite à l'intérieur de laquelle un modèle de domaine
                        est défini et cohérent. Chaque contexte a son propre langage ubiquitaire.
                    </p>
                    <p><strong>Exemple :</strong> Dans une application e-commerce, on peut avoir :</p>
                    <ul>
                        <li>Contexte <strong>Vente</strong> : panier, commande, paiement.</li>
                        <li>Contexte <strong>Livraison</strong> : transporteur, colis, adresse de livraison.</li>
                        <li>Contexte <strong>Catalogue</strong> : produit, prix, stock.</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Entité (Entity)</h3>
                    <p>
                        Une entité possède une identité propre qui persiste dans le temps, indépendamment de ses attributs.
                        Exemple : un <code>Client</code>, une <code>Commande</code>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Commande {
    private CommandeId id;        // Identité unique
    private LocalDateTime date;
    private StatutCommande statut;

    // L'égalité se base sur l'identifiant, pas sur les attributs
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Commande)) return false;
        Commande commande = (Commande) o;
        return id.equals(commande.id);
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">4. Objet de valeur (Value Object)</h3>
                    <p>
                        Un objet de valeur n'a pas d'identité propre ; il est défini par ses attributs.
                        Deux objets de valeur avec les mêmes attributs sont considérés comme égaux.
                        Ils sont immuables.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class Adresse {
    private final String rue;
    private final String ville;
    private final String codePostal;

    // constructeur, getters
    @Override
    public boolean equals(Object o) {
        // compare rue, ville, codePostal
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">5. Agrégat (Aggregate)</h3>
                    <p>
                        Un agrégat est un cluster d'entités et d'objets de valeur traités comme une unité cohérente.
                        Il possède une racine d'agrégat (aggregate root) qui est l'entité principale et contrôle l'accès aux membres internes.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// La racine d'agrégat est Commande
public class Commande {
    private List&lt;LigneCommande&gt; lignes;  // entités internes
    private Adresse adresseLivraison;    // value object

    // La racine expose des méthodes métier
    public void ajouterProduit(Produit produit, int quantite) {
        // validation, calculs, etc.
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">6. Événement de domaine (Domain Event)</h3>
                    <p>
                        Un événement de domaine représente un fait significatif qui s'est produit dans le domaine.
                        Il est utilisé pour communiquer entre agrégats ou pour déclencher des traitements asynchrones.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class CommandeValidee implements DomainEvent {
    private final CommandeId commandeId;
    private final LocalDateTime dateValidation;
    private final Montant total;
    // constructeur, getters
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">7. Repository</h3>
                    <p>
                        Un repository est un mécanisme de persistance qui donne l'illusion d'une collection en mémoire
                        pour les agrégats. Il isole le domaine de la couche technique (base de données).
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public interface CommandeRepository {
    Commande findById(CommandeId id);
    void save(Commande commande);
    void delete(Commande commande);
}

// Implémentation technique (Doctrine, JPA, etc.) séparée</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">8. Service de domaine (Domain Service)</h3>
                    <p>
                        Un service de domaine contient une logique métier qui n'appartient naturellement à aucune entité
                        ou objet de valeur. Il est sans état et porte un nom explicite dans le langage ubiquitaire.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public interface TarificationService {
    Montant calculerFraisDePort(Commande commande);
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">9. Application Service (ou Use Case)</h3>
                    <p>
                        Le service d'application orchestre les opérations : il récupère les agrégats via des repositories,
                        appelle les méthodes métier, gère les transactions et publie les événements.
                        Il ne contient <strong>aucune logique métier</strong>.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class PasserCommandeService {
    private final CommandeRepository commandeRepository;
    private final PanierRepository panierRepository;
    private final DomainEventPublisher eventPublisher;

    public void passerCommande(ClientId clientId) {
        Panier panier = panierRepository.findByClient(clientId);
        Commande commande = panier.transformEnCommande();
        commandeRepository.save(commande);
        eventPublisher.publish(new CommandeValidee(commande.getId()));
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">10. Fabrique (Factory)</h3>
                    <p>
                        Une fabrique encapsule la création d'objets complexes (agrégats, entités, value objects).
                        Elle peut être une méthode statique, une classe séparée ou une méthode sur la racine d'agrégat.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">public class CommandeFactory {
    public static Commande creerCommande(Client client, Panier panier) {
        // logique complexe de création
        return new Commande(...);
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Architecture hexagonale / couches DDD -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Architecture typique d'un projet DDD</h2>
                <div class="textExemple">
                    <p>
                        Le DDD est souvent associé à une architecture en couches ou à l'architecture hexagonale (ports & adapters).
                        Voici une organisation classique :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-text">src/
├── Domain/                # Cœur métier (pas de dépendances externes)
│   ├── Entity/
│   ├── ValueObject/
│   ├── Aggregate/
│   ├── Repository/        # Interfaces
│   ├── Service/           # Domain services
│   └── Event/
├── Application/           # Use cases, services applicatifs
│   ├── Command/
│   ├── Query/
│   └── Handler/
├── Infrastructure/        # Implémentations techniques
│   ├── Persistence/       # Implémentation des repositories
│   ├── Messaging/         # Event bus, etc.
│   └── Api/               # Clients externes
└── Interface/             # Contrôleurs, CLI, API
    ├── Web/
    └── Console/</code></pre>
                    </div>
                    <p>
                        Le <strong>Domain</strong> ne doit dépendre d'aucune couche externe (pas de framework, pas de base de données).
                        L'<strong>Application</strong> peut dépendre du Domain mais pas de l'Infrastructure (principe d'inversion des dépendances).
                    </p>
                </div>
            </section>

            <!-- Stratégies tactiques et stratégiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">DDD stratégique vs DDD tactique</h2>
                <div class="textExemple">
                    <p><strong>DDD stratégique</strong> : modélisation à grande échelle.</p>
                    <ul>
                        <li>Contexte délimité (Bounded Context)</li>
                        <li>Cartographie des contextes (Context Mapping) : relations entre contextes (partenariat, conformité, anticorruption layer, etc.)</li>
                        <li>Langage ubiquitaire</li>
                    </ul>
                    <p><strong>DDD tactique</strong> : implémentation concrète.</p>
                    <ul>
                        <li>Entités, objets de valeur, agrégats, événements de domaine</li>
                        <li>Repositories, services de domaine, fabriques</li>
                        <li>Services applicatifs</li>
                    </ul>
                </div>
            </section>

            <!-- Avantages et inconvénients -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Avantages et défis du DDD</h2>
                <div class="textExemple">
                    <h3 class="text-purple">✅ Avantages</h3>
                    <ul>
                        <li>Le code reflète le métier, ce qui le rend compréhensible par les non-développeurs.</li>
                        <li>Les règles métiers sont centralisées, testables et évolutives.</li>
                        <li>Réduction des bugs liés à une mauvaise compréhension du domaine.</li>
                        <li>Meilleure collaboration entre métier et IT.</li>
                        <li>Adapté aux systèmes complexes et en évolution constante.</li>
                    </ul>
                </div>
                <div class="textExemple">
                    <h3 class="text-purple">⚠️ Défis</h3>
                    <ul>
                        <li>Courbe d'apprentissage élevée.</li>
                        <li>Nécessite une collaboration forte avec les experts métier.</li>
                        <li>Peut être overkill pour des applications simples (CRUD).</li>
                        <li>Complexité initiale de mise en place.</li>
                        <li>Difficile à appliquer sur des projets legacy sans refonte importante.</li>
                    </ul>
                </div>
            </section>

            <!-- DDD et autres approches -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">DDD dans l'écosystème actuel</h2>
                <div class="textExemple">
                    <p>Le DDD s'intègre bien avec :</p>
                    <ul>
                        <li><strong>Event Sourcing</strong> : stocker l'état sous forme d'événements de domaine.</li>
                        <li><strong>CQRS</strong> (Command Query Responsibility Segregation) : séparer les commandes (mises à jour) des requêtes (lectures).</li>
                        <li><strong>Microservices</strong> : chaque microservice est un contexte délimité.</li>
                        <li><strong>Hexagonal Architecture</strong> : isole le domaine des détails techniques.</li>
                    </ul>
                </div>
            </section>

            <!-- Exemple concret -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple simplifié : système de réservation de billets</h2>
                <div class="textExemple">
                    <p><strong>Contexte délimité</strong> : Réservation</p>
                    <p><strong>Langage ubiquitaire</strong> : "spectacle", "représentation", "place", "réservation", "client", "paiement"</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// Entité (racine d'agrégat)
public class Reservation {
    private ReservationId id;
    private ClientId client;
    private Representation representation;
    private Set&lt;Place&gt; places;  // objets de valeur
    private StatutReservation statut;

    public void confirmer() {
        if (statut != StatutReservation.EN_ATTENTE) {
            throw new DomainException("Réservation non confirmable");
        }
        this.statut = StatutReservation.CONFIRMEE;
        DomainEventPublisher.publish(new ReservationConfirmee(this.id));
    }
}

// Objet de valeur
public class Place {
    private final int rang;
    private final int numero;
    // equals, hashCode, immuable
}

// Repository
public interface ReservationRepository {
    Reservation findById(ReservationId id);
    void save(Reservation reservation);
}

// Service applicatif
public class ConfirmerReservationService {
    private final ReservationRepository repo;
    public void confirmer(ReservationId id) {
        Reservation reservation = repo.findById(id);
        reservation.confirmer();
        repo.save(reservation);
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques DDD</h2>
                <ul class="textExemple">
                    <li><strong>Commencez par le langage ubiquitaire</strong> : faites des ateliers avec les experts métier.</li>
                    <li><strong>Identifiez les contextes délimités</strong> en repérant les termes qui changent de sens.</li>
                    <li><strong>Protégez les invariants</strong> dans les agrégats (ne laissez pas les services applicatifs les violer).</li>
                    <li><strong>Favorisez les objets de valeur</strong> au maximum ; ils réduisent la complexité.</li>
                    <li><strong>Limitez la taille des agrégats</strong> pour des performances et une cohérence transactionnelle acceptables.</li>
                    <li><strong>Utilisez des événements de domaine</strong> pour découpler les agrégats entre eux.</li>
                    <li><strong>Gardez le domaine pur</strong> (sans dépendance technique).</li>
                    <li><strong>Testez unitairement le domaine</strong> (entités, services, valeur objets) sans infrastructure.</li>
                </ul>
            </section>

            <!-- Ressources et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pour aller plus loin</h2>
                <div class="textExemple">
                    <p><strong>Livres essentiels :</strong></p>
                    <ul>
                        <li><em>Domain-Driven Design: Tackling Complexity in the Heart of Software</em> – Eric Evans</li>
                        <li><em>Implementing Domain-Driven Design</em> – Vaughn Vernon</li>
                        <li><em>Patterns, Principles and Practices of Domain-Driven Design</em> – Scott Millett</li>
                    </ul>
                    <p><strong>Ressources en ligne :</strong></p>
                    <ul>
                        <li>Domain-Driven Design Community (dddcommunity.org)</li>
                        <li>EventStorming (méthode de modélisation collaborative)</li>
                        <li>Domain Language (site d'Eric Evans)</li>
                    </ul>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Le Domain-Driven Design est une approche puissante pour maîtriser la complexité métier.
                    Il ne s'agit pas d'un framework ou d'une bibliothèque, mais d'un ensemble de principes et de patterns
                    qui placent le cœur du métier au centre du développement.
                </p>
                <p class="textExemple">
                    Bien que son adoption demande un investissement initial important (formation, collaboration),
                    il apporte une valeur considérable sur le long terme pour les systèmes complexes et stratégiques.
                </p>
                <p class="textExemple">
                    Commencez modestement : identifiez un sous-domaine clé, modélisez-le avec les experts, implémentez
                    un agrégat, et itérez. Le DDD n'est pas une fin en soi, mais un moyen de créer un logiciel qui
                    vit et respire avec le métier qu'il sert.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'DomainDrivenDesignLesson',

    mounted() {
        const loadHighlightJS = () => {
            return new Promise((resolve) => {
                if (window.hljs) { resolve(); return; }

                const link = document.createElement('link');
                link.rel = 'stylesheet';
                link.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/vs2015.min.css';
                document.head.appendChild(link);

                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js';
                script.onload = () => {
                    const languages = ['java', 'text'];
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
/* === Styles identiques aux leçons précédentes === */
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