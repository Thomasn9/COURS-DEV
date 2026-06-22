<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Styliser son Jeu de Cartes Symfony</h1>
                <p class="lesson-meta text-white">Étape 2 • CSS • Google Fonts • Asset Component • Form Styling</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    Dans la leçon précédente, on a mis en place l'écran de démarrage avec le formulaire
                    d'ajout de joueurs. Le résultat fonctionnait, mais l'interface utilisait le style par
                    défaut de Bootstrap sans aucune personnalisation.
                </p>
                <p class="textExemple">
                    Dans cette leçon, on va habiller le projet à notre image : fond noir, typographies
                    personnalisées via Google Fonts, et contrôle fin de l'apparence des champs de formulaire
                    Symfony. On va toucher à trois fichiers : <code>assets/styles/start.css</code> (les styles),
                    <code>templates/base.html.twig</code> (le chargement des ressources) et
                    <code>src/Form/PlayerType.php</code> (l'apparence du champ côté PHP).
                </p>
            </section>

            <!-- Étape 1 : le fichier CSS et l'Asset Component -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 1 : Créer et brancher le fichier CSS</h2>

                <div class="textExemple">
                    <p>
                        Symfony gère les fichiers statiques (CSS, images, JS) via le composant
                        <strong>Asset</strong>, qui fournit la fonction Twig <code>asset()</code>. Cette fonction
                        génère le chemin correct vers le fichier, en tenant compte de la configuration du projet
                        et d'un éventuel versionnage du cache.
                    </p>
                    <p class="textExemple">
                        Par convention, les feuilles de style se placent dans <code>assets/styles/</code>.
                        Créez le fichier CSS du projet :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">touch assets/styles/start.css</code></pre>
                    </div>
                    <p class="textExemple">
                        On branche ensuite ce fichier dans le template de base, dans le bloc
                        <code>stylesheets</code>. Ouvrez <code>templates/base.html.twig</code> et ajoutez
                        la ligne <code>&lt;link&gt;</code> en dessous du CDN Bootstrap :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{% block stylesheets %}

    {# Bootstrap 4 via CDN #}
    &lt;link rel="stylesheet"
        href="https://cdn.jsdelivr.net/npm/bootstrap@4.0.0/dist/css/bootstrap.min.css"
        integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
        crossorigin="anonymous"&gt;

    {# Feuille de style personnalisée via asset() #}
    &lt;link href="{{ asset('styles/start.css') }}" type="text/css" rel="stylesheet"&gt;

{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Pourquoi asset() et pas un chemin direct ?</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Écrire <code>href="/styles/start.css"</code> fonctionnerait, mais ce n'est pas la
                            bonne pratique. La fonction <code>asset()</code> préfixe automatiquement le chemin
                            avec la <strong>base URL</strong> du projet, ce qui est indispensable si l'application
                            est déployée dans un sous-dossier (ex: <code>monsite.com/jeu/</code> au lieu de
                            <code>monsite.com/</code>). Elle permet aussi d'ajouter un suffixe de version pour
                            forcer le rechargement du cache navigateur après une mise à jour.
                        </p>
                    </div>
                </div>

                <div class="textExemple">
                    <p>
                        Si le composant Asset n'est pas encore installé dans votre projet :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-bash">composer require symfony/asset</code></pre>
                    </div>
                </div>
            </section>

            <!-- Étape 2 : importer des polices Google Fonts -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 2 : Importer des polices Google Fonts</h2>

                <div class="textExemple">
                    <p>
                        Google Fonts met à disposition des polices web via une URL CDN. On les importe en
                        haut du fichier CSS avec la règle <code>@import</code>. L'URL s'obtient directement
                        sur <a href="https://fonts.google.com" target="_blank">fonts.google.com</a> en
                        sélectionnant une police puis en copiant le lien d'intégration CSS.
                    </p>
                    <p class="textExemple">
                        Dans ce projet, on utilise deux polices : <strong>Bitcount Prop Single</strong>
                        pour les titres principaux (une police variable avec des axes personnalisables) et
                        <strong>Bebas Neue</strong> pour les sous-titres (condensée, tout en majuscules).
                        Ouvrez <code>assets/styles/start.css</code> et ajoutez ces imports en tout premier :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-css">/* assets/styles/start.css */

/* Import des polices depuis Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Bitcount+Prop+Single:wght@100..900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Les paramètres de l'URL Google Fonts</h3>
                    <p>
                        L'URL de Google Fonts n'est pas arbitraire, chaque paramètre a un rôle précis :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">https://fonts.googleapis.com/css2
    ?family=Bitcount+Prop+Single   → nom de la famille (espaces remplacés par +)
    :wght@100..900                 → plage de graisses disponibles (100 à 900)
    &display=swap                  → stratégie de chargement (voir ci-dessous)</code></pre>
                    </div>
                    <p class="textExemple">
                        Le paramètre <code>display=swap</code> indique au navigateur d'afficher d'abord
                        une police de substitution (système) pendant le chargement de la police Google, puis
                        de la remplacer dès qu'elle est disponible. C'est la valeur recommandée pour les
                        performances : l'utilisateur voit du texte lisible immédiatement plutôt qu'un espace
                        vide.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Polices variables (@wght@100..900)</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            <strong>Bitcount Prop Single</strong> est une <em>police variable</em> (variable font).
                            Au lieu de charger plusieurs fichiers séparés (Regular, Bold, Light...), un seul
                            fichier contient toute la plage de graisses. La syntaxe <code>wght@100..900</code>
                            demande à Google Fonts de renvoyer ce fichier unique. Cela réduit le nombre de
                            requêtes HTTP. Pour <strong>Bebas Neue</strong>, qui n'existe qu'en une seule
                            graisse, il n'y a pas besoin de préciser de plage.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Étape 3 : styles globaux -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 3 : Styles globaux et typographie</h2>

                <div class="textExemple">
                    <p>
                        Sous les imports de polices, on définit les styles globaux de la page et on applique
                        les nouvelles polices aux titres. Complétez <code>assets/styles/start.css</code> :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-css">/* Fond et couleur globale */
body {
    background-color: black;
    color: white;
}

/* Titre principal H1 : police variable Bitcount */
h1 {
    color: blueviolet;
    font-family: "Bitcount Prop Single", system-ui;
    font-optical-sizing: auto;
    font-weight: 400;
    font-style: normal;

    /* Axes de la police variable :
       slnt  = inclinaison (0 = droit)
       CRSV  = style cursif (0 à 1)
       ELSH  = ombre portée
       ELXP  = expansion horizontale */
    font-variation-settings:
        "slnt" 0,
        "CRSV" 0.5,
        "ELSH" 0,
        "ELXP" 0;
}

/* Sous-titres H2 : Bebas Neue condensée */
h2 {
    font-family: "Bebas Neue", sans-serif;
    font-weight: 300;
    font-style: normal;
    font-size: 2rem;
}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">font-variation-settings : les axes d'une police variable</h3>
                    <p>
                        La propriété <code>font-variation-settings</code> permet de contrôler les axes
                        spécifiques d'une police variable. Ces axes sont définis par le concepteur de la police
                        et varient d'une famille à l'autre. Pour <strong>Bitcount Prop Single</strong>,
                        quatre axes sont disponibles :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">slnt  → inclinaison du texte (0 = droit, valeurs négatives = penchée à gauche)
CRSV  → activation du style cursif (0 = off, 1 = on, 0.5 = intermédiaire)
ELSH  → intensité de l'ombre portée sur les lettres
ELXP  → expansion ou compression horizontale des glyphes</code></pre>
                    </div>
                    <p class="textExemple">
                        Les axes en majuscules (<code>CRSV</code>, <code>ELSH</code>, <code>ELXP</code>)
                        sont des axes "custom" définis par le fondeur. Les axes en minuscules
                        (<code>slnt</code>, <code>wght</code>) sont des axes standardisés définis par
                        la spécification OpenType.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">La pile de polices de substitution</h3>
                    <p>
                        On écrit toujours <code>font-family: "Bebas Neue", sans-serif</code> et jamais
                        <code>font-family: "Bebas Neue"</code> seul. Le deuxième terme est la
                        <strong>police de secours</strong> : si Google Fonts est inaccessible (hors ligne,
                        bloqueur de pub, délai de chargement), le navigateur affiche une police générique
                        <code>sans-serif</code> du système plutôt que la police par défaut du navigateur.
                        Pour <code>Bitcount Prop Single</code>, on utilise <code>system-ui</code>, qui
                        correspond à la police d'interface native du système d'exploitation.
                    </p>
                </div>
            </section>

            <!-- Étape 4 : styliser les champs de formulaire Symfony -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 4 : Personnaliser l'apparence d'un champ de formulaire</h2>

                <div class="textExemple">
                    <p>
                        Par défaut, Symfony génère un champ texte avec son label et son input. Pour
                        personnaliser leur apparence, on peut agir à deux endroits : dans
                        <code>PlayerType.php</code> (côté PHP) pour modifier les attributs HTML générés,
                        et dans le template Twig pour changer le rendu de chaque partie du champ séparément.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Supprimer le label avec <code>label => false</code></h3>
                    <p>
                        Symfony génère automatiquement un <code>&lt;label&gt;</code> pour chaque champ.
                        Dans notre cas, le placeholder dans l'input suffit à guider l'utilisateur : le label
                        est redondant. Pour le supprimer, on passe <code>'label' => false</code> dans les
                        options du champ dans <code>PlayerType.php</code> :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">// src/Form/PlayerType.php
$builder
    ->add('name', TextType::class, [
        'label' => false,   // Supprime le label généré automatiquement
        'attr' => [
            'placeholder' => 'Entrez un nom',
            'autofocus'   => true,
            'class'       => 'form-control',
        ],
    ]);</code></pre>
                    </div>
                    <p class="textExemple">
                        La clé <code>'label'</code> dans les options accepte trois types de valeur :
                        une chaîne de caractères (texte du label), <code>false</code> (pas de label du tout),
                        ou <code>null</code> (label automatique généré à partir du nom du champ, comportement
                        par défaut).
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ajouter des classes CSS avec <code>attr</code></h3>
                    <p>
                        La clé <code>'attr'</code> permet de passer n'importe quel attribut HTML à l'élément
                        <code>&lt;input&gt;</code> généré. C'est ici qu'on ajoute la classe Bootstrap
                        <code>form-control</code> qui donne au champ son apparence standard :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-php">'attr' => [
    'placeholder' => 'Entrez un nom',  // attribut HTML placeholder
    'autofocus'   => true,             // attribut HTML autofocus (focus automatique)
    'class'       => 'form-control',   // classe CSS Bootstrap
]</code></pre>
                    </div>
                    <p class="textExemple">
                        Chaque clé du tableau <code>attr</code> correspond exactement à un attribut HTML.
                        Symfony les transmet tels quels lors du rendu. On peut y mettre n'importe quel
                        attribut valide : <code>id</code>, <code>data-*</code>, <code>maxlength</code>,
                        <code>disabled</code>, etc.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ce que Symfony génère avant et après</h3>
                    <div class="code-comparison">
                        <div>
                            <h5>Avant (configuration par défaut)</h5>
                            <div class="code-example">
                                <pre v-pre><code class="language-html">&lt;label for="player_name"&gt;
    Nom du joueur
&lt;/label&gt;
&lt;input type="text"
    id="player_name"
    name="player[name]"
    placeholder="Entrez un nom"
    autofocus&gt;</code></pre>
                            </div>
                        </div>
                        <div>
                            <h5>Après (label false + attr class)</h5>
                            <div class="code-example">
                                <pre v-pre><code class="language-html">&lt;input type="text"
    id="player_name"
    name="player[name]"
    placeholder="Entrez un nom"
    autofocus
    class="form-control"&gt;</code></pre>
                            </div>
                        </div>
                    </div>
                    <p class="textExemple">
                        Le <code>&lt;label&gt;</code> a disparu et la classe <code>form-control</code>
                        est bien présente sur l'input.
                    </p>
                </div>
            </section>

            <!-- Étape 5 : simplifier le template Twig -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Étape 5 : Adapter le template Twig</h2>

                <div class="textExemple">
                    <p>
                        Maintenant que le fond est noir et que Bootstrap apporte ses propres styles, on
                        simplifie le Twig en retirant les classes Bootstrap de structure (conteneurs, grilles)
                        pour laisser la place à un balisage plus neutre, que l'on stilisera nous-mêmes au fur
                        et à mesure. Voici le template mis à jour :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# templates/start/index.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
&lt;div&gt;
    &lt;h1&gt;Nom du jeu&lt;/h1&gt;
    &lt;h2&gt;Ajoutez au moins {{ minPlayers }} joueurs pour commencer.&lt;/h2&gt;

    {# Formulaire d'ajout #}
    {{ form_start(form) }}
    &lt;div&gt;
        &lt;div&gt;{{ form_row(form.name) }}&lt;/div&gt;
        &lt;div&gt;
            &lt;button type="submit" class="btn btn-outline-success"&gt;Ajouter joueur&lt;/button&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    {{ form_end(form) }}

    {# Liste des joueurs #}
    &lt;h2&gt;Joueurs enregistrés ({{ playerCount }})&lt;/h2&gt;
    &lt;ul&gt;
        {% for player in players %}
        &lt;li&gt;
            {{ player.name }}
            &lt;a href="{{ path('game_player_remove', { name: player.name }) }}"
                onclick="return confirm('Supprimer {{ player.name }} ?')"&gt;
                Supprimer
            &lt;/a&gt;
        &lt;/li&gt;
        {% else %}
        &lt;li&gt;Aucun joueur enregistré pour l'instant.&lt;/li&gt;
        {% endfor %}
    &lt;/ul&gt;

    {# Actions #}
    &lt;div&gt;
        {% if canStart %}
        &lt;a href="{{ path('game_play') }}"&gt;Début de la partie !&lt;/a&gt;
        {% else %}
        &lt;button disabled&gt;
            Ajoutez {{ minPlayers - playerCount }} joueur(s) supplémentaire(s) pour commencer
        &lt;/button&gt;
        {% endif %}

        {% if players|length > 0 %}
        &lt;a href="{{ path('game_clear') }}"
            onclick="return confirm('Vider toute la liste ?')"&gt;
            Supprimer toute la liste
        &lt;/a&gt;
        {% endif %}
    &lt;/div&gt;
&lt;/div&gt;
{% endblock %}</code></pre>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">form_row vs form_label / form_widget séparés</h3>
                    <p>
                        <code>form_row(form.name)</code> est un raccourci qui rend en une seule fois le label,
                        l'input et les messages d'erreur. Puisqu'on a désactivé le label côté PHP
                        (<code>'label' => false</code>), <code>form_row</code> rendra uniquement l'input.
                        Si vous aviez besoin d'un contrôle encore plus fin sur la structure HTML (envelopper
                        le label et l'input dans des divs spécifiques), vous pouvez les séparer dans le Twig :
                    </p>
                    <div class="code-example">
                        <pre v-pre><code class="language-twig">{# Rendu séparé : label, input et erreurs individuellement #}
{{ form_label(form.name) }}
{{ form_widget(form.name) }}
{{ form_errors(form.name) }}</code></pre>
                    </div>
                </div>
            </section>

            <!-- Récapitulatif des fichiers modifiés -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Récapitulatif des fichiers modifiés</h2>
                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-plaintext">assets/styles/start.css
    → Créé : imports Google Fonts, fond noir, styles h1 et h2

templates/base.html.twig
    → Modifié : ajout de &lt;link href="{{ asset('styles/start.css') }}"&gt;
      dans le bloc stylesheets

src/Form/PlayerType.php
    → Modifié : 'label' => false pour supprimer le label
                'class' => 'form-control' dans attr pour styliser l'input

templates/start/index.html.twig
    → Modifié : suppression des classes Bootstrap de structure,
      balisage simplifié pour laisser le CSS custom prendre le relais</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques et conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques et Conclusion</h2>

                <div class="textExemple">
                    <h3 class="text-purple">Ce qu'on a appliqué dans cette leçon</h3>
                    <ul>
                        <li><strong>asset()</strong> : toujours utiliser la fonction Twig plutôt qu'un chemin absolu codé en dur</li>
                        <li><strong>@import en tête de fichier</strong> : les imports Google Fonts doivent être les toutes premières règles du fichier CSS, avant n'importe quelle autre déclaration</li>
                        <li><strong>display=swap</strong> : paramètre à toujours inclure dans l'URL Google Fonts pour éviter le texte invisible pendant le chargement</li>
                        <li><strong>Pile de substitution</strong> : toujours indiquer une police de secours générique après la police principale</li>
                        <li><strong>label => false</strong> : supprimer le label Symfony quand le placeholder suffit à guider l'utilisateur</li>
                        <li><strong>attr => class</strong> : ajouter des classes CSS directement dans le FormType pour garder la logique de présentation cohérente avec la définition du champ</li>
                    </ul>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Ordre de priorité des styles</h3>
                    <div class="warning-section" style="background:#f3f0ff;border-color:#c9b8ff;">
                        <p>
                            Notez que <code>start.css</code> est chargé <strong>après</strong> Bootstrap dans
                            le <code>base.html.twig</code>. C'est intentionnel : les règles CSS s'appliquent
                            dans l'ordre de chargement, et les règles les plus récentes l'emportent sur les
                            précédentes (à spécificité égale). En plaçant notre fichier en dernier, nos styles
                            personnalisés écrasent naturellement les valeurs par défaut de Bootstrap sans avoir
                            à utiliser <code>!important</code>.
                        </p>
                    </div>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">Conclusion</h3>
                    <p>
                        Le projet a maintenant une identité visuelle de base : fond noir, typographies
                        personnalisées et formulaire stylisé. La structure CSS est propre et extensible :
                        on pourra ajouter de nouvelles règles dans <code>start.css</code> (ou créer d'autres
                        fichiers CSS par page) sans jamais toucher à Bootstrap.
                    </p>
                </div>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'SymfonyStyleLesson',

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
                        twigScript.onload = resolve;
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