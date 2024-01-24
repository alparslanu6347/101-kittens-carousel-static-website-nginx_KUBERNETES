- Worker-node'a git

- Worker-node içerisinde ``Project-101-kittens-carousel-static-website-nginx_KUBERNETES`` isimli klasör oluştur ==>> ``PersistentVolume``  tanımlarken ``hostPath`` olarak belirteceğiz. Bu klasörü oluşturmasan da "PersistentVolume" tanımlarken bu klasör kendisi oluşacak.

- Master-node'a git

```bash
mkdir Lesson
cd Lesson
```
  
- Master-node içerisinde çalışacağın klasör yapısı aşağıdaki gibi olsun :

    ├── kittens-deploy.yaml
    ├── kittens-service.yaml
    ├── kittens-pv.yaml
    ├── kittens-pvc.yaml
    ├── commands.md
    ├── Dockerfile
    └── myapp (klasör)
        ├── cat0.jpg
        ├── cat1.jpg
        ├── cat2.jpg
        └── index.html

- Dockerfile oluşturalım , image oluşturalım , dockerhub'a push edelim.

```bash
touch Dockerfile

    # FROM nginx:latest
    # RUN apt-get update -y
    # COPY /myapp /usr/share/nginx/html
    # WORKDIR /myapp
    # EXPOSE 80 	
    # CMD ["nginx", "-g", "daemon off;"]

docker build -t "alparslanu6347/kittens-nginx:1.0" .        # alparslanu6347 : dockerhub username
docker login # username: alparslanu6347  , password: alpU063470
docker alparslanu6347/kittens-nginx:1.0
```

- Dockerhub hesabımda bulunan image'i (yukarıda oluşturduğum) kullanarak Kubernetes ile uygulamayı çalıştıralım.

```bash
kubectl apply -f .
kubectl get ns,po,svc,deploy,pv,pvc
http://[public-node-ip]:[node-port] # http://54.127.45.88:30333  (nodePort: 30333)
kubectl delete -f .
```
