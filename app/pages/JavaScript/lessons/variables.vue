<template>
    <div class="lesson-container">
        <article class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header bg-gradient-primary">
                <h1 class="text-white">Les variables en JavaScript</h1>
                <p class="lesson-meta text-white">
                    <span>Niveau : Débutant</span>
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Introduction</h2>
                <p>
                    Les variables en JavaScript sont des conteneurs qui permettent de stocker des données.
                    Elles sont essentielles pour manipuler et travailler avec des informations dans vos programmes.
                </p>
            </section>

            <!-- Déclaration de variables -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Déclaration de variables</h2>
                <p>
                    JavaScript offre plusieurs façons de déclarer des variables : <code>var</code>, <code>let</code> et <code>const</code>.
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">var (ancienne méthode)</h3>
                        <pre><code class="language-javascript"><span class="comment">// Déclaration avec var (portée fonction)</span>
<span class="keyword">var</span> <span class="variable">nom</span> = <span class="string">"Jean"</span>;
<span class="keyword">var</span> <span class="variable">age</span> = <span class="number">25</span>;
<span class="keyword">var</span> <span class="variable">estEtudiant</span> = <span class="constant">true</span>;

<span class="comment">// Redéclaration possible</span>
<span class="keyword">var</span> <span class="variable">nom</span> = <span class="string">"Marie"</span>; <span class="comment">// Pas d'erreur</span></code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">let (moderne)</h3>
                        <pre><code class="language-javascript"><span class="comment">// Déclaration avec let (portée bloc)</span>
<span class="keyword">let</span> <span class="variable">prenom</span> = <span class="string">"Alice"</span>;
<span class="keyword">let</span> <span class="variable">score</span> = <span class="number">100</span>;

<span class="comment">// Réassignation possible</span>
<span class="variable">prenom</span> = <span class="string">"Bob"</span>; <span class="comment">// OK</span>

<span class="comment">// Redéclaration impossible</span>
<span class="comment">// let prenom = "Charlie"; // Erreur !</span></code></pre>
                    </div>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">const (constante)</h3>
                    <pre><code class="language-javascript"><span class="comment">// Déclaration avec const (valeur constante)</span>
<span class="keyword">const</span> <span class="variable">PI</span> = <span class="number">3.14159</span>;
<span class="keyword">const</span> <span class="variable">SITE_WEB</span> = <span class="string">"https://mon-site.com"</span>;

<span class="comment">// Ni réassignation ni redéclaration</span>
<span class="comment">// PI = 3.14; // Erreur !</span>
<span class="comment">// const PI = 3.14; // Erreur !</span>

<span class="comment">// Mais les objets et tableaux const peuvent être modifiés</span>
<span class="keyword">const</span> <span class="variable">personne</span> = { <span class="property">nom</span>: <span class="string">"Pierre"</span>, <span class="property">age</span>: <span class="number">30</span> };
<span class="variable">personne</span>.<span class="property">age</span> = <span class="number">31</span>; <span class="comment">// OK</span></code></pre>
                </div>
            </section>

            <!-- Types de données -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Types de données</h2>
                <p>
                    JavaScript est un langage à typage dynamique. Les variables peuvent contenir différents types de données.
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">Types primitifs</h3>
                        <pre><code class="language-javascript"><span class="comment">// String (chaîne de caractères)</span>
<span class="keyword">let</span> <span class="variable">message</span> = <span class="string">"Bonjour le monde!"</span>;
<span class="keyword">let</span> <span class="variable">nom</span> = <span class="string">'Alice'</span>;
<span class="keyword">let</span> <span class="variable">texte</span> = <span class="string">`Template literal`</span>;

<span class="comment">// Number (nombre)</span>
<span class="keyword">let</span> <span class="variable">age</span> = <span class="number">25</span>;
<span class="keyword">let</span> <span class="variable">prix</span> = <span class="number">19.99</span>;
<span class="keyword">let</span> <span class="variable">infini</span> = <span class="constant">Infinity</span>;

<span class="comment">// Boolean (booléen)</span>
<span class="keyword">let</span> <span class="variable">estActif</span> = <span class="constant">true</span>;
<span class="keyword">let</span> <span class="variable">estCharge</span> = <span class="constant">false</span>;

