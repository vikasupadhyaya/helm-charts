**internal-service-0.1.0**

helm install flask-app mycharts/internal-service
--namespace flask-app-ns
--create-namespace
--set replicaCount=1
--set service.type=LoadBalancer
--set service.port=80
--set app.containerPort=8000
--set app.name=flask-app
