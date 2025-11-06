<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">Le Modèle OSI</h1>
        <p class="lesson-meta text-white">
          Comprendre les 7 couches du modèle OSI et leur rôle dans la communication réseau
        </p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Introduction au Modèle OSI</h2>
        <p class="textExemple">
          Le modèle OSI (Open Systems Interconnection) est un modèle de référence qui décrit 
          comment les informations d'une application logicielle d'un ordinateur se déplacent 
          à travers un support physique vers une application logicielle d'un autre ordinateur.
        </p>
        <p class="textExemple">
          Développé par l'ISO en 1984, il divise le processus de communication réseau en 
          7 couches abstraites, chacune ayant une fonction spécifique.
        </p>
      </section>

      <!-- Objectifs de la leçon -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Objectifs d'Apprentissage</h2>
        <ul class="textExemple">
          <li>Comprendre l'utilité du modèle OSI</li>
          <li>Mémoriser les 7 couches dans l'ordre</li>
          <li>Connaître la fonction de chaque couche</li>
          <li>Identifier les protocoles associés à chaque couche</li>
          <li>Comprendre l'encapsulation des données</li>
          <li>Comparer avec le modèle TCP/IP</li>
        </ul>
      </section>

      <!-- Vue d'ensemble des 7 couches -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Les 7 Couches du Modèle OSI</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Couches Hautes (Host Layers)</h3>
            <pre><code class="text">7. Application
   → Interface utilisateur
6. Présentation
   → Formatage des données
5. Session
   → Gestion des sessions
4. Transport
   → Fiabilité des données</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Couches Basses (Media Layers)</h3>
            <pre><code class="text">3. Réseau
   → Adressage logique
2. Liaison de données
   → Adressage physique
1. Physique
   → Signal électrique/optique</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Mnémonique pour retenir l'ordre</h3>
          <pre><code class="text">APplication (7)
Présentation (6)
Session (5)
Transport (4)
Réseau (3)
Liaison (2)
Physique (1)

→ "APPele Ton Réseau Local Physiquement"</code></pre>
        </div>
      </section>

      <!-- Couche 7 - Application -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 7 : Application</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Interface avec l'utilisateur
• Services réseau aux applications
• Identification des partenaires
• Synchronisation de la communication
• Contrôle de l'intégrité des données</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Protocoles et Exemples</h3>
            <pre><code class="text">HTTP (Web)
