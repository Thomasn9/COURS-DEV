<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <div class="lesson-header">
        <h1 class="text-white" v-pre>Fetch des données depuis une API Symfony avec Nuxt</h1>
        <p class="lesson-meta text-white" v-pre>
          Apprenez à communiquer efficacement entre un frontend Nuxt et un backend Symfony
        </p>
      </div>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>Introduction</h2>
        <p class="textExemple" v-pre>
          Dans cette leçon, nous allons apprendre comment récupérer des données depuis une API Symfony dans une application Nuxt. 
          Cette compétence est essentielle pour créer des applications modernes où le frontend (Nuxt) et le backend (Symfony) sont découplés.
        </p>
        <p class="textExemple" v-pre>
          Nous aborderons plusieurs méthodes de fetch : <code>$fetch</code>, <code>useFetch</code> et <code>useAsyncData</code>, 
          ainsi que la gestion des erreurs, l'authentification et les bonnes pratiques.
        </p>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>1. Configuration de l'API Symfony</h2>
        <p class="textExemple" v-pre>
          Avant de pouvoir fetch des données depuis Nuxt, assurez-vous que votre API Symfony est correctement configurée pour accepter les requêtes CORS.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Configuration CORS dans Symfony</h4>
          <pre v-pre><code class="language-yaml">// config/packages/nelmio_cors.yaml
<span class="keyword">nelmio_cors</span>:
    <span class="variable">defaults</span>:
        <span class="property">origin_regex</span>: <span class="keyword">true</span>
        <span class="property">allow_origin</span>: [<span class="string">'%env(CORS_ALLOW_ORIGIN)%'</span>]
        <span class="property">allow_methods</span>: [<span class="string">'GET'</span>, <span class="string">'POST'</span>, <span class="string">'PUT'</span>, <span class="string">'PATCH'</span>, <span class="string">'DELETE'</span>, <span class="string">'OPTIONS'</span>]
        <span class="property">allow_headers</span>: [<span class="string">'Content-Type'</span>, <span class="string">'Authorization'</span>]
        <span class="property">expose_headers</span>: [<span class="string">'Link'</span>]
        <span class="property">max_age</span>: <span class="number">3600</span>
    <span class="variable">paths</span>:
        <span class="string">'^/api/'</span>:
            <span class="property">allow_origin</span>: [<span class="string">'http://localhost:3000'</span>, <span class="string">'http://127.0.0.1:3000'</span>]
            <span class="property">allow_headers</span>: [<span class="string">'*'</span>]
            <span class="property">allow_methods</span>: [<span class="string">'*'</span>]
            <span class="property">max_age</span>: <span class="number">3600</span></code></pre>
        </div>

        <p class="textExemple mt-3" v-pre>
          Dans votre <code>.env</code> Symfony, ajoutez :
        </p>
        
        <div class="code-example">
          <pre v-pre><code class="language-bash">CORS_ALLOW_ORIGIN=^https?://(localhost|127\.0\.0\.1)(:[0-9]+)?$</code></pre>
        </div>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>2. Configuration de Nuxt pour communiquer avec Symfony</h2>
        
        <p class="textExemple" v-pre>
          Dans votre projet Nuxt, vous devez configurer l'URL de base de votre API Symfony.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Configuration dans nuxt.config.ts</h4>
          <pre v-pre><code class="language-typescript"><span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineNuxtConfig</span>({
  <span class="property">runtimeConfig</span>: {
    <span class="property">public</span>: {
      <span class="property">apiBaseUrl</span>: process.<span class="property">env</span>.<span class="property">API_BASE_URL</span> || <span class="string">'http://localhost:8000/api'</span>
    }
  },
  
  <span class="comment">// Configuration pour les appels API côté serveur</span>
  <span class="property">nitro</span>: {
    <span class="property">routeRules</span>: {
      <span class="string">'/api/**'</span>: {
        <span class="property">proxy</span>: process.<span class="property">env</span>.<span class="property">API_BASE_URL</span> + <span class="string">'/**'</span>
      }
    }
  }
})</code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple" v-pre>Fichier .env de Nuxt</h4>
          <pre v-pre><code class="language-bash"><span class="comment"># .env</span>
API_BASE_URL=http://localhost:8000
NUXT_PUBLIC_API_BASE_URL=http://localhost:8000/api</code></pre>
        </div>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>3. Méthodes de Fetch dans Nuxt 4</h2>
        
        <p class="textExemple" v-pre>
          Nuxt 4 offre plusieurs méthodes pour fetch des données. Voici les principales :
        </p>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple" v-pre>useFetch (Recommandé)</h4>
            <pre v-pre><code class="language-typescript"><span class="comment">// Dans un composant ou page</span>
