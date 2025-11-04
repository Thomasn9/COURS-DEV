<template>
  <div class="lesson-container">
    <div class="lesson-content">
      <!-- En-tête de la leçon -->
      <header class="lesson-header">
        <h1 class="text-white">🔒 Audit de Sécurité Informatique</h1>
        <p class="lesson-meta text-white">Maîtriser les méthodes et outils pour évaluer et renforcer la sécurité des systèmes</p>
      </header>

      <!-- Introduction -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">🛡️ Qu'est-ce qu'un audit de sécurité ?</h2>
        <p class="textExemple">
          Un <strong>audit de sécurité</strong> est une évaluation systématique et méthodique visant à identifier 
          les vulnérabilités, mesurer les risques et vérifier la conformité aux politiques de sécurité d'un système d'information.
        </p>
        
        <div class="bg-gradient-primary text-white" style="padding: 1.5rem; border-radius: 10px; margin: 1.5rem 0;">
          <h3 class="text-white">Objectifs principaux :</h3>
          <ul>
            <li>Identifier les <strong>vulnérabilités techniques</strong> et organisationnelles</li>
            <li>Évaluer le <strong>niveau de risque</strong> pour l'organisation</li>
            <li>Vérifier la <strong>conformité</strong> aux réglementations et standards</li>
            <li>Proposer un <strong>plan d'action</strong> pour améliorer la sécurité</li>
          </ul>
        </div>

        <div class="solution-content">
          <h4 class="text-purple">🎯 Différence avec un test d'intrusion</h4>
          <p>
            Contrairement à un test d'intrusion qui se concentre sur l'exploitation technique, 
            l'audit de sécurité adopte une <strong>vision globale</strong> incluant les aspects organisationnels, 
            humains et techniques.
          </p>
        </div>
      </section>

      <!-- Types d'audit -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">📋 Types d'audits de sécurité</h2>
        
        <div class="code-comparison">
          <div class="audit-type">
            <h4 class="text-purple">🔍 Audit Technique</h4>
            <ul>
              <li>Analyse des configurations systèmes</li>
              <li>Tests de vulnérabilités automatisés</li>
              <li>Revue de code et architecture</li>
              <li>Tests d'intrusion</li>
            </ul>
          </div>
          
          <div class="audit-type">
            <h4 class="text-purple">🏢 Audit Organisationnel</h4>
            <ul>
              <li>Politiques et procédures de sécurité</li>
              <li>Gestion des identités et accès</li>
              <li>Formation et sensibilisation</li>
              <li>Plan de continuité d'activité</li>
            </ul>
          </div>
          
          <div class="audit-type">
            <h4 class="text-purple">📊 Audit de Conformité</h4>
            <ul>
              <li>RGPD / Protection des données</li>
              <li>ISO 27001 / SOC 2</li>
              <li>Hébergement de données de santé</li>
              <li>Secteurs réglementés (banque, santé)</li>
            </ul>
          </div>
          
          <div class="audit-type">
            <h4 class="text-purple">⚡ Audit d'Applications</h4>
            <ul>
              <li>Tests SAST / DAST</li>
              <li>Analyse des dépendances</li>
              <li>Revue de code sécurité</li>
              <li>Tests de sécurité API</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Méthodologie -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">🧠 Méthodologie d'audit de sécurité</h2>
        
        <div class="methodology-steps">
          <div class="step">
            <h3 class="text-purple">1️⃣ Préparation et Cadrage</h3>
            <ul>
              <li>Définition du <strong>périmètre</strong> et des <strong>objectifs</strong></li>
              <li>Signature de la <strong>charte d'audit</strong> et <strong>accords de confidentialité</strong></li>
              <li>Identification des <strong>contraintes techniques</strong> et <strong>plages horaires</strong></li>
              <li>Collecte de la <strong>documentation</strong> existante</li>
            </ul>
          </div>
          
          <div class="step">
            <h3 class="text-purple">2️⃣ Collecte d'Informations</h3>
            <ul>
              <li>Cartographie du <strong>système d'information</strong></li>
              <li>Identification des <strong>actifs critiques</strong></li>
              <li>Recensement des <strong>données sensibles</strong></li>
              <li>Analyse des <strong>flux réseau</strong> et <strong>architectures</strong></li>
            </ul>
          </div>

          <div class="step">
            <h3 class="text-purple">3️⃣ Analyse des Vulnérabilités</h3>
            <div class="vulnerability-analysis">
              <div class="vuln-category">
                <strong>🔧 Techniques</strong>
                <p>Scan de vulnérabilités, tests configurations</p>
              </div>
              <div class="vuln-category">
                <strong>👥 Organisationnelles</strong>
                <p>Politiques, procédures, formations</p>
              </div>
              <div class="vuln-category">
                <strong>📝 Conformité</strong>
                <p>Respect des réglementations applicables</p>
              </div>
            </div>
          </div>

          <div class="step">
            <h3 class="text-purple">4️⃣ Évaluation des Risques</h3>
            <div class="risk-matrix">
              <div class="risk-item critical">
                <strong>Risque Critique</strong>
                <p>Impact élevé + Probabilité élevée</p>
              </div>
              <div class="risk-item high">
                <strong>Risque Élevé</strong>
                <p>Impact élevé + Probabilité moyenne</p>
              </div>
              <div class="risk-item medium">
                <strong>Risque Moyen</strong>
                <p>Impact moyen + Probabilité moyenne</p>
              </div>
              <div class="risk-item low">
                <strong>Risque Faible</strong>
                <p>Impact faible + Probabilité faible</p>
              </div>
            </div>
          </div>

          <div class="step">
            <h3 class="text-purple">5️⃣ Rapport et Recommandations</h3>
            <ul>
              <li>Synthèse des <strong>vulnérabilités identifiées</strong></li>
              <li>Évaluation du <strong>niveau de risque</strong></li>
              <li>Recommandations <strong>priorisées</strong> (court/moyen/long terme)</li>
              <li>Plan d'action <strong>concret et réalisable</strong></li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Outils d'audit -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">🧰 Outils d'audit de sécurité</h2>
        
        <div class="tools-grid">
          <div class="tool-category">
            <h4 class="text-purple">🔍 Scan de Vulnérabilités</h4>
            <ul>
              <li><strong>Nessus</strong> - Scanner de vulnérabilités réseau</li>
              <li><strong>OpenVAS</strong> - Alternative open source à Nessus</li>
              <li><strong>Qualys</strong> - Plateforme cloud de sécurité</li>
              <li><strong>Nexpose</strong> - Gestion des vulnérabilités</li>
            </ul>
          </div>
          
          <div class="tool-category">
            <h4 class="text-purple">🌐 Tests Web</h4>
            <ul>
              <li><strong>Burp Suite</strong> - Test d'applications web</li>
              <li><strong>OWASP ZAP</strong> - Scanner web open source</li>
              <li><strong>SQLmap</strong> - Test d'injection SQL</li>
              <li><strong>Nikto</strong> - Scanner de serveurs web</li>
            </ul>
          </div>
          
          <div class="tool-category">
            <h4 class="text-purple">📊 Analyse de Code</h4>
            <ul>
              <li><strong>SonarQube</strong> - Qualité et sécurité du code</li>
              <li><strong>Checkmarx</strong> - Analyse statique de code</li>
              <li><strong>Snyk</strong> - Sécurité des dépendances</li>
              <li><strong>GitHub Security</strong> - Détection des vulnérabilités</li>
            </ul>
          </div>
          
          <div class="tool-category">
            <h4 class="text-purple">🔧 Analyse Réseau</h4>
            <ul>
              <li><strong>Nmap</strong> - Découverte réseau et ports</li>
              <li><strong>Wireshark</strong> - Analyse de trafic réseau</li>
              <li><strong>Metasploit</strong> - Framework de tests d'intrusion</li>
              <li><strong>Aircrack-ng</strong> - Sécurité WiFi</li>
            </ul>
          </div>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Exemple de scan Nmap</h4>
          <pre><code class="bash"><span class="comment"># Scan de découverte réseau</span>
<span class="variable">nmap</span> -sn <span class="number">192.168.1.0</span>/<span class="number">24</span>

<span class="comment"># Scan des ports ouverts avec détection de services</span>
<span class="variable">nmap</span> -sS -sV -O <span class="number">192.168.1.1</span>

<span class="comment"># Scan de vulnérabilités avec scripts NSE</span>
<span class="variable">nmap</span> --script vuln <span class="number">192.168.1.1</span>

<span class="comment"># Scan UDP des ports importants</span>
<span class="variable">nmap</span> -sU -p <span class="number">53,161,162</span> <span class="number">192.168.1.1</span>

<span class="comment"># Output formaté pour rapport</span>
<span class="variable">nmap</span> -oA audit_scan <span class="number">192.168.1.1</span></code></pre>
        </div>
      </section>

      <!-- Méthodologies de test -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">🎯 Méthodologies de test reconnues</h2>
        
        <div class="methodologies-comparison">
          <div class="methodology">
            <h4 class="text-purple">OWASP Testing Guide</h4>
            <p><strong>Focus :</strong> Applications web</p>
            <p><strong>Phases :</strong> Prise d'information, configuration, authentification, sessions, validation</p>
            <div class="btn-purple btn-hover" style="margin-top: 0.5rem;">Voir le guide</div>
          </div>
          
          <div class="methodology">
            <h4 class="text-purple">PTES - Penetration Testing Execution Standard</h4>
            <p><strong>Focus :</strong> Tests d'intrusion complets</p>
            <p><strong>Phases :</strong> 7 phases de pré-engagement à post-engagement</p>
            <div class="btn-purple btn-hover" style="margin-top: 0.5rem;">Voir le standard</div>
          </div>
          
          <div class="methodology">
            <h4 class="text-purple">NIST SP 800-115</h4>
            <p><strong>Focus :</strong> Tests de sécurité technique</p>
            <p><strong>Phases :</strong> Planification, découverte, attaque, reporting</p>
            <div class="btn-purple btn-hover" style="margin-top: 0.5rem;">Voir le guide</div>
          </div>
        </div>
      </section>

      <!-- Checklist OWASP Top 10 -->
      <section class="lesson-section bg-gradient-primary">
        <h2 class="text-white">📋 OWASP Top 10 - Checklist d'audit</h2>
        
        <div class="owasp-checklist">
          <div class="owasp-item">
            <h4 class="text-white">A01:2021 - Broken Access Control</h4>
            <ul>
              <li>✅ Vérifier les contrôles d'accès métier</li>
              <li>✅ Tester l'élévation de privilèges</li>
              <li>✅ Auditer les contrôles CORS</li>
            </ul>
          </div>
          
          <div class="owasp-item">
            <h4 class="text-white">A02:2021 - Cryptographic Failures</h4>
            <ul>
              <li>✅ Vérifier le chiffrement des données sensibles</li>
              <li>✅ Auditer les algorithmes cryptographiques</li>
              <li>✅ Contrôler la gestion des clés</li>
            </ul>
          </div>
          
          <div class="owasp-item">
            <h4 class="text-white">A03:2021 - Injection</h4>
            <ul>
              <li>✅ Tester les injections SQL, NoSQL, OS</li>
              <li>✅ Vérifier la validation des entrées</li>
              <li>✅ Auditer les requêtes paramétrées</li>
            </ul>
          </div>
          
          <div class="owasp-item">
            <h4 class="text-white">A07:2021 - Identification and Authentication Failures</h4>
            <ul>
              <li>✅ Tester la robustesse des mots de passe</li>
              <li>✅ Vérifier les mécanismes 2FA</li>
              <li>✅ Auditer la gestion des sessions</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Bonnes pratiques -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">💡 Bonnes pratiques d'audit de sécurité</h2>
        
        <div class="best-practices-grid">
          <div class="practice">
            <h4 class="text-purple">📝 Documentation Complète</h4>
            <p>Maintenir une trace de toutes les activités d'audit, des preuves et des constatations</p>
          </div>
          
          <div class="practice">
            <h4 class="text-purple">⚖️ Approche Éthique</h4>
            <p>Respecter le cadre légal et obtenir les autorisations nécessaires avant tout test</p>
          </div>
          
          <div class="practice">
            <h4 class="text-purple">🎯 Périmètre Défini</h4>
            <p>Clairement délimiter les systèmes, réseaux et plages horaires autorisés pour les tests</p>
          </div>
          
          <div class="practice">
            <h4 class="text-purple">🔄 Amélioration Continue</h4>
            <p>Planifier des audits réguliers et suivre l'implémentation des recommandations</p>
          </div>
          
          <div class="practice">
            <h4 class="text-purple">👥 Communication</h4>
            <p>Maintenir une communication transparente avec les parties prenantes durant tout le processus</p>
          </div>
          
          <div class="practice">
            <h4 class="text-purple">🔧 Outils Appropriés</h4>
            <p>Utiliser des outils adaptés au contexte et les maintenir à jour</p>
          </div>
        </div>
      </section>

      <!-- Cadre légal et éthique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">⚖️ Cadre légal et éthique</h2>
        
        <div class="legal-grid">
          <div class="legal-item">
            <h4 class="text-purple">📜 Autorisations Écrites</h4>
            <p>Obtenir une <strong>autorisation écrite</strong> signée par le responsable légal avant tout test</p>
          </div>
          
          <div class="legal-item">
            <h4 class="text-purple">🔒 Confidentialité</h4>
            <p>Respecter la <strong>confidentialité</strong> des données et résultats d'audit</p>
          </div>
          
          <div class="legal-item">
            <h4 class="text-purple">📋 Périmètre Défini</h4>
            <p>Ne pas dépasser le <strong>périmètre autorisé</strong> défini dans la charte d'audit</p>
          </div>
          
          <div class="legal-item">
            <h4 class="text-purple">⏰ Plages Horaires</h4>
            <p>Respecter les <strong>plages horaires</strong> convenues pour les tests intrusifs</p>
          </div>
        </div>

        <div class="code-example">
          <h4 class="text-purple">Exemple de clause de responsabilité</h4>
          <pre><code class="text"><span class="comment">CHARTE D'AUDIT DE SÉCURITÉ</span>

