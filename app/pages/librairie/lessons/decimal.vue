<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Decimal.js - Calculs précis en JavaScript</h1>
        <p class="lesson-meta text-white">Gérez les nombres décimaux avec précision dans vos applications JavaScript</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction</h2>
        <p class="textExemple">
          En JavaScript, les nombres sont représentés selon la norme IEEE 754 en virgule flottante 64 bits (double précision).
          Cette représentation peut entraîner des erreurs de précision avec les nombres décimaux. La bibliothèque Decimal.js
          résout ce problème en fournissant un type Decimal pour les calculs arithmétiques décimaux arbitrairement précis.
        </p>
        
        <div class="code-example">
          <h3 class="text-purple">Problème avec les nombres en JavaScript natif</h3>
          <pre><code>// Problème de précision en JavaScript standard
<span class="keyword">const</span> <span class="variable">a</span> = <span class="number">0.1</span>;
<span class="keyword">const</span> <span class="variable">b</span> = <span class="number">0.2</span>;
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">a</span> + <span class="variable">b</span>); <span class="comment">// Résultat: 0.30000000000000004 (au lieu de 0.3)</span>

<span class="keyword">const</span> <span class="variable">c</span> = <span class="number">0.3</span> - <span class="number">0.1</span>;
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">c</span>); <span class="comment">// Résultat: 0.19999999999999998 (au lieu de 0.2)</span></code></pre>
        </div>
      </section>

      <!-- Installation et configuration -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Installation et Configuration</h2>
        
        <h3 class="text-purple">Installation avec npm</h3>
        <div class="code-example">
          <pre><code><span class="comment"># Dans votre terminal, à la racine de votre projet</span>
<span class="variable">npm</span> <span class="function">install</span> decimal.js</code></pre>
        </div>

        <h3 class="text-purple">Importation dans votre projet</h3>
        <div class="code-comparison">
          <div>
            <h4 class="text-purple">ES6 Modules</h4>
            <pre><code><span class="keyword">import</span> <span class="variable">Decimal</span> <span class="keyword">from</span> <span class="string">'decimal.js'</span>;

<span class="comment">// Ou pour CommonJS</span>
<span class="keyword">const</span> <span class="variable">Decimal</span> = <span class="function">require</span>(<span class="string">'decimal.js'</span>);</code></pre>
          </div>
          <div>
            <h4 class="text-purple">Dans le navigateur</h4>
            <pre><code><span class="comment">&lt;!-- Via CDN --&gt;</span>
<span class="keyword">&lt;script</span> <span class="variable">src</span>=<span class="string">"https://cdnjs.cloudflare.com/ajax/libs/decimal.js/10.4.3/decimal.min.js"</span><span class="keyword">&gt;&lt;/script&gt;</span>

<span class="comment">&lt;script&gt;</span>
  <span class="comment">// Decimal est disponible globalement</span>
  <span class="keyword">const</span> <span class="variable">a</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">0.1</span>);
<span class="comment">&lt;/script&gt;</span></code></pre>
          </div>
        </div>
      </section>

      <!-- Utilisation de base -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Utilisation de Base</h2>
        
        <h3 class="text-purple">Création d'objets Decimal</h3>
        <div class="code-example">
          <pre><code><span class="keyword">import</span> <span class="variable">Decimal</span> <span class="keyword">from</span> <span class="string">'decimal.js'</span>;

<span class="comment">// Différentes façons de créer un Decimal</span>
<span class="keyword">const</span> <span class="variable">a</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">0.1</span>);
<span class="keyword">const</span> <span class="variable">b</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="string">"0.2"</span>);
<span class="keyword">const</span> <span class="variable">c</span> = <span class="function">Decimal</span>(<span class="number">0.3</span>); <span class="comment">// Sans 'new' fonctionne aussi</span>
<span class="keyword">const</span> <span class="variable">d</span> = <span class="function">Decimal</span>.<span class="function">sum</span>(<span class="variable">a</span>, <span class="variable">b</span>); <span class="comment">// Méthode statique</span>

<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">d</span>.<span class="function">toString</span>()); <span class="comment">// "0.3" (précis!)</span></code></pre>
        </div>

        <h3 class="text-purple">Opérations arithmétiques</h3>
        <div class="code-example">
          <pre><code><span class="keyword">const</span> <span class="variable">x</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">10</span>);
<span class="keyword">const</span> <span class="variable">y</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">3</span>);

<span class="comment">// Addition</span>
<span class="keyword">const</span> <span class="variable">sum</span> = <span class="variable">x</span>.<span class="function">plus</span>(<span class="variable">y</span>); <span class="comment">// 13</span>

