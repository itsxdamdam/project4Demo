[![CircleCI](https://dl.circleci.com/status-badge/img/gh/thesaam/project4Demo/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/thesaam/project4Demo/tree/main)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host. 
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally
* Setup and Configure Kubernetes locally
* Create Flask app in Container
* Run via kubectl

Tasks

Complete the Dockerfile

Specify your python version Specify a working directory. Copy the app.py source code to that directory Install any dependencies in requirements.txt (make install) Expose a port when the container is created (port 80 is standard). Specify that the app runs at container launch.

To run make lint don't forget create and activate the virtual env before:

$ make setup # create the virtual env $ source ~/.devops/bin/activate # active the virtual env $ make lint

Run a Container & Make a Prediction

Build the docker image from the Dockerfile; it is recommended that you use an optional --tag parameter as described in the build documentation. List the created docker images (for logging purposes). Run the containerized Flask app; publish the container’s port (80) to a host port (8000).

Run the container using the run_docker.sh script created before following the steps above:

$ . ./run_docker.sh 

After running the container (docker app) we can able to run the prediction using the make_prediction.sh script:

$ . ./make_prediction.sh 

Improve Logging & Save Output

Add a prediction log statement Run the container and make a prediction to check the logs

Upload the Docker Image

Create a Docker Hub account Built the docker container with this command docker build --tag=<your_tag> .Define a dockerpath which is <docker_hub_username>/<project_name> i.e. thesaam/demo1

After complete all steps run the upload using the upload_docker.sh script:

$ . ./upload_docker.sh

Configure Kubernetes to Run Locally

Install Kubernetes Install Minikube

Deploy with Kubernetes and Save Output Logs

Define a dockerpath which will be <docker_hub_username>/<project_name>, this should be the same name as your uploaded repository. Run the docker container with kubectl; you’ll have to specify the container and the port List the kubernetes pods Forward the container port to a host port, using the same ports as before

After complete all steps run the kubernetes using run_kubernetes.sh script:

$ . ./run_kubernetes.sh

After running the kubernete make a prediction using the make_prediction.sh script as we do in the second task.

Delete Cluster
If you want to delete the kubernetes cluster just run this command minikube delete. You can also stop the kubernetes cluster with this command minikube stop 8. CircleCI Integration

Create a CircleCI Account (use your Github account for a better integration)
Create a config using this template

Add a status badge using this template: [![<github_username>](https://circleci.com/gh/<github_username>/<repository>.svg?style=svg)](https://circleci.com/gh/<github_username>/<repository>) replace <github_username> and <repository> with your data as seen at the top of readme file.

Workarounds Minikube

Minikube common issues: Out of memory or No space left on the device. Change the instance type from t2.micro to t2.medium and ensure at least 4GB of free space and 2GB of memory on the device. You can all docker images using this command docker system prune -a or remove all unused or dangling image with this command docker system prune Bash scripts

Sometimes you can't run a bash script using this format ./run_docker.sh but you have some alternative like bash run_docker.sh or . ./run_docker.sh

Add pytest to the requirements.txt file and update the Makefile to add this command python3 -m pytest -vv test_app.py which is the file that contains the tests for home and predict endpoints. Linting warnings

The warning for logging format interpolation appears when we want to use f-strings but we can disable using W1202. So we need change this command pylint --disable=R,C,W1203 to pylint --disable=R,C,W1202 Tests on Circle CI

For pytest: https://circleci.com/docs/2.0/collect-test-data/#pytest Kubernetes running docker image