# Job search profile

This example is filled in for a fictional person.
Copy it outside the skill folder, replace every line with your own, and tell your agent where it is.
Raise the version whenever you change a fact or a rule, so earlier decisions keep the version they used.
Leave a line blank rather than guessing; your agent asks when a blank line decides eligibility.

Version: 3
Updated: 2026-11-07
Timezone: America/Los_Angeles

## Confirmed facts

- Name: Alex Rivera
- Education: B.S. Computer Science, Coastal State University, graduated June 2026
- Enrollment: not enrolled
- Experience: one backend internship (summer 2025, 12 weeks); a capstone that ran Go services in production for a campus app
- Work authorization: U.S. citizen, no sponsorship needed
- Location: lives in Portland, OR; would move to Seattle or the San Francisco Bay Area
- Availability: can start any time

## Resumes

- `resume-backend.pdf`: backend, platform, and infrastructure roles
- `resume-ml.pdf`: machine learning engineering roles

## Preferences

- Roles: backend engineer, platform engineer, machine learning engineer
- Seniority: new grad or entry level; skip roles asking for more than two years
- Locations and work mode: Seattle, Bay Area, Portland, or remote in the U.S.; hybrid is fine
- Industries to avoid: gambling, defense
- Companies to watch: Kestrel AI, Lumen Robotics, Summit Logistics
- Minimum compensation: $110,000 base

## Rules for your agent

These override the skill's defaults, because current user instructions take precedence.

- Application forms: draft answers only, and I submit
- Compensation questions: ask me each time
- Notify me about updates to a job already recommended: no

## Sources

Needed only for discovery and scheduled runs.
Set a fetch budget for each source family, because one slow family can use up a shared budget.

| Source | Family | Fetch budget per run |
| --- | --- | --- |
| Kestrel AI careers | Greenhouse | 40 postings |
| Lumen Robotics careers | Lever | 40 postings |
| Summit Logistics careers | Workday | 60 postings |
| A public new-grad job list | Index, for discovery only | 100 rows |

- Observation window: last 7 days
- Job history: a spreadsheet at `~/job-search/history.xlsx`, one row per recommended job
- Delivery: a daily email to myself, only when something qualifies
