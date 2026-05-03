-- E-Commerce Infrastructure Project DB
CREATE TABLE phases (
    phase_id     INT PRIMARY KEY,
    phase_name   VARCHAR(100) NOT NULL,
    start_date   DATE,
    end_date     DATE,
    duration_days INT,
    resources    VARCHAR(200)
);

CREATE TABLE tasks (
    task_id      INT PRIMARY KEY,
    phase_id     INT REFERENCES phases(phase_id),
    task_name    VARCHAR(200) NOT NULL,
    duration     VARCHAR(20),
    start_date   DATE,
    finish_date  DATE,
    predecessor  INT REFERENCES tasks(task_id),
    is_milestone BOOLEAN DEFAULT FALSE,
    resource     VARCHAR(100)
);

CREATE TABLE task_progress (
    progress_id  SERIAL PRIMARY KEY,
    task_id      INT REFERENCES tasks(task_id),
    pct_complete DECIMAL(5,2) DEFAULT 0,
    updated_at   TIMESTAMP DEFAULT NOW(),
    notes        TEXT
);
