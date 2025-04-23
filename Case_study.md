# AZ-204 Instructor Case Studies for Azure Development

## Case Study 1: Building a Web App with Azure SQL Database and Blob Storage

**Scenario:**  
You are tasked with developing an event registration platform. Users will register for events, upload profile pictures, and view their registration history.

**Azure Services:**  
- Azure Web App  
- Azure SQL Database  
- Azure Blob Storage  

**Requirements:**  
- Host a .NET 6 Web App in Azure App Service.  
- Store user and event data in Azure SQL.  
- Store uploaded profile pictures in Blob Storage.  

**Implementation Steps:**  
1. Deploy a Web App using Azure App Service.  
2. Create an Azure SQL Database and configure the connection string in App Settings.  
3. Create a Blob Storage account and container for storing images.  
4. Use Azure SDK for .NET to upload images to Blob Storage.  
5. Store image URL in SQL database linked to user profile.  
6. Add Application Insights to monitor app performance.  

**Learning Goals:**  
- Integrate Azure SQL with Web App.  
- Handle file storage with Blob.  
- Use managed identity for secure access.  

---

## Case Study 2: Serverless Backend using Azure Functions and Azure Storage Queues

**Scenario:**  
You’re building a backend process to resize uploaded images. When a user uploads an image, it should be processed in the background.

**Azure Services:**  
- Azure Function (Queue Trigger)  
- Azure Blob Storage  
- Azure Storage Queue  

**Requirements:**  
- When an image is uploaded, add a message to the queue.  
- Azure Function picks the message and resizes the image.  
- Save the resized image in another blob container.  

**Implementation Steps:**  
1. Create a Storage Account with 2 Blob Containers (original and resized).  
2. Add a Queue to the Storage Account.  
3. Write an Azure Function that is triggered by a new message in the queue.  
4. The function reads the blob, resizes the image, and writes it to the resized container.  
5. Log function execution to Application Insights.  

**Learning Goals:**  
- Use serverless compute effectively.  
- Handle blob and queue storage.  
- Implement scalable background jobs.  

---

## Case Study 3: VM-Based Legacy App Modernization

**Scenario:**  
You are migrating a legacy on-prem .NET Framework app to Azure. The app requires a Windows environment and access to SQL Server.

**Azure Services:**  
- Azure Virtual Machine (Windows)  
- Azure SQL Managed Instance  
- Azure Storage (for backups)  

**Requirements:**  
- Host the legacy app on a Windows VM.  
- Move the database to Azure SQL Managed Instance.  
- Use Blob Storage for database backup and logs.  

**Implementation Steps:**  
1. Provision a Windows Server VM.  
2. Install IIS and deploy the legacy app.  
3. Set up an Azure SQL Managed Instance and migrate DB using Data Migration Assistant.  
4. Connect app to SQL MI with private endpoint or VNet integration.  
5. Configure Blob Storage for regular database backups.  

**Learning Goals:**  
- Lift-and-shift legacy apps.  
- Use managed services like SQL MI.  
- Secure and monitor VMs and networking.  

---

## Case Study 4: Secure API using Azure Functions and Azure Key Vault

**Scenario:**  
You’re building a secure API endpoint to process payments. The API must use a secret key to access a third-party payment provider.

**Azure Services:**  
- Azure Functions (HTTP Trigger)  
- Azure Key Vault  
- Azure App Configuration (optional)  

**Requirements:**  
- Host a secure serverless API using Azure Functions.  
- Store API keys in Azure Key Vault.  
- Use Managed Identity to access secrets.  

**Implementation Steps:**  
1. Write an Azure Function with an HTTP trigger for payment processing.  
2. Store the third-party API key in Azure Key Vault.  
3. Assign a system-managed identity to the function.  
4. Access Key Vault secrets using Azure SDK.  
5. Log all transactions securely using Application Insights.  

**Learning Goals:**  
- Secure secrets with Key Vault.  
- Access secrets using managed identity.  
- Design stateless, secure APIs.  

---

## Case Study 5: Scalable Web Solution using App Service Plan and Azure Monitor

**Scenario:**  
You are building an online learning platform that needs to scale based on usage.

**Azure Services:**  
- Azure App Service  
- Azure SQL Database  
- Azure Monitor  
- Azure Auto Scale  

**Requirements:**  
- Host the platform using Azure Web App.  
- Use Azure SQL to manage course data.  
- Automatically scale based on CPU usage.  
- Monitor application health.  

**Implementation Steps:**  
1. Deploy the Web App in a Standard App Service Plan.  
2. Configure Auto Scale rules based on CPU and request count.  
3. Set up Azure Monitor to collect logs and performance data.  
4. Add alerts and dashboards to track anomalies.  
5. Enable diagnostic logging for HTTP requests and errors.  

**Learning Goals:**  
- Design for scalability.  
- Monitor applications in real time.  
- Implement cost-efficient scaling strategies.  

---

## ✅ How to Use These Case Studies

- Read the scenario and implementation logic  
- Use Azure Portal or CLI for hands-on deployment  
- Modify and extend based on new features or services  
- Review pricing, security, and scalability considerations  

---

## 🛠️ Step-by-Step Guide for Case Study 1: Web App + Azure SQL + Blob Storage

<details>
  <summary>🔑 Click to see the solution</summary>

**Assumptions:**
- You have access to the Azure Student Portal with required permissions to create resources.
- You are familiar with basic .NET development and Visual Studio or VS Code.

**Steps:**
1. Go to [Azure Portal](https://portal.azure.com) and create a new **App Service**.
2. Choose a **.NET 6 runtime stack** and a region near you.
3. Create a new **Azure SQL Database**. Use the "Create new server" option for a fresh setup.
4. Enable "Allow Azure services to access this server" under SQL firewall settings.
5. Create a new **Storage Account**, add a **Blob container** named `profilepics`.
6. Deploy your .NET Web App using Visual Studio or Azure CLI (`az webapp up`).
7. Store connection strings for SQL and Blob in **App Service → Configuration → Application Settings**.
8. Use Azure SDK (NuGet: Azure.Storage.Blobs) in your app to upload images to Blob.
9. Save the Blob URI in your SQL DB with user profile details.
10. Enable **Application Insights** from the App Service panel for monitoring.

</details>

---

## 🛠️ Step-by-Step Guide for Case Study 2: Azure Functions + Queue + Blob

<details>
  <summary>🔑 Click to see the solution</summary>

**Assumptions:**
- You have basic knowledge of Azure Functions and Azure Storage.
- You’re using Visual Studio or VS Code with Azure Functions extension.

**Steps:**
1. Create an **Azure Storage Account** with two containers: `original-images`, `resized-images`.
2. Add a **Storage Queue** named `resize-queue`.
3. Create a **Queue Trigger Azure Function** using the template.
4. Bind the queue trigger and Blob input/output using `BlobTrigger` and `BlobOutput`.
5. In the function, use a library like ImageSharp to resize the image.
6. Upload the resized image to the `resized-images` container.
7. Deploy the function to Azure using Azure CLI or Visual Studio.
8. Upload an image to `original-images`, and push a message to `resize-queue`.
9. Enable **Application Insights** for logging and diagnostics.

</details>

---

## 🛠️ Step-by-Step Guide for Case Study 3: VM + SQL MI + Storage

<details>
  <summary>🔑 Click to see the solution</summary>

**Assumptions:**
- You are familiar with Windows Server and basic networking.
- You can use the Azure portal to create VMs and manage SQL.

**Steps:**
1. Create a **Windows VM**, select Windows Server 2022 image, and configure credentials.
2. Open port 80 in Networking settings for IIS.
3. RDP into the VM, install IIS, and deploy your legacy app.
4. Create a **SQL Managed Instance** in the same region and VNet.
5. Use **Data Migration Assistant** to migrate on-prem DB to Azure SQL MI.
6. Create a **Storage Account** and use **Azure Blob Storage** for automated backups.
7. Configure the VM to use private endpoints or VNet to access SQL MI securely.
8. Use **Azure Monitor** to collect logs and monitor the VM.

</details>

---

## 🛠️ Step-by-Step Guide for Case Study 4: Azure Functions + Key Vault

<details>
  <summary>🔑 Click to see the solution</summary>

**Assumptions:**
- You know how to work with Azure Functions and HTTP triggers.
- You are aware of security practices for secrets.

**Steps:**
1. Create a **Key Vault** and add your secret (API Key).
2. Create an **HTTP-triggered Azure Function** using Visual Studio or VS Code.
3. Assign a **System-assigned Managed Identity** to your Function.
4. Grant that identity **Key Vault Secret Get** permissions.
5. In your code, use Azure SDK (Azure.Identity + Azure.Security.KeyVault.Secrets) to retrieve the secret.
6. Implement payment processing logic using the secret.
7. Enable **Application Insights** for error tracking and performance.

</details>

---

## 🛠️ Step-by-Step Guide for Case Study 5: Scalable Web App + Monitor

<details>
  <summary>🔑 Click to see the solution</summary>

**Assumptions:**
- You are deploying a scalable web platform.
- You want to monitor and optimize performance.

**Steps:**
1. Create a **Standard App Service Plan** with autoscale enabled.
2. Host your web application in **App Service**.
3. Go to **Scale Out (App Service Plan)** and define rules (e.g., scale on 70% CPU).
4. Set up **Azure Monitor** to track CPU, Memory, Requests.
5. Create a **Dashboard** in Azure Monitor for real-time viewing.
6. Enable **Diagnostic Logs** from App Service settings for troubleshooting.
7. Add **Alerts** (e.g., high response time or CPU) for proactive notifications.

</details>

---
