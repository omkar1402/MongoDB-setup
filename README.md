Project Name: MongoDB Deployment on Kubernetes
Overview
This project provides the necessary Kubernetes manifests to deploy a MongoDB instance on a Kubernetes cluster. This setup uses Kubernetes files directly, without employing Helm charts. The manifests include configurations for Persistent Volumes, StatefulSets, Services, and ConfigMaps to ensure a robust and scalable MongoDB deployment.

Prerequisites
Before deploying MongoDB on Kubernetes, ensure you have the following:

A running Kubernetes cluster (version 1.10+)
kubectl configured to interact with your Kubernetes cluster
Persistent storage provisioner in the Kubernetes cluster
Basic understanding of Kubernetes objects (StatefulSets, Services, Persistent Volumes, etc.)
Components
Persistent Volume Claims (PVC)
PVCs are used to request storage resources for MongoDB pods. These claims ensure that data is retained even if the pods are rescheduled.

StatefulSet
A StatefulSet is used to manage the deployment and scaling of MongoDB pods. It provides unique network identities and stable, persistent storage for each pod.

Services
Two services are configured:

Headless Service: Allows for stable DNS entries to be created for each pod in the StatefulSet.
ClusterIP Service: Provides an internal IP for accessing the MongoDB replica set.
ConfigMap
A ConfigMap is used to store MongoDB configuration files that are mounted into the MongoDB pods.

Directory Structure
Copy code
.
├── configmap.yaml
├── pvc.yaml
├── service.yaml
├── statefulset.yaml
└── README.md
Deployment Steps
Clone the Repository

sh
Copy code
git clone <repository-url>
cd <repository-directory>
Create the ConfigMap

Apply the ConfigMap to store MongoDB configuration.

sh
Copy code
kubectl apply -f configmap.yaml
Create Persistent Volume Claims

Apply the PVC manifests to allocate storage for MongoDB pods.

sh
Copy code
kubectl apply -f pvc.yaml
Create Services

Deploy the headless and ClusterIP services for MongoDB.

sh
Copy code
kubectl apply -f service.yaml
Deploy StatefulSet

Deploy the MongoDB StatefulSet to manage the MongoDB pods.

sh
Copy code
kubectl apply -f statefulset.yaml
Verification
Check Pods

Verify that the MongoDB pods are running.

sh
Copy code
kubectl get pods -l app=mongodb
Check Services

Ensure the services are correctly deployed.

sh
Copy code
kubectl get svc -l app=mongodb
Check Persistent Volume Claims

Verify that the PVCs are bound to Persistent Volumes.

sh
Copy code
kubectl get pvc -l app=mongodb
Cleanup
To delete all resources created by this project, run:

sh
Copy code
kubectl delete -f statefulset.yaml
kubectl delete -f service.yaml
kubectl delete -f pvc.yaml
kubectl delete -f configmap.yaml
Conclusion
This project provides a straightforward way to deploy MongoDB on a Kubernetes cluster using only Kubernetes manifests. By following the steps outlined in this README, you can set up a scalable and reliable MongoDB deployment. For more details, refer to the official documentation and resources.

Contact
For any questions or suggestions, please contact omkarane84@gmail.com.






