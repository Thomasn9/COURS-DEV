<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Décorateurs et Annotations dans Spring Boot</h1>
        <div class="lesson-meta text-white">
          Leçon 3 • Java Annotations • Mapping ORM avec Spring Data JPA
        </div>
      </header>

      <!-- Introduction aux annotations -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Introduction aux Annotations en Java</h2>
        <p class="textExemple">
          Les annotations en Java sont des métadonnées qui fournissent des informations supplémentaires au compilateur, à la JVM ou à des frameworks comme Spring Boot. Elles commencent toujours par le symbole <code>@</code> et sont placées au-dessus des classes, méthodes, variables ou paramètres.
        </p>
        
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Sans annotations</h4>
            <pre><code>
<span class="comment">// Configuration manuelle et verbeuse</span>
<span class="comment">// Beaucoup de code "boilerplate"</span>
<span class="comment">// Difficulté de maintenance</span>

<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="keyword">private</span> Long id;
    <span class="keyword">private</span> String nom;
    
    <span class="comment">// Getters et setters manuels</span>
    <span class="keyword">public</span> Long <span class="function">getId</span>() { <span class="keyword">return</span> id; }
    <span class="keyword">public void</span> <span class="function">setId</span>(Long id) { <span class="keyword">this</span>.id = id; }
    
    <span class="keyword">public</span> String <span class="function">getNom</span>() { <span class="keyword">return</span> nom; }
    <span class="keyword">public void</span> <span class="function">setNom</span>(String nom) { <span class="keyword">this</span>.nom = nom; }
}
            </code></pre>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Avec annotations</h4>
            <pre><code>
<span class="comment">// Configuration déclarative</span>
<span class="comment">// Code concis et lisible</span>
<span class="comment">// Maintenance facilitée</span>

<span class="annotation">@Entity</span>
<span class="annotation">@Table</span>(name = <span class="string">"utilisateurs"</span>)
<span class="annotation">@Data</span>
<span class="annotation">@NoArgsConstructor</span>
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    
    <span class="annotation">@Id</span>
    <span class="annotation">@GeneratedValue</span>(strategy = GenerationType.IDENTITY)
    <span class="keyword">private</span> Long id;
    
    <span class="annotation">@Column</span>(name = <span class="string">"nom_utilisateur"</span>, nullable = <span class="keyword">false</span>, length = 100)
    <span class="keyword">private</span> String nom;
}
            </code></pre>
          </div>
        </div>
        
        <p class="textExemple mt-4">
          Les annotations permettent une programmation <strong>déclarative</strong> plutôt qu'<strong>impérative</strong>. Vous dites <em>"quoi faire"</em> plutôt que <em>"comment le faire"</em>. Spring Boot utilise intensivement ce paradigme pour simplifier le développement et réduire le code répétitif.
        </p>
      </section>

      <!-- Catégories d'annotations -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Catégories d'annotations Spring Boot</h2>
        
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Annotations JPA (Jakarta Persistence)</h4>
            <ul class="textExemple">
              <li><code>@Entity</code> - Définit une classe comme entité persistante</li>
              <li><code>@Table</code> - Spécifie la table de base de données</li>
              <li><code>@Column</code> - Configure les colonnes de la table</li>
              <li><code>@Id</code> - Identifie la clé primaire</li>
              <li><code>@GeneratedValue</code> - Stratégie de génération des IDs</li>
              <li><code>@OneToMany</code> - Relation un-à-plusieurs</li>
              <li><code>@ManyToOne</code> - Relation plusieurs-à-un</li>
            </ul>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Annotations Lombok</h4>
            <ul class="textExemple">
              <li><code>@Getter</code> - Génère les getters</li>
              <li><code>@Setter</code> - Génère les setters</li>
              <li><code>@Data</code> - Génère getters, setters, equals, hashCode, toString</li>
              <li><code>@NoArgsConstructor</code> - Constructeur sans arguments</li>
              <li><code>@AllArgsConstructor</code> - Constructeur avec tous les arguments</li>
              <li><code>@Builder</code> - Pattern Builder pour l'objet</li>
            </ul>
          </div>
        </div>
        
        <div class="code-comparison mt-4">
          <div class="code-block">
            <h4 class="text-purple">Annotations Spring Core</h4>
            <ul class="textExemple">
              <li><code>@Component</code> - Composant Spring générique</li>
              <li><code>@Service</code> - Couche service métier</li>
              <li><code>@Repository</code> - Couche d'accès aux données</li>
              <li><code>@Controller</code> - Contrôleur web MVC</li>
              <li><code>@RestController</code> - Contrôleur REST API</li>
              <li><code>@Autowired</code> - Injection de dépendances</li>
              <li><code>@Configuration</code> - Classe de configuration</li>
            </ul>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Annotations Spring Web</h4>
            <ul class="textExemple">
              <li><code>@RequestMapping</code> - Mappage des requêtes HTTP</li>
              <li><code>@GetMapping</code> - Requêtes HTTP GET</li>
              <li><code>@PostMapping</code> - Requêtes HTTP POST</li>
              <li><code>@PutMapping</code> - Requêtes HTTP PUT</li>
              <li><code>@DeleteMapping</code> - Requêtes HTTP DELETE</li>
              <li><code>@PathVariable</code> - Variable dans l'URL</li>
              <li><code>@RequestParam</code> - Paramètre de requête</li>
              <li><code>@RequestBody</code> - Corps de la requête</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Annotations JPA détaillées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Annotations JPA - Mapping Objet/Relationnel</h2>
        
        <h3 class="text-purple mt-4">@Entity - Définition d'une entité</h3>
        <p class="textExemple">
          L'annotation <code>@Entity</code> marque une classe Java comme une entité persistante. Cela signifie que les instances de cette classe peuvent être stockées, récupérées et gérées par JPA (Java Persistence API).
        </p>
        <div class="code-example">
          <pre><code>
