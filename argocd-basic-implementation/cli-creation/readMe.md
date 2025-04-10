Using the ArgoCD CLI

The ArgoCD CLI provides a quick and scriptable way to create applications. Follow these steps:

Step 1: Log in to the ArgoCD CLI

Ensure you are logged into the ArgoCD CLI:

argocd login localhost:8080 --username admin --password <YOUR_PASSWORD>

Step 2: Create the Application

Run the following command:

argocd app create argocd-basic-cyber-nodejs-webserver \
    --repo https://github.com/vtb-wanderers63/argocd-gitops-resources \
    --path basic-k8s-resource-manifests \
    --dest-server https://kubernetes.default.svc \
    --dest-namespace basic-cyber-nodejs-webserver

Explanation of Flags
	•	--repo: Specifies the Git repository URL.
	•	--path: Defines the directory within the repository containing the Kubernetes manifests.
	•	--dest-server: The Kubernetes API server to deploy resources.
	•	--dest-namespace: The namespace where resources will be created.

Step 3: Verify the Application

List the applications to confirm it was created:

argocd app list

Synchronize the application to deploy resources:

argocd app sync argocd-basic-cyber-placeholder



