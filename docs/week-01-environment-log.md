# Environment State Log

Use this file to record snapshots of your environment at key points in Sprint 1. These snapshots help you understand what is installed, what is running, and how much disk space you are using.

## Sprint 1 Opening: Container Baseline

Record the baseline state from Part 3 Step 2:

**Operating System:**
```
[Output of `cat /etc/os-release` goes here]
```

**Disk Space Available:**
```
[Output of `df -h` goes here]
```

**Installed Tools:**
```
[Output of `which docker git python3 curl ansible` goes here]
```

**Docker Daemon Status:**
```
[Output of `docker info` goes here]
```

## Week 1 Storage Check

Record at the end of Week 1 (Part 3 Step 11, before submitting):

**Filesystem Usage:**
```
[Output of `df -h` goes here]
```

**Docker System Usage:**
```
[Output of `docker system df` goes here]
```

**Notes:**
- At this point, Docker usage should be minimal since you have not yet deployed the application stack
- You should see only ansible and basic system containers
- Disk space should be largely unchanged from baseline

## Key Environment Decisions

Record any important decisions or changes made to your environment setup during Sprint 1:

- [Decision 1]
- [Decision 2]
- [Decision 3]
