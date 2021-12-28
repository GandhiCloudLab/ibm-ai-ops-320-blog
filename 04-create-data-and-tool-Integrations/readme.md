# Create Data and Tool Integrations

This article explains about how to setup below Integration in Watson AIOps.

- Humio Integration
- ServiceNow Integration
- Kubernetes Integration

The article is based on the the following.

- RedHat OpenShift 4.8 on IBM Cloud (ROKS)
- Watson AIOps 3.2.0

## 1. Setup Humio Integration

This section explains about how to setup Humio Integration in Watson AIOps.

1. Goto the page `Data and tool integrations`

2. Click on  `Add Integration`

![Humio](./images/image-00001.png)

3. In the `Humio` card click on the `Add Integration` link

![Humio](./images/image-00002.png)

4. Click on `Connect` 

![Humio](./images/image-00003.png)

5. Enter the below field values

- Name 
- Description 
- Humio sevice URL

    Sample value : http://1.1.1.1:8080/api/v1/repositories/sandbox/query

- API Key of the Humio (Should be Account key not the ingestion key)

To know more about humio url and token refer to the url : 

6. Click on `Next` 

![Humio](./images/image-00004.png)
![Humio](./images/image-00005.png)

6. Click on `Test Connection` to check the connection with humio

7. Click on `Next`

![Humio](./images/image-00006.png)

8. Enter the below field values

- Dataflow : Off 
- Mode: Historical ..
- Start Date : yesterday date
- End Date  : tommorrow date

7. Click on `Done`

![Humio](./images/image-00007.png)

8. Humio connection created

![Humio](./images/image-00008.png)


## 2. Setup ServiceNow Integration

This section explains about how to setup ServiceNow Integration in Watson AIOps.

1. Goto the page `Data and tool integrations`

2. Click on  `Add Integration`

![ServiceNow](./images/image2-00001.png)

3. In the `ServiceNow` card click on the `Add Integration` link

![ServiceNow](./images/image2-00002.png)

4. Click on `Connect` 

![ServiceNow](./images/image2-00003.png)

5. Enter the below field values

- Name 
- Description 
- ServiceNow URL
- User
- Password

6. Click on `Next` 

![ServiceNow](./images/image2-00004.png)

7. Click on `Test Connection` to check the connection with humio

8. Click on `Next`

![ServiceNow](./images/image2-00005.png)

9. Click on `Next`

![ServiceNow](./images/image2-00006.png)

10. Enter the below field values

- Dataflow : Off 
- Mode: Historical ..
- Start Date : Last year date
- End Date  : tommorrow date

11. Click on `Done`

![ServiceNow](./images/image2-00007.png)

12. ServiceNow connection created

![ServiceNow](./images/image2-00008.png)

## 3. Setup Kubernetes Integration or Observer

This section explains about how to setup Kubernetes Observer in Watson AIOps.

### 1. Get Kubernetes Cluster Access Details

As part of the kubernetes observer, it is required to communicate with the target cluster. So it is required to have the URL and Access token details of the target cluster. 

Do the following.


#### 1. Login

Login into Kubernetes cluster using cli.

#### 2. Access token 

There is a script file [files/00-create-kube-observer-token.sh](./files/00-create-kube-observer-token.sh) to generate access token in Kubernetes cluster

Run the script.

```
sh files/00-create-kube-observer-token.sh
```

This will print the access token, you can copy and keep it in notepad.

#### 3. URL and Port 

Need to get the URL and Port of the Kubernetes Cluster

In the IBM Cloud, cluster detail page, Click on the `Copy Link` link under the `Servive Point URL` to get the Kubernetes URL. 

It may give a url like this 

```
https://c111.us-south.containers.cloud.ibm.com:32429
```

<img src="images/image3-00016.png">

### 2. Create Kube Observer Connection

1. Click on `Add Connection`

<img src="images/image3-00001.png">

2. Click on `Add Connection`

<img src="images/image3-00002.png">

3. Click on `Connect`

<img src="images/image3-00003.png">

4. Enter any value in `Name`,  `Description` and `Data Center`

<img src="images/image3-00004.png">

5. Enter the following

 - Connection Type : Load
 - IP Address : `URL` portion of the `Service Enpoint URL` retrieved in the above section
 - Port : `Port` portion of the `Service Enpoint URL` retrieved in the above section
 - Token : `Access Token` retrieved in the above section
 - Namespace : Any name where you have deployed your app to observe

6. Click on `Next`

<img src="images/image3-00005.png">
<img src="images/image3-00006.png">
<img src="images/image3-00007.png">

7. Enter the following

 - Schedule Request : On
 - Interval : 5

8. Click on `Done`

<img src="images/image3-00008.png">

9. Kubernetes connection is created successfully. This might have observer the resources found in the given namespace of the kubernetes cluster and create a Resource group

<img src="images/image3-00009.png">
