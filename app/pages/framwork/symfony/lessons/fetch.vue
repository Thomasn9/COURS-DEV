<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- Header de la leçon -->
      <div class="lesson-header">
        <h1 class="text-white" v-pre>Fetch des données depuis une API Symfony avec Nuxt</h1>
        <p class="lesson-meta text-white" v-pre>
          Apprenez à communiquer efficacement entre un frontend Nuxt et un backend Symfony
        </p>
      </div>

      <!-- Section d'introduction -->
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

      <!-- Section Configuration de l'API Symfony -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>1. Configuration de l'API Symfony</h2>
        <p class="textExemple" v-pre>
          Avant de pouvoir fetch des données depuis Nuxt, assurez-vous que votre API Symfony est correctement configurée pour accepter les requêtes CORS.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Configuration CORS dans Symfony</h4>
          <pre v-pre><code class="language-php">// config/packages/nelmio_cors.yaml
nelmio_cors:
    defaults:
        origin_regex: true
        allow_origin: ['%env(CORS_ALLOW_ORIGIN)%']
        allow_methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE', 'OPTIONS']
        allow_headers: ['Content-Type', 'Authorization']
        expose_headers: ['Link']
        max_age: 3600
    paths:
        '^/api/':
            allow_origin: ['http://localhost:3000', 'http://127.0.0.1:3000']
            allow_headers: ['*']
            allow_methods: ['*']
            max_age: 3600</code></pre>
        </div>

        <p class="textExemple mt-3" v-pre>
          Dans votre <code>.env</code> Symfony, ajoutez :
        </p>
        
        <div class="code-example">
          <pre v-pre><code class="language-bash">CORS_ALLOW_ORIGIN=^https?://(localhost|127\.0\.0\.1)(:[0-9]+)?$</code></pre>
        </div>
      </section>

      <!-- Section Configuration Nuxt -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>2. Configuration de Nuxt pour communiquer avec Symfony</h2>
        
        <p class="textExemple" v-pre>
          Dans votre projet Nuxt, vous devez configurer l'URL de base de votre API Symfony.
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Configuration dans nuxt.config.ts</h4>
          <pre v-pre><code class="language-typescript">// nuxt.config.ts
export default defineNuxtConfig({
  runtimeConfig: {
    public: {
      apiBaseUrl: process.env.API_BASE_URL || 'http://localhost:8000/api'
    }
  },
  
  // Configuration pour les appels API côté serveur
  nitro: {
    routeRules: {
      '/api/**': {
        proxy: process.env.API_BASE_URL + '/**'
      }
    }
  }
})</code></pre>
        </div>

        <div class="code-example">
          <h4 class="text-purple" v-pre>Fichier .env de Nuxt</h4>
          <pre v-pre><code class="language-bash"># .env
API_BASE_URL=http://localhost:8000
NUXT_PUBLIC_API_BASE_URL=http://localhost:8000/api</code></pre>
        </div>
      </section>

      <!-- Section Méthodes de Fetch -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>3. Méthodes de Fetch dans Nuxt 4</h2>
        
        <p class="textExemple" v-pre>
          Nuxt 4 offre plusieurs méthodes pour fetch des données. Voici les principales :
        </p>
        
        <div class="code-comparison">
          <div>
            <h4 class="text-purple" v-pre>useFetch (Recommandé)</h4>
            <pre v-pre><code class="language-typescript">// Dans un composant ou page
const { data, pending, error, refresh } = await useFetch('/products', {
  baseURL: config.public.apiBaseUrl,
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  onRequest({ request, options }) {
    // Ajouter un token d'authentification si nécessaire
    options.headers = {
      ...options.headers,
      'Authorization': `Bearer ${token.value}`
    }
  },
  onResponse({ response }) {
    // Traiter la réponse
    console.log('Données reçues:', response._data)
  },
  onResponseError({ error }) {
    // Gérer les erreurs
    console.error('Erreur API:', error)
  }
})

// Accéder aux données
const products = data.value</code></pre>
          </div>
          
          <div>
            <h4 class="text-purple" v-pre>$fetch (Bas niveau)</h4>
            <pre v-pre><code class="language-typescript">// Avec $fetch directement
const products = await $fetch('/products', {
  baseURL: config.public.apiBaseUrl,
  method: 'GET',
  headers: {
    'Authorization': `Bearer ${token}`
  }
})

// Avec interception d'erreur
try {
  const response = await $fetch('/api/products', {
    baseURL: config.public.apiBaseUrl
  })
} catch (error) {
  console.error('Erreur lors du fetch:', error)
}</code></pre>
          </div>
        </div>
      </section>

      <!-- Section Exemple Complet -->
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

      <!-- Section Authentification -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>5. Authentification avec Symfony API Platform</h2>
        
        <p class="textExemple" v-pre>
          Pour les endpoints protégés, vous devez gérer l'authentification. Voici comment faire avec JWT :
        </p>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Service d'authentification</h4>
          <pre v-pre><code class="language-typescript">// composables/useAuth.ts
