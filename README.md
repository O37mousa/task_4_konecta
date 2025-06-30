# task_4_konecta

---
## Initialize Minikube
First of all, we need to initialize (start) minikube by using: 
```bash
minikube start
```

![image](https://github.com/user-attachments/assets/7bbfa856-bce3-4fcb-a620-abde1d98a17d)

## 1. Create NGINX Pod via Command (no YAML)
Running a single "NGINX" pod using:
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

![image](https://github.com/user-attachments/assets/520a127c-dd41-4c60-aa7c-5c2075080fa5)
![image](https://github.com/user-attachments/assets/ea2609fa-63cd-4de9-86c9-d391547eb739)

![image](https://github.com/user-attachments/assets/c577e9f3-f994-43d7-9cce-dea8716fe4cc)

### 5
![image](https://github.com/user-attachments/assets/63542437-6844-4db3-b112-b964e62c1bd2)

![image](https://github.com/user-attachments/assets/e6b9e999-6510-4793-8212-a06b5e63cac2)

### 6
![image](https://github.com/user-attachments/assets/0b6bac11-f30e-429b-b90d-7e9ebb8807c9)
![image](https://github.com/user-attachments/assets/67eb1b2a-3813-423b-8447-7677076601bb)

### 7
![image](https://github.com/user-attachments/assets/4f4d0268-4a59-41de-8a4e-c30db7169125)
![image](https://github.com/user-attachments/assets/d5583814-7b5c-47f2-8876-9de12c8a33b2)

### 8
![image](https://github.com/user-attachments/assets/6c744def-2c33-487c-9d3a-c84492528882)
![image](https://github.com/user-attachments/assets/856a3bf7-e6d1-4a28-85bf-2d967257390e)
![image](https://github.com/user-attachments/assets/ab5f77d6-f909-448e-ade6-ad353faccc0a)

### 9
![image](https://github.com/user-attachments/assets/224e83d6-4cda-4cc4-95ec-57c50eaca9ae)
![image](https://github.com/user-attachments/assets/0621d3e9-4bbf-4a67-bc4a-2af5e4974d2d)
![image](https://github.com/user-attachments/assets/1b3e39ae-7cac-481f-8584-d28462a4da1b)

### 10
![image](https://github.com/user-attachments/assets/f2f32982-b7fe-44f7-9ed8-ef0d8667964f)

![image](https://github.com/user-attachments/assets/a043661d-40bf-427b-b51c-e98a7f942969)
![image](https://github.com/user-attachments/assets/a2730899-a692-4181-a7ce-9450909e3caf)


![image](https://github.com/user-attachments/assets/deb672bd-a828-434f-8fbc-0300701bf5ec)

### 11

### 15
![image](https://github.com/user-attachments/assets/9417b876-c7f2-4d16-823d-5ffd57312fc9)
![image](https://github.com/user-attachments/assets/3ca430be-4a41-44b7-8dc8-49ea6716fd0d)

### 16
![image](https://github.com/user-attachments/assets/d17ff5a5-799c-455b-bc1c-ba40e4e30695)
![image](https://github.com/user-attachments/assets/7cfe9ceb-2715-4936-bf32-6b828175f2ed)
#### the previous image shows that the image is incorrect

### 17
##### after rolling back
![image](https://github.com/user-attachments/assets/ae7f139b-f1cc-4233-bd49-8f2d485a1ec1)

### 18
![image](https://github.com/user-attachments/assets/4bd542ce-4e06-4098-bd55-d04d89fd8093)
![image](https://github.com/user-attachments/assets/640149b0-e45e-4072-a5a2-371141618dd7)
![image](https://github.com/user-attachments/assets/48245f3e-47bd-4552-be1c-c2afad4ac083)

### 19
![image](https://github.com/user-attachments/assets/65a889c9-5188-4a01-85fe-3c293fc7887b)
![image](https://github.com/user-attachments/assets/d8f7221f-074f-444b-914f-49f54b323c4d)

### 20
![image](https://github.com/user-attachments/assets/1dc84dc8-c089-49f0-8c6f-d433e35c841a)
![image](https://github.com/user-attachments/assets/cef0ce9b-d4d1-4325-beba-dfc293da9469)
![image](https://github.com/user-attachments/assets/be10379a-1bde-425c-976c-07fda3117a2a)

### 21
![image](https://github.com/user-attachments/assets/8782590c-0a32-40b8-9aca-df410ff07e49)

### 22
![image](https://github.com/user-attachments/assets/9a099e3a-2052-432d-a1d8-17fd43b9883d)

### 23
![image](https://github.com/user-attachments/assets/cd582748-f988-4d10-913e-dc13101ee7cc)