<span class="keyword">Périmètre autorisé</span> : 
- Domaine : *.entreprise.com
- Adresses IP : 192.168.1.0/24
- Plages horaires : 20h00 - 06h00 (HEURE LOCALE)

<span class="keyword">Activités interdites</span> :
- Deni de Service (DoS/DDoS)
- Social engineering sur le personnel
- Tests sur l'infrastructure de production critique

<span class="keyword">Engagements de l'auditeur</span> :
- Confidentialité des données et résultats
- Communication immédiate des incidents critiques
- Restitution des accès après l'audit

<span class="keyword">Signature</span> :
___________________________
Responsable Légal - Entreprise
___________________________
Auditeur - Cabinet de sécurité</code></pre>
        </div>
      </section>

      <!-- Exercice pratique -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">💻 Exercice pratique</h2>
        
        <div class="exercise">
          <h3 class="text-purple">Audit d'une application web e-commerce</h3>
          <p class="textExemple">
            Vous devez réaliser un audit de sécurité sur une application e-commerce présentant :
          </p>
          <ul>
            <li>Formulaire de paiement avec carte bancaire</li>
            <li>Espace client avec données personnelles</li>
            <li>Backoffice d'administration</li>
            <li>API REST pour application mobile</li>
          </ul>
          
          <p class="textExemple">
            Élaborez un plan d'audit détaillé incluant les tests à réaliser et les outils à utiliser.
          </p>
        </div>

        <details class="solution">
          <summary class="btn-purple">Voir la solution</summary>
          <div class="solution-content">
            <h4 class="text-purple">Plan d'audit recommandé :</h4>
            
            <h5>Phase 1 - Analyse de surface d'attaque</h5>
            <ul>
              <li>Cartographie de l'application (Burp Suite, OWASP ZAP)</li>
              <li>Identification des technologies utilisées (Wappalyzer)</li>
              <li>Analyse des en-têtes de sécurité</li>
            </ul>
            
            <h5>Phase 2 - Tests d'authentification et session</h5>
            <ul>
              <li>Tests de robustesse des mots de passe</li>
              <li>Analyse de la gestion des sessions</li>
              <li>Tests de ré-authentification sur actions sensibles</li>
            </ul>
            
            <h5>Phase 3 - Tests des fonctionnalités métier</h5>
            <ul>
              <li>Tests d'injection sur le moteur de recherche</li>
              <li>Validation des processus de paiement</li>
              <li>Tests d'accès direct aux objets</li>
            </ul>
            
            <h5>Phase 4 - Audit de l'API</h5>
            <ul>
              <li>Tests d'authentification API</li>
              <li>Validation des schémas de requêtes</li>
              <li>Tests de rate limiting</li>
            </ul>
            
            <h4 class="text-purple">Outils recommandés :</h4>
            <ul>
              <li><strong>Burp Suite Professional</strong> - Tests complets application web</li>
              <li><strong>SQLmap</strong> - Tests d'injection SQL automatisés</li>
              <li><strong>Nuclei</strong> - Scan de vulnérabilités templates</li>
              <li><strong>Postman</strong> - Tests d'API REST</li>
            </ul>
          </div>
        </details>
      </section>

      <!-- Livrables -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">📊 Livrables d'un audit de sécurité</h2>
        
        <div class="deliverables-security">
          <div class="deliverable">
            <h4 class="text-purple">📋 Rapport d'audit détaillé</h4>
            <ul>
              <li>Contexte et méthodologie</li>
              <li>Vulnérabilités classées par criticité</li>
              <li>Preuves et captures d'écran</li>
              <li>Analyse de risque détaillée</li>
            </ul>
          </div>
          
          <div class="deliverable">
            <h4 class="text-purple">🎯 Plan d'action priorisé</h4>
            <ul>
              <li>Recommandations court terme (0-30 jours)</li>
              <li>Recommandations moyen terme (1-6 mois)</li>
              <li>Recommandations long terme (6+ mois)</li>
              <li>Estimation des efforts et coûts</li>
            </ul>
          </div>
          
          <div class="deliverable">
            <h4 class="text-purple">📈 Tableau de bord de suivi</h4>
            <ul>
              <li>État d'avancement des corrections</li>
              <li>Métriques de sécurité</li>
              <li>Indicateurs de conformité</li>
              <li>Plan de ré-audit</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="lesson-section bg-light-purple border-purple">
        <h2 class="text-purple">🔐 En résumé</h2>
        
        <div class="summary-content">
          <blockquote class="summary-quote">
            L'audit de sécurité est un <strong>processus structuré et continu</strong> qui permet de protéger 
            les actifs informationnels en identifiant proactivement les vulnérabilités et en mesurant 
            l'efficacité des contrôles de sécurité.
          </blockquote>
          
          <div class="key-points">
            <div class="point">
              <span class="emoji">🎯</span>
              <p>Adopter une <strong>approche méthodique</strong> basée sur les standards</p>
            </div>
            <div class="point">
              <span class="emoji">⚖️</span>
              <p>Respecter scrupuleusement le <strong>cadre légal et éthique</strong></p>
            </div>
            <div class="point">
              <span class="emoji">🔧</span>
              <p>Utiliser les <strong>outils appropriés</strong> pour chaque type de test</p>
            </div>
            <div class="point">
              <span class="emoji">📈</span>
              <p>Fournir des <strong>recommandations actionnables</strong> et priorisées</p>
            </div>
          </div>
          
          <div class="final-quote">
            <p>💬 "La sécurité n'est pas un produit, mais un processus continu d'amélioration."</p>
          </div>
        </div>
        
        <div class="btn-purple btn-hover" style="margin-top: 2rem;">Leçon terminée</div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SecurityAuditLesson',
  data() {
    return {
      lessonTitle: 'Audit de Sécurité Informatique',
      lessonDescription: 'Maîtriser les méthodes et outils pour évaluer et renforcer la sécurité des systèmes'
    }
  },
  mounted() {
    // Animation d'entrée pour les sections
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.style.opacity = '1';
          entry.target.style.transform = 'translateY(0)';
        }
      });
    });

    document.querySelectorAll('.lesson-section').forEach((section) => {
      section.style.opacity = '0';
      section.style.transform = 'translateY(20px)';
      section.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
      observer.observe(section);
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

/* Couleurs VS Code pour la syntaxe */
.keyword { color: #c586c0 !important; }
.variable { color: #9cdcfe !important; }
.string { color: #ce9178 !important; }
.comment { color: #6a9955 !important; }
.function { color: #dcdcaa !important; }
.operator { color: #d4d4d4 !important; }
.constant { color: #4fc1ff !important; }
.number { color: #b5cea8 !important; }
.class-name { color: #4ec9b0 !important; }

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

/* Styles spécifiques pour cette leçon */
.audit-type, .methodology, .owasp-item, .deliverable {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
    margin-bottom: 1rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.tools-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.tool-category {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #6A3093;
}

.methodology-steps .step {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    margin-bottom: 1.5rem;
    border-left: 4px solid #6A3093;
}

.vulnerability-analysis, .risk-matrix {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
}

.vuln-category, .risk-item {
    background: #f8f6ff;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
}

.risk-item.critical { border-left: 4px solid #dc3545; }
.risk-item.high { border-left: 4px solid #fd7e14; }
.risk-item.medium { border-left: 4px solid #ffc107; }
.risk-item.low { border-left: 4px solid #28a745; }

.methodologies-comparison {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
}

.owasp-checklist {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
}

.owasp-item {
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.best-practices-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
}

.practice {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    text-align: center;
    border: 2px solid #e0d6ff;
}

.legal-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.legal-item {
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
    border-left: 4px solid #8B5FBF;
}

.deliverables-security {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
}

.summary-content {
    text-align: center;
}

.summary-quote {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    font-style: italic;
    font-size: 1.2rem;
    margin-bottom: 2rem;
    border-left: 4px solid #6A3093;
}

.key-points {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin: 2rem 0;
}

.point {
    display: flex;
    align-items: center;
    gap: 1rem;
    background: white;
    padding: 1.5rem;
    border-radius: 10px;
}

.emoji {
    font-size: 2rem;
}

.final-quote {
    background: #f8f6ff;
    padding: 1.5rem;
    border-radius: 10px;
    font-style: italic;
    text-align: center;
    margin-top: 2rem;
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
    
    .code-comparison, .tools-grid, .methodologies-comparison,
    .owasp-checklist, .best-practices-grid, .legal-grid,
    .deliverables-security, .key-points {
        grid-template-columns: 1fr;
        gap: 1rem;
    }
    
    .vulnerability-analysis, .risk-matrix {
        grid-template-columns: 1fr;
    }
    
    pre {
        padding: 1rem !important;
        font-size: 0.85rem;
    }
    
    .point {
        flex-direction: column;
        text-align: center;
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