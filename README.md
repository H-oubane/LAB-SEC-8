# Lab 8  Analyse de Sécurité Mobile — DIVA APK
 
**Analyste** : Houda OUBANE  
**Date** : 2026-05-21  
**Cible** : DIVA (Damn Insecure and Vulnerable App) — jakhar.aseem.diva v1.0  
**Hash SHA256** : a4a2e77291d42e32680475a15710433406578b152e1fa11d9b97189e19ec6103  
**Outils** : BeVigil (CloudSEK) + Yaazhini 2.0.2 (VegaBird Technologies)
 
---
 
## Structure du projet
 
```
lab-mobile-security/
├── 00-scope/
│   ├── application_pedagogique.apk
│   └── scope.md
├── 01-bevigil/
│   └── bevigil_notes.md
├── 02-yaazhini/
│   └── yaazhini_notes.md
├── 03-triage/
│   ├── triage.csv
│   └── owasp_mapping.md
├── 04-report/
│   └── rapport_final.md
├── analyse_info.txt
├── commands.log
└── checklist_fin.md
```
 
---
 
## Phase 0 — Préparation de l'environnement
 
L'environnement de travail a été préparé sur Windows 11 avec :
 
- Java 21 (vérifié via `java -version`)
- Yaazhini 2.0.2 installé (téléchargé depuis vegabird.com)
- Compte BeVigil créé sur bevigil.com
- Structure de dossiers créée sur le Bureau
- Fichiers de traçabilité initialisés (`commands.log`, `analyse_info.txt`)


---

<img width="1277" height="282" alt="image" src="https://github.com/user-attachments/assets/18ff361e-a2d7-4b6c-971d-a389d5fdf010" />

---
 
## Phase 1 — Scope et traçabilité
 
L'APK DIVA a été extrait directement depuis l'émulateur Genymotion via ADB :
 
```
adb shell pm path jakhar.aseem.diva
adb pull /data/app/jakhar.aseem.diva-.../base.apk application_pedagogique.apk
```
 
Le hash SHA256 a été calculé avec `certutil` pour garantir l'intégrité de l'artefact.
 
**Informations APK :**
- Package : jakhar.aseem.diva
- Version : 1.0
- Taille : 1.54 MB
- Min SDK : 15 / Target SDK : 29


---

<img width="1467" height="102" alt="image" src="https://github.com/user-attachments/assets/e940a485-14a3-4177-b45f-ace74ce5952f" />

---

<img width="922" height="106" alt="image" src="https://github.com/user-attachments/assets/1cc6cc44-8cc0-4c51-a7f7-083d5cecaba7" />

---

<img width="1407" height="135" alt="image" src="https://github.com/user-attachments/assets/3e5163a5-a05b-4d23-9f00-4d1a98c9ee75" />

---

 
## Phase 2 — Analyse BeVigil
 
L'APK a été uploadé directement sur BeVigil via la fonctionnalité "Scan App > Option 2 (APK non publié)".
 
**Security Rating obtenu : 8.2 / 10 (Good)**
 
### Findings BeVigil
 
| ID | Finding | Sévérité | Localisation |
|---|---|---|---|
| FIND-BV-001 | Non-parameterized SQL Query | Medium | SQLInjection.java |
| FIND-BV-002 | Possible Secret Detected | Low | res/values/strings.xml |
| FIND-BV-003 | File Path Exposure (CWE-200) | Low | InsecureDataStorage |
| FIND-BV-004 | URL Exposure (CWE-200) | Low | Assets |
| FIND-BV-005 | READ_EXTERNAL_STORAGE | Risky | AndroidManifest.xml |
 
**Secrets détectés dans strings.xml :**
- Tveeter API Credentials
- Vendor API Credentials
- 3rd party service password

---

<img width="1600" height="798" alt="image" src="https://github.com/user-attachments/assets/8a6ac23d-0dc6-4815-b52b-cd27f42d4dd9" />

---

<img width="1600" height="754" alt="image" src="https://github.com/user-attachments/assets/08f26075-4df9-4b41-ba7e-3418e9ab373f" />

---

<img width="1600" height="807" alt="image" src="https://github.com/user-attachments/assets/824e8bd8-19c0-456f-b2b6-0a6b170a5a91" />

---

<img width="1600" height="776" alt="image" src="https://github.com/user-attachments/assets/d632c1b2-f397-428f-92fe-511d6891905d" />

---

<img width="1600" height="790" alt="image" src="https://github.com/user-attachments/assets/e9906e94-f077-4df0-bd1f-b0ea12d43d5c" />

---

 <img width="1600" height="748" alt="image" src="https://github.com/user-attachments/assets/d6d84511-ba3b-4fd0-915c-cc3178189b47" />

---

 
## Phase 3 — Analyse Yaazhini
 
L'APK a été chargé dans Yaazhini (Project : DIVA_Lab) et analysé via "Upload & Scan".
 
### Résumé des vulnérabilités détectées
 
| Niveau | Nombre |
|---|---|
| High | 1 |
| Medium | 3 |
| Low | 1 |
| Warning | 9 |
| Information | 51 |
 
### Findings Yaazhini
 
