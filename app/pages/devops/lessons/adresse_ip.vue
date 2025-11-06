<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Les Adresses IP</h1>
        <p class="lesson-meta text-white">
          Comprendre le fonctionnement, les types et l'importance des adresses IP dans les réseaux
        </p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction aux Adresses IP</h2>
        <p class="textExemple">
          Une adresse IP (Internet Protocol) est une adresse numérique unique attribuée à chaque appareil 
          connecté à un réseau utilisant le protocole Internet. Elle sert à identifier et localiser 
          les appareils sur le réseau.
        </p>
        <p class="textExemple">
          Tout comme une adresse postale permet d'identifier une maison, une adresse IP permet 
          d'identifier un appareil sur un réseau.
        </p>
      </section>

      <!-- Objectifs de la leçon -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'Apprentissage</h2>
        <ul class="textExemple">
          <li>Comprendre le rôle des adresses IP dans les réseaux</li>
          <li>Différencier IPv4 et IPv6</li>
          <li>Maîtriser les classes d'adresses IP</li>
          <li>Comprendre le masque de sous-réseau</li>
          <li>Apprendre à calculer des sous-réseaux</li>
          <li>Connaître les adresses IP spéciales</li>
        </ul>
      </section>

      <!-- IPv4 vs IPv6 -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">IPv4 vs IPv6</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">IPv4</h3>
            <pre><code class="text">Format: 32 bits (4 octets)
Exemple: 192.168.1.1
Notation: Décimale pointée
Nombre d'adresses: ~4.3 milliards
Problème principal: Épuisement des adresses</code></pre>
            
            <div class="textExemple">
              <h4 class="text-purple">Structure IPv4</h4>
              <pre><code class="text">192    .168   .1     .1
11000000.10101000.00000001.00000001
(Format binaire)</code></pre>
            </div>
          </div>

          <div class="code-example">
            <h3 class="text-purple">IPv6</h3>
            <pre><code class="text">Format: 128 bits (16 octets)
Exemple: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
Notation: Hexadécimale
Nombre d'adresses: 3.4×10³⁸
Avantage: Espace d'adressage immense</code></pre>
            
            <div class="textExemple">
              <h4 class="text-purple">Format raccourci IPv6</h4>
              <pre><code class="text">2001:db8:85a3::8a2e:370:7334
(:: remplace les zéros consécutifs)</code></pre>
            </div>
          </div>
        </div>
      </section>

      <!-- Classes d'adresses IPv4 -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Classes d'Adresses IPv4</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Classe A</h3>
            <pre><code class="text">Plage: 1.0.0.0 à 126.255.255.255
Masque: 255.0.0.0
Réseaux: 126
Hôtes par réseau: 16+ millions
Usage: Grandes organisations</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Classe B</h3>
            <pre><code class="text">Plage: 128.0.0.0 à 191.255.255.255
Masque: 255.255.0.0
Réseaux: 16,384
Hôtes par réseau: 65,534
Usage: Organisations moyennes</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Classe C</h3>
            <pre><code class="text">Plage: 192.0.0.0 à 223.255.255.255
Masque: 255.255.255.0
Réseaux: 2+ millions
Hôtes par réseau: 254
Usage: Petits réseaux</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Classes D et E</h3>
            <pre><code class="text">Classe D: 224.0.0.0 à 239.255.255.255
→ Multicast

Classe E: 240.0.0.0 à 255.255.255.255
→ Expérimentation</code></pre>
          </div>
        </div>
      </section>

      <!-- Masques de sous-réseau -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Masques de Sous-réseau</h2>
        
        <div class="textExemple">
          <h3 class="text-purple">Notation CIDR</h3>
          <p>
            La notation CIDR (Classless Inter-Domain Routing) permet une allocation 
            plus flexible des adresses IP.
          </p>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Exemples de Masques</h3>
            <pre><code class="text">/24 → 255.255.255.0
     → 256 adresses
/25 → 255.255.255.128
     → 128 adresses
/26 → 255.255.255.192
     → 64 adresses
/30 → 255.255.255.252
     → 4 adresses (2 utilisables)</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Calcul du Masque</h3>
            <pre><code class="text">Masque: 255.255.255.0
Binaire: 11111111.11111111.11111111.00000000
Bits réseau: 24
Bits hôtes: 8
Nombre d'hôtes: 2⁸ - 2 = 254</code></pre>
          </div>
        </div>
      </section>

      <!-- Calcul de sous-réseaux -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Calcul de Sous-réseaux</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Exemple Pratique</h3>
            <pre><code class="text">Réseau: 192.168.1.0/24