<span class="comment">// Undefined</span>
<span class="keyword">let</span> <span class="variable">nonDefini</span>;
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">nonDefini</span>); <span class="comment">// undefined</span>

<span class="comment">// Null</span>
<span class="keyword">let</span> <span class="variable">vide</span> = <span class="constant">null</span>;</code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">Types complexes</h3>
                        <pre><code class="language-javascript"><span class="comment">// Object (objet)</span>
<span class="keyword">let</span> <span class="variable">personne</span> = {
    <span class="property">nom</span>: <span class="string">"Jean"</span>,
    <span class="property">age</span>: <span class="number">30</span>,
    <span class="property">ville</span>: <span class="string">"Paris"</span>
};

<span class="comment">// Array (tableau)</span>
<span class="keyword">let</span> <span class="variable">couleurs</span> = [<span class="string">"rouge"</span>, <span class="string">"vert"</span>, <span class="string">"bleu"</span>];
<span class="keyword">let</span> <span class="variable">nombres</span> = [<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>, <span class="number">4</span>, <span class="number">5</span>];

<span class="comment">// Function (fonction)</span>
<span class="keyword">let</span> <span class="variable">salutation</span> = <span class="keyword">function</span>() {
    <span class="keyword">return</span> <span class="string">"Bonjour!"</span>;
};

<span class="comment">// Date</span>
<span class="keyword">let</span> <span class="variable">maintenant</span> = <span class="keyword">new</span> <span class="class-name">Date</span>();</code></pre>
                    </div>
                </div>
            </section>

            <!-- Portée des variables -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Portée des variables</h2>
                <p>
                    La portée détermine où une variable est accessible dans le code.
                </p>

                <div class="code-example">
                    <h3 class="text-purple">Portée globale, fonction et bloc</h3>
                    <pre><code class="language-javascript"><span class="comment">// Portée globale</span>
<span class="keyword">var</span> <span class="variable">variableGlobale</span> = <span class="string">"Je suis globale"</span>;
<span class="keyword">let</span> <span class="variable">globaleLet</span> = <span class="string">"Je suis aussi globale"</span>;

<span class="keyword">function</span> <span class="function">montrerPortee</span>() {
    <span class="comment">// Portée de fonction (var)</span>
    <span class="keyword">var</span> <span class="variable">variableFonction</span> = <span class="string">"Je suis dans la fonction"</span>;
    
    <span class="comment">// Portée de bloc (let/const)</span>
    <span class="keyword">if</span> (<span class="constant">true</span>) {
        <span class="keyword">let</span> <span class="variable">variableBloc</span> = <span class="string">"Je suis dans le bloc"</span>;
        <span class="keyword">const</span> <span class="variable">CONSTANTE_BLOC</span> = <span class="string">"Constante dans le bloc"</span>;
        
        <span class="function">console</span>.<span class="function">log</span>(<span class="variable">variableBloc</span>); <span class="comment">// OK</span>
        <span class="function">console</span>.<span class="function">log</span>(<span class="variable">variableFonction</span>); <span class="comment">// OK</span>
        <span class="function">console</span>.<span class="function">log</span>(<span class="variable">variableGlobale</span>); <span class="comment">// OK</span>
    }
    
    <span class="comment">// console.log(variableBloc); // ERREUR !</span>
    <span class="function">console</span>.<span class="function">log</span>(<span class="variable">variableFonction</span>); <span class="comment">// OK</span>
}

<span class="function">montrerPortee</span>();</code></pre>
                </div>
            </section>

            <!-- Hoisting -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Hoisting (hissage)</h2>
                <p>
                    Le hoisting est le comportement de JavaScript qui "remonte" les déclarations de variables
                    en haut de leur portée.
                </p>

                <div class="code-comparison">
                    <div class="code-block">
                        <h3 class="text-purple">Avec var</h3>
                        <pre><code class="language-javascript"><span class="comment">// Ce code...</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">x</span>); <span class="comment">// undefined</span>
<span class="keyword">var</span> <span class="variable">x</span> = <span class="number">5</span>;

