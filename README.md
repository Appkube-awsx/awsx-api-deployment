# awsx-api-deployment
AWSX API deployment repo

We use 2 custom container for this service 
  - Dockerfile in this repo - standard go container. 
  - Dockerfile in awsx-api repo - contains service binaries


Deploying sevice
  - Manual commands
    - kubectl apply -f 1_namespace.yaml
    - helm upgrade -i -n "appkube-awsx-api-service" "appkube-awsx-api" "helm/awsx-api"/ --set "image.tag=<Valid tag>"
  - via pipeline
    - set "build-awsx-api-base-container" & "uninstall-awsx-api-service" to false in pipelinerun/deploy-awsx-api-service.yaml
    - deploy pipeline and pipelinerun to kubernetes "kubectl apply - "pipelinerun/deploy-awsx-api-service.yaml"

Uninstall service
  - Manual commands
    -  helm uninstall -n appkube-awsx-api-service "$(params.release_name)"
    - kubectl delete namespace appkube-awsx-api-service appkube-awsx-api
  - via pipeline
    - set "build-awsx-api-base-container" to false & "uninstall-awsx-api-service" to true in "pipelinerun/deploy-awsx-api-service.yaml"
    - deploy pipeline and pipelinerun to kubernetes "kubectl apply - "pipelinerun/deploy-awsx-api-service.yaml"

Create new go image
  - Update "Dockerfile" as per requirement
  - via pipeline
    - set "build-awsx-api-base-container" to true & "uninstall-awsx-api-service" to false in "pipelinerun/deploy-awsx-api-service.yaml"
    - deploy pipeline and pipelinerun to kubernetes "kubectl apply - "pipelinerun/deploy-awsx-api-service.yaml"