Masque: 255.255.255.0
→ 256 adresses totales
→ 254 adresses utilisables

Découpage en 4 sous-réseaux:
Nouveau masque: /26 (255.255.255.192)
Sous-réseaux:
- 192.168.1.0/26 (1-62)
- 192.168.1.64/26 (65-126)
- 192.168.1.128/26 (129-190)
- 192.168.1.192/26 (193-254)</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Méthode de Calcul</h3>
            <pre><code class="text">1. Déterminer les bits d'hôte
2. Calculer le nombre de sous-réseaux
   → 2^n (n = bits empruntés)
3. Calculer le saut entre réseaux
   → 2^(8 - n) pour un /24
4. Identifier les plages d'adresses</code></pre>
            
            <div class="textExemple">
              <h4 class="text-purple">Formules Importantes</h4>
              <pre><code class="text">Nombre de sous-réseaux = 2^bits_empruntés
Nombre d'hôtes = 2^bits_hôte - 2
Masque = 2^32 - 2^bits_hôte</code></pre>
            </div>
          </div>
        </div>
      </section>

      <!-- Adresses IP spéciales -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Adresses IP Spéciales</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Adresses Réservées</h3>
            <pre><code class="text">0.0.0.0/8 → Réseau courant
127.0.0.0/8 → Localhost (bouclage)
169.254.0.0/16 → APIPA (autoconfiguration)
224.0.0.0/4 → Multicast
240.0.0.0/4 → Réservé pour usage futur</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Adresses Privées (RFC 1918)</h3>
            <pre><code class="text">10.0.0.0/8 → Grandes entreprises
   Plage: 10.0.0.0 - 10.255.255.255

172.16.0.0/12 → Organisations moyennes
   Plage: 172.16.0.0 - 172.31.255.255

192.168.0.0/16 → Réseaux domestiques
   Plage: 192.168.0.0 - 192.168.255.255</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Adresses Notables</h3>
          <pre><code class="text">127.0.0.1 → Localhost (votre propre machine)
255.255.255.255 → Broadcast limité
192.168.1.255 → Broadcast du réseau 192.168.1.0/24
192.168.1.0 → Adresse réseau
192.168.1.1 → Routeur/gateway typique</code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice Pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Énoncé</h3>
          <p class="textExemple">
            Une entreprise possède le réseau 172.16.0.0/16. Elle doit créer 8 sous-réseaux 
            pour ses différents départements. Chaque département a besoin d'au moins 2000 adresses IP.
          </p>
          
          <p class="textExemple">
            Calculez :
          </p>
          <ul class="textExemple">
            <li>Le nouveau masque de sous-réseau</li>
            <li>Les plages d'adresses pour chaque sous-réseau</li>
            <li>L'adresse réseau, broadcast et utilisable pour le premier sous-réseau</li>
          </ul>
        </div>

        <details class="solution">
          <summary class="btn-purple btn-hover">Voir la Solution</summary>
          <div class="solution-content">
            <h4 class="text-purple">Solution Détailée</h4>
            
            <div class="textExemple">
              <h5 class="text-purple">1. Détermination du nouveau masque</h5>
              <pre><code class="text">Réseau initial: 172.16.0.0/16
Bits réseau: 16
Bits hôte: 16
Adresses totales: 65,536

Besoin: 8 sous-réseaux → 2³ = 8
Bits empruntés: 3
Nouveaux bits réseau: 16 + 3 = 19
Nouveau masque: /19 (255.255.224.0)</code></pre>
            </div>

            <div class="textExemple">
              <h5 class="text-purple">2. Vérification de la capacité</h5>
              <pre><code class="text">Nouveaux bits hôte: 13
Adresses par sous-réseau: 2¹³ = 8,192
Adresses utilisables: 8,190
→ Suffisant pour 2000 adresses/département</code></pre>
            </div>

            <div class="textExemple">
              <h5 class="text-purple">3. Calcul des sous-réseaux</h5>
              <pre><code class="text">Saut entre réseaux: 2¹³ = 8,192

Sous-réseau 1: 172.16.0.0/19
- Réseau: 172.16.0.0
- Broadcast: 172.16.31.255
- Utilisable: 172.16.0.1 - 172.16.31.254

Sous-réseau 2: 172.16.32.0/19
- Réseau: 172.16.32.0
- Broadcast: 172.16.63.255

Sous-réseau 3: 172.16.64.0/19
- Réseau: 172.16.64.0
- Broadcast: 172.16.95.255

[...]