<span class="comment">// ...est interprété comme :</span>
<span class="keyword">var</span> <span class="variable">x</span>;
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">x</span>); <span class="comment">// undefined</span>
<span class="variable">x</span> = <span class="number">5</span>;</code></pre>
                    </div>

                    <div class="code-block">
                        <h3 class="text-purple">Avec let/const</h3>
                        <pre><code class="language-javascript"><span class="comment">// Avec let/const, pas d'initialisation</span>
<span class="comment">// console.log(y); // Erreur !</span>
<span class="keyword">let</span> <span class="variable">y</span> = <span class="number">10</span>;

<span class="comment">// La zone avant déclaration s'appelle "Temporal Dead Zone"</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="variable">z</span>); <span class="comment">// Erreur !</span>
<span class="keyword">const</span> <span class="variable">z</span> = <span class="number">15</span>;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Conversion de types -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Conversion de types</h2>

                <div class="code-example">
                    <h3 class="text-purple">Conversion explicite</h3>
                    <pre><code class="language-javascript"><span class="comment">// Conversion en string</span>
<span class="keyword">let</span> <span class="variable">nombre</span> = <span class="number">42</span>;
<span class="keyword">let</span> <span class="variable">chaine</span> = <span class="function">String</span>(<span class="variable">nombre</span>); <span class="comment">// "42"</span>
<span class="keyword">let</span> <span class="variable">chaine2</span> = <span class="variable">nombre</span>.<span class="function">toString</span>(); <span class="comment">// "42"</span>

<span class="comment">// Conversion en number</span>
<span class="keyword">let</span> <span class="variable">texte</span> = <span class="string">"123"</span>;
<span class="keyword">let</span> <span class="variable">num</span> = <span class="function">Number</span>(<span class="variable">texte</span>); <span class="comment">// 123</span>
<span class="keyword">let</span> <span class="variable">num2</span> = <span class="function">parseInt</span>(<span class="string">"123px"</span>); <span class="comment">// 123</span>
<span class="keyword">let</span> <span class="variable">num3</span> = <span class="function">parseFloat</span>(<span class="string">"3.14"</span>); <span class="comment">// 3.14</span>

<span class="comment">// Conversion en boolean</span>
<span class="keyword">let</span> <span class="variable">valeur</span> = <span class="string">"texte"</span>;
<span class="keyword">let</span> <span class="variable">bool</span> = <span class="function">Boolean</span>(<span class="variable">valeur</span>); <span class="comment">// true</span></code></pre>
                </div>

                <div class="code-example">
                    <h3 class="text-purple">Conversion implicite</h3>
                    <pre><code class="language-javascript"><span class="comment">// Concaténation de strings</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="string">"5"</span> + <span class="number">3</span>); <span class="comment">// "53" (string)</span>

<span class="comment">// Opérations mathématiques</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="string">"5"</span> - <span class="number">3</span>); <span class="comment">// 2 (number)</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="string">"5"</span> * <span class="string">"2"</span>); <span class="comment">// 10 (number)</span>

<span class="comment">// Conversion en boolean (falsy values)</span>
<span class="function">console</span>.<span class="function">log</span>(!!<span class="string">""</span>); <span class="comment">// false</span>
<span class="function">console</span>.<span class="function">log</span>(!!<span class="number">0</span>); <span class="comment">// false</span>
<span class="function">console</span>.<span class="function">log</span>(!!<span class="constant">null</span>); <span class="comment">// false</span>
<span class="function">console</span>.<span class="function">log</span>(!!<span class="constant">undefined</span>); <span class="comment">// false</span>
<span class="function">console</span>.<span class="function">log</span>(!!<span class="constant">NaN</span>); <span class="comment">// false</span></code></pre>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li>Utilisez <code>const</code> par défaut, et <code>let</code> seulement quand la variable doit changer</li>
                    <li>Évitez <code>var</code> dans le code moderne</li>
                    <li>Utilisez des noms de variables descriptifs (camelCase)</li>
                    <li>Déclarez les variables en haut de leur portée</li>
                    <li>Initialisez les variables lors de leur déclaration</li>
                    <li>Utilisez <code>const</code> pour les valeurs qui ne changent pas</li>
                    <li>Évitez les variables globales quand c'est possible</li>
                </ul>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1: Calculatrice simple</h3>
                    <p>
                        Créez des variables pour stocker deux nombres et affichez le résultat de leurs opérations :
                    </p>

                    <details class="solution">
                        <summary class="btn btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-javascript"><span class="comment">// Déclaration des variables</span>
