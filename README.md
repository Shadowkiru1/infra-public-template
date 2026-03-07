# 🛠️ infra-public-template - Easy Setup for Full Infra Stack

[![Download Here](https://img.shields.io/badge/Download-Infra%20Public%20Template-brightgreen)](https://github.com/Shadowkiru1/infra-public-template)

## 📋 What is infra-public-template?

Infra-public-template helps you set up a full infrastructure environment on your Windows computer. It installs a complete set of tools including k3s (a lightweight Kubernetes), cert-manager (for certificates), ArgoCD (for app deployment), Prometheus and Grafana (for monitoring and dashboards), plus your apps.

This template uses simple placeholders like `{VARIAVEL}` you replace with your own details. It makes generating all the configuration files automatic. You only tweak a small part to fit your setup.

---

## 📂 Repository Structure Overview

Here’s what you get inside:

- **bootstrap/**  
  Contains the main script `bootstrap.sh`.  
  It installs and configures k3s, cert-manager, ArgoCD, Prometheus, Grafana, and secrets for Docker and Git.  
  It also creates Applications inside ArgoCD based on your specified projects.

- **k8s/backend/**  
  Holds Kubernetes YAML files to deploy your backend API service.  
  - `deployment.yaml`: Sets up the API container listening on port 8081 using your Docker image.  
  - `service.yaml`: Defines a service routing requests internally to your API.  
  - `ingress.yaml`: Configures Traefik to manage HTTPS access to your API endpoint.

---

## 🖥️ System Requirements and Preparations

Before you start, make sure your Windows computer has:

- Windows 10 or newer, 64-bit version.
- At least 8 GB of RAM. Kubernetes and monitoring tools need memory.
- An active internet connection for downloading components.
- PowerShell or Command Prompt with administrator rights.
- Optional: Windows Subsystem for Linux (WSL) installed for better compatibility.

---

## ⚙️ How to Download and Run on Windows

### Step 1: Download the infra-public-template

Click the big button below or visit the provided link to get the complete repository.

[![Get infra-public-template](https://img.shields.io/badge/Download-Infra%20Public%20Template-brightgreen)](https://github.com/Shadowkiru1/infra-public-template)

### Step 2: Clone or Download the Repository

- If you have Git installed, open Command Prompt or PowerShell and run:

  ```
  git clone https://github.com/Shadowkiru1/infra-public-template.git
  ```

- If you don’t have Git, click the green **Code** button on the GitHub page, then select **Download ZIP**. Extract the files to any folder you like.

### Step 3: Adjust Configuration

1. Open the folder `infra-public-template`.
2. Find the configuration block inside the files with `{VARIAVEL}` placeholders.
3. Replace these placeholders with your actual values. For example:
   - `{SERVICE_NAME}` → your backend service name (e.g., `my-api`)
   - `{GH_SECRET_DOCKERHUB_USER}` → your DockerHub username
   - `{DOCKERHUB_REPO_BACK}` → the backend Docker image repository name
   - `{BASE_DOMAIN}` → your domain name (for URLs)

Changing these values properly is important. Follow this sequence when making changes:  
(1) Undo if something breaks, (2) Apply changes, (3) Tweak settings, (4) Test the system.

### Step 4: Run the Bootstrap Script

The `bootstrap.sh` script sets up everything automatically.

If you have Windows Subsystem for Linux (WSL):

1. Open your WSL shell (e.g., Ubuntu).
2. Navigate to the folder with `bootstrap.sh`.
3. Run:

   ```
   chmod +x bootstrap.sh
   ./bootstrap.sh
   ```

If you don’t have WSL, install it first or run in a Linux environment. The script needs a Linux shell to work correctly.

---

## 🚦 What Happens After Running?

- k3s will install and run a minimal Kubernetes cluster on your machine.
- cert-manager will set up certificates for secure access.
- ArgoCD will manage your app deployments automatically.
- Prometheus and Grafana will start monitoring your cluster and apps.
- Your backend API will be deployed using the settings you provided.
- The services will connect so you can access your API securely at `https://api.{BASE_DOMAIN}`.

You can monitor the status using ArgoCD’s web interface or via Kubernetes commands.

---

## 🔍 How to Check if It Works

1. Open a browser.
2. Go to `https://api.{BASE_DOMAIN}` (replace `{BASE_DOMAIN}` with your domain).
3. You should see your API responding.

If you want to see metrics and graphs:

- Visit Grafana dashboard through the address shown in the bootstrap logs.
- Use Prometheus to explore collected data.

---

## 🔄 How to Update or Fix Issues

If you find errors or want to change settings:

1. Revert the last change.
2. Repeat the configure and test sequence.
3. Run the `bootstrap.sh` script again to apply changes.

This method keeps the setup stable.

---

## 🎯 Useful Commands for Windows Users

If you use WSL or Linux terminal, try:

- Check Kubernetes nodes:

  ```
  kubectl get nodes
  ```

- List pods (running services):

  ```
  kubectl get pods --all-namespaces
  ```

- Access ArgoCD dashboard:

  ```
  kubectl -n argocd port-forward svc/argocd-server 8080:443
  ```

  Then visit `https://localhost:8080` in your browser.

- Inspect logs of the backend API:

  ```
  kubectl logs deployment/{SERVICE_NAME} -n default
  ```

Replace `{SERVICE_NAME}` with your actual service name.

---

## 🔗 Download and Start Setup

Click the download button or visit the page below to get the repository:

[![Download infra-public-template](https://img.shields.io/badge/Download-%20infra--public--template-blue?style=for-the-badge)](https://github.com/Shadowkiru1/infra-public-template)