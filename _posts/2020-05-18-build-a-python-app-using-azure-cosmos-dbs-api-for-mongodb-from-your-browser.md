---
id: 193
title: 'Python web app with Cosmos DB on Azure'
date: '2020-05-18T22:50:06+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=193'
permalink: /build-a-python-app-using-azure-cosmos-dbs-api-for-mongodb-from-your-browser/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - 'App service'
    - Azure
    - CosmosDB
format: image
---

This tutorial will show how to create a Python straight from your browser, with free Azure resources only. You will learn how to deploy a Cosmos DB Account, and a Web App from Git using the Azure Cloud Shell without installing any software in your local computer

Based on SARATH LAL’s <https://codewithsarath.com/a-simple-to-do-python-flask-application-with-mongodb/> and Microsoft’s <https://docs.microsoft.com/en-us/azure/cosmos-db/create-mongodb-flask/>

##### [](https://github.com/azuretar/python-cosmosdb-azure-webapp-tutorial#requisitos)**Prerequisites**

- A computer with a modern web browser (Edge, Chrome or Firefox)
- Free Azure Account https://azure.microsoft.com/en-us/free/
- Free Azure Cosmos DB’s API for MongoDB
- Azure Cloud Shell

##### [](https://github.com/azuretar/python-cosmosdb-azure-webapp-tutorial#instru%C3%A7%C3%B5es)**Instructions**

First of all you need to create a free Azure account using this link [https://azure.microsoft.com/en-us/free/](https://azure.microsoft.com/pt-br/free/) it provide some free credits on the first month, free services for 12 months and other free services forever. When you get your account you will use the URL <https://portal.azure.com/> to access your Azure GUI.

**Create an Azure Cosmos DB’s API for MongoDB account**

**Step 1**: On portal.azure.com top search bar type “cosmos” and click on “Azure Cosmos DB”

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/1-2.jpg)</figure>**Step 2:** Click on +Add

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/2-1.jpg)</figure>**Step 3**: Fill the form:

- **Subscription**: Select your free subscription (Free Trial)
- **Resource Groups**: Create a new resource group, Remember this you use it on the next step and it will make easy to delete this deployment on the future.
- **Account Name**: Choose a name for your account.
- **API:** Select Azure Cosmos DB for MongoDB API
- **Notebooks:** Select Off
- **Apply Free Tier Discount**: Select Apply, it will apply your free tier discount to use Cosmos DB for free.
- **Location:** Select the closest locations for your users, it will provide a responsive app.
- **Account Type:** Non-Production. It is only a tag, you can choose whatever you want.
- **Version:** Select 3.6
- **Geo-Redundancy:** Select Disable. In this example, we will use only one geographic location, but if you are deploying a highly available service you should select yes.
- **Multi-region Writes:** Select Disable. When you deploy an App with a global footprint, it will accelerate your app world widely.

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/3.jpg)</figure>**Setp 4**: On the screenshot above click on review and create, then click on create (illustrated below).

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/4.jpg)</figure>**Step 5**: Access your Azure Cloud Shell, clicking on the terminal icon on the Azure’s Portal top bar

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/5.jpg)</figure>**Step 6:** If it is your first time create the storage account to work with the Cloud Shell. This account use Azure Files, a service that allows you to access this files on your computer as a network share. Remember, at the time I’m writing this article Azure gives away free 5Gb storage on the first 12 months.

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/6.jpg)<figcaption>Click on Create Storage to proceed with the Azure Cloud Shell</figcaption></figure>**Step 7**: Now we will clone the Github repository on our Azure Cloud Shell. We will use the git clone command with our repository URL

```
git clone https://github.com/azuretar/python-cosmosdb-azure-webapp-tutorial.git
```

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/7.jpg)</figure>**Step 8:** Now we have the source code, let’s change the directory to the cloned git

```
cd python-cosmosdb-azure-webapp-tutorial/
```

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/8.jpg)</figure>**Step 9:** To test the App we need to Install the Python requirements, we will do that using pip, with the following command

