# How to deploy .NET8 WebAPI Docker Image stored in Google Cloud Artifact Registry to Google Kubernetes Engine (GKE)

To create and upload the .NET8 WebAPI Docker image to Google Cloud Artifact Registry repo, see this github repo: 

https://github.com/luiscoco/GoogleCloud_Sample10-Artifact-Registry

## 1. Set up Google Cloud SDK

Make sure you have the Google Cloud SDK installed and initialized on your local machine

```
gcloud init
```

## 2. Authenticate with GCP

Use the gcloud auth login command to authenticate with Google Cloud

Configure Docker to use gcloud as a credential helper:

```
gcloud auth configure-docker
```

## 3. Pull the Docker Image from Artifact Registry

```
docker pull LOCATION-docker.pkg.dev/PROJECT-ID/REPOSITORY/IMAGE:TAG
```

Replace LOCATION, PROJECT-ID, REPOSITORY, IMAGE, and TAG with your specific details

## 4. Set up your Kubernetes cluster 

Search for GKE

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/6bd04ccf-8ba2-4965-a916-b1f205381c24)

Enable GKE API

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/d10d453b-85bd-49d1-87b3-c0d7b27500cb)

If you haven't already, create a Kubernetes cluster in GKE

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/f9ab2c70-5727-4050-82b3-bbbafd106243)



## 5. Configure kubectl to use your GKE cluster

```
gcloud container clusters get-credentials CLUSTER_NAME --zone ZONE --project PROJECT_ID
```

## 6. Deploy the image to GKE

You can use a Kubernetes deployment YAML file to deploy the image

**deployment.yml**

```yaml
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
```

## 7. Apply this configuration 

We run this command to apply the Kubernetes manifest file 

```
kubectl apply -f deployment.yaml
```

Verify the Deployment: Check that your deployment is running as expected.

```
kubectl get deployments
```









