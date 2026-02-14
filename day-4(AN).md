# JENKINS SET UP AND HANDSON

# Jenkins Setup

This document describes:

- Jenkins installation using WAR file
- Initial Jenkins configuration
- Creating the first Jenkins project
- Building and running a Dockerized application
- Using Freestyle and Pipeline methods


## Prerequisites

- Java installed (JDK 11 or later recommended)
- Docker installed
- Node.js and npm installed
- Git installed

Verify installations:

```bash
java -version
docker -v
node -v
npm -v
git --version
````
---

# Jenkins Installation

## Step 1: Download Jenkins

Visit:

[https://www.jenkins.io/download/](https://www.jenkins.io/download/)

Download:

**Generic Java package (.war)**



## Step 2: Run Jenkins

Navigate to the download directory:

```bash
cd ~/Downloads
```

Run Jenkins:

```bash
java -jar jenkins.war
```

<img width="1920" height="785" alt="image" src="https://github.com/user-attachments/assets/b1b6ef67-c13c-4756-ad7a-0e361fe25f25" />

## Step 3: Access Jenkins

Open browser:

```
http://localhost:8080
```

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/367bf79a-9650-493a-b8c9-87a9d22265e5" />

## Step 4: Unlock Jenkins

Retrieve initial admin password:

```bash
cat ~/.jenkins/secrets/initialAdminPassword
```

Paste into Jenkins UI.


## Step 5: Install Plugins

Select:

✔ Install Suggested Plugins


## Step 6: Create Admin User

Example credentials:

```
Username: root
Password: root
```

Store credentials securely.
<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/6c155b22-c890-428e-b19c-3aa8cc53a11f" />

---

# First Project Setup

## Repository Used

```
https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git
```



# Method 1: Freestyle Project

## Step 1: Create Job

1. Jenkins Dashboard → New Item
2. Enter project name
3. Select **Freestyle Project**
4. Click OK



## Step 2: Source Code Management

Select:

✔ Git

Repository URL:

```
https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git
```

Branch:

```
main
```

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/a838281b-254d-4f1c-bd81-ca5569483019" />

## Step 3: Build Steps

Add **Execute Shell**

```bash

#Add Each build as new build
echo "Installing dependencies..."  #Build 1
npm install

echo "Building project..."  #Build 2
npm run build || true

echo "Building Docker image..." #Build 3
docker build -t mywebsite:v1 .

echo "Running Docker container..." #Build 4
docker run -d -p 3000:3000 mywebsite:v1

