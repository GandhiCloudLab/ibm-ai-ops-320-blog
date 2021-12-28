# Create AI-Model Definition

This article explains about how create to AI-Model Definition for the following in Watson AIOps.

- Log Anomaly detection
- Similar Incidents

The article is based on the the following

- RedHat OpenShift 4.8 on IBM Cloud (ROKS)
- Watson AIOps 3.2.0


## 1. Create AI-Model Definition for log anomaly

1. Click on `AI Model Management` link

<img src="images/image-00001.png">

2. Click on `Configure` link in `Log anomaly detection - natural language` card

<img src="images/image-00002.png">

3. Click on `Next` 

<img src="images/image-00003.png">

4. Enter the below field values

- Configuration Name 
- Configuration Description 

5. Click on `Next` 

<img src="images/image-00004.png">

4. Enter the below field values

- Custom : On
- Start Date: Yesterday date
- End Date: Tomorrow date

(While training, we will go for live logs and the date of the live logs should fall under this date range)

5. Click on `Next` 

<img src="images/image-00005.png">

5. Click on `Next` 

<img src="images/image-00006.png">

5. Click on `Next` 

<img src="images/image-00007.png">

4. Enter the below field values

- Deployment Type : On Completion

5. Click on `Done` 

<img src="images/image-00008.png">

5. See the status as `Configured` 

<img src="images/image-00009.png">

9. Click on `Manage` tab.

The Log Anomaly model training definition is displayed.

<img src="images/image-00010.png">


## 2. Create AI-Model Definition for Similar Incidents


1. Goto the page `AI Model Management`

2. Click on `Configure` link in `Similar Incidents` card

![ServiceNow](./images/image2-00002.png)

3. Click on `Next`

![ServiceNow](./images/image2-00003.png)

4. Enter the below field values

- Configuration Name 
- Configuration Description 

5. Click on `Next` 

![ServiceNow](./images/image2-00004.png)

6. Click on `Next` 

![ServiceNow](./images/image2-00005.png)

7. Click on `Done` 

![ServiceNow](./images/image2-00006.png)

8. Similar incidents training definition is created

![ServiceNow](./images/image2-00007.png)

9. Click on `Manage` tab.

The Similar incidents  training definition is displayed.

![ServiceNow](./images/image2-00008.png)