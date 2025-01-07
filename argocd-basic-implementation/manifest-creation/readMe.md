Applying a Kubernetes Manifest

This method allows you to declaratively define an ArgoCD application using YAML.

Step 1: Create a Manifest File

Create a file named application.yaml with the following content:

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

Explanation of Fields
	•	metadata.name: The name of your application.
	•	spec.source.repoURL: The Git repository containing the Kubernetes manifests.
	•	spec.source.path: Directory in the repository for the application manifests.
	•	spec.destination.namespace: Namespace for the Kubernetes resources.
	•	spec.syncPolicy.automated: Automates synchronization (optional).

Step 2: Apply the Manifest

Apply the manifest to create the application:

kubectl apply -f application.yaml

Step 3: Verify the Application

Check the application status in the ArgoCD Web UI or CLI:

argocd app get argocd-basic-cyber-placeholder

Synchronize the application if it is not automated:

argocd app sync argocd-basic-cyber-placeholder