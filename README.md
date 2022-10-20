# taroko_quiz

## Docker

### Q1 What is a Docker image?

### My Answer: 

An image is a file with instructions for creating a Docker container. 
We can build our own image base on someone's image.
For example, We can build an image base on "ubuntu" image and install nginx web server, filebeat and the other application if we want, but some application need the configuration settings to run normally.


### Q2 What does this command do?
#### docker run --rm -it taroko/app /bin/bash

### My Answer: 

Use the image "taroko/app" to run the container and enter to bash mode. Let user to interactive with the container. When exit the container, it will remove the container

### Q3 How to speed up the build time and reduce the size of a docker image?

### My Answer: 

1. Move forward the commands that change infrequently to increase cache usage.
2. Use miniaml base images.
3. Use multistage builds.
4. Minimize the number of layers
5. Use dockerignore

### Q4 Please describe the following docker-compose.yml, step by step:

### My Answer:

We have three services defined and all three services behave almost the same.

The differences between each other are the image name, args be passed into $TARGET, ports number.

If image doesn't exist, it will create three images with different name but base on same Dockerfile and running three containers with ports 8080~8082:8000

Basically, they point to the same Dockerfile that defined in "context: ." , same default network setting and the same target "build-env" in Dockerfile.

#### By the way, indent in auth service (args) seems to be wrong.





## GitHub Actions
### Q5 Please describe the following

### My Answer:

Define the name of this workflow CI - Unit test

Define the concurrency, it means it will ensure only a single job or workflow run at a time on the same concurrency group.

When pull_request happens on any branch, it will trigger this workflow.

A job called test that runs on ubuntu and then runs two containers, one for postgres and one for redis.

First step is use actions/checkout@v3 to put the github repository code to ubuntu environment so we can let this workflow to use.

Then we install ruby with version 2.7.3 and libpq-dev for postgresql
and bundler installed to solve dependencies problem.

Then we setup database , copy yml for database and create database depends on env (RAILS_ENV: test) and initialize the database and install all dependencies through yarn install and precomplie the code to produce the things needed by website

We have some env variables defined so we can change easily if we have different settings on postgres's database,username and password.
Also, the env variables setting can avoid the hardcode in many files.

Finally, use Rspec run the tests to check everything works or not and skip looking for "spec/features/*" in spec directory