export const useAuth = () =&gt; {
  const token = useCookie('auth_token')
  const config = useRuntimeConfig()
  
  const login = async (email: string, password: string) =&gt; {
    try {
      const response = await $fetch('/authentication_token', {
        baseURL: config.public.apiBaseUrl,
        method: 'POST',
        body: { email, password }
      })
      
      token.value = response.token
      return { success: true }
    } catch (error) {
      return { success: false, error }
    }
  }
  
  const logout = () =&gt; {
    token.value = null
    navigateTo('/login')
  }
  
  const fetchWithAuth = async (url: string, options = {}) =&gt; {
    return await $fetch(url, {
      baseURL: config.public.apiBaseUrl,
      headers: {
        'Authorization': `Bearer ${token.value}`
      },
      ...options
    })
  }
  
  return {
    token,
    login,
    logout,
    fetchWithAuth,
    isAuthenticated: computed(() =&gt; !!token.value)
  }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Utilisation dans un composant</h4>
          <pre v-pre><code class="language-typescript">// Dans un composant
const auth = useAuth()

// Fetch de données protégées
const userProfile = await auth.fetchWithAuth('/me')

// Utilisation avec useFetch
const { data: orders } = await useFetch('/orders', {
  baseURL: config.public.apiBaseUrl,
  headers: {
    'Authorization': `Bearer ${auth.token.value}`
  }
})</code></pre>
        </div>
      </section>

      <!-- Section Bonnes Pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple mb-4" v-pre>6. Bonnes Pratiques et Optimisations</h2>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Composable réutilisable pour les appels API</h4>
          <pre v-pre><code class="language-typescript">// composables/useApi.ts
export const useApi = () =&gt; {
  const config = useRuntimeConfig()
  const auth = useAuth()
  
  const get = async (endpoint: string, options = {}) =&gt; {
    return await $fetch(endpoint, {
      baseURL: config.public.apiBaseUrl,
      method: 'GET',
      headers: authHeaders(),
      ...options
    })
  }
  
  const post = async (endpoint: string, body: any, options = {}) =&gt; {
    return await $fetch(endpoint, {
      baseURL: config.public.apiBaseUrl,
      method: 'POST',
      body,
      headers: authHeaders(),
      ...options
    })
  }
  
  const put = async (endpoint: string, body: any, options = {}) =&gt; {
    return await $fetch(endpoint, {
      baseURL: config.public.apiBaseUrl,
      method: 'PUT',
      body,
      headers: authHeaders(),
      ...options
    })
  }
  
  const del = async (endpoint: string, options = {}) =&gt; {
    return await $fetch(endpoint, {
      baseURL: config.public.apiBaseUrl,
      method: 'DELETE',
      headers: authHeaders(),
      ...options
    })
  }
  
  const authHeaders = () =&gt; {
    const headers: Record&lt;string, string&gt; = {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    }
    
    if (auth.token.value) {
      headers['Authorization'] = `Bearer ${auth.token.value}`
    }
    
    return headers
  }
  
  return {
    get,
    post,
    put,
    delete: del
  }
}</code></pre>
        </div>
        
        <div class="code-example">
          <h4 class="text-purple" v-pre>Gestion des erreurs centralisée</h4>
          <pre v-pre><code class="language-typescript">// plugins/api.ts
export default defineNuxtPlugin(() =&gt; {
  const { $fetch, FetchError } = useNuxtApp()
  
  // Intercepter toutes les erreurs d'API
  $fetch.create({
    onRequestError({ error }) {
      console.error('Erreur de requête:', error)
      // Vous pouvez rediriger vers une page d'erreur ici
    },
    onResponseError({ response }) {
      if (response.status === 401) {
        // Redirection vers la page de login
        navigateTo('/login')
      }
      if (response.status === 403) {
        // Afficher une notification d'accès refusé
        useToast().error('Accès refusé')
      }
    }
  })
})</code></pre>
        </div>
      </section>

      <!-- Section Exercice -->
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

      <!-- Section Conclusion -->
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

.ml-3 {
  margin-left: 1rem;
}

.mt-3 {
  margin-top: 1rem;
}

.mt-4 {
  margin-top: 1.5rem;
}

.mb-4 {
  margin-bottom: 1.5rem;
}

/* Styles pour les listes */
ul {
  padding-left: 1.5rem;
  margin-bottom: 1rem;
}

li {
  margin-bottom: 0.5rem;
}

/* Amélioration de l'affichage du code */
pre {
  position: relative;
  margin-top: 1rem;
}

pre::before {
  content: '📋';
  position: absolute;
  top: 10px;
  right: 10px;
  color: #aaa;
  cursor: pointer;
  font-size: 1.2rem;
}

pre:hover::before {
  color: #fff;
}
</style>