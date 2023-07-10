# Databases

**Description:**

The user is attempting to run a node web application which connects to a Postgresql database. The user wants to know how to to add the database to their project.

**Goals:**

- Modify the included config file to get a green job.
- Share link to green job.

**Help:**
<details>
  <summary>Spoiler warning</summary>

  * https://circleci.com/docs/2.0/postgres-config/
  * https://github.com/Animosity/CraftIRC/wiki/Complete-idiot's-introduction-to-yaml
  * https://circleci.com/docs/2.0/hello-world/#echo-hello-world-with-a-build-job

</details>
version: 2.1

jobs:
  build:
    docker:
      - image: cimg/base:2022.10
      - image: cimg/postgres:11.20
    steps:
      - checkout # check out the code in the project directory
      - run: echo "hello world" # run the `echo` command
      - run:
          name: install dockerize # This is a utility that will attempt to connect to a database, in place of an application for this sample.
          command: wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && sudo tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
          environment:
            DOCKERIZE_VERSION: v0.3.0
      - run:
          name: Wait for db # If no database is found in 1 minute the job will fail.
          command: dockerize -wait tcp://localhost:5432 -timeout 1m

workflows:
  build-workflow:
    jobs:
      - build
