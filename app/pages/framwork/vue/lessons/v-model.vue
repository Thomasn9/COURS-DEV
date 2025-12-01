<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les v-model en Vue.js</h1>
                <p class="lesson-meta text-white">Maîtrisez la liaison bidirectionnelle des données</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction aux v-model</h2>
                <p class="textExemple">
                    Le <code v-pre>v-model</code> est une directive de Vue.js qui permet de créer une liaison
                    bidirectionnelle
                    entre les éléments de formulaire (input, textarea, select) et les données de l'application.
                    C'est l'une des fonctionnalités les plus puissantes de Vue.js pour la gestion des formulaires.
                </p>
                <p class="textExemple">
                    En arrière-plan, <code v-pre>v-model</code> est essentiellement un sucre syntaxique qui combine
                    <code v-pre>v-bind</code> pour lier la valeur et <code v-pre>v-on</code> pour écouter les événements
                    d'entrée.
                </p>
            </section>

            <!-- Syntaxe de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Syntaxe de base</h2>
                <p class="textExemple">
                    La syntaxe de base de <code v-pre>v-model</code> est très simple :
                </p>

                <div class="code-example">
                    <pre v-pre><code><span class="html-tag">&lt;template&gt;</span>
  <span class="html-tag">&lt;div&gt;</span>
    <span class="html-tag">&lt;input</span> <span class="vue-directive">v-model</span>=<span class="string">"message"</span> <span class="html-attribute">placeholder</span>=<span class="string">"Éditez-moi"</span><span class="html-tag">&gt;</span>
    <span class="html-tag">&lt;p&gt;</span>Message est: {{ message }}<span class="html-tag">&lt;/p&gt;</span>
  <span class="html-tag">&lt;/div&gt;</span>
<span class="html-tag">&lt;/template&gt;</span>

<span class="html-tag">&lt;script&gt;</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">data</span>() {
    <span class="keyword">return</span> {
      <span class="variable">message</span>: <span class="string">''</span>
    }
  }
}
<span class="html-tag">&lt;/script&gt;</span></code></pre>
                </div>

                <p class="textExemple">
                    Dans cet exemple, chaque fois que l'utilisateur tape dans l'input, la propriété <code
                        v-pre>message</code>
                    est automatiquement mise à jour, et vice versa.
                </p>
            </section>

            <!-- Utilisation avec différents éléments -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Utilisation avec différents éléments de formulaire</h2>

                <h3 class="text-purple">Input texte</h3>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"text"</span> <span class="vue-directive">v-model</span>=<span class="string">"nom"</span><span class="html-tag">&gt;</span></code></pre>
                </div>

                <h3 class="text-purple">Textarea</h3>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;textarea</span> <span class="vue-directive">v-model</span>=<span class="string">"message"</span><span class="html-tag">&gt;</span><span class="html-tag">&lt;/textarea&gt;</span></code></pre>
                </div>

                <h3 class="text-purple">Checkbox</h3>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"checkbox"</span> <span class="html-attribute">id</span>=<span class="string">"checkbox"</span> <span class="vue-directive">v-model</span>=<span class="string">"accepte"</span><span class="html-tag">&gt;</span>
<span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"checkbox"</span><span class="html-tag">&gt;</span>J'accepte les conditions<span class="html-tag">&lt;/label&gt;</span></code></pre>
                </div>

                <h3 class="text-purple">Boutons radio</h3>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"radio"</span> <span class="html-attribute">id</span>=<span class="string">"un"</span> <span class="html-attribute">value</span>=<span class="string">"Un"</span> <span class="vue-directive">v-model</span>=<span class="string">"choix"</span><span class="html-tag">&gt;</span>
<span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"un"</span><span class="html-tag">&gt;</span>Un<span class="html-tag">&lt;/label&gt;</span>
<span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"radio"</span> <span class="html-attribute">id</span>=<span class="string">"deux"</span> <span class="html-attribute">value</span>=<span class="string">"Deux"</span> <span class="vue-directive">v-model</span>=<span class="string">"choix"</span><span class="html-tag">&gt;</span>
<span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"deux"</span><span class="html-tag">&gt;</span>Deux<span class="html-tag">&lt;/label&gt;</span></code></pre>
                </div>

                <h3 class="text-purple">Select</h3>
                <div class="code-example">
                    <pre v-pre><code><span class="html-tag">&lt;select</span> <span class="vue-directive">v-model</span>=<span class="string">"selectionne"</span><span class="html-tag">&gt;</span>
  <span class="html-tag">&lt;option</span> <span class="html-attribute">disabled</span> <span class="html-attribute">value</span>=<span class="string">""</span><span class="html-tag">&gt;</span>Choisissez une option<span class="html-tag">&lt;/option&gt;</span>
  <span class="html-tag">&lt;option&gt;</span>A<span class="html-tag">&lt;/option&gt;</span>
  <span class="html-tag">&lt;option&gt;</span>B<span class="html-tag">&lt;/option&gt;</span>
  <span class="html-tag">&lt;option&gt;</span>C<span class="html-tag">&lt;/option&gt;</span>
