
## 1️⃣ Workflow ka naam

```yaml
name: Node.js CI
```

👉 Ye workflow ka **display name** hai
GitHub Actions tab mein ye naam show hota hai.

---

## 2️⃣ Workflow kab run hoga (Triggers)

```yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```

👉 Matlab:

* Jab **main branch par push** hoga
* Ya **main branch ke liye PR** banega
  👉 Tab ye workflow automatically run hoga

💡 Real life:

> Code push = pipeline start

---

## 3️⃣ Permissions

```yaml
permissions:
  contents: write
```

👉 Workflow ko repo ke content **write** karne ki ijazat
Iska use:

* CD repo update
* commit & push

---

## 4️⃣ Global Environment Variable

```yaml
env:
  IMAGE_TAG: ${{ github.sha }}
```

👉 `github.sha` = current commit ka **unique hash**
👉 Isko Docker image tag ke liye use kar rahe ho

💡 Fayda:

* Har build ka **unique image**
* Rollback easy

---

## 5️⃣ JOB 1 – Compile (Frontend + Backend JS check)

```yaml
jobs:
  compile:
    runs-on: ubuntu-latest
```

👉 Ek **job** hai jo Ubuntu machine par run hogi

### Steps:

#### a) Repo checkout

```yaml
- uses: actions/checkout@v4
```

👉 Code machine par aa gaya

#### b) Node.js setup

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: '23'
```

👉 Node.js version 23 install

#### c) Frontend JS syntax check

```yaml
cd client
find . -name "*.js" -exec node --check {} +
```

👉 Sirf **syntax error check**
👉 Code run nahi hota

#### d) Backend JS syntax check

Same kaam `api` folder ke liye

💡 Matlab:

> Agar JS file tootay hui ho → pipeline yahin fail

---

## 6️⃣ JOB 2 – Gitleaks (Secrets Scan)

```yaml
gitleaks-scan:
  needs: compile
```

👉 Ye job **compile ke baad** chalegi
👉 Agar compile fail → ye job nahi chalegi

### Kaam:

* API keys
* passwords
* tokens leak toh nahi huay

```yaml
gitleaks detect --source ./client --exit-code 1
gitleaks detect --source ./api --exit-code 1
```

👉 Leak mila → pipeline ❌ fail

---

## 7️⃣ JOB 3 – Trivy File System Scan

```yaml
trivy_fs_scan:
  needs: gitleaks-scan
```

👉 Code & config mein:

* vulnerable packages
* risky dependencies

```yaml
severity: CRITICAL,HIGH
```

👉 Sirf **high risk issues** check

---

## 8️⃣ JOB 4 – Backend Docker Image Build & Push

```yaml
build_backend_docker_image_and_push:
  needs: trivy_fs_scan
```

### Steps:

1. DockerHub login
2. Backend ka Docker image build
3. DockerHub push

```yaml
tags:
  latest
  github.sha
```

👉 Do tags:

* `latest` (human friendly)
* `commit SHA` (production safe)

---

## 9️⃣ JOB 5 – Frontend Docker Image Build & Push

Same kaam frontend ke liye
Bas `context: ./client`

👉 Backend + Frontend **parallel build** hotay hain

---

## 🔟 JOB 6 – Trivy Image Scan

```yaml
trivy_image_scan:
  needs:
    - backend build
    - frontend build
```

👉 Docker images scan hoti hain:

* OS vulnerabilities
* node modules CVEs

👉 Agar image unsafe → pipeline fail

---

## 1️⃣1️⃣ JOB 7 – CD Repo Update (ArgoCD)

Ye **advanced DevOps part** hai 🔥

### Kya ho raha hai?

* **Alag CD repo** checkout ho raha hai
* Kubernetes YAML update
* New Docker image tag set
* Commit & push

---

### a) CD repo checkout

```yaml
repository: salman0325/argocd-project-cd.git
token: CD_REPO_TOKEN1
path: cd
```

👉 Matlab:

> Main repo → CI
> CD repo → Deployment

---

### b) yq tool install

```bash
yq_linux_amd64
```

👉 YAML edit karne ke liye

---

### c) Safety cleanup

```yaml
del(.spec.template) for Service
```

👉 Kubernetes **Service** ke andar galti se `template` na ho
(Nahi toh deploy fail)

---

### d) Backend image update

```yaml
backend:image = backend:IMAGE_TAG
```

👉 Deployment mein **naya Docker image**

### e) Frontend image update

Same logic

---

### f) Commit & push

```bash
git commit -m "bump images to SHA"
git push
```

👉 ArgoCD detect karega:

> Git change → Auto deploy 🚀

---

## 🔁 Complete Flow Summary (Yaad rakhne ke liye)

```
Push / PR
   ↓
JS Compile Check
   ↓
Secrets Scan (Gitleaks)
   ↓
Code Vulnerability Scan (Trivy FS)
   ↓
Docker Build & Push
   ↓
Docker Image Scan
   ↓
CD Repo Update
   ↓
ArgoCD Deploy
```

---

## 🧠 Kal khud ka workflow bananay ka formula

1. **Trigger define karo**
2. **Quality checks**
3. **Security scans**
4. **Build**
5. **Scan**
6. **Deploy (GitOps)**