<span class="comment">// Soustraction</span>
<span class="keyword">const</span> <span class="variable">diff</span> = <span class="variable">x</span>.<span class="function">minus</span>(<span class="variable">y</span>); <span class="comment">// 7</span>

<span class="comment">// Multiplication</span>
<span class="keyword">const</span> <span class="variable">product</span> = <span class="variable">x</span>.<span class="function">times</span>(<span class="variable">y</span>); <span class="comment">// 30</span>

<span class="comment">// Division</span>
<span class="keyword">const</span> <span class="variable">quotient</span> = <span class="variable">x</span>.<span class="function">dividedBy</span>(<span class="variable">y</span>); <span class="comment">// 3.33333333333333333333</span>

<span class="comment">// Modulo</span>
<span class="keyword">const</span> <span class="variable">mod</span> = <span class="variable">x</span>.<span class="function">mod</span>(<span class="variable">y</span>); <span class="comment">// 1</span>

<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">quotient</span>.<span class="function">toString</span>());</code></pre>
        </div>
      </section>

      <!-- Fonctions avancées -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Fonctions Avancées</h2>
        
        <h3 class="text-purple">Comparaisons</h3>
        <div class="code-example">
          <pre><code><span class="keyword">const</span> <span class="variable">a</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">10</span>);
<span class="keyword">const</span> <span class="variable">b</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">5</span>);

<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">a</span>.<span class="function">greaterThan</span>(<span class="variable">b</span>)); <span class="comment">// true</span>
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">a</span>.<span class="function">lessThanOrEqualTo</span>(<span class="variable">b</span>)); <span class="comment">// false</span>
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">a</span>.<span class="function">equals</span>(<span class="variable">b</span>)); <span class="comment">// false</span>
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">a</span>.<span class="function">comparedTo</span>(<span class="variable">b</span>)); <span class="comment">// 1 (a > b)</span></code></pre>
        </div>

        <h3 class="text-purple">Fonctions mathématiques</h3>
        <div class="code-example">
          <pre><code><span class="keyword">const</span> <span class="variable">num</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="number">16</span>);

<span class="comment">// Racine carrée</span>
<span class="keyword">const</span> <span class="variable">sqrt</span> = <span class="variable">num</span>.<span class="function">squareRoot</span>(); <span class="comment">// 4</span>

<span class="comment">// Puissance</span>
<span class="keyword">const</span> <span class="variable">pow</span> = <span class="variable">num</span>.<span class="function">toPower</span>(<span class="number">2</span>); <span class="comment">// 256</span>

<span class="comment">// Valeur absolue</span>
<span class="keyword">const</span> <span class="variable">neg</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(-<span class="number">10</span>);
<span class="keyword">const</span> <span class="variable">abs</span> = <span class="variable">neg</span>.<span class="function">absoluteValue</span>(); <span class="comment">// 10</span>

<span class="comment">// Arrondi</span>
<span class="keyword">const</span> <span class="variable">pi</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="string">"3.1415926535"</span>);
<span class="keyword">const</span> <span class="variable">rounded</span> = <span class="variable">pi</span>.<span class="function">toDecimalPlaces</span>(<span class="number">2</span>); <span class="comment">// 3.14</span></code></pre>
        </div>
      </section>

      <!-- Configuration et précision -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Configuration et Précision</h2>
        
        <h3 class="text-purple">Configuration globale</h3>
        <div class="code-example">
          <pre><code><span class="comment">// Configuration de la précision (nombre de chiffres significatifs)</span>
<span class="function">Decimal</span>.<span class="function">set</span>({ <span class="variable">precision</span>: <span class="number">40</span> });

<span class="comment">// Configuration de l'arrondi</span>
<span class="function">Decimal</span>.<span class="function">set</span>({ 
  <span class="variable">rounding</span>: <span class="class-name">Decimal</span>.<span class="variable">ROUND_HALF_UP</span>,
  <span class="variable">toExpNeg</span>: -<span class="number">7</span>,
  <span class="variable">toExpPos</span>: <span class="number">21</span>
});

<span class="comment">// Modes d'arrondi disponibles:</span>
<span class="comment">// ROUND_UP, ROUND_DOWN, ROUND_CEIL, ROUND_FLOOR</span>
<span class="comment">// ROUND_HALF_UP, ROUND_HALF_DOWN, ROUND_HALF_EVEN</span></code></pre>
        </div>

        <h3 class="text-purple">Précision par opération</h3>
        <div class="code-example">
          <pre><code><span class="keyword">const</span> <span class="variable">a</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="string">"1.23456789"</span>);

