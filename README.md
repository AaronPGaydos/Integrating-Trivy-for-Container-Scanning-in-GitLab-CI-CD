# Integrating-Trivy-for-Container-Scanning-in-GitLab-CI-CD


# 1. Set The Scene

This is a mock internal service packaged with Docker.

**Business Context**: If deployed insecurely, attackers could exploit container vulnerabilities.

📸 **Screenshot**: Dockerfile

<img width="393" height="101" alt="image" src="https://github.com/user-attachments/assets/737adfad-3d04-4b75-97af-e1858bfb6ae8" />

Create a sample app with Docker support.

## 2. SIMULATE THE CHAOS

This pipeline **builds a vulnerable base image** (`python:3.10-slim`) but still passes ✅.

📸 Screenshot: Green pipeline success despite CVEs.

<img width="1003" height="375" alt="image" src="https://github.com/user-attachments/assets/3feef5c0-f694-49e3-8c38-7776af6cf33b" />

📚 Learning Bite: Most breaches come from known, unpatched CVEs. Without scanning, CI/CD lets these slip into production.

## 3. ROOT CAUSE ANALYSIS

❓ **How would we even know this container has CVEs?**

Using [Trivy](https://aquasecurity.github.io/trivy/):

```bash
trivy image python:3.10-slim
```

<img width="897" height="373" alt="image" src="https://github.com/user-attachments/assets/33b280ea-3be7-4d25-a8f9-74ad0d659a53" />

📚 Tool Tip: Use --severity HIGH,CRITICAL to focus on urgent issues.

<img width="869" height="337" alt="image" src="https://github.com/user-attachments/assets/57045d7c-319a-40f7-87eb-422393af743a" />

📚 Learning Bite: Logs + vulnerability databases = forensic tools for containers.

## 4. REMEDIATION AND AUTOMATION

Change the .gitlab-ci.yml file to use Trivy to scan for CVEs. If any CVEs are detected the pipeline will complete the build but fail during a Trivy scan.

<img width="974" height="156" alt="image" src="https://github.com/user-attachments/assets/d850486e-685d-403f-8f5a-dced575208e4" />

## 📦 FINAL DELIVERABLES

/Dockerfile – sample app

/.gitlab-ci.yml – pipeline config

/app.py - application

✅ Built a containerized app (with Dockerfile + app.py)

✅ Created a GitLab CI/CD pipeline that builds and scans Docker images

✅ Integrated Trivy to fail builds on high/critical CVEs

✅ Externalized scan logic into a reusable trivy_scan.sh script

✅ Learned how to simulate chaos (vulnerable images), investigate, remediate, and enforce security in CI/CD
