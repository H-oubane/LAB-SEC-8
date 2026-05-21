# Mapping OWASP MASVS

## MASVS-NETWORK-1 : Communications sécurisées
- FIND-001 : Insecure Communication (High - CVSS 8.1)
- Exigence : Toutes les communications doivent utiliser TLS
- Statut app : NON CONFORME

## MASVS-CODE-4 : Prévention des injections
- FIND-002 : Non-parameterized SQL Query (Medium)
- Exigence : Utiliser des requêtes paramétrées
- Statut app : NON CONFORME

## MASVS-CODE-2 : Configuration de build
- FIND-003 : Android Debuggable Enabled (Medium)
- Exigence : Désactiver le mode debug en production
- Statut app : NON CONFORME

## MASVS-STORAGE-4 : Backup
- FIND-004 : Android Backup Vulnerability (Medium)
- Exigence : Désactiver allowBackup ou chiffrer les données
- Statut app : NON CONFORME

## MASVS-PLATFORM-2 : Export de composants
- FIND-005 : Improper Export of Providers (Medium)
- Exigence : Restreindre l'accès aux content providers
- Statut app : NON CONFORME

## MASVS-STORAGE-1 : Stockage des secrets
- FIND-006 : Possible Secret Detected (Low)
- Exigence : Ne jamais hardcoder les credentials
- Statut app : NON CONFORME

## MASVS-PLATFORM-1 : WebView
- FIND-007 : Javascript Enabled in WebView (Low)
- Exigence : Désactiver JS si non nécessaire
- Statut app : NON CONFORME

## MASVS-STORAGE-2 : Stockage externe
- FIND-008 : File Path Exposure (Low)
- FIND-009 : Android External Storage (Warning)
- FIND-010 : READ_EXTERNAL_STORAGE (Warning)
- Exigence : Protéger les données sur stockage externe
- Statut app : NON CONFORME
