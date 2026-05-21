# Yaazhini - Notes d'analyse

## App Summary
- Package : jakhar.aseem.diva
- Version : 1.0
- Min SDK : 15 / Target SDK : 29
- Taille : 1.5 MB
- Date scan : 21-MAY-2026

## Vulnerabilities

### FIND-YZ-001 - HIGH - Insecure Communication
- Fichier : jakhar/aseem/diva/APICreds2Activity.java
- CVSS : 8.1
- Detail : HTTP URL detectee dans le code source
- Remédiation : Implémenter SSL/TLS pour toutes les connexions
- Référence OWASP : MASVS-NETWORK-1

### FIND-YZ-002 - MEDIUM - Android Debuggable Enabled
- Fichier : AndroidManifest.xml
- Detail : android:debuggable=true active en production
- Remédiation : Desactiver debuggable dans les builds de production
- Référence OWASP : MASVS-CODE-2

### FIND-YZ-003 - MEDIUM - Android Backup Vulnerability
- Fichier : AndroidManifest.xml
- Detail : android:allowBackup=true permet extraction des donnees
- Remédiation : Desactiver allowBackup dans AndroidManifest.xml
- Référence OWASP : MASVS-STORAGE-4

### FIND-YZ-004 - MEDIUM - Improper Export of Providers
- Fichier : AndroidManifest.xml
- Detail : Content providers exportes sans protection
- Remédiation : Ajouter android:exported=false ou permission requise
- Référence OWASP : MASVS-PLATFORM-2

### FIND-YZ-005 - LOW - Javascript Enabled in WebView
- Detail : JavaScript active dans WebView
- Remédiation : Desactiver JS si non necessaire
- Référence OWASP : MASVS-PLATFORM-1

### FIND-YZ-006 - WARNING - Android External Storage (9 occurrences)
- Detail : Donnees ecrites sur stockage externe non protege
- Remédiation : Utiliser le stockage interne chiffre
- Référence OWASP : MASVS-STORAGE-2

## Permissions
- WRITE_EXTERNAL_STORAGE
- READ_EXTERNAL_STORAGE
- INTERNET

## Activities sensibles
- HardcodeActivity
- InsecureDataStorage1/2/3/4Activity
- SQLInjectionActivity
- AccessControl1/2Activity
- APICredsActivity

## Limitation
- Export de rapport non disponible dans Yaazhini 2.0.2
- Résultats documentés manuellement + captures d'écran
