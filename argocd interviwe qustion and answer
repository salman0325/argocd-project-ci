# 1. What is Argo CD?

### English

Argo CD is a **GitOps continuous delivery tool** for Kubernetes. It automatically deploys applications from a Git repository to a Kubernetes cluster.

**Example:**

* Your Kubernetes YAML files are stored in Git.
* Argo CD watches the Git repository.
* Whenever Git changes, Argo CD updates the Kubernetes cluster automatically.

### Roman Urdu

Argo CD ek **GitOps deployment tool** hai jo Kubernetes mein applications ko deploy karta hai.

Simple words mein:

* Aap apni YAML files Git mein rakhte ho.
* Argo CD Git ko continuously check karta rehta hai.
* Jese hi Git mein koi change hota hai, Argo CD automatically cluster update kar deta hai.

---

# 2. What is GitOps?

### English

GitOps is a way of managing infrastructure and applications where **Git is the single source of truth**.

Instead of manually running commands, you make changes in Git. Argo CD detects the changes and applies them to Kubernetes.

### Roman Urdu

GitOps ka matlab hai ke **Git hi sab se authentic source hota hai.**

Manual commands chalane ki bajaye:

* Git mein code update karo.
* Argo CD khud deployment kar dega.

---

# 3. How does Argo CD work?

### English

Argo CD follows these steps:

1. Watches the Git repository.
2. Compares Git with the Kubernetes cluster.
3. Finds differences (drift).
4. Synchronizes the cluster with Git.

### Roman Urdu

Argo CD ka workflow:

1. Git ko monitor karta hai.
2. Cluster se compare karta hai.
3. Agar difference mile to detect karta hai.
4. Cluster ko Git ke according update kar deta hai.

---

# 4. What is Sync in Argo CD?

### English

Sync means applying the latest changes from Git to Kubernetes.

Example:
You update replicas from 2 to 4 in Git.

Before Sync:

```
Git: 4 replicas
Cluster: 2 replicas
```

After Sync:

```
Git: 4 replicas
Cluster: 4 replicas
```

### Roman Urdu

Sync ka matlab hai Git ke changes ko cluster mein apply karna.

Agar Git mein replicas 4 kar diye,
to Sync ke baad cluster bhi 4 replicas chala dega.

---

# 5. What is Auto Sync?

### English

Auto Sync automatically deploys Git changes without requiring you to click the Sync button.

### Roman Urdu

Auto Sync ka matlab hai:

Git mein change karo aur Argo CD khud deployment kar dega.

Manual Sync karne ki zarurat nahi hoti.

---

# 6. What is Drift?

### English

Drift happens when the Kubernetes cluster is different from Git.

Example:

Git:

```
replicas: 3
```

Cluster:

```
replicas: 5
```

Argo CD detects this difference.

### Roman Urdu

Drift ka matlab hai Git aur cluster ka same na hona.

Example:

Git:

```
3 replicas
```

Cluster:

```
5 replicas
```

Argo CD is difference ko detect kar leta hai.

---

# 7. What is Self-Heal?

### English

Self-Heal automatically fixes manual changes made directly in the Kubernetes cluster.

Example:
Someone manually changes replicas to 10 using `kubectl`.

Argo CD changes it back to the value stored in Git.

### Roman Urdu

Self-Heal ka matlab hai agar koi cluster mein manually change kar de,
to Argo CD us change ko hata kar Git wali configuration wapas laga deta hai.

---

# 8. What is Pruning?

### English

Pruning removes Kubernetes resources that exist in the cluster but no longer exist in Git.

Example:

Git:

```
Deployment A
```

Cluster:

```
Deployment A
Deployment B
```

Pruning deletes Deployment B.

### Roman Urdu

Pruning ka matlab hai extra resources delete karna.

Agar Git mein Deployment B delete ho gaya,
to Argo CD cluster se bhi us deployment ko delete kar dega.

---

# 9. What is an Application in Argo CD?

### English

An Application is the main Argo CD object that tells Argo CD:

* Which Git repository to use
* Which branch to use
* Which folder contains manifests
* Which Kubernetes cluster to deploy to
* Which namespace to deploy into

### Roman Urdu

Application Argo CD ka main object hota hai.

Ismein bataya jata hai:

* Git repository kaunsi hai
* Branch kaunsi hai
* Folder konsa hai
* Cluster konsa hai
* Namespace konsa hai

---

# 10. Why is Argo CD better than manual deployment?

### English

Manual deployment:

* Human errors
* No history
* Difficult rollback
* Inconsistent deployments

Argo CD:

* Automatic deployments
* Git history
* Easy rollback
* Consistent deployments
* Better security
* Easy auditing

### Roman Urdu

Manual deployment mein:

* Human mistakes hoti hain.
* History maintain karna mushkil hota hai.
* Rollback difficult hota hai.

Argo CD:

* Automatic deployment karta hai.
* Git history maintain hoti hai.
* Rollback easy hota hai.
* Sab clusters same configuration follow karte hain.
* Security aur auditing behtar hoti hai.

---

# Bonus: Frequently Asked Argo CD Commands

| Command                              | Purpose                            |
| ------------------------------------ | ---------------------------------- |
| `argocd login <server>`              | Login to Argo CD                   |
| `argocd app list`                    | Show all applications              |
| `argocd app get <app-name>`          | View application details           |
| `argocd app sync <app-name>`         | Synchronize the application        |
| `argocd app history <app-name>`      | View deployment history            |
| `argocd app rollback <app-name>`     | Roll back to a previous version    |
| `argocd app delete <app-name>`       | Delete an application              |
| `kubectl get applications -n argocd` | List Argo CD Application resources |
| `kubectl get pods -n argocd`         | View Argo CD pods                  |
| `kubectl logs <pod-name> -n argocd`  | Check logs for troubleshooting     |


**Roman Urdu:**
"Argo CD ek GitOps deployment tool hai jo Git ko source of truth manta hai. Yeh Git aur Kubernetes cluster ko compare karta rehta hai. Agar dono mein koi difference ho, to Argo CD usay detect karke cluster ko Git ke mutabiq update kar deta hai. Is se deployments automatic, consistent aur easily manageable rehti hain."
