# Java Docker + Kubernetes CI/CD

This project demonstrates a full CI/CD pipeline for the same app in Vexamsre2, but containerized and deployed to EKS
<p align="center">
  <img src="https://raw.githubusercontent.com/LoayGhreep/Vexamsre3/refs/heads/master/flow.svg" alt="Flow Diagram" width="100%"/>
  <br/>
</p>
---

## 🔧 Tech Stack

- Java 17 + Spring Boot
- Maven
- Docker
- GitHub Actions for CI/CD
- K8 YAMLs

---

## 🔁 Branch Strategy

- `develop`: for staging deployments
- `master`: for production deployments

Each branch triggers:
- Maven build
- Docker image build and tag: `ghcr.io/loayghreep/java-k8s-demo:{branch}`
- Simulated deploy to EKS via `kubectl apply` and `kubectl set image`
- Deployments to EKS is mocked with `echo`, but can be activated by replacing with real credentials and uncommenting the commands

---

## ⚙️ Deployment Flow

1. Build the app via Maven
2. Dockerize with multi-stage Dockerfile
3. Tag image with branch name
4. Simulate deployment:
   - `aws eks update-kubeconfig`
   - `kubectl apply -f k8s/*.yaml`
   - `kubectl set image ...` for rolling update

---

## ✅ Status

| Stage     | Status |
|-----------|--------|
| Build     | ✅ Done |
| Dockerize | ✅ Done |
| CI/CD     | ✅ Done |
| K8s YAMLs | ✅ Done |
| README    | ✅ Done |