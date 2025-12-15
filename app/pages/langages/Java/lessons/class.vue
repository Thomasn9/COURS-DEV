<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <div class="lesson-header">
                <h1 class="text-white">Création de Classes en Java</h1>
                <p class="lesson-meta text-white">Maîtrisez les fondamentaux de la Programmation Orientée Objet en Java</p>
            </div>

            <!-- Introduction -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à la Programmation Orientée Objet (POO)</h2>
                <p class="textExemple">
                    En Java, tout est objet ! Une <strong>classe</strong> est le plan de construction d'un objet. 
                    C'est le concept fondamental de la Programmation Orientée Objet qui permet de modéliser le monde réel.
                </p>
                <p class="textExemple">
                    Cette leçon vous guidera à travers toutes les étapes nécessaires pour créer et utiliser des classes en Java.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-java">// Une classe en Java représente un concept
public class Voiture {
    // Attributs (caractéristiques)
    // Méthodes (comportements)
}</code></pre>
                </div>
            </div>

            <!-- Les 4 piliers de la POO -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les 4 piliers de la Programmation Orientée Objet</h2>
                <p class="textExemple">
                    Pour bien comprendre les classes, vous devez maîtriser ces quatre concepts fondamentaux :
                </p>
                <ol class="textExemple">
                    <li><strong>Encapsulation</strong> : Masquer les données et exposer uniquement ce qui est nécessaire</li>
                    <li><strong>Héritage</strong> : Créer de nouvelles classes basées sur des classes existantes</li>
                    <li><strong>Polymorphisme</strong> : Utiliser une interface commune pour différents types d'objets</li>
                    <li><strong>Abstraction</strong> : Simplifier la complexité en se concentrant sur l'essentiel</li>
                </ol>
            </div>

            <!-- Structure de base d'une classe -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Structure de base d'une classe</h2>
                <p class="textExemple">
                    Une classe Java est composée de plusieurs éléments essentiels. Voici la structure minimale :
                </p>
                
                <div class="code-example">
                    <pre v-pre><code class="language-java">// Déclaration de la classe
public class MaClasse {
    
    // 1. Variables d'instance (attributs)
    private String nom;
    private int age;
    
    // 2. Constructeur
    public MaClasse(String nom, int age) {
        this.nom = nom;
        this.age = age;
    }
    
    // 3. Méthodes (comportements)
    public void afficherInfo() {
        System.out.println("Nom: " + nom + ", Age: " + age);
    }
    
    // 4. Méthodes d'accès (getters/setters)
    public String getNom() {
        return nom;
    }
    
