## Use SSH authentication with a repo on GitHub

- [tuesday learning (retitle, once clear)](#tuesday-learning-retitle-once-clear)
    - [Instructions:](#instructions)

## Instructions: 
```
Delete the key in the .ssh folder, on GitHub too, re-do everything done in the code along (see recording if needed). As you do...

    Document/explain the steps / commands you used
    Include a labelled/annotated diagram of what you've learn (Suggestion: draw your own)
    Use a new repo called tech501-ssh (or a new section in an existing repo)
    Suggestion: include some screenshots
    Timeframe: Send link to repo to all trainers by <insert time>

Reminders:

    Never put your SSH keys or the .ssh folder inside of a Git repo
    Make sure you are not in your .ssh folder for any other reason than to generate SSH keys or cat the contents of a public key
``` 

--- 

## Big steps: 
<br>

* generate ssh key pair using rsa 
* register the padlock (public key) on github 
* on LM register private key (new step!)
* create test repo on github 
* push changes to the repo 
--- 
## steps (code-along) 
1. generate ssh key pair using rsa: <br>
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` <br>
key name: `emily-github-key` <br>
passphrase: [leave empty] <br>

2. register the padlock (public key) on github 

settings > ssh + gtp keys 
add new 
comand line: cat emily-github-key.pub 
paste into box 

3. on LM register private key (new step!)

```
eval `ssh-agent -s`
``` 
should see: `Agent pid 56282`
```
ssh-add emily-github-key
``` 
should see: identity added 
<br>
check with: 
```
ssh -T git@github.com
``` 
then should see (screenshot 3.10)

1. create test repo 
with name: tech501-test-ssh 


5. push changes to the repo
screenshot 3.16 - change to ssh   <br>
git remote add origin git@github.com:lowndes96/tech501-test-ssh.git <br>

```
echo "# tech501-ssh" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:lowndes96/tech501-ssh.git
git push -u origin main
``` 