<span class="comment">// Limiter la précision pour une opération spécifique</span>
<span class="keyword">const</span> <span class="variable">b</span> = <span class="variable">a</span>.<span class="function">toPrecision</span>(<span class="number">5</span>); <span class="comment">// "1.2346"</span>
<span class="keyword">const</span> <span class="variable">c</span> = <span class="variable">a</span>.<span class="function">toDecimalPlaces</span>(<span class="number">3</span>); <span class="comment">// "1.235"</span>
<span class="keyword">const</span> <span class="variable">d</span> = <span class="variable">a</span>.<span class="function">toSignificantDigits</span>(<span class="number">4</span>); <span class="comment">// "1.235"</span></code></pre>
        </div>
      </section>

      <!-- Cas d'usage pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Cas d'Usage Pratiques</h2>
        
        <h3 class="text-purple">Calculs financiers</h3>
        <div class="code-example">
          <pre><code><span class="keyword">class</span> <span class="class-name">FinancialCalculator</span> {
  <span class="function">calculateInterest</span>(<span class="variable">principal</span>, <span class="variable">rate</span>, <span class="variable">time</span>) {
    <span class="keyword">const</span> <span class="variable">p</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">principal</span>);
    <span class="keyword">const</span> <span class="variable">r</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">rate</span>).<span class="function">dividedBy</span>(<span class="number">100</span>);
    <span class="keyword">const</span> <span class="variable">t</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">time</span>);
    
    <span class="comment">// Intérêts composés: A = P(1 + r)^t</span>
    <span class="keyword">const</span> <span class="variable">amount</span> = <span class="variable">p</span>.<span class="function">times</span>(<span class="function">Decimal</span>.<span class="function">pow</span>(<span class="function">Decimal</span>.<span class="function">sum</span>(<span class="number">1</span>, <span class="variable">r</span>), <span class="variable">t</span>));
    
    <span class="keyword">return</span> <span class="variable">amount</span>.<span class="function">toDecimalPlaces</span>(<span class="number">2</span>).<span class="function">toNumber</span>();
  }
}

<span class="keyword">const</span> <span class="variable">calculator</span> = <span class="keyword">new</span> <span class="class-name">FinancialCalculator</span>();
<span class="keyword">const</span> <span class="variable">result</span> = <span class="variable">calculator</span>.<span class="function">calculateInterest</span>(<span class="number">1000</span>, <span class="number">5</span>, <span class="number">2</span>);
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">result</span>); <span class="comment">// 1102.50 (précis)</span></code></pre>
        </div>

        <h3 class="text-purple">Calculs scientifiques</h3>
        <div class="code-example">
          <pre><code><span class="keyword">function</span> <span class="function">calculateCircleArea</span>(<span class="variable">radius</span>) {
  <span class="keyword">const</span> <span class="variable">r</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">radius</span>);
  <span class="keyword">const</span> <span class="variable">pi</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="string">"3.141592653589793"</span>);
  
  <span class="comment">// A = πr²</span>
  <span class="keyword">return</span> <span class="variable">pi</span>.<span class="function">times</span>(<span class="variable">r</span>.<span class="function">toPower</span>(<span class="number">2</span>)).<span class="function">toDecimalPlaces</span>(<span class="number">5</span>);
}

<span class="keyword">const</span> <span class="variable">area</span> = <span class="function">calculateCircleArea</span>(<span class="number">2.5</span>);
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">area</span>.<span class="function">toString</span>()); <span class="comment">// "19.63495"</span></code></pre>
        </div>
      </section>

      <!-- Exercices pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercices Pratiques</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Exercice 1: Calcul de TVA</h3>
          <p class="textExemple">
            Créez une fonction qui calcule le prix TTC à partir d'un prix HT et d'un taux de TVA.
            Utilisez Decimal.js pour éviter les erreurs d'arrondi.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">function</span> <span class="function">calculateTTC</span>(<span class="variable">priceHT</span>, <span class="variable">tvaRate</span>) {
  <span class="keyword">const</span> <span class="variable">price</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">priceHT</span>);
  <span class="keyword">const</span> <span class="variable">tva</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">tvaRate</span>).<span class="function">dividedBy</span>(<span class="number">100</span>);
  
  <span class="keyword">const</span> <span class="variable">priceTTC</span> = <span class="variable">price</span>.<span class="function">times</span>(<span class="function">Decimal</span>.<span class="function">sum</span>(<span class="number">1</span>, <span class="variable">tva</span>));
  
  <span class="keyword">return</span> <span class="variable">priceTTC</span>.<span class="function">toDecimalPlaces</span>(<span class="number">2</span>).<span class="function">toNumber</span>();
}

