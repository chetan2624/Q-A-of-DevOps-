# DevOps Interview Questions

A comprehensive collection of DevOps interview questions covering essential technologies and tools. This repository contains both common and scenario-based questions to help you prepare for DevOps interviews.

## Table of Contents

- [Linux](#linux)
- [AWS (Amazon Web Services)](#aws-amazon-web-services)
- [GitHub](#github)
- [Docker](#docker)
- [Kubernetes](#kubernetes)
- [Terraform](#terraform)
- [Jenkins](#jenkins)
- [Datadog](#datadog)

---

## Linux

### Common Questions

**Q.1** What is Linux and why is it popular in DevOps?

Linux is an open-source operating system kernel. It's popular in DevOps due to its stability, security, flexibility, cost-effectiveness, and extensive community support. Most servers and cloud infrastructure run on Linux.

**Q.2** What is the difference between absolute and relative paths?

Absolute path starts from the root directory (/) and provides the complete path (e.g., /home/user/file.txt). Relative path starts from the current directory (e.g., ../documents/file.txt).

**Q.3** Explain the Linux file system hierarchy.

The Linux file system follows a tree structure starting with root (/). Key directories include:
- /bin - Essential user binaries
- /etc - Configuration files
- /home - User home directories
- /var - Variable files (logs, temp files)
- /usr - User programs
- /tmp - Temporary files

**Q.4** What are file permissions in Linux? Explain chmod.

File permissions control access to files and directories. There are three types: read (r/4), write (w/2), execute (x/1) for three categories: owner, group, and others. chmod changes permissions (e.g., chmod 755 file.txt).

**Q.5** What is the difference between hard link and soft link?

Hard link points directly to the inode of a file, shares the same data. Soft link (symbolic link) is a pointer to the file path. Hard links can't cross file systems; soft links can.

**Q.6** Explain the purpose of /etc/passwd and /etc/shadow files.

/etc/passwd stores user account information (username, UID, GID, home directory, shell). /etc/shadow stores encrypted passwords and password aging information with restricted access.

**Q.7** What is a daemon in Linux?

A daemon is a background process that runs continuously, typically started at boot time. Examples include sshd (SSH daemon), httpd (web server), and systemd.

**Q.8** What are the different run levels in Linux?

Run levels define the system's state:
- 0: Halt
- 1: Single-user mode
- 2: Multi-user without networking
- 3: Multi-user with networking
- 5: Multi-user with GUI
- 6: Reboot

**Q.9** Explain the difference between kill and killall commands.

kill terminates a process by its PID (kill -9 1234). killall terminates all processes with a specific name (killall -9 firefox).

**Q.10** What is the purpose of the cron daemon?

Cron is a time-based job scheduler that executes commands or scripts at specified intervals. It's controlled by crontab files.

**Q.11** What are inode numbers in Linux?

Inodes store metadata about files (permissions, ownership, timestamps, location) but not the filename or data. Each file has a unique inode number.

**Q.12** Explain the difference between locate and find commands.

locate searches a pre-built database (fast but may be outdated). find searches the file system in real-time (slower but always current).

**Q.13** What is SELinux?

Security-Enhanced Linux is a security architecture that provides mandatory access control (MAC) to enhance system security beyond traditional Unix discretionary access control.

**Q.14** What is swap space?

Swap space is disk space used as virtual memory when physical RAM is full. It allows the system to run more processes than RAM capacity allows.

**Q.15** Explain the purpose of systemctl command.

systemctl manages systemd services and system states. It can start, stop, restart, enable, disable services, and check their status.

### Scenario-Based Questions

**Q.16** A server is running slow. How would you troubleshoot and identify the issue?

Steps to troubleshoot:
1. Check CPU usage: `top`, `htop`, or `mpstat`
2. Check memory: `free -h`, `vmstat`
3. Check disk I/O: `iostat`, `iotop`
4. Check disk space: `df -h`
5. Check network: `netstat`, `ss`, `iftop`
6. Review logs: `/var/log/syslog`, `/var/log/messages`
7. Check running processes: `ps aux`
8. Identify resource-intensive processes and optimize or kill them

**Q.17** How do you find and kill a process that is using a specific port?

```bash
# Find the process
lsof -i :8080
# or
netstat -tulpn | grep 8080

# Kill the process
kill -9 <PID>
# or
fuser -k 8080/tcp
```

**Q.18** Your application logs are filling up disk space. How would you manage this?

Solutions:
1. Implement log rotation using logrotate configuration
2. Compress old logs: `gzip /var/log/app/*.log`
3. Archive and move to remote storage
4. Set retention policies
5. Use centralized logging (ELK, Splunk)
6. Monitor disk usage with alerts

**Q.19** You need to copy a large file between servers. What methods would you use and why?

Methods:
1. `scp`: Secure but slower for large files
   ```bash
   scp large_file.tar.gz user@server:/path/
   ```
2. `rsync`: Faster, can resume, only copies differences
   ```bash
   rsync -avz --progress large_file.tar.gz user@server:/path/
   ```
3. `nc` (netcat): Fastest for one-time transfers
4. Consider splitting large files with `split`

**Q.20** A critical configuration file was accidentally deleted. How do you recover it?

Recovery steps:
1. Check if file is still in memory: `lsof | grep deleted`
2. Restore from backup
3. Check version control (Git) if applicable
4. Use `extundelete` or `testdisk` for ext3/4 filesystems
5. Restore from configuration management (Ansible, Puppet)
6. Recreate from documentation or default templates

**Q.21** How would you secure SSH access to a Linux server?

Security measures:
1. Disable root login: `PermitRootLogin no` in /etc/ssh/sshd_config
2. Use SSH keys instead of passwords
3. Change default port 22
4. Use `fail2ban` to prevent brute force attacks
5. Limit users: `AllowUsers username`
6. Use strong encryption algorithms
7. Implement two-factor authentication
8. Keep SSH updated
9. Use firewall rules to restrict access

**Q.22** Your system is showing "Out of Memory" errors. How do you investigate and resolve?

Investigation and resolution:
1. Check memory usage: `free -h`, `cat /proc/meminfo`
2. Identify memory-consuming processes: `ps aux --sort=-%mem | head`
3. Check for memory leaks in applications
4. Review OOM killer logs: `dmesg | grep -i oom`
5. Increase swap space if needed
6. Optimize applications to use less memory
7. Add more RAM if necessary
8. Implement memory limits using cgroups

**Q.23** How do you monitor and analyze system performance over time?

Tools and methods:
1. Install monitoring tools: `sar`, `atop`, `nmon`
2. Use `sar` for historical data: `sar -u` (CPU), `sar -r` (memory)
3. Set up performance monitoring dashboards (Grafana)
4. Collect metrics with tools like Prometheus
5. Schedule regular reports with cron
6. Review logs regularly
7. Set up alerts for thresholds
8. Create performance baselines

**Q.24** You need to automate a task that runs every day at 3 AM. How do you set this up?

Using cron:
```bash
# Edit crontab
crontab -e

# Add entry (runs at 3:00 AM daily)
0 3 * * * /path/to/script.sh

# Or using systemd timer
# Create timer file: /etc/systemd/system/daily-task.timer
# Create service file: /etc/systemd/system/daily-task.service
# Enable: systemctl enable --now daily-task.timer
```

**Q.25** How would you troubleshoot a service that fails to start?

Troubleshooting steps:
1. Check service status: `systemctl status service-name`
2. View detailed logs: `journalctl -u service-name -n 50`
3. Check configuration files for syntax errors
4. Verify file permissions
5. Check dependencies: `systemctl list-dependencies service-name`
6. Test manual start for error messages
7. Check port conflicts: `netstat -tulpn`
8. Review system logs: `/var/log/syslog`
9. Check resource availability (disk space, memory)

---

## AWS (Amazon Web Services)

### Common Questions

**Q.26** What is AWS and what are its key services?

AWS is Amazon's cloud computing platform offering on-demand services. Key services include EC2 (compute), S3 (storage), RDS (databases), VPC (networking), IAM (security), Lambda (serverless), and many more.

**Q.27** Explain the difference between EC2 and Lambda.

EC2 provides virtual servers that run continuously and you manage the OS. Lambda is serverless, executes code in response to events, runs only when triggered, and you pay only for execution time.

**Q.28** What is S3 and what are its storage classes?

S3 is object storage service. Storage classes include:
- S3 Standard (frequent access)
- S3 Intelligent-Tiering (automatic optimization)
- S3 Standard-IA (infrequent access)
- S3 One Zone-IA
- S3 Glacier (archival)
- S3 Glacier Deep Archive (long-term archival)

**Q.29** What is the difference between security groups and NACLs?

Security Groups are stateful, operate at instance level, support allow rules only, and evaluate all rules. NACLs (Network ACLs) are stateless, operate at subnet level, support both allow and deny rules, and process rules in order.

**Q.30** Explain VPC and its components.

VPC (Virtual Private Cloud) is an isolated network in AWS. Components include:
- Subnets (public/private)
- Route tables
- Internet Gateway (IGW)
- NAT Gateway
- Security Groups
- Network ACLs
- VPC Peering

**Q.31** What is IAM and why is it important?

IAM (Identity and Access Management) controls access to AWS resources. It manages users, groups, roles, and policies. Important for security, implementing least privilege, and audit compliance.

**Q.32** What are AWS regions and availability zones?

Regions are geographical locations with multiple data centers. Availability Zones (AZs) are isolated data centers within a region. Using multiple AZs provides high availability and fault tolerance.

**Q.33** Explain the difference between EBS and EFS.

EBS (Elastic Block Store) is block storage attached to a single EC2 instance, like a hard drive. EFS (Elastic File System) is network file storage that can be mounted by multiple instances simultaneously.

**Q.34** What is CloudFormation?

CloudFormation is Infrastructure as Code (IaC) service that provisions AWS resources using templates (JSON/YAML). It enables automated, repeatable, and version-controlled infrastructure deployment.

**Q.35** What is Auto Scaling and how does it work?

Auto Scaling automatically adjusts the number of EC2 instances based on demand. It uses scaling policies, metrics (CPU, memory), and health checks to maintain desired capacity and performance.

**Q.36** Explain AWS Route 53.

Route 53 is AWS's DNS service that routes end users to applications. It provides domain registration, DNS routing, health checking, and various routing policies (simple, weighted, latency-based, failover).

**Q.37** What is CloudWatch?

CloudWatch is AWS's monitoring and observability service. It collects metrics, logs, and events from AWS resources, enables alarms, dashboards, and automated actions based on defined thresholds.

**Q.38** What is the difference between RDS and DynamoDB?

RDS is a managed relational database service (MySQL, PostgreSQL, etc.) with ACID properties and SQL. DynamoDB is a NoSQL database with key-value and document data models, designed for high scalability and performance.

**Q.39** What is AWS ECS and EKS?

ECS (Elastic Container Service) is AWS's container orchestration service. EKS (Elastic Kubernetes Service) is managed Kubernetes service. Both run containerized applications but EKS uses Kubernetes.

**Q.40** Explain AWS CodePipeline.

CodePipeline is a continuous delivery service that automates build, test, and deploy phases. It integrates with CodeCommit, CodeBuild, CodeDeploy, and third-party tools to create CI/CD workflows.

### Scenario-Based Questions

**Q.41** Your application running on EC2 is experiencing high traffic. How would you scale it?

Scaling strategies:
1. Implement Auto Scaling Groups with target tracking policies
2. Use Application Load Balancer to distribute traffic
3. Set up CloudWatch alarms for scaling triggers
4. Consider using multiple availability zones
5. Implement caching with ElastiCache
6. Use CloudFront CDN for static content
7. Optimize application code and database queries
8. Consider serverless architecture with Lambda

**Q.42** How would you design a highly available and fault-tolerant architecture on AWS?

Design principles:
1. Deploy across multiple Availability Zones
2. Use Elastic Load Balancer for traffic distribution
3. Implement Auto Scaling Groups
4. Use Multi-AZ RDS for database
5. Store static content in S3 with CloudFront
6. Implement backup and disaster recovery
7. Use Route 53 health checks and failover routing
8. Enable CloudWatch monitoring and alarms
9. Implement redundancy at every layer

**Q.43** Your S3 costs are increasing rapidly. How would you optimize them?

Cost optimization strategies:
1. Analyze S3 storage using Storage Lens or Cost Explorer
2. Implement lifecycle policies to move data to cheaper storage classes
3. Enable S3 Intelligent-Tiering
4. Delete incomplete multipart uploads
5. Remove old versions if versioning is enabled
6. Compress files before uploading
7. Use S3 Select for partial object retrieval
8. Review and remove unnecessary data
9. Implement data retention policies

**Q.44** How would you migrate an on-premises application to AWS with minimal downtime?

Migration approach:
1. Assessment: Analyze application dependencies and requirements
2. Choose migration strategy (lift-and-shift, re-platform, refactor)
3. Set up AWS environment (VPC, subnets, security groups)
4. Use AWS Database Migration Service for databases
5. Replicate data using AWS DataSync or Storage Gateway
6. Set up parallel environment and test thoroughly
7. Use Route 53 weighted routing for gradual traffic shift
8. Monitor closely during and after migration
9. Keep on-premises as backup until stable

**Q.45** Your application needs to process files uploaded to S3. How would you design this?

Design approach:
1. Enable S3 event notifications
2. Trigger Lambda function on file upload
3. Lambda processes file or queues job in SQS
4. Use Step Functions for complex workflows
5. Store results in S3 or database
6. Implement error handling and retry logic
7. Use DLQ for failed processing
8. Monitor with CloudWatch
9. Consider batch processing for efficiency

**Q.46** How would you implement disaster recovery for a critical application on AWS?

DR implementation:
1. Define RTO (Recovery Time Objective) and RPO (Recovery Point Objective)
2. Choose DR strategy: backup/restore, pilot light, warm standby, or multi-site
3. Set up secondary region with infrastructure
4. Implement automated backups for databases and data
5. Use S3 cross-region replication
6. Configure Route 53 failover routing
7. Automate recovery with CloudFormation
8. Regular testing of DR procedures
9. Document runbooks and procedures

**Q.47** Your AWS bill is higher than expected. How would you investigate and reduce costs?

Cost optimization steps:
1. Use AWS Cost Explorer to analyze spending
2. Enable AWS Budgets and alerts
3. Review underutilized resources (Trusted Advisor)
4. Right-size EC2 instances
5. Use Reserved Instances or Savings Plans for predictable workloads
6. Stop non-production resources during off-hours
7. Delete unused EBS volumes and snapshots
8. Use S3 lifecycle policies
9. Implement cost allocation tags
10. Consider Spot Instances for fault-tolerant workloads

**Q.48** How would you secure sensitive data in AWS?

Security measures:
1. Encrypt data at rest using AWS KMS
2. Enable encryption in transit (SSL/TLS)
3. Use IAM roles with least privilege
4. Enable MFA for sensitive operations
5. Use AWS Secrets Manager for credentials
6. Implement VPC endpoints for private connectivity
7. Enable CloudTrail for audit logging
8. Use AWS Config for compliance monitoring
9. Implement data classification and tagging
10. Regular security assessments and penetration testing

**Q.49** Your RDS database is experiencing performance issues. How would you troubleshoot?

Troubleshooting steps:
1. Check CloudWatch metrics (CPU, connections, IOPS, latency)
2. Enable Performance Insights for query analysis
3. Review slow query logs
4. Check for blocking queries and locks
5. Analyze database parameters and configuration
6. Consider read replicas for read-heavy workloads
7. Optimize queries and add indexes
8. Increase instance size if needed
9. Use ElastiCache for frequently accessed data
10. Review connection pooling settings

**Q.50** How would you implement a blue-green deployment strategy on AWS?

Implementation approach:
1. Create two identical environments (blue and green)
2. Blue runs current version, green runs new version
3. Use Auto Scaling Groups for each environment
4. Deploy new version to green environment
5. Test green environment thoroughly
6. Use Route 53 weighted routing or ALB for traffic shift
7. Gradually shift traffic from blue to green
8. Monitor metrics and logs during transition
9. Keep blue environment for quick rollback if needed
10. Once stable, update blue for next deployment

---

## GitHub

### Common Questions

**Q.51** What is Git and how is it different from GitHub?

Git is a distributed version control system for tracking code changes. GitHub is a cloud-based hosting service for Git repositories with collaboration features like pull requests, issues, and actions.

**Q.52** What is the difference between git pull and git fetch?

git fetch downloads changes from remote but doesn't merge them. git pull downloads changes and automatically merges them into your current branch (fetch + merge).

**Q.53** Explain the difference between git merge and git rebase.

git merge combines branches by creating a new merge commit, preserving history. git rebase moves or combines commits to a new base, creating a linear history.

**Q.54** What is a pull request?

A pull request is a GitHub feature to propose changes from one branch to another. It enables code review, discussion, and CI/CD checks before merging changes.

**Q.55** What are Git branches and why are they important?

Branches are separate lines of development in Git. They allow parallel work on features, isolate changes, enable experimentation without affecting main code, and facilitate team collaboration.

**Q.56** What is .gitignore file?

.gitignore specifies files and directories that Git should not track. Common examples include build artifacts, dependencies, logs, and environment files.

**Q.57** Explain the difference between git reset and git revert.

git reset moves the branch pointer backwards, removing commits from history. git revert creates a new commit that undoes changes from a previous commit, preserving history.

**Q.58** What is GitHub Actions?

GitHub Actions is a CI/CD platform integrated with GitHub. It automates workflows for building, testing, and deploying code using YAML-defined workflows triggered by repository events.

**Q.59** What is a fork in GitHub?

A fork is a personal copy of another user's repository. It allows you to freely experiment with changes without affecting the original project.

**Q.60** What are Git tags?

Tags are references to specific points in Git history, typically used for marking release versions. There are lightweight tags (simple pointers) and annotated tags (with metadata).

**Q.61** Explain Git stash.

git stash temporarily saves uncommitted changes and reverts the working directory to a clean state. Useful for switching branches without committing incomplete work.

**Q.62** What is cherry-pick in Git?

Cherry-pick applies the changes from a specific commit to your current branch. Useful for selectively applying changes without merging entire branches.

**Q.63** What are GitHub webhooks?

Webhooks are HTTP callbacks triggered by repository events (push, pull request, etc.). They send POST requests to specified URLs, enabling integration with external services.

**Q.64** Explain the purpose of .git directory.

.git directory contains all Git repository metadata: commits, branches, configuration, hooks, and object database. It's created when you run git init.

**Q.65** What is the difference between origin and upstream?

origin is the default name for the remote repository you cloned from. upstream typically refers to the original repository when working with forks.

### Scenario-Based Questions

**Q.66** You accidentally committed sensitive data (API keys) to a public repository. What do you do?

Immediate actions:
1. Rotate all exposed credentials immediately
2. Remove the file and commit: `git rm file`
3. Use git filter-branch or BFG Repo-Cleaner to remove from history:
   ```bash
   git filter-branch --force --index-filter \
     'git rm --cached --ignore-unmatch path/to/file' \
     --prune-empty --tag-name-filter cat -- --all
   ```
4. Force push: `git push origin --force --all`
5. Notify team members to rebase their work
6. Add file to .gitignore
7. Consider the data compromised and monitor for misuse

**Q.67** Multiple developers are working on the same file and there are merge conflicts. How do you resolve them?

Resolution process:
1. Pull latest changes: `git pull origin main`
2. Git will mark conflicts in files with markers
3. Review conflicts:
   ```
   <<<<<<< HEAD
   Your changes
   =======
   Incoming changes
   >>>>>>> branch-name
   ```
4. Edit file to resolve conflicts
5. Remove conflict markers
6. Test the changes
7. Stage resolved files: `git add file`
8. Commit: `git commit -m "Resolved merge conflicts"`
9. Push changes
10. Consider using merge tools like kdiff3 or meld

**Q.68** Your main branch has bugs and you need to quickly fix them while feature development continues. What's your strategy?

Hotfix strategy:
1. Create hotfix branch from main: `git checkout -b hotfix/bug-fix main`
2. Fix the bug and test thoroughly
3. Commit changes: `git commit -m "Fix critical bug"`
4. Merge to main: `git checkout main && git merge hotfix/bug-fix`
5. Tag the release: `git tag -a v1.0.1 -m "Hotfix release"`
6. Merge hotfix to development branch to prevent regression
7. Delete hotfix branch: `git branch -d hotfix/bug-fix`
8. Deploy to production
9. Notify team of the hotfix

**Q.69** How would you set up a GitHub Actions workflow for a Node.js application with automated testing and deployment?

Workflow setup:
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
      - name: Run linter
        run: npm run lint

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to production
        run: |
          # Add deployment commands
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

**Q.70** Your Git repository has grown very large and cloning takes too much time. How would you optimize it?

Optimization strategies:
1. Use shallow clone: `git clone --depth 1 repo-url`
2. Clone specific branch: `git clone -b branch-name --single-branch repo-url`
3. Use sparse checkout for specific directories:
   ```bash
   git sparse-checkout init --cone
   git sparse-checkout set directory/path
   ```
4. Clean up repository:
   ```bash
   git gc --aggressive --prune=now
   ```
5. Use Git LFS for large files
6. Remove large files from history using BFG Repo-Cleaner
7. Archive old branches
8. Split large repositories into smaller ones

**Q.71** How would you implement a branching strategy for a team of 10 developers?

Branching strategy (Git Flow):
1. Main branches:
   - `main`: Production-ready code
   - `develop`: Integration branch for features
2. Supporting branches:
   - `feature/*`: New features from develop
   - `release/*`: Prepare for production release
   - `hotfix/*`: Quick fixes for production
3. Workflow:
   - Developers create feature branches from develop
   - Complete features merged to develop via pull requests
   - Create release branch for testing
   - Merge release to main and tag version
   - Hotfixes branch from main, merge to both main and develop
4. Implement branch protection rules
5. Require code reviews and CI checks
6. Use conventional commit messages

**Q.72** Your team needs to maintain multiple versions of an application. How would you manage releases in Git?

Release management strategy:
1. Use semantic versioning (MAJOR.MINOR.PATCH)
2. Create release branches: `release/v1.0`, `release/v2.0`
3. Tag releases: `git tag -a v1.0.0 -m "Release version 1.0.0"`
4. Maintain long-term support branches for major versions
5. Backport critical fixes to supported versions
6. Use GitHub Releases for release notes and artifacts
7. Automate release process with GitHub Actions
8. Document compatibility and upgrade paths
9. Keep changelog updated

**Q.73** How would you migrate from SVN to Git while preserving history?

Migration process:
1. Install git-svn: `sudo apt-get install git-svn`
2. Create authors mapping file (svn-to-git-authors.txt):
   ```
   svnuser = Git User <email@example.com>
   ```
3. Clone SVN repository:
   ```bash
   git svn clone http://svn-repo-url \
     --authors-file=svn-to-git-authors.txt \
     --stdlayout git-repo
   ```
4. Clean up SVN metadata
5. Convert SVN tags to Git tags
6. Create GitHub repository
7. Push to GitHub:
   ```bash
   git remote add origin github-url
   git push -u origin --all
   git push --tags
   ```
8. Verify migration and test
9. Update team documentation and tools

**Q.74** How do you handle code reviews effectively using GitHub pull requests?

Code review best practices:
1. Create clear PR descriptions with context
2. Keep PRs small and focused (< 400 lines when possible)
3. Use PR templates for consistency
4. Link related issues
5. Enable required reviews (minimum 2 reviewers)
6. Use review comments for discussions
7. Request changes for issues, approve when ready
8. Use GitHub's suggestion feature for minor fixes
9. Enable automated checks (linting, tests, security scans)
10. Use CODEOWNERS file for automatic reviewer assignment
11. Respond to feedback promptly
12. Merge only after approval and passing checks

**Q.75** Your repository has hundreds of outdated branches. How would you clean them up?

Cleanup strategy:
1. List all branches:
   ```bash
   git branch -r
   git branch -a
   ```
2. Identify merged branches:
   ```bash
   git branch --merged main
   ```
3. Delete local merged branches:
   ```bash
   git branch -d branch-name
   ```
4. Delete remote branches:
   ```bash
   git push origin --delete branch-name
   ```
5. Bulk delete script:
   ```bash
   git branch --merged | grep -v "main\|develop" | xargs git branch -d
   ```
6. Set up branch protection rules
7. Implement automatic branch deletion after PR merge
8. Document branch naming conventions
9. Regularly audit and clean branches
10. Archive branches if needed instead of deleting

---

## Docker

### Common Questions

**Q.76** What is Docker and why is it used?

Docker is a containerization platform that packages applications with their dependencies into containers. It ensures consistency across environments, improves resource utilization, enables microservices, and simplifies deployment.

**Q.77** What is the difference between a Docker image and a container?

An image is a read-only template with application code and dependencies. A container is a running instance of an image, with its own file system, networking, and isolated process space.

**Q.78** Explain Dockerfile and its key instructions.

Dockerfile is a text file with instructions to build a Docker image. Key instructions:
- FROM: Base image
- RUN: Execute commands
- COPY/ADD: Copy files
- WORKDIR: Set working directory
- EXPOSE: Declare port
- ENV: Set environment variables
- CMD: Default command
- ENTRYPOINT: Container executable

**Q.79** What is Docker Compose?

Docker Compose is a tool for defining and running multi-container applications using a YAML file (docker-compose.yml). It simplifies managing multiple containers, networks, and volumes.

**Q.80** What is the difference between CMD and ENTRYPOINT?

CMD provides default commands/parameters that can be overridden from command line. ENTRYPOINT defines the container's executable and CMD arguments can be appended to it.

**Q.81** What is a Docker registry?

A Docker registry stores and distributes Docker images. Docker Hub is the public registry. Private registries can be hosted using Docker Registry, AWS ECR, or Azure Container Registry.

**Q.82** Explain Docker volumes.

Volumes are the preferred mechanism for persisting data generated by containers. They're managed by Docker, stored outside container filesystem, and can be shared between containers.

**Q.83** What is Docker networking?

Docker networking enables communication between containers and external systems. Network types include:
- bridge: Default, isolated network
- host: Uses host's network
- none: No networking
- overlay: Multi-host networking
- macvlan: Assigns MAC addresses to containers

**Q.84** What is the difference between COPY and ADD in Dockerfile?

COPY simply copies files from source to container. ADD has additional features: can extract tar files and download files from URLs. Best practice is to use COPY unless you need ADD's extra functionality.

**Q.85** What are Docker layers?

Each instruction in a Dockerfile creates a layer. Layers are cached and reused to speed up builds. Only changed layers are rebuilt. Understanding layers helps optimize image size and build time.

**Q.86** Explain Docker multistage builds.

Multistage builds use multiple FROM statements in one Dockerfile. They allow building in one stage and copying artifacts to another, reducing final image size by excluding build dependencies.

**Q.87** What is Docker Swarm?

Docker Swarm is Docker's native clustering and orchestration tool. It manages a cluster of Docker engines, provides service discovery, load balancing, scaling, and rolling updates.

**Q.88** What is the difference between docker run and docker start?

docker run creates a new container from an image and starts it. docker start starts an existing stopped container.

**Q.89** What are Docker health checks?

Health checks test container health by running commands periodically. They help orchestrators determine if a container is healthy and can receive traffic or needs restart.

**Q.90** Explain the difference between docker-compose up and docker-compose start.

docker-compose up creates and starts containers, networks, and volumes. docker-compose start only starts existing stopped containers.

### Scenario-Based Questions

**Q.91** Your Docker container keeps crashing. How would you troubleshoot it?

Troubleshooting steps:
1. Check container logs:
   ```bash
   docker logs container-name
   docker logs -f container-name  # follow logs
   ```
2. Check container status:
   ```bash
   docker ps -a
   docker inspect container-name
   ```
3. Check resource usage:
   ```bash
   docker stats
   ```
4. Access container for debugging:
   ```bash
   docker exec -it container-name /bin/bash
   ```
5. Check health status:
   ```bash
   docker inspect --format='{{.State.Health.Status}}' container-name
   ```
6. Review Dockerfile and entrypoint script
7. Check for port conflicts
8. Verify environment variables and volumes
9. Test locally with same configuration
10. Check host system resources

**Q.92** Your Docker images are very large. How would you reduce their size?

Image optimization strategies:
1. Use minimal base images (alpine, distroless)
2. Use multistage builds to exclude build dependencies
3. Combine RUN commands to reduce layers:
   ```dockerfile
   RUN apt-get update && apt-get install -y \
       package1 \
       package2 \
       && rm -rf /var/lib/apt/lists/*
   ```
4. Remove unnecessary files in same layer
5. Use .dockerignore to exclude unnecessary files
6. Avoid installing recommended packages: `apt-get install --no-install-recommends`
7. Clear package manager cache
8. Order instructions from least to most frequently changing
9. Use specific tags, not latest
10. Analyze image layers: `docker history image-name`

**Q.93** How would you implement a CI/CD pipeline using Docker?

CI/CD pipeline implementation:
1. Version control: Store Dockerfile in Git
2. Build stage:
   ```bash
   docker build -t app:${VERSION} .
   docker tag app:${VERSION} registry/app:${VERSION}
   ```
3. Test stage:
   ```bash
   docker run app:${VERSION} npm test
   ```
4. Security scanning:
   ```bash
   docker scan app:${VERSION}
   trivy image app:${VERSION}
   ```
5. Push to registry:
   ```bash
   docker push registry/app:${VERSION}
   ```
6. Deploy stage using docker-compose or orchestrator
7. Implement rollback mechanism
8. Use environment-specific configurations
9. Automate with Jenkins, GitLab CI, or GitHub Actions
10. Monitor deployment success

**Q.94** Your application needs to connect to a database running in another container. How do you set this up?

Container networking setup:
1. Create a custom network:
   ```bash
   docker network create app-network
   ```
2. Run database container:
   ```bash
   docker run -d --name database \
     --network app-network \
     -e POSTGRES_PASSWORD=secret \
     postgres:14
   ```
3. Run application container:
   ```bash
   docker run -d --name app \
     --network app-network \
     -e DB_HOST=database \
     -e DB_PORT=5432 \
     myapp:latest
   ```
4. Using docker-compose:
   ```yaml
   version: '3.8'
   services:
     database:
       image: postgres:14
       environment:
         POSTGRES_PASSWORD: secret
       networks:
         - app-network
     app:
       image: myapp:latest
       environment:
         DB_HOST: database
         DB_PORT: 5432
       depends_on:
         - database
       networks:
         - app-network
   networks:
     app-network:
   ```

**Q.95** How would you secure Docker containers in production?

Security best practices:
1. Use official images from trusted sources
2. Scan images for vulnerabilities regularly
3. Run containers as non-root user:
   ```dockerfile
   RUN useradd -m appuser
   USER appuser
   ```
4. Use read-only file systems where possible:
   ```bash
   docker run --read-only app:latest
   ```
5. Limit container resources:
   ```bash
   docker run --memory="512m" --cpus="1.0" app:latest
   ```
6. Use secrets management (Docker secrets, vault)
7. Enable Docker Content Trust for signed images
8. Keep Docker and base images updated
9. Use security profiles (AppArmor, SELinux)
10. Implement network segmentation
11. Enable logging and monitoring
12. Don't expose unnecessary ports

**Q.96** Your Docker build is very slow. How would you optimize it?

Build optimization strategies:
1. Use .dockerignore to exclude unnecessary files
2. Order Dockerfile instructions strategically (stable to volatile)
3. Leverage build cache effectively
4. Use multistage builds
5. Minimize layers by combining commands
6. Use BuildKit for parallel builds:
   ```bash
   DOCKER_BUILDKIT=1 docker build .
   ```
7. Use cache mounts for package managers:
   ```dockerfile
   RUN --mount=type=cache,target=/root/.cache/pip \
       pip install -r requirements.txt
   ```
8. Pin versions to ensure cache hits
9. Copy only necessary files:
   ```dockerfile
   COPY requirements.txt .
   RUN pip install -r requirements.txt
   COPY . .
   ```
10. Use a local registry mirror
11. Increase Docker daemon resources

**Q.97** How would you migrate an application from VMs to Docker containers?

Migration approach:
1. Assessment:
   - Analyze application architecture and dependencies
   - Identify stateful components
   - Review configuration management
2. Containerization:
   - Create Dockerfile for each service
   - Extract configuration to environment variables
   - Design volume strategy for persistent data
3. Testing:
   - Build and test containers locally
   - Create docker-compose for local development
   - Performance testing and comparison
4. Migration strategy:
   - Blue-green deployment approach
   - Run containers alongside VMs initially
   - Gradually shift traffic to containers
5. Data migration:
   - Backup data from VMs
   - Migrate databases carefully
   - Use volumes for persistent storage
6. Monitoring and logging:
   - Set up container monitoring
   - Centralize logs
7. Rollback plan in case of issues
8. Documentation and team training

**Q.98** How do you handle secrets in Docker containers?

Secrets management strategies:
1. Use Docker secrets (Swarm mode):
   ```bash
   echo "db_password" | docker secret create db_pass -
   docker service create --secret db_pass myapp
   ```
2. Use environment variables from secure sources:
   ```bash
   docker run -e DB_PASS=$(vault read -field=password secret/db) app
   ```
3. Mount secrets from files with restricted permissions:
   ```bash
   docker run -v /secure/secrets:/secrets:ro app
   ```
4. Use HashiCorp Vault or AWS Secrets Manager
5. Docker Compose with env files (not for production):
   ```yaml
   services:
     app:
       env_file:
         - secrets.env
   ```
6. Never hardcode secrets in Dockerfile or image
7. Never commit secrets to version control
8. Use .env files listed in .gitignore
9. Rotate secrets regularly
10. Audit secret access

**Q.99** Your containerized application needs to scale based on load. How do you implement this?

Scaling implementation:
1. Using Docker Swarm:
   ```bash
   docker service create --replicas 3 --name web app:latest
   docker service scale web=5
   ```
2. Using Docker Compose (multiple instances):
   ```bash
   docker-compose up --scale web=3
   ```
3. Implement health checks for proper load balancing
4. Use load balancer (nginx, HAProxy, or cloud LB)
5. Auto-scaling with orchestrators (Kubernetes preferred)
6. Monitor metrics (CPU, memory, response time)
7. Define scaling policies
8. Ensure stateless design for horizontal scaling
9. Use shared storage or database for state
10. Test scaling behavior under load
11. Implement graceful shutdown

**Q.100** How would you debug a networking issue between Docker containers?

Debugging steps:
1. Check if containers are on the same network:
   ```bash
   docker network inspect network-name
   ```
2. Test connectivity using ping:
   ```bash
   docker exec container1 ping container2
   ```
3. Check DNS resolution:
   ```bash
   docker exec container1 nslookup container2
   docker exec container1 getent hosts container2
   ```
4. Verify port exposure and binding:
   ```bash
   docker port container-name
   docker inspect container-name | grep -A 20 NetworkSettings
   ```
5. Check if service is listening:
   ```bash
   docker exec container2 netstat -tlnp
   ```
6. Inspect network configuration:
   ```bash
   docker network ls
   docker network inspect bridge
   ```
7. Check firewall rules on host
8. Test with curl or telnet:
   ```bash
   docker exec container1 curl http://container2:8080
   ```
9. Review docker-compose networking configuration
10. Check logs for both containers
11. Verify container names and aliases

---

## Kubernetes

### Common Questions

**Q.101** What is Kubernetes and why is it used?

Kubernetes (K8s) is an open-source container orchestration platform that automates deployment, scaling, and management of containerized applications. It provides high availability, scalability, load balancing, self-healing, and declarative configuration.

**Q.102** Explain the Kubernetes architecture.

Kubernetes architecture consists of:
- Master Node (Control Plane):
  - API Server: Front-end for K8s control plane
  - etcd: Key-value store for cluster data
  - Scheduler: Assigns pods to nodes
  - Controller Manager: Runs controller processes
- Worker Nodes:
  - Kubelet: Ensures containers are running
  - Kube-proxy: Network proxy
  - Container Runtime: Runs containers (Docker, containerd)

**Q.103** What is a Pod in Kubernetes?

A Pod is the smallest deployable unit in Kubernetes. It represents one or more containers that share storage, network, and specifications. Containers in a pod share the same IP address and port space.

**Q.104** What is the difference between Deployment and StatefulSet?

Deployment manages stateless applications, treats pods as interchangeable, and doesn't guarantee pod names or order. StatefulSet manages stateful applications, provides stable network identities, ordered deployment/scaling, and persistent storage.

**Q.105** What are Kubernetes Services and their types?

Services expose pods to network traffic. Types include:
- ClusterIP: Internal cluster access (default)
- NodePort: Exposes service on each node's IP at a static port
- LoadBalancer: Exposes service using cloud provider's load balancer
- ExternalName: Maps service to DNS name

**Q.106** What is a Namespace in Kubernetes?

Namespaces provide logical isolation within a cluster. They separate resources for different teams, projects, or environments. Common namespaces include default, kube-system, and kube-public.

**Q.107** What are ConfigMaps and Secrets?

ConfigMaps store non-sensitive configuration data as key-value pairs. Secrets store sensitive information (passwords, tokens) in base64 encoded format with additional security features.

**Q.108** Explain Kubernetes Ingress.

Ingress manages external HTTP/HTTPS access to services in a cluster. It provides load balancing, SSL termination, and name-based virtual hosting. Requires an Ingress Controller to function.

**Q.109** What is a DaemonSet?

DaemonSet ensures that a copy of a pod runs on all (or selected) nodes. Used for node-level operations like log collection, monitoring agents, or network plugins.

**Q.110** What are Kubernetes probes?

Probes check container health:
- Liveness Probe: Determines if container is running (restarts if fails)
- Readiness Probe: Determines if container is ready to serve traffic
- Startup Probe: Determines if application has started (for slow-starting containers)

**Q.111** What is kubectl?

kubectl is the command-line tool for interacting with Kubernetes clusters. It communicates with the API server to deploy applications, inspect resources, and manage cluster operations.

**Q.112** Explain Kubernetes Volumes.

Volumes provide persistent storage for containers. Types include:
- emptyDir: Temporary storage deleted with pod
- hostPath: Mounts host node's filesystem
- persistentVolumeClaim: Requests persistent storage
- configMap/secret: Mounts config data
- cloud volumes: AWS EBS, Azure Disk, GCE PD

**Q.113** What is Helm?

Helm is a package manager for Kubernetes. It uses charts (packages) to define, install, and upgrade Kubernetes applications. Helm simplifies complex deployments and version management.

**Q.114** What are Kubernetes Labels and Selectors?

Labels are key-value pairs attached to objects for identification. Selectors filter objects based on labels. They're used for organizing resources and defining relationships between objects.

**Q.115** What is a Kubernetes ReplicaSet?

ReplicaSet ensures a specified number of pod replicas are running at any time. It's typically managed by Deployments and provides self-healing by replacing failed pods.

### Scenario-Based Questions

**Q.116** A pod is stuck in Pending state. How would you troubleshoot this?

Troubleshooting steps:
1. Check pod status and events:
   ```bash
   kubectl describe pod pod-name
   ```
2. Common causes:
   - Insufficient resources (CPU/memory)
   - PersistentVolumeClaim not bound
   - Node selector doesn't match any nodes
   - Image pull errors
   - Taints on nodes without tolerations
3. Check node resources:
   ```bash
   kubectl describe nodes
   kubectl top nodes
   ```
4. Check PVC status:
   ```bash
   kubectl get pvc
   ```
5. Verify image availability:
   ```bash
   kubectl get events --sort-by='.lastTimestamp'
   ```
6. Check scheduling constraints
7. Review resource requests and limits
8. Check for pod affinity/anti-affinity rules

**Q.117** How would you perform a rolling update with zero downtime?

Rolling update strategy:
1. Ensure proper resource requests/limits set
2. Configure deployment strategy:
   ```yaml
   spec:
     replicas: 3
     strategy:
       type: RollingUpdate
       rollingUpdate:
         maxSurge: 1
         maxUnavailable: 0
   ```
3. Set readiness probes to ensure traffic only to ready pods
4. Update the deployment:
   ```bash
   kubectl set image deployment/app app=app:v2
   # or
   kubectl apply -f deployment.yaml
   ```
5. Monitor the rollout:
   ```bash
   kubectl rollout status deployment/app
   ```
6. If issues occur, rollback:
   ```bash
   kubectl rollout undo deployment/app
   ```
7. Use PodDisruptionBudget to ensure minimum availability:
   ```yaml
   apiVersion: policy/v1
   kind: PodDisruptionBudget
   metadata:
     name: app-pdb
   spec:
     minAvailable: 2
     selector:
       matchLabels:
         app: myapp
   ```

**Q.118** Your application needs persistent storage. How would you implement this in Kubernetes?

Persistent storage implementation:
1. Create PersistentVolume (PV):
   ```yaml
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: my-pv
   spec:
     capacity:
       storage: 10Gi
     accessModes:
       - ReadWriteOnce
     persistentVolumeReclaimPolicy: Retain
     storageClassName: standard
     hostPath:
       path: /data
   ```
2. Create PersistentVolumeClaim (PVC):
   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: my-pvc
   spec:
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 10Gi
     storageClassName: standard
   ```
3. Use PVC in pod:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: app
   spec:
     containers:
     - name: app
       image: myapp
       volumeMounts:
       - name: storage
         mountPath: /data
     volumes:
     - name: storage
       persistentVolumeClaim:
         claimName: my-pvc
   ```
4. For stateful applications, use StatefulSet with volumeClaimTemplates
5. Consider using StorageClass for dynamic provisioning
6. Implement backup strategy for persistent data

**Q.119** How would you implement auto-scaling in Kubernetes?

Auto-scaling implementation:
1. Horizontal Pod Autoscaler (HPA):
   ```yaml
   apiVersion: autoscaling/v2
   kind: HorizontalPodAutoscaler
   metadata:
     name: app-hpa
   spec:
     scaleTargetRef:
       apiVersion: apps/v1
       kind: Deployment
       name: app
     minReplicas: 2
     maxReplicas: 10
     metrics:
     - type: Resource
       resource:
         name: cpu
         target:
           type: Utilization
           averageUtilization: 70
     - type: Resource
       resource:
         name: memory
         target:
           type: Utilization
           averageUtilization: 80
   ```
2. Install Metrics Server:
   ```bash
   kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
   ```
3. Vertical Pod Autoscaler (VPA) for resource recommendations
4. Cluster Autoscaler for node scaling:
   - Configure cloud provider autoscaling groups
   - Deploy cluster autoscaler
5. Set proper resource requests and limits
6. Monitor scaling behavior:
   ```bash
   kubectl get hpa
   kubectl describe hpa app-hpa
   ```
7. Test with load testing tools

**Q.120** Your pods are getting OOMKilled. How would you diagnose and fix this?

Diagnosis and resolution:
1. Check pod status:
   ```bash
   kubectl get pods
   kubectl describe pod pod-name
   ```
2. Review container logs before restart:
   ```bash
   kubectl logs pod-name --previous
   ```
3. Check resource usage:
   ```bash
   kubectl top pod pod-name
   kubectl top pod --containers
   ```
4. Review memory limits and requests in manifest
5. Analyze application memory usage:
   - Check for memory leaks
   - Profile application memory
   - Review application logs
6. Increase memory limits:
   ```yaml
   resources:
     requests:
       memory: "256Mi"
     limits:
       memory: "512Mi"
   ```
7. Implement monitoring and alerts
8. Consider horizontal scaling instead of vertical
9. Optimize application memory usage
10. Use ResourceQuota to prevent resource exhaustion

**Q.121** How would you secure a Kubernetes cluster?

Security best practices:
1. Enable RBAC:
   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: Role
   metadata:
     name: developer
   rules:
   - apiGroups: [""]
     resources: ["pods"]
     verbs: ["get", "list"]
   ```
2. Use NetworkPolicies for pod-to-pod communication:
   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: NetworkPolicy
   metadata:
     name: deny-all
   spec:
     podSelector: {}
     policyTypes:
     - Ingress
     - Egress
   ```
3. Implement Pod Security Standards
4. Use Secrets for sensitive data, encrypt etcd
5. Enable audit logging
6. Use namespaces for isolation
7. Scan images for vulnerabilities
8. Use private registries with authentication
9. Implement admission controllers
10. Keep Kubernetes updated
11. Limit resource usage with ResourceQuotas and LimitRanges
12. Use service mesh for mTLS (Istio, Linkerd)
13. Enable API server authentication and authorization
14. Restrict access to kubelet API

**Q.122** How would you implement blue-green deployment in Kubernetes?

Blue-green deployment implementation:
1. Create blue deployment (current version):
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-blue
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: myapp
         version: blue
     template:
       metadata:
         labels:
           app: myapp
           version: blue
       spec:
         containers:
         - name: app
           image: myapp:v1
   ```
2. Create green deployment (new version):
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-green
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: myapp
         version: green
     template:
       metadata:
         labels:
           app: myapp
           version: green
       spec:
         containers:
         - name: app
           image: myapp:v2
   ```
3. Create service pointing to blue:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: app-service
   spec:
     selector:
       app: myapp
       version: blue
     ports:
     - port: 80
   ```
4. Deploy green and test thoroughly
5. Switch traffic by updating service selector:
   ```bash
   kubectl patch service app-service -p '{"spec":{"selector":{"version":"green"}}}'
   ```
6. Monitor for issues
7. Keep blue running for quick rollback if needed
8. Once stable, delete blue deployment

**Q.123** How do you troubleshoot networking issues between pods in Kubernetes?

Troubleshooting steps:
1. Verify pods are running:
   ```bash
   kubectl get pods -o wide
   ```
2. Check service endpoints:
   ```bash
   kubectl get endpoints service-name
   ```
3. Test DNS resolution:
   ```bash
   kubectl exec pod-name -- nslookup service-name
   kubectl exec pod-name -- nslookup service-name.namespace.svc.cluster.local
   ```
4. Test connectivity:
   ```bash
   kubectl exec pod1 -- ping pod2-ip
   kubectl exec pod1 -- curl http://service-name:port
   ```
5. Check NetworkPolicies:
   ```bash
   kubectl get networkpolicies
   kubectl describe networkpolicy policy-name
   ```
6. Verify service configuration:
   ```bash
   kubectl describe service service-name
   ```
7. Check kube-proxy logs:
   ```bash
   kubectl logs -n kube-system kube-proxy-xxxxx
   ```
8. Verify CNI plugin is working correctly
9. Check iptables rules on nodes
10. Review application logs for connection errors
11. Use debugging container:
    ```bash
    kubectl run debug --rm -it --image=nicolaka/netshoot -- /bin/bash
    ```

**Q.124** Your Kubernetes cluster is experiencing high CPU usage. How would you investigate?

Investigation steps:
1. Check node CPU usage:
   ```bash
   kubectl top nodes
   ```
2. Identify high CPU pods:
   ```bash
   kubectl top pods --all-namespaces --sort-by=cpu
   ```
3. Check specific pod details:
   ```bash
   kubectl describe pod pod-name
   kubectl logs pod-name
   ```
4. Review resource requests and limits:
   ```bash
   kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.containers[*].resources}{"\n"}{end}'
   ```
5. Check for CPU throttling:
   ```bash
   kubectl exec pod-name -- cat /sys/fs/cgroup/cpu/cpu.stat
   ```
6. Identify problematic deployments
7. Review application code for inefficiencies
8. Check for runaway processes
9. Implement resource quotas:
   ```yaml
   apiVersion: v1
   kind: ResourceQuota
   metadata:
     name: cpu-quota
   spec:
     hard:
       requests.cpu: "10"
       limits.cpu: "20"
   ```
10. Consider horizontal scaling for affected applications
11. Profile applications to find hotspots
12. Add monitoring and alerting

**Q.125** How would you implement disaster recovery for a Kubernetes cluster?

Disaster recovery strategy:
1. Backup etcd regularly:
   ```bash
   ETCDCTL_API=3 etcdctl snapshot save backup.db \
     --endpoints=https://127.0.0.1:2379 \
     --cacert=/etc/kubernetes/pki/etcd/ca.crt \
     --cert=/etc/kubernetes/pki/etcd/server.crt \
     --key=/etc/kubernetes/pki/etcd/server.key
   ```
2. Backup all Kubernetes resources:
   ```bash
   kubectl get all --all-namespaces -o yaml > all-resources.yaml
   ```
3. Use Velero for cluster backups:
   ```bash
   velero backup create cluster-backup
   velero schedule create daily-backup --schedule="0 2 * * *"
   ```
4. Backup persistent volumes and data
5. Document cluster configuration
6. Maintain infrastructure as code (Terraform, etc.)
7. Test restore procedures regularly
8. Implement multi-region/multi-cluster strategy
9. Use managed Kubernetes services with built-in HA
10. Create runbooks for disaster scenarios
11. Implement monitoring and alerting
12. Practice regular DR drills

---

## Terraform

### Common Questions

**Q.126** What is Terraform and why is it used?

Terraform is an Infrastructure as Code (IaC) tool that allows you to define and provision infrastructure using declarative configuration files. It supports multiple cloud providers, enables version control of infrastructure, provides consistency, and automates infrastructure management.

**Q.127** What is the difference between Terraform and Ansible?

Terraform focuses on infrastructure provisioning and is declarative (defines desired state). Ansible focuses on configuration management and is procedural (defines steps). Terraform is better for creating infrastructure, Ansible for configuring it.

**Q.128** Explain the Terraform workflow.

Terraform workflow consists of:
1. Write: Define infrastructure in .tf files
2. Init: Initialize working directory (`terraform init`)
3. Plan: Preview changes (`terraform plan`)
4. Apply: Create/update infrastructure (`terraform apply`)
5. Destroy: Remove infrastructure (`terraform destroy`)

**Q.129** What is Terraform state?

State is a file (terraform.tfstate) that maps real-world resources to configuration. It tracks resource metadata, dependencies, and current state. Essential for Terraform to know what infrastructure it manages.

**Q.130** What are Terraform providers?

Providers are plugins that interact with APIs of cloud platforms and services (AWS, Azure, GCP, Kubernetes). They must be declared and configured in Terraform configuration.

**Q.131** Explain Terraform modules.

Modules are containers for multiple resources used together. They enable code reuse, organization, and abstraction. A module is any directory containing .tf files. Root module is the main working directory.

**Q.132** What is terraform.tfvars file?

terraform.tfvars is a variable definition file where you can set values for input variables. It's automatically loaded by Terraform and commonly used for environment-specific values.

**Q.133** What are Terraform workspaces?

Workspaces allow managing multiple states for the same configuration (dev, staging, prod). Each workspace has its own state file, enabling infrastructure isolation without duplicating code.

**Q.134** What is the purpose of terraform init?

terraform init initializes the working directory, downloads required providers, initializes backend for state storage, and prepares modules. Must be run before other commands.

**Q.135** Explain Terraform backends.

Backends determine how state is stored and operations are performed. Local backend stores state on local filesystem. Remote backends (S3, Azure Storage, Terraform Cloud) enable team collaboration, state locking, and encryption.

**Q.136** What are data sources in Terraform?

Data sources fetch information from external sources to use in configuration. They don't create resources but retrieve data about existing resources (AMIs, VPCs, etc.).

**Q.137** What is terraform plan?

terraform plan creates an execution plan showing what actions Terraform will take to achieve desired state. It's a preview before applying changes, helps catch errors, and can be saved for later application.

**Q.138** Explain resource dependencies in Terraform.

Terraform automatically determines dependencies based on resource references. You can also explicitly define dependencies using depends_on. Dependencies ensure proper resource creation order.

**Q.139** What are provisioners in Terraform?

Provisioners execute scripts on resources after creation (file, local-exec, remote-exec). They're a last resort; prefer cloud-init or configuration management tools when possible.

**Q.140** What is the difference between count and for_each?

count creates multiple instances using a number, references with index. for_each creates instances from a map/set, references by key. for_each is preferred for managing similar resources as it handles removals better.

### Scenario-Based Questions

**Q.141** Your Terraform state file is corrupted or lost. How would you recover?

Recovery steps:
1. Check for state backups:
   ```bash
   ls terraform.tfstate.backup
   ```
2. If using remote backend, check backend versioning (S3 versioning)
3. Import existing resources:
   ```bash
   terraform import aws_instance.example i-1234567890abcdef0
   ```
4. Reconstruct state for all resources
5. Verify with terraform plan
6. Prevention measures:
   - Use remote backend with versioning
   - Enable state locking
   - Regular state backups
   - Use version control for configuration
   - Never manually edit state files

**Q.142** How would you manage multiple environments (dev, staging, prod) with Terraform?

Multi-environment management:
1. Using workspaces:
   ```bash
   terraform workspace new dev
   terraform workspace new prod
   terraform workspace select dev
   ```
   ```hcl
   resource "aws_instance" "app" {
     instance_type = terraform.workspace == "prod" ? "t3.large" : "t3.micro"
   }
   ```
2. Using separate directories:
   ```
   environments/
     dev/
       main.tf
       terraform.tfvars
     prod/
       main.tf
       terraform.tfvars
   modules/
     compute/
     networking/
   ```
3. Using terraform.tfvars per environment:
   ```bash
   terraform apply -var-file="dev.tfvars"
   terraform apply -var-file="prod.tfvars"
   ```
4. Using separate state files
5. Implement consistent naming conventions
6. Use modules for shared code
7. Protect production with state locking and access controls

**Q.143** Multiple team members are working on the same Terraform project. How do you prevent conflicts?

Collaboration strategies:
1. Use remote backend with state locking:
   ```hcl
   terraform {
     backend "s3" {
       bucket         = "terraform-state-bucket"
       key            = "prod/terraform.tfstate"
       region         = "us-east-1"
       dynamodb_table = "terraform-locks"
       encrypt        = true
     }
   }
   ```
2. Create DynamoDB table for locking:
   ```hcl
   resource "aws_dynamodb_table" "terraform_locks" {
     name         = "terraform-locks"
     billing_mode = "PAY_PER_REQUEST"
     hash_key     = "LockID"
     attribute {
       name = "LockID"
       type = "S"
     }
   }
   ```
3. Implement code review process for Terraform changes
4. Use version control (Git) with branch protection
5. Run terraform plan before apply
6. Use CI/CD pipeline for Terraform execution
7. Document infrastructure changes
8. Use modules to separate concerns
9. Implement naming conventions and tagging standards
10. Regular team communication about infrastructure changes

**Q.144** Your Terraform apply is taking too long. How would you optimize it?

Optimization strategies:
1. Use targeted applies for specific resources:
   ```bash
   terraform apply -target=aws_instance.web
   ```
2. Parallelize resource creation:
   ```bash
   terraform apply -parallelism=20
   ```
3. Break large configurations into smaller modules
4. Use data sources efficiently (cache when possible)
5. Optimize provider configurations
6. Review resource dependencies
7. Use local-exec provisioners sparingly
8. Enable debug logging to identify bottlenecks:
   ```bash
   TF_LOG=DEBUG terraform apply
   ```
9. Consider using terraform refresh less frequently
10. Use -refresh=false when state is current
11. Upgrade to latest Terraform version
12. Review and optimize provider API calls

**Q.145** How would you import existing infrastructure into Terraform?

Import process:
1. Write resource configuration:
   ```hcl
   resource "aws_instance" "imported_server" {
     # Configuration matching existing resource
   }
   ```
2. Import the resource:
   ```bash
   terraform import aws_instance.imported_server i-1234567890abcdef0
   ```
3. Run terraform plan to compare
4. Adjust configuration to match actual state
5. For multiple resources, script the import:
   ```bash
   #!/bin/bash
   resources=(
     "aws_instance.web1:i-111111"
     "aws_instance.web2:i-222222"
   )
   for resource in "${resources[@]}"; do
     IFS=':' read -r tf_resource resource_id <<< "$resource"
     terraform import "$tf_resource" "$resource_id"
   done
   ```
6. Use tools like terraformer for bulk imports:
   ```bash
   terraformer import aws --resources=vpc,subnet,sg
   ```
7. Validate with terraform plan (should show no changes)
8. Document the import process
9. Test in non-production first

**Q.146** How would you handle secrets in Terraform?

Secrets management:
1. Never commit secrets to version control
2. Use environment variables:
   ```hcl
   variable "db_password" {
     type      = string
     sensitive = true
   }
   ```
   ```bash
   export TF_VAR_db_password="secret"
   ```
3. Use AWS Secrets Manager:
   ```hcl
   data "aws_secretsmanager_secret_version" "db_password" {
     secret_id = "database/password"
   }
   resource "aws_db_instance" "db" {
     password = data.aws_secretsmanager_secret_version.db_password.secret_string
   }
   ```
4. Use HashiCorp Vault:
   ```hcl
   data "vault_generic_secret" "db_creds" {
     path = "secret/database"
   }
   ```
5. Encrypt tfstate file (use encrypted S3 bucket)
6. Mark variables as sensitive:
   ```hcl
   variable "api_key" {
     type      = string
     sensitive = true
   }
   ```
7. Use .gitignore for sensitive files
8. Implement RBAC for state file access
9. Rotate secrets regularly
10. Use CI/CD secrets management

**Q.147** Your Terraform state has drifted from actual infrastructure. How do you handle this?

Drift management:
1. Detect drift with terraform plan:
   ```bash
   terraform plan -out=plan.tfplan
   ```
2. Refresh state to sync:
   ```bash
   terraform refresh
   ```
3. Review what changed and why
4. Update configuration to match desired state
5. Apply changes to fix drift:
   ```bash
   terraform apply
   ```
6. For manual changes, options:
   - Update Terraform config to match
   - Revert manual changes to match Terraform
   - Remove from state if no longer managed:
     ```bash
     terraform state rm aws_instance.example
     ```
7. Prevent drift:
   - Implement policy preventing manual changes
   - Use terraform plan in CI/CD checks
   - Enable CloudTrail/audit logs
   - Regular drift detection
   - Use automated compliance tools
   - Educate team on IaC practices

**Q.148** How would you perform a blue-green deployment using Terraform?

Blue-green deployment with Terraform:
1. Create blue environment (current):
   ```hcl
   module "blue_environment" {
     source = "./environment"
     name   = "blue"
     ami_id = "ami-old-version"
   }
   ```
2. Create green environment (new):
   ```hcl
   module "green_environment" {
     source = "./environment"
     name   = "green"
     ami_id = "ami-new-version"
   }
   ```
3. Use Route53 weighted routing:
   ```hcl
   resource "aws_route53_record" "blue" {
     zone_id = aws_route53_zone.main.zone_id
     name    = "app.example.com"
     type    = "A"
     set_identifier = "blue"
     weighted_routing_policy {
       weight = 100
     }
     alias {
       name    = module.blue_environment.alb_dns
       zone_id = module.blue_environment.alb_zone_id
     }
   }
   resource "aws_route53_record" "green" {
     zone_id = aws_route53_zone.main.zone_id
     name    = "app.example.com"
     type    = "A"
     set_identifier = "green"
     weighted_routing_policy {
       weight = 0  # Switch to 100 to cutover
     }
     alias {
       name    = module.green_environment.alb_dns
       zone_id = module.green_environment.alb_zone_id
     }
   }
   ```
4. Test green environment
5. Switch traffic by updating weights
6. Monitor and rollback if needed
7. Destroy blue environment once stable

**Q.149** How would you structure a large Terraform project?

Project structure best practices:
```
terraform-project/
├── modules/
│   ├── networking/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   ├── compute/
│   └── database/
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── terraform.tfvars
│   │   └── backend.tf
│   ├── staging/
│   └── prod/
├── global/
│   ├── iam/
│   └── route53/
├── .gitignore
└── README.md
```

Best practices:
1. Use modules for reusability
2. Separate environments
3. One state file per environment
4. Use consistent naming conventions
5. Document modules with README
6. Use variables for configurability
7. Output necessary values
8. Implement remote state
9. Use version constraints:
   ```hcl
   terraform {
     required_version = ">= 1.0"
     required_providers {
       aws = {
         source  = "hashicorp/aws"
         version = "~> 4.0"
       }
     }
   }
   ```
10. Implement tagging strategy
11. Use data sources for cross-referencing

**Q.150** How would you test Terraform code?

Testing strategies:
1. Syntax validation:
   ```bash
   terraform fmt -check
   terraform validate
   ```
2. Static analysis with tflint:
   ```bash
   tflint --init
   tflint
   ```
3. Security scanning with tfsec:
   ```bash
   tfsec .
   ```
4. Policy as code with Sentinel or OPA:
   ```bash
   terraform plan -out=plan.tfplan
   conftest test plan.tfplan
   ```
5. Unit testing with Terratest:
   ```go
   func TestTerraformBasicExample(t *testing.T) {
     terraformOptions := &terraform.Options{
       TerraformDir: "../examples/basic",
     }
     defer terraform.Destroy(t, terraformOptions)
     terraform.InitAndApply(t, terraformOptions)
     instanceID := terraform.Output(t, terraformOptions, "instance_id")
     assert.NotEmpty(t, instanceID)
   }
   ```
6. Integration testing in isolated environment
7. Plan testing in CI/CD:
   ```bash
   terraform plan -detailed-exitcode
   ```
8. Cost estimation with Infracost:
   ```bash
   infracost breakdown --path .
   ```
9. Automated testing in pipeline
10. Regular review and refactoring

---

## Jenkins

### Common Questions

**Q.151** What is Jenkins and why is it used?

Jenkins is an open-source automation server for Continuous Integration and Continuous Delivery (CI/CD). It automates building, testing, and deploying applications, supports plugins for various tools, enables rapid feedback, and improves software quality.

**Q.152** What is the difference between Jenkins freestyle project and pipeline?

Freestyle projects use GUI configuration, are less flexible, and harder to version control. Pipelines use code (Jenkinsfile), support complex workflows, are version-controlled with code, enable better visualization, and follow "Pipeline as Code" approach.

**Q.153** Explain Jenkins pipeline syntax (Declarative vs Scripted).

Declarative pipeline uses structured syntax with predefined sections (pipeline, agent, stages, steps). It's easier to learn and recommended for most use cases. Scripted pipeline uses Groovy syntax, offers more flexibility, but is more complex.

**Q.154** What is a Jenkinsfile?

A Jenkinsfile is a text file containing Jenkins pipeline definition, stored in source control with application code. It enables version control of CI/CD process and "Pipeline as Code" practice.

**Q.155** What are Jenkins agents/nodes?

Agents (or slaves) are machines that execute jobs defined in Jenkins. Master node manages the system and can execute jobs. Agent nodes execute jobs delegated by master, enabling distributed builds and parallel execution.

**Q.156** Explain Jenkins plugins.

Plugins extend Jenkins functionality. Common plugins include Git, Docker, Kubernetes, AWS, Maven, Pipeline. They're installed from Jenkins Plugin Manager and enable integration with various tools and platforms.

**Q.157** What are Jenkins credentials?

Credentials securely store sensitive information (passwords, API keys, SSH keys, certificates). They're managed through Jenkins Credentials plugin and can be scoped to specific jobs or globally.

**Q.158** What is Jenkins Blue Ocean?

Blue Ocean is a modern UI for Jenkins providing better visualization of pipelines, easier pipeline creation and editing, improved user experience, and better feedback for pipeline execution.

**Q.159** Explain Jenkins shared libraries.

Shared libraries allow sharing common pipeline code across multiple projects. They're stored in separate Git repositories, imported in Jenkinsfiles, and promote DRY (Don't Repeat Yourself) principle.

**Q.160** What are Jenkins webhooks?

Webhooks trigger Jenkins jobs automatically when events occur in external systems (Git push, pull request). They eliminate polling, provide immediate feedback, and enable event-driven CI/CD.

**Q.161** What is Jenkins multibranch pipeline?

Multibranch pipeline automatically creates pipeline jobs for each branch in a repository. It detects Jenkinsfiles in branches, enables feature branch testing, and supports pull request builds.

**Q.162** Explain Jenkins build triggers.

Build triggers start jobs automatically:
- SCM polling: Periodically checks repository
- Webhook: Triggered by external events
- Scheduled: Cron-based execution
- Upstream/downstream: Triggered by other jobs
- Manual: User-initiated

**Q.163** What are Jenkins environment variables?

Environment variables store information accessible during build execution. Jenkins provides built-in variables (BUILD_NUMBER, JOB_NAME) and allows custom variables definition.

**Q.164** What is Jenkins backup strategy?

Backup includes JENKINS_HOME directory containing:
- Job configurations
- Build history
- Plugins
- Credentials
- System configuration
Use plugins like ThinBackup or periodic filesystem backups.

**Q.165** What are Jenkins parameters?

Parameters allow passing inputs to jobs at runtime:
- String: Text input
- Choice: Dropdown selection
- Boolean: Checkbox
- File: File upload
- Password: Masked input
Enable parameterized builds for flexibility.

### Scenario-Based Questions

**Q.166** Your Jenkins build is failing intermittently. How would you troubleshoot?

Troubleshooting steps:
1. Check build logs for error patterns:
   ```groovy
   echo "Analyzing logs..."
   ```
2. Review console output for:
   - Network timeouts
   - Resource constraints
   - Race conditions
   - External dependency failures
3. Check Jenkins system logs:
   - Manage Jenkins → System Log
4. Monitor system resources:
   - CPU, memory, disk space
   - Agent availability
5. Identify flaky tests:
   ```groovy
   stage('Test') {
     steps {
       sh 'mvn test || true'
       junit 'target/surefire-reports/*.xml'
     }
   }
   ```
6. Implement retry logic:
   ```groovy
   retry(3) {
     sh 'npm test'
   }
   ```
7. Add timeout to prevent hanging:
   ```groovy
   timeout(time: 30, unit: 'MINUTES') {
     sh './build.sh'
   }
   ```
8. Check agent configuration and labels
9. Review plugin compatibility
10. Enable debug logging if needed
11. Isolate issue with minimal reproduction

**Q.167** How would you implement a complete CI/CD pipeline in Jenkins?

Complete pipeline implementation:
```groovy
pipeline {
    agent {
        label 'docker'
    }
    
    environment {
        DOCKER_REGISTRY = 'docker.io'
        APP_NAME = 'myapp'
        VERSION = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh '''
                    echo "Building application..."
                    npm install
                    npm run build
                '''
            }
        }
        
        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh 'npm run test:unit'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        sh 'npm run test:integration'
                    }
                }
            }
        }
        
        stage('Code Quality') {
            steps {
                sh 'npm run lint'
                sh 'sonar-scanner'
            }
        }
        
        stage('Security Scan') {
            steps {
                sh 'npm audit'
                sh 'trivy image ${APP_NAME}:${VERSION}'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${VERSION}")
                }
            }
        }
        
        stage('Push to Registry') {
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'docker-credentials') {
                        docker.image("${DOCKER_REGISTRY}/${APP_NAME}:${VERSION}").push()
                        docker.image("${DOCKER_REGISTRY}/${APP_NAME}:${VERSION}").push('latest')
                    }
                }
            }
        }
        
        stage('Deploy to Dev') {
            steps {
                sh 'kubectl apply -f k8s/dev/'
                sh "kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${VERSION} -n dev"
            }
        }
        
        stage('Deploy to Staging') {
            when {
                branch 'develop'
            }
            steps {
                input 'Deploy to staging?'
                sh 'kubectl apply -f k8s/staging/'
                sh "kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${VERSION} -n staging"
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                input 'Deploy to production?'
                sh 'kubectl apply -f k8s/prod/'
                sh "kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${VERSION} -n prod"
            }
        }
    }
    
    post {
        success {
            slackSend color: 'good', message: "Build ${BUILD_NUMBER} succeeded"
        }
        failure {
            slackSend color: 'danger', message: "Build ${BUILD_NUMBER} failed"
        }
        always {
            cleanWs()
        }
    }
}
```

**Q.168** Your Jenkins master is overloaded. How would you scale it?

Scaling strategies:
1. Add more agent nodes:
   ```groovy
   pipeline {
       agent {
           label 'high-performance'
       }
   }
   ```
2. Use cloud agents (AWS, Azure, Kubernetes):
   - Install Kubernetes plugin
   - Configure pod templates
   - Dynamic agent provisioning
3. Implement agent labels for workload distribution:
   ```groovy
   agent {
       label 'docker && linux'
   }
   ```
4. Configure concurrent builds:
   - Manage Jenkins → Configure System
   - Set # of executors appropriately
5. Optimize pipeline execution:
   - Use parallel stages
   - Implement caching
   - Minimize master executions
6. Archive old builds:
   ```groovy
   properties([
       buildDiscarder(logRotator(numToKeepStr: '10'))
   ])
   ```
7. Move non-critical jobs to agents
8. Implement job throttling for resource-intensive tasks
9. Use shared libraries to reduce parsing overhead
10. Consider Jenkins high availability setup
11. Monitor master performance metrics
12. Increase master resources if needed

**Q.169** How would you secure Jenkins?

Security hardening:
1. Enable security realm and authorization:
   - Matrix-based security
   - Role-based access control (RBAC)
2. Configure authentication (LDAP, AD, SAML):
   ```groovy
   // In Jenkins Configuration as Code
   jenkins:
     securityRealm:
       ldap:
         server: "ldap://ldap.example.com"
   ```
3. Use HTTPS/SSL:
   - Configure reverse proxy (Nginx, Apache)
   - Enable SSL certificates
4. Implement credential management:
   - Use Jenkins Credentials plugin
   - Scope credentials appropriately
   - Rotate credentials regularly
5. Enable CSRF protection:
   - Manage Jenkins → Configure Global Security
6. Restrict agent-to-master access
7. Install security plugins:
   - OWASP Dependency-Check
   - Script Security
8. Regular updates:
   - Jenkins core
   - Plugins
9. Audit logging:
   ```groovy
   properties([
       buildDiscarder(logRotator(artifactNumToKeepStr: '5'))
   ])
   ```
10. Network security:
    - Firewall rules
    - VPN access
11. Backup encryption
12. Scan for vulnerabilities
13. Disable unused plugins
14. Implement approval process for scripts

**Q.170** How would you migrate Jenkins to a new server?

Migration process:
1. Prepare new Jenkins server:
   - Install same Jenkins version
   - Install same Java version
2. Stop Jenkins on old server:
   ```bash
   sudo systemctl stop jenkins
   ```
3. Backup JENKINS_HOME:
   ```bash
   tar -czf jenkins_backup.tar.gz /var/lib/jenkins/
   ```
4. Transfer backup to new server:
   ```bash
   rsync -avz jenkins_backup.tar.gz user@newserver:/tmp/
   ```
5. Stop Jenkins on new server:
   ```bash
   sudo systemctl stop jenkins
   ```
6. Restore JENKINS_HOME:
   ```bash
   cd /var/lib/
   sudo tar -xzf /tmp/jenkins_backup.tar.gz
   sudo chown -R jenkins:jenkins jenkins/
   ```
7. Update configurations if needed:
   - Server URLs
   - Agent configurations
   - Webhook URLs
8. Start Jenkins:
   ```bash
   sudo systemctl start jenkins
   ```
9. Verify:
   - Jobs are present
   - Plugins are installed
   - Credentials are available
   - Agents connect successfully
10. Update DNS/load balancer
11. Test builds
12. Keep old server for rollback period
13. Document the migration

**Q.171** How do you implement secrets management in Jenkins pipelines?

Secrets management:
1. Use Jenkins Credentials:
   ```groovy
   pipeline {
       environment {
           AWS_CREDS = credentials('aws-credentials-id')
       }
       steps {
           sh '''
               aws s3 ls
               # AWS_CREDS_USR and AWS_CREDS_PSW are auto-created
           '''
       }
   }
   ```
2. Mask passwords in logs:
   ```groovy
   wrap([$class: 'MaskPasswordsBuildWrapper']) {
       sh 'echo $PASSWORD'
   }
   ```
3. Use withCredentials:
   ```groovy
   withCredentials([
       string(credentialsId: 'api-key', variable: 'API_KEY'),
       usernamePassword(credentialsId: 'db-creds', 
                       usernameVariable: 'DB_USER', 
                       passwordVariable: 'DB_PASS')
   ]) {
       sh 'curl -H "Authorization: $API_KEY" api.example.com'
   }
   ```
4. Integration with external secret managers:
   ```groovy
   // HashiCorp Vault
   withVault([
       vaultSecrets: [[
           path: 'secret/myapp',
           secretValues: [[envVar: 'DB_PASS', vaultKey: 'password']]
       ]]
   ]) {
       sh 'echo $DB_PASS'
   }
   ```
5. AWS Secrets Manager:
   ```groovy
   script {
       def secret = sh(
           script: 'aws secretsmanager get-secret-value --secret-id myapp/db',
           returnStdout: true
       ).trim()
   }
   ```
6. Never log secrets
7. Use credential IDs, not values
8. Scope credentials appropriately
9. Rotate secrets regularly
10. Audit credential access

**Q.172** Your pipeline needs to run different stages based on branch. How do you implement this?

Conditional execution:
```groovy
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo "Building..."
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                echo "Testing..."
                sh 'mvn test'
            }
        }
        
        stage('Deploy to Dev') {
            when {
                anyOf {
                    branch 'feature/*'
                    branch 'develop'
                }
            }
            steps {
                echo "Deploying to dev environment"
                sh './deploy-dev.sh'
            }
        }
        
        stage('Deploy to Staging') {
            when {
                branch 'develop'
            }
            steps {
                echo "Deploying to staging"
                sh './deploy-staging.sh'
            }
        }
        
        stage('Deploy to Production') {
            when {
                allOf {
                    branch 'main'
                    expression { currentBuild.result == 'SUCCESS' }
                }
            }
            steps {
                input 'Deploy to production?'
                echo "Deploying to production"
                sh './deploy-prod.sh'
            }
        }
        
        stage('Hotfix') {
            when {
                branch 'hotfix/*'
            }
            steps {
                echo "Deploying hotfix"
                sh './deploy-hotfix.sh'
            }
        }
    }
    
    post {
        success {
            script {
                if (env.BRANCH_NAME == 'main') {
                    mail to: 'team@example.com',
                         subject: "Production Deploy Success: ${env.JOB_NAME}",
                         body: "Build ${env.BUILD_NUMBER} deployed successfully"
                }
            }
        }
    }
}
```

**Q.173** How would you implement blue-green deployment in Jenkins?

Blue-green deployment:
```groovy
pipeline {
    agent any
    
    parameters {
        choice(name: 'DEPLOYMENT_ENV', choices: ['blue', 'green'], description: 'Target environment')
    }
    
    environment {
        APP_NAME = 'myapp'
        VERSION = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t ${APP_NAME}:${VERSION} .'
            }
        }
        
        stage('Deploy to Target Environment') {
            steps {
                script {
                    def targetEnv = params.DEPLOYMENT_ENV
                    def inactiveEnv = (targetEnv == 'blue') ? 'green' : 'blue'
                    
                    echo "Deploying to ${targetEnv} environment"
                    sh """
                        kubectl set image deployment/${APP_NAME}-${targetEnv} \
                            ${APP_NAME}=${APP_NAME}:${VERSION} \
                            -n production
                        kubectl rollout status deployment/${APP_NAME}-${targetEnv} -n production
                    """
                }
            }
        }
        
        stage('Health Check') {
            steps {
                script {
                    def targetEnv = params.DEPLOYMENT_ENV
                    sh """
                        for i in {1..10}; do
                            if curl -f http://${targetEnv}.example.com/health; then
                                echo "Health check passed"
                                exit 0
                            fi
                            sleep 10
                        done
                        echo "Health check failed"
                        exit 1
                    """
                }
            }
        }
        
        stage('Switch Traffic') {
            steps {
                input 'Switch traffic to new environment?'
                script {
                    def targetEnv = params.DEPLOYMENT_ENV
                    sh """
                        # Update load balancer or ingress
                        kubectl patch service ${APP_NAME} -p \
                            '{"spec":{"selector":{"version":"${targetEnv}"}}}'
                    """
                }
            }
        }
        
        stage('Monitor') {
            steps {
                echo "Monitoring new environment for 5 minutes"
                sleep time: 5, unit: 'MINUTES'
            }
        }
    }
    
    post {
        failure {
            script {
                echo "Deployment failed, rolling back"
                def targetEnv = params.DEPLOYMENT_ENV
                def previousEnv = (targetEnv == 'blue') ? 'green' : 'blue'
                sh """
                    kubectl patch service ${APP_NAME} -p \
                        '{"spec":{"selector":{"version":"${previousEnv}"}}}'
                """
            }
        }
    }
}
```

**Q.174** How do you handle pipeline failures and notifications?

Error handling and notifications:
```groovy
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    try {
                        sh 'mvn clean package'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Build failed: ${e.message}"
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    sh 'mvn test'
                }
            }
        }
    }
    
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
        
        success {
            mail to: 'team@example.com',
                 subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build completed successfully.\n\nCheck: ${env.BUILD_URL}"
            
            slackSend channel: '#builds',
                      color: 'good',
                      message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} succeeded"
        }
        
        failure {
            mail to: 'team@example.com',
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed.\n\nCheck: ${env.BUILD_URL}console"
            
            slackSend channel: '#builds',
                      color: 'danger',
                      message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} failed"
        }
        
        unstable {
            mail to: 'team@example.com',
                 subject: "Build Unstable: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build is unstable.\n\nCheck: ${env.BUILD_URL}"
        }
        
        changed {
            echo "Build state changed"
        }
    }
}
```

**Q.175** How would you optimize slow Jenkins builds?

Build optimization strategies:
1. Use parallel execution:
   ```groovy
   stage('Parallel Tests') {
       parallel {
           stage('Unit Tests') {
               steps { sh 'npm run test:unit' }
           }
           stage('Integration Tests') {
               steps { sh 'npm run test:integration' }
           }
           stage('E2E Tests') {
               steps { sh 'npm run test:e2e' }
           }
       }
   }
   ```
2. Implement caching:
   ```groovy
   stage('Build') {
       steps {
           sh '''
               if [ -d "node_modules" ]; then
                   echo "Using cached node_modules"
               else
                   npm install
               fi
           '''
       }
   }
   ```
3. Use Docker layer caching:
   ```groovy
   docker.build("myapp:${VERSION}", "--cache-from myapp:latest .")
   ```
4. Optimize agent selection:
   ```groovy
   agent {
       label 'high-performance && docker'
   }
   ```
5. Skip unnecessary stages:
   ```groovy
   when {
       changeset "src/**"
   }
   ```
6. Use incremental builds
7. Distribute builds across multiple agents
8. Clean workspace selectively:
   ```groovy
   post {
       always {
           cleanWs deleteDirs: true, patterns: [[pattern: 'target/**', type:
