# Rapport d'analyse de sécurité mobile

## A. Informations générales
- **Date** : 2026-05-21
- **Analyste** : Houda OUBANE
- **Cible** : DIVA (Damn Insecure and Vulnerable App)
- **Package** : jakhar.aseem.diva (v1.0)
- **Hash SHA256** : a4a2e77291d42e32680475a15710433406578b152e1fa11d9b97189e19ec6103
- **Outils utilisés** : BeVigil (CloudSEK), Yaazhini 2.0.2 (VegaBird Technologies)
- **Environnement** : Windows 11, Java 21, Genymotion

## B. Résumé exécutif
L'analyse statique de l'application DIVA v1.0 a révélé 10 problèmes
de sécurité significatifs. L'application présente des vulnérabilités
critiques liées aux communications non chiffrées, au stockage non
sécurisé des données, et à une configuration Android non sécurisée.
Le niveau de risque global est élevé en raison de la présence d'une
communication HTTP non chiffrée (CVSS 8.1) et de multiples mauvaises
pratiques de développement Android.

Note : DIVA est une application pédagogique volontairement vulnérable
conçue pour la formation en sécurité mobile.

## C. Top 5 constats

### 1. FIND-001 - Insecure Communication
- **Sévérité** : High (CVSS 8.1)
- **Source** : Yaazhini
- **Preuve** : APICreds2Activity.java - HTTP URL en clair
- **Impact** : Interception du trafic réseau (attaque Man-in-the-Middle)
- **Remédiation** : Implémenter SSL/TLS pour toutes les connexions
- **Référence OWASP** : MASVS-NETWORK-1

### 2. FIND-002 - Non-parameterized SQL Query
- **Sévérité** : Medium
- **Source** : BeVigil (confiance 97.1%)
- **Preuve** : sources/jakhar/aseem/diva/SQLInjection
- **Impact** : Injection SQL possible via input utilisateur
- **Remédiation** : Utiliser des requêtes paramétrées (PreparedStatement)
- **Référence OWASP** : MASVS-CODE-4

### 3. FIND-003 - Android Debuggable Enabled
- **Sévérité** : Medium
- **Source** : Yaazhini
- **Preuve** : AndroidManifest.xml - android:debuggable=true
- **Impact** : Accès debug en production, extraction mémoire possible
- **Remédiation** : Désactiver debuggable dans les builds de production
- **Référence OWASP** : MASVS-CODE-2

### 4. FIND-004 - Android Backup Vulnerability
- **Sévérité** : Medium
- **Source** : Yaazhini
- **Preuve** : AndroidManifest.xml - android:allowBackup=true
- **Impact** : Extraction des données applicatives via ADB backup
- **Remédiation** : Désactiver allowBackup dans AndroidManifest.xml
- **Référence OWASP** : MASVS-STORAGE-4

### 5. FIND-005 - Improper Export of Providers
- **Sévérité** : Medium
- **Source** : Yaazhini
- **Preuve** : AndroidManifest.xml - content providers exportés
- **Impact** : Accès non autorisé aux données via content providers
- **Remédiation** : Ajouter android:exported=false
- **Référence OWASP** : MASVS-PLATFORM-2

## D. Faux positifs notables
- Recherche BeVigil par nom 'DIVA' : 46 apps sans rapport détectées
  → Faux positifs car DIVA pédagogique n'est pas sur le Play Store
- FIND-006 Possible Secret Detected (confiance 2.9%) : labels UI
  dans strings.xml qui ressemblent à des credentials
  → A confirmer par analyse manuelle du fichier

## E. Recommandations prioritaires
1. Implémenter immédiatement TLS pour toutes les communications réseau
2. Désactiver android:debuggable=true avant tout déploiement
3. Désactiver android:allowBackup=true pour protéger les données
4. Utiliser des requêtes SQL paramétrées pour éviter les injections
5. Stocker les secrets dans Android Keystore, jamais en dur dans le code

## F. Annexes
- BeVigil notes   : 01-bevigil/bevigil_notes.md
- Yaazhini notes  : 02-yaazhini/yaazhini_notes.md
- Triage complet  : 03-triage/triage.csv
- Mapping OWASP   : 03-triage/owasp_mapping.md
- Scope           : 00-scope/scope.md
- Log commandes   : commands.log