<span class="comment">// Exemple d'utilisation</span>
<span class="keyword">const</span> <span class="variable">ttc</span> = <span class="function">calculateTTC</span>(<span class="number">19.99</span>, <span class="number">20</span>);
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">ttc</span>); <span class="comment">// 23.99 (précis)</span></code></pre>
            </div>
          </details>
        </div>

        <div class="exercise">
          <h3 class="text-purple">Exercice 2: Conversion de devises</h3>
          <p class="textExemple">
            Implémentez un convertisseur de devises qui utilise Decimal.js pour des conversions précises.
            La fonction doit prendre un montant, un taux de change et retourner le montant converti.
          </p>
          
          <details class="solution">
            <summary class="btn-purple btn-hover">Voir la solution</summary>
            <div class="solution-content">
              <pre><code><span class="keyword">class</span> <span class="class-name">CurrencyConverter</span> {
  <span class="function">convert</span>(<span class="variable">amount</span>, <span class="variable">exchangeRate</span>, <span class="variable">fromCurrency</span>, <span class="variable">toCurrency</span>) {
    <span class="keyword">const</span> <span class="variable">decimalAmount</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">amount</span>);
    <span class="keyword">const</span> <span class="variable">rate</span> = <span class="keyword">new</span> <span class="class-name">Decimal</span>(<span class="variable">exchangeRate</span>);
    
    <span class="keyword">const</span> <span class="variable">converted</span> = <span class="variable">decimalAmount</span>.<span class="function">times</span>(<span class="variable">rate</span>);
    
    <span class="keyword">return</span> {
      <span class="variable">amount</span>: <span class="variable">converted</span>.<span class="function">toDecimalPlaces</span>(<span class="number">2</span>).<span class="function">toNumber</span>(),
      <span class="variable">from</span>: <span class="variable">fromCurrency</span>,
      <span class="variable">to</span>: <span class="variable">toCurrency</span>,
      <span class="variable">rate</span>: <span class="variable">exchangeRate</span>
    };
  }
}

<span class="comment">// Exemple d'utilisation</span>
<span class="keyword">const</span> <span class="variable">converter</span> = <span class="keyword">new</span> <span class="class-name">CurrencyConverter</span>();
<span class="keyword">const</span> <span class="variable">result</span> = <span class="variable">converter</span>.<span class="function">convert</span>(<span class="number">100</span>, <span class="number">0.85</span>, <span class="string">'USD'</span>, <span class="string">'EUR'</span>);
<span class="variable">console</span>.<span class="function">log</span>(<span class="variable">result</span>); <span class="comment">// { amount: 85, from: 'USD', to: 'EUR', rate: 0.85 }</span></code></pre>
            </div>
          </details>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          Decimal.js est une bibliothèque essentielle pour tout développeur JavaScript travaillant avec des calculs financiers,
          scientifiques ou toute application nécessitant une précision décimale exacte. En évitant les problèmes d'arrondi
          inhérents aux nombres à virgule flottante JavaScript, elle garantit l'exactitude de vos calculs.
        </p>
        
        <h3 class="text-purple">Points clés à retenir:</h3>
        <ul class="textExemple">
          <li>Utilisez Decimal.js pour les calculs financiers et scientifiques</li>
          <li>Configurez la précision selon vos besoins</li>
          <li>Les objets Decimal sont immuables - chaque opération retourne un nouvel objet</li>
          <li>Convertissez en nombre natif uniquement en fin de calcul</li>
          <li>Testez toujours vos calculs avec des valeurs limites</li>
        </ul>
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
.keyword { color: #c586c0 !important; } /* Mots-clés (for, while, if, function, etc.) */
.variable { color: #9cdcfe !important; } /* Variables et noms de fonctions */
.string { color: #ce9178 !important; } /* Chaînes de caractères */
.comment { color: #6a9955 !important; } /* Commentaires */
.function { color: #dcdcaa !important; } /* Noms de fonctions */
.operator { color: #d4d4d4 !important; } /* Opérateurs (+, -, =, =>, etc.) */
.constant { color: #4fc1ff !important; } /* Constantes */
.number { color: #b5cea8 !important; } /* Nombres */
.class-name { color: #4ec9b0 !important; } /* Noms de classes */

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

.lesson-section:nth-child(1) { animation-delay: 0.1s; }
.lesson-section:nth-child(2) { animation-delay: 0.2s; }
.lesson-section:nth-child(3) { animation-delay: 0.3s; }
.lesson-section:nth-child(4) { animation-delay: 0.4s; }
.lesson-section:nth-child(5) { animation-delay: 0.5s; }
</style>