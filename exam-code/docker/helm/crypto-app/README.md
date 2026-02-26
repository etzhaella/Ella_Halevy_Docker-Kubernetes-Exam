# Crypto App Helm Chart

This chart deploys the **frontend**, **backend**, and **MySQL** components of the crypto price exam application.

## Structure

- `Chart.yaml` – chart metadata.
- `values.yaml` – configurable values (replicas, images, database credentials, service types).
- `templates/` – Kubernetes manifests templated for:
  - `frontend` Deployment + Service
  - `backend` Deployment + Service
  - `mysqldb` Deployment + Service
  - `NOTES.txt` – post‑install instructions shown by Helm.

## Prerequisites

- A running Kubernetes cluster (for example Docker Desktop, Minikube, etc.).
- `kubectl` configured to talk to the cluster.
- `helm` v3 installed.
- Docker images built or available in a registry:
  - `devopshift-frontend:latest`
  - `devopshift-backend:latest`

You can build the images locally from the `exam-code/docker` directory:

```bash
docker build -t devopshift-frontend:latest ./fe
docker build -t devopshift-backend:latest ./be
```

## Installing the Chart

From the `exam-code/docker` directory:

```bash
helm install crypto-app ./helm/crypto-app
```

Helm will print the instructions from `NOTES.txt`, including how to:

- Check pods and services.
- Port‑forward the `frontend-service` and open the app in a browser.

## Configuration

Key values in `values.yaml`:

- **Replica counts**
  - `frontend.replicaCount`
  - `backend.replicaCount`
  - `mysql.replicaCount`

- **Images**
  - `frontend.image.repository`, `frontend.image.tag`
  - `backend.image.repository`, `backend.image.tag`
  - `mysql.image.repository`, `mysql.image.tag`

- **Database settings**
  - `mysql.env.rootPassword`
  - `mysql.env.database`
  - `mysql.env.user`
  - `mysql.env.password`
  - `backend.env.mysqlHost`, `backend.env.mysqlUser`, `backend.env.mysqlPassword`

You can override any value with your own `my-values.yaml`:

```bash
helm install crypto-app ./helm/crypto-app -f my-values.yaml
```
