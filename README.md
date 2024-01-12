# How to deploy Google Cloud Artifact Registry Docker Image to Google Kubernetes Engine (GKE)

## 1.

Set up Google Cloud SDK: Make sure you have the Google Cloud SDK installed and initialized on your local machine.

Authenticate with GCP: Use the gcloud auth login command to authenticate with Google Cloud.

Configure Docker to use gcloud as a credential helper:

bash
Copy code
gcloud auth configure-docker
Pull the Docker Image from Artifact Registry:

bash
Copy code
docker pull LOCATION-docker.pkg.dev/PROJECT-ID/REPOSITORY/IMAGE:TAG
Replace LOCATION, PROJECT-ID, REPOSITORY, IMAGE, and TAG with your specific details.

Set up your Kubernetes cluster: If you haven't already, create a Kubernetes cluster in GKE.

Configure kubectl to use your GKE cluster:

bash
Copy code
gcloud container clusters get-credentials CLUSTER_NAME --zone ZONE --project PROJECT_ID
Deploy the image to GKE:
You can use a Kubernetes deployment YAML file to deploy the image. Here is a basic example:

yaml
Copy code
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-name
spec:
  replicas: 1
  selector:
    matchLabels:
      app: your-app
  template:
    metadata:
      labels:
        app: your-app
    spec:
      containers:
      - name: your-app
        image: LOCATION-docker.pkg.dev/PROJECT-ID/REPOSITORY/IMAGE:TAG
Apply this configuration using kubectl apply -f deployment.yaml.

Verify the Deployment: Check that your deployment is running as expected.

bash
Copy code
kubectl get deployments

## 2. 




## 3. 



## 4. 








