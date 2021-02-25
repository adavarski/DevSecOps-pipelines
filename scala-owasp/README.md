### Pre: Install sbt on jenkins-slave

CentOS Example:
```
curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo
sudo yum install sbt
```

### DevSecOps J.Pipeline example: [Jenkinsfile](https://github.com/adavarski/DevSecOps-pipelines/blob/main/scala-owasp/Jenkinsfile-SCALA-PROJECT-example)

Based on [SBT Plugin for OWASP DependencyCheck](https://github.com/albuch/sbt-dependency-check) 
