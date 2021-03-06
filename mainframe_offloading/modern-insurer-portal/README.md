## Development mode

Run the application.
Notes:
* Assumption is that the first command is executed from the directory `<repo-root>/mainframe_offloading/modern-insurer-portal`
* `npm install` is only required for the first time or when dependencies change

```
host$ docker run -it --rm -v $(pwd):/home/app -p 3001:3000  node:9.5 /bin/bash
container$ cd /home/app
container$ npm install
container$ npm start
```

Open a browser pointing at http://localhost:3000/

## Package Docker container

The repository includes a Dockerfile to package the legacy-insurer-portal as container.

Replace `mentlsve/modern-insurer-portal` with whatever name you like:

```
host$ cd packaging
host$ docker build -t mentlsve/legacy-insurer-portal .
```
Then run the application with
```
host$ docker run -d -p 3000:3000 --name=legacy-insurer-portal mentlsve/legacy-insurer-portal
```

Open a browser pointing at http://localhost:3000/

Kill the container with
```
host$ docker rm -f legacy-insurer-portal
```

## Run on minikube

The repository includes Kubernetes manifests to create a deployment and expose a service.

Deploying to minikube
```
host$ minikube start
host$ kubectl apply -f packaging/deployment.yaml
host$ kubectl apply -f packaging/service.yaml
host$ minikube ip
192.168.99.100
```

You should then be able to open a browser and reach the application on http://192.168.99.100:30100



