Created by CircleCi API Token creation

[![CircleCI](https://dl.circleci.com/status-badge/img/circleci/TxPKVauowpGakqtq5eA283/JCVqKresYpcEMfcuqCVSgc/tree/main.svg?style=svg&circle-token=e321fdf0490170ed76c59222b69b1f40de7ff4df)](https://dl.circleci.com/status-badge/redirect/circleci/TxPKVauowpGakqtq5eA283/JCVqKresYpcEMfcuqCVSgc/tree/main?circle-token=e321fdf0490170ed76c59222b69b1f40de7ff4df)

```sh
[![<ORG_NAME>](https://circleci.com/<VCS>/<ORG_NAME>/<PROJECT_NAME>.svg?style=svg)](<LINK>)
```
<PROJECT_NAME> - Your project’s name. Example: circleci-docs

![evantheoS](https://github.com/evantheoS/microservice-submit/blob/main/screenshots/circleci-project.png)

<PROJECT_NAME> = microservice-submit-4

<ORG_NAME> - The organization or user name the project in question belongs to


![evantheoS](https://github.com/evantheoS/microservice-submit/blob/main/screenshots/circleci-organisation.png)

<ORG_NAME> = cci-2s5yl

VCS - your VCS provider (gh for "GitHub" and bb for Bitbucket)

VCS = gh 
<LINK> - The link you want the status badge to go to when clicked (example: the pipeline overview page)

Optional: an API token (to create badges for private projects)


![evantheoS](https://github.com/evantheoS/microservice-submit/blob/main/screenshots/circleci-api-token-creation.png)

API-token created



```sh
[![cci-2s5yl](https://circleci.com/gh/cci-2s5yl/microservice-submit-4.svg?style=svg)](<LINK>)
```
[![cci-2s5yl](https://circleci.com/gh/cci-2s5yl/microservice-submit-4.svg?style=svg)](<LINK>)

```sh
[![cci-2s5yl](https://circleci.com/gh/cci-2s5yl/microservice-submit-4.svg?style=svg&circle-token=e321fdf0490170ed76c59222b69b1f40de7ff4df)](<LINK>)
```
[![cci-2s5yl](https://circleci.com/gh/cci-2s5yl/microservice-submit-4.svg?style=svg&circle-token=e321fdf0490170ed76c59222b69b1f40de7ff4df)](<LINK>)

  
  
  
## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API.

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:

-   Test your project code using linting
-   Complete a Dockerfile to containerize this application
-   Deploy your containerized application using Docker and make a prediction
-   Improve the log statements in the source code for this application
-   Configure Kubernetes and create a Kubernetes cluster
-   Deploy a container using Kubernetes and make a prediction
-   Upload a complete Github repo with CircleCI to indicate that your code has been tested

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

-   Create a virtualenv and activate it
-   Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone: `python app.py`
2. Run in Docker: `./run_docker.sh`
3. Run in Kubernetes: `./run_kubernetes.sh`

### Kubernetes Steps

-   Setup and Configure Docker locally
-   Setup and Configure Kubernetes locally
-   Create Flask app in Container
-   Run via kubectl

## Tasks

To see the screenshots of each task go to the `screenshots` directory.

### 1. Complete the Dockerfile

-   Specify your python version
-   Specify a working directory.
-   Copy the app.py source code to that directory
-   Install any dependencies in requirements.txt (`make install`)
-   Expose a port when the container is created (port 80 is standard).
-   Specify that the app runs at container launch.


To run `make lint` don't forget crete and active the virtual env before:

```sh
$ make setup # create the virtual env
$ source ~/.devops/bin/activate # active the virtual env
$ make lint
```

### 2. Run a Container & Make a Prediction

-   Build the docker image from the Dockerfile; it is recommended that you use an optional --tag parameter as described in the build documentation.
-   List the created docker images (for logging purposes).
-   Run the containerized Flask app; publish the container’s port (`80`) to a host port (`8000`).

Run the container using the `run_docker.sh` script created before following the steps above:

```sh
$ . ./run_docker.sh # Check the `Workarounds` section if you want to get more information about this.
```

After running the container (docker app) we can able to run the prediction using the `make_prediction.sh` script:

```sh
$ . ./make_prediction.sh # Don't forget run the container before
```

### 3. Improve Logging & Save Output

-   Add a prediction log statement
-   Run the container and make a prediction to check the logs

```sh
[2023-12-22 16:42:28,254] INFO in app: JSON payload: 
{'CHAS': {'0': 0}, 'RM': {'0': 6.575}, 'TAX': {'0': 296.0}, 'PTRATIO': {'0': 15.3}, 'B': {'0': 396.9}, 'LSTAT': {'0': 4.98}}
[2023-12-22 16:42:28,285] INFO in app: Inference payload DataFrame: 
   CHAS     RM    TAX  PTRATIO      B  LSTAT
0     0  6.575  296.0     15.3  396.9   4.98
[2023-12-22 16:42:28,296] INFO in app: Scaling Payload: 
   CHAS     RM    TAX  PTRATIO      B  LSTAT
0     0  6.575  296.0     15.3  396.9   4.98
[2023-12-22 16:42:28,301] INFO in app: Prediction: [20.35373177134412]
172.17.0.1 - - [22/Dec/2023 16:42:28] "POST /predict HTTP/1.1" 200 -
```


### 4. Upload the Docker Image

-   Create a [Docker Hub](https://hub.docker.com/) account
-   Built the docker container with this command `docker build --tag=<your_tag> .` **(Don't forget the tag name)**
-   Define a `dockerpath` which is `<docker_hub_username>/<project_name>` e.g: `minorpath/kubernetes-p4`
-   Authenticate and tag image
-   Push your docker image to the `dockerpath`


After complete all steps run the upload using the `upload_docker.sh` script:

```sh
$ . ./upload_docker.sh
```

### 5. Configure Kubernetes to Run Locally

-   [Install Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux)
-   [Install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)


### 6. Deploy with Kubernetes and Save Output Logs

-   Define a dockerpath which will be `<docker_hub_username>/<project_name>`, this should be the same name as your uploaded repository (the same as in upload_docker.sh)
-   Run the docker container with kubectl; you’ll have to specify the container and the port
-   List the kubernetes pods
-   Forward the container port to a host port, using the same ports as before

After complete all steps run the kubernetes using `run_kubernetes.sh` script:

```sh
$ . ./run_kubernetes.sh
```

```sh
Error from server (AlreadyExists): pods "flaskapp" already exists
NAME       READY   STATUS    RESTARTS       AGE
flaskapp   1/1     Running   2 (8m7s ago)   18m
Forwarding from 127.0.0.1:8000 -> 80
Forwarding from [::1]:8000 -> 80
Handling connection for 8000

(.devops) jenkins:~/environment/microservice-submit (main) $ bash ./make_prediction.sh
Port: 8000
{
  "prediction": [
    20.35373177134412
  ]
}
```
After running the kubernete make a prediction using the `make_prediction.sh` script as we do in the [second task](#2-run-container--make-prediction).


### 7. Delete Cluster

If you want to delete the kubernetes cluster just run this command `minikube delete`. You can also stop the kubernetes cluster with this command `minikube stop`

### 8. CircleCI Integration

-   Create a [CircleCI Account](https://circleci.com/) (use your Github account for a better integration)
-   Create a config using this [template](https://raw.githubusercontent.com/udacity/DevOps_Microservices/master/Lesson-2-Docker-format-containers/class-demos/.circleci/config.yml)
-   Add a status badge using this template: `[![<evantheoS>](https://circleci.com/gh/evantheoS/microservice-submit.svg?style=svg)](https://circleci.com/gh/evantheoS/microservice-submit)` replace `<github_username>` and `<repository>` with your data. 

## Workarounds

### Minikube

Minikube common issue 1: `Out of memory` or `No space left on the device`. Change the instance type from `t2.micro` to `t2.medium` and ensure at least 4GB of free space and 2GB of memory on the device. You can all docker images using this command `docker system prune -a` or remove all unused or dangling image with this command `docker system prune`
Minikube common issue 2: `minkube start..gives error: "Exiting due to RSRC_INSUFFICIENT_CORES"..Is it possible to start minikube on this Mac with 2 CPU cores?`. solution:  minikube --extra-config=kubeadm.ignore-preflight-errors=NumCPU --force --cpus=1 start

### Bash scripts

Sometimes you can't run a bash script using this format `./run_docker.sh` but you have some alternative like `bash run_docker.sh` or `. ./run_docker.sh`

> **Note:** This is the same for all scripts (`*.sh`)

### Adding tests

Add `pytest` to the `requirements.txt` file and update the `Makefile` to add this command `python3 -m pytest -vv test_app.py` which is the file that contains the tests for `home` and `predict` endpoints.

### Linting warnings

The warning for logging format interpolation appears when we want to use f-strings but we can disable using W1202. So we need change this command `pylint --disable=R,C,W1203` to `pylint --disable=R,C,W1202`

### Tests on Circle CI

For pytest: https://circleci.com/docs/2.0/collect-test-data/#pytest

### Kubernetes running docker image

Don't use **80** as a port. e.g: `kubectl run app --image=$dockerpath --port=80` you can have some troubles with the forwarding of that port. Use a different port like **8080** e.g: `kubectl run app --image=$dockerpath --port=8080` so now you can forward that port with `kubectl port-forward deployment/app 8080:80`.

> Don't forget update the `make_prediction.sh` script to use the same port as you are using to run the docker app _(with or without kubernetes)_