API Specifications - GeoLogix
Mission
Définir les interfaces permettant aux différents composants de GeoLogix de communiquer entre eux.

Les API doivent supporter :

les observations ;
les rapports ;
les documents ;
les analyses IA ;
les KPI ;
la traçabilité ;
la conservation ;
les intégrations externes.
Principes
API First
Toute fonctionnalité métier doit pouvoir être utilisée :

depuis l'interface utilisateur ;
depuis une application externe ;
depuis un moteur IA ;
depuis un processus automatisé.
Traçabilité
Toute opération doit produire un événement métier.

Versionnement
Les API doivent supporter :

/api/v1/
/api/v2/
Module Observation API
Créer une observation
POST /api/v1/observations
Payload
{ "title": "Affleurement Nord", "description": "...", "latitude": 48.85, "longitude": -67.53 }

Obtenir une observation
GET /api/v1/observations/{id}
Modifier une observation
PUT /api/v1/observations/{id}
Archiver une observation
POST /api/v1/observations/{id}/archive
Module Rapport API
Créer un rapport
POST /api/v1/reports
Ajouter une observation
POST /api/v1/reports/{id}/observations
Générer un PDF
POST /api/v1/reports/{id}/pdf
Signer un rapport
POST /api/v1/reports/{id}/sign
Obtenir l'historique
GET /api/v1/reports/{id}/history
Module Documents
Téléverser un document
POST /api/v1/documents
Formats :

PDF
JPG
PNG
DOCX
XLSX
Audio
OCR
POST /api/v1/documents/{id}/ocr
Transcription Audio
POST /api/v1/documents/{id}/transcribe
Module IA
Résumé
POST /api/v1/ai/summarize
Corrélations
POST /api/v1/ai/correlations
Recherche Contextuelle
POST /api/v1/ai/context-search
Détection d'Anomalies
POST /api/v1/ai/anomalies
Contradictions
POST /api/v1/ai/contradictions
Recommandations
POST /api/v1/ai/recommendations
Module Validation
Signature unique
POST /api/v1/validation/sign
Double signature
POST /api/v1/validation/double-sign
Triple signature
POST /api/v1/validation/triple-sign
Module KPI
KPI Globaux
GET /api/v1/kpi/global
Retour :

{ "transmissionRate": 97, "readingRate": 92, "actionRate": 43 }

KPI IA
GET /api/v1/kpi/ai
Choses qui auraient pu être manquées
GET /api/v1/kpi/missed-things
Module Conservation
Politique active
GET /api/v1/retention-policy
Modifier une politique
PUT /api/v1/retention-policy
Archiver une ressource
POST /api/v1/archive
Anonymiser
POST /api/v1/anonymize
Module Audit
Consulter les événements
GET /api/v1/events
