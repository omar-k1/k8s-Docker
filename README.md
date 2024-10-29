![k8s-photo](https://github.com/user-attachments/assets/f9e2617e-9ed7-45f9-8d86-992c399bf909)


---
# Application Deployment on KinD

This project is designed to provide a comprehensive learning experience for those interested in React development and container orchestration using Kubernetes and Docker. It aims to guide users through the fundamentals of React while demonstrating how to deploy a React application using Kubernetes and Docker.

In addition to React, this project introduces users to the principles of containerization with Docker. It showcases how to create and manage Docker images, enabling developers to package their applications along with all dependencies for consistent deployment across various environments.

Furthermore, the project leverages Kubernetes for orchestration, illustrating how to deploy, scale, and manage containerized applications. Users will gain practical experience in configuring Kubernetes resources, including Deployments, Services, and ConfigMaps, which are essential for running production-grade applications.

Through this project, learners will not only acquire the technical skills necessary for developing React applications but also understand the deployment processes and tools that are critical in today’s DevOps landscape. By the end of the tutorial, participants will have a solid understanding of both front-end development and modern deployment practices, empowering them to tackle real-world projects with confidence.
Technologies Used

---
## Prerequisites

Make sure you have the following tools installed before proceeding:

- [Docker](https://docs.docker.com/get-docker/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [KinD](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

----

##  1: Set Up KinD Cluster

1. *Install KinD*: Follow the installation instructions in the [KinD documentation](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).
2. *Create a KinD Cluster*: Use the following command to create a KinD cluster with a specific name (e.g., todos-cluster).
   bash
   kind create cluster --name todos-cluster
   

----   

## 2: Docker

1. **Dockerfile**: Create a Dockerfile for your todos application. Define the environment and dependencies required to run your app.

2. **Build Docker Image**: Build an image from the Dockerfile using:
   bash
   docker build -t <your-dockerhub-username>/todos-app:latest .
   
3. Push Docker Image: Push this image to a Docker registry (e.g., Docker Hub).
    bash
    docker push <your-dockerhub-username>/todos-app:latest.
4. Run Docker Container: Run a container using the newly built image to verify functionality.
     bash
     docker run -p 3000:3000 <your-dock
     erhub-username>/todos-app:latest.
5. Verify Container: Ensure the application is accessible from the container.     

-----
## 3: kubernates(k8s)

###  deployments
  
  1. Create Deployment YAML: Write a deployment.yaml file that specifies replicas, selectors, and the container image for your app.
  
  2. Apply the Deployment to the KinD cluster.
  
     bash
     kubectl apply -f <deployment_name>.yaml
  
  3. Verify Deployment and Pods: Confirm the deployment and pods are running.
     bash
     kubectl get deployments
     kubectl get pods
     
    
###  service  

  1. Create Service YAML: Write a service.yaml to expose the Deployment internally within the cluster.
  
  
  2. Apply the Service to the KinD cluster.
  
     bash
     kubectl apply -f <service_name>.yaml  
  
  3. Verify Service: List services to ensure connectivity within the cluster.
  
     bash
     kubectl get services

### ingress  

  1. install NGINX Ingress Controller: Set up NGINX Ingress to manage external access to services in KinD.

     bash
     kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

  2. Create and Apply Ingress YAML: Write an ingress.yaml file to configure access to the Service and apply it.

     bash
     kubectl apply -f <ingress_name>.yaml

  3. Access Application Externally: Add an entry in /etc/hosts pointing todos.local to your KinD node’s IP (use kubectl get nodes -o wide to find the IP).



### ConfigMap and Secret
![Screenshot from 2024-10-29 16-54-38](https://github.com/user-attachments/assets/cd2fd630-5e36-4db8-8bc9-71698f80a2d2)

  -  Create ConfigMap YAML: Add configmap.yaml with necessary configuration data for your application.

  -  Create Secret YAML: Add secret.yaml with sensitive information (e.g., database credentials).
  
  - Apply ConfigMap and Secret to the cluster.
    ```bash
    kubectl apply -f <configmap_name>.yaml
    kubectl apply -f <secret_name>.yaml
  
  - *Reference ConfigMap and Secret in Pod Configuration*: Update deployment.yaml to use these values.
  

###  PersistentVolume and PersistentVolumeClaim

  - Create PersistentVolume YAML: Define storage capacity and access in pv.yaml.
  
  - Create PersistentVolumeClaim YAML: Request the required storage in pvc.yaml.
  
  - Apply PV and PVC to the cluster. 
  
  - Mount PVC in Deployment Configuration: Update deployment.yaml to mount the PersistentVolumeClaim for data persistence.
  
  
  
###  Final Steps

  - Access the App: Visit the application via the configured Ingress endpoint (e.g., http://frontend.local) to confirm setup completion.
  
  
---------------------------------
![Screenshot from 2024-10-29 16-54-38](https://github.com/user-attachments/assets/4961e085-868a-4792-a567-d2b1d523e645)