<span class="html-tag">&lt;/select&gt;</span></code></pre>
                </div>
            </section>

            <!-- Modificateurs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Modificateurs de v-model</h2>

                <h3 class="text-purple">.lazy</h3>
                <p class="textExemple">
                    Par défaut, <code v-pre>v-model</code> synchronise l'input après chaque événement <code
                        v-pre>input</code>.
                    Avec <code v-pre>.lazy</code>, la synchronisation se fait après l'événement <code
                        v-pre>change</code>.
                </p>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;input</span> <span class="vue-directive">v-model.lazy</span>=<span class="string">"message"</span><span class="html-tag">&gt;</span></code></pre>
                </div>

                <h3 class="text-purple">.number</h3>
                <p class="textExemple">
                    Convertit automatiquement l'entrée utilisateur en nombre.
                </p>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;input</span> <span class="vue-directive">v-model.number</span>=<span class="string">"age"</span> <span class="html-attribute">type</span>=<span class="string">"number"</span><span class="html-tag">&gt;</span></code></pre>
                </div>

                <h3 class="text-purple">.trim</h3>
                <p class="textExemple">
                    Supprime automatiquement les espaces blancs au début et à la fin de l'entrée.
                </p>
                <div class="code-example">
                    <pre
                        v-pre><code><span class="html-tag">&lt;input</span> <span class="vue-directive">v-model.trim</span>=<span class="string">"message"</span><span class="html-tag">&gt;</span></code></pre>
                </div>
            </section>

            <!-- v-model avec les composants -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">v-model avec les composants personnalisés</h2>
                <p class="textExemple">
                    Dans Vue 3, <code v-pre>v-model</code> peut être utilisé avec des composants personnalisés.
                    Par défaut, <code v-pre>v-model</code> sur un composant utilise <code v-pre>modelValue</code> comme
                    prop
                    et <code v-pre>update:modelValue</code> comme événement.
                </p>

                <div class="code-comparison">
                    <div>
                        <h4 class="text-purple">Composant enfant</h4>
                        <pre v-pre><code><span class="html-tag">&lt;template&gt;</span>
  <span class="html-tag">&lt;input</span>
    <span class="vue-directive">:value</span>=<span class="string">"modelValue"</span>
    <span class="vue-directive">@input</span>=<span class="string">"$emit('update:modelValue', $event.target.value)"</span>
  <span class="html-tag">&gt;</span>
<span class="html-tag">&lt;/template&gt;</span>