<span class="keyword">const</span> { <span class="property">data</span>, <span class="property">pending</span>, <span class="property">error</span>, <span class="property">refresh</span> } = <span class="keyword">await</span> <span class="function">useFetch</span>(<span class="string">'/products'</span>, {
  <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
  <span class="property">headers</span>: {
    <span class="string">'Accept'</span>: <span class="string">'application/json'</span>,
    <span class="string">'Content-Type'</span>: <span class="string">'application/json'</span>
  },
  <span class="function">onRequest</span>({ <span class="property">request</span>, <span class="property">options</span> }) {
    <span class="comment">// Ajouter un token d'authentification si nécessaire</span>
    options.<span class="property">headers</span> = {
      ...options.<span class="property">headers</span>,
      <span class="string">'Authorization'</span>: <span class="template-string">`Bearer ${token.value}`</span>
    }
  },
  <span class="function">onResponse</span>({ <span class="property">response</span> }) {
    <span class="comment">// Traiter la réponse</span>
    console.<span class="function">log</span>(<span class="string">'Données reçues:'</span>, response.<span class="property">_data</span>)
  },
  <span class="function">onResponseError</span>({ <span class="property">error</span> }) {
    <span class="comment">// Gérer les erreurs</span>
    console.<span class="function">error</span>(<span class="string">'Erreur API:'</span>, error)
  }
})

<span class="comment">// Accéder aux données</span>
<span class="keyword">const</span> products = data.<span class="property">value</span></code></pre>
          </div>
          
          <div>
            <h4 class="text-purple" v-pre>$fetch (Bas niveau)</h4>
            <pre v-pre><code class="language-typescript"><span class="comment">// Avec $fetch directement</span>
<span class="keyword">const</span> products = <span class="keyword">await</span> <span class="function">$fetch</span>(<span class="string">'/products'</span>, {
  <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
  <span class="property">method</span>: <span class="string">'GET'</span>,
  <span class="property">headers</span>: {
    <span class="string">'Authorization'</span>: <span class="template-string">`Bearer ${token}`</span>
  }
})

<span class="comment">// Avec interception d'erreur</span>
<span class="keyword">try</span> {
  <span class="keyword">const</span> response = <span class="keyword">await</span> <span class="function">$fetch</span>(<span class="string">'/api/products'</span>, {
    <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>
  })
} <span class="keyword">catch</span> (error) {
  console.<span class="function">error</span>(<span class="string">'Erreur lors du fetch:'</span>, error)
}</code></pre>
          </div>
        </div>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>4. Exemple Complet : Fetch de Produits</h2>
        
        <p class="textExemple" v-pre>
          Créons un exemple complet qui fetch des produits depuis une API Symfony et les affiche.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Composant ProductsList.vue</h4>
          <pre v-pre><code class="language-html">&lt;template&gt;
  &lt;div&gt;
    &lt;h2&gt;Liste des Produits&lt;/h2&gt;
    
    &lt;div v-if="pending" class="loading"&gt;
      Chargement des produits...
    &lt;/div&gt;
    
    &lt;div v-else-if="error" class="error"&gt;
      Erreur: {{ error.message }}
    &lt;/div&gt;
    
    &lt;div v-else&gt;
      &lt;div v-if="products.length === 0"&gt;
        Aucun produit trouvé
      &lt;/div&gt;
      
      &lt;div v-else class="products-grid"&gt;
        &lt;div v-for="product in products" :key="product.id" class="product-card"&gt;
          &lt;h3&gt;{{ product.name }}&lt;/h3&gt;
          &lt;p&gt;{{ product.description }}&lt;/p&gt;
          &lt;span class="price"&gt;{{ product.price }} €&lt;/span&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
    
    &lt;button @click="refresh" class="btn-purple"&gt;
      Rafraîchir
    &lt;/button&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script setup lang="ts"&gt;
const config = useRuntimeConfig()

// Fetch des produits
const { data: products, pending, error, refresh } = await useFetch('/products', {
  baseURL: config.public.apiBaseUrl,
  headers: {
    'Accept': 'application/json'
  },
  // Transformer la réponse si nécessaire
  transform: (response) =&gt; {
    return response['hydra:member'] || response
  }
})
&lt;/script&gt;

&lt;style scoped&gt;
.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5rem;
  margin: 2rem 0;
}