```
pip install -r requirements.txt
```

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/9.jpg)</figure>**Step 10**: Now we need to edit the code to insert the Cosmos DB details. We will use the code editor included on the Azure Cloud Shell, to open the editor use the following command:

```
code .
```

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/10.jpg)<figcaption>As you can see, the files are on the left hand side and the editor on the right hand side.</figcaption></figure>**Step 11**: We need to edit the app.py, open it clicking on app.py and you will view the file opened on editor.

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/11.jpg)<figcaption>Watch for the line starting with client = MongoClient…</figcaption></figure>**Step 12:** Now we need to get the database details to connect our app, so open a new tab on [portal.microsoft.com](https://portal.microsoft.com/) in your browser and Access the Cosmos DB account you have created, click in Settings /Connection String and copy the PRIMARY CONNECTION STRING

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/12.jpg)</figure>**Step 13**: Now you can go back to the code editor and paste the Primary Connection String between the signalled quotes and save and close the editor.

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/13.jpg)</figure>**Python Tip**: This “r” before the Primary Connection String makes the Python accept the “&amp;” character included on the string.

**Step 14:** Let’s test the app. Run the code with the following command:

```
python app.py
```

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/14.jpg)<figcaption>As you can see the app is waiting for conections on http://127.0.0.1:5000, which means the port 5000 on localhost, but the localhost inside the Cloud Shell Container</figcaption></figure>**Step 15**: To be able to see the website preview, Click on Web Preview icon (highlighted), click on Configure, type the 5000, and click open and browse, check if the site opens

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/15.jpg)<figcaption>The webpreview open maps the conection from your browser to inside the container</figcaption></figure><figure class="wp-block-image size-large">![](https://azuretar.com/wp-content/uploads/2020/05/15.1.jpg)<figcaption>The Web App test is working!</figcaption></figure>**Step 16:** Now you have seen the app working. go back to the Cloud Shell and stop the code pressing CTRL+C

<figure class="wp-block-image size-large">![](https://azuretar.com/wp-content/uploads/2020/05/16.jpg)</figure>**Step 17:** Now let’s publish this App on Azure Web App via AZ CLI. We could do that using the Azure Web interface, but now let’s try an AZ CLI Command

```
az webapp up --sku F1 --name <name of your application> --resource-group <use the same resource group you>
```

The AZ CLI stands for Azure Command Line Interface, which can deploy anything to Azure and helps a lot with automation. The AZ Cli comes pre-configured to the Azure Cloud Shell. Bellow the command explanation. You need write the command with your own application name and resource group.

- az is the main command
- webapp is the command to manage Web Apps
- up is the command to deploy your Web App
- –sku let you select the WebApp size, in this case we are using the F1 that is the Free Tier
- –name is where you specify your app name. Your Web App URL you be https://&lt;name&gt;.azurewebsites.net/
- –resource-group is where you specify your resource group. Use the same as your Cosmos DB Account

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/17.jpg)</figure>**Step 18**: Now let’s check what our az command has created. On [portal.microsoft.com](https://portal.microsoft.com/) search for App Services, click on the Web App you have created, then click on the App URL and check it working!

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/18.jpg)<figcaption>You will see the Web App you have created, then click on its name.</figcaption></figure><figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/18.1.jpg)<figcaption>Here you can see all properties and click in you Web App URL to open your deployment</figcaption></figure><figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/18.2.jpg)<figcaption>Now you can test the Application</figcaption></figure>**Step 19 (Optional)**: Everything you have created in this tutorial is free, you can keep online, but if you want to delete. Type Resource Groups on the portal search bar

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/19.jpg)</figure>Fird the resource group you have deployed your Web App and Cosmos DB and click on it. You will see all your resources inside, then click on “Delete resource group”

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/19.1.jpg)</figure>Type the recource group name and click on delete.

<figure class="wp-block-image size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/05/19.2.jpg)</figure>After a few minutes all resources will be deleted. You can Create another free Cosmos DB and WebApp again.