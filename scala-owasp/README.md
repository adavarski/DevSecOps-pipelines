### Pre: Install sbt on jenkins-slave

CentOS Example:
```
curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo
sudo yum install sbt
```
### build.sbt (SCALA-PROJECT-example)
```
dependencyCheckSuppressionFiles += (ThisBuild / baseDirectory).value / "project" / "owasp.xml"
dependencyCheckFormat := "ALL"
dependencyCheckAssemblyAnalyzerEnabled := Some(false)
```
### DevSecOps J.Pipeline example: [Jenkinsfile](https://github.com/adavarski/DevSecOps-pipelines/blob/main/scala-owasp/Jenkinsfile-SCALA-PROJECT-example)

Based on [DependencyCheck](https://github.com/jeremylong/DependencyCheck) & [SBT Plugin for OWASP DependencyCheck](https://github.com/albuch/sbt-dependency-check)
