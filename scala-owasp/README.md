Pre: Install sbt on jenkins-slave

CentOS Example:
```
curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo
sudo yum install sbt
```

DevSecOps J.Pipeline example: Jenkinsfile

Based on https://github.com/albuch/sbt-dependency-check
