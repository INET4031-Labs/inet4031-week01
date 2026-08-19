## Week 1: Setup and Team Formation

**Sprint 1 Kickoff | Synchronous**

### Overview

In this lab, you will form your team, assign Sprint 1 roles, establish your shared GitHub repository, and verify access to your team's shared container environment. You will also initialize the Ansible playbook that will grow throughout the semester and serve as the blueprint for rebuilding your entire environment on Demo Day. This course models how real operations teams work: rotating responsibilities, tracking work in sprints, and treating infrastructure as code from day one. After completing this lab, you will have a functioning team charter, a structured GitHub repository, and a working Ansible playbook committed to version control that installs Docker and configures your baseline container environment.

### Learning Objectives

- Assign team roles and build a 7-sprint rotation schedule that satisfies coverage requirements
- Create and structure a GitHub repository for a semester-long infrastructure project
- Verify access to a shared privileged team container and document its baseline state
- Initialize an Ansible playbook targeting localhost that runs idempotently
- Apply the sprint ceremony structure to open Sprint 1 with a defined backlog

### Prerequisites

- A GitHub account
- Access to the team container provisioned by the professor (SSH credentials or exec method provided in class)
- No prior tool experience required for this lab

### Sprint 1 Kickoff

This is the first synchronous lab session. There is no prior sprint to review. Use this session to establish the foundation every future sprint depends on: who does what, where work lives, and how your environment is built. Work that is not tracked or reproducible from your repository does not count.

---

### Part 1: Team Roles and Sprint Structure

Before assigning roles, discuss the following questions as a group. You do not need to write your answers yet. Record your answers in the team Google Doc (created in Part 3) after the lab session.

**Discussion (whole group, before role assignments):**

1. Why would an operations team benefit from rotating responsibilities rather than fixed specialization?
2. In infrastructure work, what does "QA" mean when the deliverable is a config file or a deployment manifest?
3. How does a Scrum Master differ from a project manager? Why does that distinction matter on a team that operates systems?

After the discussion, assign roles for Sprint 1.

**Roles for this course:**

| Role | Count | Primary responsibilities |
|---|---|---|
| Scrum Master | 1 | Runs sprint ceremonies, owns the sprint board, unblocks teammates |
| System Admin | 1 | Owns environment configuration, leads infrastructure steps |
| QA | 1 | Runs all validation checks, signs off before deliverables are submitted |
| Developer | 2-3 | Writes configuration files, sets up tooling, follows lab steps |

**Step 1.** Create a GitHub repository and add your teammates as collaborators. As a group, decide who holds each role for Sprint 1. Write it down now. You will commit this to the repo in Part 2.

**Step 2.** Build your 7-sprint rotation schedule.

Every team member must hold Scrum Master, System Admin, and QA at least once across the seven sprints. With 4-6 members and 7 sprints, plan this now to avoid conflicts later. Create your  the table in your Google document in the following format:

```
Sprint 1: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
Sprint 2: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
Sprint 3: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
Sprint 4: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
Sprint 5: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
Sprint 6: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
Sprint 7: Scrum Master = ___, System Admin = ___, QA = ___, Developers = ___
```

**Step 3.** Agree on your team's communication norms. Decide the following before moving on:

- Where your team communicates outside of class (Discord, Slack, group text, etc.)
- How you will notify each other when something is merged or when something breaks
- What your expected response time is when a teammate is blocked on a task

Record these norms. You will commit them to the repo in Part 2.

---

### Part 2: Version Control and Project Tracking

Before writing any configuration, get your version control environment in order. Every artifact you create in this course lives in the repo, or it does not exist.

**Step 1.** Complete the following two GitHub Skills tutorials before creating your team repo. These cover the basics you will use throughout the semester.

