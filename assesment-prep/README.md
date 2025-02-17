```
    Consultancy questions about: 
        how CI helps to be Agile  
        what types of organisations use DevOps practices  
        benefits for a business in using DevOps practices  
    Technical questions about: 
        what is Jenkins  
        alternatives to Jenkins  
        required dependencies for setting up own Jenkins server for testing  
        understand differences between CI and CD  
        benefits of CICD  
        disadvantages of running a single node vs multi node Jenkins server  
        best practice if a job fails  
        what is a Jenkins node  
        webhook  
            parts that need to be setup  
        CICD pipeline you setup for Sparta test app  
            what is needed to setup each job  
            what does each job do  
            how is it triggered  
            how was CI vs CD done in the pipeline  
            how to give Jenkins permissions to deploy the code to a cloud instance  
            how Jenkins will access the cloud instance - what port will be used and why  
            what does Jenkins do on the cloud instance in Job 3  
        best practices for creating jobs in Jenkins  
``` 
# consultancy Questions

## how CI helps to be Agile
* enables quick intergration of code changes 
* fast feeback on those changes 
* automated testing

## what types of organisations use DevOps practices
DevOps practices are used by many types of organizations, including those in technology, finance, healthcare, and manufacturing

## benefits for a business in using DevOps practices
* changes quickly make there way to the end user 
* no 'merge day' madness 
  

# Technical questions 

## what is Jenkins
* An open-source automation server that automates tasks related to building, testing, and deploying software
  
## alternatives to Jenkins
* CircleCI, Azure DevOps, GitHub Actions, Bitrise, travis, and TeamCity
  
## required dependencies for setting up own Jenkins server for testing


* need a test suite within our code 
* Prerequisites
  * A machine with: 256 MB of RAM, although more than 2 GB is recommended. 10 GB of drive space (for Jenkins and your Docker image)
  * The following software installed: Java 17 or 21. Docker (navigate to Get Docker site to access the Docker download that's suitable for your platform)

## what is a Jenkins node
* a node refers to any machine that is part of your Jenkins environment
* master node: central hub, mostly delegates 
* worker node: connects to master node and is used to run the jobs 
  
## disadvantages of running a single node vs multi node Jenkins server 
* multi node can have multipe jobs running concurrently 
* mulit node is scalable 
* multi node is more resiliant and fault tolerant - stops there being one point of failure 

## best practice if a job fails
* check logs to work out the cause of failure 
* have notifications set up on your jobs to the relavant parties 
* have an automated retry or recovery plan 

## webhook  
### parts that need to be setup 
* add webhook to a github repo 
* build trigger on jenkins is set to `github hook trigger for GITScm polling`

## CICD pipeline you setup for Sparta test app  
### what is needed to setup each job  
### what does each job do  
* job1: test changes
* job2: merge changes
* job 3: deploy changes
### how is it triggered  
* job 1 is triggered by a webhook 
* subsequent jobs are triggered via post build steps 
### how was CI vs CD done in the pipeline  
* CI: test, merge 
* CD: deploy app 
### how to give Jenkins permissions to deploy the code to a cloud instance 
* tick ssh agent under build environment 
* provide jenkins with the private key to ssh into our VM
### how Jenkins will access the cloud instance - what port will be used and why  
* port 8080  - default for web servers 
### what does Jenkins do on the cloud instance in Job 3
* updates or replaces app code with new code as tested by our jenkins server 