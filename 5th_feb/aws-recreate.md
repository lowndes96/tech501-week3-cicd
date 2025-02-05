# Deploying a 2 teir arcitecture using AWS 

- [Deploying a 2 teir arcitecture using AWS](#deploying-a-2-teir-arcitecture-using-aws)
  - [task overview](#task-overview)
  - [Documentation of blockers](#documentation-of-blockers)
    - [creation of new ssh key for AWS](#creation-of-new-ssh-key-for-aws)
    - [Creation of database VM](#creation-of-database-vm)
    - [copy sparta app to vm:](#copy-sparta-app-to-vm)


## task overview
```
Reason for this task: Consolidation of what you've done, show how fast you can deploy the app using your scripts

    Use your scripts to deploy the database + app (with the reverse proxy working)
        Use VM size: t2.micro for both your VMs
        Use the default VPC
        Use the naming convention
    Post link to /posts page as soon as you get it working - once you get the thumbs up, you can stop the VMs when you are ready (i.e. before you go to lunch as normal)
    Document anything new you learnt to get the /posts page as quickly as possible, especially any blockers you had and how you overcame them
    Post link to documentation around COB
``` 
## Documentation of blockers
* had some issues that I believe were due to my version of node, will redo / troubleshoot further when I am able to 

### creation of new ssh key for AWS 
* used create key button
* downloaded from aws and stored in my local .ssh folder 
* Could also do via command line as with azure, but nice to have a built in option
```
scp -i ~/.ssh/tech501-emily-aws-key.pem -r nodejs20-sparta-test-app ubuntu@ec2-54-74-135-124.eu-west-1.compute.amazonaws.com:/home/ubuntu
```

### Creation of database VM 
settings as follows: 
* name as usual 
* Ubuntu 22.04 LTS
* t3.micro
* stick to defaults for virtual network and subnets (via edit button on side of box) 

* ended up changing the security groups after launching, as could not find them initially, however they were easy to edit from the instance main page under security 

### copy sparta app to vm: 

* ran into some errors here (add screenshots**)


app installing node
sudo DEBIAN_FRONTEND=noninteractive bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -" && \
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs