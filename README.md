# Enterprise CI/CD Pipeline for Java Application on Amazon EKS

A complete enterprise-grade CI/CD pipeline for a Java application, automating the full delivery workflow from source code integration to deployment on Amazon EKS.

## Architecture / Pipeline Flow

**CI Pipeline — 9 Stages**
1. Clean Workspace
2. Source Code Integration (GitHub)
3. Build Application (Maven)
4. Code Quality Analysis (SonarQube)
5. Quality Gate Validation
6. Artifact Publishing (Nexus Repository)
7. Docker Image Build
8. Security Scanning (Trivy)
9. Docker Image Push (Docker Hub)

**CD Pipeline — 2 Stages**
1. Fetch Kubernetes manifest files from GitHub
2. Deploy application to Amazon EKS using Kubernetes manifests

```
GitHub → Jenkins (CI: 9 stages) → Docker Hub
                                        │
                                        ▼
                          Jenkins (CD) → Amazon EKS
```
*(Replace with an actual diagram image for a stronger visual.)*

## Tech Stack

| Category | Tools |
|---|---|
| CI/CD Orchestration | Jenkins |
| Build Tool | Maven |
| Code Quality | SonarQube (with Quality Gate) |
| Artifact Repository | Nexus |
| Containerization | Docker |
| Security Scanning | Trivy |
| Image Registry | Docker Hub |
| Orchestration / Cloud | Amazon EKS, Kubernetes, AWS |

## Repository Structure

```
├── Jenkinsfile               # CI pipeline definition
├── pom.xml                   # Maven build config
├── Dockerfile
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
├── sonar-project.properties
└── README.md
```
*(Update to match your actual repo layout.)*

## How to Run

1. **Prerequisites**: Jenkins with Docker, kubectl, and AWS CLI configured; access to an EKS cluster; SonarQube and Nexus reachable from Jenkins; Docker Hub credentials configured.
2. CI pipeline runs stages 1–9 automatically on push, ending with the image pushed to Docker Hub.
3. CD pipeline pulls the latest Kubernetes manifests from GitHub and applies them to the EKS cluster.
4. Verify rollout:
   ```
   kubectl get pods
   kubectl get svc
   ```

## What I Learned

- Artifact management with Nexus Repository
- Deploying applications on Amazon EKS
- Cloud-native CI/CD workflows on AWS
- Production-style DevSecOps practices (quality gates + security scanning as pipeline gates, not afterthoughts)