<span class="annotation">@Entity</span>
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="comment">// Propriétés et méthodes...</span>
}

<span class="comment">// Options disponibles :</span>
<span class="annotation">@Entity</span>(name = <span class="string">"UtilisateurEntity"</span>)  <span class="comment">// Nom de l'entité pour les requêtes JPQL</span>

<span class="comment">// Règles importantes :</span>
<span class="comment">// 1. Doit avoir un constructeur public sans arguments</span>
<span class="comment">// 2. Ne peut pas être une classe finale</span>
<span class="comment">// 3. Doit avoir une propriété annotée @Id</span>
          </code></pre>
        </div>

        <h3 class="text-purple mt-4">@Table - Configuration de la table</h3>
        <p class="textExemple">
          <code>@Table</code> spécifie les détails de la table de base de données associée à l'entité. Si omise, JPA utilise le nom de la classe comme nom de table.
        </p>
        <div class="code-example">
          <pre><code>
<span class="annotation">@Entity</span>
<span class="annotation">@Table</span>(
    name = <span class="string">"utilisateurs"</span>,                    <span class="comment">// Nom de la table</span>
    schema = <span class="string">"gestion"</span>,                      <span class="comment">// Schéma de base de données</span>
    catalog = <span class="string">"entreprise_db"</span>,                <span class="comment">// Catalogue de base de données</span>
    uniqueConstraints = {                      <span class="comment">// Contraintes d'unicité</span>
        <span class="annotation">@UniqueConstraint</span>(
            name = <span class="string">"uk_email"</span>,
            columnNames = {<span class="string">"email"</span>}
        )
    },
    indexes = {                                <span class="comment">// Index de la table</span>
        <span class="annotation">@Index</span>(
            name = <span class="string">"idx_nom"</span>,
            columnList = <span class="string">"nom"</span>
        )
    }
)
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="comment">// Propriétés...</span>
}
          </code></pre>
        </div>

        <h3 class="text-purple mt-4">@Id et @GeneratedValue - Clé primaire</h3>
        <p class="textExemple">
          <code>@Id</code> identifie la propriété comme clé primaire de l'entité. <code>@GeneratedValue</code> définit comment cette clé primaire est générée.
        </p>
        <div class="code-example">
          <pre><code>
<span class="annotation">@Id</span>
<span class="annotation">@GeneratedValue</span>(
    strategy = GenerationType.<span class="variable">IDENTITY</span>,  <span class="comment">// Auto-incrément de la base de données</span>
    generator = <span class="string">"utilisateur_seq"</span>        <span class="comment">// Nom du générateur (optionnel)</span>
)
<span class="keyword">private</span> Long id;

<span class="comment">// Stratégies disponibles pour @GeneratedValue :</span>
<span class="comment">// GenerationType.AUTO - Laissé à JPA de décider (défaut)</span>
<span class="comment">// GenerationType.IDENTITY - Auto-incrément de la base (MySQL, SQL Server)</span>
<span class="comment">// GenerationType.SEQUENCE - Séquence de base de données (Oracle, PostgreSQL)</span>
<span class="comment">// GenerationType.TABLE - Table spéciale pour générer les IDs</span>

<span class="comment">// Exemple avec séquence PostgreSQL :</span>
<span class="annotation">@Id</span>
<span class="annotation">@GeneratedValue</span>(
    strategy = GenerationType.<span class="variable">SEQUENCE</span>,
    generator = <span class="string">"utilisateur_generator"</span>
)
<span class="annotation">@SequenceGenerator</span>(
    name = <span class="string">"utilisateur_generator"</span>,
    sequenceName = <span class="string">"utilisateur_id_seq"</span>,
    allocationSize = 1
)
<span class="keyword">private</span> Long id;
          </code></pre>
        </div>

        <h3 class="text-purple mt-4">@Column - Configuration des colonnes</h3>
        <p class="textExemple">
          <code>@Column</code> permet de personnaliser le mapping entre une propriété d'entité et une colonne de table. Chaque attribut correspond à une caractéristique de la colonne en base de données.
        </p>
        <div class="code-example">
          <pre><code>
<span class="annotation">@Column</span>(
    name = <span class="string">"nom_complet"</span>,               <span class="comment">// Nom de la colonne en base</span>
    nullable = <span class="keyword">false</span>,                   <span class="comment">// NOT NULL constraint</span>
    unique = <span class="keyword">true</span>,                     <span class="comment">// Contrainte d'unicité</span>
    length = 100,                       <span class="comment">// Taille maximale (pour VARCHAR)</span>
    columnDefinition = <span class="string">"TEXT"</span>,          <span class="comment">// Définition SQL personnalisée</span>
    precision = 10,                     <span class="comment">// Précision pour les nombres décimaux</span>
    scale = 2,                          <span class="comment">// Échelle pour les nombres décimaux</span>
    insertable = <span class="keyword">true</span>,                  <span class="comment">// Incluse dans les INSERT</span>
    updatable = <span class="keyword">true</span>,                   <span class="comment">// Incluse dans les UPDATE</span>
    table = <span class="string">"utilisateurs"</span>              <span class="comment">// Table (pour les entités secondaires)</span>
)
<span class="keyword">private</span> String nomComplet;

<span class="comment">// Exemples pratiques courants :</span>
<span class="annotation">@Column</span>(nullable = <span class="keyword">false</span>, length = 150)
<span class="keyword">private</span> String email;

<span class="annotation">@Column</span>(name = <span class="string">"date_creation"</span>, updatable = <span class="keyword">false</span>)
<span class="keyword">private</span> LocalDateTime dateCreation;

<span class="annotation">@Column</span>(columnDefinition = <span class="string">"DECIMAL(10,2)"</span>)
<span class="keyword">private</span> BigDecimal prix;
          </code></pre>
        </div>
      </section>

      <!-- Annotations Lombok détaillées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Annotations Lombok - Réduction du code boilerplate</h2>
        
        <p class="textExemple">
          Lombok est une bibliothèque Java qui génère automatiquement du code répétitif (getters, setters, constructeurs, etc.) via des annotations de compilation. Cela rend le code plus lisible et réduit les erreurs manuelles.
        </p>

        <h3 class="text-purple mt-4">@Getter et @Setter</h3>
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Sans Lombok</h4>
            <pre><code>
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="keyword">private</span> Long id;
    <span class="keyword">private</span> String nom;
    <span class="keyword">private</span> String email;
    
    <span class="keyword">public</span> Long <span class="function">getId</span>() {
        <span class="keyword">return</span> id;
    }
    
    <span class="keyword">public void</span> <span class="function">setId</span>(Long id) {
        <span class="keyword">this</span>.id = id;
    }
    
    <span class="comment">// Répéter pour chaque propriété...</span>
    <span class="comment">// 6 méthodes pour 3 propriétés !</span>
}
            </code></pre>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Avec Lombok</h4>
            <pre><code>