<span class="html-tag">&lt;script&gt;</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="variable">props</span>: [<span class="string">'modelValue'</span>],
  <span class="variable">emits</span>: [<span class="string">'update:modelValue'</span>]
}
<span class="html-tag">&lt;/script&gt;</span></code></pre>
                    </div>

                    <div>
                        <h4 class="text-purple">Utilisation du composant</h4>
                        <pre
                            v-pre><code><span class="html-tag">&lt;CustomInput</span> <span class="vue-directive">v-model</span>=<span class="string">"searchText"</span> <span class="html-tag">/&gt;</span></code></pre>
                    </div>
                </div>
            </section>

            <!-- Exemple pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple pratique complet</h2>
                <p class="textExemple">
                    Voici un exemple complet utilisant plusieurs types d'inputs avec <code v-pre>v-model</code> :
                </p>

                <div class="code-example">
                    <pre v-pre><code><span class="html-tag">&lt;template&gt;</span>
  <span class="html-tag">&lt;div&gt;</span>
    <span class="html-tag">&lt;h3&gt;</span>Formulaire d'inscription<span class="html-tag">&lt;/h3&gt;</span>
    
    <span class="comment">&lt;!-- Input texte --&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"nom"</span><span class="html-tag">&gt;</span>Nom:<span class="html-tag">&lt;/label&gt;</span>
      <span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"text"</span> <span class="html-attribute">id</span>=<span class="string">"nom"</span> <span class="vue-directive">v-model.trim</span>=<span class="string">"nom"</span><span class="html-tag">&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="comment">&lt;!-- Email --&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"email"</span><span class="html-tag">&gt;</span>Email:<span class="html-tag">&lt;/label&gt;</span>
      <span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"email"</span> <span class="html-attribute">id</span>=<span class="string">"email"</span> <span class="vue-directive">v-model.lazy</span>=<span class="string">"email"</span><span class="html-tag">&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="comment">&lt;!-- Âge --&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"age"</span><span class="html-tag">&gt;</span>Âge:<span class="html-tag">&lt;/label&gt;</span>
      <span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"number"</span> <span class="html-attribute">id</span>=<span class="string">"age"</span> <span class="vue-directive">v-model.number</span>=<span class="string">"age"</span><span class="html-tag">&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="comment">&lt;!-- Checkbox --&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"checkbox"</span> <span class="html-attribute">id</span>=<span class="string">"newsletter"</span> <span class="vue-directive">v-model</span>=<span class="string">"newsletter"</span><span class="html-tag">&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"newsletter"</span><span class="html-tag">&gt;</span>S'abonner à la newsletter<span class="html-tag">&lt;/label&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="comment">&lt;!-- Boutons radio --&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"radio"</span> <span class="html-attribute">id</span>=<span class="string">"homme"</span> <span class="html-attribute">value</span>=<span class="string">"homme"</span> <span class="vue-directive">v-model</span>=<span class="string">"genre"</span><span class="html-tag">&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"homme"</span><span class="html-tag">&gt;</span>Homme<span class="html-tag">&lt;/label&gt;</span>
      <span class="html-tag">&lt;input</span> <span class="html-attribute">type</span>=<span class="string">"radio"</span> <span class="html-attribute">id</span>=<span class="string">"femme"</span> <span class="html-attribute">value</span>=<span class="string">"femme"</span> <span class="vue-directive">v-model</span>=<span class="string">"genre"</span><span class="html-tag">&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"femme"</span><span class="html-tag">&gt;</span>Femme<span class="html-tag">&lt;/label&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="comment">&lt;!-- Select --&gt;</span>
    <span class="html-tag">&lt;div&gt;</span>
      <span class="html-tag">&lt;label</span> <span class="html-attribute">for</span>=<span class="string">"pays"</span><span class="html-tag">&gt;</span>Pays:<span class="html-tag">&lt;/label&gt;</span>
      <span class="html-tag">&lt;select</span> <span class="html-attribute">id</span>=<span class="string">"pays"</span> <span class="vue-directive">v-model</span>=<span class="string">"pays"</span><span class="html-tag">&gt;</span>
        <span class="html-tag">&lt;option</span> <span class="html-attribute">value</span>=<span class="string">""</span><span class="html-tag">&gt;</span>Choisissez un pays<span class="html-tag">&lt;/option&gt;</span>
        <span class="html-tag">&lt;option</span> <span class="html-attribute">value</span>=<span class="string">"fr"</span><span class="html-tag">&gt;</span>France<span class="html-tag">&lt;/option&gt;</span>
        <span class="html-tag">&lt;option</span> <span class="html-attribute">value</span>=<span class="string">"be"</span><span class="html-tag">&gt;</span>Belgique<span class="html-tag">&lt;/option&gt;</span>
        <span class="html-tag">&lt;option</span> <span class="html-attribute">value</span>=<span class="string">"ch"</span><span class="html-tag">&gt;</span>Suisse<span class="html-tag">&lt;/option&gt;</span>
      <span class="html-tag">&lt;/select&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
    
    <span class="comment">&lt;!-- Affichage des données --&gt;</span>
    <span class="html-tag">&lt;div</span> <span class="html-attribute">class</span>=<span class="string">"resultat"</span><span class="html-tag">&gt;</span>
      <span class="html-tag">&lt;h4&gt;</span>Données saisies:<span class="html-tag">&lt;/h4&gt;</span>
      <span class="html-tag">&lt;p&gt;</span>Nom: {{ nom }}<span class="html-tag">&lt;/p&gt;</span>
      <span class="html-tag">&lt;p&gt;</span>Email: {{ email }}<span class="html-tag">&lt;/p&gt;</span>
      <span class="html-tag">&lt;p&gt;</span>Âge: {{ age }}<span class="html-tag">&lt;/p&gt;</span>
      <span class="html-tag">&lt;p&gt;</span>Newsletter: {{ newsletter ? 'Oui' : 'Non' }}<span class="html-tag">&lt;/p&gt;</span>
      <span class="html-tag">&lt;p&gt;</span>Genre: {{ genre }}<span class="html-tag">&lt;/p&gt;</span>
      <span class="html-tag">&lt;p&gt;</span>Pays: {{ pays }}<span class="html-tag">&lt;/p&gt;</span>
    <span class="html-tag">&lt;/div&gt;</span>
  <span class="html-tag">&lt;/div&gt;</span>
