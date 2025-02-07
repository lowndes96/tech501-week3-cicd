# jenkins pipeline 

- [jenkins pipeline](#jenkins-pipeline)
- [task instructions:](#task-instructions)
  - [Job 1 set up](#job-1-set-up)
    - [setting up access to github via ssh keys](#setting-up-access-to-github-via-ssh-keys)
      - [in github](#in-github)
      - [in jenkins](#in-jenkins)
    - [setting up the webhook](#setting-up-the-webhook)
    - [dev branch set up](#dev-branch-set-up)
      - [on command line](#on-command-line)
      - [on jenkins](#on-jenkins)
    - [other jenkins set-up](#other-jenkins-set-up)
  - [Job 2 set up](#job-2-set-up)
    - [way 1: execute shell](#way-1-execute-shell)
      - [job 2 working](#job-2-working)
  - [Job 3 set up](#job-3-set-up)


# task instructions: 

```
Pre-requisites: You already have: 

    Job 1 <yourname>-job1-ci-test working 

Steps: 

    Get Job 2 working: 
        Name Job 2: similar to <yourname>-job2-ci-merge 
        Create a dev branch on your local git repo sparta-test-app-cicd 
        Make a change to dev branch and push the code to GitHub - the webhook needs to trigger the pipeline 
        If the tests pass on Job 1, Job 2 should run (and the code should merge from dev to main branch) 
    Get Job 3 working: 
        Name Job 3: similar to <yourname>-job3-cd-deploy 
        Copy the updated & tested code from Jenkins to the AWS EC2 instance 
        Jenkins will need to SSH into the EC2 instance to update the code & re-run the app 
        Each person will need to add the key/SSH credentials/pem file on Jenkins for Job 3 to access your EC2 instance (unless everyone is using the same key pair for their EC2 instances - in this case only one person needs to add the private key on Jenkins) 
        To copy the code from Jenkins to to EC2, use the scp or rsync commands from Jenkins 
            DO NOT: git clone from main branch and push to production 
        You will need an EC2 instance already running 
            Should use normal image you need to run the app. Examples: 
                For the Sparta test app using Node JS 20, you will need Ubuntu 22.04 LTS 
                For the Sparta test app using Node JS 12, you will need Ubuntu 18.04 LTS 
                For the Java 17 "World" API, you will need Ubuntu 22.04 LTS 
            Use normal SG rules, but allow Jenkin's IP to SSH in 
            Must have all dependencies installed to run your app 
    Document with: 
        important screenshots (especially homepage updated via CICD pipeline) 
        diagram to explain your CICD pipeline 
        paste link to documentation around COB 
``` 



## Job 1 set up 

### setting up access to github via ssh keys

#### in github
![alt text](jenkins-task-images/key-for-github.png)
* within the repository, go to settings and click on deploy keys
* add the public key created for this task into the repo
#### in jenkins 
* under source code management tick git
* add the repo 
![alt text](jenkins-task-images/add-jenkins-cedentiL.png)
* add private key here
![alt text](jenkins-task-images/creds-working.png)
### setting up the webhook 
![text](jenkins-task-images/github-add-webhook.png)
![alt text](jenkins-task-images/github-webhook-settings.png)
### dev branch set up 

#### on command line
![alt text](jenkins-task-images/dev-branch-added.png)
#### on jenkins
![alt text](jenkins-task-images/dev-branch-jenkins.png)
### other jenkins set-up 
* github project needs to jave the project https url, with a `/` at the end - jenkins is fussy!
![alt text](jenkins-task-images/link-repo-jenkins.png)
![alt text](jenkins-task-images/build-env.png)
![alt text](jenkins-task-images/build-steps.png)
![alt text](jenkins-task-images/build-trigger-job1.png)
![alt text](<jenkins-task-images/disgard old builds.png>)
## Job 2 set up 
### way 1: execute shell 
![alt text](jenkins-task-images/job2-buildenv.png)
* need to enable the ssh plugin 
![alt text](jenkins-task-images/job2-setup-git.png)
Build step (shell):
```
git checkout main
git pull origin main
git merge --ff-only origin/dev
git push origin main
``` 
#### job 2 working
![alt text](jenkins-task-images/job2-working.png)
## Job 3 set up 

Shell script: 
```
scp -o StrictHostKeyChecking=no -r /var/jenkins/workspace/emily-job1-ci-merge/app/ ubuntu@ec2-3-253-101-19.eu-west-1.compute.amazonaws.com:/home/ubuntu
ssh ubuntu@ec2-3-253-101-19.eu-west-1.compute.amazonaws.com << 'EOF'
  # Delete previous directory
  sudo rm -rf /repo/app
  # Move the app directory
  sudo mv /home/ubuntu/app /repo/app
  # Restart Nginx
  sudo systemctl restart nginx
  #move to app folder 
  cd /repo/app
  # start app
  npm install 
  sudo npm install pm2 -g 
  pm2 stop appjs
  pm2 start app.js 

EOF
``` 