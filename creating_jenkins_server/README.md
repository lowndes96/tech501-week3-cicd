# Creating a jenkins server (17th feb)

Instructions: 
```
    DO NOT create an agent node (use the built-in node only)
        Your servers were set to spin up agent nodes to run the jobs because the whole group was using it
    Re-build the pipeline in your own Jenkins

Steps:

    Create new repo CICD-with-own-Jenkins-project for the documentation of this task
    Build your own Jenkins server
        Use Ubuntu 22.04 LTS
        Size:
            For Sparta test app using Node JS 20: Use t3.micro size
            For Java 17 app using a MySQL database e.g. the "World" API: use t3.small (since compiling this app requires more than 1 GB of memory)
        Launch it in your own VPC (1 subnet)
    Rebuild your Jenkins pipeline up to the deployment of the app
    Record a record 5-7min video:
        How to build Jenkins
        How to build environment
        How did you rebuild the pipeline
    Include your markdowns that you have made today in the new repo, and create a new markdown documenting how you have created Jenkins with the required environments. Make sure to include two diagrams:
        Jenkins pipeline diagram
        General diagram about the process
    Hand-in everything you've done around COB

``` 


* need to make a vcp with a single subnet 
* create a VM per the instructions above 
* do the update and install 
* `sudo apt install openjdk-11-jdk` 
* install latest versions of jenkins 
* open port 8080 
