Workflow MVP
Statut
Version 1.0

Alignée sur le MVP actuel :

Logistics Report AI

Mission
Transformer des informations terrain non structurées en rapports logistiques standardisés, validés et exploitables.

Le MVP actuel est conçu pour réduire le temps consacré à la rédaction administrative tout en améliorant la qualité et la cohérence des rapports.

Principe fondamental
L'utilisateur fournit les informations.

Géologix les organise.

L'IA les analyse.

L'utilisateur conserve la décision finale.

Flux opérationnel
Étape 1 - Collecte terrain
L'utilisateur collecte les informations disponibles.

Exemples :

notes de terrain
photographies
coordonnées GPS
météo
mesures
documents
fichiers audio
Étape 2 - Création des Observations
L'utilisateur transforme les informations collectées en Observations.

Chaque Observation doit contenir :

un type
une description
une date
un auteur
Les médias et documents peuvent être ajoutés au besoin.

Résultat :

Une ou plusieurs Observations validées.

Étape 3 - Construction du RapportTerrain
Les Observations sont regroupées à l'intérieur d'un RapportTerrain.

Le RapportTerrain devient le conteneur principal du dossier terrain.

Il peut contenir :

plusieurs observations
plusieurs photos
plusieurs documents
plusieurs pièces jointes
Résultat :

Un dossier terrain complet.

Étape 4 - Validation automatique
Avant l'analyse IA, Géologix exécute les règles de validation.

Contrôles :

champs obligatoires
cohérence des données
fichiers joints
coordonnées GPS
doublons potentiels
Les codes d'erreur MVP sont utilisés pour signaler les problèmes.

Résultat :

Rapport valide ou liste d'erreurs à corriger.

Étape 5 - Analyse IA
L'IA analyse les informations disponibles.

Fonctions MVP :

OCR
transcription audio
extraction de données
structuration du contenu
validation de cohérence
détection d'erreurs
Résultat :

Données enrichies et organisées.

Étape 6 - Génération automatique
L'IA produit un rapport logistique standardisé.

Le rapport contient :

résumé terrain
observations
médias associés
informations extraites
données structurées
Résultat :

Rapport prêt à être partagé.

Étape 7 - Révision humaine
L'utilisateur vérifie :

l'exactitude
la cohérence
les corrections proposées
L'IA ne peut jamais publier ou valider un rapport seule.

Résultat :

Rapport approuvé par un humain.

Étape 8 - Exportation
Formats prévus :

PDF
archivage interne
partage opérationnel
Le PDF constitue actuellement la sortie principale du MVP.

Rôle de l'IA
L'IA agit comme un assistant.

Elle peut :

analyser
résumer
structurer
signaler
Elle ne peut pas :

approuver
certifier
confirmer une interprétation
remplacer l'utilisateur
Architecture logique
Observation ↓ Validation ↓ RapportTerrain ↓ Analyse IA ↓ Rapport logistique ↓ Validation humaine ↓ PDF

Évolutions futures
SampleTrack AI
Ajoutera :

suivi des échantillons
chaîne de possession
géolocalisation avancée
suivi transport-laboratoire
Safety & Incident AI
Ajoutera :

gestion des incidents
analyse des risques
conformité
archivage réglementaire
Vision à long terme
Le MVP actuel automatise la production des rapports.

Les futures versions de Géologix

États du workflow
Observation
Brouillon
Observation créée mais non validée.

Transition possible :

Brouillon → Validée

Brouillon → Rejetée

Validée
Observation conforme aux règles de validation.

Transition possible :

Validée → Archivée

Validée → Brouillon (révision)

Rejetée
Observation ne respectant pas les règles minimales.

Corrections requises avant réintégration.

Archivée
Observation conservée à des fins de référence.

Aucune modification directe autorisée.

RapportTerrain
En préparation
Le rapport est en cours de construction.

Des observations peuvent encore être ajoutées.

Validation
Vérification automatique des données.

Détection :

erreurs
doublons
incohérences
Analyse IA
Traitement des données :

extraction
OCR
transcription
enrichissement
À réviser
Le rapport attend une validation humaine.

Approuvé
Le responsable confirme le contenu.

Exporté
Le rapport a été généré.

Exemple :

PDF

Archivé
Le rapport devient consultable mais non modifiable.

Entrées et sorties
Étape 1 - Collecte terrain
Entrées
Notes terrain
Photos
Audio
Coordonnées GPS
Mesures
Documents
Sorties
Informations brutes
Étape 2 - Création Observation
Entrées
Informations brutes
Sorties
Observation valide
Observation rejetée
Étape 3 - Construction RapportTerrain
Entrées
Observations validées
Sorties
RapportTerrain
Étape 4 - Validation
Entrées
RapportTerrain
Sorties
Rapport valide
Liste d'erreurs MVP
Étape 5 - Analyse IA
Entrées
Rapport valide
Observations
Médias
Documents
Sorties
Données structurées
Résumés
Suggestions
Alertes
Étape 6 - Révision humaine
Entrées
Rapport enrichi
Sorties
Rapport approuvé
Rapport retourné en correction
Étape 7 - Exportation
Entrées
Rapport approuvé
Sorties
PDF
Archive
Diagramme Mermaid
flowchart TD

A[Collecte terrain]

A --> B[Création Observation]

B --> C{Validation Observation}

C -->|Valide| D[RapportTerrain]

C -->|Erreur| E[Correction]

E --> B

D --> F[Validation Rapport]

F --> G[Analyse IA]

G --> H[Révision humaine]

H -->|Approuvé| I[Export PDF]

H -->|Correction| D

I --> J[Archivage]
Principe directeur
Aucun rapport ne peut être exporté sans validation humaine.

L'IA peut assister le processus.

L'utilisateur demeure responsable de l'approbation finale.

Gestion des erreurs
Les contrôles de validation utilisent les codes d'erreur définis dans Observation.md.

Erreurs bloquantes
Les erreurs suivantes empêchent la progression du workflow :

ER-001 Type d'observation manquant
ER-002 Description manquante
ER-004 Date invalide
ER-005 Auteur non identifié
ER-006 Statut invalide
ER-015 Observation non conforme
Résultat :

L'observation retourne à l'état Brouillon.

Erreurs mineures
Les erreurs suivantes autorisent la poursuite du processus mais génèrent un avertissement :

ER-007 Coordonnées GPS invalides
ER-008 Média corrompu
ER-009 Format non supporté
ER-010 Document incomplet
ER-011 Observation dupliquée
ER-013 Incohérence détectée
ER-014 Données insuffisantes
Résultat :

Création d'un avertissement et demande de vérification humaine.
