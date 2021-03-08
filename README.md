# vls-workshop-practice
    I looked at the following areas:
       AWS beanstalk in depth:
          Setting EB CLI
          Creating Two environemnts(beta environment and production environment.
          Looked how you can update environment from one solution stack to another.
          How to save configurations to be able to replicate them to other environments incase of DR 
          How to update your saved configurations.
          How to intergrate the elasticbeanstalk with codecommit.
          Sharedload balancer
          Configuring your environments more using .ebextensions
          Various eb config commands using eb cli.
          Single docker applicatio deployment.
          Application depoloynment and app path and logs(troubleshooting)
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
