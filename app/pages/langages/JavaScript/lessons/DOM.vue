<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Manipuler le DOM en JavaScript</h1>
                <p class="lesson-meta text-white">JavaScript • DOM • API • Événements</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce que le DOM ?</h2>
                <p class="textExemple">
                    Le <strong>DOM (Document Object Model)</strong> est une interface de programmation pour les documents HTML et XML.
                    Il représente la page web sous forme d'une arborescence d'objets que JavaScript peut manipuler dynamiquement.
                </p>
                <p class="textExemple">
                    Grâce au DOM, vous pouvez ajouter, modifier ou supprimer des éléments HTML, changer les styles,
                    réagir aux événements (clics, saisies, etc.) et interagir avec l'utilisateur en temps réel.
                </p>
                <div class="code-example">
                    <pre v-pre><code class="language-plaintext">Document
   │
   └── html
        ├── head
        │    └── title
        └── body
             ├── h1
             ├── p
             └── div
                  └── a</code></pre>
                </div>
            </section>

            <!-- Accéder aux éléments -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Accéder aux éléments du DOM</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Les sélecteurs classiques</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Par ID (élément unique)
const header = document.getElementById('main-header');

// Par classe (collection d'éléments)
const items = document.getElementsByClassName('item');

// Par balise
const paragraphes = document.getElementsByTagName('p');

// Selecteur CSS moderne (premier élément)
const firstButton = document.querySelector('.btn-primary');

// Tous les éléments correspondant au sélecteur
const allButtons = document.querySelectorAll('.btn');</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Naviguer dans l'arborescence</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const element = document.getElementById('menu');

// Parent
const parent = element.parentNode;

// Enfants
const enfants = element.children;
const premierEnfant = element.firstElementChild;
const dernierEnfant = element.lastElementChild;

// Frères et sœurs
const precedent = element.previousElementSibling;
const suivant = element.nextElementSibling;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Modifier le contenu et les attributs -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Modifier le contenu et les attributs</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Texte et HTML</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const titre = document.querySelector('h1');

// Texte brut (safe)
titre.textContent = 'Nouveau titre';

// HTML interprété (attention XSS)
titre.innerHTML = '&lt;span class="highlight"&gt;Nouveau&lt;/span&gt; titre';

// Texte sans mise en forme
const texte = titre.innerText;</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Attributs et classes</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const lien = document.querySelector('a');

// Lire / écrire un attribut
const href = lien.getAttribute('href');
lien.setAttribute('target', '_blank');

// Version simplifiée pour les attributs standards
lien.href = 'https://example.com';
lien.id = 'monLien';

// Gestion des classes CSS
lien.classList.add('btn', 'btn-primary');
lien.classList.remove('btn');
lien.classList.toggle('active');
lien.classList.contains('btn'); // true/false</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Styles CSS inline</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const box = document.querySelector('.box');
box.style.backgroundColor = 'blue';
box.style.padding = '1rem';
box.style.borderRadius = '8px';

// Lire un style calculé (final)
const bgColor = getComputedStyle(box).backgroundColor;</code></pre>
                    </div>
                </div>
            </section>

            <!-- Créer, ajouter, supprimer des éléments -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Créer et supprimer des éléments</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Créer un élément</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Créer un nouvel élément
const newDiv = document.createElement('div');
newDiv.textContent = 'Je suis un nouveau bloc';
newDiv.classList.add('alert', 'alert-success');

// Créer un texte seul
const textNode = document.createTextNode('Hello world');</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ajouter dans le DOM</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const parent = document.querySelector('.container');

// À la fin
parent.appendChild(newDiv);

// Au début
parent.prepend(newDiv);

// Avant un élément existant
const reference = document.querySelector('#target');
parent.insertBefore(newDiv, reference);

// Après un élément (méthode moderne)
reference.after(newDiv);

// Remplacer un élément
parent.replaceChild(newDiv, oldElement);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Supprimer un élément</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const element = document.querySelector('#toRemove');

