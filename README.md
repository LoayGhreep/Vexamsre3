# Java CI/CD Pipeline – Dev ➝ Test ➝ STG

This project is a minimal Java Spring Boot application set up with a complete GitHub Actions CI/CD pipeline across three environments: **Dev**, **Test**, and **Staging (STG)**

<p align="center">
  <img src="https://raw.githubusercontent.com/LoayGhreep/Vexamsre2/refs/heads/master/flow.svg" alt="Flow Diagram" width="100%"/>
  <br/>
</p>

---

## 📦 Application

This is a basic hello-world Spring Boot REST app with one endpoint:

```
GET /hello → "Hello, world!"
```

It's Maven-based and builds a `.jar` file using:

```bash
mvn clean package
```

The final JAR is renamed to `target/app.jar`.

---

## 🌿 Branching Strategy

This project uses a standard 3-branch environment simulation:

| Branch     | Purpose                      |
|------------|------------------------------|
| `feature/*`| Development features (PR to develop) |
| `develop`  | CI/CD runs Dev + Test deploys |
| `master`   | CI/CD runs Staging deploy only |

### ✅ Required Merge Requests:
1. `feature/cicd` → `develop` (Dev → Test deploys)
2. `develop` → `master` (Staging deploy only)

---

## ⚙️ CI/CD Flow (GitHub Actions)

The pipeline is defined in `.github/workflows/main.yml` and consists of 4 jobs:

1. **Build** (always)
2. **Deploy to DEV**
3. **Deploy to TEST** (only if branch is `develop` AND DEV succeeded)
4. **Deploy to STAGING** (only if branch is `master`)

## 🔐 Branch Protection

The `master` branch is protected via GitHub UI settings:

- ✅ PR required before merging
- ✅ Direct pushes blocked
- ✅ Only owners can merge

This was configured under **Settings → Branches → Rules**.

---

## 🚀 Simulated AWS Deployment (STAGING)

Since no specific AWS service was mentioned, the deployment was simulated using dummy SCP and SSH commands that mirror a real EC2 or even lightsail flow

### STG Job Logic:

```bash
echo "scp -i mock-key.pem target/app.jar ec2-user@1.2.3.4:/home/ec2-user/"
echo "ssh -i mock-key.pem ec2-user@1.2.3.4 'pkill -f java -jar'"
echo "ssh -i mock-key.pem ec2-user@1.2.3.4 'mv /home/ec2-user/app.jar /home/ec2-user/app-latest.jar'"
echo "ssh -i mock-key.pem ec2-user@1.2.3.4 'nohup java -jar /home/ec2-user/app-latest.jar &'"
```

### 🔒 Note:
The commands are echoed (not executed) to avoid unsafe or unverified actions. We can replace `"mock-key.pem"` with a real key and uncomment them to go live instantly

---

## ✅ Repo Summary

| Item                        | Status |
|-----------------------------|--------|
| Java app pushed             | ✅     |
| Branches: `develop`, `master`, `feature/*` | ✅ |
| GitHub Actions CI/CD        | ✅     |
| Dev → Test → STG logic      | ✅     |
| Merge PRs created           | ✅     |
| Branch protection applied   | ✅     |
| Deployment simulated        | ✅     |
