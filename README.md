[![CircleCI](https://dl.circleci.com/status-badge/img/gh/abelasfaw/project-ml-microservice-kubernetes/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/abelasfaw/project-ml-microservice-kubernetes/tree/main)

## Project Overview
This is a flask application that has been containerized to provide predictions (inference) on housing prices through API calls. The project has the potential to be expanded to other pre-trained machine learning models, including those used for image recognition and data labeling. The application uses a pre-trained sklearn model that has been specifically trained to predict housing prices in Boston based on various features, such as the average number of rooms in a home, as well as information relating to highway access and teacher-to-pupil ratios

## Setup the Environment
* Create a virtualenv with Python3 and activate it 
  * create environment
    ```bash
        python3 -m venv .{environment_name}
  * activate environment
        source .{environment_name}/bin/activate
    ```
* Run `make install` to install the necessary dependencies. all dependencies are listed in requirements.txt file

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally
  * Build: run the command docker build -t <dockerhub_username>/<image-tag-name> to build app locally
  * Run: docker run -p <host_port>:<container_port> <dockerhub_username>/<image-tag-name>
  * Test local docker: execute ./make_prediction.sh and confirm prediction
  * Upload image: execute ./upload_docker.sh to push the image to a dockerhub account (authentication required)
* Setup and Configure Kubernetes locally
  * Start cluster: run the command minikube start
* Create Flask app in Container
  * deploy Flask app: execute ./run_kubernetes.sh. 
  * Note: When you run the script for the first time, you may encounter issues such as the container still being created and port forwarding failing due to the           container being in a pending state. In such instances, it is recommended that you wait for a few minutes before running the script again. This will              allow sufficient time for the container to be created and for the port forwarding to be established correctly.
* Run via kubectl
  * Check running pods: kubectl get pods
  * Make prediction: While the pod is running, execute .make_prediction.sh to see prediction results

### File Description
* app.py code that is responsible for prediction.
* Dockerfile a file that holds docker image specifications.
* run_docker.sh script that builds the docker image and runs the flask app.
* run_kubernetes.sh script that runs the docker hub container with kubernetes and forwards the container port to a host.
* upload_docker.sh Script that builds, tags and uploads the docker image.
* docker_out.txt output logs from docker execution.
* ubernetes_out.txt output logs from kubernetes execution.
