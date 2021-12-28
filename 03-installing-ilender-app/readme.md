# Watson AIOps AI-Manager Installation

This article explains about how to install iLender demo app and how to generate load in the app for training.

This application can be installed on any of the Kubernetes cluster (IKS, OCP and etc)

## 1. Deploying iLender Application

### 1. Update Humio properties

Update `humioUrl` and `humioToken` properties in the file `./yaml/20-deployable-common.yaml`

```
  humioUrl: http://1.1.1.1:8080/api/v1/ingest/humio-unstructured
  humioToken: 
```

### 2. Apply the yaml

Apply the yaml in the Openshift or Kubernetes (OCP/IKS) clusters

```
kubectl apply -f ./yaml
```

### 3. Access the app

App is installed in the `ilender-ns` namespace.

![ilender](./images/iLender-Login.png)


#### 3.1 User Id and Password

```
sam/sam
sandy/sandy
```

#### 3.2 URLs

You can access the application using the `EXTERNAL-IP` from node and `NodePort` from svc.

#### 3.2.1 Get EXTERNAL-IP

Run the below command to get `EXTERNAL-IP`

```
kubectl get nodes -o wide
```

Output could be like this.

```
Jeyas-MacBook-Pro:frontuiservice jeyagandhi$ kubectl get nodes -o wide
NAME             STATUS   ROLES    AGE   VERSION       INTERNAL-IP      EXTERNAL-IP       OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
10.241.253.157   Ready    <none>   26d   v1.20.7+IKS   10.241.253.157   1.1.1.1   Ubuntu 18.04.5 LTS   4.15.0-144-generic   containerd://1.4.6
10.241.253.189   Ready    <none>   26d   v1.20.7+IKS   10.241.253.189   1.2.3.5   Ubuntu 18.04.5 LTS   4.15.0-144-generic   containerd://1.4.6
```

#### 3.2.2 Get NodePort

Run the below command to get `NodePort`of the svc

```
kubectl get svc
```

Output could be like this.

```
Jeyas-MacBook-Pro:frontuiservice jeyagandhi$ kubectl get svc
NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)          AGE
ilender-bigbank           ClusterIP   172.21.165.179   1.1.1.1       9090:30598/TCP   10d
ilender-creditscore       NodePort       172.21.55.156    <none>          9090:30601/TCP   10d
ilender-customerprofile   ClusterIP   172.21.145.229   1.1.1.1   9090:32751/TCP   10d
ilender-frontweb          NodePort       172.21.44.159    <none>          9090:30600/TCP   10d
ilender-greatbank         ClusterIP   172.21.84.144    <pending>       9090:31622/TCP   10d
ilender-loan              ClusterIP   172.21.161.226   1.1.1.1   9090:30301/TCP   10d
ilender-loanprocessor     ClusterIP   172.21.82.15     1.1.1.1   9090:30880/TCP   10d
ilender-openbanking       ClusterIP   172.21.235.41    1.1.1.1   9090:31331/TCP   10d
ilender-user              ClusterIP   172.21.43.214    1.1.1.1       9090:32427/TCP   10d
```

#### 3.2.3 Get URLs

The URL would be of this format.

```
http://< EXTERNAL-IP >: < NodePort >
```

Here are the 2 urls that we need.

```
App URL  (ilender-frontweb) : http://1.1.1.1:30600
CreditScore Service URL  (ilender-creditscore) : http://1.1.1.1:30601
```


## 2. Generate Load for iLender App

Here we use docker image to create a load. 

### 1. Open the file script file

Open the file `files/01-create-load.sh`

### 2. Update iLender URL

In the above script file, update the below property to point to iLender URL

```
export P_HOST=http://1.1.1.1:30600
```

### 3. Load duration

By default the load is generated for 20 minutes. You can increase it by updating this property. 

```
export P_TIME_DURATION=20m
```

### 4.  Run the load

Run the below script to start the load. It will run for the given time duration and stop automatically.

```
sh files/01-create-load.sh
```

### To Stop the load in-between

To stop the load in the middle you can use the below commands.

```
Jeyas-MacBook-Pro:~ jeyagandhi$ docker ps
CONTAINER ID   IMAGE                               COMMAND      CREATED          STATUS          PORTS     NAMES
d396bd6c2ca8   gandigit/ilender-load-dev-2:0.0.1   "./run.sh"   23 seconds ago   Up 22 seconds             naughty_mendeleev
```

```
Jeyas-MacBook-Pro:~ jeyagandhi$ docker stop d396bd6c2ca8
d396bd6c2ca8
```




