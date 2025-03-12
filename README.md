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
