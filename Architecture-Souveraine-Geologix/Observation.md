Observation
Définition
Une Observation constitue l'unité fondamentale d'information du RapportTerrain.

Elle représente un fait observé, mesuré, documenté ou signalé par un utilisateur terrain.

Les observations alimentent directement les rapports logistiques générés par Géologix.

Mission
Capturer une information terrain significative sous une forme structurée afin de faciliter :

l'analyse
la validation
la détection d'erreurs
la génération automatisée de rapports
Chaque observation constitue une pièce d'information pouvant être exploitée individuellement ou regroupée dans un RapportTerrain.

Rôle dans le MVP
Une ou plusieurs observations peuvent être regroupées à l'intérieur d'un RapportTerrain.

Les observations servent de matière première aux fonctions suivantes :

extraction de données
validation de cohérence
détection d'erreurs
génération de rapports PDF
analyse IA
Champs obligatoires
Identifiant unique
Identifiant généré automatiquement par Géologix.

Exemple :

OBS-000001
OBS-000002
OBS-000003
Type d'observation
Permet de classifier l'information.

Exemples :

Affleurement
Structure
Échantillon
Minéralisation
Anomalie
Forage
Observation documentaire
Observation cartographique
Description
Description factuelle de l'observation.

Exemple :

Présence de sulfures disséminés dans un schiste noir fortement fracturé.

Date
Date de l'observation.

Par défaut : date courante.

Auteur
Utilisateur ayant créé l'observation.

Attribué automatiquement par Géologix.

Statut
État actuel de l'observation.

Valeurs autorisées :

Brouillon
Validée
Archivée
Champs optionnels
Coordonnées
Latitude
Longitude
Altitude
Médias associés
Photographies
Audio
Vidéo
Croquis
Documents associés
PDF
Rapports
Cartes
Tableaux
Résultats d'analyse
Conditions terrain
Météo
Température
Conditions particulières
Mesures
Toute mesure pertinente observée sur le terrain :

distance
profondeur
orientation
volume
dimension
valeur instrumentale
Types d'observation
Terrain
Affleurement
Structure géologique
Minéralisation
Échantillon
Forage
Tranchée
Documentaire
Rapport historique
Étude scientifique
Archive
Document gouvernemental
Cartographique
Carte géologique
Imagerie satellite
Donnée géophysique
Analytique
Corrélation
Modélisation
Anomalie détectée
Hypothèses
L'utilisateur peut associer une ou plusieurs hypothèses à une observation.

Les hypothèses demeurent distinctes des faits observés.

Exemple :

Observation
Présence de sulfures dans un schiste noir.

Hypothèse
Présence possible d'un corridor minéralisé.

Corrélations IA
L'IA peut relier plusieurs observations entre elles afin d'identifier :

similitudes
tendances
incohérences
anomalies potentielles
Les corrélations demeurent consultatives et ne remplacent jamais le jugement professionnel.

Relation avec le RapportTerrain
Une Observation peut exister seule ou être intégrée dans un RapportTerrain.

Un RapportTerrain peut contenir :

une seule observation
plusieurs observations
plusieurs types d'observations
Le RapportTerrain constitue l'unité opérationnelle utilisée pour la génération des rapports logistiques.

Règles de validation
Validation minimale
Une Observation ne peut être enregistrée que si les informations suivantes sont présentes :

Identifiant unique
Type d'observation
Description
Date
Auteur
Statut
Description
La description doit contenir au moins une information significative.

Non autorisé :

champ vide
espace uniquement
contenu généré automatiquement sans validation humaine
Date
La date doit être valide.

La date ne peut pas être absente.

Auteur
Chaque observation doit être associée à un utilisateur identifié.

L'attribution est réalisée automatiquement par Géologix.

Statut
Le statut doit appartenir à l'une des valeurs reconnues :

Brouillon
Validée
Archivée
Médias
Les médias sont facultatifs.

Toutefois :

les fichiers doivent être lisibles
les formats doivent être supportés
les fichiers corrompus doivent être rejetés
Coordonnées
Les coordonnées GPS sont facultatives.

Si elles sont présentes :

latitude valide
longitude valide
Documents joints
Les documents doivent posséder :

un format accepté
un fichier complet
une taille compatible avec les limites du système
Hypothèses
Les hypothèses doivent demeurer distinctes des observations factuelles.

Analyse IA
L'IA ne peut jamais modifier une observation originale.

Les résultats produits par l'IA sont enregistrés séparément.

L'observation originale demeure conservée.

Traçabilité
Toute modification doit enregistrer :

l'auteur
la date
la modification effectuée
Aucune donnée ne doit être supprimée sans laisser une trace dans l'historique.

Principe directeur
Une observation valide doit pouvoir être comprise et vérifiée par un autre professionnel sans information supplémentaire provenant de son auteur.

Philosophie Géologix
Une observation décrit ce qui est observé.

L'interprétation vient ensuite.

Géologix favorise la séparation entre :

les faits observés
les hypothèses humaines
les suggestions produites par l'IA
afin de préserver la traçabilité, la transparence et la qualité de l'information.
