# google-cloud-platform-commands
This project will contain google cloud platform commands in order to clone a String Boot Project with one Rest Controller to containerize, upload the image into Google Cloud Registry and deploy it to Google Kubernate Engine.



delete old container from google cloud regsitry:
gcloud container images delete gcr.io/pristine-rock-272810/google-cloud-platform-dummy-project:v1

clone git repo from github:
git clone https://github.com/JoydeepSur/google-cloud-platform-dummy-project.git
cd google-cloud-platform-dummy-project/
mvn -N io.takari:maven:wrapper

clean install project:
./mvnw clean install
cd target/
ls -ltr

run jar file:
java -jar google-cloud-platform-dummy-project-0.0.1-SNAPSHOT.jar
ctrl + c
cd ../

create docker container using jib-maven-plugin:
./mvnw com.google.cloud.tools:jib-maven-plugin:build -Dimage=gcr.io/$GOOGLE_CLOUD_PROJECT/google-cloud-platform-dummy-project:v1

get credentials for clusters:
gcloud container clusters get-credentials hello-cluster-1 --zone us-central1-c

details of pods,services,deployments if any:
kubectl get pods
kubectl get services
kubectl get deployments

run docker container:
docker run -ti --rm -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/google-cloud-platform-dummy-project:v1
ctrl + c

kubectl run google-cloud-platform-dummy-project --image=gcr.io/$GOOGLE_CLOUD_PROJECT/google-cloud-platform-dummy-project:v1 --port=8080

kubectl get pods
kubectl get services
kubectl get deployments

kubectl expose deployment google-cloud-platform-dummy-project --type=LoadBalancer
kubectl get services

kubectl delete services google-cloud-platform-dummy-project
kubectl get services

kubectl delete deployments google-cloud-platform-dummy-project
kubectl get deployments

kubectl get pods
kubectl delete pods google-cloud-platform-dummy-project<number>
kubectl get pods
kubectl get services
kubectl get deployments