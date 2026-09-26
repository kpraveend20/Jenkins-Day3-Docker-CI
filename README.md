# Jenkins Day 3 - Docker CI

## Project Overview

This project demonstrates a Jenkins Multibranch Pipeline that checks out application code from GitHub, tests the application, and builds a Docker image.

The project is part of Jenkins Day 3 practical learning.

## Architecture

```text
Developer
    |
    v
GitHub Repository
    |
    +----------------+
    |                |
   main             dev
    |                |
    +--------+-------+
             |
             v
      Jenkins Multibranch
             |
             v
          Checkout
             |
             v
            Test
             |
             v
       Docker Build
             |
             v
       Docker Image
             |
             v
          SUCCESS
```

## Technologies Used

* Git
* GitHub
* Jenkins
* Jenkins Multibranch Pipeline
* Docker
* Python
* Linux Shell

## Project Structure

```text
Jenkins-Day3-Docker-CI/
│
├── app.py
├── Dockerfile
├── Jenkinsfile
└── README.md
```

## Application

The `app.py` file contains a simple Python application.

When executed, it displays:

```text
================================
 Jenkins Day 3 Docker Project
 Application is running
================================
```

## Dockerfile

The Dockerfile uses Python 3.12 Slim as the base image.

Docker performs the following steps:

1. Pulls the Python base image.
2. Creates `/app` as the working directory.
3. Copies `app.py` into the container.
4. Runs the Python application when the container starts.

## Jenkins Pipeline

The Jenkinsfile contains three stages.

### 1. Checkout

Jenkins checks out the source code from GitHub.

```groovy
checkout scm
```

### 2. Test

Jenkins verifies Python and executes the application.

```bash
python3 --version
python3 app.py
```

### 3. Docker Build

Jenkins builds a Docker image.

```bash
docker build -t jenkins-day3-docker:${BUILD_NUMBER} .
```

The Jenkins build number is used as the Docker image tag.

For example:

```text
jenkins-day3-docker:1
jenkins-day3-docker:2
jenkins-day3-docker:3
```

## Git Branches

This project uses:

```text
main
dev
```

The Jenkins Multibranch Pipeline automatically discovers the branches containing a Jenkinsfile.

## Local Docker Test

Build the Docker image manually:

```bash
docker build -t jenkins-day3-docker:test .
```

Check the image:

```bash
docker images
```

Run the container:

```bash
docker run --rm jenkins-day3-docker:test
```

Expected output:

```text
================================
 Jenkins Day 3 Docker Project
 Application is running
================================
```

## Jenkins Expected Pipeline

```text
Checkout
   ↓
Test
   ↓
Docker Build
   ↓
SUCCESS
```

## Learning Outcomes

After completing this project, I understand:

* Jenkins Multibranch Pipeline
* Jenkinsfile
* GitHub branch discovery
* Jenkins checkout
* Jenkins pipeline stages
* Dockerfile
* Docker image creation
* Jenkins `BUILD_NUMBER`
* Jenkins and Docker integration
* Basic CI workflow

## Future Enhancement

The next project will extend this workflow by adding:

```text
Docker Build
      ↓
Docker Tag
      ↓
AWS ECR Login
      ↓
Docker Push
      ↓
Amazon ECR
```

## Development Branch

This project is being tested through the Jenkins Multibranch Pipeline dev branch.
