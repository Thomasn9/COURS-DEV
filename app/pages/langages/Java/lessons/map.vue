<template>
    <div class="lesson-container">
        <div class="lesson-content">

            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Les Map en Java</h1>
                <p class="lesson-meta text-white">Java • Map • HashMap • TreeMap • LinkedHashMap • Collections</p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Qu'est-ce qu'une Map ?</h2>
                <p class="textExemple">
                    Une <code>Map</code> est une structure de données qui permet d'associer une <strong>clé</strong> à une <strong>valeur</strong>.
                    Chaque clé est unique et permet de retrouver rapidement la valeur correspondante.
                </p>
                <p class="textExemple">
                    Contrairement aux listes (List) ou aux ensembles (Set), les Map stockent des paires (clé, valeur). Les clés ne peuvent pas être dupliquées,
                    mais les valeurs peuvent l'être. Java fournit plusieurs implémentations de l'interface <code>Map</code>, adaptées à différents besoins.
                </p>
            </section>

            <!-- Hiérarchie des interfaces -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Hiérarchie et implémentations</h2>
                <div class="textExemple">
                    <p>L'interface principale est <code>java.util.Map&lt;K, V&gt;</code>. Ses principales implémentations sont :</p>
                    <ul>
                        <li><strong>HashMap</strong> : basée sur une table de hachage. Insertion, suppression et recherche en O(1) en moyenne. Ordre non garanti.</li>
                        <li><strong>LinkedHashMap</strong> : extension de HashMap qui maintient l'ordre d'insertion (ou l'ordre d'accès).</li>
                        <li><strong>TreeMap</strong> : basée sur un arbre rouge-noir. Les clés sont triées (ordre naturel ou via un Comparator). Opérations en O(log n).</li>
                        <li><strong>Hashtable</strong> : ancienne classe synchronisée (déconseillée, préférer ConcurrentHashMap).</li>
                        <li><strong>ConcurrentHashMap</strong> : version thread-safe pour environnements concurrents.</li>
                    </ul>
                    <p>Il existe aussi des implémentations spécialisées comme <code>EnumMap</code>, <code>WeakHashMap</code>, <code>IdentityHashMap</code>.</p>
                </div>
            </section>

            <!-- Création et opérations de base -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Opérations de base sur une Map</h2>
                <div class="textExemple">
                    <h3 class="text-purple">Création</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// HashMap
Map&lt;String, Integer&gt; map = new HashMap&lt;&gt;();

// Avec capacité initiale et facteur de charge
Map&lt;String, String&gt; map2 = new HashMap&lt;&gt;(16, 0.75f);

// TreeMap (ordre naturel des clés)
Map&lt;Integer, String&gt; treeMap = new TreeMap&lt;&gt;();

// LinkedHashMap (ordre d'insertion)
Map&lt;String, Double&gt; linkedMap = new LinkedHashMap&lt;&gt;();</code></pre>
                    </div>

                    <h3 class="text-purple">Ajouter / modifier une paire</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">Map&lt;String, Integer&gt; ages = new HashMap&lt;&gt;();
ages.put("Alice", 25);      // ajoute
ages.put("Bob", 30);
ages.put("Alice", 26);      // remplace la valeur pour la clé "Alice"</code></pre>
                    </div>

                    <h3 class="text-purple">Récupérer une valeur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">Integer ageAlice = ages.get("Alice");   // retourne 26
Integer ageCharlie = ages.get("Charlie"); // retourne null (clé absente)</code></pre>
                    </div>

                    <h3 class="text-purple">Vérifier la présence d'une clé ou d'une valeur</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">if (ages.containsKey("Bob")) {
    System.out.println("Bob est présent");
}
if (ages.containsValue(30)) {
    System.out.println("Quelqu'un a 30 ans");
}</code></pre>
                    </div>

                    <h3 class="text-purple">Supprimer une entrée</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">Integer valeurRetiree = ages.remove("Alice"); // retourne 26
boolean supprime = ages.remove("Bob", 30);   // suppression conditionnelle (Java 8)</code></pre>
                    </div>

                    <h3 class="text-purple">Obtenir la taille et vider</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">int taille = ages.size();      // nombre de paires
boolean vide = ages.isEmpty();
ages.clear();                   // vide la map</code></pre>
                    </div>
                </div>
            </section>

            <!-- Parcours d'une Map -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Parcourir une Map</h2>
                <div class="textExemple">
                    <p>Il existe plusieurs façons de parcourir une Map.</p>

                    <h3 class="text-purple">Parcourir les clés (keySet)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">Map&lt;String, Integer&gt; ages = new HashMap&lt;&gt;();
ages.put("Alice", 25);
ages.put("Bob", 30);

for (String nom : ages.keySet()) {
    System.out.println(nom + " a " + ages.get(nom) + " ans");
}</code></pre>
                    </div>

                    <h3 class="text-purple">Parcourir les valeurs (values)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (Integer age : ages.values()) {
    System.out.println(age);
}</code></pre>
                    </div>

                    <h3 class="text-purple">Parcourir les entrées (entrySet) – recommandé</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">for (Map.Entry&lt;String, Integer&gt; entry : ages.entrySet()) {
    String nom = entry.getKey();
    int age = entry.getValue();
    System.out.println(nom + " : " + age);
}</code></pre>
                    </div>

                    <h3 class="text-purple">Parcourir avec forEach (Java 8+)</h3>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">ages.forEach((nom, age) -> System.out.println(nom + " -> " + age));</code></pre>
                    </div>
                </div>
            </section>

            <!-- HashMap en détail -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">HashMap – l'implémentation la plus courante</h2>
                <div class="textExemple">
                    <p><code>HashMap</code> stocke les paires dans des "buckets" en fonction du code de hachage de la clé.
                    Il offre des performances O(1) en moyenne pour <code>put()</code>, <code>get()</code> et <code>remove()</code>.</p>
                    <ul>
                        <li><strong>Clés et valeurs peuvent être null</strong> : une seule clé null autorisée, plusieurs valeurs null possibles.</li>
                        <li><strong>Ordre non garanti</strong> : l'ordre peut changer au fil du temps (redimensionnement).</li>
                        <li><strong>Capacité initiale et facteur de charge</strong> : la capacité par défaut est 16, le facteur de charge 0.75f.</li>
                        <li><strong>Non synchronisée</strong> : pour un usage concurrent, utilisez <code>Collections.synchronizedMap()</code> ou <code>ConcurrentHashMap</code>.</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">HashMap&lt;Integer, String&gt; map = new HashMap&lt;&gt;();
map.put(1, "un");
map.put(2, "deux");
map.put(null, "null key");
System.out.println(map.get(null));  // "null key"</code></pre>
                    </div>
                </div>
            </section>

            <!-- LinkedHashMap -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">LinkedHashMap – avec ordre prévisible</h2>
                <div class="textExemple">
                    <p><code>LinkedHashMap</code> étend <code>HashMap</code> en ajoutant une liste doublement chaînée qui maintient l'ordre des entrées.</p>
                    <ul>
                        <li><strong>Ordre d'insertion</strong> (par défaut) : les entrées sont itérées dans l'ordre où elles ont été ajoutées.</li>
                        <li><strong>Ordre d'accès</strong> : si on utilise le constructeur <code>LinkedHashMap(capacité, facteur, true)</code>, les entrées sont ordonnées du moins récemment accédé au plus récemment accédé (utile pour les caches LRU).</li>
                    </ul>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">Map&lt;String, Integer&gt; map = new LinkedHashMap&lt;&gt;();
map.put("A", 1);
map.put("B", 2);
map.put("C", 3);
// Itération : A, B, C

// Cache LRU avec ordre d'accès
LinkedHashMap&lt;String, String&gt; cache = new LinkedHashMap&lt;&gt;(16, 0.75f, true);
cache.get("A"); // déplace A à la fin</code></pre>
                    </div>
                </div>
            </section>

            <!-- TreeMap -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">TreeMap – clés triées</h2>
                <div class="textExemple">
                    <p><code>TreeMap</code> stocke les clés dans un arbre binaire de recherche équilibré (arbre rouge-noir). Les clés sont triées :</p>
                    <ul>
                        <li>Selon l'ordre naturel (<code>Comparable</code>) si les clés l'implémentent.</li>
                        <li>Ou selon un <code>Comparator</code> fourni au constructeur.</li>
                    </ul>
                    <p>Les opérations sont en O(log n). La clé ne peut pas être null (sauf si Comparator l'autorise).</p>
                    <div class="code-example">
                        <pre v-pre><code class="language-java">TreeMap&lt;Integer, String&gt; map = new TreeMap&lt;&gt;();
map.put(3, "trois");
map.put(1, "un");
map.put(2, "deux");
System.out.println(map); // {1=un, 2=deux, 3=trois} (ordre trié)

// Méthodes spécifiques
Integer firstKey = map.firstKey();   // 1
Integer lastKey = map.lastKey();     // 3
Map.Entry&lt;Integer, String&gt; lower = map.lowerEntry(2); // {1=un}
SortedMap&lt;Integer, String&gt; sub = map.subMap(1, 3);   // clés 1 à 2</code></pre>
                    </div>
                </div>
            </section>

            <!-- Méthodes utiles (Java 8+) -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Méthodes pratiques de l'API Map (Java 8+)</h2>
                <div class="textExemple">
                    <div class="code-example">
                        <pre v-pre><code class="language-java">// getOrDefault : valeur par défaut si clé absente
int age = map.getOrDefault("Charlie", 18);

// putIfAbsent : ajoute seulement si la clé n'existe pas
map.putIfAbsent("Alice", 25);

// replace : modification conditionnelle
map.replace("Bob", 31);
map.replace("Bob", 30, 31); // seulement si valeur actuelle = 30

// compute, computeIfAbsent, computeIfPresent
map.computeIfAbsent("David", k -> k.length()); // associe "David" -> 5

// merge : fusionne deux valeurs pour une même clé
map.merge("Alice", 1, (oldVal, newVal) -> oldVal + newVal);</code></pre>
                    </div>
                </div>
            </section>

            <!-- Comparaison des implémentations -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Quand utiliser quelle Map ?</h2>
                <div class="textExemple">
                    <ul>
                        <li><strong>HashMap</strong> : usage général, pas d'ordre requis, meilleures performances.</li>
                        <li><strong>LinkedHashMap</strong> : besoin de l'ordre d'insertion ou d'accès (cache).</li>
                        <li><strong>TreeMap</strong> : besoin de clés triées, de recherches par intervalle.</li>
                        <li><strong>ConcurrentHashMap</strong> : accès concurrents multiples (thread-safe).</li>
                        <li><strong>EnumMap</strong> : clés d'un type enum, très efficace en mémoire/vitesse.</li>
                        <li><strong>WeakHashMap</strong> : clés avec références faibles (utile pour caches sans fuite mémoire).</li>
                    </ul>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes pratiques</h2>
                <ul class="textExemple">
                    <li><strong>Override equals() et hashCode()</strong> si vous utilisez des clés personnalisées (obligatoire pour HashMap).</li>
                    <li><strong>Choisir le type d'interface le plus général</strong> : déclarez toujours <code>Map&lt;K,V&gt; map = new HashMap&lt;&gt;();</code> plutôt que <code>HashMap</code> directement.</li>
                    <li><strong>Capacité initiale</strong> : estimez la taille pour éviter les redimensionnements coûteux.</li>
                    <li><strong>Préférer <code>entrySet()</code> pour l'itération</strong> (pas besoin de refaire un <code>get</code>).</li>
                    <li><strong>Utiliser les méthodes <code>computeIfAbsent()</code></strong> pour initialiser des valeurs à la volée.</li>
                    <li><strong>Attention aux clés null</strong> : toutes les Maps ne les acceptent pas (TreeMap non).</li>
                </ul>
            </section>

            <!-- Erreurs fréquentes -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Erreurs courantes</h2>
                <ul class="textExemple">
                    <li><strong>Modifier une Map pendant une itération</strong> (sauf via l'Iterator).</li>
                    <li><strong>Utiliser un objet mutable comme clé</strong> et le modifier après insertion (rend la clé introuvable).</li>
                    <li><strong>Oublier d'override hashCode() quand on override equals()</strong> (rend HashMap incohérent).</li>
                    <li><strong>Supposer un ordre dans une HashMap</strong> (l'ordre peut changer).</li>
                </ul>
            </section>

            <!-- Exemple complet -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemple concret : compteur de mots</h2>
                <div class="code-example">
                    <pre v-pre><code class="language-java">import java.util.*;

public class CompteurMots {
    public static void main(String[] args) {
        String texte = "le chat le chien le chat oiseau";
        String[] mots = texte.split(" ");

        Map&lt;String, Integer&gt; occurrences = new HashMap&lt;&gt;();
        for (String mot : mots) {
            occurrences.put(mot, occurrences.getOrDefault(mot, 0) + 1);
        }

        // Affichage
        occurrences.forEach((mot, nb) -> System.out.println(mot + " : " + nb));
        // Résultat : le : 3, chat : 2, chien : 1, oiseau : 1
    }
}</code></pre>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Les Map sont des structures de données essentielles pour associer des clés à des valeurs.
                    Le choix de l'implémentation dépend des besoins : performances, ordre, tri, concurrence.
                </p>
                <p class="textExemple">
                    Maîtriser les Map permet d'écrire du code plus clair, plus efficace et de résoudre de nombreux problèmes
                    courants comme le comptage, la mise en cache, l'indexation, etc.
                </p>
            </section>

        </div>
    </div>
</template>

<script>
export default {
    name: 'JavaMapLesson',

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
                    const languages = ['java'];
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