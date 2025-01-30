# Dockerized .NET API with GitHub Actions CI/CD

This is a basic **ASP.NET Core Web API** project that has been **Dockerized** and configured with **CI/CD using GitHub Actions**. When changes are pushed to the repository, the API is automatically built and deployed.

## 🛠 Features

- Basic ASP.NET Core Web API.
- Docker containerization for easy deployment.
- CI/CD pipeline using GitHub Actions.
- Automatic deployment on push.

## 🚀 Technologies Used

- **.NET 8.0** – Web API framework.
- **Docker** – Containerization.
- **GitHub Actions** – CI/CD automation.
- **Railway** (or another deployment platform).

## 🔧 Setup & Run Locally

To run this project on your local machine:

1. Clone the repository:
    ```bash
    git clone https://github.com/abulfez/dockerized-api.git
    cd dockerized-api
    ```

2. Build and run using Docker:
    ```bash
    docker build -t dockerized-api .
    docker run -p 8080:8080 dockerized-api
    ```

3. Open the API documentation:
    ```
    http://localhost:8080/swagger/index.html
    ```

## 🔄 CI/CD Workflow

This project uses **GitHub Actions** for CI/CD automation.  
Each time you push changes to the repository:

1. GitHub Actions runs the pipeline.
2. The API is built and tested.
3. The Docker image is created and pushed to a container registry (if configured).
4. The application is deployed automatically.

### 📜 GitHub Actions Workflow (`.github/workflows/deploy.yml`)

```yaml
name: Deploy API

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Set up .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'

      - name: Build Application
        run: dotnet build --configuration Release

      - name: Build Docker Image
        run: docker build -t abulfez/dockerized-api:latest .

      - name: Deploy to Server (Optional)
        run: echo "Deploy step here"
