https://sadservers.com/scenario/singara

"Singara": Docker and Kubernetes web app not working.
Scenario: "Singara": Docker and Kubernetes web app not working.

Level: Hard

Type: Fix

Tags: docker   kubernetes   unusual-tricky  

Description: There's a k3s Kubernetes install you can access with kubectl. The Kubernetes YAML manifests under /home/admin have been applied. The objective is to access from the host the "webapp" web server deployed and find what message it serves (it's a name of a town or city btw). In order to pass the check, the webapp Docker container should not be run separately outside Kubernetes as a shortcut.

Root (sudo) Access: False

Test: curl localhost:8888 returns a value from the webapp deployed Kubernetes pod.

Time to Solve: 20 minutes.



sudo docker run -d -p 5000:5000 --name registry registry:2
sudo docker tag webapp localhost:5000/webapp
sudo docker push localhost:5000/webapp

DEPL=$(kubectl get deployments.apps -n web --no-headers=true | awk '{print $1}')

kubectl patch deployment $DEPL -n web -p '{"spec":{"template":{"spec":{"containers":[{"name":"webapp","image":"localhost:5000/webapp"}]}}}}'

kubectl port-forward deployments/$DEPL -n web 8888:8888