# DevOpsTry
## Project Title
Assignment to create a automation system for connecting developer team, testing team and production team.

### Getting Started



#### Prerequisites

For doing this project you need to have yum configured for RHEL8 and install and configure docker and jenkins.
Developer team need to have git in their system.


### Steps
#### Getting started with developer end.

First need to create a GitHub repo for centalised source code management.
Then developer can clone the  repo to his local directory.
```
git clone <url of git repo>

```

Now copy his website html files to the folder and do a commit

```
until finished
```
and to first push to origin from master branch.
```
until finished
```
Now, for further changes and testing, developer can create branches, modify/add code, do commits!
```
until finished
```
Create a hook, for automation. Automate push after each commit.
```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

### Running the tests 
For doing tests on the developer modified code we , need to send it to the testing environment.These environments will be created using docker images. And we will automate this sending data from github developers branch to testing environment using Jenkins.

* 3 jobs

  * Job1--> monitor the dev branch, when ever there is change, deploy it to testing docker environment.And after succesfull test, trigger Job3(Right now we dont have any tests, will add in future).
  
  * Job2-->monitor the master branch, when ever there is changes, deploy it to production environment for client.
  
  * Job3-->Merge dev and master brnach, after successfull test ,hence modifying master and thus triggering job2 again.

#### Setting up jenkins and creating the Jobs/tasks.

Currently we havent created the testing part, so it will be a manual check that if the site is working or not.

* configuring the jobs
  * Job1
    * SCM : use git
    * trigger : PollSCM
    * Build : Execute shell
      ```
       sudo cp -rvf * /websitepro

       if sudo docker ps -a | grep master
       then
       echo "Already Running"
       else
       sudo docker run -dit 8081:80 --name production -v /WebsitePro:/usr/local/apache2/htdocs/httpd
       fi
      ```
  * Job1
    * SCM : use git
    * trigger : PollSCM
    * Build : Execute shell
      ```
       sudo cp -rvf * /websiteTest

       if sudo docker ps -a | grep dev1
       then
       echo "Already Running"
       else
       sudo docker run -dit 8081:80 --name production -v /WebsiteTest:/usr/local/apache2/htdocs/httpd
       fi
      ```   
  * Job3
    * SCM:git
    * Additional Behaviors :Merge Before build Dev and Master using fast-forward mode.
    * trigger: Build after other projects are built( here job1s successfull build )
    * Post build action: Push to Master branch after succesful build.
    
    

#### 

Explain what these tests test and why

```
Give an example
```

### Deployment

Add additional notes about how to deploy this on a live system.

### Final Thanks
  To Vimal Daga sir, for explaining things so well and imparting us with knowledge and for imparting us with the thirst and interest to learn DevOps concepts.