| ID | Finding | Sévérité | CVSS | Fichier |
|---|---|---|---|---|
| FIND-YZ-001 | Insecure Communication | High | 8.1 | APICreds2Activity.java |
| FIND-YZ-002 | Android Debuggable Enabled | Medium | — | AndroidManifest.xml |
| FIND-YZ-003 | Android Backup Vulnerability | Medium | — | AndroidManifest.xml |
| FIND-YZ-004 | Improper Export of Providers | Medium | — | AndroidManifest.xml |
| FIND-YZ-005 | Javascript Enabled in WebView | Low | — | WebView config |
| FIND-YZ-006 | Android External Storage | Warning | — | 9 occurrences |
 
**Activities sensibles identifiées :**
- HardcodeActivity
- InsecureDataStorage1/2/3/4Activity
- SQLInjectionActivity
- AccessControl1/2Activity
- APICredsActivity

---

<img width="1127" height="742" alt="image" src="https://github.com/user-attachments/assets/0decf831-25a2-4f55-ac8b-5cd0c706d367" />

---

<img width="1600" height="848" alt="image" src="https://github.com/user-attachments/assets/1a430e15-a315-4b00-adcd-b2b983f2ced6" />

---

<img width="1600" height="744" alt="image" src="https://github.com/user-attachments/assets/fc30513c-e282-4577-ac18-7502bdbeb6b8" />

---

<img width="1600" height="598" alt="image" src="https://github.com/user-attachments/assets/42a08f3e-db58-413f-af92-812dc412fe1d" />

---

<img width="1600" height="832" alt="image" src="https://github.com/user-attachments/assets/7a167035-fa45-4f95-ba92-90eeb2dc1ae1" />

---

<img width="1600" height="343" alt="image" src="https://github.com/user-attachments/assets/9f985c8c-aa3a-4800-9e80-f52e3afde52d" />


---
 
## Phase 4 — Triage et mapping OWASP
 
L'ensemble des findings a été consolidé dans `triage.csv` (10 entrées) et mappé aux catégories OWASP MASVS dans `owasp_mapping.md`.
 
### Vue consolidée
 
| ID | Source | Finding | Sévérité | OWASP |
|---|---|---|---|---|
| FIND-001 | Yaazhini | Insecure Communication | High | MASVS-NETWORK-1 |
| FIND-002 | BeVigil | SQL Query non paramétrée | Medium | MASVS-CODE-4 |
| FIND-003 | Yaazhini | Debuggable Enabled | Medium | MASVS-CODE-2 |
| FIND-004 | Yaazhini | Backup Vulnerability | Medium | MASVS-STORAGE-4 |
| FIND-005 | Yaazhini | Export of Providers | Medium | MASVS-PLATFORM-2 |
| FIND-006 | BeVigil | Secret Detected | Low | MASVS-STORAGE-1 |
| FIND-007 | Yaazhini | JS in WebView | Low | MASVS-PLATFORM-1 |
| FIND-008 | BeVigil | File Path Exposure | Low | MASVS-STORAGE-2 |
| FIND-009 | Yaazhini | External Storage | Warning | MASVS-STORAGE-2 |
| FIND-010 | BeVigil | Permission READ_STORAGE | Warning | MASVS-STORAGE-2 |
 
**Faux positifs documentés :**
- Recherche BeVigil "DIVA" : 46 apps sans rapport (DIVA non publiée sur Play Store)
- FIND-006 confiance 2.9% : labels UI dans strings.xml ressemblant à des credentials
 
---
 
## Phase 5 — Rapport final
 
Le rapport final a été rédigé dans `04-report/rapport_final.md` avec les sections :
 
- A. Informations générales
- B. Résumé exécutif
- C. Top 5 constats détaillés
- D. Faux positifs notables
- E. Recommandations prioritaires
- F. Annexes
### Recommandations prioritaires
 
1. Implémenter TLS pour toutes les communications réseau
2. Désactiver `android:debuggable=true` avant tout déploiement
3. Désactiver `android:allowBackup=true` pour protéger les données
4. Utiliser des requêtes SQL paramétrées
5. Stocker les secrets dans Android Keystore

---

<img width="972" height="737" alt="image" src="https://github.com/user-attachments/assets/b539baf6-ace9-4872-846e-56683a8c1a69" />

---
 
## Phase 6 — Clôture
 
La checklist de fin a été complétée et signée dans `checklist_fin.md`.
 
**Statut de conformité MASVS :**
 
| Catégorie | Statut |
|---|---|
| MASVS-NETWORK-1 | Non conforme |
| MASVS-CODE-2 | Non conforme |
| MASVS-CODE-4 | Non conforme |
| MASVS-STORAGE-1 | Non conforme |
| MASVS-STORAGE-2 | Non conforme |
| MASVS-STORAGE-4 | Non conforme |
| MASVS-PLATFORM-1 | Non conforme |
| MASVS-PLATFORM-2 | Non conforme |
 

---

<img width="1455" height="486" alt="image" src="https://github.com/user-attachments/assets/051cd912-5604-4163-9495-b8f6cc7b18fa" />

---
 
## Limitations
 
- Export de rapport Yaazhini non disponible en v2.0.2 — résultats documentés manuellement
- DIVA non indexée sur BeVigil via recherche par nom — analysée via upload direct
---


## Auteur
**H-oubane**




*Analyse réalisée dans un cadre pédagogique sur une application volontairement vulnérable. Aucune exploitation réelle n'a été effectuée.*