Sous-réseau 8: 172.16.224.0/19
- Réseau: 172.16.224.0
- Broadcast: 172.16.255.255</code></pre>
            </div>
          </div>
        </details>
      </section>

      <!-- Types d'adresses IP -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Types d'Adresses IP</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">IP Publique</h3>
            <pre><code class="text">Unique sur Internet
Attribuée par l'ISP
Routeable globalement
Exemple: 85.203.19.104
Coût: Souvent payante
Sécurité: Exposition directe</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">IP Privée</h3>
            <pre><code class="text">Utilisée en interne
Non routeable sur Internet
Gratuite
Exemple: 192.168.1.15
Sécurité: Protégée par NAT
Plages RFC 1918</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">IP Dynamique</h3>
            <pre><code class="text">Change périodiquement
Attribuée par DHCP
Typique pour les clients
Avantage: Économique
Inconvénient: Pas fixe</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">IP Statique</h3>
            <pre><code class="text">Adresse fixe
Configurée manuellement
Pour les serveurs, imprimantes
Avantage: Adresse constante
Inconvénient: Gestion manuelle</code></pre>
          </div>
        </div>
      </section>

      <!-- Protocoles associés -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Protocoles Associés</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">DHCP</h3>
            <pre><code class="text">Dynamic Host Configuration Protocol
Attribution automatique des IP
Gère les baux (leases)
Évite les conflits d'adresses
Réduction de la configuration manuelle</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">NAT</h3>
            <pre><code class="text">Network Address Translation
Traduction IP privée → publique
Économise les IP publiques
Couche de sécurité supplémentaire
Masquage du réseau interne</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">DNS</h3>
            <pre><code class="text">Domain Name System
Traduction nom de domaine → IP
Exemple: google.com → 172.217.20.206
Système hiérarchique distribuée
Essentiel pour la navigation web</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">ARP</h3>
            <pre><code class="text">Address Resolution Protocol
Traduction IP → MAC address
Utilisé au niveau liaison de données
Table ARP locale
Découverte des voisins réseau</code></pre>
          </div>
        </div>
      </section>

      <!-- Outils de diagnostic -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Outils de Diagnostic IP</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Commandes Windows</h3>
            <pre><code class="cmd"># Afficher la configuration IP
ipconfig
ipconfig /all

# Vider le cache DNS
ipconfig /flushdns

# Renouveler l'adresse IP
ipconfig /release
ipconfig /renew

# Test de connectivité
ping 192.168.1.1
tracert google.com</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Commandes Linux/macOS</h3>
            <pre><code class="bash"># Afficher la configuration IP
ifconfig
ip addr show

# Test de connectivité
ping 192.168.1.1
traceroute google.com

# Informations de routage
route -n
netstat -rn

# Résolution DNS
nslookup google.com
dig google.com</code></pre>
          </div>
        </div>
      </section>

      <!-- Checklist de connaissances -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Checklist de Connaissances</h2>
        
        <div class="textExemple">
          <ul>
            <li>✅ Comprendre la différence IPv4/IPv6</li>
            <li>✅ Maîtriser les classes d'adresses IPv4</li>
            <li>✅ Savoir calculer des sous-réseaux</li>
            <li>✅ Connaître les adresses privées (RFC 1918)</li>
            <li>✅ Différencier IP publique/privée</li>
            <li>✅ Comprendre le rôle du masque de sous-réseau</li>
            <li>✅ Connaître les adresses spéciales (localhost, broadcast)</li>
            <li>✅ Maîtriser les outils de diagnostic IP</li>
          </ul>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          Les adresses IP sont fondamentales pour le fonctionnement des réseaux modernes. 
          La compréhension de leur structure, de leurs types et de leur gestion est essentielle 
          pour tout professionnel des technologies de l'information.
        </p>
        <p class="textExemple">
          Avec l'épuisement des adresses IPv4, la transition vers IPv6 devient de plus en plus 
          cruciale, offrant un espace d'adressage quasi illimité pour l'Internet des objets 
          et les technologies émergentes.
        </p>
        <a href="#" class="btn-purple btn-hover">Passer à la leçon suivante</a>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonIPAddresses',
  data() {
    return {
      lessonTitle: 'Les Adresses IP',
      lessonDescription: 'Comprendre le fonctionnement, les types et la gestion des adresses IP dans les réseaux'
    }
  },
  head() {
    return {
      title: this.lessonTitle,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.lessonDescription
        }
      ]
    }
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

/* Couleurs pour différents types de code */
.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }

/* Styles spécifiques pour le texte réseau */
.text { color: #d4d4d4 !important; }
.cmd .keyword { color: #569cd6 !important; }
.bash .keyword { color: #569cd6 !important; }
.regex { color: #d16969 !important; }

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