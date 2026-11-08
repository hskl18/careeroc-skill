# Example output

The person, companies, jobs, and links are fictional, for the profile in [example-profile.md](example-profile.md).

## One role

The user asked "Should I apply?" with a job link.

**Kestrel AI, Backend Engineer, New Grad: apply**

- Official link: https://jobs.example.com/kestrel-ai/4821937
- Location: Seattle, hybrid three days a week
- Posted 2026-11-03 on the official page; verified 2026-11-07 09:12 PT
- Eligibility: asks for a degree by June 2027 (confirmed: June 2026); no sponsorship needed
- Matches: Go services run in production in the capstone; REST API design in the internship
- Gaps: no Kubernetes; asks for distributed tracing, and the resume shows logging only
- Resume: `resume-backend.pdf`

## Dry run

Run `dry-2026-11-07-a`, status `partial`.
A dry run stages and delivers nothing.

- Sources: 4 declared, 3 checked; Summit Logistics showed a challenge page, so its jobs are unknown and left for retry
- Counts: 37 discovered, 31 unique, 9 verified, 2 eligible, 0 staged, 0 delivered

Would recommend:

| Company | Role | Fit | Gap | Resume |
| --- | --- | --- | --- | --- |
| Kestrel AI | Backend Engineer, New Grad | Go services in production | No Kubernetes | `resume-backend.pdf` |
| Lumen Robotics | ML Engineer I | Model serving project | No C++ | `resume-ml.pdf` |

Skipped after verification, 2 of 7 shown:

- Kestrel AI, Senior Platform Engineer: asks for five years of experience
- Lumen Robotics, Robotics Intern: internship, and the profile is not enrolled
