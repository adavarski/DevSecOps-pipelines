### Docker Bandit SAST (Static Application Security Testing) for python projects and DevSecOps pipelines


#### Bandit
Bandit: SAST (Static Application Security Testing) for python projects

#### Docker-Bandit

Simple Bandit docker image/container to run static security tests on python project in stand-alone mode, ideal for integration into a DevSecOps pipelines: 

#### Build
```
   docker build -t davarski/bandit -f Dockerfile .
   docker login
   docker push davarski/bandit
```

#### Use
```
    docker run -u root --rm -v YOUR_PYTHON_PROJECT_PATH:/app davarski/bandit bandit -r ./
    //help
    docker run -u root --rm -v YOUR_PYTHON_PROJECT_PATH:/app davarski/bandit bandit -h
```
#### Example DevSecOps J.Pipeline: [Jenkinsfile](https://github.com/adavarski/docker-bandit/blob/master/Jenkinsfile-SAST-Bandit-PYTHON_PROJECT-example)
