# Node.js, Express, Docker, Kubernetes, and Minikube Hello World API

This is a sample project that demonstrates how to containerize a Node.js application using Docker and deploy it to Kubernetes using Minikube.

## Prerequisites

Before you begin, make sure you have the following installed:

- [Node.js](https://nodejs.org/)
- [Docker](https://www.docker.com/)
- [Kubernetes (Kubectl)](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
- [Minikube](https://minikube.sigs.k8s.io/)

## Getting Started

1. Clone this repository:

    `git clone https://github.com/your-username/your-project.git`

2. Navigate to the project directory:

    `cd your-project`

3. Install the dependencies:

    `npm install`

## Usage
 
**Running the application locally**



To run the application locally, use the following command:

`npm start`


This will start the server on http://localhost:3000.


**Running the application locally**

To containerize the application with Docker, follow these steps:

1. Build the Docker image:
 
    `docker build -t my-express-app .`

2.  Run the Docker container:

    `docker run -p 3000:3000 my-express-app`


**Pushing the Docker Image to Docker Hub**

1. Log in to Docker Hub using the command:

    `docker login`

2. Tag your Docker image with your Docker Hub username and repository name using the command:

    `docker tag <image ID> <username>/<repository name>:<tag>`

    For example: `docker tag my-express-app parthrupapara/my-express-app:latest`

3. Push the Docker image to Docker Hub using the command: 

    `docker push <username>/<repository name>:<tag>`

    For example: `docker push parthrupapara/my-express-app:latest`


**Updating the Deployment YAML File**

1. Open the deployment YAML file (deployment.yaml) in a text editor.

2. Update the image field under the spec.template.spec.containers section to reflect the new Docker image you pushed to Docker Hub.

    For example:
    ```spec:
    template:
        spec:
        containers:
        - name: my-express-app
            image: your-username/your-repository-name:latest
            ports:
            - containerPort: 3000```

3. Save the changes to the deployment.yaml file.

**Setting up a Kubernetes Cluster with Minikube**

1. Start Minikube: 

    `minikube start`

2. Verify that the cluster is running:

    `kubectl cluster-info`

**Deploying the Application to Kubernetes**

1. Deploy the application to Kubernetes:

    `kubectl apply -f deployment.yaml`

    `kubectl apply -f kubernetes/service.yaml`

    `kubectl get deployments`

2. Get the external IP address of the service:

    `kubectl get services`

3. Get the service URL:

    `minikube service my-express-app --url`

4. Open the URL in a web browser or use curl to make a request:

    `curl http://<service-url>`

    The response should be "Hello, World!"


## Clean Up

To delete the deployment and service from Kubernetes, run:

`kubectl delete deployment my-express-app`
`kubectl delete service my-express-app`

To stop Minikube, run:

`minikube stop`

## Conclusion

Congratulations! You have successfully built and deployed a Node.js and Express API using Docker, Kubernetes, and Minikube. You can now use this project as a starting point for building your own APIs.