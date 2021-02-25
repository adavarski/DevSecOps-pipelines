### docker-clair-scanner

This is a docker container for [clair-scanner](https://github.com/arminc/clair-scanner) ideal for integration into a DevSecOps pipelines.


#### Clair-scanner: docker containers vulnerability scan

When you work with containers (Docker) you are not only packaging your application but also part of the OS. It is crucial to know what kind of libraries might be vulnerable in your container. One way to find this information is to look at the Docker registry [Hub or Quay.io] security scan. This means your vulnerable image is already on the Docker registry.

What you want is a scan as a part of CI/CD pipeline that stops the Docker image push on vulnerabilities:

- Build and test your application
- Build the container
- Test the container for vulnerabilities
- Check the vulnerabilities against allowed ones, if everything is allowed then pass otherwise fail

This straightforward process is not that easy to achieve when using the services like Docker Hub or Quay.io. This is because they work asynchronously which makes it harder to do straightforward CI/CD pipeline.

Clair to the rescue

CoreOS has created an awesome container scan tool called [Clair](https://github.com/arminc/clair-scanner). Clair is also used by Quay.io. What clair does not have is a simple tool that scans your image and compares the vulnerabilities against a whitelist to see if they are approved or not.

This is where clair-scanner comes into place. The clair-scanner does the following:

- Scans an image against Clair server
- Compares the vulnerabilities against a whitelist
- Tells you if there are vulnerabilities that are not in the whitelist and fails
- If everything is fine it completes correctly



#### Build docker-clair-scanner
```
docker build -t davarski/docker-clair-scanner .
docker login 
docker push davarski/docker-clair-scanner 
```
#### Quick how-to
```
docker network create scanning
docker run -p 5432:5432 -d --net=scanning --name db arminc/clair-db:latest
docker run -p 6060:6060  --net=scanning --link db:postgres -d --name clair arminc/clair-local-scan:latest
docker run --net=scanning --rm --name=scanner --link=clair:clair -v '/var/run/docker.sock:/var/run/docker.sock'  davarski/docker-clair-scanner --clair="http://clair:6060" --ip="scanner" -t Medium <local-image-to-scan>
```
#### Example with generated json report and date formated
```
docker network create scanning
docker run -p 5432:5432 -d --net=scanning --name db arminc/clair-db:latest
docker run -p 6060:6060  --net=scanning --link db:postgres -d --name clair arminc/clair-local-scan:latest
docker run --net=scanning --name=scanner --link=clair:clair -v '/var/run/docker.sock:/var/run/docker.sock'  davarski/docker-clair-scanner --clair="http://clair:6060" --ip="scanner" -t Medium -r report.json <local-image-to-scan>
docker container cp scanner:report.json ./report.json
docker container rm scanner
```
#### Clean:
```
docker container stop db 
docker container stop clair 
docker container rm db 
docker container rm clair 
docker network rm scanning 
docker container prune -f 
docker image prune -f 
```
Example DevSecOps J.Pipeline: [Jenkinsfile](https://github.com/adavarski/docker-clair-scanner/blob/main/Jenkinsfile-example)
