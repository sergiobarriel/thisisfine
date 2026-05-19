# This is fine!

## Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY video.mp4 /usr/share/nginx/html/video.mp4

EXPOSE 80
```

## Build Docker image

```shell
docker build -t thisisfine .
```

## Run Docker image

```shell
docker run -d -p 8080:80 thisisfine
```

Open [http://localhost:8080](http://localhost:8080)