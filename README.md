

Medium-draft is a Medium like rich text editor built upon [draft-js](https://facebook.github.io/draft-js/) with an emphasis on eliminating mouse usage by adding relevant keyboard shortcuts.

[Documentation](https://github.com/brijeshb42/medium-draft/wiki) in progress.

This is a clone of https://github.com/brijeshb42/medium-draft with the following added CI Flow: 

When a version is pushed to GitHub -> Travis-CI runs three jobs [Test, Package as a Docker container and pushed to DockerHub, Deploy to AWS] -> Elastic beanstalk pulls package from DockerHub and deploys current version to a single Docker enabled EC2 instance. 


Here's a step by step instructions for running the whole process:  

1. Create an AWS user with programmatic access to Elastic beanstalk using the procedure in this article: https://medium.com/@andrew.bestbier/how-to-create-an-aws-user-for-a-ci-cd-service-to-use-when-deploying-to-elastic-beanstalk-a9dd0877fd6f
2. Use this guide to create an Elastic Beanstalk Application and Docker enabled environment to deploy the project into: https://medium.com/@andrew.bestbier/how-to-create-an-elastic-beanstalk-application-8431e7960bad.

Note that it's recommended to use at least a t2.micro instance which requires being a part of a VPC to run.  
3. Use this guide to create a Docker Hub repository: https://medium.com/@andrew.bestbier/how-to-create-a-docker-hub-repository-f07d1e0ddf5e?source=post_page-----4ee180222819----------------------
4. Clone the project 
5. Sign with your GitHub account into https://travis-ci.com/
6. Add a new project and choose 'settings' next to the medium-draft repository.  
7. Add the following environment variables: 
 - AWS_ACCESS_KEY_ID -> your access ID
 - AWS_SECRET_ACCESS_KEY -> your secret key
 - DOCKER_USER -> your Docker hub username
 - DOCKER_PASS -> password for your Docker hub
8. Edit the .travis.yml file in the project root and change the region, app, env, bucket_name and bucket_path with your relevant details as created in step 2, And the docker build and docker push with your Docker hub details from step 3.  
9. Edit Dockerrun.aws.json with your DockerHub details. 
10. Commit the changes and push to Github. If everything is ok, you should see your pipline runs and Medium-draft deployed to your Elastic Beantstalk environment. 

Good Luck! 