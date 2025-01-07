Using the ArgoCD UI

This method is intuitive and ideal for users who prefer graphical interfaces.

Step 1: Access the ArgoCD Web UI
	1.	Ensure port-forwarding is active:

kubectl port-forward svc/argocd-server -n argocd 8080:443


	2.	Open your browser and navigate to https://localhost:8080.
	3.	Log in using your credentials (default username: admin).

Step 2: Create a New Application
	1.	Go to the Applications section.
	2.	Click New App.

Step 3: Fill in Application Details

In the New Application form, fill out these fields:
	•	Application Name: argocd-basic-cyber-placeholder
	•	Project: default
	•	Sync Policy: Manual (or choose Automated if desired).
	•	Source Repository URL: https://github.com/cyber-placeholder/argocd-gitops-resources.git
	•	Path: argocd-basic-implementation-resources
	•	Destination Cluster URL: https://kubernetes.default.svc
	•	Destination Namespace: cyber-placeholder

Step 4: Create the Application

Click Create. You’ll be redirected to the application dashboard.

Step 5: Synchronize the Application

Click Sync on the application dashboard to deploy resources.