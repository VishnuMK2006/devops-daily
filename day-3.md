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

