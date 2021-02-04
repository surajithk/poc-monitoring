Steps to deploy and test:

export PROJECT_ID=nyt-messaging-dev

docker build -t gcr.io/${PROJECT_ID}/monitoring-poc:v1 .

docker images

docker run --rm -p 8080:8080 gcr.io/${PROJECT_ID}/monitoring-poc:v1

gcloud auth configure-docker

docker push gcr.io/${PROJECT_ID}/monitoring-poc:v1

kubectl create deployment monitoring-poc --image=gcr.io/${PROJECT_ID}/monitoring-poc:v1

kubectl scale deployment monitoring-poc --replicas=1

kubectl autoscale deployment monitoring-poc --cpu-percent=80 --min=1 --max=5

kubectl get pods

kubectl expose deployment monitoring-poc --name=monitoring-poc-service --type=LoadBalancer --port 80 --target-port 8080

kubectl get service

