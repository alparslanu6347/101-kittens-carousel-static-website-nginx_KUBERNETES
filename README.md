# 101-kittens-carousel-static-website-nginx_KUBERNETES

- Go to the `Worker_node`

- In the worker node, create a folder named `Project-101-kittens-carousel-static-website-nginx_KUBERNETES`  ==>> We will specify this folder as the `hostPath` while defining the `PersistentVolume`. Even if you don't create this folder, it will be automatically created when defining the `PersistentVolume`.

- Go to the `Master node`

```bash
mkdir Lesson
cd Lesson
tree
```
  
- The folder structure you will work with in the Master node should be as follows :

    ├── kittens-deploy.yaml
    ├── kittens-service.yaml
    ├── kittens-pv.yaml
    ├── kittens-pvc.yaml
    ├── commands.md
    ├── Dockerfile
    └── myapp (sub-folder)
        ├── cat0.jpg
        ├── cat1.jpg
        ├── cat2.jpg
        └── index.html

- Let's create a `Dockerfile`, build an image, and push it to `Docker Hub`.

```bash
touch Dockerfile
```

```Dockerfile
FROM nginx:latest
RUN apt-get update -y
COPY /myapp /usr/share/nginx/html
WORKDIR /myapp
EXPOSE 80 	
CMD ["nginx", "-g", "daemon off;"]
```

```bash
docker build -t "alparslanu6347/kittens-nginx:1.0" .        # alparslanu6347 : dockerhub username
docker login                                                # username: alparslanu6347  ; password: ********
docker alparslanu6347/kittens-nginx:1.0
```

- Using the image I created and pushed to my Docker Hub account, let's deploy the application with Kubernetes.

```bash
kubectl apply -f .
kubectl get ns,po,svc,deploy,pv,pvc
http://[public-node-ip]:[node-port] # http://54.127.45.88:30333  (nodePort: 30333)
kubectl delete -f .
```
