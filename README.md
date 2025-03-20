# az204-0325-pm

### Pet Management Application
[Git Code](https://github.com/LinkedInLearning/building-a-web-application-on-microsoft-azure-4405955)

### Azure Devops
[Azure Devops](https://azure.microsoft.com/en-us/products/devops)
[My Azure DevOps Organizations](https://portal.azure.com/#view/AzureTfsExtension/OrganizationsTemplateBlade)

### To setup the project



#### Pushing the code from the local folder into the Azure Repo

>git init
 
>git status

>git config --global --list
 
if missing
 
>git config --global user.name "User Name"

>git config --global user.email "username@example.com"
 
>git remote -v

If origin is listed but points to the wrong URL, you can change it with:
 
>git remote add origin https://rswisdompetmanagement@dev.azure.com/rswisdompetmanagement/wpm/_git/wpm

>git push -u origin --all
 
No refs in common and none specified; doing nothing.
Perhaps you should specify a branch.
Everything up-to-date
 
>git branch

or

>git branch -r
 
if no branch found then will set the branch
 
>git branch --set-upstream-to=origin/main main

or

>git branch --set-upstream-to=origin/master master
 
>git checkout -b main

or

>git checkout -b master

>echo "# Initial commit" > README.md

>git add README.md
 
>git add .

>git commit -m "Initial commit"
 
>git push --set-upstream origin main

or

>git push --set-upstream origin master



### AZURE CLI

### Creating SQL Server

```
RESOURCE_GROUP="wpm"
SQL_SERVER="iyowpmsqlserver"
SQL_ADMIN="sqladmin"
SQL_PASSWORD="<your-password>"
DATABASE_NAME="wpm"
LOCATION="eastus"  # Change to your preferred region
```

```
az sql server create \
  --name $SQL_SERVER \
  --resource-group $RESOURCE_GROUP \
  --location $LOCATION \
  --admin-user $SQL_ADMIN \
  --admin-password $SQL_PASSWORD
```

```
az sql db create \
  --resource-group $RESOURCE_GROUP \
  --server $SQL_SERVER \
  --name $DATABASE_NAME \
  --service-objective S0  # Change the SKU if needed
```

```
az sql server firewall-rule create \
  --resource-group $RESOURCE_GROUP \
  --server $SQL_SERVER \
  --name AllowMyIP \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 255.255.255.255
```

### To delete all the resources in the Resource Group

```
az group delete --name wpm --yes --no-wait
```


### Option 1: Delete the Entire Resource Group (Recommended)

This will delete all resources inside the wpm resource group, including SQL Server, databases, virtual machines, storage accounts, etc.

```
sh
az group delete --name wpm --yes --no-wait
--yes: Confirms deletion without prompting.
--no-wait: Runs the command in the background (optional).
```
🔹 This is the fastest and simplest way to remove everything.

### Option 2: Delete All Resources One by One (If You Want to Keep the Resource Group)

If you want to keep the resource group but delete all resources inside it, use:

```
sh
az resource list --resource-group wpm --query "[].id" --output tsv | xargs az resource delete --ids
```

### Option 3: Delete Specific Resource Types (Optional)

If you only want to delete certain resources, use:

#### Delete SQL Server and All Databases

```
sh
az sql server delete --name iyowpmsqlserver --resource-group wpm --yes
```

#### Delete Virtual Machines

```
sh
az vm delete --name myVM --resource-group wpm --yes
```

#### Delete Storage Accounts

```
sh
az storage account delete --name mystorageaccount --resource-group wpm --yes
```