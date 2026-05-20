# 🔥 This is fine

> *Sample project for academic and learning purposes*

This repository is a hands-on demo of how to build and publish Docker images. Perfect for learning containerization fundamentals without the hassle.

## 📄 Github Action

```yml
name: build & publish docker image

on:
  push:
    branches:
      - main

jobs:

  build-and-publish:

    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ vars.DOCKER_HUB_USERNAME }}
          password: ${{ secrets.DOCKER_HUB_TOKEN }}

      - name: Get timestamp
        id: timestamp
        run: echo "tag=$(date +'%Y%d%m%H%M%S')" >> $GITHUB_OUTPUT

      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: ./src
          file: ./src/dockerfile
          push: true
          tags: |
            ${{ vars.DOCKER_HUB_USERNAME }}/thisisfine:latest
            ${{ vars.DOCKER_HUB_USERNAME }}/thisisfine:${{ steps.timestamp.outputs.tag }}
```

## 📄 Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY video.mp4 /usr/share/nginx/html/video.mp4

EXPOSE 80
```

## 📦 Build Docker image

```shell
docker build -t thisisfine .
```

## ⚡ Run Docker image

```shell
docker run -d -p 8080:80 thisisfine
```

Once the container is running, open your browser and navigate to [http://localhost:8080](http://localhost:8080) to see the magic happen

![This is fine](frame.png)

