# Google-Cloud-Project
# LAB 1 : GETTING STARTED WITH APP ENGINE

## OVERVIEW
In this lab, you create and deploy a simple App Engine application using a virtual environment in the Google Cloud Shell.

### Objectives
In this lab, you learn how to perform the following tasks:

*Initialize App Engine.
*Preview an App Engine application running locally in Cloud Shell.
*Deploy an App Engine application, so that others can reach it.
*Disable an App Engine application, when you no longer want it to be visible.

#### TASK 1 :INITIALIZE APP ENGINE
*Initialize your App Engine app with your project and choose its region:
    -gcloud projects create [YOUR_PROJECT_ID] --set-as-default
Verify the project was created:
    -gcloud projects describe [YOUR_PROJECT_ID]
    -gcloud app create --project=[YOUR_PROJECT_ID].When prompted, select the region where you want your App Engine application located.
*Clone the source code repository for a sample application in the hello_world directory:
    -git clone https://github.com/GoogleCloudPlatform/python-docs-samples
*Navigate to the source directory:
    -cd python-docs-samples/appengine/standard_python3/hello_world

#### TASK 2 : RUN HELLO WORLD APPLICATION LOCALLY
*Execute the following command to download and update the packages list.
    -sudo apt-get update
*Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system.
    -sudo apt-get install virtualenv. If prompted [Y/n], press Y and then Enter.
    -virtualenv -p python3 venv
*Activate the virtual environment.
    -source venv/bin/activate
*Navigate to your project directory and install dependencies.
    -pip install  -r requirements.txt
*Run the application:
    -python main.py
*In your web browser, enter the following address:
    -http://localhost:8080

#### TASK 3: DEPLOY AND RUN HELLO WORLD ON APP ENGINE
To deploy your application to the App Engine Standard environment:
*Navigate to the source directory:
    -cd ~/python-docs-samples/appengine/standard_python3/hello_world
*Deploy your Hello World application.
    -gcloud app deploy. If prompted "Do you want to continue (Y/n)?", press Y and then Enter.
  This app deploy command uses the app.yaml file to identify project configuration.
*Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com
    -gcloud app browse

#### TASK 4: DISABLE THE APPLICATION
    -gcloud app versions stop 20200910t135648


# LAB 2: Getting Started with GKE
## Overview
In this lab, you create a Google Kubernetes Engine cluster containing several containers, each containing a web server. You place a load balancer in front of the cluster and view its contents.
### Objectives
In this lab, you learn how to perform the following tasks:
*Provision a Kubernetes cluster using Kubernetes Engine.
*Deploy and manage Docker containers using kubectl.

#### TASK 2 : CONFIRM THAT NEEDED APIs ARE ENABLED
*Before checking we need to set and create our project
    -gcloud config set project project-id
*Setting a default compute zone
*Run the following command, replacing compute-zone with your compute zone, such as us-west1-a:
    -gcloud config set compute/zone compute-zone
*Use the gcloud services command to confirm that both the Kubernetes Engine API and the Containers Registry API are enabled:
    -gcloud services list --enabled

#### TASK 3: START A KUBERNETES ENGINE CLUSTER
*Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
    -gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
*After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
    -kubectl version

#### TASK 4 : RUN AND DEPLOY A CONTAINER
*From your Cloud Shell or SDK , launch a single instance of the nginx container. (Nginx is a popular web server.)
    -kubectl create deploy nginx --image=nginx:1.17.10
*View the pod running the nginx container:
    -kubectl get pods
*Expose the nginx container to the Internet:
    -kubectl expose deployment nginx --port 80 --type LoadBalancer
*View the new service:
    -kubectl get services
*You can use the displayed external IP address to test and contact the nginx container remotely. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
*Scale up the number of pods running on your service:
    -kubectl scale deployment nginx --replicas 3
*Confirm that Kubernetes has updated the number of pods:
    -kubectl get pods
*Confirm that your external IP address has not changed:
    -kubectl get services

#### CLEAN UP
*To avoid incurring charges to your Google Cloud account for the resources used in the SDK, follow these steps.
*Delete the application's Service by running kubectl delete:
    -kubectl delete service hello-server
*This command deletes the Compute Engine load balancer that you created when you exposed the Deployment.
*Delete your cluster by running gcloud container clusters delete:
    -gcloud container clusters delete cluster-name



# LAB 3 :Google Cloud Fundamentals: Getting Started with Compute Engine
## Objectives:
In this lab, you will learn how to perform the following tasks:
*Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
*Create a Compute Engine virtual machine using the gcloud command-line interface.
*Connect between the two instances.

#### Steps:
*Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
    -gcloud compute instances create "my-vm-1"--machine-type "n1-standard-1"--image-project "debian-cloud"--image "debian-9-stretch-v20190213"
--subnet "default" --tags http
    -gcloud compute firewall-rules create allow-http--action=ALLOW--destination=INGRESS--rules=http:80--target-tags=http
*Create a Compute Engine virtual machine using the gcloud command-line interface.
    -gcloud config set compute/zone us-central1-b
    -gcloud compute instances create "my-vm-2"--machine-type "n1-standard-1"--image-project "debian-cloud"--image "debian-9-stretch-v20190213"--subnet "default"

#### TASK 4 : CONNECT BETWEEN VM INSTANCES

*Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
  -Connect to my-vm-2:
    -gcloud compute ssh my-vm-2
  -Ping my-vm-1 from my-vm-2:
*Use the ssh command to open a command prompt on my-vm-1:
    -ssh my-vm-1
  If you are prompted about whether you want to continue connecting to a host with unknown authenticity, enter yes to confirm that you do.
*At the command prompt on my-vm-1, install the Nginx web server:
    -sudo apt-get install nginx-light -y
*Use the nano text editor to add a custom message to the home page of the web server:
    -sudo nano /var/www/html/index.nginx-debian.html
*Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
    -Hi from YOUR_NAME
  Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.

*Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
    -curl http://localhost/
  The response will be the HTML source of the web server's home page, including your line of custom text.
*To exit the command prompt on my-vm-1, execute this command:
    -exit
*You will return to the command prompt on my-vm-2
  To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
    -curl http://my-vm-1/
The response will again be the HTML source of the web server's home page, including your line of custom text


