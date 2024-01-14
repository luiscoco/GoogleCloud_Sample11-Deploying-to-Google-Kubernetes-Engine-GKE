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

Navigate to Google Cloud Artifact Registry list

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/77e2dd25-943c-4fc0-997e-5ebe5729db64)

See the repos list

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/2a43e7bf-a03c-49ec-93f7-2f7d8fa94ae3)



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

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/29b78cea-e7ae-4e96-976c-50b86a296cf3)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/ebd2acf4-7a4a-47d6-add9-233057094284)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/3f186a4a-2ca6-418b-95dd-52934ca9b97b)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/082f6af2-5195-40f6-ab47-c759574208fd)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/3a39cd70-8359-49ac-9ddf-313391efa9fb)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/c14d39e1-b9fd-4629-b615-8e84095b72ba)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/808a0827-e2d2-421c-a71b-f868b0226168)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/b9d38bea-9672-4554-8837-f243ef974a19)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/dcade725-9fac-4999-8cb9-4db6ddf1f492)

![image](https://github.com/luiscoco/GoogleCloud_Sample11-Deploying-to-Google-Kubernetes-Engine-GKE/assets/32194879/210ea496-92fe-452c-95be-86fcea02750c)

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









