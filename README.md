# 🚀 End-to-End DevOps CI/CD Pipeline

### Java Web Application Deployment using Jenkins, Maven, Docker, Kubernetes & AWS EKS

<p align="center">
  <img src="https://img.shields.io/badge/CI%2FCD-Jenkins-red?style=for-the-badge&logo=jenkins" />
  <img src="https://img.shields.io/badge/Build-Maven-orange?style=for-the-badge&logo=apachemaven" />
  <img src="https://img.shields.io/badge/Container-Docker-blue?style=for-the-badge&logo=docker" />
  <img src="https://img.shields.io/badge/Orchestration-Kubernetes-326CE5?style=for-the-badge&logo=kubernetes" />
  <img src="https://img.shields.io/badge/Cloud-AWS%20EKS-FF9900?style=for-the-badge&logo=amazonaws" />
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge" />
</p>

---

## 📌 Project Overview

This project demonstrates a complete **End-to-End DevOps CI/CD pipeline** for a Java Web Application.

The project automates the complete application delivery process starting from source code management to production-style deployment on a Kubernetes cluster running on AWS EKS.

The pipeline automatically performs:

**GitHub → Jenkins → Maven → Docker → Docker Hub → Kubernetes → AWS EKS → LoadBalancer → Application**

---

## 🎯 Project Objective

The main objective of this project is to implement a practical DevOps workflow where application code can be:

- Stored and managed using GitHub
- Automatically built using Jenkins
- Packaged using Maven
- Containerized using Docker
- Published to Docker Hub
- Deployed into Kubernetes
- Hosted on AWS EKS
- Exposed to users through an AWS Load Balancer

This eliminates repetitive manual deployment steps and demonstrates the fundamentals of CI/CD automation.

---

# 🏗️ Architecture

```text
                         👨‍💻 Developer
                              |
                              |
                              ▼
                     ┌─────────────────┐
                     │     GitHub      │
                     │  Source Code    │
                     └────────┬────────┘
                              |
                              | Git Clone
                              ▼
                     ┌─────────────────┐
                     │     Jenkins     │
                     │    CI / CD      │
                     └────────┬────────┘
                              |
                ┌─────────────┼─────────────┐
                │             │             │
                ▼             ▼             ▼
           ┌────────┐   ┌──────────┐   ┌──────────┐
           │ Maven  │   │  Docker  │   │  Kubectl │
           │ Build  │   │  Build   │   │  Deploy  │
           └────┬───┘   └────┬─────┘   └────┬─────┘
                │            │              │
                ▼            ▼              │
          ┌──────────┐  ┌─────────────┐    │
          │  WAR     │  │ Docker Hub  │    │
          │  File    │  │   Registry  │    │
          └──────────┘  └──────┬──────┘    │
                               │            │
                               └──────┬─────┘
                                      ▼
                              ┌───────────────┐
                              │    AWS EKS    │
                              │  Kubernetes   │
                              │    Cluster    │
                              └───────┬───────┘
                                      |
                         ┌────────────┴────────────┐
                         │                         │
                         ▼                         ▼
                   ┌────────────┐           ┌────────────┐
                   │    Pod 1   │           │    Pod 2   │
                   │   Tomcat   │           │   Tomcat   │
                   │ Java Web   │           │ Java Web   │
                   │ Application│           │ Application│
                   └──────┬─────┘           └──────┬─────┘
                          │                          │
                          └────────────┬─────────────┘
                                       ▼
                              ┌─────────────────┐
                              │ AWS LoadBalancer│
                              └────────┬────────┘
                                       |
                                       ▼
                              🌐 Web Application
```

---

# 🔄 CI/CD Workflow

The complete pipeline follows these stages:

```text
1. Developer pushes code
           ↓
2. GitHub stores source code
           ↓
3. Jenkins clones repository
           ↓
4. Maven builds the application
           ↓
5. WAR file is generated
           ↓
6. Docker creates container image
           ↓
7. Image pushed to Docker Hub
           ↓
8. Jenkins deploys to Kubernetes
           ↓
9. Kubernetes creates application Pods
           ↓
10. AWS LoadBalancer exposes application
           ↓
11. User accesses application
```

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| ☕ Java | Application development |
| 📦 Maven | Build and package Java application |
| 🐙 GitHub | Source Code Management |
| 🔨 Jenkins | CI/CD automation |
| 🐳 Docker | Application containerization |
| 🐳 Docker Hub | Container image registry |
| ☸️ Kubernetes | Container orchestration |
| ☁️ AWS EKS | Managed Kubernetes service |
| 🔐 AWS IAM | AWS authentication and permissions |
| ⚖️ AWS Load Balancer | External application access |
| 🐧 Ubuntu | Server operating system |
| 🐱 Apache Tomcat | Java Web Application Server |
| 💻 Linux | Server administration |

---

# 📂 Project Structure

```text
maven-web-app/
│
├── src/
│   └── main/
│       └── webapp/
│
├── target/
│   └── maven-web-app.war
│
├── Dockerfile
├── k8s-deploy.yml
├── pom.xml
├── Jenkinsfile
└── README.md
```

---

# 1️⃣ GitHub

GitHub is used as the **Source Code Management (SCM)** platform.

Repository:

```text
https://github.com/Saf1111/maven-web-app.git
```

Jenkins retrieves the application source code from this repository during the pipeline execution.

---

# 2️⃣ Jenkins

Jenkins is used as the **CI/CD automation server**.

Jenkins performs the complete automated workflow:

```text
Clone
  ↓
Build
  ↓
Dockerize
  ↓
Push
  ↓
Deploy
```

### Jenkins Pipeline Stages

```text
┌──────────────────────────┐
│       Clone Repo         │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│      Maven Build         │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│      Docker Build        │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│      Docker Push         │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│     Kubernetes Deploy    │
└──────────────────────────┘
```

---

# 3️⃣ Maven Build

Maven is responsible for compiling and packaging the Java application.

Command:

```bash
mvn clean package
```

The build generates:

```text
target/maven-web-app.war
```

The WAR file is then used to create the Docker image.

---

# 4️⃣ Docker

Docker is used to containerize the Java web application.

The Docker image contains:

```text
Docker Container
│
└── Apache Tomcat
      │
      └── maven-web-app.war
```

Docker image:

```text
safwan112/mavenwebapp:latest
```

Build command:

```bash
docker build -t safwan112/mavenwebapp:latest .
```

---

# 5️⃣ Docker Hub

Docker Hub is used as the container image registry.

The Jenkins pipeline authenticates with Docker Hub using Jenkins Credentials and pushes the generated image.

```bash
docker push safwan112/mavenwebapp:latest
```

Image:

```text
Docker Hub
└── safwan112
      └── mavenwebapp
            └── latest
```

---

# 6️⃣ Kubernetes

Kubernetes is responsible for running and managing the application containers.

The deployment uses:

```text
Replicas: 2
Container Port: 8080
Service Type: LoadBalancer
```

### Kubernetes Resources

```text
Kubernetes Cluster
│
├── Deployment
│
├── Pod 1
│
├── Pod 2
│
└── Service
      │
      └── LoadBalancer
```

---

# 7️⃣ AWS EKS

Amazon Elastic Kubernetes Service (EKS) is used to host the Kubernetes cluster.

The cluster contains multiple worker nodes where the application Pods are scheduled.

```text
AWS
│
└── EKS Cluster
      │
      ├── Worker Node 1
      │     └── Application Pod
      │
      └── Worker Node 2
            └── Application Pod
```

---

# 8️⃣ AWS IAM

AWS IAM is used to provide AWS permissions to the EC2 instances involved in the project.

The EC2 instances use an IAM role to communicate with AWS services without manually configuring AWS access keys.

Example role:

```text
eksroleec2
```

---

# 9️⃣ Kubernetes Deployment

The Kubernetes deployment uses the Docker image:

```yaml
image: safwan112/mavenwebapp:latest
```

Container:

```yaml
name: mavenwebappcontainer
```

Container port:

```yaml
containerPort: 8080
```

Replicas:

```yaml
replicas: 2
```

---

# 🔟 Kubernetes Service

The application is exposed using a Kubernetes `LoadBalancer` service.