- [Introduction to GitHub](https://github.com/skills/introduction-to-github)
- [Introduction to Git](https://github.com/skills/introduction-to-git)

One team member can work through these while others handle role planning, but every member should review the material before the end of lab.

**Step 2.** One team member creates the repository. Name it exactly:

```
inet4031-team-[number]
```

Replace `[number]` with your assigned team number (provided by the professor). Set visibility to **Public**. Add all teammates as collaborators with **Write** access under Settings > Collaborators.

**Step 3.** Clone the repository into your team container. The System Admin leads this step while others verify the output.

```bash
git clone https://github.com/[your-org-or-username]/inet4031-team-[number].git
cd inet4031-team-[number]
```

You should see an empty repository directory with no files listed.

**Step 4.** Create the top-level directory structure. This structure anticipates tooling you will add in future sprints.

```bash
mkdir -p ansible week-1 week-2 week-3 week-4 week-5 week-6 week-7 week-8 week-9 scripts
```

**Step 5.** Create `README.md` at the repo root. Include: your team name, team roster (names and UMN IDs), a one-paragraph project description, and a placeholder line for the Google Doc link. You will fill in the link during Part 3.

**Step 6.** Create `team-charter.md` at the repo root. This file must include all of the following:

- Team name and full roster
- Sprint 1 role assignments
- Full 7-sprint rotation schedule
- One-sentence description of each role
- Communication norms from Part 1 Step 3
- Three decisions the team made about how you will operate the container together (for example: who is responsible for committing playbook changes, how you will handle merge conflicts, what your team will do if the container behaves unexpectedly)

**Step 7.** Commit and push both files.

```bash
git add README.md team-charter.md
git commit -m "feat: add README and team charter for Sprint 1"
git push origin main
```

You should see output ending in `main -> main`. If you see an authentication error, confirm your GitHub credentials are configured on the container.

**Step 8.** The Scrum Master creates a GitHub Project board linked to the repository. Add four columns: Backlog, In Progress, In Review, Done.

**Step 9.** Open Sprint 1 tickets on the board. Create at minimum one ticket per Part of this lab, and one ticket for each major task in Week 2. The Scrum Master owns the board. Developers and the System Admin pull tickets as they work through the steps.

**Discussion (answer in Google Doc, Sprint 1 section):**

- You committed a team charter and project structure before writing a single line of configuration. Why does this ordering matter on a team that operates shared infrastructure?
- What would happen if two teammates both pushed changes to `team-charter.md` at the same time? What does Git do in that situation, and whose job is it to resolve it?

---

### Part 3: Container Environment and Ansible Bootstrap

Your team has been assigned one shared container for the entire semester. This replaces individual VMs. Every member of your team can access it simultaneously.

> **Enterprise Pattern:** Large infrastructure teams often share environment access rather than maintaining identical individual environments. The tradeoff is coordination overhead in exchange for consistency. Your shared team container makes that tradeoff explicit.

**Step 1.** Every team member independently verifies they can access the team container using the method the professor provided (SSH or `docker exec`). Do not move forward until everyone on the team can get in.

**Step 2.** The System Admin runs the following commands to document the baseline state of the container. Every other team member should be watching and noting what they see.

Check the operating system:

```bash
cat /etc/os-release
```

Check available disk space:

```bash
df -h
```

Check which course-relevant tools are already installed:

```bash
which docker git python3 curl ansible
```

Check the Docker daemon status (this is the nested Docker daemon running inside the container):

```bash
docker info
```

**Step 3.** Record your observations in `team-charter.md` under a new section called "Container Baseline." Include: OS name and version, total disk space available, and which of the listed tools are already installed versus missing.

Commit the update:

```bash
git add team-charter.md
git commit -m "docs: add container baseline observations to charter"
git push origin main
```

**Step 4.** Install Ansible inside the container if it is not already present.

```bash
apt-get update && apt-get install -y ansible
```

Verify the installation succeeded:

```bash
ansible --version
```

You should see a version line starting with `ansible [core` or `ansible 2.`. If you see "command not found," check whether `apt-get` ran without errors and retry.

**Step 5.** Create the Ansible directory structure inside the repo. The System Admin creates this while Developers observe and QA prepares to verify the output.

```bash
mkdir -p ansible/roles
touch ansible/site.yml ansible/inventory
```

**Step 6.** Configure the Ansible inventory file to target localhost. Open `ansible/inventory` and add:

```ini
[local]
localhost ansible_connection=local
```

This tells Ansible to run tasks on the same machine where it is invoked, without trying to SSH anywhere.

**Step 7.** Create the initial `ansible/site.yml`. This playbook will grow one role per week through Week 4. Right now it does one thing: ensure the baseline environment is configured.

Open `ansible/site.yml` and copy & paste the following:

```yaml
---
- name: Baseline environment setup
  hosts: localhost
  connection: local
  become: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600

    - name: Ensure baseline packages are installed
      apt:
        name:
          - curl
          - git
          - vim
          - python3
          - python3-pip
        state: present

    - name: Ensure Docker is installed
      apt:
        name: docker.io
        state: present
```

**Step 8.** Run the playbook to verify it executes without errors.

```bash
ansible-playbook -i ansible/inventory ansible/site.yml
```

Look for the `PLAY RECAP` section at the bottom of the output. You should see `failed=0` and `unreachable=0`.

**Step 9.** Run the playbook a second time without making any changes.

```bash
ansible-playbook -i ansible/inventory ansible/site.yml
```

This time, every task should report `ok` rather than `changed`. This confirms the playbook is idempotent: running it twice produces the same end state as running it once.

> **Enterprise Pattern:** Idempotency is a core requirement for automation in production. If a playbook makes changes on every run, it is not safe to run automatically on a schedule. The `ok` versus `changed` distinction in Ansible output is how you verify idempotency before trusting a playbook in production.

**Step 10.** Commit the Ansible files to the repo.

```bash
git add ansible/
git commit -m "feat: initialize site.yml with baseline environment play"
git push origin main
```

**Step 11.** Create the Google Doc for your team. Open Google Drive using your UMN Google Workspace account (not personal Gmail). Create a new Google Doc titled:

```
INET 4031 Team [number] Reflections
```

 Add the doc's URL (Ensure that the copy link allows access to all users within University of Minnesota) to `README.md` under a "Team Documents" section. Commit and push the update.

```bash
git add README.md
git commit -m "docs: add Google Doc link to README"
git push origin main
```

Answer the Part 1 and Part 2 discussion questions in the Google Doc now, under a section labeled "Sprint 1 Reflections."

**Discussion (answer in Google Doc, Sprint 1 section):**

- What would happen to your work if this container were wiped right now? How much of what you built exists in a form that can be recreated automatically?
- What is the difference between a manual setup process and an automated one? Which one is reproducible across all team members, and which one depends on someone remembering what they did?

---

### Storage Check

Run these two commands inside the container and record the output in your Google Doc under a section labeled "Week 1 Storage Baseline."

```bash
df -h
docker system df
```

The `df -h` output shows filesystem usage on the container's file system. The `docker system df` output shows space used by Docker images, containers, and volumes managed by the Docker daemon. At this point both should show minimal usage. You will compare against these numbers at the end of each future week.

Note: starting in Week 3, you will install k3d, which uses a separate containerd image store that `docker system df` does not report. Both tools consume disk space. More on this in Week 3.

---

### Validation Checks

**QA runs all validation checks.** Every other team member watches and verifies the output matches what is expected below.

#### Validation Check: All Team Members Can Access the Container

Every team member must run this individually from their own machine or terminal connected to the Docker container:

```bash
whoami
hostname
```

Expected output: a username and the container hostname provided by the professor. If any team member cannot connect, stop and resolve access before moving on.

#### Validation Check: Repository Structure Is Correct

Run from the repo root inside the container:

```bash
ls -1
```

Expected output includes at minimum: `README.md`, `ansible`, `scripts`, `team-charter.md`, `week-1`, `week-2`. If any directory is missing, create it and push the change before running the check script.

#### Validation Check: Ansible Playbook Is Idempotent

Run the playbook twice in a row without making any changes between runs:

```bash
ansible-playbook -i ansible/inventory ansible/site.yml
ansible-playbook -i ansible/inventory ansible/site.yml
```

Expected output of the second run: every task shows `ok` in the status column, not `changed`. The `PLAY RECAP` line should show `changed=0`.

If any task shows `changed` on the second run, that task is not idempotent. Identify which task it is and correct the playbook before submitting.

#### Validation Check: Google Doc Is Linked and Shared

Open `README.md` and confirm the Google Doc URL is present. Open the URL and confirm: the doc is accessible to those within the University of  Minnesota, and it contains at least the Sprint 1 reflection section with answers to Parts 1, 2, and 3 discussion questions.

#### Validation Check: Check Script Passes

```bash
./scripts/check-week1.sh
```

Expected: all checks pass. If any check fails, the script will identify which requirement is not met. Fix the issue and re-run before marking deliverables complete.

---

### Deliverables

- `README.md` committed to repo root (team name, roster, Google Doc link filled in)
- `team-charter.md` committed to repo root (all required sections present, including container baseline)
- `ansible/site.yml` committed (runs without error, passes the idempotency check)
- `ansible/inventory` committed
- Google Doc created with UMN-wide access, doc URL in `README.md`
- Google Doc contains Sprint 1 reflection answers for Parts 1, 2, and 3
- All validation checks pass

**Screenshot requirements (add to the team Google Doc):**

- **Screenshot 1:** Terminal output showing each team member's `whoami` result from inside the container
- **Screenshot 2:** `ansible-playbook` output from the second run showing `changed=0` in the PLAY RECAP

---

### Sprint Backlog: Preparing for Week 2

Week 2 is asynchronous. Before leaving today's lab session, the Scrum Master ensures the sprint board has the following tickets open in the Backlog column.

Tickets to open:

- Define Docker Compose services (Nginx, Flask, PostgreSQL)
- Configure named network and named volume
- Set up `.env` pattern for credentials
- Add `app-stack` role to `ansible/site.yml`
- Run Week 2 validation checks and check script
- Update Google Doc with Week 2 reflections and storage check