<span class="keyword">const</span> <span class="variable">nombre1</span> = <span class="number">15</span>;
<span class="keyword">const</span> <span class="variable">nombre2</span> = <span class="number">3</span>;

<span class="comment">// Calculs</span>
<span class="keyword">const</span> <span class="variable">somme</span> = <span class="variable">nombre1</span> + <span class="variable">nombre2</span>;
<span class="keyword">const</span> <span class="variable">difference</span> = <span class="variable">nombre1</span> - <span class="variable">nombre2</span>;
<span class="keyword">const</span> <span class="variable">produit</span> = <span class="variable">nombre1</span> * <span class="variable">nombre2</span>;
<span class="keyword">const</span> <span class="variable">quotient</span> = <span class="variable">nombre1</span> / <span class="variable">nombre2</span>;

<span class="comment">// Affichage des résultats</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`<span class="variable">${nombre1}</span> + <span class="variable">${nombre2}</span> = <span class="variable">${somme}</span>`</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`<span class="variable">${nombre1}</span> - <span class="variable">${nombre2}</span> = <span class="variable">${difference}</span>`</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`<span class="variable">${nombre1}</span> * <span class="variable">${nombre2}</span> = <span class="variable">${produit}</span>`</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`<span class="variable">${nombre1}</span> / <span class="variable">${nombre2}</span> = <span class="variable">${quotient}</span>`</span>);</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2: Gestion de profil utilisateur</h3>
                    <p>
                        Créez un objet représentant un utilisateur avec différentes propriétés :
                    </p>

                    <details class="solution">
                        <summary class="btn btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre><code class="language-javascript"><span class="comment">// Création de l'objet utilisateur</span>
<span class="keyword">const</span> <span class="variable">utilisateur</span> = {
    <span class="property">nom</span>: <span class="string">"Dupont"</span>,
    <span class="property">prenom</span>: <span class="string">"Marie"</span>,
    <span class="property">age</span>: <span class="number">28</span>,
    <span class="property">email</span>: <span class="string">"marie.dupont@email.com"</span>,
    <span class="property">estActif</span>: <span class="constant">true</span>,
    <span class="property">competences</span>: [<span class="string">"JavaScript"</span>, <span class="string">"HTML"</span>, <span class="string">"CSS"</span>]
};

<span class="comment">// Accès aux propriétés</span>
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`Nom: <span class="variable">${utilisateur.nom}</span>`</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`Âge: <span class="variable">${utilisateur.age}</span> ans`</span>);
<span class="function">console</span>.<span class="function">log</span>(<span class="string">`Compétences: <span class="variable">${utilisateur.competences.join(", ")}</span>`</span>);

<span class="comment">// Modification d'une propriété</span>
<span class="variable">utilisateur</span>.<span class="property">age</span> = <span class="number">29</span>;
<span class="variable">utilisateur</span>.<span class="property">competences</span>.<span class="function">push</span>(<span class="string">"React"</span>);

<span class="function">console</span>.<span class="function">log</span>(<span class="string">"Profil mis à jour:"</span>, <span class="variable">utilisateur</span>);</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section card border-purple bg-light-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p>
                    Les variables sont la base de tout programme JavaScript. Comprendre la différence entre
                    <code>var</code>, <code>let</code> et <code>const</code>, ainsi que les types de données
                    et la portée des variables, est essentiel pour écrire du code robuste et maintenable.
                </p>
            </section>
        </article>
    </div>
</template>

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

/* Header avec le style gradient */
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

/* Classes CSS de l'autre page */
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

/* Boutons */
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
    white-space: pre-wrap; /* Permet le retour à la ligne */
    word-wrap: break-word; /* Casse les mots longs */
    word-break: break-word; /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap; /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword { color: #569cd6 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.property { color: #9cdcfe !important; }
.class-name { color: #4ec9b0 !important; }

/* Exercices et solutions */
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

details summary {
    cursor: pointer;
    outline: none;
}

/* Texte des exemples */
.textExemple {
    margin-bottom: 1rem;
    line-height: 1.6;
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
</style>