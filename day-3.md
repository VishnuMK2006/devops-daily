## 1)Get free project

```bash
https://themewagon.com/theme-price/free/
```


## 2 Build Custom Docker Image (Node App)

```bash
docker build -t mywebsite:v1 .
docker images
```

Run and test:

```bash
docker run -d -p 3000:3000 sample:v1
docker ps
```

Stop container:

```bash
docker stop <container_id>
docker rm <container_id>
```


#  NGINX WORKFLOW


## 3) Pull Nginx Image

```bash
docker pull nginx:alpine
docker images
```

## 4) Test Nginx (Check if Working)

```bash
docker run -d -p 8080:80 nginx:alpine
docker ps
```

Test in browser:

```bash
curl localhost:8080
```

Stop & remove test container:

```bash
docker stop <container_id>
docker rm <container_id>
```

## 5) Build Your React / Web App

```bash
npm install
npm run build
```

This creates:

```
dist/   or   build/
```

## 6) Deploy Web App into Nginx Path

Run nginx with volume mapping:

```bash
docker run -d \
  --name mynginx \
  -p 8080:80 \
  -v $(pwd)/dist:/usr/share/nginx/html \
  nginx:alpine
```

Now your app is served by nginx.

Check:

```bash
docker ps
```

Test:

```
http://localhost:8080
```


## 7) Stop Container

```bash
docker stop mynginx
```


## 8) Delete Container

```bash
docker rm mynginx
```

Nice workflow notes 👍
Let’s add a clean **“Afternoon Session – Jenkins Installation & Setup”** section.

---

# AFTERNOON SESSION — JENKINS INSTALLATION


## 1️ Update system

```bash
sudo apt update
sudo apt upgrade -y
```

---

##  2️ Install Java (Jenkins requirement)

Check if Java exists:

```bash
java -version
```

If not installed:

```bash
sudo apt install openjdk-17-jdk -y
```

Verify:

```bash
java -version
```

---

##  3️ Add Jenkins repository key

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

---

## 4️ Add Jenkins repository

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

## 5️ Install Jenkins

```bash
sudo apt update
sudo apt install jenkins -y
```

---

## 6️ Start Jenkins

```bash
sudo systemctl start jenkins
```

Enable at boot:

```bash
sudo systemctl enable jenkins
```

Check status:

```bash
sudo systemctl status jenkins
```

---

##  7 Open Jenkins in browser

Default port:

```
http://localhost:8080
```

## 🔹 Allow firewall (if enabled)

```bash
sudo ufw allow 8080
sudo ufw reload
```

---

## 🔹 Restart Jenkins

```bash
sudo systemctl restart jenkins
```
