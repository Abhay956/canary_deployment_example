
## canary_deployment_example

![image](https://github.com/Abhay956/canary_deployment_example/assets/141961610/25dd6b32-3dac-482b-bccf-eb4df772a69d)


Deploy the canary application with a 80%/20% traffic split, using the image docker.io/httpd. In the 80% and 20% ratio means that 80% of the traffic will be sent to the V1 of the app and 20% of the traffic will be sent to the V2 of the app. This way, if there are any problems with the V2 app, only a small number of users will be affected.

Create all deployment.

```bash
  $ kubectl create -f .
```

Then check if all pods are running.

```bash
  $ kubectl get pod -w
```
Now, add this message in 8 pods of V1.

```bash
  $  echo "this meassage from V1" > index.html 
```
Add this message in pod with the help of this command.

```bash
  $  kubectl cp index.html app-v1-pod-name:/usr/local/apache2/htdocs/
```
Add this message in 2 pods V2.
```bash
  $  echo "this meassage from V2" > index.html 
```
Use this command to add a message to a pod.
```bash
  $  kubectl cp index.html app-v2-pod-name:/usr/local/apache2/htdocs/
```
Now, check the service IP and port number.
```bash
  $  kubectl get svc
```
Run this command with your service IP, it will route on all pods, and the ratio of V2 to V1 is 80% and V2 to 20%.
```bash
  $  for VAR in {1..10}; do curl 10.110.204.186:80; done 
```

![image](https://github.com/Abhay956/canary_deployment_example/assets/132220412/8821fa91-db27-484c-a523-b17a947bf5b8)

