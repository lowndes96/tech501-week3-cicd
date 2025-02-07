# CICD pipeline

- [CICD pipeline](#cicd-pipeline)
  - [Our pipline](#our-pipline)
    - [basic outline](#basic-outline)
    - [more detail](#more-detail)
  - [Why build a pipeline?](#why-build-a-pipeline)
  - [Why jenkins?](#why-jenkins)
- [Code along - using jenkins](#code-along---using-jenkins)
  - [Code along - creating a multi-stage pipeline](#code-along---creating-a-multi-stage-pipeline)
    - [setting up ssh key (move)](#setting-up-ssh-key-move)

## Our pipline 
### basic outline 
![basic pipeline detail](../images/our_cicd_pipeline.drawio.png)
### more detail 
![complex pipeline detail](../images/jenikins-cicd-pipeline.drawio.png)
## Why build a pipeline? 
* making devs life easier 
* quickly get changes to end users 
* reduce risk of big code changes messing up our code base 
* **business value** save time, saves money, users benefit quickly 

## Why jenkins? 
* free
* has powerful plugins 
* great to help understand the CICD pipeline 

# Code along - using jenkins 
1. aws instances - start servers (ramon will do every day we are using, we are now using much bigger servers than previously on azure)
2. Group split between server 1 (http://34.254.6.118:8080) and server 2 ( http://52.31.15.176:8080) 
    * I'm in group 1 
3. login, using stored login + pw 
4. add new item to create new pipeline
   * [jenkins-add-build](README.md)
5. build settings: 
   * under configure > general 
   * select to only store the most reacent 5 builds (can change depending on needs) 
   * ![alt text](code-along-images-am/disgard-old-builds.png)
6. add build step - execute shell 
   * ![alt text](code-along-images-am/build-shell-commands.png)
   * for this example we have run `uname -a` which displays the name of the operating system 
7. click ok 
8. build now 
   ![build-now-img](code-along-images-am/build-now.png)
9. check output 

## Code along - creating a multi-stage pipeline  
* can link jobs to create a muti-stage pipeline 

1. go to job 1 
2. configure > post build actions 

** add screenshots from this task 
### setting up ssh key (move)
ssh-keygen -t rsa -b 4096 -C myemail 
promted to add file name: emily-key-purpose
no passphrase, hit enter twice 
