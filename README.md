# Jenkins, Docker, Pipeline

* https://www.youtube.com/watch?v=38SAyBLSHUM&feature=youtu.be
* https://www.docker.com/sites/default/files/UseCase/RA_CI%20with%20Docker_08.25.2015.pdf
* https://jenkins.io/solutions/pipeline/
* https://jenkins.io/doc/book/pipeline/

## Run Jenkins

```
$ mkdir jenkins-data
$ docker run -p 8888:8080 -v $PWD/jenkins-data:/var/jenkins_home jenkinsci/blueocean:latest
$ open localhost:8888
```

## Setup a git repo

```
$ mkdir demo-app
$ cd demo-app
$ git init
...
```

## Add Jenkinsfile to demo-app

[Jenkinsfile](https://jenkins.io/doc/book/pipeline/jenkinsfile/)

```
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
```

## Importing file based git repo in Jenkins

Add new volume to the docker container

```
$ docker run -p 8888:8080 -v $PWD/jenkins-data:/var/jenkins_home -v $PWD/demo-app:/demo-app jenkinsci/blueocean:latest
```

Using in Jenkins: `file:///demo-app`