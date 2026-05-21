# BeVigil - Notes d'analyse

## Cible recherchée
- Package : jakhar.aseem.diva
- Nom : DIVA (Damn Insecure and Vulnerable App)

## Résultat de la recherche
- Statut : Found 0 Apps
- Raison : Application pédagogique locale, non publiée sur le Play Store
- BeVigil indexe uniquement les apps publiques du Google Play Store

## Recherches alternatives tentées
- jakhar.aseem.diva → 0 résultats
- DIVA android → 0 résultats

## Conclusion
DIVA n'étant pas indexée par BeVigil, l'analyse BeVigil
ne peut pas être réalisée sur cette cible.
L'analyse sera concentrée sur Yaazhini (analyse statique locale).

## Référence document lab
ISSUE: BeVigil search returned no results for jakhar.aseem.diva

## Recherche 'DIVA' (nom générique)
- Résultat : 46 apps trouvées
- Toutes sans rapport avec jakhar.aseem.diva
- Faux positifs : apps commerciales contenant 'DIVA' dans leur nom
- Ex: 'Gossip Girls Divas Highschool' (air.com.bmapps...) - non pertinent
- Conclusion : aucun résultat exploitable via recherche par nom

## Résultats Vulnerabilities
- Security Rating : 8.2 / 10 (Good)
- Total issues : 2

### FIND-BV-001 : Non-parameterized SQL Query
- Sévérité : Medium
- Confiance : 97.1%
- Localisation : sources/jakhar/aseem/diva/SQLInjection...
- Référence OWASP : MASVS-CODE-4

### FIND-BV-002 : Possible Secret Detected
- Sévérité : Low
- Confiance : 2.9%
- Localisation : resources/res/values/strings.xml
- Référence OWASP : MASVS-STORAGE-1

## Strings - Associated Files (3 matches)
- Fichier : resources/res/values/strings.xml
  - Match 1 : apic2_label > Tveeter API Credentials
  - Match 2 : apic_label > Vendor API Credentials
  - Match 3 : ids1_password > Enter 3rd party service password
- Analyse : credentials hardcodes dans strings.xml
- Risque : decouvrable par reverse engineering

## Assets - Findings
### File Path - CWE-200
- Type : File Path Exposure
- CWE : CWE-200 (Information Exposure)
- Risque : Revele la structure interne de l'application
- Localisation : sources/jakhar/aseem/diva/InsecureDat...
- Référence OWASP : MASVS-STORAGE-2

### URL - CWE-200
- Type : URL Exposure
- CWE : CWE-200 (Information Exposure)
- Risque : URLs contenant des parametres sensibles
- Impact : Fuite d'informations, acces non autorise
- Référence OWASP : MASVS-NETWORK-1

## APKiD
- Fichier : classes.dex
- Compilateur : r8 (Google R8 compiler/shrinker)
- Analyse : app compilée avec R8, obfuscation possible
- Note : R8 est le compilateur standard Android, pas de packer malveillant détecté

## Malware
- Résultat : Aucun malware détecté
- Statut : Clean

## Permissions
### android.permission.READ_EXTERNAL_STORAGE - RISKY
- Niveau : RISKY
- API ajoutée : 16
- Description : Permet la lecture du stockage externe
- Risque : Acces aux fichiers utilisateur sur la carte SD
- Référence OWASP : MASVS-STORAGE-2