<span class="html-tag">&lt;/template&gt;</span>

<span class="html-tag">&lt;script&gt;</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">data</span>() {
    <span class="keyword">return</span> {
      <span class="variable">nom</span>: <span class="string">''</span>,
      <span class="variable">email</span>: <span class="string">''</span>,
      <span class="variable">age</span>: <span class="number">0</span>,
      <span class="variable">newsletter</span>: <span class="keyword">false</span>,
      <span class="variable">genre</span>: <span class="string">''</span>,
      <span class="variable">pays</span>: <span class="string">''</span>
    }
  }
}
<span class="html-tag">&lt;/script&gt;</span></code></pre>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice pratique</h2>
                <div class="exercise">
                    <p class="textExemple">
                        <strong>Objectif :</strong> Créez un composant de recherche avec un champ de saisie et un bouton
                        de réinitialisation.
                    </p>
                    <p class="textExemple">
                        <strong>Consignes :</strong>
                    </p>
                    <ul class="textExemple">
                        <li>Utilisez <code v-pre>v-model</code> pour lier le champ de recherche à une donnée réactive
                        </li>
                        <li>Ajoutez un bouton qui réinitialise la recherche quand on clique dessus</li>
                        <li>Affichez le nombre de caractères saisis en temps réel</li>
                        <li>Utilisez le modificateur <code v-pre>.trim</code> pour ignorer les espaces</li>
                    </ul>

                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code><span class="html-tag">&lt;template&gt;</span>
  <span class="html-tag">&lt;div&gt;</span>
    <span class="html-tag">&lt;h3&gt;</span>Composant de recherche<span class="html-tag">&lt;/h3&gt;</span>
    <span class="html-tag">&lt;input</span> 
      <span class="html-attribute">type</span>=<span class="string">"text"</span> 
      <span class="vue-directive">v-model.trim</span>=<span class="string">"termeRecherche"</span> 
      <span class="html-attribute">placeholder</span>=<span class="string">"Tapez votre recherche..."</span>
    <span class="html-tag">&gt;</span>
    <span class="html-tag">&lt;button</span> <span class="vue-directive">@click</span>=<span class="string">"reinitialiserRecherche"</span><span class="html-tag">&gt;</span>Réinitialiser<span class="html-tag">&lt;/button&gt;</span>
    <span class="html-tag">&lt;p&gt;</span>Caractères saisis: {{ termeRecherche.length }}<span class="html-tag">&lt;/p&gt;</span>
    <span class="html-tag">&lt;p</span> <span class="vue-directive">v-if</span>=<span class="string">"termeRecherche"</span><span class="html-tag">&gt;</span>Résultats pour: "{{ termeRecherche }}"<span class="html-tag">&lt;/p&gt;</span>
  <span class="html-tag">&lt;/div&gt;</span>
<span class="html-tag">&lt;/template&gt;</span>

