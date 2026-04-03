<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Stimulus : JavaScript modeste pour Symfony</h1>
                <p class="lesson-meta text-white">Stimulus • Symfony • WebpackEncore • AssetMapper • Contrôleurs JS</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction à Stimulus</h2>
                <p class="textExemple">
                    <strong>Stimulus</strong> est un framework JavaScript modeste créé par Basecamp (les créateurs de Ruby on Rails).
                    Il est conçu pour enrichir un HTML existant avec des comportements interactifs, sans prendre le contrôle total de la page.
                    Contrairement à React ou Vue, Stimulus ne génère pas le DOM ; il se branche sur le DOM déjà présent.
                </p>
                <p class="textExemple">
                    Dans l'écosystème Symfony, Stimulus est parfaitement intégré via <strong>WebpackEncore</strong> (ou AssetMapper).
                    Il complète Twig et Symfony en apportant la couche "comportement" de manière progressive et maintenable.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-bash"># Installer Stimulus avec WebpackEncore
composer require symfony/stimulus-bundle
# ou avec AssetMapper (Symfony 6.4+)
composer require symfony/stimulus-bundle</code></pre>
                </div>
                <p class="textExemple">La commande installe le bundle et génère les fichiers de base dans <code>assets/controllers/</code>.</p>
            </section>

            <!-- Philosophie de Stimulus -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Philosophie : HTML d'abord</h2>
                <p class="textExemple">
                    Stimulus repose sur trois concepts principaux :
                </p>
                <ul>
                    <li><strong>Contrôleurs</strong> : des classes JavaScript qui encapsulent le comportement.</li>
                    <li><strong>Actions</strong> : connectent des événements DOM (clic, soumission, etc.) à des méthodes du contrôleur.</li>
                    <li><strong>Targets</strong> : permettent d'accéder facilement à des éléments spécifiques à l'intérieur du contrôleur.</li>
                    <li><strong>Values</strong> : des données paramétrables directement dans le HTML (via attributs <code>data-...-value</code>).</li>
                </ul>
                <div class="warning-section">
                    <p>✅ <strong>Principe fondamental</strong> : Stimulus lit le HTML, n'écrit pas le HTML. Le HTML reste la source de vérité.</p>
                </div>
            </section>

            <!-- Structure d'un contrôleur -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer un contrôleur Stimulus</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Génération automatique (Symfony 6.4+)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">php bin/console make:stimulus-controller hello</code></pre>
                    </div>
                    <p>Cette commande crée <code>assets/controllers/hello_controller.js</code>.</p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Contrôleur simple : compteur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// assets/controllers/counter_controller.js
import { Controller } from '@hotwired/stimulus';

export default class extends Controller {
    static targets = ['count'];

    connect() {
        this.count = 0;
        this.updateDisplay();
    }

    increment() {
        this.count++;
        this.updateDisplay();
    }

    decrement() {
        this.count--;
        this.updateDisplay();
    }

    updateDisplay() {
        this.countTarget.textContent = this.count;
    }
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation dans Twig</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;div data-controller="counter"&gt;
    &lt;button data-action="click->counter#decrement"&gt;-&lt;/button&gt;
    &lt;span data-counter-target="count"&gt;0&lt;/span&gt;
    &lt;button data-action="click->counter#increment"&gt;+&lt;/button&gt;
&lt;/div&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Actions -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les actions (<code>data-action</code>)</h2>
                <p class="textExemple">
                    Les actions relient un événement DOM à une méthode du contrôleur.
                    Syntaxe : <code>data-action="[événement]->[contrôleur]#[méthode]"</code>.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Exemples d'actions</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;!-- Clic sur un bouton --&gt;
&lt;button data-action="click->modal#open"&gt;Ouvrir&lt;/button&gt;

&lt;!-- Changement de valeur dans un champ --&gt;
&lt;input data-action="change->search#filter"&gt;

&lt;!-- Souris au-dessus --&gt;
&lt;div data-action="mouseenter->tooltip#show mouseleave->tooltip#hide"&gt;Info&lt;/div&gt;

&lt;!-- Événement personnalisé (dispatché par vous) --&gt;
&lt;div data-action="refresh->list#update"&gt;&lt;/div&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Événement global : clic sur document</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;div data-controller="dropdown" data-action="click@window->dropdown#close"&gt;
    ...
&lt;/div&gt;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Targets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les targets (<code>data-...-target</code>)</h2>
                <p class="textExemple">
                    Les targets permettent d'accéder directement à des éléments importants d'un contrôleur,
                    sans faire de <code>querySelector</code> manuel.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Déclaration dans le contrôleur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">static targets = ['input', 'output', 'submitButton'];</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Utilisation dans le HTML</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;div data-controller="form"&gt;
    &lt;input data-form-target="input" type="text"&gt;
    &lt;div data-form-target="output"&gt;&lt;/div&gt;
    &lt;button data-form-target="submitButton" data-action="click->form#validate"&gt;Envoyer&lt;/button&gt;
&lt;/div&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Propriétés automatiquement disponibles</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Dans la méthode du contrôleur
this.inputTarget        // l'élément input (unique)
this.inputTargets       // tableau des éléments (si plusieurs)
this.hasInputTarget     // booléen (existe-t-il ?)

this.submitButtonTarget
this.hasSubmitButtonTarget</code></pre>
                    </div>
                </div>
            </section>

