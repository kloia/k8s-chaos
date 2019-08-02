Kubernetes CHAOS ENGINEERING REPO
Kloia team is applying chaos scenarios at two level :
Pod
Node 

We have several tools for implement them 
# PowerfulSeal : 
This tool has a policy types for nodes and pods for customizing them , policy file example : 
config:
  minSecondsBetweenRuns: 1
  maxSecondsBetweenRuns: 10
podScenarios:
  - name: "delete random pods in default namespace"
match:
      - namespace:
          name: "mynamespace"
filters:
      - randomSample:
          size: 1
    actions:
      - kill:
          probability: 0.77
          force: true
These only detecting app at the namespace mynamespace if you want to specify deployment labels . 
podScenarios:
  - name: "delete random pods in default namespace"
match:
  - labels:
      namespace: "mynamespace"
      selector: "app=microservice1"
if application tag `app=microservice` it will hard KILL at the docker level . (Removing docker container in the pod) 
sudo docker kill -s SIGKILL HASH_OF_THE_CONTAINER


