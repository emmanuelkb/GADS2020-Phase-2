# LAB: AK8S-03 Creating a GKE Cluster via GCP Console

## Objectives: 

In this lab, you will learn how to perform the following tasks:

	-Use the GCP Console to build and manipulate GKE clusters

	-Use the GCP Console to deploy a Pod

	-Use the GCP Console to examine the cluster and Pods


## Steps:

1. Use the GCP Console to build and manipulate GKE clusters

		gcloud container clusters create standard-cluster-1 --zone us-central1-a

		gcloud container clusters describe standard-cluster-1

2. Use the GCP Console to deploy a Pod

		gcloud container clusters resize standard-cluster-1 --node-pool default-pool --num-nodes 4

		gcloud container node-pools describe default-pool --cluster standard-cluster-1

3. Use the GCP Console to examine the cluster and Pods
		
		export PROJECT_ID=project-id (replace project-id)
		docker build -t gcr.io/${PROJECT_ID}/nginx:v1
		docker images
		docker run --rm -p 8080:8080 gcr.io/${PROJECT_ID}/nginx:v1
		curl http://localhost:8080
		gcloud auth configure-docker
		docker push gcr.io/${PROJECT_ID}/nginx:v1

		kubectl create deployment nginx --image=gcr.io/${PROJECT_ID}/nginx:v1
		kubectl scale deployment nginx --replicas=3
		kubectl autoscale deployment nginx --cpu-percent=80 --min=1 --max=5
		
		kubectl get pods
		gcloud container clusters describe standard-cluster-1