<span class="annotation">@Getter</span>
<span class="annotation">@Setter</span>
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="keyword">private</span> Long id;
    <span class="keyword">private</span> String nom;
    <span class="keyword">private</span> String email;
    <span class="comment">// Lombok génère automatiquement tous les getters et setters</span>
}

<span class="comment">// Variantes :</span>
<span class="annotation">@Getter</span>(<span class="variable">AccessLevel</span>.<span class="variable">PROTECTED</span>)  <span class="comment">// Getters protégés seulement</span>
<span class="annotation">@Setter</span>(<span class="variable">AccessLevel</span>.<span class="variable">NONE</span>)     <span class="comment">// Pas de setters pour cette propriété</span>
<span class="keyword">private</span> String password;

<span class="annotation">@Getter</span>                        <span class="comment">// Getter seulement (immutable)</span>
<span class="keyword">private final</span> String idUnique;
            </code></pre>
          </div>
        </div>

        <h3 class="text-purple mt-4">@Data - L'annotation "tout-en-un"</h3>
        <p class="textExemple">
          <code>@Data</code> est probablement l'annotation Lombok la plus utilisée. Elle combine plusieurs fonctionnalités en une seule annotation.
        </p>
        <div class="code-example">
          <pre><code>
<span class="annotation">@Data</span>  <span class="comment">// Equivalent à :</span>
        <span class="comment">// @Getter sur toutes les propriétés</span>
        <span class="comment">// @Setter sur toutes les propriétés non-final</span>
        <span class="comment">// @ToString (génère méthode toString())</span>
        <span class="comment">// @EqualsAndHashCode (génère equals() et hashCode())</span>
        <span class="comment">// @RequiredArgsConstructor (constructeur pour les champs final/@NonNull)</span>

<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    
    <span class="keyword">private</span> Long id;
    
    <span class="annotation">@NonNull</span>  <span class="comment">// Inclus dans le constructeur requis</span>
    <span class="keyword">private</span> String nom;
    
    <span class="keyword">private</span> String email;
    
    <span class="comment">// Lombok génère automatiquement :</span>
    <span class="comment">// - Getters et setters pour id, nom, email</span>
    <span class="comment">// - toString() incluant toutes les propriétés</span>
    <span class="comment">// - equals() et hashCode() basés sur id et nom</span>
    <span class="comment">// - Constructeur Utilisateur(String nom)</span>
}

<span class="comment">// @Data peut être combinée avec d'autres annotations :</span>
<span class="annotation">@Data</span>
<span class="annotation">@AllArgsConstructor</span>
<span class="annotation">@NoArgsConstructor</span>
<span class="annotation">@Builder</span>
<span class="keyword">public class</span> <span class="class-name">Produit</span> {
    <span class="keyword">private</span> Long id;
    <span class="keyword">private</span> String nom;
    <span class="keyword">private</span> BigDecimal prix;
}

<span class="comment">// Utilisation avec @Builder :</span>
Produit produit = Produit.<span class="function">builder</span>()
    .<span class="function">id</span>(1L)
    .<span class="function">nom</span>(<span class="string">"Ordinateur"</span>)
    .<span class="function">prix</span>(<span class="keyword">new</span> BigDecimal(<span class="string">"999.99"</span>))
    .<span class="function">build</span>();
          </code></pre>
        </div>

        <h3 class="text-purple mt-4">Annotations de constructeur</h3>
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">@NoArgsConstructor</h4>
            <pre><code>
<span class="annotation">@NoArgsConstructor</span>
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="comment">// Génère : public Utilisateur() {}</span>
}

