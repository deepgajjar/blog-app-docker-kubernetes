First setup docker and kubernetes in your system

pull nodejs image 
docker pull nodejs

then build images for all be services and fe 

please don't change name of image otherwise you will have to change inside kubernetes configuration because we are not using docker images from the dockerhub we are using local images.

client
cd client
docker build -t "deepgajjar/client:0.0.1" .

comments
cd comments
docker build -t "deepgajjar/comments:0.0.1" .

event-bus
cd event-bus
docker build -t "deepgajjar/event-bus:0.0.1" .

moderation
cd moderation
docker build -t "deepgajjar/moderation:0.0.1" .

posts
cd posts
docker build -t "deepgajjar/posts:0.0.1" .

query
cd query
docker build -t "deepgajjar/query:0.0.1" .

after genereting build setup ingress-nginx

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/cloud/deploy.yaml

if you are facing any errors regarding nginx then follpw below steps otherwise skip it

1. First kubectl get ValidatingWebhookConfiguration
2. Then kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission
3. Delete that admission, and then it’s normal

and apply again ingress-nginx configuration

kubectl apply -f ./infra/k8s/ingress-srv.yaml

after following above steps ingress-nginx shoul work but still you are facing any error then please follow below doc

https://programmerah.com/solved-kubernetes-ingress-srv-error-failed-calling-webhook-validate-nginx-ingress-kubernetes-io-51118/


and if you are not facing any error then follow below step for start pods and services in kubernetes

kubectl apply -f  .\infra\k8s\

and then access 