In this step we want to run a Node.js Express Web App Container which we developed in step 00 and will run it in Google Container Engine.

We will follow this tutorial:


https://cloud.google.com/container-engine/docs/tutorials/hello-app


We will follow Option B: Use command-line tools locally


gcloud config set project PROJECT_ID

gcloud config set compute/zone us-central1-b

export PROJECT_ID="$(gcloud config get-value project -q)"

docker build -t gcr.io/${PROJECT_ID}/web-express:v1 .

To check if image has been created:

docker images

or 

docker image ls

Run it locally:

docker run --rm -p 8080:3000 gcr.io/${PROJECT_ID}/web-express:v1

To check either open in browser or:

curl http://localhost:8080

Now we will create the container cluster:

gcloud container clusters create hello-cluster --num-nodes=3

To check 3 VM instances:

gcloud compute instances list

To deploy:

kubectl run hello-web --image=gcr.io${PROJECT_ID}/web-express:v1 --port 8080

Note: The tutorial wrongly wanted us to give this command with a /, which did not work:

kubectl run hello-web --image=gcr.io/${PROJECT_ID}/web-express:v1 --port 8080

To check the pods:

kubectl get pods

To expose it on the internet:

kubectl expose deployment hello-web --type=LoadBalancer --port 80 --target-port 8080

To get external IP address:

kubectl get service

Run the external IP address in browser or using curl


To cleanup:

kubectl delete service hello-web




