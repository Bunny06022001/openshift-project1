# 🚀 Git → OpenShift Deployment Demo

This project demonstrates deploying an application directly from GitHub to **Red Hat OpenShift Developer Sandbox** using OpenShift’s native build and deployment workflow.

---

## 📌 Project Overview

In this project, a static web application was:

* Built inside OpenShift using **BuildConfig (Docker strategy)**
* Automatically deployed using **Deployment**
* Exposed externally using **OpenShift Route**
* Debugged to resolve **SCC (non-root container) permission issues**
* Verified through logs, builds, and running pods

This shows a complete Git → Build → Deploy → Route lifecycle.

---

## 🧰 Tech Stack

* OpenShift Developer Sandbox
* Docker (Dockerfile build strategy)
* Nginx (container runtime)
* GitHub (source repository)
* oc CLI

---

## ⚙️ Deployment Workflow

1. Login to OpenShift cluster

```bash
oc login --token=<token> --server=<cluster>
```

2. Create / switch project

```bash
oc project srinivas06022001-dev
```

3. Deploy from GitHub

```bash
oc new-app https://github.com/Bunny06022001/openshift-project1 --strategy=docker
```

4. Monitor builds

```bash
oc get builds
```

5. Verify pods

```bash
oc get pods
```

6. Expose application

```bash
oc expose svc/openshift-project1
oc get route
```

---

## 🐞 Debugging & Fixes

During deployment the application entered **CrashLoopBackOff** due to OpenShift Security Context Constraints (SCC):

* Containers run as random non-root UID
* Nginx attempted to write to root-owned paths

### Fix implemented

* Moved nginx temp paths to `/tmp`
* Updated PID location to `/tmp/nginx.pid`
* Configured nginx to listen on port **8080**
* Patched Service targetPort to **8080**

This allowed the container to run under OpenShift’s default security model.

---

## 📸 Proof of Deployment

Screenshots available in the **screenshots/** folder showing:

* OpenShift objects (BuildConfig, ImageStream, Deployment, Route)
* Build history
* Running pods
* Application accessible via Route
* Logs and service configuration

---

## ⭐ Key Learnings

* OpenShift native build pipeline (BuildConfig)
* ImageStreams vs standard container images
* SCC security model and non-root containers
* Route vs Kubernetes Ingress
* Debugging container runtime issues in OpenShift

---

## 🔗 Application URL

Accessible via OpenShift Route after deployment.

---

## 📈 Future Improvements

* Add CI pipeline (Tekton / Jenkins)
* Configure HTTPS route
* Integrate GitOps (ArgoCD)
* Deploy multi-service application

---

## 👤 Author

Srinivas — DevOps & Cloud Engineer

Hands-on with Docker, Jenkins, Kubernetes and OpenShift.