HTTPS (Web sécurisé)
FTP (Transfert de fichiers)
SMTP (Email)
DNS (Résolution de noms)
DHCP (Attribution d'IP)

Exemples: Navigateurs, Clients email</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Données (Data)</h4>
          <p>Cette couche fournit des services directement aux applications utilisateur.</p>
        </div>
      </section>

      <!-- Couche 6 - Présentation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 6 : Présentation</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Traduction des données
• Chiffrement/Déchiffrement
• Compression/Décompression
• Conversion des formats
• Encodage/décodage</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Exemples Concrets</h3>
            <pre><code class="text">• Conversion ASCII → EBCDIC
• Chiffrement SSL/TLS
• Compression JPEG, MPEG
• Encodage Base64
• Sérialisation JSON/XML</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Données (Data)</h4>
          <p>Cette couche s'assure que les données sont dans un format compréhensible par le système récepteur.</p>
        </div>
      </section>

      <!-- Couche 5 - Session -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 5 : Session</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Établissement des sessions
• Maintien des sessions
• Fermeture des sessions
• Synchronisation du dialogue
• Gestion des jetons (tokens)</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Protocoles et Technologies</h3>
            <pre><code class="text">• RPC (Remote Procedure Call)
• NetBIOS
• PPTP (Point-to-Point Tunneling)
• Sessions HTTP
• Authentification</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Données (Data)</h4>
          <p>Cette couche gère les dialogues entre les applications des différents ordinateurs.</p>
        </div>
      </section>

      <!-- Couche 4 - Transport -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 4 : Transport</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Segmentation des données
• Contrôle de flux
• Contrôle d'erreurs
• Multiplexage des connexions
• Fiabilité de bout en bout</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Protocoles Clés</h3>
            <pre><code class="text">TCP (Transmission Control Protocol)
→ Connexion, fiable, contrôlé

UDP (User Datagram Protocol)
→ Sans connexion, non fiable, rapide

SCTP, DCCP</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">TCP vs UDP</h3>
            <pre><code class="text">TCP (Fiable)
• Accusé de réception
• Retransmission
• Contrôle de flux
• Réorganisation
Ex: HTTP, FTP, Email

UDP (Rapide)
• Aucun accusé
• Pas de retransmission
• Pas de contrôle de flux
Ex: DNS, VoIP, Streaming</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">En-tête TCP</h3>
            <pre><code class="text">Port Source (16 bits)
Port Destination (16 bits)
Numéro de Séquence (32 bits)
Numéro d'Acquittement (32 bits)
Drapeaux (SYN, ACK, FIN, etc.)
Fenêtre (16 bits)
Checksum (16 bits)
Urgent Pointer (16 bits)</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Segment (TCP) / Datagram (UDP)</h4>
          <p>Cette couche assure le transport fiable des données entre les systèmes d'extrémité.</p>
        </div>
      </section>

      <!-- Couche 3 - Réseau -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 3 : Réseau</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Adressage logique (IP)
• Routage des paquets
• Découverte de chemin
• Fragmentation des paquets
• Contrôle de congestion</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Protocoles et Équipements</h3>
            <pre><code class="text">• IP (Internet Protocol)
• ICMP (Ping, Traceroute)
• RIP, OSPF, BGP (Routage)
• Routers (Routeurs)
• Couche 3 Switches</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">En-tête IP</h3>
            <pre><code class="text">Version (4 bits)
IHL (4 bits)
Type of Service (8 bits)
Longueur Totale (16 bits)
Identification (16 bits)
Flags (3 bits)
Fragment Offset (13 bits)
TTL (8 bits)
Protocole (8 bits)
Checksum (16 bits)
IP Source (32 bits)
IP Destination (32 bits)</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Routage vs Commutation</h3>
            <pre><code class="text">Routage (Couche 3)
• Basé sur adresses IP
• Entre différents réseaux
• Prend des décisions
• Plus lent

Commutation (Couche 2)
• Basé sur adresses MAC
• Au sein d'un réseau
• Plus rapide
• Moins intelligent</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Paquet (Packet)</h4>
          <p>Cette couche gère l'adressage logique et le routage entre différents réseaux.</p>
        </div>
      </section>

      <!-- Couche 2 - Liaison de données -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 2 : Liaison de Données</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Adressage physique (MAC)
• Accès au média
• Contrôle d'erreurs
• Synchronisation des trames
• Contrôle de flux local</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Sous-couches</h3>
            <pre><code class="text">LLC (Logical Link Control)
• Interface avec couche réseau
• Contrôle de flux

MAC (Media Access Control)
• Accès au média physique
• Adressage MAC
• Détection d'erreurs</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Adresse MAC</h3>
            <pre><code class="text">Format: XX:XX:XX:XX:XX:XX
Exemple: 00:1B:44:11:3A:B7

• 48 bits (6 octets)
• 24 premiers bits: Fabricant
• 24 derniers bits: Numéro série
• Unique mondiale
• Couche 2 uniquement</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Protocoles et Équipements</h3>
            <pre><code class="text">• Ethernet (802.3)
• Wi-Fi (802.11)
• PPP (Point-to-Point)
• Switches (Commutateurs)
• Bridges (Ponts)
• ARP (Address Resolution)</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Trame (Frame)</h4>
          <p>Cette couche gère la communication entre les appareils sur le même réseau local.</p>
        </div>
      </section>

      <!-- Couche 1 - Physique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Couche 1 : Physique</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Fonctions Principales</h3>
            <pre><code class="text">• Transmission des bits
• Caractéristiques électriques
• Caractéristiques physiques
• Débit binaire
• Synchronisation des bits
• Topologie physique</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Composants et Standards</h3>
            <pre><code class="text">• Câbles (Cuivre, Fibre)
• Connecteurs (RJ45, USB)
• Hubs (Concentrateurs)
• Répéteurs
• Cartes réseau (NIC)
• Signaux radio (Wi-Fi)</code></pre>
          </div>
        </div>

        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Types de Câbles</h3>
            <pre><code class="text">Cuivre:
• UTP (Cat5e, Cat6, Cat7)
• STP (Blindé)
• Coaxial

Fibre optique:
• Multimode (courte distance)
• Monomode (longue distance)

Sans fil:
• Radio (Wi-Fi)
• Infrarouge
• Bluetooth</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Caractéristiques</h3>
            <pre><code class="text">• Bande passante
• Atténuation
• Diaphonie (Crosstalk)
• Immunité au bruit
• Impédance
• Longueur maximale</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h4 class="text-purple">Unité de données : Bit</h4>
          <p>Cette couche transmet physiquement les bits bruts sur le support de communication.</p>
        </div>
      </section>

      <!-- Processus d'encapsulation -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Processus d'Encapsulation</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Émission (Encapsulation)</h3>
            <pre><code class="text">7. Données de l'application
6. + En-tête Présentation
5. + En-tête Session
4. + En-tête Transport → Segment
3. + En-tête Réseau → Paquet
2. + En-tête Liaison → Trame
1. Conversion en bits → Transmission</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Réception (Désencapsulation)</h3>
            <pre><code class="text">1. Réception des bits
2. - En-tête Liaison → Trame
3. - En-tête Réseau → Paquet
4. - En-tête Transport → Segment
5. - En-tête Session
6. - En-tête Présentation
7. Données pour l'application</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Exemple Concret - Envoi d'un Email</h3>
          <pre><code class="text">Application: Compose le message
Présentation: Chiffre le contenu
Session: Établit la connexion SMTP
Transport: Segmente en paquets TCP
Réseau: Ajoute les adresses IP
Liaison: Ajoute les adresses MAC
Physique: Envoie les bits sur le câble</code></pre>
        </div>
      </section>

      <!-- Comparaison OSI vs TCP/IP -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">OSI vs TCP/IP</h2>
        
        <div class="code-comparison">
          <div class="code-example">
            <h3 class="text-purple">Modèle OSI (7 couches)</h3>
            <pre><code class="text">7. Application
6. Présentation
5. Session
4. Transport
3. Réseau
2. Liaison
1. Physique

→ Modèle théorique
→ Standard international
→ Pédagogique
→ Moins utilisé en pratique</code></pre>
          </div>

          <div class="code-example">
            <h3 class="text-purple">Modèle TCP/IP (4 couches)</h3>
            <pre><code class="text">Application
   (OSI 5-7)
Transport
   (OSI 4)
Internet
   (OSI 3)
Network Access
   (OSI 1-2)

→ Modèle pratique
→ Implémentation réelle
→ Base d'Internet
→ Plus simple</code></pre>
          </div>
        </div>

        <div class="textExemple">
          <h3 class="text-purple">Correspondance des Couches</h3>
          <pre><code class="text">OSI           TCP/IP
Application → Application
Présentation
Session
Transport   → Transport
Réseau      → Internet
Liaison     → Network Access
Physique</code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Exercice Pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Énoncé</h3>
          <p class="textExemple">
            Vous êtes administrateur réseau et devez résoudre un problème de connexion. 
            Un utilisateur ne peut pas accéder à un site web, mais peut ping l'adresse IP du site.
          </p>
          
          <p class="textExemple">
            En utilisant le modèle OSI, déterminez :
          </p>
          <ul class="textExemple">
            <li>Quelles couches fonctionnent correctement ?</li>
            <li>Sur quelle couche se situe probablement le problème ?</li>
            <li>Quels diagnostics supplémentaires effectuer ?</li>
            <li>Quelles solutions potentielles proposer ?</li>
          </ul>
        </div>

        <details class="solution">
          <summary class="btn-purple btn-hover">Voir la Solution</summary>
          <div class="solution-content">
            <h4 class="text-purple">Analyse par Couches OSI</h4>
            
            <div class="textExemple">
              <h5 class="text-purple">1. Couches fonctionnelles</h5>
              <pre><code class="text">Ping réussi → Les couches basses fonctionnent:
• Physique (1): Câbles OK
• Liaison (2): Connexion locale OK  
• Réseau (3): Routage IP OK
• Transport (4): ICMP (ping) fonctionne</code></pre>
            </div>

            <div class="textExemple">
              <h5 class="text-purple">2. Couche problématique</h5>
              <pre><code class="text">Le problème se situe probablement à la:
• Couche Application (7): HTTP/HTTPS
• Ou Couche Session (5): Gestion session web
• Ou Couche Présentation (6): Chiffrement SSL</code></pre>
            </div>

            <div class="textExemple">
              <h5 class="text-purple">3. Diagnostics supplémentaires</h5>
              <pre><code class="text">• Tester avec HTTP vs HTTPS
• Vérifier les paramètres proxy
• Tester un autre navigateur
• Vérifier le firewall
• Tester le port 80/443: telnet site.com 80
• Vérifier les certificats SSL
• Analyser avec Wireshark</code></pre>
            </div>

            <div class="textExemple">
              <h5 class="text-purple">4. Solutions potentielles</h5>
              <pre><code class="text">• Réinitialiser les paramètres navigateur
• Vérifier la configuration proxy
• Désactiver temporairement le firewall
• Mettre à jour les certificats
• Vérifier les paramètres DNS
• Redémarrer les services réseau</code></pre>
            </div>
          </div>
        </details>
      </section>

      <!-- Tableau récapitulatif -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Tableau Récapitulatif des Couches OSI</h2>
        
        <div class="textExemple">
          <table style="width: 100%; border-collapse: collapse; margin: 1rem 0;">
            <thead>
              <tr style="background: #6A3093; color: white;">
                <th style="padding: 12px; border: 1px solid #ddd;">Couche</th>
                <th style="padding: 12px; border: 1px solid #ddd;">Fonction</th>
                <th style="padding: 12px; border: 1px solid #ddd;">Unité</th>
                <th style="padding: 12px; border: 1px solid #ddd;">Protocoles</th>
                <th style="padding: 12px; border: 1px solid #ddd;">Équipements</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">7. Application</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Interface utilisateur</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Données</td>
                <td style="padding: 8px; border: 1px solid #ddd;">HTTP, FTP, SMTP</td>
                <td style="padding: 8px; border: 1px solid #ddd;">PC, Serveurs</td>
              </tr>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">6. Présentation</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Formatage données</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Données</td>
                <td style="padding: 8px; border: 1px solid #ddd;">SSL, JPEG, MPEG</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Gateways</td>
              </tr>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">5. Session</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Gestion sessions</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Données</td>
                <td style="padding: 8px; border: 1px solid #ddd;">NetBIOS, RPC</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Gateways</td>
              </tr>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">4. Transport</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Fiabilité données</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Segment</td>
                <td style="padding: 8px; border: 1px solid #ddd;">TCP, UDP</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Gateways</td>
              </tr>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">3. Réseau</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Routage logique</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Paquet</td>
                <td style="padding: 8px; border: 1px solid #ddd;">IP, ICMP</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Routeurs</td>
              </tr>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">2. Liaison</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Accès média</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Trame</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Ethernet, Wi-Fi</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Switches</td>
              </tr>
              <tr>
                <td style="padding: 8px; border: 1px solid #ddd;">1. Physique</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Transmission bits</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Bit</td>
                <td style="padding: 8px; border: 1px solid #ddd;">RJ45, Fiber</td>
                <td style="padding: 8px; border: 1px solid #ddd;">Hubs, Câbles</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>

      <!-- Checklist de connaissances -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Checklist de Connaissances</h2>
        
        <div class="textExemple">
          <ul>
            <li>✅ Nommer les 7 couches OSI dans l'ordre</li>
            <li>✅ Expliquer la fonction de chaque couche</li>
            <li>✅ Associer les protocoles aux couches appropriées</li>
            <li>✅ Différencier les unités de données par couche</li>
            <li>✅ Comprendre le processus d'encapsulation</li>
            <li>✅ Comparer OSI avec TCP/IP</li>
            <li>✅ Résoudre des problèmes réseau avec l'approche OSI</li>
            <li>✅ Identifier les équipements par couche</li>
          </ul>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">Conclusion</h2>
        <p class="textExemple">
          Le modèle OSI reste une référence fondamentale pour comprendre les réseaux informatiques. 
          Bien que le modèle TCP/IP soit plus utilisé en pratique, la connaissance du modèle OSI 
          est essentielle pour le dépannage, la conception et la compréhension des réseaux.
        </p>
        <p class="textExemple">
          L'approche par couches permet de modulariser les problèmes complexes et facilite 
          l'interopérabilité entre les différents fabricants et technologies.
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

/* Styles pour le tableau */
table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

th, td {
    padding: 12px;
    border: 1px solid #e0d6ff;
    text-align: left;
}

th {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
    color: white;
    font-weight: 600;
}

tr:nth-child(even) {
    background-color: #f8f6ff;
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
    
    /* Tableau responsive */
    table {
        display: block;
        overflow-x: auto;
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
    
    th, td {
        padding: 8px;
        font-size: 0.9rem;
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