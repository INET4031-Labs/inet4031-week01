# Sprint 1 Acceptance Criteria

This document tracks the requirements for Sprint 1 completion. Each item below must be verified before marking the sprint complete.

## Repository Structure

- [ ] `README.md` exists at repo root with team name and roster filled in
- [ ] `team-charter.md` exists at repo root with all required sections
- [ ] `ansible/` directory exists
- [ ] `ansible/site.yml` exists and is committed
- [ ] `ansible/inventory` exists and is committed
- [ ] `scripts/` directory exists
- [ ] `week-1/`, `week-2/`, `week-3/`, etc. directories created (up to `week-9/`)
- [ ] `.gitignore` file exists

## GitHub Project Setup

- [ ] Repository name is exactly `inet4031-team-[number]`
- [ ] Repository is public
- [ ] All team members added as collaborators with Write access
- [ ] Project board created with columns: Backlog, In Progress, In Review, Done
- [ ] Week 2 tickets opened in Backlog on the project board

## Team Charter Completion

- [ ] Team name documented
- [ ] All team members listed with UMN IDs
- [ ] Sprint 1 role assignments documented
- [ ] Full 7-sprint rotation schedule documented
- [ ] Role one-sentence descriptions included
- [ ] Communication norms documented (channel, notification method, response time)
- [ ] Three operating agreements documented
- [ ] Container baseline section filled in (OS, disk space, pre-installed tools)

## Container Access Verification

- [ ] Every team member can connect to the shared container independently
- [ ] Each team member runs `whoami` and `hostname` successfully
- [ ] Container output is documented and added to Google Doc (Screenshot 1)

## Ansible Setup and Testing

- [ ] `ansible/inventory` configured with localhost for local connection
- [ ] `ansible/site.yml` contains baseline environment play
- [ ] Playbook runs without error on first run
- [ ] Playbook is idempotent: second run shows `changed=0` in PLAY RECAP
- [ ] `changed=0` output added to Google Doc (Screenshot 2)
- [ ] Ansible is installed in the container

## Google Doc Completion

- [ ] Google Doc created with UMN Google Workspace account
- [ ] Doc titled: "INET 4031 Team [number] Reflections"
- [ ] Doc URL added to `README.md` under "Team Documents" section
- [ ] Doc permissions set to allow access to all University of Minnesota users
- [ ] Sprint 1 Reflections section contains answers to Part 1 discussion questions
- [ ] Sprint 1 Reflections section contains answers to Part 2 discussion questions
- [ ] Sprint 1 Reflections section contains answers to Part 3 discussion questions
- [ ] Week 1 Storage Baseline section contains:
  - [ ] Output of `df -h`
  - [ ] Output of `docker system df`

## Validation Checks Passed

- [ ] All team members can access container (validation check 1)
- [ ] Repository structure is correct (validation check 2)
- [ ] Ansible playbook is idempotent (validation check 3)
- [ ] Google Doc is linked and shared (validation check 4)
- [ ] Check script passes: `./scripts/check-week1.sh` (validation check 5)

## Git Commits

- [ ] README.md committed
- [ ] team-charter.md committed
- [ ] ansible/ directory committed
- [ ] All commits have descriptive messages
- [ ] All branches merged to main before submission

## Screenshots Required in Google Doc

- [ ] Screenshot 1: Terminal output showing each team member's `whoami` result
- [ ] Screenshot 2: Second `ansible-playbook` run with `changed=0` in PLAY RECAP