<span class="annotation">@NoArgsConstructor</span>(access = <span class="variable">AccessLevel</span>.<span class="variable">PROTECTED</span>)
<span class="keyword">public class</span> <span class="class-name">EntiteBase</span> {
    <span class="comment">// Génère : protected EntiteBase() {}</span>
}
            </code></pre>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">@AllArgsConstructor</h4>
            <pre><code>
<span class="annotation">@AllArgsConstructor</span>
<span class="keyword">public class</span> <span class="class-name">Utilisateur</span> {
    <span class="keyword">private</span> Long id;
    <span class="keyword">private</span> String nom;
    <span class="keyword">private</span> String email;
    <span class="comment">// Génère : public Utilisateur(Long id, String nom, String email)</span>
}

<span class="annotation">@AllArgsConstructor</span>(staticName = <span class="string">"of"</span>)
<span class="keyword">public class</span> <span class="class-name">Point</span> {
    <span class="keyword">private</span> <span class="keyword">int</span> x;
    <span class="keyword">private</span> <span class="keyword">int</span> y;
    <span class="comment">// Génère : public static Point of(int x, int y)</span>
}
            </code></pre>
          </div>
        </div>
      </section>

      <!-- Exemple complet intégré -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Exemple complet : Entité avec toutes les annotations</h2>
        
        <div class="code-example">
          <pre><code>
<span class="keyword">package</span> com.example.bibliotheque.entity;

<span class="keyword">import</span> jakarta.persistence.*;
<span class="keyword">import</span> lombok.*;
<span class="keyword">import</span> java.time.LocalDateTime;
<span class="keyword">import</span> java.util.ArrayList;
<span class="keyword">import</span> java.util.List;

