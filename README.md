# task_4_konecta
## Kubernetes Task

---

## Initialize Minikube
First of all, we need to initialize (start) minikube by using: 
```bash
minikube start
```

![image](https://github.com/user-attachments/assets/7bbfa856-bce3-4fcb-a620-abde1d98a17d)

## 1. Create NGINX Pod via Command (no YAML)
Running a single NGINX pod using:
```bash
kubectl run mynginx --image=nginx
```

![image](https://github.com/user-attachments/assets/bc966508-5703-40cd-b510-0059a3713c12)

Checking for NGINX pods
```bash
kubectl get pods
```

![image](https://github.com/user-attachments/assets/df50653a-ff7b-41f9-a4c2-18bc56eef607)

## 2. Create NGINX Pod with Wrong Image (nginx123)
Command used:
```bash
kubectl run mynginx --image=nginx123
```
![image](https://github.com/user-attachments/assets/9a783c48-7891-4d27-8fdb-541940f9c9fa)

Check pods by:

![image](https://github.com/user-attachments/assets/b39f30cc-db92-42a9-bd93-76ad8bc20d30)

-> Output: We can conclude that Pod created but crashes due to image pull error

## 3. Check Pod status and check why it fails
To check for the Pod status and every details in the pod, use:
```bash
kubectl describe pod mynginx
```
Basic Details:

![image](https://github.com/user-attachments/assets/520a127c-dd41-4c60-aa7c-5c2075080fa5)

More details:

![image](https://github.com/user-attachments/assets/ea2609fa-63cd-4de9-86c9-d391547eb739)

-> Output: ImagePullBackOff error is shgown due to `nginx123` does not exist in DockerHub

## 4. Get Pod name, IP, and Image
This is applied by using:
```bash
kubectl get pod mynginx -o wide
```

![image](https://github.com/user-attachments/assets/c577e9f3-f994-43d7-9cce-dea8716fe4cc)

-> Outputs the node name, IP Address and Image that was used.

## 5. Delete Pod
Pod is deleted by using:
```bash
kubectl delete pod mynginx
```

![image](https://github.com/user-attachments/assets/63542437-6844-4db3-b112-b964e62c1bd2)

Check the Pods:

![image](https://github.com/user-attachments/assets/e6b9e999-6510-4793-8212-a06b5e63cac2)

## 6. Create Pod using YAML with Labels
Creating the Pod using the YAML file through the command:
```bash
kubectl apply -f mynginx.yaml
```

![image](https://github.com/user-attachments/assets/0b6bac11-f30e-429b-b90d-7e9ebb8807c9)

Check the created Pod:

![image](https://github.com/user-attachments/assets/67eb1b2a-3813-423b-8447-7677076601bb)

## 7. Create ReplicaSet of 3 replicas
ReplicaSet have been created of 3 Replicas using the NGINX image in YAML file using command:
```bash
kubectl apply -f replicaset.yaml
```

![image](https://github.com/user-attachments/assets/4f4d0268-4a59-41de-8a4e-c30db7169125)

Check the created ReplicaSets:

![image](https://github.com/user-attachments/assets/d5583814-7b5c-47f2-8876-9de12c8a33b2)

## 8. ReplicaSet Scaling
Scaled the ReplicaSet to be 5 without editing in the YAML file through the command:
```bash
kubectl scale rs nginx-replicaset --replicas=5
```

![image](https://github.com/user-attachments/assets/6c744def-2c33-487c-9d3a-c84492528882)

Check the updated Replicas, new replicas are created to be 5 replicas

![image](https://github.com/user-attachments/assets/856a3bf7-e6d1-4a28-85bf-2d967257390e)

![image](https://github.com/user-attachments/assets/ab5f77d6-f909-448e-ade6-ad353faccc0a)

## 9. Pod deletion from the Replicaset
Delete Pod from Replicaset using command:
```bash
kubectl delete pod nginx-replicaset-gmwj7 
```

`nginx-replicaset-gmwj7` = podID/podName

![image](https://github.com/user-attachments/assets/224e83d6-4cda-4cc4-95ec-57c50eaca9ae)

The Replicaset has been deleted and another one has been replaced to create and make it have 5 Replicas once again.

![image](https://github.com/user-attachments/assets/0621d3e9-4bbf-4a67-bc4a-2af5e4974d2d)
![image](https://github.com/user-attachments/assets/1b3e39ae-7cac-481f-8584-d28462a4da1b)

## 10. Downscaling Pods
Pods scaled down to be **ONLY** 2 pods without using the `scale` command, but using:
```bash
kubectl edit rs nginx-replicaset
```

![image](https://github.com/user-attachments/assets/f2f32982-b7fe-44f7-9ed8-ef0d8667964f)

Pods Configuration script has been shown once the command has been entered, then navigate to `spec.replicas` and adjust it to be _**2**_ instead of _**5**_, then exit the script shelll by pressing `esc` button then writing `:wq`

![image](https://github.com/user-attachments/assets/a043661d-40bf-427b-b51c-e98a7f942969)
![image](https://github.com/user-attachments/assets/a2730899-a692-4181-a7ce-9450909e3caf)

Once exited, it will show that the `nginx-replicaset` has been edited.

![image](https://github.com/user-attachments/assets/deb672bd-a828-434f-8fbc-0300701bf5ec)

## 11. Find Error in ReplicaSet YAML
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-2
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
```
-> i think 'tier' should be changed to app, also the template.metadata.labels.tier = "nginx" does not match with the selector.matchLabels.tier = "frontend" 

## 12. Find out the issue in the YAML
```
apiVersion: apps/v1
kind: deployment
metadata:
  name: deployment-1
spec:
  replicas: 2
  selector:
    matchLabels:
      name: busybox-pod
  template:
    metadata:
      labels:
        name: busybox-pod
    spec:
      containers:
      - name: busybox-container
        image: busybox
        command:
        - sh
        - "-c"
        - echo Hello Kubernetes! && sleep 3600
```

-> I am not sure, but I think kind should be renamed = "Deployment" instead of "deployment"

## 13. Find out the issue in the YAML
```
apiVersion: v1
kind: Deployment
metadata:
  name: deployment-1
spec:
  replicas: 2
  selector:
    matchLabels:
      name: busybox-pod
  template:
    metadata:
      labels:
        name: busybox-pod
    spec:
      containers:
      - name: busybox-container
        image: busybox
        command:
        - sh
        - "-c"
        - echo Hello Kubernetes! && sleep 3600
```

-> I think that the apiVersion should be "apps/v1" NOT just "v1"

## 14. What's the command used to know what Image name that running the deployment
```
kubectl get deployment <deployment-name> -o jsonpath="{.spec.template.spec.containers[*].image}"
```

## 15. Create a deployment using the following 
  - Name: httpd-frontend;
  - Replicas: 3;
  - Image: httpd:2.4-alpine

After creation of `httpd-frontend.yaml` file in a separate directory, apply the command:
```
kubectl apply -f deployment/httpd-frontend.yaml
``` 

![image](https://github.com/user-attachments/assets/9417b876-c7f2-4d16-823d-5ffd57312fc9)

Then, check deployment pods

![image](https://github.com/user-attachments/assets/3ca430be-4a41-44b7-8dc8-49ea6716fd0d)

## 16. Replacing Image with command
Pod image is changed to be `nginx777`, using the following command:
```
kubectl set image deployment/httpd-frontend httpd=nginx777
```

![image](https://github.com/user-attachments/assets/d17ff5a5-799c-455b-bc1c-ba40e4e30695)

Check the Pods

![image](https://github.com/user-attachments/assets/7cfe9ceb-2715-4936-bf32-6b828175f2ed)
#### the previous image shows that the image is incorrect, as it is not available on Docker Hub

### 17. Roll back to the previous version
Using:
```
kubectl rollout undo deployment httpd-frontend
```

![image](https://github.com/user-attachments/assets/ce148781-bd05-494b-9fa0-1766c6d728ae)

After rolling back

![image](https://github.com/user-attachments/assets/ae7f139b-f1cc-4233-bd49-8f2d485a1ec1)

## 18. Create a Web App
Create a Dcokerfile that create a simple web application such as `nginx`, then build the docker image and push it to the DockerHub of my private account.
```
docker build -t omousa37/my-nginx-app .
```

![image](https://github.com/user-attachments/assets/4bd542ce-4e06-4098-bd55-d04d89fd8093)

Docker account logging in using:
```
docker login
```
Then, open browser to verify the authentication.

![image](https://github.com/user-attachments/assets/640149b0-e45e-4072-a5a2-371141618dd7)

Finally, push the docker image to the DockerHub using:
```
docker push omousa37/my-nginx-app
```

![image](https://github.com/user-attachments/assets/48245f3e-47bd-4552-be1c-c2afad4ac083)

### 19. Create a deployment
Apply a deplyment to deploy the docker image uploaded from DockerHub to K8s that has 3 Replicas using 
```
kubectl apply -f web_deploy.yaml
```

![image](https://github.com/user-attachments/assets/65a889c9-5188-4a01-85fe-3c293fc7887b)

Check the newly created pods:

![image](https://github.com/user-attachments/assets/d8f7221f-074f-444b-914f-49f54b323c4d)

## 20. Expose the Frontend

Exposing the Frontend page using a servide to make it accessible from the browser using
```
kubectl expose deployment web-deployment --type=NodePort --port=80
```

![image](https://github.com/user-attachments/assets/1dc84dc8-c089-49f0-8c6f-d433e35c841a)

Create a URL for access through
```
minikube service web-deployment --url
```
Then, open the URL preovided on a browser

![image](https://github.com/user-attachments/assets/cef0ce9b-d4d1-4325-beba-dfc293da9469)
![image](https://github.com/user-attachments/assets/be10379a-1bde-425c-976c-07fda3117a2a)

## 21. Create a Backend
Create another Deployment for the backend using the following:
  - Image: python:3.8-slim
  - Command: ["python", "-m", "http.server", "8080"] (include this command in the deployment file)'

After creating the `ba_deploy.yaml` file, apply it using
```
kubecxtl apply -f be_deploy.yaml
```
![image](https://github.com/user-attachments/assets/8782590c-0a32-40b8-9aca-df410ff07e49)

## 22. Expose the Backend 
![image](https://github.com/user-attachments/assets/9a099e3a-2052-432d-a1d8-17fd43b9883d)

### 23
![image](https://github.com/user-attachments/assets/cd582748-f988-4d10-913e-dc13101ee7cc)

