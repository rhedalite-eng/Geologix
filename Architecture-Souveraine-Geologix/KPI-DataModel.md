Modèle de Données KPI - Géologix
Mission
Ce document définit les structures de données nécessaires au calcul des indicateurs de performance (KPI) de Géologix.

L'objectif est d'assurer une mesure cohérente de la circulation de l'information, de l'utilisation du système et de la valeur produite.

Relations
Ce module est directement lié à :

Observation.md
RapportTerrain.md
Workflow-MVP.md
Vision-IA.md
Tableau-Bord-Efficacite.md
Entité : Observation
Description
Représente une observation terrain initiale.

Observation {
  id: UUID
  createdAt: DateTime

  auteurId: UUID

  titre: string
  description: string

  latitude: number
  longitude: number

  statut: enum

  rapportId?: UUID
}
Entité : Rapport
Description
Rapport consolidé issu d'une ou plusieurs observations.

Rapport {
  id: UUID

  createdAt: DateTime
  transmittedAt?: DateTime
  openedAt?: DateTime

  auteurId: UUID

  titre: string

  statut: enum

  observationCount: number

  clarificationRequested: boolean

  transmissionDelayMinutes: number

  actionCount: number
}
Entité : Action
Description
Action déclenchée suite à l'analyse d'un rapport.

Action {
  id: UUID

  rapportId: UUID

  createdAt: DateTime

  type: enum

  statut: enum

  completedAt?: DateTime

  resultatUtile: boolean
}
Entité : Recommandation IA
Description
Suggestion produite par l'intelligence artificielle.

AIRecommendation {
  id: UUID

  generatedAt: DateTime

  rapportId?: UUID
  observationId?: UUID

  type: enum

  description: string

  confidenceScore: number

  verified: boolean

  useful: boolean

  utilisateurValidationId?: UUID
}
Entité : Corrélation
Correlation {
  id: UUID

  generatedAt: DateTime

  confidenceScore: number

  sourceIds: UUID[]

  accepted: boolean

  commentaire?: string
}
Entité : Anomalie
Anomaly {
  id: UUID

  generatedAt: DateTime

  type: string

  confidenceScore: number

  confirmed: boolean

  commentaire?: string
}
Entité : Contradiction
Contradiction {
  id: UUID

  generatedAt: DateTime

  description: string

  sourceA: UUID
  sourceB: UUID

  confidenceScore: number

  significant: boolean

  verificationRequested: boolean

  verified: boolean
}
Entité : Consultation
Description
Permet de savoir si un rapport a été lu.

ReportView {
  id: UUID

  rapportId: UUID

  utilisateurId: UUID

  viewedAt: DateTime

  durationSeconds: number
}
Entité : KPI Snapshot
Description
Valeurs agrégées calculées périodiquement.

KPISnapshot {
  id: UUID

  generatedAt: DateTime

  periodStart: DateTime
  periodEnd: DateTime

  transmissionRate: number

  readingRate: number

  comprehensionRate: number

  actionRate: number

  impactRate: number

  secondLookRate: number

  aiRelevanceRate: number

  discoveriesCount: number
}
Calculs KPI
Taux de Transmission
transmissionRate =
(transmittedReports / createdReports) * 100
Taux de Lecture
readingRate =
(openedReports / transmittedReports) * 100
Taux de Compréhension
comprehensionRate =
100 -
(
clarificationRequests
/
openedReports
* 100
)
Taux d'Action
actionRate =
(
reportsWithActions
/
openedReports
)
* 100
Taux d'Impact
impactRate =
(
usefulActions
/
triggeredActions
)
* 100
Indice de Second Regard
secondLookRate =
(
verifiedRecommendations
/
generatedRecommendations
)
* 100
Pertinence IA
aiRelevanceRate =
(
usefulRecommendations
/
verifiedRecommendations
)
* 100
KPI Signature Géologix
Choses Qui Auraient Pu Être Manquées
missedThingsCount =
usefulCorrelations
+
confirmedAnomalies
+
significantContradictions
+
recoveredDocuments
+
validatedSecondLooks
Historisation
Aucune valeur KPI ne doit être écrasée.

Tous les calculs doivent être historisés afin de permettre :

analyses mensuelles ;
analyses annuelles ;
comparaison entre projets ;
comparaison entre secteurs ;
évaluation continue du système.