echo "Server is running from Jenkins"  #Build 5
```
<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/fbe568e7-70b8-4021-abc5-664967be6425" />

## Step 4: Save and Build

Click:

✔ Apply
✔ Save
✔ Build Now


## Output screen
<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/019ea09d-9a89-4f8c-b836-975befe3721b" />

## Logs
`Started by user vishnumanikandan`<br>
Running as SYSTEM<br>
`Building in workspace /home/vishnumanikandan/.jenkins/workspace/git automation`<br>
[WS-CLEANUP] Deleting project workspace...<br>
[WS-CLEANUP] Deferred wipeout is used...<br>
The recommended git tool is: NONE<br>
No credentials specified<br>
Cloning the remote Git repository<br>
`Cloning repository` <br>
https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git<br>
 > git init /home/vishnumanikandan/.jenkins/workspace/git automation # timeout=10<br>
Fetching upstream changes from https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git<br>
 > git --version # timeout=10<br>
 > git --version # 'git version 2.43.0'<br>
 > git fetch --tags --force --progress -- https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git +refs/heads/*:refs/remotes/origin/* # timeout=10<br>
 > git config remote.origin.url https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git # timeout=10<br>
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10<br>
Avoid second fetch<br>
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10<br>
Checking out Revision aea6121318a52d8cfbd82f7c5171907a1f24b4f7 (refs/remotes/origin/main)<br>
 > git config core.sparsecheckout # timeout=10<br>
 > git checkout -f aea6121318a52d8cfbd82f7c5171907a1f24b4f7 # timeout=10<br>
Commit message: "Merge pull request #2 from VishnuMK2006/mian"<br>
First time build. Skipping changelog.<br>
[git automation] $ /bin/sh -xe /tmp/jenkins451065861153576153.sh<br>

`+ echo 🚀 Installing dependencies...`<br>
🚀 Installing dependencies...<br>
+ npm install<br>
npm WARN EBADENGINE Unsupported engine {<br>
npm WARN EBADENGINE   package: 'react-router@7.1.5',<br>
npm WARN EBADENGINE   required: { node: '>=20.0.0' },<br>
npm WARN EBADENGINE   current: { node: 'v18.19.1', npm: '9.2.0' }<br>
npm WARN EBADENGINE }<br>
npm WARN EBADENGINE Unsupported engine {<br>
npm WARN EBADENGINE   package: 'react-router-dom@7.1.5',<br>
npm WARN EBADENGINE   required: { node: '>=20.0.0' },<br>
npm WARN EBADENGINE   current: { node: 'v18.19.1', npm: '9.2.0' }<br>
npm WARN EBADENGINE }<br>
<br>
added 260 packages, and audited 261 packages in 3s<br>
<br>
57 packages are looking for funding<br>
  run `npm fund` for details<br>
<br>
10 vulnerabilities (3 low, 6 moderate, 1 high)<br>
<br>
To address all issues, run:<br>
  npm audit fix<br>
<br>
Run `npm audit` for details.<br>

`+ echo 🏗 Building project...`<br>
🏗 Building project...<br>
+ npm run build<br>
<br>
> sungo-react@0.0.0 build<br>
> tsc -b && vite build<br>
<br>
vite v6.1.0 building for production...<br>
transforming...<br>
DEPRECATION WARNING [import]: Sass @import rules are deprecated and will be removed in Dart Sass 3.0.0.<br>
<br>
More info and automated migrator: https://sass-lang.com/d/import<br>
<br>
17 │ @import "_mixins";<br>
19 │ @import "_variables";<br>
21 │ @import "_buttons";<br>
23 │ @import "_typography";<br>
26 │ @import "_customDropdown";<br>
<br>
WARNING: 21 repetitive deprecation warnings omitted.<br>
<br>
✓ 764 modules transformed.<br>
rendering chunks...<br>
computing gzip size...<br>
dist/index.html 0.51 kB<br>
dist/assets/index.css 501.26 kB<br>
dist/assets/index.js 792.77 kB<br>
<br>
(!) Some chunks are larger than 500 kB after minification.<br>
✓ built in 2.95s<br>

[git automation] $ /bin/sh -xe /tmp/jenkins6770705363029805810.sh<br>

`+ echo 🐳 Building Docker image...`<br>
🐳 Building Docker image...<br>
+ docker build -t mywebsite:v1 .<br>
<br>
#0 building with "default" instance using docker driver<br>
#1 load build definition from Dockerfile<br>
#2 load metadata for node:20-alpine<br>
#3 load metadata for nginx:1.27-alpine<br>
#4 load .dockerignore<br>
#5 FROM node:20-alpine<br>
#6 FROM nginx:1.27-alpine<br>
#7 load build context<br>
#8 WORKDIR /app<br>
#9 RUN npm install<br>
#10 COPY . .<br>
#11 RUN rm /etc/nginx/conf.d/default.conf<br>
#12 COPY package*.json ./<br>
#13 RUN npm run build<br>
#14 COPY nginx.conf<br>
#15 COPY dist<br>
#16 exporting to image<br>
#16 naming to docker.io/library/mywebsite:v1<br>
#16 DONE<br>

[git automation] $ /bin/sh -xe /tmp/jenkins13552382043254450619.sh<br>

`+ echo Server is running from jenkins`<br>
Server is running from jenkins<br>
`+ docker run -d -p 3000:3000 mywebsite:v1`<br>
ad6a9c6418879f530f0d6e0508495c86ca6053dabd7dde08918e8239012389a2<br>
<br>
`Finished: SUCCESS`


---

# Method 2: Freestyle Project with Triggers
## Step 1: Enable Build Trigger

In job configuration:

✔ Build periodically

Use cron expression generated from:

[https://crontab.guru/](https://crontab.guru/)

Example:

```
H/5 * * * *
```

(Runs every 5 minutes)


## Step 2: Save Job

✔ Save

Jenkins will trigger builds automatically.

---

# Method 3: Pipeline Project

## Step 1: Create Pipeline Job

1. Jenkins Dashboard → New Item
2. Enter name
3. Select **Pipeline**
4. Click OK


## Step 2: Pipeline Script

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "mywebsite"
        TAG = "v1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'npm install'
                sh 'npm run build || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop mycontainer || true
                docker rm mycontainer || true
                docker run -d -p 3000:3000 --name mycontainer $IMAGE_NAME:$TAG
                '''
            }
        }
    }
}
```

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/45362ee8-19d5-498d-8946-bd099c74d599" />

## Step 3: Save and Run

✔ Save
✔ Build Now

## Pipeline

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/4b38471d-234b-4c20-95da-3a8ca20f59ab" />

# Verification

Check running containers:

```bash
docker ps
```

Access application:

```
http://localhost:3000
```
# Final Output Screen

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/019ea09d-9a89-4f8c-b836-975befe3721b" />