```text
Service Type:

LoadBalancer
```

Traffic flow:

```text
Internet
    ↓
AWS Load Balancer
    ↓
Kubernetes Service
    ↓
Application Pods
    ↓
Tomcat : 8080
```

---

# 🌐 Application Access

The application is deployed through the AWS Load Balancer.

Because the WAR file is named:

```text
maven-web-app.war
```

Tomcat deploys the application under:

```text
/maven-web-app/
```

Therefore the application is accessed using:

```text
http://<LOAD-BALANCER-DNS>/maven-web-app/
```

---

# 🐱 Why Apache Tomcat?

The application is packaged as a Java Web Application WAR file.

```text
maven-web-app.war
```

Tomcat acts as the Java Web Application Server responsible for:

- Deploying the WAR file
- Running the Java web application
- Handling HTTP requests
- Listening on port 8080

Application flow:

```text
WAR File
   ↓
Apache Tomcat
   ↓
Java Web Application
   ↓
HTTP : 8080
```

---

# 🔐 Jenkins Docker Hub Credentials

Docker Hub authentication is handled securely through Jenkins Credentials.

Credential ID:

```text
dockerhub
```

The Docker Hub access token is stored inside Jenkins and is not hardcoded into the pipeline.

The pipeline uses:

```groovy
withCredentials([usernamePassword(
    credentialsId: 'dockerhub',
    usernameVariable: 'DOCKER_USERNAME',
    passwordVariable: 'DOCKER_PASSWORD'
)])
```

This prevents the Docker Hub password/token from being directly written into the Jenkinsfile.

---

# 📜 Jenkinsfile

```groovy
pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Saf1111/maven-web-app.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t safwan112/mavenwebapp:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {

                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                        -u "$DOCKER_USERNAME" --password-stdin

                        docker push safwan112/mavenwebapp:latest

                        docker logout
                    '''
                }
            }
        }

        stage('K8s Deploy') {
            steps {
                sh 'kubectl apply -f k8s-deploy.yml'
            }
        }
    }
}
```

---

# 🧪 Kubernetes Verification

### Check Cluster Nodes

```bash
kubectl get nodes
```

Expected:

```text
NAME                             STATUS
ip-xxx-xxx-xxx-xxx.ec2.internal  Ready
ip-xxx-xxx-xxx-xxx.ec2.internal  Ready
```

---

### Check Pods

```bash
kubectl get pods
```

Expected:

```text
NAME                                    READY   STATUS
mavenwebappdeployment-xxxxx-xxxxx       1/1     Running
mavenwebappdeployment-xxxxx-xxxxx       1/1     Running
```

---

### Check Deployment

```bash
kubectl get deployment
```

---

### Check Service

```bash
kubectl get svc
```

Expected:

```text
NAME             TYPE           EXTERNAL-IP
mavenwebappsvc   LoadBalancer   <AWS-LOAD-BALANCER-DNS>
```

---

### Check Application Image

```bash
kubectl get deployment mavenwebappdeployment \
-o jsonpath='{.spec.template.spec.containers[*].image}'
```

Expected:

```text
safwan112/mavenwebapp:latest
```

---

# 📊 Successful Pipeline

The Jenkins pipeline successfully performs:

```text
✅ GitHub Repository Clone
        ↓
✅ Maven Build
        ↓
✅ WAR File Generation
        ↓
✅ Docker Image Build
        ↓
✅ Docker Hub Authentication
        ↓
✅ Docker Image Push
        ↓
✅ Kubernetes Deployment
        ↓
✅ EKS Pod Creation
        ↓
✅ LoadBalancer Creation
        ↓
✅ Application Deployment
        ↓
✅ Application Access
```

---

# 🛠️ Troubleshooting Experience

During deployment, the Kubernetes Pods initially reported:

```text
ErrImagePull
```

The issue was identified using:

```bash
kubectl describe pod <pod-name>
```

The Kubernetes deployment was attempting to pull:

```text
vinodses/mavenwebapp
```

while the correct Docker image was:

```text
safwan112/mavenwebapp:latest
```

The deployment image was corrected using:

```bash
kubectl set image deployment/mavenwebappdeployment \
mavenwebappcontainer=safwan112/mavenwebapp:latest
```

After updating the image:

```text
Pod 1 → Running
Pod 2 → Running
```

This demonstrated practical Kubernetes troubleshooting and deployment debugging.

---

# 📚 DevOps Concepts Demonstrated

This project provides hands-on experience with:

### Source Control
- Git
- GitHub
- Repository management

### Continuous Integration
- Jenkins
- Automated builds
- Maven

### Containerization
- Docker
- Dockerfile
- Docker images
- Docker Hub

### Container Orchestration
- Kubernetes
- Deployments
- Pods
- Services
- Replicas
- LoadBalancer

### Cloud
- AWS EC2
- AWS IAM
- AWS EKS
- AWS Load Balancer

### Linux Administration
- Ubuntu
- Shell commands
- Package installation
- Service management

### Troubleshooting
- Jenkins build troubleshooting
- Docker authentication
- Kubernetes image pull errors
- Pod troubleshooting
- Deployment verification

---

# 💡 Key Learning Outcomes

Through this project, I gained practical knowledge of how a modern DevOps deployment pipeline works from source code to a running application.

I learned how to:

- Build Java applications using Maven
- Manage source code using GitHub
- Automate CI/CD using Jenkins
- Create Docker images
- Push container images to Docker Hub
- Deploy applications using Kubernetes
- Create Kubernetes Deployments and Services
- Work with AWS EKS
- Configure EC2 instances for DevOps tools
- Use IAM roles for AWS authentication
- Expose Kubernetes applications using LoadBalancer
- Troubleshoot Kubernetes deployment issues
- Verify application availability after deployment

---

# 🚀 End-to-End Deployment Flow

```text
                    SOURCE
                       │
                       ▼
                  ┌─────────┐
                  │ GitHub  │
                  └────┬────┘
                       │
                       ▼
                  ┌─────────┐
                  │ Jenkins │
                  └────┬────┘
                       │
                       ▼
                  ┌─────────┐
                  │  Maven  │
                  └────┬────┘
                       │
                       ▼
                maven-web-app.war
                       │
                       ▼
                  ┌─────────┐
                  │ Docker  │
                  └────┬────┘
                       │
                       ▼
                  ┌────────────┐
                  │ Docker Hub │
                  └─────┬──────┘
                        │
                        ▼
                   ┌─────────┐
                   │ AWS EKS │
                   └────┬────┘
                        │
                ┌───────┴────────┐
                ▼                ▼
             ┌───────┐       ┌───────┐
             │ Pod 1 │       │ Pod 2 │
             │Tomcat │       │Tomcat │
             └───┬───┘       └───┬───┘
                 │               │
                 └───────┬───────┘
                         ▼
                 ┌──────────────┐
                 │ LoadBalancer │
                 └───────┬──────┘
                         │
                         ▼
                     🌐 USER
```

---

# ⭐ Project Highlights

- 🔄 Automated CI/CD Pipeline
- 🐳 Docker Containerization
- ☸️ Kubernetes Deployment
- ☁️ AWS EKS Infrastructure
- 🔐 IAM-based AWS Authentication
- 📦 Docker Hub Registry
- ⚖️ LoadBalancer-based Application Exposure
- 🛠️ Real-world Troubleshooting
- 📈 Scalable Kubernetes Deployment
- 🚀 End-to-End DevOps Implementation

---

# 👨‍💻 Author

**Safwan S**

B.Tech Information Technology

Interested in:

```text
DevOps | Cloud | Kubernetes | AWS | CI/CD | DevSecOps
```

---

# 📌 Conclusion

This project demonstrates how DevOps tools can be integrated to create an automated application delivery pipeline.

Instead of manually building and deploying the application, Jenkins automates the workflow from source code retrieval to Kubernetes deployment.

The final architecture combines:

```text
GitHub
   +
Jenkins
   +
Maven
   +
Docker
   +
Docker Hub
   +
Kubernetes
   +
AWS EKS
   +
LoadBalancer
```

resulting in a complete **End-to-End CI/CD deployment pipeline**.

---

## ⭐ If you found this project useful, consider giving the repository a star!
