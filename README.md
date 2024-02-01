# awsx-api-deployment
AWSX API deployment repo

kubectl apply -f 1_namespace.yaml

helm upgrade -i -n "appkube-awsx-api-service" "appkube-awsx-api" "helm/awsx-api"/ --set "image.tag=9a1bf21d8a3a05344ec7a6f46fdd864376946897"