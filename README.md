# Azure Function ETL with Pandas and CI/CD


This repository hosts a pair of Azure Functions designed for Extract, Transform, Load (ETL) operations:

    1. HTTP-triggered Function:
        Handles CSV file uploads from request body to the Blob 'in/input.csv' under container 'hvalfangstcontainer'.

    2. Blob-triggered Function:
        Listens for changes to aforementioned Blob 'in/input.csv' and responds by loading the CSV into a Pandas dataframe on changes.
        Conducts calculations to determine correlations between specific columns.
        Stores the resulting correlations in a dictionary and dumps said dictionary to JSON.
        It then proceeds to upload the JSON contents to the Blob 'out/statistics.json'.



A CI/CD pipeline has been implemented utilizing a GitHub Actions Workflow script,
which enabled automatic deployment to Azure Function App on repository pushes. Azure resources are provisioned with Terraform via shell scripts 'up' and 'down'.

## Requirements

* x86-64
* Linux/Unix
* [Python](https://www.python.org/downloads/)

## Creating resources

The shell script 'up' allocates Azure resources with Terraform.

## Deleting resources

The shell script 'down' deallocates Azure resources.

## Guide

### 1. Provision Azure Resources

- Run the 'up' script to provision Azure resources with Terraform.


### 2. Access Azure Portal

- Open your browser and navigate to the Azure Portal.


### 3. Function App Publish Profile

- Navigate to the newly created Function App 'hvalfangstlinuxfunctionapp'
- Click on 'Get publish profile' to download a file.
- The associated file contents will be used in the next step.

### 4. GitHub Repository Secrets

- Open the 'Settings' tab of your GitHub repository.
- Click on 'Actions' under 'Security' -> 'Secrets and variables'.
- Create the following repository secret:
    - PUBLISH_PROFILE: Copy value from downloaded file obtained in step #3

### 5. Deploy Workflow

Our Azure Function will be deployed on repository pushes by utilizing a GitHub Actions workflow script.