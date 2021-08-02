# vls-workshop-practice
    I looked at the following areas:
       AWS beanstalk in depth:
          Setting AWS CLI
             curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
             unzip awscliv2.zip
             sudo ./aws/install
             aws --version
          Setting EB CLI
              pip install awsebcli --upgrade --user
              export PATH=~/.local/bin:$PATH
              source ~/.bash_profile
              eb --version
              
          Creating Two environemnts(beta environment and production environment.
              eb create (environment name)
              
          Looked how you can update environment from one solution stack to another.
          
              aws elasticbeanstalk list-available-solution-stacks(this command was not very helpful in my case, it displayed all the solutions stacks which was confusing)
              aws elasticbeanstalk describe-environments --application-name test --region eu-west-2 --profile vls-workshop( this will help show exactly whats your solution stack.)
              aws elasticbeanstalk update-environment --solution-stack-name "64bit Amazon Linux 2018.03 v2.16.5 running Docker 19.03.13-ce" --environment-name "beta-env" --region "eu-west-2" --profile vls-workshop( this command help downgrade to amazon linux).
              Challenge faced here was dockerfile could be built by amazon linux 2.
         eb upgrade environment-name     
              
          How to save configurations to be able to replicate them to other environments incase of DR 
              eb config save (environment name) --cfg (name-you-want-to-call-your-config)
          How to update your saved configurations.
              eb config put (name-of-the-saved-config-file-you-want-to-update)
          How to intergrate the elasticbeanstalk with codecommit.
              prerequisites:
                 install git.
                 If git is already there associated with another repo. type; rm -rf .git, then re-initialize
                 type eb init 
                 
          Sharedload balancer
              this one I never implemented but I understood it as a way of AWS helping customers utilise one ALB with multiple environments.
          Configuring your environments more using .ebextensions
             I realised beanstalk use simple scaling. I want to use target scaking whereby you set once and forget about it.Since it was not there I used an ebextension which would create that and disable alarms associated with beanstalk.
          Single docker applicatio deployment.
          Application deploynment and app path and logs(troubleshooting)
              - for amazon linux 2, app path = /var/app/current, logs = /var/log   very useful logs in troubleshooting = cfn-init logs and eb-engine logs
              - for amazon linux  , app path = /opt/python/ondeck logs = .var/log  very useful logs in troubleshooting  = cfn-init logs and eb-engine logs
 #Challenges Faced On beanstalk
    unable to update a saved configuration using the below command:
       eb config put prod.
    investigating further I found some case also stipulating the same. (https://github.com/aws/aws-elastic-beanstalk-cli/issues/32(bug)
 
     2. I went further and decided to set up a pipeline which would have 4 starges( source , build, manual approval the prod).In my practice wanted to understand other devops concept in AWS in this case dockerization in AWS.
        Lab:
          - Created a cluster group(
          - Created task definition( this defines how your containers will run in AWS)
          - I created service.This helps manage tasks.
            nb: think of tasks as containers.
          - Then I created a repository (elastic container registry)
          - docker login and pushed my image with the tag as the name of the repo.
          - Next step, I decided to create a pipeline. I started with first creating a build project and manually created a build to make sure that everything was working as expected.
          - I proceeded now to create a pipeline.
