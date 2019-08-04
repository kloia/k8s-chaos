# PowerfulSeal : 
This tool has a policy types for nodes and pods for customizing them , policy file example : 


```
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
```

These only detecting app at the namespace mynamespace if you want to specify deployment labels . 
```
podScenarios:
  - name: "delete random pods in default namespace"
match:
  - labels:
      namespace: "mynamespace"
      selector: "app=microservice1"
```

## Multi Label Pod Policy

```
    match:
      - labels:
          namespace: "mynamespace"
          selector: "app=microservice1,chaos=enabled"
```


if application tag `app=microservice` it will hard KILL at the docker level . (Removing docker container in the pod) 
`sudo docker kill -s SIGKILL HASH_OF_THE_CONTAINER`


* Seal example run command :
`
seal autonomous --kubeconfig $KUBECONFIG --policy-file ./pod-policy.yaml   --no-cloud  -i inventory --ssh-path-to-private-key PRIVATE_KEY  --remote-user USER --ssh-allow-missing-host-keys `

## Before Applied Chaos 
<img width="600px" height="200px" src="https://github.com/kloia/k8s-chaos/blob/master/media/normal.png"></img>

## After Applied Chaos
<img width="600px" height="200px" src="https://github.com/kloia/k8s-chaos/blob/master/media/chaos.png"></img>




