# INET 4031: Team [number] Repository

**Sprint 1 Kickoff | Synchronous**

This is the semester-long repository for our team's INET 4031 Systems Administration
project: an incident-tracking application built and operated across nine weeks,
moving from Docker Compose through Kubernetes, Infrastructure as Code, CI/CD,
observability, security hardening, and backup/recovery.

## Important: Container Architecture Assumption

This course assumes the university's container platform allows Docker containers to
run in privileged mode (`--privileged` flag). This configuration has not yet been
confirmed by the professor. If privileged mode is unavailable, the team container
model described in this course will not function as designed starting Week 3, and
the course will need to fall back to individual student VMs. If you encounter errors
related to Docker or container permissions, contact the professor immediately before
proceeding further with the labs.

## Team

**Team Name:** [To be filled in during Part 2]

**Team Number:** [Enter number provided by professor]

**Roster:**

| Name | UMN ID |
|------|--------|
| | |
| | |
| | |
| | |

See `team-charter.md` for role assignments, the 7-sprint rotation schedule, and
communication norms.

## Directory Structure

```
README.md            - this file
team-charter.md       - team roles, rotation schedule, operating agreements
ansible/              - playbook that grows one role per week (Weeks 1-4)
scripts/               - validation check scripts, one per week
docs/                   - sprint retrospectives, environment log, acceptance criteria, QA reports
week-1/ .. week-9/    - per-week working directories (some weeks' real deliverables
                          live in top-level dirs instead - manifests/, infrastructure/,
                          .github/workflows/ - see each week-N/README.md for specifics)
```

## Getting Each Week's Starter Content

Starting Week 2, each week has a corresponding `inet4031-week0N` repo with starter
and reference files for that week. You pull only what you need from it into this one
repo using a temporary git remote -- you never clone it standalone, and it never
replaces this repo. Each week's own README has the exact command for that week, for
example:

```bash
git remote add week2 https://github.com/INET4031-Labs/inet4031-week02.git
git fetch week2
git checkout week2/main -- <that week's paths>
git remote remove week2
```

## Team Documents

**Google Doc:** [Google Doc link will go here - create during Part 3 Step 11]

All sprint reflections, screenshots, and storage-check output are recorded in this
document as each week's lab directions require.

## Getting Started

1. Read the Week 1 lab directions completely before beginning.
2. Follow Part 1, then Part 2, then Part 3 in order.
3. Before submitting, run `./scripts/check-week1.sh` from the repo root to verify
   all Week 1 requirements are met.
4. Reference `docs/week-01-acceptance-criteria.md` and `docs/qa-report-1.md` for the sign-off
   checklist.

## Questions or Issues

1. Check the troubleshooting section in the lab directions.
2. Review `docs/week-01-acceptance-criteria.md`.
3. Consult with your team's System Admin and QA roles.
4. Contact the course instructor if blocked.