.product-card {
  background: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.product-card:hover {
  transform: translateY(-5px);
}

.price {
  font-weight: bold;
  color: #6A3093;
  font-size: 1.2rem;
}

.loading {
  padding: 2rem;
  text-align: center;
  color: #6A3093;
}

.error {
  padding: 2rem;
  background: #fee;
  border-radius: 10px;
  color: #c33;
}
&lt;/style&gt;</code></pre>
        </div>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>5. Authentification avec Symfony API Platform</h2>
        
        <p class="textExemple" v-pre>
          Pour les endpoints protégés, vous devez gérer l'authentification. Voici comment faire avec JWT :
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Service d'authentification</h4>
          <pre v-pre><code class="language-typescript"><span class="keyword">export</span> <span class="keyword">const</span> <span class="function">useAuth</span> = () =&gt; {
  <span class="keyword">const</span> token = <span class="function">useCookie</span>(<span class="string">'auth_token'</span>)
  <span class="keyword">const</span> config = <span class="function">useRuntimeConfig</span>()
  
  <span class="keyword">const</span> <span class="function">login</span> = <span class="keyword">async</span> (email: <span class="builtin">string</span>, password: <span class="builtin">string</span>) =&gt; {
    <span class="keyword">try</span> {
      <span class="keyword">const</span> response = <span class="keyword">await</span> <span class="function">$fetch</span>(<span class="string">'/authentication_token'</span>, {
        <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
        <span class="property">method</span>: <span class="string">'POST'</span>,
        <span class="property">body</span>: { email, password }
      })
      
      token.<span class="property">value</span> = response.<span class="property">token</span>
      <span class="keyword">return</span> { <span class="property">success</span>: <span class="keyword">true</span> }
    } <span class="keyword">catch</span> (error) {
      <span class="keyword">return</span> { <span class="property">success</span>: <span class="keyword">false</span>, error }
    }
  }
  
  <span class="keyword">const</span> <span class="function">logout</span> = () =&gt; {
    token.<span class="property">value</span> = <span class="keyword">null</span>
    <span class="function">navigateTo</span>(<span class="string">'/login'</span>)
  }
  
  <span class="keyword">const</span> <span class="function">fetchWithAuth</span> = <span class="keyword">async</span> (url: <span class="builtin">string</span>, options = {}) =&gt; {
    <span class="keyword">return</span> <span class="keyword">await</span> <span class="function">$fetch</span>(url, {
      <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
      <span class="property">headers</span>: {
        <span class="string">'Authorization'</span>: <span class="template-string">`Bearer ${token.value}`</span>
      },
      ...options
    })
  }
  
  <span class="keyword">return</span> {
    token,
    login,
    logout,
    fetchWithAuth,
    <span class="property">isAuthenticated</span>: <span class="function">computed</span>(() =&gt; !!token.<span class="property">value</span>)
  }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Utilisation dans un composant</h4>
          <pre v-pre><code class="language-typescript"><span class="comment">// Dans un composant</span>
<span class="keyword">const</span> auth = <span class="function">useAuth</span>()

<span class="comment">// Fetch de données protégées</span>
<span class="keyword">const</span> userProfile = <span class="keyword">await</span> auth.<span class="function">fetchWithAuth</span>(<span class="string">'/me'</span>)

<span class="comment">// Utilisation avec useFetch</span>
<span class="keyword">const</span> { <span class="property">data</span>: orders } = <span class="keyword">await</span> <span class="function">useFetch</span>(<span class="string">'/orders'</span>, {
  <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
  <span class="property">headers</span>: {
    <span class="string">'Authorization'</span>: <span class="template-string">`Bearer ${auth.token.value}`</span>
  }
})</code></pre>
        </div>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>6. Bonnes Pratiques et Optimisations</h2>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Composable réutilisable pour les appels API</h4>
          <pre v-pre><code class="language-typescript"><span class="keyword">export</span> <span class="keyword">const</span> <span class="function">useApi</span> = () =&gt; {
  <span class="keyword">const</span> config = <span class="function">useRuntimeConfig</span>()
  <span class="keyword">const</span> auth = <span class="function">useAuth</span>()
  
  <span class="keyword">const</span> <span class="function">get</span> = <span class="keyword">async</span> (endpoint: <span class="builtin">string</span>, options = {}) =&gt; {
    <span class="keyword">return</span> <span class="keyword">await</span> <span class="function">$fetch</span>(endpoint, {
      <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
      <span class="property">method</span>: <span class="string">'GET'</span>,
      <span class="property">headers</span>: <span class="function">authHeaders</span>(),
      ...options
    })
  }
  
  <span class="keyword">const</span> <span class="function">post</span> = <span class="keyword">async</span> (endpoint: <span class="builtin">string</span>, body: <span class="builtin">any</span>, options = {}) =&gt; {
    <span class="keyword">return</span> <span class="keyword">await</span> <span class="function">$fetch</span>(endpoint, {
      <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
      <span class="property">method</span>: <span class="string">'POST'</span>,
      body,
      <span class="property">headers</span>: <span class="function">authHeaders</span>(),
      ...options
    })
  }
  
  <span class="keyword">const</span> <span class="function">put</span> = <span class="keyword">async</span> (endpoint: <span class="builtin">string</span>, body: <span class="builtin">any</span>, options = {}) =&gt; {
    <span class="keyword">return</span> <span class="keyword">await</span> <span class="function">$fetch</span>(endpoint, {
      <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
      <span class="property">method</span>: <span class="string">'PUT'</span>,
      body,
      <span class="property">headers</span>: <span class="function">authHeaders</span>(),
      ...options
    })
  }
  
  <span class="keyword">const</span> <span class="function">del</span> = <span class="keyword">async</span> (endpoint: <span class="builtin">string</span>, options = {}) =&gt; {
    <span class="keyword">return</span> <span class="keyword">await</span> <span class="function">$fetch</span>(endpoint, {
      <span class="property">baseURL</span>: config.<span class="property">public</span>.<span class="property">apiBaseUrl</span>,
      <span class="property">method</span>: <span class="string">'DELETE'</span>,
      <span class="property">headers</span>: <span class="function">authHeaders</span>(),
      ...options
    })
  }
  
  <span class="keyword">const</span> <span class="function">authHeaders</span> = () =&gt; {
    <span class="keyword">const</span> headers: Record&lt;<span class="builtin">string</span>, <span class="builtin">string</span>&gt; = {
      <span class="string">'Accept'</span>: <span class="string">'application/json'</span>,
      <span class="string">'Content-Type'</span>: <span class="string">'application/json'</span>
    }
    
    <span class="keyword">if</span> (auth.<span class="property">token</span>.<span class="property">value</span>) {
      headers[<span class="string">'Authorization'</span>] = <span class="template-string">`Bearer ${auth.token.value}`</span>
    }
    
    <span class="keyword">return</span> headers
  }
  
  <span class="keyword">return</span> {
    get,
    post,
    put,
    <span class="property">delete</span>: del
  }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Gestion des erreurs centralisée</h4>
          <pre v-pre><code class="language-typescript"><span class="comment">// plugins/api.ts</span>
<span class="keyword">export</span> <span class="keyword">default</span> <span class="function">defineNuxtPlugin</span>(() =&gt; {
  <span class="keyword">const</span> { $fetch, FetchError } = <span class="function">useNuxtApp</span>()
  
  <span class="comment">// Intercepter toutes les erreurs d'API</span>
  $fetch.<span class="function">create</span>({
    <span class="function">onRequestError</span>({ <span class="property">error</span> }) {
      console.<span class="function">error</span>(<span class="string">'Erreur de requête:'</span>, error)
      <span class="comment">// Vous pouvez rediriger vers une page d'erreur ici</span>
    },
    <span class="function">onResponseError</span>({ <span class="property">response</span> }) {
      <span class="keyword">if</span> (response.<span class="property">status</span> === <span class="number">401</span>) {
        <span class="comment">// Redirection vers la page de login</span>
        <span class="function">navigateTo</span>(<span class="string">'/login'</span>)
      }
      <span class="keyword">if</span> (response.<span class="property">status</span> === <span class="number">403</span>) {
        <span class="comment">// Afficher une notification d'accès refusé</span>
        <span class="function">useToast</span>().<span class="function">error</span>(<span class="string">'Accès refusé'</span>)
      }
    }
  })
})</code></pre>
        </div>
      </section>

      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>Exercice Pratique</h2>
        
        <div class="exercise">
          <h4 class="text-purple" v-pre>Objectif</h4>
          <p class="textExemple" v-pre>
            Créez une page Nuxt qui affiche une liste d'articles depuis une API Symfony. L'API Symfony expose un endpoint <code>/api/articles</code> qui retourne des articles au format JSON.
          </p>
          
          <h4 class="text-purple" v-pre>Requirements</h4>
          <ul class="textExemple" v-pre>
            <li>Utilisez <code>useFetch</code> pour récupérer les données</li>
            <li>Affichez un indicateur de chargement pendant le fetch</li>
            <li>Gérez les erreurs (si l'API n'est pas disponible)</li>
            <li>Ajoutez un bouton pour rafraîchir les données</li>
            <li>Implémentez une recherche côté client sur les articles</li>
          </ul>
          
          <details class="solution">
            <summary class="btn-purple" v-pre>Voir la solution</summary>
            <div class="solution-content">
              <h4 class="text-purple" v-pre>Solution proposée</h4>
              <pre v-pre><code class="language-html">&lt;template&gt;
  &lt;div&gt;
    &lt;h1&gt;Articles&lt;/h1&gt;
    
    &lt;input v-model="search" placeholder="Rechercher..." class="search-input" /&gt;
    
    &lt;div v-if="pending"&gt;Chargement...&lt;/div&gt;
    &lt;div v-else-if="error"&gt;Erreur: {{ error.message }}&lt;/div&gt;
    
    &lt;div v-else&gt;
      &lt;div v-for="article in filteredArticles" :key="article.id"&gt;
        &lt;h2&gt;{{ article.title }}&lt;/h2&gt;
        &lt;p&gt;{{ article.content }}&lt;/p&gt;
      &lt;/div&gt;
    &lt;/div&gt;
    
    &lt;button @click="refresh" class="btn-purple"&gt;
      Rafraîchir les articles
    &lt;/button&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script setup lang="ts"&gt;
const config = useRuntimeConfig()
const search = ref('')

const { data: articles, pending, error, refresh } = await useFetch('/articles', {
  baseURL: config.public.apiBaseUrl
})

const filteredArticles = computed(() =&gt; {
  if (!search.value) return articles.value
  return articles.value.filter(article =&gt; 
    article.title.toLowerCase().includes(search.value.toLowerCase()) ||
    article.content.toLowerCase().includes(search.value.toLowerCase())
  )
})
&lt;/script&gt;</code></pre>
            </div>
          </details>
        </div>
      </section>

      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white mb-4" v-pre>Conclusion</h2>
        <p class="text-white" v-pre>
          Vous savez maintenant comment fetch des données depuis une API Symfony dans Nuxt 4. 
          Les points clés à retenir :
        </p>
        <ul class="text-white" v-pre>
          <li>Utilisez <code>useFetch</code> pour la plupart des cas d'usage</li>
          <li>Configurez correctement CORS dans Symfony</li>
          <li>Gérez l'authentification avec des tokens JWT</li>
          <li>Créez des composables réutilisables pour vos appels API</li>
          <li>Implémentez une gestion d'erreurs robuste</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script setup lang="ts">
const refreshPage = () => {
  window.location.reload()
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

pre code {
  display: block;
  white-space: pre-wrap;
  overflow-x: auto;
  max-width: 100%;
  width: 100%;
  word-wrap: break-word;
  word-break: break-word;
}

/* Couleurs VS Code pour la syntaxe */
.keyword { color: #c586c0 !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.variable { color: #9cdcfe !important; }
.property { color: #9cdcfe !important; }
.number { color: #b5cea8 !important; }
.operator { color: #d4d4d4 !important; }
.builtin { color: #4ec9b0 !important; }
.constant { color: #4fc1ff !important; }
.class-name { color: #4ec9b0 !important; }
.template-string { color: #ce9178 !important; }

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

.textExemple {
  margin-bottom: 1rem;
  line-height: 1.6;
}

.search-input {
  padding: 10px 15px;
  border: 2px solid #e0d6ff;
  border-radius: 8px;
  width: 100%;
  max-width: 400px;
  margin-bottom: 1.5rem;
  font-size: 1rem;
}

.search-input:focus {
  outline: none;
  border-color: #8B5FBF;
}

.mt-3 { margin-top: 1rem; }
.mt-4 { margin-top: 1.5rem; }
.mb-4 { margin-bottom: 1.5rem; }

ul {
  padding-left: 1.5rem;
  margin-bottom: 1rem;
}

li {
  margin-bottom: 0.5rem;
}

@media (max-width: 768px) {
  .lesson-container { padding: 1rem; }
  .lesson-header { padding: 2rem 1rem; }
  .lesson-header h1 { font-size: 2rem; }
  .lesson-section { padding: 1.5rem; }
  .code-comparison { grid-template-columns: 1fr; gap: 1rem; }
  pre { padding: 1rem !important; font-size: 0.85rem; }
}

@media (max-width: 480px) {
  pre { padding: 0.75rem !important; font-size: 0.8rem; }
  .lesson-container { padding: 0.5rem; }
  .lesson-section { padding: 1rem; }
  .lesson-header { padding: 1.5rem 1rem; }
  .lesson-header h1 { font-size: 1.75rem; }
}

@media (min-width: 1400px) {
  .lesson-content { max-width: 1300px; }
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
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