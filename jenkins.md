# Jenins Setup

Start Jenkins

```bash
$  java -jar ~/apps/jenkins/jenkins.war
```

Go to http://localhost:8080

User / pass : admin/admin

## Install plugin

Manage Jenkins --> Manage Plugins

Install 'Docker pipeline'

Restart Jenkins

## Add Credentials

'Manage Jenkins' --> 'Manage Credentials' --> 'Jenkins'  --> 'Global'

Add user / pass for 
- Github
- and Dockerhub

## Create a Job

- Name : docker1-pipeline
- Type : pipeline
- Pipeline
    - Script from SCM
    - scm = git
    - repo url = https://github.com/sujee/jenkins-test
    - no github credentials needed as it is a public repo
    - branches to build : main  (not 'master')

## Build

Click on build now

inspect the logs

Verify built images by `docker images`.  Check the image-id

verify docker image at : https://hub.docker.com/repository/docker/sujee/jenkins-docker1

Check the tags and timeline

## Doing a push

- Update `webapp/index.html`
- Increment the version
- Commit and push it to github
- Build again
- Check dockerhub
- `run.sh` will launch new docker.  go to  http://localhost:8081  and check for version