<span class="annotation">@Entity</span>
<span class="annotation">@Table</span>(
    name = <span class="string">"livres"</span>,
    schema = <span class="string">"bibliotheque"</span>,
    indexes = {
        <span class="annotation">@Index</span>(name = <span class="string">"idx_titre"</span>, columnList = <span class="string">"titre"</span>),
        <span class="annotation">@Index</span>(name = <span class="string">"idx_auteur"</span>, columnList = <span class="string">"auteur_id"</span>)
    },
    uniqueConstraints = {
        <span class="annotation">@UniqueConstraint</span>(
            name = <span class="string">"uk_isbn"</span>,
            columnNames = {<span class="string">"isbn"</span>}
        )
    }
)
<span class="annotation">@Data</span>                                    <span class="comment">// Lombok: getters, setters, equals, hashCode, toString</span>
<span class="annotation">@NoArgsConstructor</span>                       <span class="comment">// Lombok: constructeur sans arguments</span>
<span class="annotation">@AllArgsConstructor</span>                      <span class="comment">// Lombok: constructeur avec tous les arguments</span>
<span class="annotation">@Builder</span>                                 <span class="comment">// Lombok: pattern Builder</span>
<span class="keyword">public class</span> <span class="class-name">Livre</span> {
    
    <span class="annotation">@Id</span>
    <span class="annotation">@GeneratedValue</span>(strategy = GenerationType.<span class="variable">IDENTITY</span>)
    <span class="keyword">private</span> Long id;
    
    <span class="annotation">@Column</span>(
        name = <span class="string">"titre"</span>,
        nullable = <span class="keyword">false</span>,
        length = 200
    )
    <span class="keyword">private</span> String titre;
    
    <span class="annotation">@Column</span>(
        name = <span class="string">"isbn"</span>,
        nullable = <span class="keyword">false</span>,
        unique = <span class="keyword">true</span>,
        length = 13
    )
    <span class="keyword">private</span> String isbn;
    
    <span class="annotation">@Column</span>(
        name = <span class="string">"annee_publication"</span>,
        columnDefinition = <span class="string">"INTEGER"</span>
    )
    <span class="keyword">private</span> Integer anneePublication;
    
    <span class="annotation">@Column</span>(
        name = <span class="string">"prix"</span>,
        precision = 10,
        scale = 2
    )
    <span class="keyword">private</span> BigDecimal prix;
    
    <span class="annotation">@Column</span>(
        name = <span class="string">"disponible"</span>,
        nullable = <span class="keyword">false</span>
    )
    <span class="keyword">private</span> Boolean disponible = <span class="keyword">true</span>;
    
    <span class="annotation">@Column</span>(
        name = <span class="string">"date_ajout"</span>,
        updatable = <span class="keyword">false</span>
    )
    <span class="keyword">private</span> LocalDateTime dateAjout = LocalDateTime.<span class="function">now</span>();
    
    <span class="comment">// Relation Many-to-One avec Auteur</span>
    <span class="annotation">@ManyToOne</span>(
        fetch = FetchType.<span class="variable">LAZY</span>,
        optional = <span class="keyword">false</span>
    )
    <span class="annotation">@JoinColumn</span>(
        name = <span class="string">"auteur_id"</span>,
        foreignKey = <span class="annotation">@ForeignKey</span>(name = <span class="string">"fk_livre_auteur"</span>)
    )
    <span class="keyword">private</span> Auteur auteur;
    
    <span class="comment">// Relation One-to-Many avec Emprunt</span>
    <span class="annotation">@OneToMany</span>(
        mappedBy = <span class="string">"livre"</span>,
        cascade = CascadeType.<span class="variable">ALL</span>,
        orphanRemoval = <span class="keyword">true</span>
    )
    <span class="annotation">@ToString</span>.<span class="function">Exclude</span>                     <span class="comment">// Exclure de toString() pour éviter la récursion</span>
    <span class="annotation">@EqualsAndHashCode</span>.<span class="function">Exclude</span>            <span class="comment">// Exclure de equals() et hashCode()</span>
    <span class="annotation">@Builder</span>.<span class="function">Default</span>                       <span class="comment">// Initialiser avec Builder</span>
    <span class="keyword">private</span> List&lt;Emprunt&gt; emprunts = <span class="keyword">new</span> ArrayList&lt;&gt;();
    
    <span class="comment">// Méthode utilitaire pour gérer la relation bidirectionnelle</span>
    <span class="keyword">public void</span> <span class="function">ajouterEmprunt</span>(Emprunt emprunt) {
        emprunts.<span class="function">add</span>(emprunt);
        emprunt.<span class="function">setLivre</span>(<span class="keyword">this</span>);
    }
    
    <span class="keyword">public void</span> <span class="function">supprimerEmprunt</span>(Emprunt emprunt) {
        emprunts.<span class="function">remove</span>(emprunt);
        emprunt.<span class="function">setLivre</span>(<span class="keyword">null</span>);
    }
}
          </code></pre>
        </div>
        
        <p class="textExemple mt-3">
          Cet exemple montre comment combiner intelligemment les annotations JPA et Lombok pour créer une entité complète, propre et facile à maintenir. Notez l'utilisation de <code>@Builder.Default</code> pour initialiser les collections et les annotations d'exclusion pour éviter les problèmes de récursion dans <code>toString()</code>, <code>equals()</code> et <code>hashCode()</code>.
        </p>
      </section>

      <!-- Bonnes pratiques et pièges à éviter -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-3">Bonnes pratiques et pièges à éviter</h2>
        
        <h3 class="text-purple mt-4">Utilisation correcte des annotations</h3>
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">À faire ✅</h4>
            <ul class="textExemple">
              <li>Utiliser <code>@Data</code> avec prudence (peut générer trop de méthodes)</li>
              <li>Combiner <code>@Entity</code> avec <code>@NoArgsConstructor</code> (requis par JPA)</li>
              <li>Spécifier explicitement les noms de colonnes avec <code>@Column(name="...")</code></li>
              <li>Utiliser <code>@Builder</code> pour les objets complexes avec plusieurs propriétés</li>
              <li>Exclure les relations circulaires de <code>toString()</code> et <code>equals()</code></li>
              <li>Initialiser les collections dans la déclaration</li>
            </ul>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">À éviter ❌</h4>
            <ul class="textExemple">
              <li>Éviter <code>@Data</code> sur les entités avec relations circulaires</li>
              <li>Ne pas mélanger <code>@Data</code> avec des getters/setters manuels</li>
              <li>Éviter les stratégies de génération d'ID incompatibles avec la base</li>
              <li>Ne pas oublier <code>@EqualsAndHashCode.Exclude</code> sur les relations</li>
              <li>Éviter les noms de colonnes ambigus ou réservés</li>
              <li>Ne pas utiliser <code>@AllArgsConstructor</code> sans <code>@NoArgsConstructor</code> sur les entités JPA</li>
            </ul>
          </div>
        </div>

        <h3 class="text-purple mt-4">Configuration Lombok dans le projet</h3>
        <p class="textExemple">
          Pour utiliser Lombok dans votre projet Spring Boot, ajoutez la dépendance dans votre <code>pom.xml</code> (Maven) ou <code>build.gradle</code> (Gradle) :
        </p>
        
        <div class="code-comparison">
          <div class="code-block">
            <h4 class="text-purple">Maven (pom.xml)</h4>
            <pre><code>
