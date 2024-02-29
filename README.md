# angi
This project helps deploy podinfo resources and have enabled HPA using CPU utilization as 50%.

Tools needed: kubectl, kustomize, minikube, docker-desktop, postman

Steps:
1. Download the git repo in folder and open command prompt with the path to the folder:
2. To deploy resources without connection to redis, follow below steps:
A. kustomize build base
B. kubectl apply -k base
3. To deploy resources connection to redis, follow below steps:
A. kustomize build overlay\redis
B. kubectl apply -k overlay\redis


Tests:
*Verify if cache is working*
1. Use port forwarding to forward the port 9898
A.  kubectl port-forward <pod-name> 9898:9898
2. Open postman and send a post query with data for key: "http://localhost:9898/cache/test"
3. Send a GET query for key: "http://localhost:9898/cache/test"

*Update the color or Ui message:*
1. Update the environment variable in deploy.yaml file and deploy the resources again.

*Key features added or could be considered:*
1. Redis is currently added as a single instance and only leader but followers could be added as read replicas for scaling
2. HPA has been added for podinfo deployments with minimum replica set to 2.

