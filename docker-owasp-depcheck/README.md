### Simple script ideal for integration into a DevSecOps pipelines

#### OWASP Dependency-Check

OWASP dependency-check is a software composition analysis utility that detects publicly disclosed vulnerabilities in application dependencies.

#### OWASP Dependency-Check script for DevSecOps pipelines

Script is based on [Docker dependency-check image](https://hub.docker.com/r/owasp/dependency-check)

#### Usage

In the following example it is assumed that the source to be checked is in the current working directory. Persistent data and report directories are used, allowing you to destroy the container after running.

```
PROJECT_NAME=foo owasp-check.sh
```
#### DevSecOps J.Pipeline example: [Jenkinsfile](https://github.com/adavarski/owasp-docker-depcheck/blob/master/Jenkinsfile-PROJECT-OWASP)

