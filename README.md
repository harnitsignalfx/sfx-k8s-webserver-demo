# sfx-k8s-webserver-demo
SFx Mock webservice to demo percolator 

Contains 3 yaml files - 

1) webserver - 3 replicas each serving get requests and sending "http_get_requests" metric to SFx. This metric tracks the number of get requests served by each server. You need to specify your SFx Access Token.

2) lb - Internal Load Balancer listening on the internal cluster at port 80 and distributing load to the webserver service defined above.

3) webrequests - Service sending mock http requests to the Internal Load Balancer IP (You can get that by typing `kubectl get svc` and retreiving the External IP for the Load Balancer, then setting that as the TARGET_ADDRESS)


Deployment process:
1) Clone this repo
2) Add SFx token to webserver.yaml
3) Deploy the webserver and lb - ```kubectl create -f webserver.yaml -f lb.yaml``` 
4) Run ```kubectl get svc``` and get the External IP of the Load Balancer
5) Add the IP as the TARGET_ADDRESS to webrequests.yaml
6) Deploy the webrequests - ```kubectl create -f webrequests.yaml```
