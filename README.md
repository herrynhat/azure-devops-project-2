# Overview Of Udacity Azure Project 2

Hello, I am Nhat, this is project 2 has been created during the Nanodegree for DevOps Engineer using MS Azure on Udacity.

This project consists of flask application that is developed to predict housing prices in Boston (the model is already created by the instructor).
After planning the different steps regarding the deployment of a Python Flask Machine Learning app, we will manage to add GitHub Actions and Azure Pipeline to it to have a fully working CI/CD environment. 

This repositry demonstrate:
- Deploying the app in Azure CloudShell
- Deploying the app as a web server using Azure App Service.

If anything changed in it repository,  it will trigger the Github Action and also the Azure DevOps Pipelines to perform the CICD process and finally deploy to my app service.

## Badge

[![Python application test with Github Actions](https://github.com/herrynhat/azure-devops-project-2/actions/workflows/pythonapp.yml/badge.svg)](https://github.com/herrynhat/azure-devops-project-2/actions/workflows/pythonapp.yml)

## Project Plan
The planning tool I used are Trello Google Spreadsheets to keep track of the tasks and manage the project plan.

- [Trello](https://trello.com/b/YcFc1u1k/build-cicd-pipeline-for-azure-devops)

- [Spreadsheet](https://docs.google.com/spreadsheets/d/1DBxOIONEjgb9IKWU4g13gmGFElez7C8sp3p-by-qsBc/edit?usp=sharing)

## Instructions

Here is an architectural diagram:
Azure Cloud Shell

![Azure Cloud Shell](./Screenshot/azure-cloud-shell.png)

Azure CI

![Azure CI](./Screenshot/ci-diagram.png)

Azure CD

![Azure CD](./Screenshot/cd-diagram.png)

## Setup and Deploy the app in Azure Cloud Shell

In Azure Cloud Shell, clone the repo:
```
git clone git@github.com:herrynhat/azure-devops-project-2.git
```
![screenshot-gitClone-AzureCloud](./Screenshot/git_clone.png)

Change into the new directory:
```
cd azure-devops-project2.1
```

Change to branch "ci-to-git-action"

```
git checkout ci-to-git-action
```

Create a virtual environment:
```
python3 -m venv ~/.myrepo
```

Activate the virtual environment:
```
source ~/.myrepo/bin/activate
```

Install dependencies in the virtual environment and run tests:
```
make all
```

![make-all](./Screenshot/make_all.png)

Make change and test GitHub action
![screenshot-test-githubaAction](./Screenshot/test_git_action.png)


## Deploy the app to an Azure App Service

Create an App Service in Azure. 

Use this [file](./commands.sh) to create new App Services

```
az webapp up -n azure-devops-project2
```

Next, create the pipeline in Azure DevOps. The basic steps are:

- Go to [https://dev.azure.com](https://dev.azure.com) and sign in.
- Create a new private project.
- Create a new service connection to ARM, select subscription and the app service.
- Create a new pipeline linked to your GitHub repo using GiThub YAML File.

Screenshot of the App Service:

![My WebApp](./Screenshot/web_app.png)

Screenshot of Azure DevOps Project:

![My_DevOps](./Screenshot/my_devops.png)

To test the app running in Azure App Service, edit line 28 of the make_predict_azure_app.sh script with the DNS name of your app. Then run the script:
```
./make_predict_azure_app.sh 
```

If it's working you should see the following output:

![screenshot-prediction](./Screenshot/make_prediction.jpg)

You can also visit the URL of the App Service via the browser and you should see the following page:

![screenshot-browser](./Screenshot/app.png)

View the app logs:

To view the log in Cloud Shell
```
az webapp log tail -g Azuredevops -n azure-devops-project-2-nhat
```
![screenshot-log-webapp](./Screenshot/log_tail.png)

> 

## Load test

I use locust to perform load test on my local computer. 

Install locust:
```
pip install locust
```

Start load test:
```
locust -f locustfile.py --host https://azure-devops-project-2-nhat.azurewebsites.net/ --users 500 --spawn-rate 5 
```
Open a browser and go to [http://localhost:8089](http://localhost:8089) then click Start Swarming:

![screenshot-loadtest#1](./Screenshot/load_test1.png)
![screenshot-loadtest#2](./Screenshot/load_test2.png)
![screenshot-loadtest#3](./Screenshot/load_test3.png)
![screenshot-loadtest#4](./Screenshot/load_test4.png)

## Future Enhancements
- Creating a UI for making predictions.
- Adding test cases.
- Deploying my app with AKS.

## Demo 
Demo Video on Youtube 
[https://dev.azure.com](https://youtu.be/LM6cWs3EIXU)

