Beginner’s Guide to ArgoCD: Installation, Setup, and Application Creation

Introduction

ArgoCD is a declarative, GitOps-based continuous delivery tool for Kubernetes. By the end of this guide, you will:
	1.	Install and configure ArgoCD on your local machine.
	2.	Access the ArgoCD API server.
	3.	Create and manage a basic ArgoCD application that deploys Kubernetes resources.

This guide is designed for users with minimal experience, offering step-by-step instructions, practical examples, and explanations.

Prerequisites

Before starting, ensure the following tools are installed on your machine:
	•	kubectl
	•	Minikube
	•	Docker Desktop or Podman

1. Installing ArgoCD in Kubernetes

Step 1: Create the argocd Namespace

kubectl create namespace argocd

This namespace will host all ArgoCD components.

Step 2: Install the ArgoCD CRDs

Run the following command to apply ArgoCD manifests:

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

	•	This will install the necessary Custom Resource Definitions (CRDs) and ArgoCD components.

Step 3: Verify the Installation

List pods in the argocd namespace:

kubectl get pods -n argocd

Ensure all pods are in the Running state.

2. Installing the ArgoCD CLI

macOS

brew install argocd

Windows
	1.	Download the CLI from the ArgoCD Releases.
	2.	Add the binary to your system’s PATH.

Verify installation:

argocd version

3. Accessing the ArgoCD API Server

Step 1: Forward the ArgoCD Server Port

kubectl port-forward svc/argocd-server -n argocd 8080:443

	•	Access the server at: https://localhost:8080.

Note: Ingress-based access will be covered in future updates.

4. Retrieving the Default Admin Password

The default admin password is stored in a secret:

kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

5. Logging into ArgoCD CLI

Step 1: Log in Using Default Admin Credentials

argocd login localhost:8080 --username admin --password <DEFAULT_PASSWORD>

Step 2: Update the Admin Password

argocd account update-password

This enhances security by replacing the default password.

6. Creating an ArgoCD Application

You can create an ArgoCD application using three methods:

Method 1: Using the ArgoCD CLI

argocd app create argocd-basic-cyber-placeholder \
    --repo https://github.com/cyber-placeholder/argocd-gitops-resources.git \
    --path argocd-basic-implementation-resources \
    --dest-server https://kubernetes.default.svc \
    --dest-namespace cyber-placeholder

Method 2: Using the ArgoCD UI
	1.	Log in to the ArgoCD Web UI (https://localhost:8080).
	2.	Navigate to Applications > New App.
	3.	Fill in the following details:
	•	Application Name: argocd-basic-cyber-placeholder
	•	Project: default
	•	Sync Policy: Manual
	•	Git Repository URL: https://github.com/cyber-placeholder/argocd-gitops-resources.git
	•	Path: argocd-basic-implementation-resources
	•	Destination Cluster URL: https://kubernetes.default.svc
	•	Destination Namespace: cyber-placeholder
	4.	Click Create.

Method 3: Applying a Kubernetes Manifest

Create a file named application.yaml:

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: argocd-basic-cyber-placeholder
  namespace: argocd
spec:
  destination:
    namespace: cyber-placeholder
    server: https://kubernetes.default.svc
  source:
    path: argocd-basic-implementation-resources
    repoURL: https://github.com/cyber-placeholder/argocd-gitops-resources.git
    targetRevision: HEAD
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true

Apply the manifest:

kubectl apply -f application.yaml

Troubleshooting Tips
	•	If the application doesn’t sync, verify the repository URL and path.
	•	Use kubectl logs to debug ArgoCD components:

kubectl logs -n argocd <POD_NAME>

By following this guide, you’ve successfully set up ArgoCD and deployed a basic application. 🎉 Happy GitOps!