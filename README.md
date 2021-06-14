# struts-rest-showcase

[Struts Rest Showcase Application source code](https://archive.apache.org/dist/struts/2.3.20/ ) packaged in version 2.3.20 

Exploit from
* https://techblog.mediaservice.net/2017/09/detection-payload-for-the-new-struts-rest-vulnerability-cve-2017-9805/
* https://www.exploit-db.com/exploits/42627

## Setup for Intellij
* Download IntelliJ community
* Import from VCS
* File > Project Structure > Project SDK > JDK 1.8
    * Install JDK 8 if it does not exist
* View > Maven > Toggle 'Skip Tests' Mode & Run Maven Build

### Dockerfile Run & exploit
```
git clone https://github.com/samqbush/struts-rest-showcase.git && cd ./struts2-rest-showcase
docker build -t struts2-rest-showcase:latest ./
docker run --name struts2-rest-showcase -d -p 8361:8080 struts2-rest-showcase:latest
```
### Access to the [WebUI](http://localhost:8361/struts2-rest-showcase/orders)

### Exploit from outside the container on linux
```
apt update && apt install -y python3-pip
cd ./Exploit CVE-2017-9805
python3 restshowcasedetect.py http://localhost:8361/struts2-rest-showcase/orders/3
```
* You should see a 10 second delay in response before receiving a 500 error.