&lt;dependency&gt;
    &lt;groupId&gt;org.projectlombok&lt;/groupId&gt;
    &lt;artifactId&gt;lombok&lt;/artifactId&gt;
    &lt;optional&gt;true&lt;/optional&gt;
&lt;/dependency&gt;
            </code></pre>
          </div>
          
          <div class="code-block">
            <h4 class="text-purple">Gradle (build.gradle)</h4>
            <pre><code>
dependencies {
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
}
            </code></pre>
          </div>
        </div>
        
        <p class="textExemple mt-3">
          Assurez-vous également d'installer le plugin Lombok dans votre IDE (IntelliJ, Eclipse, VS Code) pour que les méthodes générées soient reconnues pendant le développement.
        </p>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white mb-3">Conclusion</h2>
        

        
        <div class="mt-4">
          <h3 class="text-white">Récapitulatif des annotations essentielles</h3>
          <table style="width:100%; color:white; margin-top:1rem;">
            <thead>
              <tr>
                <th style="text-align:left">Annotation</th>
                <th style="text-align:left">Package</th>
                <th style="text-align:left">Objectif principal</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>@Entity</code></td>
                <td>jakarta.persistence</td>
                <td>Déclare une classe comme entité persistante</td>
              </tr>
              <tr>
                <td><code>@Table</code></td>
                <td>jakarta.persistence</td>
                <td>Configure la table de base de données</td>
              </tr>
              <tr>
                <td><code>@Id</code></td>
                <td>jakarta.persistence</td>
                <td>Identifie la clé primaire</td>
              </tr>
              <tr>
                <td><code>@GeneratedValue</code></td>
                <td>jakarta.persistence</td>
                <td>Définit comment générer les IDs</td>
              </tr>
              <tr>
                <td><code>@Column</code></td>
                <td>jakarta.persistence</td>
                <td>Configure le mapping d'une propriété</td>
              </tr>
              <tr>
                <td><code>@Getter/@Setter</code></td>
                <td>lombok</td>
                <td>Génère les méthodes getter/setter</td>
              </tr>
              <tr>
                <td><code>@Data</code></td>
                <td>lombok</td>
                <td>Génère getters, setters, equals, hashCode, toString</td>
              </tr>
              <tr>
                <td><code>@NoArgsConstructor</code></td>
                <td>lombok</td>
                <td>Génère un constructeur sans arguments</td>
              </tr>
              <tr>
                <td><code>@Builder</code></td>
                <td>lombok</td>
                <td>Implémente le pattern Builder</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
// Logique minimale pour cette page de leçon
</script>

<style scoped>
/* Votre CSS fourni est intégré ici */
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

.bg-gradient-primary {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
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

/* Couleurs pour Java/JPA */
.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }
.annotation { color: #569cd6 !important; }

.exercise {
    margin: 2rem 0;
}

.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
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
    
    .btn-purple {
        display: block;
        margin: 0.5rem 0;
        width: 100%;
        text-align: center;
    }
    
    .ml-2 {
        margin-left: 0 !important;
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

.mt-3 { margin-top: 1rem; }
.mt-4 { margin-top: 1.5rem; }
.mb-3 { margin-bottom: 1rem; }
.ml-2 { margin-left: 0.5rem; }

/* Styles pour le tableau */
table {
    border-collapse: collapse;
    width: 100%;
}

th, td {
    padding: 0.75rem;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

th {
    font-weight: 600;
}
</style>