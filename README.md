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

Docker networking enables communication between containers