// Méthode moderne
element.remove();

// Ancienne méthode (via le parent)
element.parentNode.removeChild(element);</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Cloner un élément</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const original = document.querySelector('.card');
const clone = original.cloneNode(true); // true = copie profonde (enfants inclus)
parent.appendChild(clone);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Gestion des événements -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Gestion des événements</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Ajouter un écouteur d'événement</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const button = document.querySelector('#myButton');

// Méthode recommandée
button.addEventListener('click', function(event) {
    console.log('Clic détecté !');
    console.log('Élément cible :', event.target);
});

// Fonction fléchée
button.addEventListener('click', (e) => {
    e.preventDefault(); // Empêche le comportement par défaut
    alert('Bouton cliqué');
});</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les événements les plus courants</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Souris
element.addEventListener('click', handler);
element.addEventListener('dblclick', handler);
element.addEventListener('mouseenter', handler);
element.addEventListener('mouseleave', handler);

// Clavier
document.addEventListener('keydown', (e) => {
    console.log(`Touche pressée : ${e.key}`);
    if (e.key === 'Enter') { /* action */ }
});

// Formulaire
input.addEventListener('input', (e) => console.log(e.target.value));
form.addEventListener('submit', (e) => {
    e.preventDefault();
    // Traitement du formulaire
});

// Chargement de la page
window.addEventListener('DOMContentLoaded', () => {
    console.log('DOM entièrement chargé');
});</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Supprimer un écouteur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">function handleClick() { console.log('clic'); }
button.addEventListener('click', handleClick);
// Plus tard
button.removeEventListener('click', handleClick);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Délégation d'événements -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Délégation d'événements</h2>

                <div class="textExemple">
                    <p>
                        La <strong>délégation d'événements</strong> consiste à attacher un écouteur à un élément parent
                        pour capturer les événements de ses enfants, même ceux créés dynamiquement.
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">// Au lieu d'ajouter un écouteur sur chaque bouton
document.querySelector('.btn-list').addEventListener('click', (event) => {
    // Vérifier que la cible est bien un bouton
    if (event.target.matches('.delete-btn')) {
        const id = event.target.dataset.id;
        console.log(`Supprimer l'élément ${id}`);
    }
});

// Avec des éléments créés dynamiquement
function addNewButton() {
    const newBtn = document.createElement('button');
    newBtn.textContent = 'Nouveau';
    newBtn.classList.add('delete-btn');
    newBtn.dataset.id = Date.now();
    document.querySelector('.btn-list').appendChild(newBtn);
    // Pas besoin d'ajouter un écouteur supplémentaire !
}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Attributs data-* -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Attributs data-* pour stocker des données</h2>

                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-html">&lt;!-- HTML --&gt;
&lt;button data-id="123" data-role="admin" data-active="true"&gt;Mon bouton&lt;/button&gt;</code></pre>
                    </div>
                    <div class="code-example">
                        <pre v-pre><code class="language-javascript">const btn = document.querySelector('button');

// Accès via dataset
console.log(btn.dataset.id);     // "123"
console.log(btn.dataset.role);   // "admin"
console.log(btn.dataset.active); // "true"

// Modification
btn.dataset.active = 'false';
btn.dataset.newAttr = 'valeur';</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques avec le DOM</h2>

                <div class="textExemple">
                    <ul>
                        <li><strong>Attendre que le DOM soit prêt</strong> : utilisez <code>DOMContentLoaded</code> ou placez vos scripts en fin de body.</li>
                        <li><strong>Limiter les accès au DOM</strong> : mettez en cache les références d'éléments (les requêtes sont coûteuses).</li>
                        <li><strong>Préférer <code>textContent</code> à <code>innerHTML</code></strong> pour du texte simple (évite les failles XSS).</li>
                        <li><strong>Utiliser la délégation d'événements</strong> pour les éléments dynamiques.</li>
                        <li><strong>Ne pas abuser des styles inline</strong> : préférez les classes CSS.</li>
                        <li><strong>Détacher les écouteurs avant de supprimer des éléments</strong> pour éviter les fuites mémoire.</li>
                    </ul>
                </div>
            </section>

            <!-- Exercices pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercices pratiques</h2>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 1 : Liste de tâches dynamique</h3>
                    <p>Créez une page avec :</p>
                    <ul>
                        <li>Un champ texte et un bouton "Ajouter"</li>
                        <li>Une liste UL vide</li>
                        <li>Chaque nouvelle tâche s'ajoute à la liste</li>
                        <li>Chaque tâche possède un bouton "Supprimer" à côté</li>
                        <li>Les suppressions fonctionnent même pour les tâches ajoutées dynamiquement</li>
                    </ul>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-html">&lt;input type="text" id="taskInput" placeholder="Nouvelle tâche"&gt;
&lt;button id="addBtn"&gt;Ajouter&lt;/button&gt;
&lt;ul id="taskList"&gt;&lt;/ul&gt;

&lt;script&gt;
    const input = document.getElementById('taskInput');
    const addBtn = document.getElementById('addBtn');
    const list = document.getElementById('taskList');

    function addTask(text) {
        const li = document.createElement('li');
        li.textContent = text;
        const delBtn = document.createElement('button');
        delBtn.textContent = 'Supprimer';
        delBtn.classList.add('delete-btn');
        li.appendChild(delBtn);
        list.appendChild(li);
    }

    addBtn.addEventListener('click', () => {
        if (input.value.trim()) {
            addTask(input.value.trim());
            input.value = '';
        }
    });

    list.addEventListener('click', (e) => {
        if (e.target.classList.contains('delete-btn')) {
            e.target.parentElement.remove();
        }
    });
&lt;/script&gt;</code></pre>
                        </div>
                    </details>
                </div>

                <div class="exercise">
                    <h3 class="text-purple">Exercice 2 : Mode sombre</h3>
                    <p>Ajoutez un bouton qui bascule entre le thème clair et sombre en modifiant la classe d'un élément <code>body</code>.</p>
                    <details class="solution">
                        <summary class="btn-purple btn-hover">Voir la solution</summary>
                        <div class="solution-content">
                            <pre v-pre><code class="language-html">&lt;button id="themeToggle"&gt;🌙 Mode sombre&lt;/button&gt;

&lt;style&gt;
    body.dark {
        background-color: #1e1e1e;
        color: #eee;
    }
&lt;/style&gt;

&lt;script&gt;
    const toggle = document.getElementById('themeToggle');
    toggle.addEventListener('click', () => {
        document.body.classList.toggle('dark');
        toggle.textContent = document.body.classList.contains('dark') ? '☀️ Mode clair' : '🌙 Mode sombre';
    });
&lt;/script&gt;</code></pre>
                        </div>
                    </details>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>

                <div class="textExemple">
                    <p>
                        Le DOM est le cœur de l'interactivité en JavaScript. En maîtrisant sa manipulation,
                        vous pouvez créer des interfaces riches, réactives et dynamiques.
                    </p>
                    <p>
                        Les notions clés à retenir : sélection d'éléments, modification de contenu/attributs,
                        création/suppression d'éléments, gestion d'événements et délégation.
                    </p>
                    <p>
                        Prochaines étapes : explorer les <strong>Web Components</strong>, le <strong>Shadow DOM</strong>,
                        ou vous initier à des frameworks comme Vue.js ou React qui abstraient la manipulation directe du DOM.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'DomLesson',

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
                    const jsScript = document.createElement('script');
                    jsScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/javascript.min.js';
                    jsScript.onload = () => {
                        const htmlScript = document.createElement('script');
                        htmlScript.src = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/xml.min.js';
                        htmlScript.onload = resolve;
                        document.head.appendChild(htmlScript);
                    };
                    document.head.appendChild(jsScript);
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