            <!-- Values -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les values (paramètres configurables)</h2>
                <p class="textExemple">
                    Les values permettent de passer des données statiques ou dynamiques depuis le HTML vers le contrôleur.
                </p>

                <div class="textExemple">
                    <h3 class="text-purple">Déclaration dans le contrôleur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">static values = {
    apiUrl: String,      // chaîne
    autoRefresh: Boolean,// booléen
    interval: Number,    // nombre
    config: Object,      // objet (JSON)
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Passage des valeurs dans Twig</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;div data-controller="poll"
     data-poll-api-url-value="/api/notifications"
     data-poll-auto-refresh-value="true"
     data-poll-interval-value="5000"&gt;
    ...
&lt;/div&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Accès et modification dans le contrôleur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">connect() {
    console.log(this.apiUrlValue);    // "/api/notifications"
    console.log(this.autoRefreshValue); // true
    console.log(this.intervalValue);    // 5000

    // Modifier une value (déclenche une réaction si `valueChanged` est définie)
    this.intervalValue = 10000;
}

// Observateur de changement
intervalValueChanged(value, previousValue) {
    console.log(`Intervalle modifié de ${previousValue} à ${value}`);
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Classes CSS -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Les classes CSS dynamiques</h2>
                <p class="textExemple">
                    Stimulus permet de gérer des classes CSS de manière déclarative, par exemple pour afficher/masquer ou animer.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-javascript">// assets/controllers/toggle_controller.js
export default class extends Controller {
    static classes = ['hidden'];

    toggle() {
        this.element.classList.toggle(this.hiddenClass);
    }
}</code></pre>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-twig">&lt;div data-controller="toggle"
     data-toggle-hidden-class="d-none"&gt;
    &lt;p&gt;Ce texte peut être masqué&lt;/p&gt;
    &lt;button data-action="click->toggle#toggle"&gt;Afficher/masquer&lt;/button&gt;
&lt;/div&gt;</code></pre>
                </div>
            </section>

            <!-- Outlets (communication entre contrôleurs) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Outlets : communication entre contrôleurs</h2>
                <p class="textExemple">
                    Les outlets permettent à un contrôleur parent de trouver et d'interagir avec des contrôleurs enfants.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-javascript">// parent_controller.js
export default class extends Controller {
    static outlets = ['child'];

    callChild() {
        this.childOutlets.forEach(child => child.doSomething());
    }
}</code></pre>
                </div>
                <div class="code-example">
                    <pre v-pre><code class="language-twig">&lt;div data-controller="parent"&gt;
    &lt;div data-controller="child" data-parent-target="child.outlet"&gt;...&lt;/div&gt;
    &lt;div data-controller="child" data-parent-target="child.outlet"&gt;...&lt;/div&gt;
&lt;/div&gt;</code></pre>
                </div>
            </section>

            <!-- Intégration avec Symfony -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Intégration native avec Symfony</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Le bundle StimulusBundle</h3>
                    <p>Il fournit :</p>
                    <ul>
                        <li>Un fichier <code>assets/bootstrap.js</code> qui charge automatiquement tous les contrôleurs.</li>
                        <li>Un fichier <code>assets/controllers.json</code> qui liste les packages Stimulus externes (ex: <code>@symfony/stimulus-bridge</code>).</li>
                        <li>L'intégration avec Symfony UX (ex: <code>ux-autocomplete</code>, <code>ux-dropzone</code>).</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Installer un package UX (exemple : Autocomplete)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require symfony/ux-autocomplete
php bin/console importmap:require @symfony/ux-autocomplete</code></pre>
                    </div>
                    <p>Puis dans Twig :</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{{ form_row(form.categories, { attr: {'data-controller': 'autocomplete'} }) }}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Exemples concrets -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples pratiques</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple 1 : Confirmation avant suppression</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// confirm_controller.js
export default class extends Controller {
    static values = { message: String };

    confirm(event) {
        if (!confirm(this.messageValue || 'Êtes-vous sûr ?')) {
            event.preventDefault();
        }
    }
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;form method="post" action="{{ path('delete') }}" data-controller="confirm" data-confirm-message-value="Supprimer définitivement ?"&gt;
    &lt;button data-action="click->confirm#confirm"&gt;Supprimer&lt;/button&gt;
&lt;/form&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple 2 : Recherche en direct avec fetch</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// search_controller.js
export default class extends Controller {
    static targets = ['input', 'results'];
    static values = { url: String };

    async search() {
        const query = this.inputTarget.value;
        const response = await fetch(`${this.urlValue}?q=${encodeURIComponent(query)}`);
        const html = await response.text();
        this.resultsTarget.innerHTML = html;
    }
}</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">&lt;div data-controller="search" data-search-url-value="{{ path('api_search') }}"&gt;
    &lt;input type="text" data-search-target="input" data-action="input->search#search"&gt;
    &lt;div data-search-target="results"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Exemple 3 : Tabs (onglets) avec classes CSS</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// tabs_controller.js
export default class extends Controller {
    static targets = ['tab', 'panel'];
    static classes = ['active'];

    select(event) {
        const index = this.tabTargets.indexOf(event.currentTarget);
        this.tabTargets.forEach((tab, i) => {
            tab.classList.toggle(this.activeClass, i === index);
            this.panelTargets[i].classList.toggle(this.activeClass, i === index);
        });
    }
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul>
                    <li><strong>Un contrôleur = une responsabilité</strong> (ne pas tout mettre dans un seul).</li>
                    <li><strong>Nommer les contrôleurs avec des noms significatifs</strong> : <code>search_controller.js</code>, <code>modal_controller.js</code>.</li>
                    <li><strong>Préférer les <code>targets</code> aux <code>querySelector</code> manuels</strong> pour la maintenabilité.</li>
                    <li><strong>Utiliser les <code>values</code> plutôt que des variables d'instance</strong> pour les données configurables.</li>
                    <li><strong>Désactiver JavaScript ?</strong> Votre application doit rester fonctionnelle (amélioration progressive).</li>
                    <li><strong>Ne pas surcharger Stimulus</strong> : pour des interfaces très complexes, privilégiez un framework plus lourd (React, Vue).</li>
                    <li><strong>Utiliser les bundles Symfony UX</strong> : ils fournissent des contrôleurs Stimulus prêts à l'emploi.</li>
                </ul>
            </section>

            <!-- Exercices -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Compteur avec limite</h3>
                    <p>Créez un contrôleur <code>counter_limit</code> qui :</p>
                    <ul>
                        <li>Affiche une valeur initiale passée via une <code>value</code> (par défaut 0).</li>
                        <li>Possède une limite maximale (value <code>max</code>).</li>
                        <li>Les boutons + et - ne doivent pas dépasser cette limite (ni descendre en dessous de 0).</li>
                        <li>Lorsque la limite est atteinte, le bouton + est désactivé (target sur les boutons).</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-javascript">// counter_limit_controller.js
import { Controller } from '@hotwired/stimulus';

export default class extends Controller {
    static targets = ['value', 'incrementButton', 'decrementButton'];
    static values = { count: Number, max: Number };

    connect() {
        this.updateButtons();
    }

    increment() {
        if (this.countValue < this.maxValue) {
            this.countValue++;
            this.valueTarget.textContent = this.countValue;
            this.updateButtons();
        }
    }

    decrement() {
        if (this.countValue > 0) {
            this.countValue--;
            this.valueTarget.textContent = this.countValue;
            this.updateButtons();
        }
    }

    updateButtons() {
        this.incrementButtonTarget.disabled = (this.countValue >= this.maxValue);
        this.decrementButtonTarget.disabled = (this.countValue <= 0);
    }
}</code></pre>
                            <pre v-pre><code class="language-twig">&lt;div data-controller="counter-limit"
     data-counter-limit-count-value="0"
     data-counter-limit-max-value="10"&gt;
    &lt;button data-counter-limit-target="decrementButton"
            data-action="click->counter-limit#decrement"&gt;-&lt;/button&gt;
    &lt;span data-counter-limit-target="value"&gt;0&lt;/span&gt;
    &lt;button data-counter-limit-target="incrementButton"
            data-action="click->counter-limit#increment"&gt;+&lt;/button&gt;
&lt;/div&gt;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Formulaire avec chargement (spinner)</h3>
                    <p>Créez un contrôleur <code>form_with_spinner</code> qui :</p>
                    <ul>
                        <li>Intercepte la soumission d'un formulaire.</li>
                        <li>Affiche un spinner (caché au départ) et désactive le bouton d'envoi.</li>
                        <li>Laisse le formulaire se soumettre normalement après (pas de fetch).</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-javascript">// form_with_spinner_controller.js
export default class extends Controller {
    static targets = ['submitButton', 'spinner'];

    submit(event) {
        this.submitButtonTarget.disabled = true;
        this.spinnerTarget.classList.remove('d-none');
        // Le formulaire continue sa soumission normale
    }
}</code></pre>
                            <pre v-pre><code class="language-twig">&lt;form data-controller="form-with-spinner"
      data-action="submit->form-with-spinner#submit"&gt;
    &lt;!-- champs du formulaire --&gt;
    &lt;button type="submit" data-form-with-spinner-target="submitButton"&gt;
        Envoyer
    &lt;/button&gt;
    &lt;div data-form-with-spinner-target="spinner" class="spinner-border d-none"&gt;&lt;/div&gt;
&lt;/form&gt;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 3 : Dark mode avec valeurs booléennes</h3>
                    <p>Créez un contrôleur <code>dark_mode</code> qui :</p>
                    <ul>
                        <li>Lit une value <code>enabled</code> (booléenne) pour activer/désactiver le mode sombre.</li>
                        <li>Ajoute/retire une classe <code>dark-theme</code> sur l'élément <code>&lt;html&gt;</code>.</li>
                        <li>Sauvegarde la préférence dans <code>localStorage</code>.</li>
                        <li>Au chargement, restore la préférence depuis le localStorage.</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-javascript">// dark_mode_controller.js
export default class extends Controller {
    static values = { enabled: Boolean };

    connect() {
        const saved = localStorage.getItem('darkMode');
        if (saved !== null) this.enabledValue = JSON.parse(saved);
        this.apply();
    }

    toggle() {
        this.enabledValue = !this.enabledValue;
        localStorage.setItem('darkMode', this.enabledValue);
        this.apply();
    }

    apply() {
        document.documentElement.classList.toggle('dark-theme', this.enabledValue);
    }
}</code></pre>
                            <pre v-pre><code class="language-twig">&lt;button data-controller="dark-mode"
        data-dark-mode-enabled-value="false"
        data-action="click->dark-mode#toggle"&gt;
    🌓 Basculer le thème
&lt;/button&gt;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Stimulus est un outil idéal pour ajouter de l'interactivité à vos applications Symfony sans complexité inutile.
                    Sa philosophie "HTML-first" s'aligne parfaitement avec Twig et le rendu serveur.
                </p>
                <p class="textExemple">
                    Avec le bundle StimulusBundle et les packages Symfony UX, vous pouvez construire des interfaces modernes
                    (autocomplete, carrousel, dropzone, etc.) tout en gardant un code JavaScript simple, modulaire et testable.
                </p>
                <p class="textExemple">
                    Pour aller plus loin : découvrez <strong>Turbo</strong> (le compagnon de Stimulus) qui permet de créer des
                    applications monopages (SPA) sans écrire de JavaScript, grâce à des échanges HTML sur les liens et formulaires.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'StimulusLesson',

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
                    const languages = ['javascript', 'html', 'twig', 'bash', 'php'];
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
/* === Mêmes styles que les leçons précédentes === */
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
.lesson-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}
.lesson-table th, .lesson-table td {
    border: 1px solid #ddd;
    padding: 10px 12px;
    text-align: left;
    vertical-align: top;
}
.lesson-table th {
    background: #6A3093;
    color: white;
    font-weight: 600;
}
.lesson-table tr:nth-child(even) {
    background-color: #f9f9f9;
}
.warning-section {
    background: #fff3f3;
    border: 2px solid #ff6b6b;
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
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
    .lesson-table th, .lesson-table td { padding: 6px 8px; }
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