    public void setNom(String nom) {
        this.nom = nom;
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Explication des composants :</h3>
                <ul class="textExemple">
                    <li><code>public class MaClasse</code> : Déclaration de la classe avec son nom</li>
                    <li><code>private String nom</code> : Attribut (variable d'instance) avec encapsulation</li>
                    <li><code>public MaClasse(...)</code> : Constructeur pour initialiser l'objet</li>
                    <li><code>public void afficherInfo()</code> : Méthode pour définir le comportement</li>
                    <li><code>getNom()/setNom()</code> : Getters et setters pour accéder aux attributs privés</li>
                </ul>
            </div>

            <!-- Étape 1 : Déclarer une classe -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : Déclarer une classe</h2>
                <p class="textExemple">
                    Commençons par créer notre première classe. Nous allons modéliser une <strong>Personne</strong> :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Personne.java</h4>
                    <pre v-pre><code class="language-java">// Fichier: Personne.java
public class Personne {
    // Attributs de la classe
    private String prenom;
    private String nom;
    private int age;
    private String email;
    
    // Constructeur par défaut (sans paramètres)
    public Personne() {
        this.prenom = "Inconnu";
        this.nom = "Inconnu";
        this.age = 0;
        this.email = "inconnu@example.com";
    }
    
    // Constructeur avec paramètres
    public Personne(String prenom, String nom, int age, String email) {
        this.prenom = prenom;
        this.nom = nom;
        this.age = age;
        this.email = email;
    }
    
    // Méthode pour afficher les informations
    public void sePresenter() {
        System.out.println("Bonjour, je m'appelle " + prenom + " " + nom);
        System.out.println("J'ai " + age + " ans");
        System.out.println("Mon email: " + email);
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Types de classes en Java</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java">// 1. Classe concrète (instanciable)
public class Voiture { }

// 2. Classe abstraite (ne peut pas être instanciée)
public abstract class Animal { }

// 3. Classe finale (ne peut pas être héritée)
public final class MathUtils { }

// 4. Classe imbriquée (définie dans une autre classe)
public class Universite {
    public class Etudiant { }
}

// 5. Classe interne statique
public class Collection {
    public static class Iterateur { }
}</code></pre>
                </div>
            </div>

            <!-- Étape 2 : Les modificateurs d'accès -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Comprendre les modificateurs d'accès</h2>
                <p class="textExemple">
                    Java propose 4 niveaux de visibilité pour contrôler l'accès aux membres d'une classe :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Tableau des modificateurs d'accès</h4>
                    <pre v-pre><code class="language-java">public class ExempleModificateurs {
    
    // Public - accessible de partout
    public String publicVariable = "Tout le monde peut me voir";
    
    // Protected - accessible dans le package et les sous-classes
    protected String protectedVariable = "Visible dans le package et les enfants";
    
    // Default (package-private) - accessible seulement dans le package
    String defaultVariable = "Visible uniquement dans ce package";
    
    // Private - accessible seulement dans la classe
    private String privateVariable = "Seulement visible dans cette classe";
    
    // Méthodes avec différents niveaux d'accès
    public void methodePublique() {
        System.out.println("Méthode publique");
    }
    
    private void methodePrivee() {
        System.out.println("Méthode privée");
    }
    
    protected void methodeProtegee() {
        System.out.println("Méthode protégée");
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Règles d'accès</h3>
                <table class="access-table">
                    <thead>
                        <tr>
                            <th>Modificateur</th>
                            <th>Classe</th>
                            <th>Package</th>
                            <th>Sous-classe</th>
                            <th>Monde</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><code>public</code></td>
                            <td>✓</td>
                            <td>✓</td>
                            <td>✓</td>
                            <td>✓</td>
                        </tr>
                        <tr>
                            <td><code>protected</code></td>
                            <td>✓</td>
                            <td>✓</td>
                            <td>✓</td>
                            <td>✗</td>
                        </tr>
                        <tr>
                            <td><code>default</code></td>
                            <td>✓</td>
                            <td>✓</td>
                            <td>✗</td>
                            <td>✗</td>
                        </tr>
                        <tr>
                            <td><code>private</code></td>
                            <td>✓</td>
                            <td>✗</td>
                            <td>✗</td>
                            <td>✗</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Étape 3 : Les constructeurs -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Maîtriser les constructeurs</h2>
                <p class="textExemple">
                    Les constructeurs sont des méthodes spéciales appelées lors de la création d'un objet. 
                    Ils initialisent les attributs de l'objet.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Différents types de constructeurs</h4>
                    <pre v-pre><code class="language-java">public class Etudiant {
    private String nom;
    private int age;
    private String matricule;
    private double moyenne;
    
    // 1. Constructeur par défaut (sans paramètres)
    public Etudiant() {
        this.nom = "Nouvel étudiant";
        this.age = 18;
        this.matricule = "ETU000";
        this.moyenne = 10.0;
        System.out.println("Étudiant créé avec valeurs par défaut");
    }
    
    // 2. Constructeur avec paramètres
    public Etudiant(String nom, int age, String matricule) {
        this.nom = nom;
        this.age = age;
        this.matricule = matricule;
        this.moyenne = 10.0; // Valeur par défaut
        System.out.println("Étudiant " + nom + " créé");
    }
    
    // 3. Constructeur avec tous les paramètres
    public Etudiant(String nom, int age, String matricule, double moyenne) {
        this.nom = nom;
        this.age = age;
        this.matricule = matricule;
        this.moyenne = moyenne;
        System.out.println("Étudiant " + nom + " créé avec moyenne " + moyenne);
    }
    
    // 4. Constructeur de copie
    public Etudiant(Etudiant autreEtudiant) {
        this.nom = autreEtudiant.nom;
        this.age = autreEtudiant.age;
        this.matricule = autreEtudiant.matricule;
        this.moyenne = autreEtudiant.moyenne;
        System.out.println("Copie de l'étudiant " + nom + " créée");
    }
    
    // 5. Appel d'un constructeur depuis un autre constructeur (this())
    public Etudiant(String nom) {
        this(nom, 18, "ETU" + System.currentTimeMillis());
        System.out.println("Étudiant créé avec nom seulement");
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Utilisation des constructeurs</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        // Utilisation des différents constructeurs
        Etudiant etudiant1 = new Etudiant(); // Constructeur par défaut
        Etudiant etudiant2 = new Etudiant("Alice", 20, "ETU12345");
        Etudiant etudiant3 = new Etudiant("Bob", 21, "ETU67890", 15.5);
        Etudiant etudiant4 = new Etudiant(etudiant3); // Constructeur de copie
        Etudiant etudiant5 = new Etudiant("Charlie"); // Constructeur avec this()
    }
}</code></pre>
                </div>
            </div>

            <!-- Étape 4 : Getters et Setters (Encapsulation) -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4 : Encapsulation avec Getters et Setters</h2>
                <p class="textExemple">
                    L'encapsulation est un principe fondamental de la POO. Elle permet de protéger les données 
                    et de contrôler leur accès via des méthodes spécifiques.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Classe CompteBancaire avec encapsulation</h4>
                    <pre v-pre><code class="language-java">public class CompteBancaire {
    // Attributs privés (encapsulés)
    private String numeroCompte;
    private String titulaire;
    private double solde;
    private double decouvertAutorise;
    
    // Constructeur
    public CompteBancaire(String numeroCompte, String titulaire, double soldeInitial) {
        this.numeroCompte = numeroCompte;
        this.titulaire = titulaire;
        this.solde = soldeInitial;
        this.decouvertAutorise = 500.0; // Découvert autorisé par défaut
    }
    
    // GETTERS (accesseurs) - pour lire les valeurs
    public String getNumeroCompte() {
        return numeroCompte;
    }
    
    public String getTitulaire() {
        return titulaire;
    }
    
    public double getSolde() {
        return solde;
    }
    
    public double getDecouvertAutorise() {
        return decouvertAutorise;
    }
    
    // SETTERS (mutateurs) - pour modifier les valeurs avec validation
    public void setTitulaire(String titulaire) {
        if (titulaire != null && !titulaire.trim().isEmpty()) {
            this.titulaire = titulaire;
        } else {
            System.out.println("Erreur: Le nom du titulaire ne peut pas être vide");
        }
    }
    
    public void setDecouvertAutorise(double decouvertAutorise) {
        if (decouvertAutorise >= 0 && decouvertAutorise <= 2000) {
            this.decouvertAutorise = decouvertAutorise;
        } else {
            System.out.println("Erreur: Le découvert doit être entre 0 et 2000");
        }
    }
    
    // Méthodes métiers (comportements)
    public void deposer(double montant) {
        if (montant > 0) {
            solde += montant;
            System.out.println("Dépôt de " + montant + "€ effectué. Nouveau solde: " + solde + "€");
        } else {
            System.out.println("Erreur: Le montant doit être positif");
        }
    }
    
    public boolean retirer(double montant) {
        if (montant > 0 && (solde - montant) >= -decouvertAutorise) {
            solde -= montant;
            System.out.println("Retrait de " + montant + "€ effectué. Nouveau solde: " + solde + "€");
            return true;
        } else {
            System.out.println("Erreur: Retrait impossible. Solde insuffisant ou montant invalide");
            return false;
        }
    }
    
    public void afficherSolde() {
        System.out.println("Compte: " + numeroCompte);
        System.out.println("Titulaire: " + titulaire);
        System.out.println("Solde: " + solde + "€");
        System.out.println("Découvert autorisé: " + decouvertAutorise + "€");
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Pourquoi l'encapsulation ?</h3>
                <ul class="textExemple">
                    <li><strong>Sécurité</strong> : Contrôle d'accès aux données</li>
                    <li><strong>Validation</strong> : Vérification des données avant modification</li>
                    <li><strong>Flexibilité</strong> : Possibilité de changer l'implémentation interne sans affecter les utilisateurs</li>
                    <li><strong>Maintenabilité</strong> : Code plus facile à déboguer et à maintenir</li>
                </ul>
            </div>

            <!-- Étape 5 : Les méthodes -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 5 : Créer des méthodes</h2>
                <p class="textExemple">
                    Les méthodes définissent le comportement d'un objet. Elles peuvent être de différents types :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Types de méthodes dans une classe</h4>
                    <pre v-pre><code class="language-java">public class Calculatrice {
    
    // 1. Méthode d'instance (non-statique) - opère sur l'instance
    public double additionner(double a, double b) {
        return a + b;
    }
    
    // 2. Méthode statique - ne nécessite pas d'instance
    public static double multiplier(double a, double b) {
        return a * b;
    }
    
    // 3. Méthode avec paramètres variables (varargs)
    public double faireSomme(double... nombres) {
        double somme = 0;
        for (double n : nombres) {
            somme += n;
        }
        return somme;
    }
    
    // 4. Méthode qui retourne un objet
    public ResultatOperation calculerComplexe(double x, double y) {
        double somme = x + y;
        double produit = x * y;
        return new ResultatOperation(somme, produit);
    }
    
    // 5. Méthode récursive
    public int factorielle(int n) {
        if (n <= 1) {
            return 1;
        }
        return n * factorielle(n - 1);
    }
    
    // 6. Méthode avec signature surchargée (overloading)
    public int additionner(int a, int b) {
        return a + b;
    }
    
    public int additionner(int a, int b, int c) {
        return a + b + c;
    }
    
    public String additionner(String a, String b) {
        return a + b; // Concaténation pour les chaînes
    }
    
    // 7. Méthode privée (utilisée en interne)
    private boolean estNombreValide(double nombre) {
        return !Double.isNaN(nombre) && !Double.isInfinite(nombre);
    }
    
    // 8. Méthode finale (ne peut pas être redéfinie)
    public final void afficherVersion() {
        System.out.println("Calculatrice version 2.0");
    }
}

// Classe auxiliaire pour l'exemple
class ResultatOperation {
    private double somme;
    private double produit;
    
    public ResultatOperation(double somme, double produit) {
        this.somme = somme;
        this.produit = produit;
    }
    
    // Getters...
}</code></pre>
                </div>

                <h3 class="text-purple">Utilisation des différentes méthodes</h3>
                <div class="code-example">
                    <pre v-pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        Calculatrice calc = new Calculatrice();
        
        // Méthode d'instance
        double resultat1 = calc.additionner(5.5, 3.2);
        
        // Méthode statique (appelée sur la classe)
        double resultat2 = Calculatrice.multiplier(4, 2.5);
        
        // Méthode avec varargs
        double resultat3 = calc.faireSomme(1, 2, 3, 4, 5);
        
        // Méthode récursive
        int factorielle5 = calc.factorielle(5);
        
        // Surcharge de méthode
        int sommeInt = calc.additionner(10, 20);
        String concat = calc.additionner("Bon", "jour");
        
        // Méthode finale
        calc.afficherVersion();
    }
}</code></pre>
                </div>
            </div>

            <!-- Étape 6 : Variables de classe vs d'instance -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 6 : Variables statiques vs d'instance</h2>
                <p class="textExemple">
                    Comprendre la différence entre variables d'instance et variables de classe (statiques) est crucial :
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Compteur d'objets avec variable statique</h4>
                    <pre v-pre><code class="language-java">public class Produit {
    
    // Variables d'instance (uniques pour chaque objet)
    private int id;
    private String nom;
    private double prix;
    
    // Variable de classe (statique) - partagée par toutes les instances
    private static int compteurProduits = 0;
    
    // Constante statique (final + static)
    public static final double TAUX_TVA = 0.20;
    
    // Constructeur
    public Produit(String nom, double prix) {
        this.id = ++compteurProduits; // Incrémente le compteur et l'assigne à l'ID
        this.nom = nom;
        this.prix = prix;
        System.out.println("Produit #" + id + " créé. Total produits: " + compteurProduits);
    }
    
    // Méthode d'instance
    public double getPrixTTC() {
        return prix * (1 + TAUX_TVA);
    }
    
    // Méthode statique (ne peut accéder qu'aux variables statiques)
    public static int getNombreTotalProduits() {
        return compteurProduits;
    }
    
    public static void reinitialiserCompteur() {
        compteurProduits = 0;
        System.out.println("Compteur réinitialisé");
    }
    
    // Getters pour les variables d'instance
    public int getId() { return id; }
    public String getNom() { return nom; }
    public double getPrix() { return prix; }
    
    // Setter avec validation
    public void setPrix(double prix) {
        if (prix >= 0) {
            this.prix = prix;
        } else {
            System.out.println("Erreur: Le prix ne peut pas être négatif");
        }
    }
}

// Classe principale pour tester
public class GestionProduits {
    public static void main(String[] args) {
        // La constante statique est accessible sans instance
        System.out.println("TVA applicable: " + Produit.TAUX_TVA + "%");
        
        // Création de produits
        Produit p1 = new Produit("Laptop", 899.99);
        Produit p2 = new Produit("Souris", 29.99);
        Produit p3 = new Produit("Clavier", 49.99);
        
        // Appel de méthode statique
        System.out.println("Nombre total de produits: " + Produit.getNombreTotalProduits());
        
        // Appel de méthodes d'instance
        System.out.println("Prix TTC du laptop: " + p1.getPrixTTC() + "€");
        System.out.println("Prix TTC de la souris: " + p2.getPrixTTC() + "€");
        
        // Réinitialisation du compteur
        Produit.reinitialiserCompteur();
        
        // Nouveau produit après réinitialisation
        Produit p4 = new Produit("Écran", 199.99);
        System.out.println("Nouveau total: " + Produit.getNombreTotalProduits());
    }
}</code></pre>
                </div>

                <h3 class="text-purple">Différence clé :</h3>
                <ul class="textExemple">
                    <li><strong>Variables d'instance</strong> : Chaque objet a sa propre copie</li>
                    <li><strong>Variables statiques</strong> : Une seule copie partagée par toutes les instances</li>
                    <li><strong>Méthodes d'instance</strong> : Opèrent sur les données de l'objet (accèdent à <code>this</code>)</li>
                    <li><strong>Méthodes statiques</strong> : N'opèrent pas sur une instance spécifique (pas de <code>this</code>)</li>
                </ul>
            </div>

            <!-- Exemple complet : Système de bibliothèque -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple complet : Système de gestion de bibliothèque</h2>
                <p class="textExemple">
                    Appliquons tous les concepts avec un exemple réel : un système de gestion de livres.
                </p>

                <div class="code-example">
                    <h4 class="text-purple">Livre.java</h4>
                    <pre v-pre><code class="language-java">import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

public class Livre {
    // Attributs
    private String isbn;
    private String titre;
    private String auteur;
    private int anneePublication;
    private boolean estEmprunte;
    private LocalDate dateEmprunt;
    private static final int DUREE_EMPRUNT_JOURS = 14;
    private static int totalLivres = 0;
    private static int livresEmpruntes = 0;
    
    // Constructeurs
    public Livre(String isbn, String titre, String auteur, int anneePublication) {
        this.isbn = isbn;
        this.titre = titre;
        this.auteur = auteur;
        this.anneePublication = anneePublication;
        this.estEmprunte = false;
        this.dateEmprunt = null;
        totalLivres++;
    }
    
    // Getters
    public String getIsbn() { return isbn; }
    public String getTitre() { return titre; }
    public String getAuteur() { return auteur; }
    public int getAnneePublication() { return anneePublication; }
    public boolean isEstEmprunte() { return estEmprunte; }
    public LocalDate getDateEmprunt() { return dateEmprunt; }
    
    // Setters avec validation
    public void setTitre(String titre) {
        if (titre != null && titre.length() >= 2) {
            this.titre = titre;
        }
    }
    
    public void setAnneePublication(int annee) {
        if (annee >= 1450 && annee <= LocalDate.now().getYear()) {
            this.anneePublication = annee;
        }
    }
    
    // Méthodes métier
    public boolean emprunter() {
        if (!estEmprunte) {
            estEmprunte = true;
            dateEmprunt = LocalDate.now();
            livresEmpruntes++;
            System.out.println("Livre '" + titre + "' emprunté avec succès");
            return true;
        } else {
            System.out.println("Livre '" + titre + "' déjà emprunté");
            return false;
        }
    }
    
    public boolean retourner() {
        if (estEmprunte) {
            estEmprunte = false;
            
            // Calcul des jours de retard
            long joursRetard = calculerJoursRetard();
            if (joursRetard > 0) {
                System.out.println("Attention: Retard de " + joursRetard + " jours");
            }
            
            dateEmprunt = null;
            livresEmpruntes--;
            System.out.println("Livre '" + titre + "' retourné avec succès");
            return true;
        } else {
            System.out.println("Livre '" + titre + "' n'était pas emprunté");
            return false;
        }
    }
    
    private long calculerJoursRetard() {
        if (dateEmprunt != null) {
            LocalDate dateRetourPrevue = dateEmprunt.plusDays(DUREE_EMPRUNT_JOURS);
            LocalDate aujourdhui = LocalDate.now();
            
            if (aujourdhui.isAfter(dateRetourPrevue)) {
                return ChronoUnit.DAYS.between(dateRetourPrevue, aujourdhui);
            }
        }
        return 0;
    }
    
    public boolean estEnRetard() {
        return calculerJoursRetard() > 0;
    }
    
    public void afficherDetails() {
        System.out.println("=== Détails du Livre ===");
        System.out.println("ISBN: " + isbn);
        System.out.println("Titre: " + titre);
        System.out.println("Auteur: " + auteur);
        System.out.println("Année: " + anneePublication);
        System.out.println("Statut: " + (estEmprunte ? "Emprunté" : "Disponible"));
        
        if (estEmprunte && dateEmprunt != null) {
            System.out.println("Emprunté le: " + dateEmprunt);
            System.out.println("À retourner avant: " + dateEmprunt.plusDays(DUREE_EMPRUNT_JOURS));
            
            long joursRetard = calculerJoursRetard();
            if (joursRetard > 0) {
                System.out.println("⚠ RETARD de " + joursRetard + " jours");
            }
        }
        System.out.println("=======================");
    }
    
    // Méthodes statiques
    public static int getTotalLivres() {
        return totalLivres;
    }
    
    public static int getLivresEmpruntes() {
        return livresEmpruntes;
    }
    
    public static int getLivresDisponibles() {
        return totalLivres - livresEmpruntes;
    }
    
    public static void afficherStatistiques() {
        System.out.println("\n=== STATISTIQUES DE LA BIBLIOTHÈQUE ===");
        System.out.println("Total livres: " + getTotalLivres());
        System.out.println("Livres empruntés: " + getLivresEmpruntes());
        System.out.println("Livres disponibles: " + getLivresDisponibles());
        System.out.println("======================================\n");
    }
}</code></pre>
                </div>

                <div class="code-example">
                    <h4 class="text-purple">Main.java - Programme de test</h4>
                    <pre v-pre><code class="language-java">import java.time.LocalDate;

public class Main {
    public static void main(String[] args) {
        // Afficher les statistiques initiales
        Livre.afficherStatistiques();
        
        // Création de livres
        Livre livre1 = new Livre("978-0134685991", "Effective Java", "Joshua Bloch", 2018);
        Livre livre2 = new Livre("978-0596009205", "Head First Java", "Kathy Sierra", 2005);
        Livre livre3 = new Livre("978-1491956257", "Java Concurrency in Practice", "Brian Goetz", 2006);
        
        // Afficher les statistiques après création
        Livre.afficherStatistiques();
        
        // Emprunter des livres
        System.out.println("\n=== Emprunts ===");
        livre1.emprunter();
        livre2.emprunter();
        
        // Essayer d'emprunter un livre déjà emprunté
        livre1.emprunter();
        
        // Afficher les détails
        System.out.println("\n=== Détails des livres ===");
        livre1.afficherDetails();
        livre2.afficherDetails();
        livre3.afficherDetails();
        
        // Retourner un livre
        System.out.println("\n=== Retour ===");
        livre1.retourner();
        
        // Statistiques finales
        Livre.afficherStatistiques();
        
        // Tester les setters
        System.out.println("\n=== Modification ===");
        livre1.setTitre("Effective Java 3rd Edition");
        livre1.setAnneePublication(2018);
        livre1.afficherDetails();
        
        // Tester une année invalide
        livre1.setAnneePublication(1300); // Ne sera pas acceptée
    }
}</code></pre>
                </div>
            </div>

            <!-- Bonnes pratiques -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques de conception de classes</h2>
                <ul class="textExemple">
                    <li><strong>Nommage</strong> : Utilisez des noms significatifs (CamelCase pour les classes)</li>
                    <li><strong>Encapsulation</strong> : Toujours rendre les attributs privés et fournir des accesseurs</li>
                    <li><strong>Responsabilité unique</strong> : Une classe = une responsabilité</li>
                    <li><strong>Constructeurs</strong> : Fournissez toujours un constructeur par défaut</li>
                    <li><strong>Immuabilité</strong> : Rendez les classes immuables quand c'est possible</li>
                    <li><strong>Documentation</strong> : Commentez votre code avec JavaDoc</li>
                    <li><strong>Validation</strong> : Validez les paramètres dans les setters et constructeurs</li>
                </ul>

                <div class="code-example">
                    <h4 class="text-purple">Exemple de classe bien conçue avec JavaDoc</h4>
                    <pre v-pre><code class="language-java">/**
 * Représente un compte bancaire avec les opérations de base.
 * Cette classe est immuable pour les données sensibles.
 * 
 * @author Votre Nom
 * @version 1.0
 */
public final class CompteSecurise {
    
    /** Numéro de compte unique et immuable */
    private final String numeroCompte;
    
    /** Solde courant du compte */
    private double solde;
    
    /** Nom du titulaire du compte */
    private String titulaire;
    
    /**
     * Constructeur pour créer un nouveau compte.
     * 
     * @param numeroCompte Numéro unique du compte (non null)
     * @param titulaire Nom du titulaire (non null)
     * @param soldeInitial Solde initial (doit être positif)
     * @throws IllegalArgumentException si les paramètres sont invalides
     */
    public CompteSecurise(String numeroCompte, String titulaire, double soldeInitial) {
        // Validation des paramètres
        if (numeroCompte == null || numeroCompte.trim().isEmpty()) {
            throw new IllegalArgumentException("Le numéro de compte ne peut pas être null ou vide");
        }
        if (titulaire == null || titulaire.trim().isEmpty()) {
            throw new IllegalArgumentException("Le titulaire ne peut pas être null ou vide");
        }
        if (soldeInitial < 0) {
            throw new IllegalArgumentException("Le solde initial ne peut pas être négatif");
        }
        
        this.numeroCompte = numeroCompte;
        this.titulaire = titulaire.trim();
        this.solde = soldeInitial;
    }
    
    /**
     * Retourne le numéro de compte.
     * 
     * @return le numéro de compte (jamais null)
     */
    public String getNumeroCompte() {
        return numeroCompte;
    }
    
    /**
     * Retourne le solde courant.
     * 
     * @return le solde courant
     */
    public double getSolde() {
        return solde;
    }
    
    /**
     * Dépose un montant sur le compte.
     * 
     * @param montant le montant à déposer (doit être positif)
     * @return le nouveau solde après dépôt
     * @throws IllegalArgumentException si le montant est négatif
     */
    public double deposer(double montant) {
        if (montant <= 0) {
            throw new IllegalArgumentException("Le montant à déposer doit être positif");
        }
        solde += montant;
        return solde;
    }
    
    /**
     * Retire un montant du compte.
     * 
     * @param montant le montant à retirer (doit être positif)
     * @return true si le retrait a réussi, false sinon
     * @throws IllegalArgumentException si le montant est négatif
     */
    public boolean retirer(double montant) {
        if (montant <= 0) {
            throw new IllegalArgumentException("Le montant à retirer doit être positif");
        }
        if (montant <= solde) {
            solde -= montant;
            return true;
        }
        return false;
    }
    
    /**
     * Affiche le solde du compte.
     */
    public void afficherSolde() {
        System.out.println("Compte: " + numeroCompte);
        System.out.println("Titulaire: " + titulaire);
        System.out.println("Solde: " + solde + "€");
    }
}</code></pre>
                </div>
            </div>

            <!-- Conclusion et ressources -->
            <div class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion et ressources</h2>
                <p class="textExemple">
                    Félicitations ! Vous maîtrisez maintenant les bases de la création de classes en Java.
                    Vous pouvez créer des classes bien structurées, encapsulées et maintenables.
                </p>

                <h3 class="text-purple">Prochaines étapes :</h3>
                <ul class="textExemple">
                    <li>Apprendre l'héritage et le polymorphisme</li>
                    <li>Découvrir les interfaces et les classes abstraites</li>
                    <li>Explorer les collections Java (List, Set, Map)</li>
                    <li>Maîtriser les exceptions et la gestion d'erreurs</li>
                    <li>Découvrir les génériques (Generics)</li>
                </ul>

                <h3 class="text-purple">Ressources supplémentaires :</h3>
                <ul class="textExemple">
                    <li><a href="https://docs.oracle.com/javase/tutorial/java/concepts/index.html" target="_blank"
                            class="btn-purple btn-hover">Tutoriel officiel Java - Concepts POO</a></li>
                    <li><a href="https://www.oreilly.com/library/view/effective-java/9780134686097/" target="_blank"
                            class="btn-purple btn-hover">Effective Java (Joshua Bloch)</a></li>
                    <li><a href="https://www.codecademy.com/learn/learn-java" target="_blank" class="btn-purple btn-hover">Codecademy - Learn Java</a></li>
                    <li><a href="https://github.com/iluwatar/java-design-patterns" target="_blank" class="btn-purple btn-hover">Design Patterns en Java</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
</script>

<style scoped>
/* Styles adaptés aux couleurs violettes de votre projet */
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

/* Header avec le style gradient violet */
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

/* Sections de leçon */
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

/* Classes CSS avec couleurs violettes */
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

/* Boutons violets */
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

/* CORRECTION RESPONSIVE POUR LES BLOCS DE CODE */
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

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* COULEURS POUR JAVA */
.java-keyword {
    color: #569CD6 !important;
}

.java-function {
    color: #DCDCAA !important;
}

.java-class {
    color: #4EC9B0 !important;
}

.java-variable {
    color: #9CDCFE !important;
}

.java-string {
    color: #CE9178 !important;
}

.java-comment {
    color: #6A9955 !important;
    font-style: italic;
}

.java-number {
    color: #B5CEA8 !important;
}

/* Tableau des modificateurs d'accès */
.access-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1.5rem 0;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 10px rgba(106, 48, 147, 0.1);
}

.access-table th {
    background: #8B5FBF;
    color: white;
    padding: 12px;
    text-align: left;
}

.access-table td {
    padding: 12px;
    border-bottom: 1px solid #eee;
}

.access-table tr:nth-child(even) {
    background: #f8f6ff;
}

.access-table tr:hover {
    background: #f0e6ff;
}

.access-table td:first-child {
    font-family: monospace;
    color: #6A3093;
    font-weight: bold;
}

/* Texte des exemples */
.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
    color: #333;
}

/* RESPONSIVE DESIGN AMÉLIORÉ */
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
    
    .access-table {
        font-size: 0.9rem;
    }
}

/* POUR LES TRÈS PETITS ÉCRANS */
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
    
    .access-table {
        font-size: 0.8rem;
    }
}

/* POUR LES TRÈS GRANDS ÉCRANS */
@media (min-width: 1400px) {
    .lesson-content {
        max-width: 1300px;
    }
}

/* Animations */
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
.lesson-section:nth-child(6) { animation-delay: 0.6s; }
.lesson-section:nth-child(7) { animation-delay: 0.7s; }
.lesson-section:nth-child(8) { animation-delay: 0.8s; }
.lesson-section:nth-child(9) { animation-delay: 0.9s; }
.lesson-section:nth-child(10) { animation-delay: 1.0s; }
</style>