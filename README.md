# 🚀 AWS CI/CD Pipeline — GitHub to EC2

## 📌 Project Overview

This project demonstrates a complete **CI/CD pipeline on AWS** that automatically builds and deploys a web application from a GitHub repository to an Amazon EC2 instance.

AWS services were directly configured and integrated through **AWS CodePipeline**, with GitHub configured as the source provider.

The pipeline consists of three stages:

```text
GitHub
   │
   ▼
AWS CodePipeline
   │
   ▼
AWS CodeBuild
   │
   ▼
AWS CodeDeploy
   │
   ▼
Amazon EC2
   │
   ▼
Apache HTTP Server
   │
   ▼
Web Application
```

## 🔄 CI/CD Workflow

### 1. Source — GitHub

The application source code is maintained in a GitHub repository.

The GitHub repository is configured directly as the **Source stage** of AWS CodePipeline.

When a new source revision is released through the pipeline, CodePipeline retrieves the source and passes it to the build stage.

---

### 2. Build — AWS CodeBuild

AWS CodeBuild is configured as the **Build stage** of the CodePipeline.

CodeBuild receives the source artifact from the pipeline and uses:

```text
buildspec.yml
```

to execute the configured build commands.

The build process completes successfully before the deployment stage begins.

---

### 3. Deploy — AWS CodeDeploy

AWS CodeDeploy is configured as the **Deploy stage** of CodePipeline.

The deployment uses:

```text
appspec.yml
```

and the associated deployment lifecycle scripts.

The application is deployed automatically to the target Amazon EC2 instance.

---

### 4. EC2 — Application Hosting

The EC2 instance acts as the deployment target.

AWS CodeDeploy installs/deploys the application files on the instance, while Apache HTTP Server serves the application.

The deployed application can then be accessed through the EC2 instance's public endpoint.

---

## 🏗️ Architecture

```text
                         ┌──────────────────┐
                         │      GitHub      │
                         │                  │
                         │ Application Code │
                         └────────┬─────────┘
                                  │
                                  │ Source
                                  ▼
                     ┌────────────────────────┐
                     │    AWS CodePipeline    │
                     │                        │
                     │   Source → Build       │
                     │            → Deploy    │
                     └───────────┬────────────┘
                                 │
                                 ▼
                     ┌────────────────────────┐
                     │     AWS CodeBuild      │
                     │                        │
                     │    buildspec.yml       │
                     │                        │
                     │  Build / Validation    │
                     └───────────┬────────────┘
                                 │
                                 │ Build Artifact
                                 ▼
                     ┌────────────────────────┐
                     │     AWS CodeDeploy     │
                     │                        │
                     │     appspec.yml        │
                     │   Deployment Hooks     │
                     └───────────┬────────────┘
                                 │
                                 │ Deployment
                                 ▼
                    ┌───────────────────────────┐
                    │       Amazon EC2          │
                    │                           │
                    │      Apache HTTPD         │
                    │                           │
                    │     /var/www/html         │
                    └────────────┬──────────────┘
                                 │
                                 ▼
                         🌐 Web Browser
```

## ☁️ AWS Services Used

| Service              | Role                                     |
| -------------------- | ---------------------------------------- |
| **GitHub**           | Source code repository                   |
| **AWS CodePipeline** | Orchestrates the complete CI/CD workflow |
| **AWS CodeBuild**    | Builds and validates the source          |
| **AWS CodeDeploy**   | Deploys the application to EC2           |
| **Amazon EC2**       | Application deployment target            |
| **Amazon S3**        | Stores pipeline artifacts                |
| **IAM**              | Provides required AWS permissions        |
| **Apache HTTPD**     | Serves the deployed application          |

## 📂 Repository Structure

```text
aws-cicd-pipeline/
│
├── index.html
├── buildspec.yml
├── appspec.yml
├── README.md
│
├── scripts/
│   ├── install_dependencies.sh
│   ├── after_install.sh
│   ├── start_server.sh
│   ├── stop_server.sh
│   └── validate_service.sh
│
└── screenshots/
    ├── pipeline.png
    ├── build.png
    ├── deploy.png
    └── application.png
```

## ⚙️ Pipeline Configuration

The pipeline was configured using the AWS Management Console.

### Source Stage

```text
Provider: GitHub
Connection: GitHub App
Repository: <your-repository>
Branch: main
```

### Build Stage

```text
Provider: AWS CodeBuild
Build Project: AWS-Build
Build Specification: buildspec.yml
```

### Deploy Stage

```text
Provider: AWS CodeDeploy
Application: AWS-code-deploy
Deployment Group: AWS-project-Dgroup
Deployment Configuration: CodeDeployDefault.AllAtOnce
```

## 🔄 Complete Pipeline Execution

When the pipeline is executed:

```text
1. GitHub
   │
   │ Source revision
   ▼
2. CodePipeline
   │
   ▼
3. CodeBuild
   │
   │ Build succeeds
   ▼
4. CodeDeploy
   │
   │ Deployment succeeds
   ▼
5. EC2
   │
   ▼
6. Apache
   │
   ▼
7. Live Application
```

The demonstrated pipeline successfully completed all three stages:

```text
✅ Source
✅ Build
✅ Deploy
```

## 📄 Configuration Files

### `buildspec.yml`

Defines the commands executed by AWS CodeBuild during the build process.

### `appspec.yml`

Defines how AWS CodeDeploy installs and manages the application on the EC2 instance.

### Deployment Scripts

The deployment scripts are executed during the CodeDeploy lifecycle to install dependencies, stop/start the web server, update application permissions, and validate the deployed service.

## 📸 Screenshots

### AWS CodePipeline

<img width="1910" height="1020" alt="pipeline" src="https://github.com/user-attachments/assets/5bbc7e3f-24fb-433b-8ca9-376a2e9711e0" />


### AWS CodeBuild

<img width="1916" height="1017" alt="build" src="https://github.com/user-attachments/assets/70cf61da-3c59-41de-b287-7ae139f6480d" />



### AWS CodeDeploy

<img width="1912" height="1012" alt="deploy" src="https://github.com/user-attachments/assets/15c02591-4fbb-4ac5-aed3-cc99bf0fff49" />



### Deployed Application


<img width="1916" height="1017" alt="ot" src="https://github.com/user-attachments/assets/33918791-798a-4d21-86d5-0d42584a9cc1" />




## ✅ Project Outcome

Successfully implemented an automated CI/CD workflow using:

```text
GitHub
   ↓
AWS CodePipeline
   ↓
AWS CodeBuild
   ↓
AWS CodeDeploy
   ↓
Amazon EC2
   ↓
Apache
   ↓
Web Application
```

The project demonstrates practical experience in:

* AWS CI/CD
* GitHub integration
* AWS CodePipeline
* AWS CodeBuild
* AWS CodeDeploy
* Amazon EC2
* Linux
* Bash scripting
* Apache HTTPD
* IAM
* Automated application deployment




# awscodedeploy

sudo yum update -y

sudo yum install -y ruby wget

wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install

chmod +x ./install

sudo ./install auto

sudo service codedeploy-agent status

