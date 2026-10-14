-- =====================================================
-- ENUMS
-- =====================================================

CREATE TYPE observation_status AS ENUM (
    'draft',
    'submitted',
    'archived'
);

CREATE TYPE report_status AS ENUM (
    'draft',
    'transmitted',
    'opened',
    'reviewed',
    'closed'
);

CREATE TYPE action_status AS ENUM (
    'pending',
    'in_progress',
    'completed',
    'cancelled'
);

CREATE TYPE action_type AS ENUM (
    'field_verification',
    'sampling',
    'lab_analysis',
    'mapping_revision',
    'expert_review',
    'follow_up'
);

CREATE TYPE recommendation_type AS ENUM (
    'correlation',
    'anomaly',
    'contradiction',
    'verification',
    'sampling',
    'review'
);

-- =====================================================
-- OBSERVATIONS
-- =====================================================

CREATE TABLE observations (

    id UUID PRIMARY KEY,

    created_at TIMESTAMP NOT NULL,

    created_by UUID NOT NULL,

    title TEXT NOT NULL,

    description TEXT,

    latitude NUMERIC(10,6),

    longitude NUMERIC(10,6),

    status observation_status
        DEFAULT 'draft'
);

-- =====================================================
-- REPORTS
-- =====================================================

CREATE TABLE reports (

    id UUID PRIMARY KEY,

    created_at TIMESTAMP NOT NULL,

    transmitted_at TIMESTAMP,

    opened_at TIMESTAMP,

    created_by UUID NOT NULL,

    title TEXT NOT NULL,

    status report_status
        DEFAULT 'draft',

    clarification_requested BOOLEAN
        DEFAULT FALSE
);

-- =====================================================
-- OBSERVATION REPORT LINK
-- =====================================================

CREATE TABLE report_observations (

    report_id UUID REFERENCES reports(id)
        ON DELETE CASCADE,

    observation_id UUID REFERENCES observations(id)
        ON DELETE CASCADE,

    PRIMARY KEY (
        report_id,
        observation_id
    )
);

-- =====================================================
-- ACTIONS
-- =====================================================

CREATE TABLE actions (

    id UUID PRIMARY KEY,

    report_id UUID REFERENCES reports(id),

    created_at TIMESTAMP NOT NULL,

    completed_at TIMESTAMP,

    type action_type NOT NULL,

    status action_status
        DEFAULT 'pending',

    useful_result BOOLEAN
        DEFAULT FALSE,

    notes TEXT
);

-- =====================================================
-- IA RECOMMENDATIONS
-- =====================================================

CREATE TABLE ai_recommendations (

    id UUID PRIMARY KEY,

    generated_at TIMESTAMP NOT NULL,

    report_id UUID REFERENCES reports(id),

    type recommendation_type NOT NULL,

    description TEXT NOT NULL,

    confidence_score NUMERIC(5,2),

    verified BOOLEAN DEFAULT FALSE,

    useful BOOLEAN DEFAULT FALSE
);

-- =====================================================
-- CORRELATIONS
-- =====================================================

CREATE TABLE correlations (

    id UUID PRIMARY KEY,

    generated_at TIMESTAMP NOT NULL,

    confidence_score NUMERIC(5,2),

    accepted BOOLEAN DEFAULT FALSE,

    notes TEXT
);

-- =====================================================
-- ANOMALIES
-- =====================================================

CREATE TABLE anomalies (

    id UUID PRIMARY KEY,

    generated_at TIMESTAMP NOT NULL,

    anomaly_type TEXT,

    confidence_score NUMERIC(5,2),

    confirmed BOOLEAN DEFAULT FALSE
);

-- =====================================================
-- CONTRADICTIONS
-- =====================================================

CREATE TABLE contradictions (

    id UUID PRIMARY KEY,

    generated_at TIMESTAMP NOT NULL,

    description TEXT NOT NULL,

    confidence_score NUMERIC(5,2),

    significant BOOLEAN DEFAULT FALSE,

    verification_requested BOOLEAN DEFAULT FALSE,

    verified BOOLEAN DEFAULT FALSE
);

-- =====================================================
-- REPORT VIEWS
-- =====================================================

CREATE TABLE report_views (

    id UUID PRIMARY KEY,

    report_id UUID NOT NULL
        REFERENCES reports(id),

    viewed_by UUID NOT NULL,

    viewed_at TIMESTAMP NOT NULL,

    duration_seconds INTEGER
        CHECK (duration_seconds >= 0)
);

-- =====================================================
-- KPI SNAPSHOTS
-- =====================================================

CREATE TABLE kpi_snapshots (

    id UUID PRIMARY KEY,

    generated_at TIMESTAMP NOT NULL,

    period_start TIMESTAMP NOT NULL,

    period_end TIMESTAMP NOT NULL,

    transmission_rate NUMERIC(5,2),

    reading_rate NUMERIC(5,2),

    comprehension_rate NUMERIC(5,2),

    action_rate NUMERIC(5,2),

    impact_rate NUMERIC(5,2),

    second_look_rate NUMERIC(5,2),

    ai_relevance_rate NUMERIC(5,2),

    missed_things_count INTEGER
);
