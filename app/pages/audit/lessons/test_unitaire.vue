<template>
    <div class="lesson-container">
        <div class="lesson-content">
            <!-- En-tête de la leçon -->
            <header class="lesson-header">
                <h1 class="text-white">Tests Unitaires dans un Audit</h1>
                <p class="lesson-meta text-white">
                    Maîtrisez l'importance et la mise en œuvre des tests unitaires dans le cadre d'un audit de code
                </p>
            </header>

            <!-- Introduction -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Introduction</h2>
                <p class="textExemple">
                    Les tests unitaires sont une composante essentielle du développement logiciel moderne.
                    Dans le contexte d'un audit, ils jouent un rôle crucial pour évaluer la qualité,
                    la maintenabilité et la fiabilité du code.
                </p>
                <p class="textExemple">
                    Cette leçon vous présentera l'importance des tests unitaires dans un audit,
                    les bonnes pratiques à suivre et des exemples concrets d'implémentation.
                </p>
            </section>

            <!-- Objectifs de la leçon -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Objectifs d'Apprentissage</h2>
                <ul class="textExemple">
                    <li>Comprendre le rôle des tests unitaires dans un audit</li>
                    <li>Apprendre à évaluer la qualité des tests unitaires existants</li>
                    <li>Maîtriser les indicateurs clés de couverture de code</li>
                    <li>Identifier les patterns de tests efficaces</li>
                    <li>Implémenter des tests unitaires robustes</li>
                </ul>
            </section>

            <!-- Importance des tests unitaires -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Pourquoi les Tests Unitaires sont Cruciaux dans un Audit</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Indicateur de Qualité du Code</h3>
                    <p>
                        La présence et la qualité des tests unitaires sont des indicateurs directs
                        de la maturité des pratiques de développement.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Détection Précoce des Défauts</h3>
                    <p>
                        Les tests unitaires permettent d'identifier rapidement les régressions
                        et les bugs introduits par de nouvelles modifications.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Documentation Vivante</h3>
                    <p>
                        Un bon test unitaire sert de documentation sur le comportement attendu
                        du code, facilitant la compréhension pour les nouveaux développeurs.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">4. Facilité de Refactoring</h3>
                    <p>
                        Avec une bonne couverture de tests, le refactoring devient moins risqué
                        et plus efficace.
                    </p>
                </div>
            </section>

            <!-- Métriques d'audit -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Métriques Clés à Examiner lors d'un Audit</h2>

                <div class="code-comparison">
                    <div class="code-example">
                        <h3 class="text-purple">Couverture de Code</h3>
                        <pre><code class="javascript">// Exemple de rapport de couverture
{
  "statements": 85,
  "branches": 75,
  "functions": 90,
  "lines": 85
}</code></pre>
                        <p class="textExemple">
                            Une couverture de 80% est généralement considérée comme bonne,
                            mais la qualité des tests est plus importante que le pourcentage.
                        </p>
                    </div>

                    <div class="code-example">
                        <h3 class="text-purple">Taux de Succès</h3>
                        <pre><code class="javascript">// Résultats des tests
Tests: 152 passed, 0 failed, 3 skipped
Time: 2.4s</code></pre>
                        <p class="textExemple">
                            Un taux de succès de 100% est idéal, mais les tests skip peuvent
                            être acceptables dans certains contextes.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Exemples de tests -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exemples de Tests Unitaires</h2>

                <div class="code-comparison">
                    <div class="code-example">
                        <h3 class="text-purple">Fonction à Tester</h3>
                        <pre><code class="javascript">// utils/calculations.js
<span class="keyword">export function</span> <span class="function">calculateTax</span>(<span class="variable">amount</span>, <span class="variable">taxRate</span> = <span class="number">0.2</span>) {
  <span class="keyword">if</span> (<span class="variable">amount</span> < <span class="number">0</span>) {
    <span class="keyword">throw new</span> <span class="class-name">Error</span>(<span class="string">'Le montant ne peut pas être négatif'</span>);
  }
  
  <span class="keyword">if</span> (<span class="variable">taxRate</span> < <span class="number">0</span> <span class="operator">||</span> <span class="variable">taxRate</span> > <span class="number">1</span>) {
    <span class="keyword">throw new</span> <span class="class-name">Error</span>(<span class="string">'Le taux de taxe doit être entre 0 et 1'</span>);
  }
  
  <span class="keyword">return</span> <span class="variable">amount</span> <span class="operator">*</span> <span class="variable">taxRate</span>;
}</code></pre>
                    </div>

                    <div class="code-example">
                        <h3 class="text-purple">Tests Unitaires Correspondants</h3>
                        <pre><code class="javascript">// tests/calculations.spec.js
<span class="keyword">import</span> { <span class="variable">calculateTax</span> } <span class="keyword">from</span> <span class="string">'@/utils/calculations'</span>;

<span class="function">describe</span>(<span class="string">'calculateTax'</span>, () => {
  <span class="function">test</span>(<span class="string">'calcule correctement la taxe avec le taux par défaut'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">calculateTax</span>(<span class="number">100</span>);
    <span class="function">expect</span>(<span class="variable">result</span>).<span class="function">toBe</span>(<span class="number">20</span>);
  });

  <span class="function">test</span>(<span class="string">'calcule correctement la taxe avec un taux personnalisé'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">calculateTax</span>(<span class="number">100</span>, <span class="number">0.1</span>);
    <span class="function">expect</span>(<span class="variable">result</span>).<span class="function">toBe</span>(<span class="number">10</span>);
  });

  <span class="function">test</span>(<span class="string">'lance une erreur pour un montant négatif'</span>, () => {
    <span class="function">expect</span>(() => <span class="function">calculateTax</span>(<span class="operator">-</span><span class="number">50</span>)).<span class="function">toThrow</span>(
      <span class="string">'Le montant ne peut pas être négatif'</span>
    );
  });

  <span class="function">test</span>(<span class="string">'lance une erreur pour un taux de taxe invalide'</span>, () => {
    <span class="function">expect</span>(() => <span class="function">calculateTax</span>(<span class="number">100</span>, <span class="number">1.5</span>)).<span class="function">toThrow</span>(
      <span class="string">'Le taux de taxe doit être entre 0 et 1'</span>
    );
  });
});</code></pre>
                    </div>
                </div>
            </section>

            <!-- Bonnes pratiques -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Bonnes Pratiques pour les Tests Unitaires</h2>

                <div class="textExemple">
                    <h3 class="text-purple">1. Tests Isolés et Indépendants</h3>
                    <p>
                        Chaque test doit être indépendant et ne pas dépendre de l'état
                        laissé par d'autres tests.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">2. Nommage Descriptif</h3>
                    <p>
                        Utilisez des noms de tests qui décrivent clairement ce qu'ils testent
                        et le comportement attendu.
                    </p>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">3. Structure AAA (Arrange-Act-Assert)</h3>
                    <pre><code class="javascript"><span class="function">test</span>(<span class="string">'doit ajouter deux nombres correctement'</span>, () => {
  <span class="comment">// Arrange: Préparer les données</span>
  <span class="keyword">const</span> <span class="variable">a</span> = <span class="number">5</span>;
  <span class="keyword">const</span> <span class="variable">b</span> = <span class="number">3</span>;
  
  <span class="comment">// Act: Exécuter l'action</span>
  <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">add</span>(<span class="variable">a</span>, <span class="variable">b</span>);
  
  <span class="comment">// Assert: Vérifier le résultat</span>
  <span class="function">expect</span>(<span class="variable">result</span>).<span class="function">toBe</span>(<span class="number">8</span>);
});</code></pre>
                </div>

                <div class="textExemple">
                    <h3 class="text-purple">4. Tests des Cas Limites</h3>
                    <p>
                        Pensez toujours à tester les cas limites, les valeurs nulles,
                        et les scénarios d'erreur.
                    </p>
                </div>
            </section>

            <!-- Exercice pratique -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Exercice Pratique</h2>

                <div class="exercise">
                    <h3 class="text-purple">Énoncé</h3>
                    <p class="textExemple">
                        Vous devez créer des tests unitaires pour la fonction suivante qui valide
                        une adresse email. Implémentez des tests couvrant tous les cas possibles.
                    </p>

                    <pre><code class="javascript"><span class="keyword">export function</span> <span class="function">validateEmail</span>(<span class="variable">email</span>) {
  <span class="keyword">if</span> (<span class="operator">!</span><span class="variable">email</span>) {
    <span class="keyword">return</span> { <span class="variable">isValid</span>: <span class="keyword">false</span>, <span class="variable">error</span>: <span class="string">'Email requis'</span> };
  }
  
  <span class="keyword">const</span> <span class="variable">emailRegex</span> = <span class="regex">/^[^\s@]+@[^\s@]+\.[^\s@]+$/</span>;
  <span class="keyword">if</span> (<span class="operator">!</span><span class="variable">emailRegex</span>.<span class="function">test</span>(<span class="variable">email</span>)) {
    <span class="keyword">return</span> { <span class="variable">isValid</span>: <span class="keyword">false</span>, <span class="variable">error</span>: <span class="string">'Format d\'email invalide'</span> };
  }
  
  <span class="keyword">return</span> { <span class="variable">isValid</span>: <span class="keyword">true</span>, <span class="variable">error</span>: <span class="keyword">null</span> };
}</code></pre>
                </div>

                <details class="solution">
                    <summary class="btn-purple btn-hover">Voir la Solution</summary>
                    <div class="solution-content">
                        <h4 class="text-purple">Solution Recommandée</h4>
                        <pre><code class="javascript"><span class="keyword">import</span> { <span class="variable">validateEmail</span> } <span class="keyword">from</span> <span class="string">'@/utils/validation'</span>;

<span class="function">describe</span>(<span class="string">'validateEmail'</span>, () => {
  <span class="function">test</span>(<span class="string">'retourne vrai pour un email valide'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">validateEmail</span>(<span class="string">'test@example.com'</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">isValid</span>).<span class="function">toBe</span>(<span class="keyword">true</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">error</span>).<span class="function">toBeNull</span>();
  });

  <span class="function">test</span>(<span class="string">'retourne une erreur pour un email vide'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">validateEmail</span>(<span class="string">''</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">isValid</span>).<span class="function">toBe</span>(<span class="keyword">false</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">error</span>).<span class="function">toBe</span>(<span class="string">'Email requis'</span>);
  });

  <span class="function">test</span>(<span class="string">'retourne une erreur pour un email sans @'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">validateEmail</span>(<span class="string">'invalid-email'</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">isValid</span>).<span class="function">toBe</span>(<span class="keyword">false</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">error</span>).<span class="function">toBe</span>(<span class="string">'Format d\'email invalide'</span>);
  });

  <span class="function">test</span>(<span class="string">'retourne une erreur pour un email sans domaine'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">validateEmail</span>(<span class="string">'test@'</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">isValid</span>).<span class="function">toBe</span>(<span class="keyword">false</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">error</span>).<span class="function">toBe</span>(<span class="string">'Format d\'email invalide'</span>);
  });

  <span class="function">test</span>(<span class="string">'retourne une erreur pour un email avec espaces'</span>, () => {
    <span class="keyword">const</span> <span class="variable">result</span> = <span class="function">validateEmail</span>(<span class="string">'test @example.com'</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">isValid</span>).<span class="function">toBe</span>(<span class="keyword">false</span>);
    <span class="function">expect</span>(<span class="variable">result</span>.<span class="variable">error</span>).<span class="function">toBe</span>(<span class="string">'Format d\'email invalide'</span>);
  });
});</code></pre>
                    </div>
                </details>
            </section>

            <!-- Checklist d'audit -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Checklist d'Audit des Tests Unitaires</h2>

                <div class="textExemple">
                    <ul>
                        <li>✅ Couverture de code supérieure à 80%</li>
                        <li>✅ Tests exécutés automatiquement dans la CI/CD</li>
                        <li>✅ Tests rapides et indépendants</li>
                        <li>✅ Présence de tests pour les cas d'erreur</li>
                        <li>✅ Nommage clair et descriptif des tests</li>
                        <li>✅ Absence de code de test dupliqué</li>
                        <li>✅ Mocking approprié des dépendances externes</li>
                        <li>✅ Tests maintenus à jour avec le code</li>
                    </ul>
                </div>
            </section>

            <!-- Conclusion -->
            <section class="lesson-section bg-light-purple border-purple">
                <h2 class="text-purple">Conclusion</h2>
                <p class="textExemple">
                    Les tests unitaires sont bien plus qu'une simple vérification technique.
                    Dans le cadre d'un audit, ils représentent un indicateur précieux de la
                    qualité globale du code et des pratiques de développement.
                </p>
                <p class="textExemple">
                    Un projet avec des tests unitaires bien conçus et maintenus démontre
                    une approche professionnelle du développement et une préoccupation
                    pour la qualité à long terme.
                </p>
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
    /* Permet le retour à la ligne */
    word-wrap: break-word;
    /* Casse les mots longs */
    word-break: break-word;
    /* Assure la césure des mots */
}

/* CONTENEUR PRINCIPAL POUR TOUS LES BLOCS DE CODE */
pre code {
    display: block;
    white-space: pre-wrap;
    /* Retour à la ligne automatique */
    overflow-x: auto;
    max-width: 100%;
    width: 100%;
    word-wrap: break-word;
    word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe JavaScript */
.keyword {
    color: #c586c0 !important;
}

/* Mots-clés (for, while, if, function, etc.) */
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

/* Opérateurs (+, -, =, =>, etc.) */
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
</style>