<span class="html-tag">&lt;script&gt;</span>
<span class="keyword">export</span> <span class="keyword">default</span> {
  <span class="function">data</span>() {
    <span class="keyword">return</span> {
      <span class="variable">termeRecherche</span>: <span class="string">''</span>
    }
  },
  <span class="variable">methods</span>: {
    <span class="function">reinitialiserRecherche</span>() {
      <span class="keyword">this</span>.<span class="variable">termeRecherche</span> = <span class="string">''</span>
    }
  }
}
<span class="html-tag">&lt;/script&gt;</span></code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Points clés à retenir -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Points clés à retenir</h2>
                <ul class="textExemple">
                    <li><code v-pre>v-model</code> crée une liaison bidirectionnelle entre les données et les éléments
                        de formulaire</li>
                    <li>Il fonctionne avec <code v-pre>input</code>, <code v-pre>textarea</code>, <code
                            v-pre>select</code>, et les composants personnalisés</li>
                    <li>Les modificateurs <code v-pre>.lazy</code>, <code v-pre>.number</code> et <code
                            v-pre>.trim</code> permettent de modifier le comportement par défaut</li>
                    <li>Dans Vue 3, <code v-pre>v-model</code> sur les composants utilise <code v-pre>modelValue</code>
                        et <code v-pre>update:modelValue</code></li>
                    <li><code v-pre>v-model</code> est un sucre syntaxique pour <code v-pre>v-bind:value</code> et <code
                            v-pre>v-on:input</code></li>
                </ul>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-gradient-primary border-purple">
                <h2 class="text-white">Conclusion</h2>
                <div class="text-white">
                    <p class="textExemple">
                        Le <code v-pre>v-model</code> est sans conteste l'une des fonctionnalités les plus élégantes et
                        pratiques de Vue.js.
                        Tout au long de cette leçon, nous avons exploré comment cette directive simplifie
                        considérablement
                        la gestion des formulaires et la synchronisation des données.
                    </p>

                    <div class="conclusion-points">
                        <h4 class="text-white">Ce que vous maîtrisez maintenant :</h4>
                        <ul>
                            <li>La syntaxe de base de <code v-pre>v-model</code> avec différents types d'inputs</li>
                            <li>L'utilisation des modificateurs pour adapter le comportement selon vos besoins</li>
                            <li>L'intégration de <code v-pre>v-model</code> avec des composants personnalisés</li>
                            <li>La création d'interfaces utilisateur réactives et intuitives</li>
                        </ul>
                    </div>

                    <div class="conclusion-benefits">
                        <h4 class="text-white">Les avantages principaux :</h4>
                        <ul>
                            <li><strong>Productivité accrue</strong> : Moins de code à écrire pour gérer la liaison de
                                données</li>
                            <li><strong>Code plus lisible</strong> : La syntaxe est intuitive et facile à comprendre
                            </li>
                            <li><strong>Maintenance simplifiée</strong> : Les modifications sont propagées
                                automatiquement</li>
                            <li><strong>Expérience développeur améliorée</strong> : Moins de bugs liés à la gestion
                                manuelle des états</li>
                        </ul>
                    </div>

                    <p class="textExemple">
                        En maîtrisant <code v-pre>v-model</code>, vous disposez d'un outil puissant pour créer des
                        applications
                        Vue.js modernes, réactives et maintenables. Cette connaissance constitue une base solide
                        pour aborder des concepts plus avancés comme la gestion d'état global avec Pinia ou Vuex.
                    </p>

                    <p class="textExemple">
                        <strong>Prochaine étape :</strong> Pratiquez ces concepts en créant vos propres composants
                        avec <code v-pre>v-model</code> et explorez les v-model multiples dans Vue 3 pour des cas
                        d'usage complexes.
                    </p>
                </div>
            </section>
        </div>
    </div>
</template>

<script>

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

/* COULEURS VS CODE COMPLÈTES */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés JavaScript */
.variable {
    color: #9cdcfe !important;
}

/* Variables et noms de fonctions */
.string {
    color: #ce9178 !important;
}

/* Chaînes de caractères */
.comment {
    color: #6a9955 !important;
}

/* Commentaires */
.function {
    color: #dcdcaa !important;
}

/* Noms de fonctions */
.operator {
    color: #d4d4d4 !important;
}

/* Opérateurs */
.constant {
    color: #4fc1ff !important;
}

/* Constantes */
.number {
    color: #b5cea8 !important;
}

/* Nombres */
.class-name {
    color: #4ec9b0 !important;
}

/* Noms de classes */

/* NOUVELLES CLASSES POUR HTML/VUE */
.html-tag {
    color: #569cd6 !important;
}

/* Balises HTML */
.html-attribute {
    color: #9cdcfe !important;
}

/* Attributs HTML */
.vue-directive {
    color: #c586c0 !important;
}

/* Directives Vue */
.interpolation {
    color: #d7ba7d !important;
}

/* Interpolations {{ }} */

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

.solution-content h4 {
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
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

/* Styles pour la conclusion */
.conclusion-points,
.conclusion-benefits {
    margin: 1.5rem 0;
}

.conclusion-points ul,
.conclusion-benefits ul {
    margin-left: 1.5rem;
}

.conclusion-points li,
.conclusion-benefits li {
    margin-bottom: 0.5rem;
    line-height: 1.6;
}

.conclusion-benefits strong {
    color: #e0d6ff;
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

    .conclusion-points ul,
    .conclusion-benefits ul {
        margin-left: 1rem;
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

.lesson-section:nth-child(1) {
    animation-delay: 0.1s;
}

.lesson-section:nth-child(2) {
    animation-delay: 0.2s;
}

.lesson-section:nth-child(3) {
    animation-delay: 0.3s;
}

.lesson-section:nth-child(4) {
    animation-delay: 0.4s;
}

.lesson-section:nth-child(5) {
    animation-delay: 0.5s;
}

.lesson-section:nth-child(6) {
    animation-delay: 0.6s;
}

.lesson-section:nth-child(7) {
    animation-delay: 0.7s;
}
</style>